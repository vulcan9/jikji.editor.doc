# Video/Audio Element API

## Element 공통 API

[Element 공통 API ](mediaapi.md#text-element-api)문서 내용을 참고하세요.

## Media Element API

Media를 설정하고 제어할 수 있는 Video/Audio Element 관련 API 입니다. ![](../.gitbook/assets/reference\_08.png)

* _**api**_
  *   _**pause (params: Object, callback: Function): void**_

      미디어를 일시 정지 합니다.

      * params: **Object**

      ```javascript
      $self.api.pause();
      $self.api.pause(null, callback);
      $self.api.pause({}, callback);
      function callback(){}
      ```
  *   _**play (params: Object, callback: Function): void**_

      미디어를 재생 합니다.

      * params: **Object**

      ```javascript
      $self.api.play();
      $self.api.play(null, callback);
      $self.api.play({}, callback);
      function callback(){}
      ```
  *   _**stop (params: Object, callback: Function): void**_

      미디어가 재생중이면 재생을 멈춤니다.

      * params: **Object**

      ```javascript
      $self.api.stop();
      $self.api.stop(null, callback);
      $self.api.stop({}, callback);
      function callback(){}
      ```
  *   _**togglePlay (params: Object, callback: Function): void**_

      미디어 재생과 멈춤 (또는 일시정지)를 반복 합니다.

      * params: **Object**
        *   toggleValue : **String** \


            toggle 동작시 멈춤 동작을 할것인지 일시정지 할것인지를 설정.\


            일시정지("pause"). 멈춤("stop")

      ```javascript
      $self.api.togglePlay();
      $self.api.togglePlay(null, callback);
      $self.api.togglePlay({toggleValue: 'stop'}, callback);
      function callback(){}
      ```
  *   _**toggleFullScreen (params: Object, callback: Function): void**_

      Video를 Fullscreen 모드로 전환 합니다. (Only video)

      * params: **Object**

      ```javascript
      $self.api.toggleFullScreen();
      $self.api.toggleFullScreen(null, callback);
      $self.api.toggleFullScreen({}, callback);
      function callback(){}
      ```
  *   _**autoplay (params: Object): Boolean**_

      자동재생 설정 여부를 설정하거나 설정값을 가져옵니다.

      * params: **Object**
        *   value: **Boolean** \


            자동 재생(true). 재생 대기(false)

      ```javascript
      // Getter
      var auto = $self.api.autoplay();

      //Setter
      $self.api.autoplay({value: true});
      $self.api.autoplay(true);
      ```
  *   _**controls (params: Object): Boolean**_

      컨트롤러 보이기 상태를 설정.

      * params: **Object**
        *   value: **Boolean | String** \


            설정(true), 해지(false), 토글("toggle")

      ```javascript
      // Getter
      var visible = $self.api.controls();

      //Setter
      $self.api.controls({value: true});
      $self.api.controls({value: 'toggle'});
      $self.api.controls('toggle');
      $self.api.controls(false);
      ```
  *   _**currentTime (params: Object): Number**_

      재생 위치(시간), second 단위.

      * params: **Object**
        *   value: **Number** \


            이동할 재생 시간(위치, second)

      ```javascript
      // Getter
      var time = $self.api.currentTime();

      //Setter
      $self.api.currentTime({value: 10});
      $self.api.currentTime(10);
      // 재생 위치를 10초로 이동됨
      ```
  *   _**loop (params: Object): Boolean**_

      loop 재생을 설정.

      * params: **Object**
        *   value: **Boolean | String** \


            설정(true), 해지(false), 토글("toggle")

      ```javascript
      // Getter
      var visible = $self.api.loop();

      //Setter
      $self.api.loop({value: true});
      $self.api.loop({value: 'toggle'});
      $self.api.loop('toggle');
      $self.api.loop(false);
      ```
  *   _**muted (params: Object): Boolean**_

      묵음 상태를 설정.

      * params: **Object**
        *   value: **Boolean | String** \


            설정(true), 해지(false), 토글("toggle")

      ```javascript
      // Getter
      var isMuted = $self.api.muted();

      //Setter
      $self.api.muted({value: true});
      $self.api.muted({value: 'toggle'});
      $self.api.muted('toggle');
      $self.api.muted(false);
      ```
  *   _**src (params: Object): String**_

      미디어가 위치한 http 경로

      * params: **Object**
        *   value: **String** \


            미디어 경로 문자열

      ```javascript
      // Getter
      var src = $self.api.src();

      //Setter
      $self.api.src({value: 'http://미디어 경로'});
      $self.api.src('http://미디어 경로');
      ```
  *   _**volume (params: Object): Number**_

      소리 조절 (0\~1)

      * params: **Object**
        *   value: **Number** \


            0 (최소)에서 1 (최대)사이의 값

      ```javascript
      // Getter
      var volume = $self.api.volume();

      //Setter
      $self.api.volume({value: 0.5});
      $self.api.volume(0.5);
      ```
  *   _**config (params, callback): void**_

      media 속성을 한꺼번에 설정 합니다.

      * params: **Object**
        * currentTime : **Number** 재생 위치(시간)
        * loop : **Boolean | String** loop 재생을 설정. 설정(true), 해지(false), 토글("toggle")
        * muted : **Boolean | String** 묵음 상태를 설정. 설정(true), 해지(false), 토글("toggle")
        * controls : **Boolean | String** 컨트롤러 보이기 상태를 설정. 설정(true), 해지(false), 토글("toggle")
        * src : **String** 미디어가 위치한 http 경로
        * volume : **Number** 소리 조절 (0\~1)
        * autoplay : **Boolean | String** 자동재생 설정. 자동 재생(true), 재생 대기(false)
        * callback: **Function** `params.src` 설정이 있는 경우에만 재생 준비가 되었을때 호출됩니다. `params.src` 설정이 없는 경우 호출되지 않으므로 생략합니다.

      ```javascript
      $self.config({
        src: 'http 경로',
        autoplay: true,
        controls: true,
        loop: false
      }, callback);
      function callback(){
        // params에 src 설정이 있는 경우에만 (재생 준비가 되었을때) 호출됩니다.
      }
      ```
  *   _**dispose (): void**_

      media 객체의 연결을 끊고 media player를 화면에서 완전히 제거합니다. (DOM에서도 삭제됨)

      ```javascript
      $self.api.dispose();
      ```
  *   _**duration (): Number**_

      (읽기 전용) media 소스가 연결되면 전체 재생 시간을 반환합니다. 재생이 불가능한 상황일때에는 0을 반환합니다.

      ```javascript
      $self.api.src('http://미디어 경로');
      $self.on('durationchange', function(){
        var runningTime = $self.api.duration();
      });
      ```
  *   _**formatTime (second: Number, guide: Number): String**_

      초(second) 단위의 숫자를 time 형식의 문자열로 변환해 줍니다. (예) 150 (초) ------> "0:02:30"

      *   second: **Number** \


          변환하려고 하는 시간(초)
      *   guide: **Number** \


          시간으로 변환할때 포맷을 알려줄 임의의 시간 (주로 duration). \


          여기에 전달하는 값이 `h:m:s` 형식으로 나타나기에 충분히 큰 값이면 실제 변환될 second도 `h:m:s` 포맷으로 문자열이 구성됩니다.

      ```javascript
      $self.api.formatTime(150); // "2:30"
      $self.api.formatTime(1000);// "16:40"
      $self.api.formatTime(150, 1000); // 02:30 (1000 값이 포맷을 결정함)

      $self.api.formatTime(10000);// "2:46:40"
      $self.api.formatTime(150, 10000); // "0:02:30" (시간까지 표기됨)

      // 전체 재생시간을 전달하면 포맷을 자동으로 조정할수 있다.
      var currentTime = $self.api.currentTime();
      var duration = $self.api.duration();
      $self.api.formatTime(currentTime, duration) + ' / ' + $self.api.formatTime(duration)
      // "0:25:00 / 8:20:00" 형식으로 출력됨
      ```
  *   _**parseTime (timeText: String): Number**_

      `formatTime()` API와 반대로 time 형식의 문자열을 초(second) 단위 숫자로 변환해 줍니다. (예) "0:02:30" ------> 150 (초)

      *   timeText: **String** \


          변환하려고 하는 time 형식의 문자열

      ```javascript
      $self.api.formatTime("2:30"); // 150 (second)
      $self.api.formatTime("16:40");// 1000 (second)
      $self.api.formatTime("2:46:40");// 10000 (second)
      ```
