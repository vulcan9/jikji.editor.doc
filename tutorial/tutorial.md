# API 사용 방법

API를 사용해 작성된 스크립트는 다음 두가지 방법으로 Jik-ji 저작툴에 삽입할 수 있습니다.

* 외부 JS 파일에 작성한 후 파일 임포트 시키는 방법
* `이벤트 설정창`의 `스크립트 작성` 항목을 선택한 후 코드를 직접 작성하는 방법

버튼을 클릭하면 이미지가 보였다 사라지는 토글 버튼을 위 두가지 방법으로 만들어 보겠습니다. 먼저 Jik-ji 저작툴에서 UI를 만듭니다.

&#x20;

![이미지에 아이디를  "image"로 지정](../.gitbook/assets/using\_02.png)

![버튼에 아이디를  "button"으로 지정](../.gitbook/assets/using\_01.png)

버튼과 이미지를 각각 하나씩 만들고 아이디를 `button`, `image`로 설정해 주었습니다. 이렇게 설정한 아이디를 통하여 각 element의 API에 접근할 것입니다. 필요한 UI는 이것으로 다 만들어 졌습니다. 이제 이 두개의 element를 제어하는 코드를 작성해 보겠습니다.

