# Web Element API

## Element 공통 API

[Element 공통 API ](web-element-api.md#text-element-api)문서 내용을 참고하세요.

## Web Element API

web 페이지를 로드할 수 있는 Web Element 관련 API 입니다. ![](../.gitbook/assets/20181206\_113333.png)

#### Web api 객체

* _**api**_
  *   **source (value: String, stateName: String): String**

      web element에 로드할 url을 설정합니다.

      ```javascript
      // Getter
      var src = $self.api.source();
      // Setter
      $self.api.source('http://web 페이지 url');
      ```

      다음 같은 방법으로 웹 페이지를 로드하는 Toggle 버튼을 만들 수 있습니다.

      ```javascript
      var web = $self.children('element-4f4a6eef-4fac-4b5b-8855-9c6a40a9761a');
      var currentUrl = web.api.source();
      if(currentUrl){
          web.api.source('');
      }else{
          web.api.source('http://naver.com');
      }
      ```
