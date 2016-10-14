# 문제 해결 기록 및 팁 모음

### vim-airline
#### 픽셀 문제
* vim-airline 플러그인 사용시 상태표시 라인의 특수 기호들의 픽셀이 한 두 개씩 어긋나 있다.
* vim-airline은 예쁘기 때문에 쓰는 플러그인인데 픽셀이 이렇게 눈에 띄어서야 설치한 의미가 없다.

##### 해결책 1
* 다음과 같이 설정하면 뾰족한 특수문자를 사용하지 않기 때문에 눈에 띄는 문제는 해결된다.
```viml
let g:airline_left_sep = ''
let g:airline_right_sep = ''
```
* 그러나 밋밋한 VIM 화면을 보면 아쉽다.

##### 해결책 2
* 찾아보니 powerline 을 위해 개조된 폰트들이 있다.
* https://github.com/powerline/fonts
* 폰트를 다운받아 설치하고, 다음과 같이 설정한다.
```viml
let g:airline_powerline_fonts = 1
```
* iTerm2 에서 폰트를 바꿔보며 상태를 확인한다. 폰트 사이즈도 변경해 보도록 한다.

##### 참고 자료
* https://vi.stackexchange.com/questions/3359/how-to-fix-status-bar-symbols-in-airline-plugin
