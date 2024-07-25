# 외부 JS 파일에 코드 작성

`이벤트 설정창`을 사용하지 않고 외부 `.js`파일에 원하는 기능을 구현한뒤 Jik-ji 저작툴에 적용하는 방법을 알아보겠습니다.

* 먼저 위와 같이 `button`, `image` 아이디가 지정된 두개의 element가 저작툴에 만들어져 있는지 확인합니다.
* 외부 javascript 편집기에서 다음 코드를 작성한 후 원하는 이름의 `JS` 파일로 저장합니다. 여기에서는 `imageToggle.js`라는 이름으로 저장하겠습니다.

```javascript
$(document).ready(function(){
  var button = window.$this.children('button');
  button.setStyle('cursor', 'pointer');

  // 클릭 이벤트 등록
  button.on('click', function(event){
    var image = window.$this.children('image');
    image.toggleVisible();
  });
});
```

* 같은 내용의 코드가 `document`가 로드된 뒤에 실행되도록 핸들러로 감싸여져 있습니다. 그렇지 않으면 element 생성 전에 코드가 실행되게 되어 원하는 element를 참조할 수 없는 경우가 발생합니다.
* 저장할때는 꼭 인코딩 형식을 `utf-8` 형식으로 저장하시기 바랍니다. 아이디등에 한글 문자를 사용하는 경우 간혹 인식하지 못하는 경우가 생깁니다.

![](../.gitbook/assets/using\_04\_1.png)

* 파일이 준비 되었으면 저작툴 상단 메뉴에서 `파일 목록 편집기`를 엽니다.&#x20;
*   JS 파일 버튼을 눌러 파일을 선택하면 파일이 임포트 됩니다.&#x20;

    이때 꼭 버튼이 삽입된 문서가 선택된 상태에서 `파일 목록 편집기`를 열어야 합니다. 그렇지 않으면 다른 문서에 해당 JS 파일이 임포트 되게 됩니다.&#x20;

![](../.gitbook/assets/using\_04\_2.png)

* `사용중` 체크박스에 체크된 것을 확인하고 확인을 눌러 창을 닫습니다.
* 미리보기를 통해 동작을 확인합니다.

![](<../.gitbook/assets/using\_03\_3 (1).png>)

{% hint style="info" %}
외부 JS 파일에서 인스턴스를 찾기 위해 element나 group의 uid를 사용할 수도 있습니다만,  콤포넌트나 템플릿을 만들기 위해서라면 권장하지는 않습니다.

콤포넌트나 템플릿으로 변환할때 uid 값들이 변경되는데 외부 JS 파일안의 uid는 자동으로 변경되지 않습니다.

이런  경우에는 이벤트 창 등에서 미리 uid 값들을 변수에 담은뒤 JS 파일에 전달하여 사용하면 자동으로 변경된 uid를 참조할 수 있습니다.
{% endhint %}

