---
description: 컴포넌트를 만들어 배포하는 방법을 설명합니다.
---

# loadComponent API를 이용하여 컴포넌트 작성하기

&#x20;`jikji 3.3.31` 버전 이상에서 지원되는 `loadComponent` API를 이용하여 컴포넌트를 작성하는 방법을 소개합니다. \
컴포넌트에 대한 기본적인 내용은 [Element에서 JS 파일 동적으로 로드](element-js.md) 페이지를 참고하세요

### 작업 내용

작업   내용은 다음과 같습니다.

* 외부 JS 파일에 컴포넌트를 구현합니다.
* 이벤트 창에서 컴포넌트가 구현된 JS 파일을 로드합니다.
* 이벤트 창에서는 컴포넌트 구현에 필요한 정보를 컴포넌트 구현 객체에  넘겨줍니다.
  * element 요소들을 참조할 수 있도록 이름 정보
  * 컴포넌트 설정 옵션
  * 컴포넌트 초기화 완료 후 실행할 콜백함수

외부 JS 파일에 컴포넌트를 구현하면 다음과 같은 장점이 있습니다.

* 이벤트 코드 창에 컴포넌트 구현로직이 있으면 컴포넌트를 생성할때 또는  Element를  복사해서 사용할때마다 코드 복제본이 생성되게 되어 코드 수정 및 관리가 어려워 집니다.
* 컴포넌트 로직을 직지 외부에서 일괄 수정할 수 있습니다.  재 출판 없이 수정된 기능을 일괄적으로 적용 가능하기 때문에 컴포넌트 기능 관리가 쉬워집니다.

### 요소들 배치 (디자인)

먼저 직지에서 그룹을 하나 생성한 후 그룹 내부에 컴포넌트에서 사용할 element 요소들을 디자인 합니다.\


<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Tab 네비게이션 그룹 내부에 요소들을 배치</p></figcaption></figure>

Tab 네비게이션 그룹을 선택한 후 `initialize` 이벤트에 스크립트를 추가합니다.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### 컴포넌트 로드 및 설정 코드

`initialize` 이벤트에 추가할 코드 샘플입니다.

```java
(function (){
    
    // 컴포넌트 설치 정보
    const component = {
        // 컴포넌트 소스 파일에서 정의한 component 객체 참조 문자열
        name: 'jikjiComponent.Navi.Tab',
        // 컴포넌트 소스 파일 경로--
        // (_share 폴더 아래에 중복되지 않을만한 경로가 좋음)
        source: './_share/jikji.component/Navi/Tab.0.0.1.js'
    }
    
    // 컴포넌트 설정
    const config = {
        // 처음 선택 버튼 (1 부터 카운팅)
        select: 1,

        // 탭 버튼 네이밍 prefix : 탭버튼_1, 탭버튼_2, ...
        tabButtonName: '탭버튼_',
        //  탭 컨텐츠 네이밍 prefix : 탭컨텐츠_1, 탭컨텐츠_2, ...
        tabContentName: '탭컨텐츠_',

        elements: {
            prevButton: '이전버튼',
            nextButton: '다음버튼',

            // 탭 버튼으로 구성된 그룹
            // 각 버튼의 네이밍 규칙: 탭메뉴01, 탭메뉴02 ...  ~ 탭메뉴00
            tabButtonGroup: '탭버튼 그룹',

            // 탭 컨텐츠로 구성된 그룹
            // 각 컨텐츠의 네이밍 규칙: 탭컨텐츠01, 탭컨텐츠02 ...  ~ 탭컨텐츠00
            tabContentGroup: '탭컨텐츠 그룹',
        }
    };
    
    //-------------------------
    
    // 깜빡임 방지 위해 초기화 완료 이전까지 감추기
    $self.hide();
    
    // 컴포넌트 로드 & 초기화
    $self.loadComponent(component, (Component) => {
    	const onInitialize = () => $self.show();
        new Component($self, config, onInitialize);
    });
})();

```

컴포넌트 정의 JS 파일을 로드해서 컴포넌트 초기화를 실행하는 코드입니다.\
전달되는 `config` 속성은 컴포넌트에 따라 알맞게 설정하여 전달하면 됩니다.\
컴포넌트를 페이지에 여러개 사용하더라도 컴포는트 소스는 최초 한번만 로드됩니다

### 컴포넌트 구현 코드 (외부 JS 파일)

