# 업스트림과 배포 기준

이 포크는 `@jeongshin/react-native-animated-rolling-numbers`로 배포해요.

- 업스트림: https://github.com/BouarourMohammed/react-native-animated-rolling-numbers
- 소유 저장소: https://github.com/jeongshin/react-native-animated-rolling-numbers
- 앱이 쓰는 배포본: `2.0.1`, npm gitHead `747cec8a8ffa59962bcc9fc5a3e87cc1c4fa3703`예요.
- 이번 후보: `2.0.2`예요. FE가 적용하던 AnimatedDigit의 useAnimatedStyle 의존성 배열 제거를 src로 옮겨 생성된 lib에 포함해요.
- 검증 개발 조합은 RN0.88.1·React19.3.0·Reanimated4.7.1·Worklets0.13.1이에요. 공개 props/API와 peer 최소 범위는 유지해요.

## 변경을 반영할 때

업스트림 변경은 별도 브랜치에서 비교하고 적용해요. `yarn build`로 lib를 다시 만들고 `yarn pack` 결과에 수정된 AnimatedDigit이 들어가는지 확인해요. lib는 직접 수정하지 않아요.

TypeScript의 ESM 출력을 유지해요. CommonJS 출력은 scheduleOnRN 호출을 모듈 객체의 멤버 접근으로 바꿔 worklet closure가 NativeWorklets 모듈 전체를 캡처할 수 있어요. 앱에서 Worklets Babel 변환과 실제 숫자 애니메이션을 검증해요.

## 발행 게이트

이 저장소에는 발행 workflow가 없고 build 후 scoped npm package를 수동으로 발행해요. 소유자의 권한 경로와 발행 지시를 확인한 뒤 배포해요. 이번 호환성 작업에서 npm publish나 릴리스 태그 push는 실행하지 않아요. 새 버전 발행과 앱 검증이 완료되면 FE manifest의 yarn patch를 제거하고 새 exact 버전을 사용해요.
