# 공통 API

제공되는 API는 크게 4가지 영역으로 구분할 수 있습니다.

* Window 범주 - window scope으로 제공되는 전역 API
* Document 범주 - 문서(paper)와 관련된 API (`window.document` 와 관련 없음)
* Element 범주
  * Text Element - 텍스트 표시 요소
  * Input Element - 입력박스 표시 요소
  * Image Element - 이미지 표시 요시
  * Video/Audio Element - 미디어 표시 요소
* Group 범주 - group화된 element를 제어하는 API

## 공통으로 가지고있는 API

위에서 분류한 모든 범주의 API는 다음과 같은 공통된 인터페이스를 구현하고 있습니다.

### 속성

*   _**uid: String**_

    (읽기전용) API를 구별하는 고유 uid값

    ```javascript
    // element의 uid 찾기
    var uid = window.$this.find('element 아이디').uid;
    ```
*   _**dom: DOMEleemnt**_

    (읽기전용) API 대상이되는 HTML DOM 객체 참조

    ```javascript
    // element의 DOM (node)
    var dom = window.$this.find('element 아이디').dom;
    ```
*   _**document: APIObject**_

    (읽기전용) 여기에서 지칭하는 `document`는 `window.document`가 아닙니다. Jik-ji 저작툴에서 생성된 하나의 문서( 또는 Paper or page)를 의미합니다. Document API에서는 자기 자신을 나타내므로 `document` 속성은 없습니다.

    ```javascript
    // documentAPI 찾기
    var documentAPI = window.$this.document;
    var documentAPI = window.$this.find('element 아이디').document;
    ```
*   _**scope: Object**_

    API 코드 작성자가 런타임에 변수를 저장하기 위한 용도로 사용합니다. window context에 글로벌 변수를 정의하여 사용하면 변수이름이 서로 중복되거나 덮어쓰기 되는 경우가 발생하므로 자신의 API내에서 임시 저장하여 사용할 수 있도록 `scope` 속성을 제공합니다.

    ```javascript
    window.$this.scope.someString = '임시 저장 문자열';
    window.$this.scope.someObject = {};
    window.$this.scope.someFunction = function(){};

    // 저장된 변수 사용
    console.log(window.$this.scope.someString);
    ```

### 메서드

*   _**scaleFactor (): Number**_

    document.body에 적용된 scale transform 속성값 입니다.

    ```javascript
    var scaleNumber = $self.scaleFactor();
    // document.body.style의 scale transform 속성값
    ```
*   _**find (any, onlyChild:Boolean): APIObject**** **<mark style="color:red;">**(DEPRECATE: 대신 children API 사용)**</mark>_

    ~~DOM 또는 DOM id Attribute 값을 통해 Element 객체의 API를 찾습니다. 아무 값도 전달하지 않으면 자기 자신(API)을 리턴 합니다. `window API`와 `docuemnt API`는 각각 `$this`와 `$api.document` 를 통해 접근할 수 있습니다.~~\
    \
    (ver.3.3.31 이후수정된 사항)\
    id, uid, name 문자열   및 DOM 참조를 비교하여 Element 객체의 API를 찾습니다. 이전과 다르게 DOM으로부터 검색하지 않고 데이터에서 검색한  결과를 리턴합니다. 아무것도   전달되지 않을때에는 `undefined`  값을 리턴 합니다.\
    `window API`와 `docuemnt API`는 각각 `$this`와 `$api.document` 를 통해 접근할 수 있습니다.

    * any: **String | DOMElement** \
      id, uid, dom, name 값으로 element의 API Object 찾기   &#x20;
    *   onlyChild: **Boolean**  (생략가능) 자신의 하위(1-Depth) 노드에 대해서만 탐색할지(true) 여부\
        onlyChild 값이  true 이면 자신의 바로 아래 (1-Depth) child element 만 검색합니다.\
        onlyChild 값이  false 이면 자신의 하위 Depth 전체의 element를 검색합니다.       &#x20;

        ```javascript
        // uid 값과 일치하는 element의 API를 리턴
        var api = $self.find(uid);
        // id 값과 일치하는한 element의 API를 리턴
        var api = $self.find(id);
        // dom 참조와 일치하는 element의 API를 리턴
        var api = $self.find(dom);
        // name 값과 일치하는 element의 API를 리턴
        var api = $self.find(name);

        // 반환되는 api 는 배열일수도 있습니다. 
        ```

        (주의) ~~재사용 가능한 Component를 제작을위해서는 `uid`를 사용하는 것이 좋습니다.~~ Copy\&Paste 또는 Component로 저장하는 과정에서 `uid`는 자동으로 새로 생성되는 element를 찾지만 id 값은 변하지 않기 때문에 항상 같은 element만을 찾게 됩니다.\
        \
        (ver.3.3.31 이후수정된 사항)\
        컴포넌트를 제작할때 이전처럼 uid 를 사용해도 되지만 find api의 onlyChild 옵션을 사용하면 name, id 등을 사용해도 하위 그룹에 있을지 모를 중복된 id 또는 name을 사용하는 다른 컴포넌트의 element가 검색되는 염려가 없기때문에 가독성 있는 코드를 생성할 수 있습니다.
