# Image Element API

## Element 공통 API

[Element 공통 API ](image-element-api.md#text-element-api)문서 내용을 참고하세요.

## Image Element API

이미지를 표시할 수 있는 Image Element 관련 API 입니다. ![](../.gitbook/assets/reference\_07.png)

#### Image api 객체

* _**api**_
  *   **source (value: String, stateName: String): String**

      이미지 경로를 가져오거나 설정합니다.

      ```javascript
      // Getter
      var src = $self.api.source();

      // Setter
      $self.api.source('http://이미지 경로');
      $self.api.source('http://이미지 경로', 'over');

      // asset UID를 사용할수 있음
      $self.api.source('asset-87f315a5-b31f-4379-b57a-9a2ab1f5a21c');
      ```

##
