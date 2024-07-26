---
description: 유형별로 컴포넌트 파일을 작성하는 방법을 정리해 보았습니다.
---

# loadComponent API를 이용하여 컴포넌트 작성하기 2

{% hint style="info" %}
직지 3.3.32 버전 이상에서 사용가능한 방법입니다.
{% endhint %}

## case 1. Module type이 아닌 JS 파일경우

#### 컴포넌트 정의 파일

```javascript
//  case 1. CompScript.js 파일 작성
(function(component){
  
  // 컴포넌트 객체 정의
  function Comp($self, config, onInitialize){
    // 컴포넌트 기능 구현...
    
  }

  // Export
  if(!component.Comp) component.Comp= Comp;
  window['jikjiComponent'] = component;

})(window['jikjiComponent'] || {});
```

#### 컴포넌트 로드 방법

```javascript
//  case 1. CompScript.js 파일 로드
// ./_share/jikji.component 폴더는 임의로 저장한 경로임
const component = {
    css: './_share/jikji.component/Comp.css'
    js: './_share/jikji.component/CompScript.js'
}

// 깜빡임 방지 위해 초기화 완료 이전까지 감추기
$self.hide();

$self.loadComponent(component, () => {
    const onInitialize = () => $self.show();
    
    // JS 파일에서 전역 변수에 저장된 객체를 사용함
    const Comp = window['jikjiComponent'].Comp;
    new Comp($self, config, onInitialize);
});
```

## case 2. Module type인 경우 (type='module')

#### 컴포넌트 정의 파일

```javascript
//  case 2. CompModule.js 파일 작성
import {CompBase} from "./CompBase.js";

export class Comp2 extends CompBase{

    constructor($self, config, onInitialize) {
        super($self, config, onInitialize);
        // 컴포넌트 기능 구현...
        
    }

}

export class Comp3 extends CompBase{

    constructor($self, config, onInitialize) {
        super($self, config, onInitialize);
        // 컴포넌트 기능 구현...
        
    }

}

```

#### 컴포넌트 로드 방법 1

```javascript
//  case 2. CompModule.js 파일 로드
// ./_share/jikji.component 폴더는 임의로 저장한 경로임
const component = {
    css: './_share/jikji.component/Comp.css'
    // case 2. module JS 소스 로드한 경우
    js: { type: 'module', './_share/jikji.component/CompModule.js' }
}

// 깜빡임 방지 위해 초기화 완료 이전까지 감추기
$self.hide();

$self.loadComponent(component, (modules) => {
    const onInitialize = () => $self.show();
    
    // 전달된 modules 인자에서 로드한 모듈 파일 경로로 모듈 참조
    const {Comp2, Comp3} = modules['./_share/jikji.component/CompModule.js'];
    new Comp2($self, config, onInitialize);
    new Comp3($self, config, onInitialize);
});
```

#### 컴포넌트 로드 방법 2

다음 방법은 일반적이지 않아 권장하지는 않지만 사용 가능한 코드입니다.

{% hint style="info" %}
`document.baseURI` 속성값이 `OPS` 폴더를 가리키고 있을때 사용 가능합니다.
{% endhint %}

initialize 이벤트에 코드 등록합니다.

```javascript
// 깜빡임 방지 위해 초기화 완료 이전까지 감추기
$self.hide();

import(document.baseURI + "_share/jikji.component/Media/CompModule.js")
    .then(onLoaded)
    .catch(onError);
    
function onLoaded(module){
    const onInitialize = () => $self.show();
    new module.Comp2($self, config, onInitialize);
}  
function onError(err){
    console.error('모듈 로드에러: ', err);
}
```
