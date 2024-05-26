# loadComponent API를 이용하여 컴포넌트 작성하기 2





```javascript

    // 컴포넌트 설정
    const config = {
        // dev: true,
        // element api를 설정된 name으로 찾음
        elements: {
            loading: '로딩중',
            video: '비디오'
        },
        
        options: {
            loop: false,
            muted: false,
            src: 'https://vjs.zencdn.net/v/oceans.mp4',
        }
    };
    
    //-------------------------
    
    // 깜빡임 방지 위해 초기화 완료 이전까지 감추기
    $self.hide();
    
    // 컴포넌트 소스 파일 로드 & 초기화
    const source = {
        // css: ''
        js: [
            './_share/jikji.component/Media/Video.js',
            // 모듈 로드할때
            // { type: 'module', source: './_share/jikji.component/Media/Module.js' },
            // 코드 실행할때
            {
                type: 'module',
                code: `
                import {Module} from "./_share/jikji.component/Media/Module.js";
                `
            }
        ]
    };
    $self.loadComponent(source, () => {
    	const onInitialize = () => $self.show();
        // 컴포넌트 소스 파일에서 정의한 component 객체 참조
        const Component = window.jikjiComponent.Media.Video;
        new Component($self, config, onInitialize);
    });
```

