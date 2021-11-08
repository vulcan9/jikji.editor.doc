# Element 공통 API

#### $self

Element API의 샘플 코드에 사용된 `$self` 변수는 Element API 자신을 참조하는 변수입니다. `이벤트 동작 설정` 창의 `코드 작성` 항목에 코드를 작성할때 사용되며 외부 JS 파일에 작성되는 코드에는 사용할 수 없습니다. 대신 외부 JS 파일에서는 find() API를 이용하여 Element API를 찾을 수 있습니다.

```javascript
$self == window.$this.find('아이디');
$self == window.$this.find(uid);
$self == window.$this.find(dom);
```

자세한 사항은 [이벤트 설정창에서 코드 작성 도움말>미리정의된 변수](../../tutorial/eventwindow/properties.md) 를 참고하세요.

#### stateName

모든 element는 `normal`, `over`, `down` 상태가 존재합니다. `stateName` 매개변수를 필요로 하는 API의 경우 stateName을 설정하지 않으면 기본적으로 `normal` 상태의 값으로 처리됩니다.

![](../../.gitbook/assets/reference\_04.png)

### Element 공통 API

Text, Input, Image, Video/Audio Element API에 공통으로 제공되는 내용입니다.

* ****[**uid: String**](../jjapi.md#undefined)****
* ****[**dom: DOMElement**](../jjapi.md#undefined)****
* ****[**scope: Object**](../jjapi.md#undefined)****
* ****[**document: APIObject**](../jjapi.md#undefined)****
* ****[**scaleFactor (): Number**](../jjapi.md#undefined-1)****
* ****[**find (): APIObject**](../jjapi.md#undefined-1)****
* ****[**findAll (): Object**](../jjapi.md#undefined-1)****
* **disable (): Boolean**

#### 객체

*   **animation: Object**

    animation 객체에 대한 내용은 [Animation 객체](../animationapi.md) 문서를 참고하세요.
*   **capsule: Object**

    캡슐화 목록에서 설정된 값이 전달됩니다. capsule 객체에 대한 내용은 [캡슐화 기능 사용하기](../../tutorial/capsulize/#capsule) 문서를 참고하세요.

#### 속성

*   **\_eventNames: String**

    (읽기전용) 등록 가능한 이벤트 type을 문자열로 가지고 있습니다. 사용 가능한 이벤트 이름을 참고하여 이벤트를 등록하여 사용할 수 있습니다.

    ```javascript
    (API Object)._eventNames
    // 출력 : "click, dblclick, mousedown, mousemove, mouseout, mouseover, mouseup, resize"
    ```
*   **id: String**

    (읽기전용) Jik-ji 저작툴에서 설정한 element의 id 값입니다. ![](../../.gitbook/assets/reference\_01.png)

#### 이벤트 관련 메서드

`_eventNames` 속성에 포함된 이벤트 이름을 참고하여 이벤트를 등록하여 사용할 수 있습니다.

*   **on (type: String, handler: Function): void**

    이벤트 핸들러를 등록합니다.

    ```javascript
    $self.on('click', handler);
    function handler(e){
      console.error('click');
    }
    ```
*   **off (type: String, handler: Function): void**

    등록된 이벤트 핸들러를 제거합니다.

    ```javascript
    $self.off('click', handler);
    function handler(e){
      console.error('click');
    }
    ```
*   **trigger (type:String|Event, detail:Array): void**

    이벤트를 발생시킵니다.

    ```javascript
    $self.trigger('click');
    // document API의 'click' 이벤트가 발생했습니다.

    $self.trigger(new Event('custom'), [dataObject]);
    ```

#### 속성 관련 메서드

Jik-ji 저작툴에서 설정된 크기, 위치 관련 API입니다. 매개변수를 전달하지 않으면 설정된 값을 반환하고, 매개변수를 전달하면 전달된 값을 적용합니다.

![](../../.gitbook/assets/reference\_03.png)

*   **width (value: Number, stateName: String): Number**

    element의 가로 크기입니다.

    ```javascript
    // Getter
    var w = $self.width();
    // 'over' 상태의 값을 가져옴
    var w = $self.width('over');

    // Setter
    // 'normal' 상태의 width를 10으로 설정함
    $self.width(10);
    // 'over' 상태의 width를 20으로 설정함
    $self.width(20, 'over');
    ```
*   **height (value: Number, stateName: String): Number**

    element의 세로 크기입니다.

    ```javascript
    // Getter
    var h = $self.height();
    // 'over' 상태의 값을 가져옴
    var h = $self.height('over');

    // Setter
    // 'normal' 상태의 height를 10으로 설정함
    $self.height(10);
    // 'over' 상태의 height를 20으로 설정함
    $self.height(20, 'over');
    ```
*   **x (value: Number, stateName: String): Number**

    element의 가로 위치입니다.

    ```javascript
    // Getter
    var x = $self.x();
    // 'over' 상태의 값을 가져옴
    var x = $self.x('over');

    // Setter
    // 'normal' 상태의 x 위치를 10으로 설정함
    $self.x(10);
    // 'over' 상태의 x 위치를 20으로 설정함
    $self.x(20, 'over');
    ```
*   **y (value: Number, stateName: String): Number**

    element의 세로 위치입니다.

    ```javascript
    // Getter
    var y = $self.y();
    // 'over' 상태의 값을 가져옴
    var y = $self.y('over');

    // Setter
    // 'normal' 상태의 y 위치를 10으로 설정함
    $self.y(10);
    // 'over' 상태의 y 위치를 20으로 설정함
    $self.y(20, 'over');
    ```
*   **rotate (value: Number, stateName: String): Number**

    element의 회전 각도(`degree`)입니다. 회전 중심은 설정은 `setStyle()` 메서드를 이용하여 [`transformOrigin`](https://www.w3schools.com/cssref/css3\_pr\_transform-origin.asp) 값으로 설정합니다.

    ```javascript
    // Getter
    var degree = $self.rotate();
    // 'over' 상태의 값을 가져옴
    var degree = $self.rotate('over');

    // Setter
    // 'normal' 상태의 회전각을 10도 설정함
    $self.rotate(10);
    // 'over' 상태의 회전각을 20도 설정함
    $self.rotate(20, 'over');
    ```
*   **scale (value: Number, stateName: String): Number**

    element의 scale(`0 ~ 1`)입니다.

```javascript
// Getter
var scale = $self.scale();
// 'over' 상태의 값을 가져옴
var scale = $self.scale('over');
// Setter
// 'normal' 상태의 scale을 두배로 설정함
$self.scale(2);
// 'over' 상태의 scale을 0.5로 설정함
$self.scale(0.5, 'over');
```

#### visible 관련 메서드

*   **show (): void**

    element를 보이기 상태로 전환합니다.

    ```javascript
    $self.show();
    ```
*   **hide (): void**

    element를 감추기 상태로 전환합니다. 이 메서드는 opacity를 0으로 설정 합니다.

    ```javascript
    $self.hide(); // opacity = 0 설정
    $self.setStyle({display:'none'}); // display style 설정
    ```
*   **toggleVisible (): void**

    element를 보이기/감추기 토글 기능입니다.

    ```javascript
    $self.toggleVisible();
    ```
*   **isVisible (): Boolean**

    element의 현재 보이기(true)/감추기(false) 상태값을 나타냅니다.

    ```javascript
    var visible = $self.isVisible();
    ```

#### 스타일 관련 메서드

Jik-ji 저작툴에서 생성된 element에 style을 적용할때에는 알아야할 몇가지 사항이 있습니다. [Element에 스타일 적용](https://github.com/vulcan9/jjapi/tree/f02bad6f9eae8fb70b93aa89ed5803a58060d3de/tutorial/element.md) 문서의 내용을 먼저 참고하시는 것이 좋습니다.

*   **getStyle (cssName: String, stateName: String): any**

    element의 style 속성값을 반환합니다. 설정되지 않은 style인 경우 `undefined`가 반환됩니다.

    ```javascript
    var value = $self.getStyle('borderWidth');
    var value = $self.getStyle('borderWidth', 'over');

    // 특별히 지원되는 align 속성
    // alignX: left, right, center, horizontal (양쪽 맞춤)
    // alignY: top, bottom, middle, vertical (양쪽 맞춤)
    var value = $self.getStyle('alignX');
    ```
*   **setStyle (obj: Object, stateName: String): void**

    element의 style 속성값을 설정합니다.

    ```javascript
    // 선 두께를 10px로 설정함.
    $self.setStyle('borderWidth', 10);
    $self.setStyle('borderWidth', 10, 'over');

    // 여러 style 속성을 하나의 객체로 전달해도 됨.
    $self.setStyle({
      borderWidth:10,
      borderColor: "rgb(106, 168, 79)"
    }, 'over');

    // 특별히 지원되는 align 속성
    // alignX: left, right, center, horizontal (양쪽 맞춤)
    // alignY: top, bottom, middle, vertical (양쪽 맞춤)
    // 부모 그룹 기준에서 오른쪽 하단으로 정렬
    $self.setStyle({
      alignX: 'right', right: 0,
      alignY: 'bottom', bottom: 0
    });
    ```

#### 드래그 기능 메서드

*   **setDrag (onStart: Function, onDrag: Function, onEnd: Function, option:Object): void**

    element에 드래그 기능을 부여합니다.

    * option: **Object**
      *   direction: **String** \


          x축 방향으로만 이동('x'). y축 방향으로만 이동('y'). 생략하면 x,y축 이동이 가능합니다.
      * minX: **Number** \
        &#x20;x축 이동가능한 최소값.
      * maxX: **Number** \
        &#x20;x축 이동가능한 최대값.
      * minY: **Number** \
        &#x20;y축 이동가능한 최소값.
      * maxY: **Number** \
        &#x20;y축 이동가능한 최대값.

    ```javascript
    // element에 드래그 기능을 구현하는 가장 간단한 방법 입니다.
    $self.setDrag();

    // x 축으로만 이동
    $self.setDrag(null, null, null, {
      direction: 'x'
    });
    ```

    *   onStart: _**Function**_\


        `mousedown` 이벤트 핸들러로 등록될 함수입니다.

        ```javascript
        function onStart(event, info){
          // your code...
        }
        /*
        // info 내용
        {
          x: 드래그 시작 x 위치,  
          y: 드래그 시작 y 위치
        }
        */
        ```
    *   onDrag: _**Function**_\


        `mousemove` 이벤트 핸들러로 등록될 함수입니다.

        ```javascript
        function onDrag(event, info){
          // your code...
          // event.preventDefault() 를 호출하면 x, y 위치가 적용되지 않습니다.
        }
        /*
        // info 내용
        {
          movedX: 드래그 시작부터 누적 x 이동 거리,
          movedY: 드래그 시작부터 누적 y 이동 거리,
          dx: 순간 x 이동 거리, 
          dy: 순간 y 이동 거리,
          x: 이동할 x 위치, 
          y: 이동할 y 위치
        }
        */
        ```
    *   onEnd: _**Function**_\


        `mouseup` 이벤트 핸들러로 등록될 함수입니다.

        ```javascript
        function onEnd(event, info){
          // your code...
        }
        /*
        // info 내용
        {
          x: 최종 x 위치, 
          y: 최종 y 위치
        }
        */
        ```
*   **removeDrag(): void**

    드래그 기능을 제거합니다.

    ```javascript
    $self.removeDrag();
    ```
*   **isDragable (): Boolean**

    `setDrag()` API에 의해 드래그 기능이 설정(`true`) 되었는지 여부를 나타냅니다. `removeDrag()` API에 의해 드래그 기능을 제거하면 `false` 값을 가집니다.

    ```javascript
    // 드래그 기능을 없애는 코드
    if($self.isDragrable()){
      $self.removeDrag();
    }
    ```

#### 비활성화 메서드

*   **disable (value: Boolean): Boolean**

    element가 마우스 이벤트를 받지 못하도록 비활성화 시킵니다. element가 가진 기능까지 비활성화 시켜주진 않습니다.

    ```javascript
    $self.disable(false);
    $self.disable(true);
    var disable = $self.disable();
    ```