*   _**findAll (onlyChild): Object**** **<mark style="color:red;">**(DEPRECATE: 대신 childrenAll API 사용)**</mark>_

    모든 Element API 목록을 리턴 합니다.

    * onlyChild: **Boolean**  (생략가능 ) 자신의 하위(1-Depth) 노드에 대해서만 탐색할지(true) 여부   \
      onlyChild 값이  true 이면 자신의 바로 아래 (1-Depth) child element 만 검색합니다.\
      onlyChild 값이  false 이면 자신의 하위 Depth 전체의 element를 검색합니다.

    ```javascript
    var map = $self.findAll();
    // Map {elementUID: elementAPI, ...}

    // onlyChild를 지정하면 그룹 element인 경우 하위 element만 필터링 합니다. 
    var childMap = $self.findAll(true)
    ```
* _**loadJS (jsURL:String, onLoaded:Function):void**_\
  외부 JS 파일을 동적으로 로드합니다. 이미 로드된 JS 파일이면 중복 로드하지 않고 바로 `onLoaded` 메서드를 호출합니다.\
  자세한 내용은 [Element에서 JS 파일 동적으로 로드](https://app.gitbook.com/s/y5qQb2jYHinob4a78GGK/\~/changes/d4OY85wjhCe2MUMUVOq3/tutorial/element-js) 페이지를 참고하세요\
  <mark style="color:red;">(Jik-ji 3.1.44 버전 이상에서 지원됨)</mark>
* _**loadComponent(info, onload):void**_\
  컴포넌트를 정의한 외부 JS파일을 loadJS 함수를 이용하여 로드하고 컴포넌트 정의 객체를 전달해 줍니다.\
  자세한 내용은 [loadComponent API를 이용하여  컴포넌트 작성하기](../tutorial/loadcomponent-api.md) 페이지를 참고하세요\
  <mark style="color:red;">(Jik-ji 3.3.31 버전 이상에서 지원됨)</mark>
  * info: {name:String, source: String}\
    name: 컴포넌트 정의 객체를 찾을 수 있는 문자열\
    source: 컴포넌트가 정의된 JS 파일 경로
  *   onLoaded: Function \
      로드가 완료되어 컴포넌트 객체가 전달되는 콜백 함수

      ```javascript
      // 컴포넌트 설치 정보
      const component = {
        // 컴포넌트 소스 파일에서 정의한 component 객체 참조 문자열
        name: 'jikjiComponent.Navi.Tab',
        // 컴포넌트 소스 파일 경로
        // (_share 폴더 아래에 중복되지 않을만한 경로가 좋음)
        source: './_share/jikji.component/Navi/Tab.js'
      }

      $self.loadComponent(component, (Component) => {
        // new Component($self, config, onInitialize, ...);
      });

      //---------------------
      // Tab.js 파일 작성
      (function(component){
        
        // 컴포넌트 객체 정의
        function Tab($self, config, onInitialize){
          // 컴포넌트 기능 구현
        }

        // Export
        if(!component.Tab) component.Tab = Tab;
        window['jikjiComponent'] = component;

      })(window['jikjiComponent'] || {});
      ```

