# Animation 객체

저작툴에서 제작된 객체의 속성이 변하면 자동으로 transition 애니메이션이 동작합니다. 각각에 변경된 속성들은 동시에 애니메이션이 동작하며 `enable()` 메서드와 `config()` 메서드를 통해서 애니메이션 동작을 설정할 수 있습니다.

애니메이션을 순차적으로 적용하고 싶은 경우에는 `sequence()` 메서드를 사용합니다. 이 메서드는 순차적인 애니메이션 실행을 설정할 수있는 객체를 반환합니다.

`sequence()` 메서드에 의해 애니메이션이 진행되는 동안에는 `enable()`, `config()` 메서드를 사용할 수 없습니다. 또한 `setDrag()` 메서드를 통해 설정된 드래그 기능도 애니메이션이 완료될때까지 동작하지 않습니다.

### _**메서드**_

*   _**enable (value: Boolean): void**_

    group 또는 element가 transition을 사용할지 여부를 결정합니다. `false` 값인 경우 애니메이션 없이 속성 값이 바로 적용되어 표시됩니다.

    *   value: **Boolean** 설정(true), 해지(false)

        ```javascript
        // group객체의 transition을 사용하지 않음
        group.animation.enable(false);

        // Getter
        var enable = group.animation.enable();
        // group에 속한 element들중 하나라도 enable 값이 false이면 false 값을 반환합니다.
        ```
