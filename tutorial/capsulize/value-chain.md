# 하위 요소에 값 전달

서로 다른 요소들간에 값을 전달하는 일반적인 방법은 다음과 같습니다.

#### Element에서 다른 Element로 값을 전달하는 경우

```
var selfContext = $this.children('element uid');
selfContext['속성 이름'] = '값';
```

#### document에서 Element로 값을 전달하는 경우

```
$(function(){
  var selfContext = $this.children('element uid');
  selfContext['속성 이름'] = '값';
});
```

#### 전달받은 값 사용

전달받은 값은 `$self` 속성을 통해 접근할 수 있습니다.

```
// Element의 이벤트 창(스크립트 설정창)에서 값 사용
console.log($self['속성 이름']);
// '값' 출력됨.
```

#### HTML Element의 스크립트 편집창에서 사용

`capsule` 객체에 설정된 값을 HTML Element의 내부 script에서 참조하고 싶은 경우 다음과 같이 값을 전달할 수 있습니다.

1. 캡슐화 기능을 사용하여 `capsule` 객체를 설정합니다.
2.  다음 코드로 HTML Element에 값을 할당합니다.

    ```
    var selfContext = $this.children('html element uid');
    selfContext['속성 이름'] = $self.capsule;
    ```
3.  HTML Element의 코드 편집창에서 전달된 값을 사용합니다.

    ```
    // 전달된 capsule 값 참조.
    $self['속성 이름'];
    ```

