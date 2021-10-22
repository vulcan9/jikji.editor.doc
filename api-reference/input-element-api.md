# Input Element API

## Element 공통 API

[Element 공통 API ](input-element-api.md#text-element-api)문서 내용을 참고하세요.

## Input Element API

텍스트를 입력할 수 있는 입력박스 Element 관련 API 입니다. 입력받은 값은 임시 저장되어 기록에 남아 있게 됩니다. ![](../.gitbook/assets/reference\_06.png)

#### Input api 객체

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

##
