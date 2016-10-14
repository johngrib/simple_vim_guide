# .vimrc 설정 방법

* `.vimrc`는 VIM의 설정 파일입니다.
* `.vimrc`의 위치는 다음과 같습니다. 파일이 존재하지 않는다면 새로 생성하면 됩니다.

OS         | VIM    | 위치
------     | ------ | :----------
Linux, mac | VIM    | `~/.vimrc`
Windows    | GVIM   | `C:\Users\사용자이름\_vimrc`
Linux, mac | NeoVIM | `~/.config/nvim/init.vim`

* VIM을 에뮬레이트하는 유명한 IDE 플러그인들도 비슷한 설정 파일을 갖고 있습니다.

OS         | IDE           | PlugIn  | 위치
------     | ------        | ------  | :----------
Linux, mac | Eclipse       | vrapper | `~/.vrapperrc`
Windows    | Eclipse       | vrapper | `C:\Users\사용자이름\_vrapperrc`
Linux, mac | IntelliJ IDEA | IdeaVim | `~/.ideavimrc`
...        | ...           | ...     | ...

## 설정 예제

* 다음과 같이 `.vimrc`파일 내용을 구성하면 됩니다.

```viml
"앞에 쌍따옴표를 쓰면 주석이 됩니다.
source functions.vim    "source 로 다른 설정 파일을 include 할 수 있습니다.

"set을 사용해 VIM의 기본 설정을 지정할 수 있습니다.
set number      "라인 넘버가 보이도록 합니다. (라인 넘버가 보이도록 설정하는 쪽이 좋습니다.)
set ignorecase  "검색시 검색어의 대소문자를 무시한다.

"map을 사용해 자신만의 단축키를 설정할 수 있습니다.
nnoremap <F2> :w    "<F2>키를 누르면 저장합니다.

"자신만의 function을 선언하여 VIM에서 사용하는 것도 가능합니다.
function! ToggleNumber()
    if(&relativenumber == 1)
        set norelativenumber
        set number
    else
        set relativenumber
    endif
endfunc

"자신만의 command를 설정하는 것도 가능합니다.
command! ToHtml :so $VIMRUNTIME/syntax/2html.vim
command! Ncd :cd %:p:h
```

## 옵션의 종류

* 옵션은 설정하는 방법에 따라 크게 네 가지로 나뉩니다.
    * boolean : `on`값과 `off`값이 있는 옵션.
    * number : 숫자로 값을 지정해 주는 옵션.
    * string : 문자열로 값을 지정해 주는 옵션.
    * list : 콤마로 구분된 문자열 값의 목록을 지정해 주는 옵션.

> boolean 옵션은 옵션 이름 앞에 no 를 붙이면 off 로 설정하게 됩니다.

* 예제
```viml
set number                     " boolean 옵션 number 를 on 으로 설정한다.
set nonumber                   " boolean 옵션 number 를 off 로 설정한다.
set history=2000               " number 옵션 history 를 1000 으로 설정한다.
set background=dark            " string 옵션 background 를 dark 로 설정한다.
set backspace=indent,eol,start " list 옵션 backspace 를 indent,eol,start 로 설정한다.
```

## 주요 옵션 소개

VIM에는 아랍어 키보드 설정은 물론이고 백업 파일이나 특수 키보드를 위한 설정까지 굉장히 다채로운 옵션들이 있습니다.
심지어는 정규식 엔진을 교체(`regexpengine`)하거나 MS Windows 에서 VIM 에디터 화면을 DirectX로 그려낼 때 텍스트 렌더러를 지정하는 옵션(`renderoptions`)까지 있을 정도입니다.
자신에게 필요한 옵션들을 선정하여 `.vimrc`에 정의하고, Github repository 등으로 관리하면 무척 편리합니다.
언제나 어디서나 인터넷이 되는 환경이라면 자신에게 친숙한 VIM 설정을 그대로 사용할 수 있습니다.

VIM을 처음 배울 때에는 이것저것 설정하고 싶은 욕심이 있어도,
옵션이 너무 많아 어떤 것을 설정해야 하는지 잘 모를 수 있습니다.
따라서 전부 소개하기는 어렵고 주관적으로 선정한 주요 옵션들만 소개하도록 합니다.

* 옵션에 대한 전체 도움말은 `:help option-summary`로 찾아보면 됩니다.
* 개별 옵션에 대한 도움말은 `:help '옵션명'`으로 찾아보면 됩니다.
> 옵션명은 도움말 내에 따옴표와 함께 나와있기 때문에 따옴표를 넣어주면 정확하게 검색됩니다.

* 아래 옵션 목록은 옵션명과 축약형 옵션명을 함께 소개합니다.

#### `autochdir`, `acd`
* boolean 옵션. 기본값은 `off`. 도움말은 `:help acd`.
* 파일을 열거나, 버퍼를 이동할 때 작업 디렉토리를 자동으로 변경해줍니다.
* 이 옵션이 사용 가능한지 확인하려면 `:echo exists("+autuchdir")`을 실행해봅니다. 출력값이 1 이면 사용 가능합니다.
* 특별한 상황이 아니라면 `off`를 추천합니다. 프로젝트 단위의 작업을 할 때 번거로워집니다.

```viml
set autochdir   " on 으로 설정
set noautochdir " off 로 설정
set acd         " on 으로 설정(축약형)
set noacd       " off 로 설정(축약형)
```

#### `autoindent`, `ai`

