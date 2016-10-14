# [Eclim](http://eclim.org/)

## Eclim 이란?
* headless eclipse. eclipse 를 로컬 서버로 띄워,  gui 는 사용하지 않고 타 에디터의 플러그인처럼 사용할 수 있는 도구.
* 즉, Eclipse 를 VIM 플러그인으로 사용할 수 있다.
* Java code autocomplete 등의 용도로 사용하면 편리하다.

## 설치

### 설치 준비

* JDK(1.7 이상)를 설치한다.
* VIM(7.1 이상)을 설치한다.
* .vimrc 에 `set nocp` 를 설정해 둔다.
* .vimrc 에 `filetype plugin indent on` 을 설정해 둔다.
* .vimrc 에 `let g:EclimCompletionMethod = 'omnifunc'` 을 추가해 둔다.

### OSX

1. eclim 을 [다운로드](http://eclim.org/install.html)받는다.
1. Eclipse 를 [다운로드](https://www.eclipse.org/downloads/) 받는다. 단, Installer가 아니라, tar.gz 로 압축된 Eclipse 를 다운받도록 한다.
> OSX 에서 Installer 를 사용해 Eclipse 를 설치하면 하위 디렉토리 구성이 Eclim 과 맞지 않아 설치에 실패한다.
1. 적당한 위치에 Eclipse 압축을 푼다.
1. `$ java -jar eclim_x.x.x.jar` 로 Eclim Installer 를 실행한다. Eclim Installer 를 사용하지 않고 수동으로 설치하거나 빌드하거나 하면 에러가 발생하며 설치가 되지 않을 확률이 매우 높다.
1. Eclipse 위치로는 `설치한경로/Eclipse_neon.app/Contents/Eclipse` 를 지정해 주도록 한다.
> 하위 경로에 features 라는 디렉토리가 있어야 한다. Eclim 은 Eclipse 에 plugin 형식으로 추가되기 때문에 경로가 맞지 않으면 설치에 실패한다.
1. vim 경로로는 `~/.vim` 을 지정해 주도록 한다.
1. 이후로는 설치가 완료될 때까지 next 버튼을 눌러주면 된다.
1. 설치가 완료되면 eclimd 가 자동으로 실행된다. 이제 vim 으로 java 파일을 열고 `<C-x><C-o>` 하면 java 자동완성 기능을 사용할 수 있다.
1. 만약 eclimd 가 실행되지 않았다면 다음과 같이 실행하면 된다.
    * `설치한경로/Eclipse_neon.app/Contents/Eclipse/eclimd` 를 실행하면 eclimd 서버가 시작된다.
    * osx 의 gui 환경에서 설치한 경로의 이클립스 아이콘을 더블클릭하여 실행하고, `상단메뉴 > Window > Show View > Other > Eclimd` 를 선택하면 eclimd 서버가 시작된다.

## 참고 자료
* http://eclim.org/install.html
* https://github.com/ervandew/eclim/issues/479

