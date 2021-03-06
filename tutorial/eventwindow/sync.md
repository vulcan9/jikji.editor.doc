# 동기/비동기 실행

`이벤트 동작 설정` 창의 하단에는 그림과 같이 실행 순서를 선택하는 체크박스가 하나 있습니다. 추가된 코드가 `동기적`으로 실행이되는지 아니면 `비동기적`으로 실행되는지 확인하는 옵션입니다.

![](../../.gitbook/assets/eventwindow\_02\_1.png)

### 동기 (synchronous)

`동기적`이란 말은 앞의 코드가 실행되기 전 그다음 코드가 실행될 수 없음을 뜻합니다. 대부분의 코드는 동기적으로 실행됩니다. 예를 들면 다음과 같이 동기적으로 실행되는 코드는 첫째줄이 완전히 실행된 후 그 결과값을 두번째 줄에서 사용할 수 있습니다.

```javascript
var result = someFunction();
// 위에서부터 순차적으로 실행되므로 result값을 사용할 수 있습니다.
console.log(result);
```

### 비동기 (asynchronous)

`비동기적`이란 말은 코드가 실행될때 시간적인 delay를 거친 후 실행이 완료되는 경우 입니다. 따라서 선행된 코드의 결과를 그다음줄에서 바로 사용할 수 없습니다. 예를 들면 시간관련 함수를 호출할때, http 통신으로 데이터를 불러올때 일정 시간뒤 그 결과를 받아오므로 모두 비동기적으로 동작한다고 할 수 있습니다.

```javascript
var result = '동기적'
setTimeout(function(){
  result = '비동기적';
}, 1000);
// 여기에서 result 값은 '동기적을 출력'
console.log(result);
```

위에서 이벤트에 추가된 스크립트들은 순서대로 실행이 된다고 하였습니다. 먼저 실행된 코드는 그 결과값(`$result`)을 그다음에 실행된 코드에 전달할 수 있습니다. 하지만 `비동기`로 실행되는 코드에서는 그 결과값을 다음 코드에 바로 넘기기 어려우므로 코드 작성자가 직접 그 다음 코드를 실행할 시점을 알려주어야 합니다.

`비동기` 옵션이 선택된 코드는 실행 후 그 다음 단계로 바로 이동하지 않습니다. 코드 실행이 완료됬다고 판단될때 미리 정의된 함수 `resolve()` 또는 `reject()`를 호출하면 그제서야 다음 코드가 실행되면서 결과값도 함께 전달됩니다.

간단한 예를 들어보겠습니다.

### 동기적으로 동작하는 코드 만들기

첫번째 코드가 실행된 결과값을 두번째 코드에서 받아 보여주는 예제를 만들어 보겠습니다.

* 원하는 element를 화면에서 선택\
  ![](<../../.gitbook/assets/eventwindow\_01\_1 (1).png>)
* `on click` 이벤트의 `코드 작성` 박스에 첫번째 실행할 코드를 입력합니다.

```javascript
var data = '기본값';
// return 값을 지정하면 두번째 코드에 전달됩니다.
return data;
```

* `add action` 버튼을 한번 더 눌러 `on click` 이벤트의 `코드 작성` 박스에 두번째 실행할 코드를 입력합니다. 첫번째 코드에서 전달한 값은 `$result` 변수로 참조할 수 있습니다.

```javascript
alert($result);
```

* 코드 작성이 다 되었으면 두개의 스크립트가 추가되어져 있을 것입니다.

![](../../.gitbook/assets/eventwindow\_02\_3.png)

* 미리보기를 하여 버튼을 클릭하면 다음과 같이 값이 전달 되었음을 확인할 수 있습니다.

![](../../.gitbook/assets/eventwindow\_02\_2.png)

### 비동기적으로 동작하는 코드 만들기

같은 방법으로 전달된 값을 보여주기는 하되, 첫번째 코드가 실행된 1초 후에 실행 결과값을 두번째 코드에서 보여주는 예제를 만들어 보겠습니다.

* 원하는 element를 화면에서 선택\
  ![](<../../.gitbook/assets/eventwindow\_01\_1 (2).png>)
* `on click` 이벤트의 `코드 작성` 박스에 첫번째 실행할 코드를 입력합니다.

```javascript
var run = ($asynchronous) ? '비동기 실행 : ' : '동기 실행 : ';
var server_data = '기본값';

// 시간 지연
setTimeout(function(){
  server_data = '서버에서 전달받은 값';
  // 첫번째 코드 실행이 완료됨을 알림
  $resolve(run + server_data);
}, 1000);

// 동기 실행 결과값을 보기 위해 리턴값을 보내줘 보자.
return run + server_data;
```

* `실행 순서` 체크박스를 선택하여 `비동기` 실행 코드임을 선택합니다.&#x20;
* 코드에서는 `$asynchronous` 변수로 현재 실행 코드가 비동기(`true`) 실행인지 아닌지(`false`) 알수 있습니다.

![](../../.gitbook/assets/eventwindow\_02\_4.png)

* `add action` 버튼을 한번 더 눌러 `on click` 이벤트의 `코드 작성` 박스에 두번째 실행할 코드를 입력합니다.&#x20;
* 첫번째 코드에서 전달한 값은 `$result` 변수로 참조할 수 있습니다.

```javascript
alert($result);
```

* 두번째 코드에는 `실행 순서` 체크 박스를 선택하지 않아도 됩니다.
* 미리보기를 하여 버튼을 클릭하면 다음과 같이 값이 전달 되었음을 확인할 수 있습니다.

![](../../.gitbook/assets/eventwindow\_02\_5.png)

* `resolve()` 함수 대신 `reject()` 함수를 호출하면 현재 실행 코드를 마지막으로 실행이 종료됩니다. 이후 실행될 코드가 있다 하더라도 모두 무시됩니다.
* 만약 첫번째 코드에서 `실행 순서` 체크박스를 선택하지 않고 실행한다면 다음과 같은 결과가 표시됩니다.

![](../../.gitbook/assets/eventwindow\_02\_6.png)

* 1초 후에 `resolve()` 함수가 호출된다 해도 두번째 코드는 이미 동기적으로 호출이 됬으므로 다시 두번째 코드를 호출하지 않게 됩니다.
