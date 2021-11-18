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
*   _**find (any): APIObject**_

    DOM 또는 DOM id Attribute 값을 통해 Element 객체의 API를 찾습니다. 아무 값도 전달하지 않으면 자기 자신(API)을 리턴 합니다. `window API`와 `docuemnt API`는 각각 `$this`와 `$api.document` 를 통해 접근할 수 있습니다.

    ```javascript
    // uid값과 일치하는 element의 API를 리턴
    var api = $self.find(uid);
    // id값과 일치한 id attribute을 가진 element의 API를 리턴
    var api = $self.find(id);
    // dom과 일치하는 element의 API를 리턴
    var api = $self.find(dom);
    ```

    주) 재사용 가능한 Component를 제작을위해서는 `uid`를 사용하는 것이 좋습니다. Copy\&Paste 또는 Component로 저장하는 과정에서 `uid`는 자동으로 새로 생성되는 element를 찾지만 id 값은 변하지 않기 때문에 항상 같은 element만을 찾게 됩니다.
*   _**findAll (onlyChild): Object**_

    모든 Element API 목록을 리턴 합니다.

    ```javascript
    var map = $self.findAll();
    // Map {elementUID: elementAPI, ...}

    // onlyChild를 지정하면 그룹 element인 경우 하위 element만 필터링 합니다. 
    var childMap = $self.findAll(true)
    ```
