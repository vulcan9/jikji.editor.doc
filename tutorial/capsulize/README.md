# 캡슐화 기능 사용하기

## 캡슐화 기능 사용하기 <a href="capsule" id="capsule"></a>

캡슐화 기능은 이벤트 설정창에서 작성된 사용자 스크립트에서 옵션으로 선택할수 있을만한 변수들을 UI로 노출시킴으로써 스크립트에 작성된 세부 로직을 알고있지 않아도 옵션 선택만으로 로직을 제어할수 있도록 하는 기능입니다.

그룹으로 지정된 `mask` element에서 사용 가능하고, 컴포넌트화 할때 잠금기능으로 캡슐화 목록을 편집하지 못하게 하여 배포할 수도 있습니다.

캡슐화 기능을 사용하여 컴포넌트로 배포하는 방법을 차례대로 알아보겠습니다. 두개의 텍스트박스의 문자열을 코드수정 없이 사용자가 제어하는 간단한 컴포넌트를 제작해 보겠습니다.

1. 캡슐화 기능이 적용된 컴포넌트를 만듭니다.
2. 컴포넌트를 배포합니다.
3. 다른 사용자가 배포된 컴포넌트를 import 합니다.
4. import된 컴포넌트를 캡슐화 기능을 사용하여 설정을 변경합니다.
5. 미리보기로 동작을 확인합니다.

