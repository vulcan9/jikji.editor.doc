# dnd 객체 (Drag \&Drop )

dnd 객체를 이용하면 드래그 & 드랍 기능을 구현할 수 있습니다.\
실제 사용 예제는 [Drag & Drop 기능 사용하기](../../tutorial/drag-and-drop.md)를 참고하세요.

### _**메서드**_

매개변수 **dndID** 는 마우스 이벤트를 구분하는 구분자로 사용됩니다. \
객체끼리 드래그 또는 드랍이 서로 가능한지 여부는 `setDrag`, `setDrop`에 전달되는 `id` 값으로 판별합니다. (`id` 값이 같아야 drop 가능합니다.)

* **create (dndID: String): void**\
  dnd 객체의 인스턴스를 생성합니다.\
  이 메서드는 `setDrag` 또는 `setDrop`   메서드 호출 이전에 실행해야 합니다.
* **destroy (dndID: String): void**\
  dnd 객체의 인스턴스를 제거합니다.\
  이 메서드는 `removeDrag` 또는 `removeDrop` 메서드 호출 이후에 실행해야 합니다.
* **setDrag (dndID: String, dragConfig: Object): void**\
  `dragConfig` 설정을 통해 드래그 기능을 구현합니다.\
  `dragConfig` 설정 내용은 아래 내용을 참고하세요.
* **removeDrag (dndID: String): void**\
  드래그 기능을 제거 합니다
* **setDrop (dndID: String, dropConfig: Object): void**\
  `dropConfig` 설정을 통해 드랍 기능을 구현합니다.\
  `dropConfig` 설정 내용은 아래 내용을 참고하세요.
* **removeDrop (dndID: String): void**\
  드랍 기능을 거 합니다.

### dragConfig 매개변수

`dropConfig`에 설정된 `id`와 같은 `id`로 설정된 dnd (drop)객체에 drop 기능이 허용됩니다.

* **id: String**\
  드래그-드랍 동작을 구분하는 고유 아이디
* **element: DOMElement**\
  드래그 기능을 추가할 대상 DOM Element (jquery)
*   **dragStart: Function**\
    드래그 시작 이벤트

    ```
    function(event){}
    ```
*   **dragEnd: Function**\
    드래그 종료 이벤트

    ```
    function(event){}
    ```
* **selects: Array**\
  여러 dnd 객체를 한번에 드래그할때 사용.\
  드래그되는 각 요소를 구분할 수 있는 고유 id를 저장한 후 ghost 또는 drop 할때 식별해서 사용.
* **ghost: Function**\
  ghost 이미지 캡쳐에 사용될 element를 리턴하는 함수

```
// Some code
function (){
  return $element.find('[jj-thumbnail]');
}
```

* **ghostName: String**\
  ghost element에 적용할 CSS Class name
* **ghostSort: Function**\
  ghost에 사용될 리스트 정렬

```
function(selects){
    // 역순으로 정렬
    selects.reverse();
}
```

### dropConfig 매개변

`dragConfig`에 설정된 `id`와 같은 `id`로 설정된 dnd (drag)객체에 drop 기능이 허용됩니다.

* **id: String**\
  드래그-드랍 동작을 구분하는 고유 아이디
* **element: DOMElement**\
  드랍 기능을 추가할 대상 DOM Element (jquery)
*   **dragEnter: Function**

    ```
    function(event){}
    ```
*   **dragLeave: Function**

    ```
    function(event){}
    ```
*   **dragOver: Function**

    ```
    function(event){}
    ```
*   **drop: Function**

    ```
    function(event){}
    ```
