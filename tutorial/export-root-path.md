# 콤포넌트 경로 참조 변수

Element의 이이벤트 스크립트 작성 창이나 HTML Element의 코드 편집기에서 작성한 코드에 에셋 경로가 포함되어져 있다면 이 Element를 컴포넌트 또는 템플릿으로 만들때 에셋 경로가 바뀌게 됩니다.

HTML Element에는 여러 방법으로 경로를 지정할 수 있으므로 HTML Element 요소를 가지고 예를 들어보겠습니다.

*   HTML Element Css에 경로 지정하는 경우

    ![](<../.gitbook/assets/image (3) (1).png>)
*   HTML 태그에서 이미지 경로를 지정하는 경우&#x20;

    ![](<../.gitbook/assets/image (1) (1).png>)
* API를 사용하여 이미지 소스를 바꾸는 경우

![](<../.gitbook/assets/image (9).png>)

위와 같은 경우 컴포넌트, 템플릿으로 만든 후 경로는 다음과 같이 변경되기 때문에 이미지는 나타나지 않는다.

```
// "OPS/클릭.gif" 에셋 파일을 
// 컴포넌트, 템플릿 만들때 포함시킨다면
// 파일 위치는 다음과 같이 바뀐다.
// _share/asset-(컴포넌트 또는 템플릿의 uid)/클릭.gif
```

### {exportRoot} 문자열 사용

{exportRoot} 문자열을 경로에 포함시켜주면 컴포넌트, 템플릿을 배포할때 경로를 자동으로 치환해 줍니다. {exportRoot} 문자열은 항상 배포된 폴더 경로를 가르킵니다.

*   배포된 컴포넌트, 템플릿에는 다음과 같이 경로가 자동으로 바뀝니다.

    * 배포전&#x20;

    ![](<../.gitbook/assets/image (5) (1).png>)

    * 배포후&#x20;

    <img src="../.gitbook/assets/image (2) (1).png" alt="" data-size="original">

{% hint style="info" %}
{exportRoot} 은 변수로 사용되는것이 아니라 문자열을 경로로 치환하는 것입니다.
{% endhint %}
