# 플러그인 매니저 사용하기

* [플러그인이 설치되는 경로](#플러그인이-설치되는-경로)
* [플러그인 매니저](#플러그인-매니저)
    * [플러그인 매니저 VimPlug 설치 방법](#플러그인-매니저-vimplug-설치-방법)
    * [.vimrc 설정으로 플러그인 추가](#vimrc-설정으로-플러그인-추가)
    * [VimAwesome을 이용합니다](#vimawesome을-이용합니다)
* [플러그인 설치 튜토리얼 : matchit을 설치해 봅시다](#플러그인-설치-튜토리얼--matchit을-설치해-봅시다)
* [플러그인 해제 및 삭제 방법](#플러그인-해제-및-삭제-방법)

VIM은 VIM 스크립트만 작성할 수 있다면 누구나 플러그인을 만들 수 있습니다.
그리고 만들어진지도 오래되어 플러그인도 많습니다.

> Vi는 Bill Joy가 개발하여 1976년에 릴리즈, Vim은 Bram Moolenaar가 개발하여 1991년에 릴리즈하였습니다.

[VIM 공식 홈페이지](http://www.vim.org/)에는 [5천개 이상의 플러그인](http://www.vim.org/scripts/script_search_results.php)이 등록되어 있으며,
VIM 플러그인 사이트인 [VimAwesome](http://vimawesome.com/)에서는 1만 7천개 이상의 플러그인을 소개하고 있습니다.
어지간한 기능은 찾아보면 누가 이미 만들어 놓은 플러그인이 있으므로 가져다 꽂아 쓰면 됩니다.
만약 원하는 기능을 가진 플러그인이 없다면 직접 개발하면 됩니다.

## 플러그인이 설치되는 경로

* 플러그인을 설치하는 가장 단순한 방법은 다운로드 받은 플러그인을 `.vim` 경로에 복사해 넣는 것입니다.
* 이 작업은 아래에서 소개 할 플러그인 매니저가 대행해주게 되지만, 그래도 경로 정도는 알아두는 쪽이 좋습니다.

운영체제    | 플러그인 경로
-------     | ----------------------------
Unix        | ~/.vim/plugin/
PC and OS/2 | $HOME/vimfiles/plugin or $VIM/vimfiles/plugin
Amiga       | s:vimfiles/plugin
Macintosh   | $VIM:vimfiles:plugin
Mac OS X    | ~/.vim/plugin/
RISC-OS     | Choices:vimfiles.plugin

## 플러그인 매니저

다음의 네 가지 플러그인 매니저가 주로 사용됩니다.

* [Vundle](https://github.com/VundleVim/Vundle.vim)
* [NeoBundle](https://github.com/Shougo/neobundle.vim)
* [VimPlug](https://github.com/junegunn/vim-plug)
* [Pathogen](https://github.com/tpope/vim-pathogen)

이 글에서는 VimPlug 위주로 설명합니다.

> 저는 Vundle과 VimPlug를 사용해 보았고, 현재 VimPlug를 사용하고 있습니다.
다운로드 후에 쉘 스크립트 등을 실행시켜야 설치가 완료되는 플러그인들이 있습니다(youcompleteme, fzf 등).
VimPlug는 쉘 스크립트 실행 작업도 미리 설정할 수 있어 편리합니다.

### 플러그인 매니저 VimPlug 설치 방법

[설치 방법](https://github.com/junegunn/vim-plug#installation)을 참고하여 플러그인 매니저를 설치합니다.
설명이 영어로 되어 있긴 하지만 어렵지는 않습니다.

설치 방법을 Unix, Neovim, Windows 세 가지로 제공하고 있으므로
맥이나 리눅스 유저라면 Unix 설치 명령어를 복사해 터미널에서 실행하면 되고,
윈도우즈 유저라면 Windows(PowerShell) 설치 명령어를 복사해서 파워쉘에서 실행하면 됩니다. 또한 WSL을 설치하여 사용하는 것도 좋은 방법입니다.

### .vimrc 설정으로 플러그인 추가

VimPlug 를 설치했다면, .vimrc 최상단에 다음과 같이 작성하는 것으로 플러그인을 추가할 수 있습니다.

```viml
" plug#begin 과 plug#end 사이에 사용하고 싶은 플러그인들을 선언해 줍니다.
call plug#begin('~/.vim/plugged')
    "Plug 'GitHub계정명/저장소명'   " 추가하고 싶은 플러그인의 GitHub 저장소 주소를 Plug 뒤에 적어줍니다.
    Plug 'othree/eregex.vim'        " https://github.com/othree/eregex.vim 플러그인을 설치하는 경우
    Plug 'ctrlpvim/ctrlp.vim'       " https://github.com/ctrlpvim/ctrlp.vim 플러그인을 설치하는 경우
    Plug 'matchit.zip'              " vim.org에 등록된 플러그인의 경우
    Plug 'valloric/youcompleteme', { 'do': './install.py --all'}    " 설치 후 실행해야 하는 터미널 명령어가 있을 경우 'do' 옵션으로 지정해 줍니다.
call plug#end()

syntax on
filetype plugin indent on

" 이 아래쪽부터 자신의 .vimrc 설정을 작성하면 됩니다.

set number
set hlsearch
...
```

추가한 다음엔 다음 두 방법 중 하나를 골라 실행하면 각 플러그인이 설치됩니다.
* 방법 1 : `.vimrc`파일을 다시 읽어들이기 위해 VIM을 재실행한 다음에 `:PlugInstall`하면 됩니다.
* 방법 2 : `:source ~/.vimrc`로 `.vimrc`를 다시 읽어들인 다음 `:PlugInstall`하면 됩니다.

### VimAwesome을 이용합니다

* 위의 예제를 보면, 어떤 플러그인은 GitHub 주소를 사용하고, 어떤 플러그인은 `.zip`형식을 명시하는 방식으로 설치합니다.
* 다음과 같이 생각하는 분들이 분명히 있을 것입니다.
    * '내가 원하는 플러그인이 GitHub에 있는지 vim.org에 있는지 어떻게 알 수 있지?' 
    * '어디에 있는지 모르면 설치를 할 수가 없잖아?'

VIM 플러그인 검색 서비스인 [VimAwesome](http://vimawesome.com/)는
플러그인마다 각 플러그인 매니저별 설치 코드를 제공하고 있기 때문에 사용하면 이런 고민을 하지 않아도 됩니다.
가령 VimAwesome의 [surround.vim 플러그인 페이지](http://vimawesome.com/plugin/surround-vim)를 보면
`INSTALL FROM`항목 아래로 Vundle, NewBundle, VimPlug, Pathogen 의 설치 코드를 보여줍니다.

설치 코드를 복사해서 위의 예제와 같이 추가해주면 됩니다.

> VimAwesome 웹페이지는 VIM유저를 위한 사이트답게 `j`, `k`, `/` 등의 명령어 키를 지원합니다.

## 플러그인 설치 튜토리얼 : matchit을 설치해 봅시다

* matchit은 괄호 짝으로 점프하는 `%`를 html tag 에서도 사용할 수 있도록 확장해주는 플러그인입니다.

> matchit 설치후에는 html 파일을 편집할 때 `<div>`에 커서를 놓고 `%`를 입력하면 `</div>`로 점프하게 됩니다. 반대로도 가능합니다.

* 다음과 같은 .vimrc 가 있다고 할 때 matchit 플러그인을 설치해 봅시다.

```viml
set nu
set ruler
set background=dark
```

* 일단 터미널을 열고 다음의 명령어를 입력하여 VimPlug를 설치합니다.

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

* 그리고 .vimrc를 다음과 같이 수정합니다.

```viml
call plug#begin('~/.vim/plugged')
    " 사용하고 싶은 플러그인을 선언할 곳
call plug#end()
syntax on
filetype plugin indent on
set nu
set ruler
set background=dark
```

* [VimAwesome](http://vimawesome.com/)에서 `matchit`을 검색합니다.

* 검색 결과 첫 번째로 나온 결과를 살펴보면 `extended % matching for HTML, LaTeX, and many other languages` 라고 되어 있습니다. 클릭합니다.

* 왼쪽의 `INSTALL FROM`에서 `VimPlug`를 선택하면, 오른쪽에 다음과 같은 설치 코드가 나타납니다.

```
Place this in your .vimrc:
Plug 'matchit.zip'
… then run the following in Vim:
:source %
:PlugInstall
```

.vimrc 에 `Plug matchit.zip` 이라 추가하고, Vim에서 `:source %`, `:PlugInstall`을 차례대로 실행하면 된다는 내용입니다.

* `.vimrc`에 다음과 같이 matchit 설치 코드를 추가하고 저장해줍니다.

```viml
call plug#begin('~/.vim/plugged')
    Plug matchit.zip    " 새로 추가된 라인
call plug#end()
syntax on
filetype plugin indent on
set nu
set ruler
set background=dark
```

* 그 다음은 `:source %`를 입력하거나, 잘 모르겠으면 VIM을 종료하고 다시 실행하면 됩니다.

> `:source %`는 `%`를 VIM스크립트로 읽어들이라는 의미입니다. `%`레지스터는 현재 파일명을 담고 있으므로 결국 현재 편집중인 `.vimrc`를 다시 읽어들이라는 뜻입니다.
> VIM을 종료한 후에 다시 실행하면 어차피 방금 저장한 `.vimrc`를 읽게 되므로 재실행해도 똑같습니다.

* 이제 `:PlugInstall`을 입력하면 설치가 시작됩니다.

* 테스트 삼아 html 파일 하나를 열어서, `%`로 태그 점프가 되는지 확인하면 됩니다.

* 도움말은 `:help matchit`으로 볼 수 있습니다.

> 또는 `~/.vim/plugged/doc`에서도 볼 수 있습니다.

> `~/.vim/plugged/matchit.zip/plugin`로 가 보면 matchit의 소스코드를 볼 수 있습니다. 작동원리를 파악해두거나, 마음에 안 드는 부분을 고쳐서 사용하는 것도 가능합니다.

## 플러그인 해제 및 삭제 방법

* .vimrc의 Plug 구문을 삭제하거나 주석처리하면 해당 플러그인이 해제됩니다.
* 삭제하고 싶다면 .vimrc를 다시 읽은다음, `:PlugClean`하면 해제된 플러그인들이 삭제됩니다. 삭제하기 전에 `(y/n)`을 물어보는데 `y`를 누르면 됩니다.
