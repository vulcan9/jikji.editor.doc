# Jik-ji API for Javacript

Jik-ji API (`jj-API`) 는 Jik-ji 저작툴에서 각 문서에 생성한 요소들을 보다 확장성 있게 컨트롤 하기위해 정의된 API 입니다.

`jj-API`가 제공되는 목적은 저작툴에서 직관적으로 만들어진 각 DOM 요소들을 script에서 찾아내어 보다 디테일한 동작을 제어하는 것입니다. 따라서 API에서 DOM 요소를 찾는 것이 중요합니다.

DOM을 찾았으면 여기에 style등을 지정하는 방법으로 제어할 수도 있겠지만 Jik-ji에서 생성된 DOM을 (Jquery등의 라이브러리를 사용하여) 직접적으로 다루는 것은 예상과 다른 결과가 나올 수있으니 되도록 사용하지 않는 것이 좋습니다.

다음 메서드와 속성을 통해 문서에 삽입된 모든 element 요소에 접근할 수 있습니다.

```javascript
- window.$this 속성
- (api 객체).document 속성
- (api 객체).find() 메서드
- (api 객체).findAll() 메서드
```

정확히 말하면 위 메서드와 속성을 통해 element가 자지고 있는 API 객체를 찾을 수 있습니다. API 객체의 `dom` 속성을 통해 DOM 객체를 참조할 수 있으나 위에서 얘기했듯이 직접 다루는 것 보다는 API를 통해 제어하는 것을 권합니다. 다음 코드는 보이기/감추기 기능을 가진 토글 버튼을 만드는 간단한 예입니다.

```javascript
var buttonAPI = window.$this.find('버튼 아이디');
buttonAPI.on('click', function(){
    var targetAPI= window.$this.find('target 아이디');
    targetAPI.toggleVisible();
});
```

실제 기능을 구현하다 보면 DOM을 찾는 것이 목적이 아니라 찾은 DOM을 제어하는 것이 목적이므로 `jj-API`는 `dom`이 아닌 API간 연결고리에 의해 원하는 기능이 제작 됩니다. API 지원이 되지않아 어쩔수 없는 경우도 있겠지만 다음 원칙을 지키는것이 좋습니다.

```
JJ-API로 해결할 수 있다면 DOM 객체를 직접 조작하지 않고 API 사용을 먼저 고려해 봅니다.
```