위 코드에서 `./_share/jikji.component/Navi/Tab.0.0.1.js` 경로로 설정된 파일에 작성되는 코드입니다.

#### `_share` 폴더 경로 사용

`_share` 폴더 하위에 에셋 파일을 설정해 놓으면 컴포넌트로 등록할때 경로가 바뀌지 않는 이점이 있습니다. \
`OPS/asset.file` 경로에 있는 asset 파일을 사용하여 컴포넌트를 만든 경우 컴포넌트 등록 후 파일 경로는 다음과 같이 바뀝니다.

```
OPS/asset.file
컴포넌트 등록 후 경로: _share/<component-uid...>/asset.file

OPS/_share/asset.file
컴포넌트 등록 후 경로: _share/asset.file
// 처음부터 _share 폴더를 사용한 경우에는 경로가 그대로 유지됨
```

**주의할 점**

* 다른 컴포넌트가 사용하는 경로와 겹치지 않을만한 경로를 사용해야 다른 컴포넌트 설치시 같은  경로에   덮어쓰기 되는 것을 방지할 수 있습니다.
* 직지에서 설치된 컴포넌트를 삭제할때 자동 삭제되지 않습니다.

#### 컴포넌트 구현 템플릿 코드

컴포넌트 구현 샘플입니다. 코드 템플릿으로 사용하시면 좋을것 같습니다.

```javascript
(function(component){

    // 버전 기록
    Tab.version = '0.0.1';

    // 최소 동작 가능 직지 버전 체크 (3.3.31 이상)
    (function (major, minor, build){
        // Jikji.API.version 체크
        var warn = () => console.error(`${window.VERSION?.project} ${major}.${minor}.${build} 이상에서 출판해야 동작합니다. (현재 버전: ${window.VERSION.number})`);
        if(!window.VERSION?.number) return warn();
        var ar = window.VERSION.number.split('.').map(n=>parseInt(n));
        if(ar[0] !== major) return ((ar[0] < major) ? warn() : undefined);
        if(ar[1] !== minor) return ((ar[1] < minor) ? warn() : undefined);
        return (ar[2] < build) ? warn() : undefined;
    })(3, 3, 31);

    //-------------------------------------
    // Tab 컴포넌트 구현
    //-------------------------------------

    // 사용
    // new window['jikjiComponent'].Navi.Tab($self, ...);

    function Tab($self, config, onInitialize){

        // 전달된 이름으로 api 객체 찾기
        ((elements)=>{
            // 이전, 다음 버튼
            elements.prevButton = findAPI(elements.prevButton);
            elements.nextButton = findAPI(elements.nextButton);

            // 탭 버튼으로 구성된 그룹
            // 각 버튼의 네이밍 규칙: 탭메뉴01, 탭메뉴02 ...  ~ 탭메뉴00
            elements.tabButtonGroup = findAPI(elements.tabButtonGroup);

            // 탭 컨텐츠로 구성된 그룹
            // 각 컨텐츠의 네이밍 규칙: 탭컨텐츠01, 탭컨텐츠02 ...  ~ 탭컨텐츠00
            elements.tabContentGroup = findAPI(elements.tabContentGroup);

            // ...

            function findAPI(name){
                return (typeof name === 'string') ? $self.find(name, true) : name;
            }
        })(config.elements);

        // 컴폰넌트 구현 코드...

        setTimeout(function (){
            // 초기화 완료 콜백
            if(onInitialize) onInitialize();
        }, 250);
    }

    //-------------------------------------
    // Export
    //-------------------------------------

    if(!component.Navi) component.Navi = {};
    if(!component.Navi.Tab) component.Navi.Tab = Tab;
    window['jikjiComponent'] = component;

})(window['jikjiComponent'] || {});

```

주목할 부분은  컴포넌트 객체를 `window['jikjiComponent'].Navi.Tab` 으로 전역 범위에  설정 했습니다. 이는 나중에 `loadComponent` API 사용할때 `name` 속성으로 전달되어 컴포넌트  객체를 찾는데용됩니다.

**컴포넌트 로드할때 이름으로사용됨**&#x20;

```
    // 컴포넌트 설치 정보
    const component = {
        // 컴포넌트 소스 파일에서 정의한 component 객체 참조 문자열
        name: 'jikjiComponent.Navi.Tab',
        // 컴포넌트 소스 파일 경로--
        // (_share 폴더 아래에 중복되지 않을만한 경로가 좋음)
        source: './_share/jikji.component/Navi/Tab.0.0.1.js'
    }
```