* boolean 옵션. 기본값은 `off`. 추천값은 `on`. 도움말은 `:help ai`.
* INSERT 모드에서 엔터를 입력하여 다음 줄로 내려가면, 자동으로 들여쓰기를 해 줍니다.

#### `autoread`, `ar`

* boolean 옵션. 기본값은 `off`. 도움말은 `:help autoread`.
* VIM 외부에서 파일 내용이 변경되면 자동으로 다시 읽어들입니다.

#### `autowrite`, `aw`

* boolean 옵션. 기본값은 `off`. 도움말은 `:help autowrite`.
* 변경 사항이 있을 때마다 자동으로 파일을 저장합니다.
* 사용할 생각이 있다면, 비슷하게 작동하지만 조건이 다른 `autowriteall`과도 비교해 볼 필요가 있습니다.

#### `background`, `bg`
* string 옵션. `dark`, `light` 둘 중 하나의 값만 설정 가능. 도움말은 `:help 'bg'`
* 배경색을 `dark`로 하느냐, `light`로 하느냐에 따라 폰트 색깔에 영향을 줍니다.
* 특히 syntax color 를 위해 color scheme 을 지정한 경우 효과를 볼 수 있습니다.

```viml
set background=dark
```

#### `backspace`, `bs`

* list 옵션. `indent`,`eol`,`start` 를 나열하는 방식으로 설정할 수 있습니다. 도움말은 `:help bs`.
* 이 옵션은 `<BS>`키의 삭제 기능을 설정해 줍니다.
* 일반적인 gui 문서 편집 프로그램의 백스페이스 키와 똑같이 작동하게 하고 싶으면 `set bs=indent,eol,start`로 설정해 주면 됩니다.

