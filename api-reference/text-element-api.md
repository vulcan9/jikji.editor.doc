# Text Element API

## Element 공통 API

[Element 공통 API ](text-element-api.md#text-element-api)문서 내용을 참고하세요.

## Text Element API

텍스트를 표시할 수 있는 Text Element 관련 API 입니다. ![](../.gitbook/assets/reference\_05.png)

#### Text api 객체

* _**api**_
  *   **text (value: String, stateName: String): String**

      텍스트 내용을 가져오거나 변경합니다.

      ```javascript
      // Getter
      var textValue = $self.api.text();

      // Setter
      $self.api.text('표시될 문자열');
      $self.api.text('표시될 문자열', 'over');
      ```
  * **overflowX (value: String, stateName: String): String**\
    value: 'auto', 'scroll', 'hidden'
  * **overflowY (value: String, stateName: String): String**
  *   **overflowVisible (value: Boolean, stateName: String): String**