*   _**config (transition: Object): void**_

    transition 속성값을 설정합니다.

    *   transition : **Object**

        * duration: **Number** transition이 진행 완료되는 시간(second 단위)
        * timeFunction: **String** transition 효과를 나타내는 [speed 곡선 함수](https://www.w3schools.com/cssref/css3\_pr\_transition-timing-function.asp) 이름
        * delay: **Number** transition 효과 시작전 시간 지연 설정값(second 단위)

        ```javascript
        var transition = {
          duration: 1,
          timeFunction: 'ease',
          delay: 0
        }
        group.animation.config(transition);
        ```
*   _**sequence (name: String): Object**_

    순차적인 애니메이션을 정의할 수 있는 객체를 반환합니다.

    * name: **String** 정의될 애니메이션의 이름을 지정합니다. (생략 가능)
    *   반환되는 객체에 대해서는 아래 sequence 객체 내용 참고

        ```javascript
        group.animation.sequence()
          .next({x: 30})
          .play(function(){
            // transition 완료
          })
        ```

    **sequence 메서드 반환객체**

    *   _**next (style: Object, transition: Object): sequence Object**_

        애니메이션 설정을 추가합니다.

        * style : **Object** element의 스타일 속성을 객체 형식으로 기술합니다.
        *   [transition : **Object**](animationapi.md#animation-config) `config()` 메서드의 transition 파라메터를 참고하세요

            * duration: **Number**
            * timeFunction: **String**
            * delay: **Number**
            * enable: **Boolean**

            transition 옵션은 해당 구간에서만 적용됩니다. 이 값을 생략하면 `config()`에서 설정했던 값 또는 기본값이 다시 적용됩니다.

        ```javascript
        // transition 설정
        group.animation.config({
            duration: 1,
            timeFunction: 'ease',
            delay: 0
        });
        group.animation.sequence()
          .next({x: 300, y: 300})
          .next({x: 600, y: 300})
          .next({x: 600, y: 600})

          // 값 변동 없으므로 아래 두 next 메서드는 무시됨
          .next({x: 600, y: 600})
          .next({x: 600, y: 600})

          .next({x: 300, y: 600})
          .next({x: 300, y: 300});
          .play();
        ```

        ```javascript
        // `transition`을 개별적으로 지정하고자 할때
        group.animation.sequence()
          .next({x: 300, y: 300}, { duration: 0.3, timeFunction: 'linear', delay: delay})
          .next(x: 600, y: 300})
          .next({x: 600, y: 600})
          .next({x: 300, y: 600}, { duration: 2, timeFunction: 'ease', delay: delay })
          .next({x: 300, y: 300}, { duration: 1, timeFunction: 'linear', delay: delay});
          .play()
        ```
    *   _**delay (second: Number): sequence Object**_

        다음 애니메이션 시작하기 전에 시간을 지연시킵니다.

        *   second : **Number**\


            지연 시간 (단위: 초)

        ```javascript
        // `transition`을 개별적으로 지정하고자 할때
        group.animation.sequence()
          .next({x: 300, y: 300})

          // 1 초 후 (600,300) 위치로 transition 됨
          .delay(1)

          .next({x: 600, y: 300})
          .play();
        ```
    *   _**play (callback: Function): void**_

        `sequence` 객체에 정의된 애니메이션을 시작합니다.

        *   callback : **Function**\


            transition이 모두 완료되어 멈출때 호출됨

        ```javascript
        // `transition`을 개별적으로 지정하고자 할때
        group.animation.sequence()
          .next({x: 300, y: 300})
          .play(function(loop_counter){
              // loop_counter :  현재 몇번 반복 실행되고 있는지 횟수
          });
        ```
    *   _**stop (): sequence Object**_

        실행중인 애니메이션을 중지합니다. 다시 `play()` 시키면 처음부터 다시 시작합니다.

        ```javascript
        var seq = group.animation.sequence()
          .next({x: 100})
          .next({x: 200})
          .next({x: 300});

        // 실행
        seq.play();
        ...
        // (200으로 이동 후) 멈춤
        seq.stop();
        ...
        // 다시 실행 : (100) 위치로 다시 이동하여 실행됨
        seq.play();

        // stop의 경우 리턴 값에 특별히 pipe 메서드가 제공되어
        // 다른 animation으로 전환할 수 있습니다.
        seq.stop()
          .pipe(function(){
            // 계속해서 다른 seq2 실행
            seq2.play();
          });
        ```
    *   _**pause (): sequence Object**_

        실행중인 애니메이션을 일시 정지합니다. 다시 `play()` 시키면 멈춘 위치부터 시작합니다.

        ```javascript
        var seq = group.animation.sequence()
          .next({x: 100})
          .next({x: 200})
          .next({x: 300});

          // 실행
          seq.play();
          ...
          // (200으로 이동 후) 일시 정지
          seq.pause();
          ...
          // 다시 실행 : (300) 위치로 이동됨
          seq.play();
        ```
    *   _**loop (repeat): sequence Object**_

        애니메이션 반복 실행 횟수를 지정합니다.

        ```javascript
        var seq = group.animation.sequence()
          .next({x: 100})
          .next({x: 200})
          .next({x: 300})

          // 무한반복
          .loop();
          .play();

          ...
        seq.stop()
          // 5회만 반복
          .loop(5)
          .play();
        ```

        ```javascript
        // callback 함수로 반복 실행 만들기
        var seq = group.animation.sequence()
          .next({x: 100})
          .next({x: 200})
          .next({x: 300})
          //.loop();
          .play(onComplete);

        function onComplete(repeat){
          // 무한반복
          seq.play(onComplete);
        }
        ```
    *   _**reverse (): sequence Object**_

        애니메이션을 역순으로 실행합니다.

        ```javascript
        var seq = group.animation.sequence()
          .next({x: 100})
          .next({x: 200})
          .next({x: 300})
          .loop();
          .play(onComplete);

        function onComplete(repeat){
          if(repeat%2 === 0){
            // 역방향 진행
            seq.reverse();
          }
        }
        ```
    *   _**clear (): void**_

        정의된 애니메이션을 메모리에서 모두 제거합니다. 더이상 사용되지 않는 애니메이션은 반드시 `clear()` 시켜줍니다.

        ```javascript
        var seq = group.animation.sequence()
          ...
          .loop()
          .play();

        // 애니메이션 실행됨
        seq.stop().play();

        // 실행 객체를 찾지 못해 실행할 수 없음
        seq.clear()
        seq.play();
        ```