> [Bill Joy](https://en.wikipedia.org/wiki/Bill_Joy)가 VI를 개발했을 때 사용하던 장비는
[ADM-3A 터미널](https://en.wikipedia.org/wiki/ADM-3A)이었는데 이 키보드에는 `<BS>`키가 없었습니다.
즉, 옛날 옛적 VI가 개발되었을 무렵의 키보드에는 `<BS>`키가 없었기 때문에 VIM 에서 새롭게 생긴 옵션이라 할 수 있습니다.
ADM-3A 터미널의 키 레이아웃을 잘 살펴보면
[VIM에서 `HJKL`이 왜 화살표 역할을 맡게 되었는지](http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys/)도 알 수 있습니다.

#### `backup`, `bk`

* boolean 옵션. 기본값은 `off`. 도움말은 `:help bk`.
* 파일을 덮어씌워 저장하기 전에 백업을 생성합니다.

#### `backupdir`, `bdir`
* list 옵션. 백업을 저장할 디렉토리 경로를 콤마로 구분하여 설정하면 됩니다. 도움말은 `:help bdir`.

#### `backupskip`, `bsk`
* list 옵션. 백업하지 않을 파일명, 경로 패턴을 콤마로 구분하여 설정하면 됩니다. 도움말은 `:help bsk`.

#### `cedit`
* string 옵션. Command-line 에서 히스토리 윈도우를 열어주는 단축키를 지정합니다. 도움말은 `:help cedit`.
* Command-line 윈도우는 Command-line 의 히스토리를 조회/검색할 수 있으며, `:`명령어 입력을 NORMAL 모드와 같이 편집할 수 있습니다.
* 기본값은 `<C-f>`이며, 다른 키 조합 설정 예제는 다음과 같습니다.

```viml
set cedit=<C-y>     " <C-y>로 설정
set cedit=<Esc>     " <Esc>로 설정
```

#### `cindent`, `cin`
* 편집시에 자동으로 C 언어 스타일의 인덴트를 적용해 줍니다. 도움말은 `:help cin`.

#### `clipboard`, `cb`
* list 옵션. 클립보드와 연결할 레지스터를 설정하는 옵션. 도움말은 `:help 'clipboard'`. (이 항목은 따옴표를 넣어야 정확히 검색됩니다.)
* 설정을 위해 알아야 하는 내용이 좀 있는 편입니다. 도움말을 꼼꼼히 읽어보는 것을 권장합니다.
* 모든 복사/삭제 작업이 입력되는 `unnamed`레지스터를 클립보드와 연결한다던가 `+`레지스터와 연결하는 등의 설정을 할 수 있습니다.
* gui 버전 VIM 또는 `+xterm_clipboard`기능이 포함된 채 컴파일된 VIM에서만 사용할 수 있습니다.

> 확인 방법은 `$ vim --version | grep +xterm_clipboard`

#### `compatible`, `cp`
* boolean 옵션. VI와의 호환 여부를 설정합니다. 기본값은 `on`.
* 다른 많은 옵션들의 기본값에 영향을 줍니다. 추천값은 `off`. (예제 참고)

```viml
set nocp
```

#### `complete`, `cpt`
* string 옵션. `<C-p>`, `<C-n>` 자동완성의 작동방식을 설정합니다.

#### `confirm`, `cf`
* boolean 옵션. `:q`, `:bd`등의 명령어를 사용할 때 사용자의 확인을 받습니다.

> 편집중에 다른 파일을 열거나 하면 `No write since last change` 에러가 발생하며 명령이 취소됩니다.
작업한 내용의 안전을 위한 것이긴 한데 짜증날 때가 있습니다. 이 옵션을 설정해주면 명령이 취소되지 않고 Yes, No, Cancel 을 물어봅니다.

#### `cursorcolumn`, `cuc`
* boolean 옵션. 커서가 있는 컬럼을 하이라이트처리해준다. 기본값은 `off`.
* 재미있는 설정을 좋아하는 사람에게 `on`추천.

> 커서가 있는 라인을 하이라이트해주는 기능은 편집기의 상식이죠.
이 옵션을 설정해주면 이미지 편집기처럼 커서 위치에서 교차하는 거대한 하이라이트 십자가를 볼 수 있게 됩니다.
즉, 커서의 x 좌표상의 위치를 한 눈에 볼 수 있게 됩니다.

#### `cursorline`, `cul`
* boolean 옵션. 커서가 있는 라인을 하이라이트처리해줍니다. 기본값은 `off`.
* 커서 위치를 쉽게 파악하게 해 주는 중요한 기능. 가급적이면 `on`으로 설정해줍시다.

> 설정하는 것만으로도 이 값이 `on`이 되는 color scheme 도 존재합니다.
> 한편, 마음에 드는 color scheme 을 발견했는데 커서 라인이 보이지 않아 실망했다면, 이 옵션을 `on`으로 설정해주면 됩니다.

#### `dictionary`, `dict`
* list 옵션. INSERT 모드에서 `<C-x><C-k>`로 자동완성할 사전 파일의 목록을 지정해줍니다.

#### `expandtab`, `et`
* boolean 옵션. 탭키를 누르면 탭이 아니라 설정한 수의 스페이스가 입력된다. 기본값은 `off`.
* 스페이스의 수는 `tabstop` 옵션으로 설정해주면 됩니다.

```viml
set expandtab
set tabstop=4
```

#### `gdefault`, `gd`
* boolean 옵션. `:substitute`명령, 즉 `:s`를 사용할 때 `g`플래그를 기본값으로 설정합니다. 기본값은 `off`.
* 이 옵션이 `on`상태일 때 `:s`에 `g`옵션을 주면, 반대의 의미로 작동합니다.

#### `guifont`, `gfn`
* string 옵션. gui 버전의 VIM에서 사용할 폰트를 지정해 줍니다.

```viml
set guifont=Meslo\ LG\ M\ DZ:h11    " gui font 로 Meslo LG M DZ 를, 폰트 크기를 h11로 설정하였다.
```

#### `hlsearch`, `hls`
* boolean 옵션. 검색 결과, 검색어와 매치된 문자열에 강조 표시를 합니다. 기본값 `off`.
* 추천값은 `on`.

> 검색 결과를 확인한 다음 강조 표시를 끄고 싶다면 `:noh`를 입력하면 됩니다. 물론 다음 검색 때에는 다시 강조 표시가 됩니다.

#### `history`, `hi`
* number 옵션. `:` 명령어의 히스토리를 지정한 숫자만큼 기억합니다. 기본값은 50.
* 설정 max 값은 10000 입니다.

> 히스토리는 `~/.viminfo`파일에 저장됩니다.

```viml
set history=300
```

#### `ignorecase`, `ic`
* boolean 옵션. 이 옵션을 설정하면 검색시 대소문자를 무시합니다. 기본값은 `off`.
* 다음 예제와 같이 `smartcase`와 함께 설정하는 쪽을 추천합니다.

```viml
set ignorecase   " 검색시 대소문자 무시 (소문자로도 대문자 검색 가능)
set smartcase    " 검색어에 대문자가 포함되어 있다면 대소문자를 무시하지 않는다.
```

#### `incsearch`, `is`
* boolean 옵션. `/`검색시 한 글자씩 입력할 때마다 검색을 수행합니다. 기본값은 `off`.
* 추천값은 `on` 이며, `hlsearch`와 함께 설정하면 더 좋습니다.

```viml
set hlsearch
set incsearch
```

#### `langmap`, `lmap`
* list 옵션. 비 영어권 키보드를 위한 옵션으로, 특정 문자를 영문으로 매핑할 수 있습니다.
* 한/영 전환을 하지 않아도 명령어를 입력할 수 있다는 장점이 있습니다. 이에 대해서는 [한국어 키보드로 VIM 사용하기](with_korean.md) 참고.
* Command-line 은 이 옵션에 영향을 받지 않습니다.
* 한국어라면 다음과 같이 설정할 수 있습니다.

```viml
" 설정방법 1
set langmap=ㅁa,ㅠb,ㅊc,ㅇd,ㄷe,ㄹf,ㅎg,ㅗh,ㅑi,ㅓj,ㅏk,ㅣl,ㅡm,ㅜn,ㅐo,ㅔp,ㅂq,ㄱr,ㄴs,ㅅt,ㅕu,ㅍv,ㅈw,ㅌx,ㅛy,ㅋz

" 설정방법 2
set langmap=ㅁㅠㅊㅇㄷㄹㅎㅗㅑㅓㅏㅣㅡㅜㅐㅔㅂㄱㄴㅅㅕㅍㅈㅌㅛㅋ;abcdefghijklmnopqrstuvwxyz
```

#### `langremap`, `lrm`
* boolean 옵션. `off`로 설정하면 `langmap`이 디폴트 상태가 됩니다.

#### `laststatus`, `ls`
* number 옵션. 마지막 윈도우에 status line을 표시할지의 여부를 설정할 수 있습니다. 기본값은 `1`.
    * `0`: 표시하지 않습니다.
    * `1`: 윈도우가 하나일 때에는 표시하지 않습니다.
    * `2`: 항상 표시합니다.
* 추천값은 `2`.

#### `lazyredraw`, `lz`
* boolean 옵션. (매크로 등의) 작업을 진행중일 때에는 화면을 갱신하지 않습니다. 기본값은 `off`.
* 매크로를 자주 사용한다면 이 옵션을 `on` 해두길 추천합니다. 매크로가 끝난 다음에 화면을 갱신하기 때문에 굉장히 빨라진 것처럼 느껴집니다.

> IntelliJ IDEA의 VIM플러그인인 IdeaVim 의 경우 이 옵션이 없어서 매크롤 쓸 때마다 지루한 중간 과정을 전부 지켜보고 있어야 합니다.

#### `linebreak`, `lbr`
* boolean 옵션. 한 줄이 너무 길어서 화면을 넘어가면, 한 줄을 여러 줄로 표현하게 되는데 이 옵션을 설정해두면 단어 단위로 라인이 잘립니다. 기본값은 `off`.
* 글자 단위로 라인이 잘리는 것을 싫어한다면 `on`을 추천합니다.

#### `linespace`, `lsp`
* number 옵션. 행간 거리를 설정할 수 있습니다. 기본값은 `0`.
* 테스트 삼아 `:set lsp=100`으로 해보면 모니터 전체에 몇 개 라인 밖에 안 나오게 됩니다.
* 행간이 좁아 답답하다면 적당히 테스트해보며 마음에 드는 값을 찾아 설정하면 됩니다.
* 단, MacVIM 같은 gui VIM 에서만 됩니다.

#### `list`
* boolean 옵션. `listchars`에서 설정한 문자들로 공백 문자들을 보여줍니다. 기본값은 `off`.
* 이 옵션을 설정해두면 `<Space>`와 `<Tab>`, 그리고 짜증나는 trailing blanks 를 더 쉽게 파악할 수 있습니다.
* 추천값은 `on`. 그리고 `listchar`를 함께 설정하면 좋습니다.

#### `listchars`, `lcs`
* list 옵션. `list` 옵션이 `on` 상태일 때 공백 문자 등을 보여주는 방식을 설정합니다.
* 설정 가능한 항목은 `eol`, `tab`, `space`, `trail`, `extends`, `precedes`, `conceal`, `nbsp` 8가지입니다.

```viml
" 탭을 » 와 공백들로 표현하고, trailing blanks 를 · 로 표현합니다.
set list listchars=tab:»\ ,trail:·
```

#### `loadplugins`, `lpl`
* boolean 옵션. 이 옵션을 `off`하면 플러그인을 로드하지 않습니다. 기본값은 `on`.
* 매우 드물게 발생하는 일이지만, 플러그인에 문제가 생겼을 때 사용할 만합니다.

#### `macthinstrokes`
* boolean 옵션. 글자를 좀 더 가늘게 표현해줍니다. 기본값은 `off`.
* 꽤 예쁩니다. 다만 gui VIM 에서만 됩니다.

#### `macmeta`
* boolean 옵션. 맥의 옵션 키, 즉 `⌥`키를 `meta`키로 사용하게 해줍니다. 기본값은 `off`.
* 비슷한 느낌이 있긴 하지만 맥의 `option`키는 `alt`키가 아닙니다.
맥 터미널에서 `option`키와 알파벳을 조합하면 특수문자들(그리스 문자 등등)이 입력됩니다.
`<M-a>`같은 조합이 입력되지 않는 것입니다. (리눅스나 윈도우는 잘 됩니다.)
이 때문에 맥 터미널을 사용하면 `map`을 설정할 때 고민스러운 상황에 봉착하게 됩니다.
* 다행히 이 옵션을 사용하면 MacVIM 에서는 `meta`키 조합을 사용할 수 있게 해 줍니다.
* 주의: gui VIM 에서만 됩니다.

```viml
if has('mac')
    nnoremap ˚ ddkP
    nnoremap ∆ ddp
endif
nnoremap <M-k> ddkP
nnoremap <M-j> ddp
```

#### `matchpairs`, `mps`
* list 옵션. `%`로 이동할 괄호의 짝을 지정해 줍니다. 기본값은 `(:),{:},[:]`.
* VIM의 기본 기능 중 `(`위에 커서를 놓고 `%`를 입력하면 짝이 맞는 `)`위로 커서를 옮겨주는 것이 있습니다.
이 옵션을 편집하면 괄호 외에도 지정한 문자의 짝을 찾아 이동하게 할 수 있습니다.

```viml
" 다음과 같이 하면 < 과 > 도 짝으로 지정되어 % 로 이동할 수 있게 됩니다.
set mps=(:),{:},[:],<:>

" 기본 설정을 또다시 작성하는 것이 번거롭다면 다음과 같이 하면 기본 설정에 <:> 을 추가할 수 있습니다.
set mps+=<:>
```

* `:autocmd`를 사용하면 파일 타입에 따라 다르게 작동하게 만들 수도 있습니다.

```viml
" 파일 확장명이 c,cpp,java 인 경우 = 와 ; 를 짝으로 지정합니다.
:au FileType c,cpp,java set mps+==:;
```

* 주의 : 같은 문자는 짝으로 지정할 수 없습니다. 따라서 `":"`나 `':'`는 설정할 수 없습니다.
* 참고 : [matchit 플러그인](http://www.vim.org/scripts/script.php?script_id=39)을 사용하면
`%`로 html 태그와 닫는 태그 사이를 점프할 수 있습니다.

#### `mouse`
* string 옵션. 모드별 마우스 사용을 설정합니다. 기본값은 gui 인 경우 `a`.
* 터미널 VIM의 경우 마우스 사용이 설정되어 있지 않기 때문에 VIM 편집 화면을 마우스로 클릭해도 커서 위치가 이동하는 일은 없습니다.
따라서 (드물겠지만)마우스로 편집 화면을 클릭해서 커서 위치를 옮기는 일이 가능하게 하려면 이 옵션을 설정해주어야 합니다.
* `n`,`v`,`i`,`c`,`h`,`a`,`r` 이렇게 7 가지의 옵션이 있지만 대부분 모드에 따라 마우스 사용을 하나씩 허용하는 내용입니다.
* 기왕 마우스 사용을 설정하고 싶다면 모든 모드를 의미하는 `a`옵션만 설정해 주면 됩니다.

```viml
set mouse=a
```

#### `mousehide`, `mh`
* boolean 옵션. 타이핑 중엔 마우스 포인터를 숨겨줍니다. 기본값은 `on`.
* gui VIM 에서만 설정 가능합니다.

#### `nrformats`, `nf`
* list 옵션. `<C-a>`, `<C-x>` 증감 대상이 되는 숫자의 패턴을 지정합니다. 기본값은 `bin,ortal,hex`
* NORMAL 모드에서 숫자 위에 커서를 올린 다음 `<C-a>`를 입력하면 숫자가 `1`씩 늘어나고, `<C-x>`를 입력하면 숫자가 `1`씩 줄어듭니다.
종종 복잡한 숫자를 변경할 일이 있을 때 편리합니다. 가령 `248`같은 숫자를 뺄셈하려면 암산을 하거나 계산기를 써야 할 텐데,
그냥 NORMAL 모드에서 `248<C-x>`만 입력하면 되거든요. 특히 암산이 어려운 2진수, 8진수, 16진수를 다룰 때 도움이 됩니다.
* 옵션 목록은 다음과 같습니다.
    * `alpha` : 알파벳을 증감합니다. 즉, `a`위에 커서를 놓고 `<C-a>`를 입력하면 `b`가 됩니다.
    * `octal` : `0`으로 시작하는 숫자들을 8진수로 인식하고 증감합니다.
    * `hex` : `0x`, `0X`로 시작하는 숫자들을 16진수로 인식하고 증감합니다.
    * `bin` : `0b`, `0B`로 시작하는 숫자들을 2진수로 인식하고 증감합니다.
* 참고 : `1`에서 `9`로 시작하는 보통 숫자는 기본적으로 10진수로 인식됩니다.

```viml
" 모두 설정하려면 다음과 같이 하면 됩니다.
set nf=alpha,octal,hex,bin
```

```viml
" 작업중, 잠시의 필요에 따라 추가하려면 커맨드라인에서 다음과 같이 입력합니다.
:set nf+=bin
" 제거하려면 다음과 같이 합니다.
:set nf-=bin
```

#### `number`, `nu`
* boolean 옵션. 화면 왼쪽에 라인 넘버를 보여줍니다. 기본값은 `off`.
* VIM 사용 중에는 라인 점프를 많이 하게 되니 필수적인 옵션이라 볼 수 있습니다. 추천값은 `on`.

#### `numberwidth`, `nuw`
* number 옵션. 화면 왼쪽 라인 넘버의 width를 설정합니다. 기본값은 `4`.

#### `omnifunc`, `ofu`
* string 옵션. INSERT 모드에서의 `<C-x><C-o>` 자동완성 기능을 설정합니다. 기본 값은 없습니다.
* 설정을 위해 공부해야 하는 내용이 많은 옵션입니다. 자세한 내용을 보려면 `:h complete-functions`를 입력합니다.
* 자동완성 플러그인인 [youcompleteme](https://github.com/Valloric/YouCompleteMe)을 설치했다면 다음과 같이 설정하게 됩니다.

```viml
set omnifunc=syntaxcomplete#Complete
```

#### `operatorfunc`, `opfunc`
* string 옵션. 자신만의 operator 를 만들 수 있는 옵션입니다. 기본값은 없습니다.
* NORMAL 모드의 핵심을 이루는 operator 는 motion 앞에 쓰여 각 모션의 동작을 지시합니다.
`d`나 `y`같은 명령어들이 operator 라 할 수 있습니다. 예를 들어 `d3j`는 3줄을 삭제합니다.
* `operatorfunc` 옵션은 `g@` operator 에 사용자가 작성한 함수이름을 매핑하는 기능이라 할 수 있습니다.
이후 `g@` 와 motion을 입력하면 지정한 함수를 실행해줍니다.
* `g@`의 입력이 번거롭게 느껴지겠지만 큰 문제는 안 됩니다. `:map`이 있으니까요.
* 자세한 내용과 예제는 `:help 'operatorfunc'`를 참고하면 됩니다.

#### `pumheight`, `ph`
* number 옵션. INSERT 모드에서 자동완성 기능을 사용할 때 보여줄 아이템 숫자의 max 값을 설정합니다.

#### `readonly`, `ro`
* boolean 옵션. READONLY 모드가 되어 `:w`로 저장이 되지 않습니다. 기본값은 `off`.
* READONLY 모드일 때 저장을 하려면 `:w!`를 통해 강제로 하면 됩니다.

#### `relativenumber`, `rnu`
* boolean 옵션. 라인 넘버를 커서 위치 상대값으로 보여줍니다. 기본값은 `off`.
* 만약 수시로 상대 라인 넘버와 절대 라인 넘버를 바꿔가며 사용하려면 다음과 같은 함수를 `.vimrc`에 넣어두고 `:map`을 정의하면 편리합니다.

```viml
function! ToggleNumber()
    if(&relativenumber == 1)
        set norelativenumber
        set number
    else
        set relativenumber
    endif
endfunc
```

#### `remap`
* boolean 옵션. `:map`으로 설정한 값들이 재귀적으로 작동하는 것을 허용합니다. 기본값은 `on`.
* 이 값은 가능한 한 `off`로 하지 않는 쪽이 좋습니다.
수많은 Vim script 와 플러그인들이 이 값이 `on`인 상태를 전제하고 작성되었기 때문입니다.
(`:map`을 멀리하고 `:nnoremap`, `:inoremap`, `:vnoremap`, `:cnoremap`을 가까이 하는 것이 좋습니다.)

#### `revins`, `ri`
* boolean 옵션. INSERT 모드에서 타이핑을 하면 가장 왼쪽에 새로운 글자들이 들어갑니다. 즉 오른쪽에서 왼쪽으로 글을 쓰게 됩니다. 기본값은 `off`.

#### `rightleft`, `rl`
* boolean 옵션. 이 옵션을 설정하면 (아랍어처럼) 오른쪽에서 왼쪽 쓰기가 되어 화면의 좌우가 바뀝니다.
* VIM을 시작한 친구에게 이 옵션으로 장난을 치지 마세요.

#### `ruler`, `ru`
* boolean 옵션. 커서 위치 정보를 상태 라인에 보여줍니다. 기본값은 `off`.

#### `runtimepath`, `rtp`
* list 옵션. VIM이 런타임에 파일을 검색해 참조하는 디렉토리의 목록입니다.
* 자세한 내용은 `:help 'runtimepath'`를 참고.

#### `scroll`, `scr`
* number 옵션. `<C-u>`, `<C-d>`로 한 번에 스크롤할 라인의 숫자를 지정합니다. 기본값은 터미널 height의 절반.

#### `scrolljump`, `sj`
* number 옵션. 커서가 화면 끝에 도달한 다음, 한 번 더 이동할 때 점프할 라인 수를 지정합니다. 기본값은 `1`.
* 이 옵션은 `<C-y>`, `<C-e>`에 영향을 주는 옵션이 아닙니다.
말하자면 화면 끝에 도달했을 때의 `j`,`k`에 영향을 주는 옵션이라 할 수 있습니다.

#### `scrolloff`, `so`
* number 옵션. 커서 스크롤의 offset을 지정합니다. 기본값은 `0`.
* 이 옵션을 설정하고 `H`, `L`을 입력해 보면 의미를 바로 알 수 있습니다. 예를 들어 `3`으로 설정하면 커서를 아무리 위로 올려도 (가장 윗 줄이 아니라면) 항상 커서보다 위에 3 줄이 있게 됩니다. 아래쪽도 마찬가지입니다.

#### `shell`, `sh`
* string 옵션. `:!` 명령에서 사용할 쉘을 지정합니다. 기본값은 `$SHELL` 또는 `sh` 입니다. MS 계열이라면 기본값은 `command.com`이나 `cmd.exe`가 됩니다.
* VIM 을 사용해 편집작업을 하는 도중 쉘 명령어를 사용하는 방법들이 몇 가지 있습니다.
    * `:shell` 명령어 사용. VIM에서 관리하는 터미널이 열립니다. 다시 돌아오려면 `$ exit`하면 됩니다.
    * `:!` 명령어 사용. 내부에서 외부 명령어를 바로 실행할 수 있습니다. 가령, `:! touch test`는 test라는 파일을 생성하고, `:! rm test`는 test 파일을 삭제합니다. 자세한 내용은 `:help :!`을 참고.
        * 실행 결과를 보려면 `:r!`를 쓰면 됩니다. 예를 들어 `:r! ls`는 `ls`실행 결과를 현재 커서 위치에 붙여넣습니다.
        * 만약 실행 결과를 보고는 싶은데 편집기에 붙여넣고 싶지는 않다면, 레지스터에 집어넣는 방법도 있습니다.
```viml
:let @a=system('ls')    " a 레지스터에 ls 실행 결과 출력문을 입력합니다.
```

#### `shiftwidth`, `sw`
* number 옵션. `cindent`, `<<`, `>>`에서 사용하는 인덴트 길이를 지정합니다. 기본값은 `8`.

#### `showbreak`, `sbr`
* string 옵션.  한 줄이 너무 길어 여러 줄로 표현될 때, 아래쪽 줄들이 윗쪽 줄에서 이어짐을 설정한 기호를 사용해 가장 왼쪽에 표시합니다.
* 추천하는 값은 다음과 같습니다.

```viml
set showbreak=+++\ 

" 다음과 같이 해도 됩니다.
:let &showbreak = '+++ '
```

#### `showcmd`, `sc`
* boolean 옵션. NORMAL 모드에서 입력중인 명령어를 화면의 오른쪽 아래에 보여줍니다. 기본값은 `on` 이지만, Unix라면 `off`입니다.
* 만약 터미널이 느리다면 이 옵션을 `off`로 해보는 것도 도움이 될 수 있습니다.

#### `showmatch`, `sm`
* boolean 옵션. 짝이 맞는 괄호에 하이라이팅 처리를 해 줍니다. 기본값은 `off`.

#### `showtabline`, `stal`
* number 옵션. 화면 상단의 탭 라인 노출을 설정합니다. 기본값은 `1`.
* 세 가지 옵션이 있습니다.
    * `0` : 탭 라인을 보여주지 않습니다.
    * `1` : 탭이 두 개 이상일 때만 보여줍니다.
    * `2` : 탭 라인을 항상 보여줍니다.

#### `sidescroll`, `ss`
* number 옵션. 수평 스크롤을 할 때 한 번에 스크롤할 컬럼 수를 지정합니다. 기본값은 `0`.
* 참고 : 좌우 스크롤를 사용하려면 `wrap`옵션을 `off`로 설정해야 합니다.

```viml
set nowrap
set sidescroll=2
set sidescrolloff=10
```

#### `sidescrolloff`, `siso`
* number 옵션. 수평 스크롤을 할 때의 offset을 지정합니다. 기본값은 `0`.

#### `smartcase`, `scs`
* boolean 옵션. 검색시 검색어에 대문자가 포함되어 있다면 `ignorecase`옵션을 무시합니다. 기본값은 `off`.
* `ignorecase`옵션과 함께 설정하는 쪽을 추천합니다.

#### `smartindent`, `si`
* boolean 옵션. 다음 라인을 편집할 때 프로그래밍 언어 신택스를 고려하여 자동으로 인덴트를 넣어줍니다. 기본값은 `off`.

#### `smarttab`, `sta`
* boolean 옵션. `<BS>`로 스페이스 인덴트를 지울 때 탭 단위로 삭제합니다. 기본값은 `off`.
* 탭을 스페이스로 대체할 때 가장 귀찮은 점인 인덴트 삭제를 편리하게 해 주는 기능입니다. `shiftwidth`, `tabstop`등을 고려하여 작동합니다.
* 예를 들어 탭 하나를 스페이스 4 개로 설정해 놓았다면, 8개 스페이스로 이루어진 인덴트를 `<BS>` 두 번으로 지울 수 있씁니다.

#### `startofline`, `sol`
* boolean 옵션. 라인 점프를 할 때, 커서를 첫 번째 글자 위치로 옮깁니다. 기본값은 `on.`
* 이 옵션이 `on`이면 `H`, `G`같은 명령을 사용할 때, 커서가 항상 가장 왼쪽 글자의 위치로 이동합니다.
* `off` 상태일 때는 커서의 좌우 위치를 이동하지 않고 점프합니다.

#### `statusline`, `stl`
* 화면 하단의 상태표시줄 형식을 편집할 수 있습니다.
* 자세한 내용은 `:help statusline` 참고.

#### `switchbuf`, `swb`
* list 옵션. 버퍼 이동을 할 때 윈도우와 탭 등의 작동을 설정합니다. 기본값은 없습니다.
* 가능한 옵션들은 다음과 같습니다.
    * `useopen` : 버퍼 이동을 하면 해당 버퍼가 열려 있는 첫 번째 윈도우로 점프합니다. 해당 윈도우가 없다면, 현재 윈도우에 열어줍니다.
    * `usetab` : `useopen`과 비슷하지만, 이 옵션은 탭을 사용합니다.
    * `split` : 윈도우를 상하로 분할합니다.
    * `vsplit` : 윈도우를 좌우로 분할합니다.
    * `newtab` : 새로운 탭을 엽니다.
* 기본값으로 사용하는 것을 추천합니다.

#### `syntax`, `syn`
* string 옵션. 해당 신택스를 적용합니다. 기본값은 없습니다.
* 주로 프로그래밍 언어별 신택스 플러그인 내부에 정의됩니다.

#### `tabline`
* string 옵션. 탭 페이지 라인의 형식을 편집할 수 있습니다. 기본값은 없습니다.
* `statusline`과 비슷한 값으로 편집할 수 있습니다. 자세한 내용은 `:help setting-tabline` 참고.

#### `tabstop`, `ts`
* number 옵션. `<Tab>`을 몇 개의 `<Space>`로 대체할지를 설정합니다. 기본값은 `0`.
* `<Tab>`을 `<Space>`로 변경해주는 `:retab` 명령어가 이 값을 참조합니다.

#### `tildeop`, `top`
* `~` 명령어를 operator 처럼 사용할 수 있게 됩니다. 기본값은 `off`.
* 대소문자 변경을 자주 한다면 이 옵션이 도움될 수 있습니다. `~$`, `~3j`같은 명령이 가능하게 됩니다.

#### `timeout`, `to`
* boolean 옵션. 명령어 키스트로크 입력시의 타임아웃을 설정해 줍니다.
* 단독으로 설정하기보다 `ttimeout`, `timeoutlen`, `ttimeoutlen` 도움말 항목을 읽어보고 함께 설정해주는 것이 좋습니다.
* 가급적이면 건드리지 않도록 합니다.

#### `title`
* boolean 옵션. 윈도우 타이틀이 표시되도록 합니다. 기본값은 `off`.
* VIM이 `+title` 옵션과 함께 컴파일 되었어야 쓸 수 있습니다.

> `$ vim --version | grep +title` 로 확인할 수 있습니다.

#### `titlelen`
* number 옵션. 윈도우 타이틀 문자열의 길이를 설정합니다. 기본값은 `85`.
* VIM이 `+title` 옵션과 함께 컴파일 되었어야 쓸 수 있습니다.

#### `titlestring`
* string 옵션. 윈도우 타이틀의 형식을 설정합니다. 기본값은 없습니다.
* 터미널이 해당 기능을 지원해야만 사용할 수 있습니다.
* 형식은 `statusline`과 같습니다.

#### `transparency`, `transp`
* number 옵션. 백그라운드 화면의 투명도를 퍼센트 값으로 설정합니다. 기본값은 `0`.
* 불투명인 `0`부터, 완전 투명인 `100`사이에서 지정해 주면 됩니다.
* MacVIM 에서만 됩니다.

#### `undodir`, `udir`
* list 옵션. undo 파일을 보관할 디렉토리의 이름을 나열합니다. 기본값은 `.`.
* 편집중 발생하는 undo 가능한 문자열들을 따로 파일로 보관하는 기능을 활용할 때 사용합니다.
* 포맷은 `:help backupdir`을 참고하면 됩니다.

#### `undofile`, `udf`
* boolean 옵션. VIM이 자동으로 undo history 를 파일로 기록하게 합니다. 기본값은 `off`.

#### `undolevels`, `ul`
* number 옵션. undo history 사이즈를 설정합니다. 기본값은 `100`, Unix/Windows는 `1000`.
* 이 옵션을 `0` 으로 주면 undo 가 한 번 밖에 안 됩니다!
* 이 옵션을 음수 값으로 주면 undo 를 사용할 수 없게 됩니다!
* 이 옵션을 음수 값으로 설정했다가 다시 양수 값으로 설정하면 undo 기록을 clear할 수 있습니다.

#### `visualbell`, `vb`
* boolean 옵션. 에러가 발생했을 때 삑 소리를 내지 않고 화면으로 알려 줍니다. 기본값은 `off`.
* `errorbells` 도움말 항목도 참고.

#### `whichwrap`, `ww`
* list 옵션. 좌우방향 이동으로 라인 이동 가능 여부를 설정합니다. 기본값은 `b,s`.
* `h`, `l`로는 라인 끝에 도달했을 때, 이전/다음 라인으로 이동할 수 없는데, 이 설정으로 가능하게 할 수 있습니다.
* 자세한 내용은 `:help 'ww'`를 참고.

```viml
set ww+=h,l     " h,l 로도 라인 이동이 가능합니다.
```

#### `wildchar`, `wc`
* number 옵션. command-line 에서 자동완성 기능에 사용할 키를 설정합니다. 기본값은 `<Tab>`.
* 키 넘버를 입력해야 하는 number 옵션이지만, `<키>`형식을 사용할 수 있습니다.

```viml
set wc=<Tab>    " command-line 자동 완성 키를 <Esc>로 변경. (이렇게 하면 불편합니다. 그냥 <Tab>을 쓰세요.)
```

#### `wildcharm`, `wcm`
* number 옵션. `wildchar`와 비슷하지만 매크로 내에서만 사용됩니다.
* 다음은 vim help 의 예제입니다.

```viml
:set wcm=<C-Z>
:cnoremap ss so $vim/sessions/*.vim<C-Z>
```

#### `wildignore`, `wig`
* list 옵션. 파일/디렉토리명 자동완성을 할 때 무시할 패턴을 설정합니다. 기본값은 없습니다.

```viml
set wildignore=*.o,*.bak
```

#### `whildignorecase`, `wic`
* boolean 옵션. 파일명이나 디렉토리명을 자동완성할 때 대소문자를 무시합니다. 기본값은 `off`.
* 추천값은 `on`.

#### `wildmenu`, `wmnu`
* boolean 옵션. command-line 자동 완성 기능을 좀 더 편리하게 확장합니다. 기본값은 `off.`
* 추천값은 `on`.

#### `wrap`
* boolean 옵션. 화면을 넘어가는 긴 라인을 여러 줄로 표현합니다. 기본값은 `on`.
* 이 옵션을 `on`으로 하면 좌우 스크롤이 필요없게 됩니다.
다만 라인 하나가 최소 두 줄이 되어 커서를 움직일 때 좀 헷갈릴 수도 있습니다.
    * `on`으로 사용하려면 `linebreak`, `showbreak` 등을 함께 설정해주면 좋습니다.

```viml
set linebreak       " 라인을 끊을 때 단어 단위로 자릅니다.
set showbreak=+++\  " 윗 줄과 연결되는 줄은 '+++ ' 로 시작되어 알아볼 수 있게 합니다.
```

* 이 옵션을 `off`로 설정하면 긴 라인이 있는 경우 좌우 스크롤을 해야 할 수 있습니다.
    * `off`로 사용하려면 `sidescroll`, `list`, `listchars` 등을 함께 설정해주면 좋습니다.

```viml
set nowrap
set sidescroll=2
set sidescrolloff=10    " 좌우 스크롤 offset 설정
set list listchars+=extends:>,precedes:<    " 왼쪽 스크롤이 필요한 경우 <, 오른쪽 스크롤이 필요한 경우 > 를 보여준다.
```

#### `write`
* boolean 옵션. 파일 쓰기를 가능하게 합니다. 기본값은 `on`.
* 이 옵션을 `off`로 하면 readonly 모드가 됩니다. 편집은 되지만 저장하려 하면 경고가 나옵니다.
VIM을 less 처럼 사용하는 방법이라 할 수 있습니다.

#### `writebackup`, `wb`
* boolean 옵션. 파일을 덮어쓰기 전에 백업 파일을 만듭니다. 기본값은 `on`.
* 파일이 성공적으로 저장되면 백업 파일은 자동으로 삭제됩니다.

## 참고 자료
* `:help option-summary`
* http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys

