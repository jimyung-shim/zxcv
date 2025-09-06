# ✅ 내비게이션 타입 강화 (Props 적용)

`react-navigation`의 `NativeStackScreenProps` / `BottomTabScreenProps`를 적용하여 각 Screen 컴포넌트의 Props 타입을 강화합니다.

---

## 1) `types.ts`에 전체 네비게이션 타입 정의 확장
```ts
import type { NavigatorScreenParams } from '@react-navigation/native';

export type AuthStackParamList = {
  Login: undefined;
  Signup: undefined;
};

export type AppTabParamList = {
  HomeTab: undefined;
  ChatTab: undefined;
  ReserveTab: undefined;
  MypageTab: undefined;
};

export type AppStackParamList = {
  Tabs: NavigatorScreenParams<AppTabParamList> | undefined;
  PersonaSelect: undefined;
};

export type RootStackParamList = {
  Auth: NavigatorScreenParams<AuthStackParamList>;
  App: NavigatorScreenParams<AppStackParamList>;
};
```

---

## 2) 각 Screen에 Props 타입 적용

### `LoginScreen.tsx`
```tsx
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { AuthStackParamList } from '../../navigation/types';

type Props = NativeStackScreenProps<AuthStackParamList, 'Login'>;

export default function LoginScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `SignupScreen.tsx`
```tsx
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { AuthStackParamList } from '../../navigation/types';

type Props = NativeStackScreenProps<AuthStackParamList, 'Signup'>;

export default function SignupScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `MyPageScreen.tsx`
```tsx
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { AppTabParamList } from '../../navigation/types';

type Props = NativeStackScreenProps<AppTabParamList, 'MypageTab'>;

export default function MyPageScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `HomeScreen.tsx`
```tsx
import type { BottomTabScreenProps } from '@react-navigation/bottom-tabs';
import type { AppTabParamList } from '../../navigation/types';

type Props = BottomTabScreenProps<AppTabParamList, 'HomeTab'>;

export default function HomeScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `ChatScreen.tsx`
```tsx
import type { BottomTabScreenProps } from '@react-navigation/bottom-tabs';
import type { AppTabParamList } from '../../navigation/types';

type Props = BottomTabScreenProps<AppTabParamList, 'ChatTab'>;

export default function ChatScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `ReservationScreen.tsx`
```tsx
import type { BottomTabScreenProps } from '@react-navigation/bottom-tabs';
import type { AppTabParamList } from '../../navigation/types';

type Props = BottomTabScreenProps<AppTabParamList, 'ReserveTab'>;

export default function ReservationScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

### `PersonaSelectScreen.tsx`
```tsx
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { AppStackParamList } from '../../navigation/types';

type Props = NativeStackScreenProps<AppStackParamList, 'PersonaSelect'>;

export default function PersonaSelectScreen({ navigation }: Props) {
  // ... 기존 코드 동일
}
```

---

## 3) 기대 효과
- 네비게이션 시 라우트 이름 오타, 잘못된 Params 전달 등을 **빌드 타임에 체크**할 수 있음
- IDE 자동완성 지원으로 생산성 증가
- 팀 협업 시 API 계약(라우트/파라미터)을 안전하게 공유 가능


---

## 4) 스크린 `Props` 타입 강화 가이드 (Stack/Tab 안전 네비게이션)
아래 패치를 적용하면 각 스크린에서 `navigation`, `route`가 **완전 타입 안전**해집니다. 탭 안에 있는 스크린이 스택 라우트(예: `PersonaSelect`)로 이동해야 할 때는 `CompositeScreenProps`를 씁니다.

### 4.1 `navigation/types.ts`에 헬퍼 타입 추가
```ts
// app/src/navigation/types.ts
import type { NavigatorScreenParams } from '@react-navigation/native';
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { BottomTabScreenProps } from '@react-navigation/bottom-tabs';
import type { CompositeScreenProps } from '@react-navigation/native';

export type AuthStackParamList = {
  Login: undefined;
  Signup: undefined;
};

export type AppTabParamList = {
  HomeTab: undefined;
  ChatTab: undefined;
  ReserveTab: undefined;
  MypageTab: undefined;
};

export type AppStackParamList = {
  Tabs: NavigatorScreenParams<AppTabParamList> | undefined;
  PersonaSelect: undefined;
};

// ★ 스크린별 편의 타입(alias)
export type AuthStackScreenProps<T extends keyof AuthStackParamList> =
  NativeStackScreenProps<AuthStackParamList, T>;

export type AppStackScreenProps<T extends keyof AppStackParamList> =
  NativeStackScreenProps<AppStackParamList, T>;

export type AppTabScreenProps<T extends keyof AppTabParamList> =
  BottomTabScreenProps<AppTabParamList, T>;

// ★ 탭 스크린이 상위 스택으로도 내비게이션 해야 할 때(예: PersonaSelect로 이동)
export type TabInStackProps<TTab extends keyof AppTabParamList> = CompositeScreenProps<
  BottomTabScreenProps<AppTabParamList, TTab>,
  NativeStackScreenProps<AppStackParamList>
>;
```

---

### 4.2 각 스크린에 타입 적용 예시/패치

#### HomeScreen (Tabs 안에 있고, 스택의 `PersonaSelect`로 이동 가능)
```tsx
// app/src/screens/home/HomeScreen.tsx
import React, { useEffect } from 'react';
import { View, Text, StyleSheet, Image } from 'react-native';
import ScreenContainer from '../../components/ScreenContainer';
import { usePersona } from '../../stores/personaStore';
import { colors } from '../../theme/colors';
import type { TabInStackProps } from '../../navigation/types';

type Props = TabInStackProps<'HomeTab'>;

export default function HomeScreen({ navigation }: Props) {
  const { personaLabel, imageUrl, reason } = usePersona();

  useEffect(() => {
    if (!imageUrl) {
      navigation.navigate('PersonaSelect');
    }
  }, [imageUrl, navigation]);

  // ... 이하 동일
}
```

#### MyPageScreen (Tabs 안)
```tsx
// app/src/screens/account/MyPageScreen.tsx
import type { TabInStackProps } from '../../navigation/types';

type Props = TabInStackProps<'MypageTab'>;

export default function MyPageScreen({ navigation }: Props) {
  // navigation.navigate('PersonaSelect') 등 상위 스택 라우트도 타입 안전
  // ... 기존 로직 유지
}
```

#### ChatScreen / ReservationScreen (Tabs 안)
```tsx
// app/src/screens/chat/ChatScreen.tsx
import type { AppTabScreenProps } from '../../navigation/types';

type Props = AppTabScreenProps<'ChatTab'>;
export default function ChatScreen({}: Props) {
  // route, navigation 타입 안전
  // ... 기존 로직 유지
}
```
```tsx
// app/src/screens/reservation/ReservationScreen.tsx
import type { AppTabScreenProps } from '../../navigation/types';

type Props = AppTabScreenProps<'ReserveTab'>;
export default function ReservationScreen({}: Props) {
  // ... 기존 로직 유지
}
```

#### PersonaSelectScreen (AppStack에 속함)
```tsx
// app/src/screens/persona/PersonaSelectScreen.tsx
import type { AppStackScreenProps } from '../../navigation/types';

type Props = AppStackScreenProps<'PersonaSelect'>;

export default function PersonaSelectScreen({ navigation }: Props) {
  // 완료 후 navigation.navigate('Tabs') 등 타입 안전
  // ... 기존 로직 유지
}
```

#### LoginScreen / SignupScreen (AuthStack에 속함)
```tsx
// app/src/screens/auth/LoginScreen.tsx
import type { AuthStackScreenProps } from '../../navigation/types';

type Props = AuthStackScreenProps<'Login'>;
export default function LoginScreen({ navigation }: Props) {
  // navigation.navigate('Signup') 타입 안전
  // ... RHF 로직 유지
}
```
```tsx
// app/src/screens/auth/SignupScreen.tsx
import type { AuthStackScreenProps } from '../../navigation/types';

type Props = AuthStackScreenProps<'Signup'>;
export default function SignupScreen({ navigation }: Props) {
  // navigation.replace('Login') 타입 안전
  // ... RHF 로직 유지
}
```

---

### 4.3 `useNavigation` 훅을 반드시 타입으로 쓰고 싶다면 (선택)
컴포넌트 깊숙한 곳에서 `useNavigation`만 쓰는 경우 아래처럼 명시 타입을 부여할 수 있습니다.
```ts
import { useNavigation } from '@react-navigation/native';
import type { CompositeNavigationProp } from '@react-navigation/native';
import type { BottomTabNavigationProp } from '@react-navigation/bottom-tabs';
import type { NativeStackNavigationProp } from '@react-navigation/native-stack';
import type { AppTabParamList, AppStackParamList } from '../../navigation/types';

type Nav = CompositeNavigationProp<
  BottomTabNavigationProp<AppTabParamList, 'HomeTab'>,
  NativeStackNavigationProp<AppStackParamList>
>;

const navigation = useNavigation<Nav>();
```

---

### 4.4 체크리스트
- [ ] 각 스크린 파일 상단에 **맞는 Props 타입**을 선언했는가?
- [ ] 탭 스크린에서 **스택 라우트로 이동**이 필요한 경우 `TabInStackProps`를 썼는가?
- [ ] 새 파일/타입을 export하여 다른 스크린에서 import 가능한가?
- [ ] 라우트 이름이 `types.ts`와 실제 등록된 네비게이터의 키와 **일치**하는가?

적용 중 충돌 나는 부분 있으면 알려주세요. 빠르게 맞춰 드릴게요.
