# Youtube Element API

## Element 공통 API

[Element 공통 API ](web-element-api-1.md#text-element-api)문서 내용을 참고하세요.

## Youtube Element API

유튜브 페이지를 로드할 수 있는  Youtube Element 관련 API 입니다.&#x20;

#### Youtube api 객체

*   _**api**_

    *   **source (url: String): String**

        youtube element에 로드할 url을 설정합니다.

        ```javascript
        // Getter
        var src = $self.api.source();
        // Setter
        $self.api.source('https://www.youtube.com/embed/(유튜브 비디오 아이디)');
        ```


    * 유튜브 `비디오 아이디` 및 embed 주소를   얻는 방법은 다음과 같습니다.&#x20;
      *   유튜브 페이지를 열고 브라우저 주소창에서 주소를 복사

          ```
          주소는 다음 형식입니다.
          https://www.youtube.com/watch?v=(유튜브 비디오 아이디)
          ```
      *   유트브 비디오 화면에서 오른쪽 마우스 버튼을 눌러 메뉴에서 `동영상 URL 복사` 메뉴 선택

          ```
          주소는 다음 형식입니다.
          https://youtu.be/(유튜브 비디오 아이디)
          ```
      *   유튜브 페이지에서 공유 버튼을  눌러  주소를 복사

          <pre><code><strong>주소는 다음 형식입니다.
          </strong><strong>https://www.youtube.com/embed/(유튜브 비디오 아이디)
          </strong></code></pre>



    *   **getPlayer (): Object**\
        로드된 유튜브를  제어할 수 있는 기능을 가진 player 객체를 리턴합니다. \
        [player 기능에 대한 문서](https://developers.google.com/youtube/iframe_api_reference?hl=ko#Functions)를 참조하여 이벤트와 함수 기능을 활용할 수 있습니다.\


        ```javascript
        // API를사용하여 동영상을 로드한 후 volume을 조절하는 예
        // youtube element의 initialize 이벤트에서 스크립트를 작성함
        $self.api.source('https://www.youtube.com/watch?v=M7lc1UVf-VE');

        $self.on('ready', (e)=>{
            // player : e.originalEvent.detail.target
            var player = $self.api.getPlayer();
            player.setVolume(100);
        });

        // ready 이벤트 전에는 player 기능이 제한적임
        // 자동 재생 기능은 실행환경에 따라 제한적으로 구현 가능함 (예: mute 상태일때)
        ```

## Youtube  API 참고 문서

* [유튜브 IFrame API](https://developers.google.com/youtube/iframe_api_reference?hl=ko)
* [플레이어 매개변수](https://developers.google.com/youtube/player_parameters?hl=ko#Parameters)
* #### [자동 재생 유의사항](https://developers.google.com/youtube/iframe_api_reference?hl=ko#Autoplay_and_scripted_playback) <a href="#autoplay_and_scripted_playback" id="autoplay_and_scripted_playback"></a>
