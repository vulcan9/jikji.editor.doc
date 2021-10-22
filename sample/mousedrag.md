# 마우스 드래그 기능

마우스 드래그 기능을 두가지 방법으로 만들어 보겠습니다.

* mouse Event를 이용하여 구현하는 방법
* `setDrag()` API를 이용하는 방법

두번째 방법이 기능 구현이 훨씬 간단한 방법이지만, API 사용 방법을 학습하기 위해 Mouse Event를 이용하는 방법으로 먼저 기능을 구현해 보겠습니다.

## UI 구성

* `paper`에 `이미지` Element 하나를 추가합니다.

![](../.gitbook/assets/d\_01.png)

*   코드에서 삽입한 이미지 객체를 찾기 위해 아이디를 `image`로 설정합니다.\


    `uid` 값으로도 찾을 수 있지만 기억하기 힘들기 때문에 아이디를 설정하였습니다.

## 1. Mouse Event를 이용하여 구현하는 방법

외부 JS 파일에 코드를 작성하여 동작을 확인해 보겠습니다.

* 외부 JS 파일에 다음 코드를 작성합니다.
* `utf-8` 형식으로 JS 파일을 저장합니니다.

```javascript
$(document).ready(function(){

    // 코드에는 드래그 중인 Element가 최상위(`zIndex`)로 올라오도록 하는 기능도 함께 구현되어 있습니다.
    try{
        // Image Element API 찾기
        var image = window.$this.find('image');
        var zIndex = image.getStyle('zIndex');

        // 이벤트 등록
        image.on('mousedown', function(e){
            $(window.document).on('mousemove', onMousemove);
            $(window.document).on('mouseup', onMouseup);

            image.setStyle('zIndex', 10000);
        });

        var _last;
        function onMousemove(e){
            if(!_last) _last = {x: e.pageX, y: e.pageY};

            // 이동 거리
            var distX = e.clientX - _last.x;
            var distY = e.clientY - _last.y;

            // 화면 scale 값 보정
            var scaleFactor = image.scaleFactor();
            var x = image.x() + distX / scaleFactor;
            var y = image.y() + distY / scaleFactor;

            // 위치 이동
            image.x(x);
            image.y(y);

            _last.x = e.clientX;
            _last.y = e.clientY;
        }

        function onMouseup(){
            $(window.document).off('mousemove', onMousemove);
            $(window.document).off('mouseup', onMouseup);
            _last = null;

            image.setStyle('zIndex', zIndex);
        }

    }catch(err){
        console.error('[Error]', err.stack);
    }
});
```

* 저장한 JS 파일을 \`파일 목록 편집기에서 불러옵니다.

![](../.gitbook/assets/d\_02.png)

* 미리보기를 통해 기능을 확인합니다.

## 2. setDrag() API를 이용하는 방법

*   \`파일 목록 편집기에서 방금 불러온 JS 파일을 비활성화 시킵니다.\


    미리보기를 통해 드래그 기능이 더이상 작동하지 않음을 확인합니다.

![](../.gitbook/assets/d\_03.png)

*   `paper`에서 이미지 Element가 선택된 상태에서 `이벤트 동작 설정`창을 열어 코드를 작성합니다. \


    `initialize` 이벤트에 다음 코드를 작성하겠습니다.

```javascript
$self.setDrag();
```

![](../.gitbook/assets/d\_04.png)

* 미리보기를 통해 이미지가 드래그 되는 것을 확인합니다.
* 위와 같이 드래그 할때 최상위에 보여지도록 하는 코드를 추가합니다.

```javascript
var zIndex = $self.getStyle('zIndex');
$self.setDrag(onStart, onDrag, onEnd);

// 핸들러에서 this context는 $self,즉 'image' API 객체입니다.
function onStart(e, info){
    this.setStyle('zIndex', 10000);
}

function onDrag(e, info){
    // 이동 취소
    // e.preventDefault();
}

function onEnd(e, info){
    this.setStyle('zIndex', zIndex);
}
```

* 매개변수에 핸들러 함수를 전달하여 같은 기능을 구현하였습니다.
* 미리보기를 통해 기능을 확인합니다.
