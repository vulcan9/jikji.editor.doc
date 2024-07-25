---
description: >-
  youtube API를 사용하여 직지에 유튜브 영상을 삽입하는 방법을 알아봅니다. 단순히 youtube 영상을 삽입하는 것이 아니라 직지에서
  youtube API를 통해 영상을 제어 가능하도록 만드는 방법입니다.
---

# youtube API 활용하기

#### 유튜브 비디오 플레이어 삽입   방법

youtube API는 기존 DIV 태그를  IFrame으로 변환 하거나 새로 생성하여  플레이어를 구성합니다.\
그러므로 직지에서 플레이어를 구성할 공간(DIV 또는 IFrame)을  제공하고, 제어 코드를 삽입하여 youtube API를 사용할 수 있습니다.

* `이미지` 요소에 생성하는 방법
* `Web 뷰어` 요소에 생성하는 방법
* `HTML 박스` 요소에 생성하는 방법

**데모 보기** ( [https://me2.do/xHngPwMi](https://me2.do/xHngPwMi) )

{% file src="../.gitbook/assets/API 단위 테스트.zip" %}
유튜브 API 단위 테스트  문서&#x20;
{% endfile %}

{% file src="../.gitbook/assets/유튜브API 활용.jik" %}
유튜브 API 활용 예제
{% endfile %}

## `이미지` 요소에 생성하는 방법

`유튜브 API 활용.jik` 파일에 포함된 `유튜브  API.js` 파일을 임포트 합니다.

<img src="../.gitbook/assets/image (5).png" alt="" data-size="original"><img src="../.gitbook/assets/image (8).png" alt="" data-size="original">

그림 처럼 요소를 배치한 후 그룹화 합니다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

그룹을 선택한 후 `initialize` 이벤트 창에 스크립트를 작성합니다.

![](<../.gitbook/assets/image (2) (2).png>)

```
// ... 코드 주요 내용
var playerID = 'youtube_video';

//------------------
// IFrame 설정
//------------------

(function (){
    // ID 설정: ID는 속성창에 아이디 입력란에 작성해도 됨
    var $player = $self.children('element-69d1db71-5a09-486f-bb96-e01b2ce20556');
    $player.dom.id = playerID;
    // console.error('$player : ', $player);
})();

//------------------
// Player 설정
//------------------

var option = {
  videoId: 'M7lc1UVf-VE'
}

var player;
window.youtube_in_element(playerID, option, function (playerInterface){
  player = playerInterface;
});

// ...나머지 코드는 예제 참고
```

**동작 방식**

* 이미지 요소 내부 DOM이 youtubeAPI에 의해 변경됨 (IFrame으로 변경됨)
* 이미지 요소 특성은 사라짐 (이미지 요소의 API는 동작 안함)
* `videoId` 옵션으로 재생 대상을 바꿀 수 있음
* 이미지 요소 이외의 요소에도 적용 가능한 방법임 (이미지 요소가 가장 무난함)

(참조) iframe 삽입에 대한 YouTube Player API [https://developers.google.com/youtube/iframe\_api\_reference?hl=ko](https://developers.google.com/youtube/iframe\_api\_reference?hl=ko)

## `Web 뷰어` 요소에 생성하는 방법&#x20;

`유튜브 API 활용.jik` 파일에 포함된 `유튜브  API.js` 파일을 임포트 합니다.

<img src="../.gitbook/assets/image (5).png" alt="" data-size="original"><img src="../.gitbook/assets/image (8).png" alt="" data-size="original">

그림 처럼 요소를 배치한 후 그룹화 합니다.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Web 요소의 속성창에서 URL을 설정합니다.\
URL 뒤에 `enablejsapi=1` 매개변수를 전달해 주어야 JS를 통해 컨트롤 가능해 집니다.

<img src="../.gitbook/assets/image (1).png" alt="" data-size="original">

그룹을 선택한 후 `initialize` 이벤트 창에 스크립트를 작성합니다.

![](<../.gitbook/assets/image (2) (2).png>)

<pre><code><strong>// ... 코드 주요 내용
</strong><strong>var playerID = 'youtube_video';
</strong>
//------------------
// IFrame 설정
//------------------

(function (){
  // http://www.youtube.com/embed/M7lc1UVf-VE?enablejsapi=1&#x26;origin=http://localhost:5301
  var $player = $self.children('element-3b9d2eb3-7db1-451a-b6a5-a8d71593c374', true);
  var iframe = $($player.dom).find('iframe')[0];
  iframe.id = playerID;
  iframe.setAttribute('sandbox', 'allow-forms allow-scripts allow-pointer-lock allow-same-origin allow-top-navigation allow-presentation allow-popups allow-popups-to-escape-sandbox');
  iframe.setAttribute('allow', 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture');
  iframe.setAttribute('allowfullscreen', true);
  // console.error('iframe : ', iframe);
  // console.error('$player : ', $player);
})();

var player;
window.youtube_in_element(playerID, null, function (playerInterface){
  player = playerInterface;
});

// ...나머지 코드는 예제 참고
</code></pre>

**동작 방식**

* WEB 뷰어의 IFrame을 이용하는 방법임
* WEB 뷰어에 URL을 직접 설정해 주어야함
* 대신URL 변수로  player 매개변수 값을 전달할 수 있음\
  ( [https://developers.google.com/youtube/player\_parameters?hl=ko](https://developers.google.com/youtube/player\_parameters?hl=ko) )

## `HTML 박스` 요소에 생성하는 방법

~~`유튜브 API 활용.jik` 파일에 포함된 `유튜브  API.js` 파일을 임포트 합니다.~~

그림 처럼 요소를 배치한 후 HTML 편집창을 열고 코드를 입력합니다.

<img src="../.gitbook/assets/image (3) (2).png" alt="" data-size="original">

**HTML 설정**

```
<div id="youtube_video"></div>

<!-- button -->
<div id="play">재생</div>
<div id="pause">일시정지</div>

// 본 콘텐츠는 IFrame에서 동작하므로 별도로 로드해야함
<script src="./유튜브API.js"></script>
```

**JS 설정**

```
// ... 코드 주요 내용
var playerID = 'youtube_video';

//------------------
// Player 설정
//------------------

// $self 객체는 저작도구에서는 지원 안됨 (미리보기에서는 동작함)
//console.error('$self.height(): ', $self.width(), $self.height());

var option = {
  width: window.innerWidth,
  height: (window.innerHeight - 100),
  videoId: 'M7lc1UVf-VE',
}

var player;
window.youtube_in_element(playerID, option, function (playerInterface){
  player = playerInterface;
});

// ...나머지 코드는 예제 참고
```

**동작 방식**

* HTML 박스(IFrame) 안에서 독립된 context (html 페이지)에서 구성됨
* HTML 박스(IFrame) 안에 유튜브  플레이어 (IFrame)가 생성됨되는 구조임
* HTML 편집창에서는 $self, $this 변수 사용할 수는 있으나 편집창 미리보기 화면에는 적용되지 않음 (브라우저 미리보기에서는 적용됨)

