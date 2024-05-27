# Document API

여기에서 지칭하는 `document`는 `window.document`가 아닙니다. Jik-ji 저작툴에서 생성된 하나의 문서( 또는 Paper or page)를 의미합니다. 따라서 다음 속성들은 문서의 geometry 값을 가집니다. 문서의 크기는 API를 통해 임의로 변경할 수 없으므로 아래 속성은 모두 읽기전용 속성입니다. 각 API 객체가 가지고 있는 `document` 변수를 통해 접근할 수 있습니다.

```javascript
var api = window.$this.document
var w = api.width();
console.log('문서 너비 : ', w);
```

### 공통 API

*   _**\_eventNames: String**_

    (읽기전용) 등록 가능한 이벤트 type을 문자열로 가지고 있습니다. 사용 가능한 이벤트 이름을 참고하여 이벤트를 등록하여 사용할 수 있습니다.

    ```javascript
    (API Object)._eventNames
    // 출력 : "$destroy, click, dblclick, mousedown, mousemove, mouseout, mouseover, mouseup"
    ```
* [_**uid: String**_](jjapi.md#common-property-uid)
* [_**dom: DOMElement**_](jjapi.md#common-property-dom)
* [_**scope: Object**_](jjapi.md#common-property-scope)
* [_**scaleFactor (): Number**_](jjapi.md#common-method-scalefactor)
* [_**find (any): APIObject**_](jjapi.md#common-method-find) _**(deplecate)**_
* [_**findAll (): Object**_](jjapi.md#common-method-findall) _**(deplecate)**_
* [_**children (): Object**_](jjapi.md#undefined-1) _**(v3.3.32\~)**_
* [_**childrenAll (): Object**_](jjapi.md#undefined-1) _**(v3.3.32\~)**_
* [_**loadCSS(): void**_](jjapi.md#undefined-1) _**(v3.3.32\~)**_
* [_**loadJS(): void**_](jjapi.md#undefined-1) _**(v3.3.32\~)**_
* [_**loadComponent(): void**_](jjapi.md#undefined-1) _**(v3.3.32\~)**_

### 속성

*   **$injector**

    동적으로 UI를 추가할 필요가 있는 경우 페이지의 angular application을 이용할 수 있습니다.

```
// $injector 사용 예 (element 내에서 angular를 사용하고자 할때)
function compile(){
    // injection
    const {$injector} = $self.document.angular();
    const $compile = $injector.get('$compile');
    const $rootScope = $injector.get('$rootScope');

    // dom
    const domString = '<div>{{name}}</div>'
    const $dom = angular.element(domString);

    // scope
    const scope = $rootScope.$new(true);
    scope.name = '이름';

    // 컴파일
    $compile($dom)(scope);
    // scope.$applyAsync();
    // $dom.insertAfter($node);
    $parentNode.append($dom);
}
```

### 이벤트 관련 메서드

`_eventNames` 속성에 포함된 이벤트 이름을 참고하여 이벤트를 등록하여 사용할 수 있습니다.

*   _**on (type: String, handler: Function): void**_

    이벤트 핸들러를 등록합니다.

    ```javascript
    window.$this.document.on('click', handler);
    function handler(e){
      console.error('click');
    }
    ```
*   _**off (type: String, handler: Function): void**_

    등록된 이벤트 핸들러를 제거합니다.

    ```javascript
    window.$this.document.off('click', handler);
    function handler(e){
      console.error('click');
    }
    ```
*   _**trigger (type: String): void**_

    이벤트를 발생시킵니다.

    ```javascript
    window.$this.document.trigger('click');
    // document API의 'click' 이벤트가 발생했습니다.
    ```

### 메서드

*   _**width (): Number**_

    (읽기전용) Jik-ji 저작툴에서 설정된 문서(paper)의 가로 크기를 가져옵니다. ![](../.gitbook/assets/reference\_02.png)

    ```javascript
    var paper_width = window.$this.document.width();
    ```
*   _**height (): Number**_

    (읽기전용) Jik-ji 저작툴에서 설정된 문서(paper)의 세로 크기를 가져옵니다. ![](<../.gitbook/assets/reference\_02 (1).png>)

    ```javascript
    var paper_height = window.$this.document.height();
    ```
*   _**x (): Number**_

    (읽기전용) 문서(paper)의 시작 가로 위치값입니다. 항상 `0`값을 가집니다.

    ```javascript
    var paper_x = window.$this.document.x();
    // 항상값을 0값을 가짐
    ```
*   _**y (): Number**_

    (읽기전용) 문서(paper)의 세로 크기를 위치값입니다. 항상 `0`값을 가집니다.

    ```javascript
    var paper_y = window.$this.document.y();
    // 항상값을 0값을 가짐
    ```
