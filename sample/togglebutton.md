# 토글 버튼

버튼을 클릭 할때마다 이미지가 보이기/감추기를 반복하는 토글 버튼을 만들겠습니다.

## UI 구성

* 먼저 paper에 `이미지` element 하나를 드래그하여 생성합니다.
* 적당한 이미지 소스를 적용합니다. 저는 간단한 아이콘 이미지를 적용했습니다.

![](../.gitbook/assets/r\_01.png)

*   속성창에서 `over` 또는 `down` 탭을 클릭하여 state 설정을 바꿉니다. \


    체크박스도 함께 선택하여 속성창을 활성화 시킵니다.

![](../.gitbook/assets/r\_02.png)

*   버튼을 눌렀을때 나타날 이미지를 선택하여 적용합니다. \


    그리고 체크박스를 다시 비활성화 상태로 선택합니다.

![](../.gitbook/assets/r\_03.png)

```
이미지를 불러온 뒤 `over` state를 비활성 시킨 이유는 
`over` 상태 마우스 동작은 사용하지 않고 `over` 상태에 적용된 이미지만을 코드에서 사용하기 위함입니다.
토글 상태의 이미지 경로를 http:// 경로로 사용한다면 `normal` 상태의 이미지만 설정해도 됩니다.
```

* 토글 버튼을 누를 때마다 보이기/감추기 하게될 이미지를 생성합니다.

![](../.gitbook/assets/r\_04.png)

## 코드 작성

Component로 만들기 위해 `이벤트 설정` 창에서 코드를 작성하겠습니다. 버튼을 선택한 상태에서 `이벤트 설정` 창을 열어 `스크립트 작성` 항목을 선택합니다.

`initialize` 이벤트에 다음 코드를 작성합니다.

### 토글 버튼 구현

```javascript
// 토글 버튼 커서 모양 설정
$self.setStyle('cursor', 'pointer');

// 토글 버튼 Element에 임시 변수를 저장
$self.scope.toggle = false;

// 토글 상태 업데이트(초기화)
update();

// 클릭 이벤트 핸들러 설정
$self.on('click', function(){
  $self.scope.toggle = !$self.scope.toggle;
  update();
});

function update(){
  if($self.scope.toggle){
    // `over` 이미지 불러올때 생성된 Asset UID
    $self.api.source('asset-173d0e08-0197-4c74-9884-5a68dea47941');
  }else{
    // `normal` 이미지 불러올때 생성된 Asset UID
    $self.api.source('asset-dcaf5929-38e8-43cc-bbc5-07f2109a1b7b');
  }
}
```

### 이미지 toggle 기능

`update()` 함수 내용을 수정합니다.

```javascript
function update(){
  // 이미지 Element 찾기
  var image = $self.children('element-5445d04c-6129-494b-90cd-e0c967206f27');

  if($self.scope.toggle){
    // `over` 이미지 불러올때 생성된 Asset UID
    $self.api.source('asset-173d0e08-0197-4c74-9884-5a68dea47941');
    // 이미지 보이기
    image.show();
  }else{
    // `normal` 이미지 불러올때 생성된 Asset UID
    $self.api.source('asset-dcaf5929-38e8-43cc-bbc5-07f2109a1b7b');
    // 이미지 감추기
    image.hide();
  }
}
```

### 토글 버튼 결과

*   한번 클릭으로 Toggle (true) 상태

    ![](../.gitbook/assets/r\_05.png)
