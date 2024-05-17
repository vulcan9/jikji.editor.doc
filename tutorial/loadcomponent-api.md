---
description: 컴포넌트를 만들어 배포하는 방법을 설명합니다.
---

# loadComponent API를 이용하여 컴포넌트 작성하기



&#x20;`jikji 3.3.31` 버전 이상에서 지원되는 `loadComponent` API를 이용하여 컴포넌트를 작성하는 방법을 소개합니다. \
컴포넌트에 대한 기본적인 내용은 [Element에서 JS 파일 동적으로 로드](element-js.md) 페이지를 참고하세요



먼저 직지에서 그룹을 하나 생성한 후 그룹 내부에 컴포넌트에서 사용할 element 요소들을 디자인 합니다.\


<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Tab 네비게이션 그룹 내부에 요소들을 배치</p></figcaption></figure>

Tab 네비게이션 그룹을 선택한 후 `initialize` 이벤트에 스크립트를 추가합니다.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

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

작업   내용은 다음과 같습니다.

* 외부 JS 파일에 컴포넌트를 구현합니다.
* 이벤트 창에서 컴포넌트가 구현된 JS 파일을 로드합니다.
* 이벤트 창에서는 컴포넌트 구현에 필요한 정보를 컴포넌트 구현 객체에  넘겨줍니다.
  * element 요소들을 참조할 수 있도록 이름 정보
  * 컴포넌트 설정 옵션
  * 컴포넌트 초기화 완료 후 실행할 콜백함수

외부 JS 파일에 컴포넌트를 구현하면 다음과 같은 장점이 있습니다.

이벤트 코드 창에 컴포넌트 구현로직이 있으면 컴포넌트를 생성할때 또는  Element를  복사해서 사용할때마다 코드 복제본이 생성되게 되어 코드 수정 및 관리가 어려워 집니다.

