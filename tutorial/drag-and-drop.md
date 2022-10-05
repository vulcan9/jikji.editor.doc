# Drag & Drop 기능 사용하기

## 드래그 기능 설정

```
// 마우스 기능 생성 id
_mouseID = '드래그 마우스 이벤트 ID';

// dnd 기능 식별 (id)
_dndID = '드래그&드랍 아이디';

removeUI(){
    if(!this._mouseID) return;

    this.$self.dnd.removeDrag(this._mouseID);
    this.$self.dnd.destroy(this._mouseID);

    this._mouseID = null;
    this._dndID = null;
}

createUI() {
    this.$self.dnd.create(this._mouseID);
    this.$self.dnd.setDrag(this._mouseID , {
        id: this._dndID,
        element: this.$self.uid,
        ghostName: 'ghost-drager-container',

        dragStart: this.onDragStart.bind(this),
        dragEnd: this.onDragEnd.bind(this)
    });
}

onDragStart(e, dragData){
    // e.preventDefault();

    // ghost 이미지 표시 위해 id가 필요함
    dragData.selects = {
        id: this._mouseID
    };
    // document.body.classList.add("being-dragged");
    
    // drop 이벤트으로 임의의 데이터 전달
    dragData.start = '드래그 시작 값 설';
}

onDragEnd(e, dragData){
    // console.error("being-dragged");
    // document.body.classList.remove("being-dragged");
}
```

## 드랍 기능 설정&#x20;

```
// 마우스 기능 생성 id
_mouseID = '드랍 마우스 이벤트 ID';

// dnd 기능 식별 (id)
_dndID = '드래그&드랍 아이디';

removeUI(){
    if(!this._mouseID) return;

    this.$self.dnd.removeDrop(this._mouseID);
    this.$self.dnd.destroy(this._mouseID);

    this._mouseID = null;
    this._dndID = null;
}

createUI() {
    this.$self.dnd.create(this._mouseID);
    this.$self.dnd.setDrop(this._mouseID , {
        id: this._dndID,
        element: this.$self.uid,

        isDropAllowed: this.isDropAllowed.bind(this),
        dragEnter: this.onDragEnter.bind(this),
        dragOver: this.onDragOver.bind(this),
        dragLeave: this.onDragLeave.bind(this),
        drop: this.onDrop.bind(this)
    });
}

// dragData, dropData 는 드래그 이벤트에서 설정된 값임
isDropAllowed(dragData) {
    return (dragData && dragData.selects);
}

onDragEnter(e, dragData){}

onDragOver(e, dragData){
    dragData.end = '드랍했을때 전달값 지정';
}

onDragLeave(e, dropData){}

onDrop(e, dropData){
    console.error('Drag&Drop 결과: ', dropData.start, '-->', dropData.end);
}
```
