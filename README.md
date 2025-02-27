## 과제 체크포인트

### 기본과제

- [x] shallowEquals 구현 완료
- [x] deepEquals 구현 완료
- [x] memo 구현 완료
- [x] deepMemo 구현 완료
- [x] useRef 구현 완료
- [x] useMemo 구현 완료
- [x] useDeepMemo 구현 완료
- [x] useCallback 구현 완료

### 심화 과제

- [x] 기본과제에서 작성한 hook을 이용하여 렌더링 최적화를 진행하였다.
- [x] Context 코드를 개선하여 렌더링을 최소화하였다.

## 과제 셀프회고

<!-- 과제에 대한 회고를 작성해주세요 -->

리액트의 기본 훅을 직접 구현하며 훅의 내부동작과 장점이 무엇인지 어떻게 사용해야하는지 알게되었다. 이전에 사용할 때는 주의점이나 올바른 활용방법을 충분히 알지 못한 채 사용했었지만, 이번 과제를 통해 기본 훅과 커스텀 훅에 대해 알게되었고, 설계 방향성을 고민해보는 시간이 되었다! 앞으로 기본적인 훅과 커스텀 훅을 활용하여 효율적인 코드를 작성할 수 있을 것 같다.

### 기술적 성장

<!-- 예시
- 새로 학습한 개념
- 기존 지식의 재발견/심화
- 구현 과정에서의 기술적 도전과 해결
-->

훅에 대한 개념이 부족하다 생각해 기본 훅에 대해 집중적으로 학습했다. 그리고 사실 학습자료와 같은 내용이지만 한번 더 정리해보았다..ㅎ

React Hooks는?
함수형 컴포넌트에서 상태와 생명주기 기능을 사용할 수 있게 해주는 함수들.

- 함수형 컴포넌트에서 상태 관리 기능
- 생명주기 메서드 대체
- 로직의 재사용성 향상
- 관심사의 분리를 통한 코드 구조화 <br/>
  ⇒ 따라서 복잡한 로직을 가진 컴포넌트도 구조화하고 관리할 수 있다!

~~(개념도 모르고 쓰라길래 여기저기 사용하던)~~ useState와 useEffect의 개념과 주의할 점은 다음과 같다.

- **useState**

  함수형 컴포넌트에서 상태를 관리할 수 있게 해준다.

  - 컴포넌트에 지역 상태를 추가할 수 있음
  - 함수형 컴포넌트를 다시 렌더링하여 상태를 업데이트함
  - 배열 구조 분해를 통해 현재 상태값과 상태를 업데이트하는 함수를 제공

  주의할 점으로는

  - 상태 업데이트는 비동기적 (정확히는 스냅샷)
  - 객체나 배열을 상태로 사용할 때는 항상 새로운 참조를 생성
  - 복잡한 상태 로직의 경우 useReducer를 고려할 수 있음

- **useEffect**

  데이터 가져오기, 구독 설정, 수동으로 DOM 조작하기 등 컴포넌트의 주요 렌더링 작업 외의 작업들

  - 컴포넌트가 렌더링 된 후 실행
  - 기본적으로 모든 렌더링 이후에 실행, but 최적화를 통해 특정 값들이 변경되었을 때만 실행되도록 설정할 수 있음

  주의할 점으로는

  - 의존성 배열을 올바르게 설정, 빈 매열은 컴포넌트 마운트 시에만 실행됨을 의미
  - 정리함수를 반환하여 필요한 정리 작업을 수행
  - 무한 루프를 방지하기 위해 의존성 배열을 신중히 설정
  - 비동기 작업 수행 시 경쟁 상태를 주의
    <br/>
    ⇒ 함수형 컴포넌트에서 생명주기와 관련된 작업을 수행할 수 있게 해주는 강력한 도구

<h3>직접 구현해본 useRef, useMemo, useCallback의 개념과 주의할 점은 다음과 같다.</h3>

