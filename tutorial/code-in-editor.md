# 이벤트 설정창에서 코드 작성

모든 코드는 `이벤트 동작 설정창` 에서 작성됩니다.

### 코드 작성 방법 1

* `button` element를 선택한 후 좌측 이벤트 메뉴 버튼을 선택합니다. `on click` 이벤트 항목에 `add action` 버튼을 클릭하여 `이벤트 동작 설정` 창을 띄웁니다.



![](../.gitbook/assets/using\_03\_1.png)

* `이벤트 동작 설정` 창에서 `스크립트 작성` 항목을 선택 합니다.

![](../.gitbook/assets/using\_03\_2.png)

* `코드 작성` 박스에 다음 코드를 작성 합니다.

```javascript
//var buttonAPI = $self;
var imageAPI = $self.children('image', false);
// 또는
// var imageAPI = window.$this.children('image');
imageAPI.toggleVisible();
```

여기에서 사용한 `$self`는 `코드 작성` 박스에서만 제공되는 예약어로 element 자기 자신의 API를 참조합니다. `self`는 다음 코드와 동일합니다.

```javascript
$self = window.$this.children('자신의 element 아이디');
```

자세한 내용은 [이벤트 설정창에서 스크립트 작성](eventwindow/) 도움말을 참고 하세요.

![](../.gitbook/assets/using\_03\_2\_1.png)

* `미리보기`를 실행하면 버튼을 클릭할 때마다 이미지가 보였다 사라지기를 반복합니다.

![](../.gitbook/assets/using\_03\_3.png)

### 코드 작성 방법 2 :

이번에는 다른 이벤트에 코드를 작성해 보겠습니다. 실행 결과는 같습니다.

* 방금 `on click` 이벤트에 추가했던 스크립트를 휴지통 아이콘을 눌러 삭제합니다.

![](../.gitbook/assets/using\_03\_4.png)

* 이번에는 `button`의 `on initialize` 이벤트에 코드를 작성해 보겠습니다. 이 이벤트는 문서에 삽입된 모든 element가 생성된 후 초기화 될때 호출되는 이벤트 입니다.

![](../.gitbook/assets/using\_03\_5.png)

* 위와 같은 방식으로 `add action`버튼을 누르고 `이벤트 동작 설정창`에서 `스크립트 작성` 항목을 선택 합니다.
* `코드 작성`란에 다음 코드를 작성 합니다.

```javascript
var button = $self.children('button');

// 클릭 이벤트 등록
button.on('click', function(e){
  var image = $self.children('image');
  image.toggleVisible();
});
```

버튼의 `click` 이벤트 핸들러를 직접 작성하여 element가 초기화 될때 실행되도록 `initial` 이벤트 항목에 스크립트를 추가한 것입니다. 버튼에 마우스가 왔을때 커서 모양을 바꾸려면 다음 코드 한줄을 추가합니다.

```javascript
// 버튼 모양 커서로 변경
button.setStyle('cursor', 'pointer');
```
