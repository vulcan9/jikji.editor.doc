# media 객체

*   _**media: Object**_

    Video/Audio element를 제어하기 위한 API를 제공합니다. media element에서 사용하는 경우 `params.target`을 생략하면 자기 자신을 컨트롤 합니다. window API에서 사용하는 경우 반드시 `params.target`(제어 대상 media)을 설정해야 합니다.

    ```javascript
    // target media의 uid 찾기
    var uid = $this.find('media 아이디').uid;
    var params = {
      target: uid
    };
    ```

    *   _**media.pause (params: Object, callback: Function): void**_

        미디어를 일시 정지 합니다.

        * params: **Object**&#x20;
          *   target : **String** \


              미디어 Element의 uid값

        ```javascript
        window.$this.media.pause({target:uid});
        ```
    *   _**media.play (params: Object, callback: Function): void**_

        미디어를 재생 합니다.

        * params: **Object**&#x20;
          *   target : **String**\


              미디어 Element의 uid값

        ```javascript
        window.$this.media.play({target:uid});
        ```
    *   _**media.stop (params: Object, callback: Function): void**_

        미디어가 재생중이면 재생을 멈춤니다.

        * params: **Object**&#x20;
          *   target : **String**\


              미디어 Element의 uid값

        ```javascript
        window.$this.media.stop({target:uid});
        ```
    *   _**media.togglePlay (params: Object, callback: Function): void**_

        미디어 재생과 멈춤 (또는 일시정지)를 반복 합니다.

        * params: **Object**&#x20;
          *   target : **String**\


              미디어 Element의 uid값
          *   toggleValue : **String** \


              toggle 동작시 멈춤 동작을 할것인지 일시정지 할것인지를 설정.\


              일시정지("pause"). 멈춤("stop")

        ```javascript
        window.$this.media.togglePlay({
          target:uid, 
          toggleValue:"pause"
        });
        ```
    *   _**media.stopAllSound (param: Object): void**_

        재생중인 모든 미디어의 동작을 정지(또는 일시정지) 합니다.

        * params: **Object**&#x20;
          *   toggleValue : **String** \


              toggle 동작시 멈춤 동작을 할것인지 일시정지 할것인지를 설정.\


              일시정지("pause"). 멈춤("stop")

        ```javascript
        window.$this.media.stopAllSound({
          toggleValue:"pause"
        });
        ```
    *   _**media.toggleFullScreen (params: Object): void**_

        Video를 Fullscreen 모드로 전환 합니다. (Only video)

        * params: **Object**&#x20;
          *   target : **String**\


              미디어 Element의 uid값

        ```javascript
        window.$this.media.toggleFullScreen({target:uid});
        ```
    *   _**media.config (params: Object, callback: Function): void**_

        media 속성을 설정 합니다.

        * params: **Object**
          * target : **String** 미디어 Element의 uid값
          * controls : **Boolean | String** 컨트롤러 보이기 상태를 설정. 설정(true), 해지(false), 토글("toggle")
          * currentTime : **Number** 재생 위치(시간)
          * loop : **Boolean | String** loop 재생을 설정. 설정(true), 해지(false), 토글("toggle")
          * muted : **Boolean | String** 묵음 상태를 설정. 설정(true), 해지(false), 토글("toggle")
          * src : **String** 미디어가 위치한 http 경로
          * volume : **Number** 소리 조절 (0\~1)

        ```javascript
        window.$this.media.config({
          target:uid,
          muted: true
        });
        // 해당 media가 묵음처리 되었습니다.
        ```
    *   _**media.control (name: String, params: Object, callback: Function): void**_

        media API를 문자열 이름으로 호출하는 방식을 제공합니다.

        * name : **String** 호출하고자 하는 media API의 이름. ("play", "stop", "pause", "togglePlay"...)
        * params : **Object** name에 해당되는 media API에 설명된 내용과 같습니다.

        ```javascript
        window.$this.media.control('play', {
          target:uid
        });

        // window.$this.media.play() API가 실행된것과 같습니다.
        ```