- **useRef**

  렌더링에 필요하지 않은 변경 가능한 값을 저장하는데 사용되는 Hook

  - 반환된 ref 객체는 컴포넌트의 전체 생명주기 동안 유지
  - ref 객체의 .current 속성을 변경해도 리렌더링이 트리거되지 않음
  - DOM 요소에 접근하거나 이전 상태를 저장하는 등 다양한 용도로 사용될 수 있음

  주의할 점으로는

  - ref의 .current 속성 변경은 리렌더링을 트리거하지 않음
    <br/>따라서, 렌더링과 관련된 값을 저장하는 데는 적합하지 않음
  - useRef로 생성된 ref 객체는 컴포넌트가 언마운트될 때까지 유지
    <br/>이는 메모리 누수를 일으킬 수 있으므로 필요하지 않은 경우 정리
  - DOM 조작을 직접 수행할 때는 React의 선언적 패러다임을 벗어나므로 주의해서 사용해야 함

- **useMemo**

  계산 비용이 큰 함수의 결과값을 **메모이제이션**하는 Hook

  - 의존성 배열의 값이 변경되지 않는 한, 이전에 계산된 값을 재사용
  - 렌더링 중에 실행되는 비용이 큰 계산을 최적화하는 데 유용
  - 값뿐만 아니라 객체나 배열도 메모이제이션할 수 있음

  주의할 점으로는

  - 모든 값에 useMemo를 사용하는 것은 메모리 사용량을 증가시키고 초기 렌더링 성능을 저하시킬 수 있음
  - 의존성 배열을 올바르게 설정해야 함<br/>
    잘못된 의존성은 최신 값을 사용하지 못하는 버그를 유발할 수 있음
  - 성능 최적화를 위한 도구, 의미론적 보장을 위해 사용X

- **useCallback**

  **메모이제이션**된 콜백 함수를 반환하는 Hook

  - 의존성 배열이 변경되지 않는 한, 동일한 함수 참조를 유지함
  - 주로 자식 컴포넌트에 콜백을 전달할 때 사용
  - React.memo와 함께 사용하여 컴포넌트의 불필요한 리렌더링 방지

  주의할 점으로는

  - 모든 함수에 useCallback을 사용하는 것은 오히려 성능 저하, 필요한 경우에만 사용
  - 의존성 배열을 올바르게 설정, 잘못된 의존성은 버그를 유발
  - 자식 컴포넌트에 함수를 prop으로 전달할 때 유용

### 코드 품질

<!-- 예시
- 특히 만족스러운 구현
- 리팩토링이 필요한 부분
- 코드 설계 관련 고민과 결정
-->

App.tsx는 관심사가 모두 모여있는 구조로 리팩토링이 필요할 것 같다. 현재 과제에서의 테스트 코드를 통과하는 포인트는 아니었지만 나중에 시간을 내서 관심사 분리와 컴포넌트 계층화 작업을 진행해야겠다는 목표를 세우게 되었다. ~~(설날, 쉬는 주차 Chapter1에 대해 전체적으로 리팩토링을 진행해보아야겠다)~~

### 학습 효과 분석

<!-- 예시
- 가장 큰 배움이 있었던 부분
- 추가 학습이 필요한 영역
- 실무 적용 가능성
-->

과제에서 나오지 않은 기본 React Hooks들도 당!연!히! 살펴볼 필요가 있다고 느꼈다.

훅의 개념을 이해하는 데 시간이 오래 걸려 리팩토링을 진행하지 못한 점은 아쉬웠지만, 이번 과제를 통해 React가 왜 프레임워크의 대세가 되었는지, 그리고 그 장점이 무엇인지 깊이 알아가는 시간이었다. 단순히 사용만 했던 과거와 비교해 이제는 React의 원리와 효율성에 대해 더 명확히 이해하게 되어 의미 있는 성장이었다!

### 과제 피드백

<!-- 예시
- 과제에서 모호하거나 애매했던 부분
- 과제에서 좋았던 부분
-->

훅을 직접 구현하고, 이를 활용하여 성능 최적화를 진행하며 기본과 심화 과제가 자연스럽게 연결되어있어 해결하고 이해하기 수월했다. 특히, 리액트의 내장 훅과 내가 직접 구현한 코드를 비교하며, 리액트가 제공하는 기본 훅들의 장점을 알았지만 동시에 이러한 훅들을 커스텀 훅으로도 충분히 구현하고 활용해볼 수 있겠다는 생각이 들었다.

