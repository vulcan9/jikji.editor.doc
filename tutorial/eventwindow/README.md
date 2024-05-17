# 이벤트 설정창에서 코드 작성 도움말

기본적으로 사용하는 API 내용은 [API Reference](../../api-reference/jjapi.md) 내용과 같으므로 차이나는 점만 설명 하겠습니다.

외부 JS 파일을 임포트하는 것과 달리 이벤트 설정창에서는 단편적인 코드를 작성하는 것으로 원하는 기능을 구현할 수 있습니다.

### 코드 작성 절차

1. 원하는 element를 화면에서 선택\
   ![](../../.gitbook/assets/eventwindow\_01\_1.png)
2. 왼쪽 이벤트 메뉴에서 실행 시점(이벤트)을 결정\
   ![](../../.gitbook/assets/eventwindow\_01\_2.png)
3. `add action` 버튼을 눌러 이벤트 설정창을 뛰우기\
   ![](../../.gitbook/assets/eventwindow\_01\_3.png)
4. `코드 작성` 박스에 실행할 코드를 입력\
   ![](../../.gitbook/assets/eventwindow\_01.png)
5. 런타임에 element 생성이 완료된 후 해당 이벤트가 발생했을때 실행되게 됩니다.
6. 같은 이벤트에 여러개의 스크립트 코드를 추가할 수 있고, 추가된 코드들은 그림에서와 같이 추가된 순서대로 정렬됩니다. 이것은 런타임에 코드가 실행되는 순서와 같습니다.\
   ![](../../.gitbook/assets/eventwindow\_01\_4.png)