그리고 조금 스스로 조금 아쉬운 점은 타입스크립트에 대한 이해도였다.. 이렇게 느낀 이유는 as T 와 같은 방식을 사용하여 해결했다는 점에서 타입스크립트를 보다 깊이 이해하고 활용하지 못해 아쉬웠다. 왜 특정 타입이 그렇게 결정되는 것인지 null로 들어올 수 있는 가능성에 대한 처리가 왜 필요한지를 명확히 이해하지 못하였다. 타입스크립트의 타입을 결정하는 시스템은 강력한 도구이지만, 그만큼 활용하고 충분히 이해하지 못해 아쉽고, 안정적이고 예측 가능한 코드를 작성할 수 있도록 노력해야겠다.

## 리뷰 받고 싶은 내용

<!--
피드백 받고 싶은 내용을 구체적으로 남겨주세요
모호한 요청은 피드백을 남기기 어렵습니다.

참고링크: https://chatgpt.com/share/675b6129-515c-8001-ba72-39d0fa4c7b62

모호한 요청의 예시)
- 코드 스타일에 대한 피드백 부탁드립니다.
- 코드 구조에 대한 피드백 부탁드립니다.
- 개념적인 오류에 대한 피드백 부탁드립니다.
- 추가 구현이 필요한 부분에 대한 피드백 부탁드립니다.

구체적인 요청의 예시)
- 현재 함수와 변수명을 보면 직관성이 떨어지는 것 같습니다. 함수와 변수를 더 명확하게 이름 지을 수 있는 방법에 대해 조언해주실 수 있나요?
- 현재 파일 단위로 코드가 분리되어 있지만, 모듈화나 계층화가 부족한 것 같습니다. 어떤 기준으로 클래스를 분리하거나 모듈화를 진행하면 유지보수에 도움이 될까요?
- MVC 패턴을 따르려고 했는데, 제가 구현한 구조가 MVC 원칙에 맞게 잘 구성되었는지 검토해주시고, 보완할 부분을 제안해주실 수 있을까요?
- 컴포넌트 간의 의존성이 높아져서 테스트하기 어려운 상황입니다. 의존성을 낮추고 테스트 가능성을 높이는 구조 개선 방안이 있을까요?
-->

```typescript
...useMemo.ts 중

  // 2. 현재 의존성과 이전 의존성 비교
  if (ref.current?.deps === null || !_equals(ref.current?.deps, _deps)) {
    // 3. 의존성이 변경된 경우 factory 함수 실행 및 결과 저장
    ref.current.value = factory();
    ref.current.deps = _deps;
  }

  // 4. 메모이제이션된 값 반환
  return ref.current?.value as T;

```

    타입 안전성 관련
    -  ref.current?.value as T에서 이것은 잘못된 값이 반환되어도 컴파일러가 경고하지 않게 만들 수 있다고 찾아보았습니다. 따라, as T를 사용하는 방식이 안전한지에 대해 검토받고싶습니다.

    고생하셨습니다 원표님!

> as T를 사용하는 방식이 안전한지에 대해 검토받고싶습니다.

네 고민하신 부분이 맞습니다. 타입스크립트를 사용하는 이유는 타입을 추론하게 하여 트랜스파일단계에서 타입에러를 사전에 체크하기 위함인데요. 타입단언은 추론을 못하게 만드는 장치이다보니 정말 추론이 어려운 써드파티의 코드들에서만 사용을 권장하곤합니다. 
현재의 코드를 제네릭으로 구현하시다보니 반환코드에서 타입 린트에러가 나셨던 듯 하네요. 내부 로직에서 undefined 가드를 해보셔서 단언을 없애보시면 좋을 듯 합니다.

기본과제 피드백으로 갈음하겠습니다!
취소선에 있는 리팩토링 계획 기대할게요 ㅎㅎ!! 리팩토링후에 개인적으로 리뷰 주셔도 좋습니다~
