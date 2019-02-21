# map과 abbreviate

* [map 사용법](#map-사용법)
    * [map 명령어](#map-명령어)
    * [map 사용 예제](#map-사용-예제)
    * [nore의 의미](#nore의-의미)
* [abbreviate 사용법](#abbreviate-사용법)
    * [abbreviate 사용 예제](#abbreviate-사용-예제)
    * [필요한 경우 abbreviate에서도 nore를 고려합시다](#필요한-경우-abbreviate에서도-nore를-고려합시다)
    * [normal 모드의 활용](#normal-모드의-활용)
* [참고 자료](#참고-자료)

## map 사용법

* `:map` 명령어 시리즈를 사용하면 자신만의 단축키를 설정할 수 있습니다.
* 단순히 특정 명령과 키 조합을 연결하는 기능이 아니라 키스트로크를 지정하는 방식이기 때문에 기능에 제한이 없습니다.

예를 들자면 다음과 같은 일들이 가능합니다. 다음 예는 모두 vim help에 있는 것들입니다.
```viml
:map <F3>  o#include                "<F3>을 누르면 커서 아래에 새로운 라인을 추가하고 #include 라고 씁니다.
:map <M-g> /foo<CR>cwbar<Esc>       "<M-g>를 누르면 foo를 검색하고 첫 번째로 검색된 foo를 bar로 replace합니다.
:map _x    d/END/e<CR>              "_x를 누르면 현재 커서 위치부터 이후에 나오는 첫 번째 END의 D위치까지 삭제합니다.
:map! qq   quadrillion questions    "qq를 누르면 quadrillion questions를 입력합니다.
:map <F1><Esc>OP :echo "yes"<CR>    "<F1><Esc>OP를 순서대로 입력하면 'yes'를 출력합니다.
```

즉, 사용자가 할 수 있는 거의 모든 일들을 `map`을 사용해 등록해 두고 원하는대로 사용할 수 있습니다.

### map 명령어

* `map`명령어는 기본형이
`:map`, `:nmap`, `:vmap`, `:smap`, `:xmap`, `:omap`, `:map!`, `:imap`, `:lmap`, `:cmap`
으로 10 가지가 있으며, `:noremap`, `:nnoremap` 과 같이 `nore`조합을 따지면 20가지가 됩니다.
* 이는 초심자에게는 너무 많으므로 핵심적인 몇 가지만 소개하도록 합니다.

명령어    | 사용자 정의 호출 방지 | 적용 대상                                       | 축약 표현 | 축약표현(사용자정의호출방지)
--------  | ------                | :---------------------------------------------- | ------    | ------
`:nmap`   | `:nnoremap`           | NORMAL 모드의 단축키를 지정합니다.              | `:nm`     | `:nn`
`:nunmap` |                       | `nmap`을 해제                                   | `:nun`    |
`:vmap`   | `:vnoremap`           | VISUAL 모드의 단축키를 지정합니다.              | `:vm`     | `:vn`
`:vunmap` |                       | `vmap`을 해제                                   | `:vun`    |
`:imap`   | `:inoremap`           | INSERT  모드의 단축키를 지정합니다.             | `:im`     | `:ino`
`:iunmap` |                       | `imap`을 해제                                   | `:iun`    |
`:cmap`   | `:cnoremap`           | Command-line 입력 모드의 단축키를 지정합니다.   | `:cm`     | `:cno`
`:cunmap` |                       | `cmap`을 해제                                   | `:cun`    |

* 너무 많다 싶으면 `:nnoremap` 과 `:inoremap`만 기억해두어도 충분합니다.

### map 사용 예제

* 기본적인 사용법은 VIM을 사용도중 `:map ...`과 같이 등록하여 사용하는 것이지만,
    이렇게 하면 VIM을 종료한 후 다시 실행했을 때에는 해당 단축키는 사라지게 됩니다.
* 따라서 `map`명령어를 잘 사용하는 방법은 VIM 설정 파일인 `.vimrc`에 등록해서 사용하는 것입니다.

> 참고로 `.vimrc`에 `map` 명령어를 추가할 때에는 Command-line을 활성화시키는 명령어인 `:`를 제외하도록 합니다.

명령어              | 기능
------              | :--------------------------------------------------------------------------
`nmap <F2> :w<CR>`  | NORMAL 모드에서 `<F2>`를 누르면 현재 편집중인 버퍼를 파일에 저장한다. (`<CR>`은 `<Enter>`와 같음)
`imap <C-a> <Home>` | INSERT 모드에서 `<C-a>`를 누르면 `<Home>`키를 입력하여 현재 라인의 첫째 글자로 이동한다.
`vnoremap <Space>y "*y` | VISUAL 모드에서 `<Space>`를 누르고 `y`를 누르면 선택한 영역을 `"*` 레지스터로 복사한다.

### nore의 의미
* `:nnoremap`은 기본적으로는 `:nmap`과 같습니다. 단, 사용자가 매핑한 키 조합을 호출하는 경우를 방지합니다.

예를 들어 `.vimrc`에 다음과 같이 설정했다고 가정해 봅시다.
```viml
nmap w 3l
nmap e w
nnoremap r w
```
* `w`를 누르면 `3l`을 입력하게 됩니다.
* `e`를 누르면 `w`를 입력하게 되어 최종적으로는 `3l`을 입력하게 됩니다.
* `r`를 누르면 사용자가 정의한 `3l`이 아니라 그냥 `w`를 입력하게 됩니다.
`w`는 VIM의 기본 명령어이므로 커서를 다음 단어로 이동시킵니다.

`e`와 `r`이 똑같이 `w` 입력을 매핑했음에도 결과가 달라집니다. 가급적이면 `nore`명령어를 사용하는 쪽이 혼란을 줄일 수 있습니다.

* 결론 : `:nnoremap`, `:vnoremap`, `:inoremap`, `:cnoremap`을 씁시다.

## abbreviate 사용법

* abbreviate는 자주 사용하는 상용구 등을 등록하여 타이핑을 편하게 해 주는 명령어입니다.
* 이것 또한 `.vimrc`에 등록해 놓고 사용하면 편리합니다.
* 등록한 abbreviate 자동 완성은 INSERT 모드와 command-line 입력 모드에서만 사용할 수 있습니다.

명령어          | 사용자 정의 호출 방지 | 적용 대상/기능            | 축약 표현 | 축약표현(사용자정의호출방지)
--------        | ------                | :-----------              | ------    | ------
`:abbreviate`   | `:noreabbrev`         | INSERT, Command-line 모드 | `:ab`     | `:norea`
`:unabbreviate` |                       | `abbreviate`해제          | `:una`    |
`:cabbrev`      | `:cnoreabbrev`        | Command-line 모드         | `:ca`     | `:cnorea`
`:cunabbrev`    |                       | `cabbrev`해제             | `:cuna`   |
`:iabbrev`      | `:inoreabbrev`        | INSERT 모드               | `:ia`     | `:inorea`
`:iunabbrev`    |                       | `iabbrev`해제             | `:iuna`   |
`:abclear`      |                       | 모든 `abbreviate`를 해제  | `:abc`    |
`:iabclear`     |                       | 모든 `iabbrev`를 해제     | `:iabc`   |
`:cabclear`     |                       | 모든 `cabbrev`를 해제     | `:cabc`   |

명령어가 많고 복잡하니 간편하게 사용하고 싶다면 `:ab`와 `:una`만 알아둬도 됩니다.

### abbreviate 사용 예제
```viml
:ab rtfm read the fine manual
```
* 위와 같이 설정하면 INSERT 모드에서 `rtfm<Space>` 또는 `rtfm<CR>`을 입력하면 입력한 `rtfm`을 `read the fine manual`로 자동 완성해 줍니다.
* `:ab`는 사용자 정의를 호출할 수 있으므로 의도적으로 이를 사용할 수도 있습니다.
```viml
:ab myname John Grib
:ab hi hello myname
```
이와 같이 등록해 놓고 `hi`를 입력하면 `hello John Grib`으로 자동완성해 줍니다.

### 필요한 경우 abbreviate에서도 nore를 고려합시다

* `:map` 명령어 시리즈의 경우, 가능한한 `:map`이 아니라 `:noremap`시리즈를 사용하는 쪽이 안전합니다.
하지만 `:abbreviate`는 INSERT 모드와 Command-line 모드에서만 작동하므로 잘못 조작해서 문자열을 마구 삭제한다던가 하는 일은 일어나지 않습니다. 즉 `:map`에 비해 상대적으로 안전하므로 사용자 정의 호출 방지를 크게 신경쓸 필요가 없습니다.
* 그러나 자동완성 문구가 축약어를 포함하는 경우에 대해서도 알아두도록 합시다.
* 결론을 먼저 말하자면, `abbreviate`가 재귀하는 경우 스택오버플로우는 일어나지 않습니다.
그리고 재귀호출은 1번만 일어납니다.

위의 예제를 수정하여, 다음과 같은 `abbreviate`를 지정해 주었다고 합시다.
```viml
:ab rtfm read the fine manual rtfm
```
INSERT 모드에서 `rtfm`을 입력해 보면 다음과 같은 결과를 볼 수 있습니다.
```
read the fine manual read the fine manual rtfm
```
`rtfm`이 `read the fine manual rtfm`으로 완성되고, 마지막으로 추가된 `rtfm`이 다시 한 번 자동완성 되어 `read the fine manual`이 두 번 반복된 모양이 되었습니다. 그리고 두 번째 완성된 문구의 마지막에 `rtfm`이 남아 있는 것으로 보아 재귀는 한 번만 가능함을 알 수 있습니다.

이것이 의도된 결과라면 괜찮겠지만,
그렇지 않다면 `:norea rtfm read the fine manual rtfm`을 사용하는 쪽이 바람직합니다.

```viml
:norea rtfm read the fine manual rtfm
```
위와 같이 설정한 다음 INSERT 모드에서 `rtfm`을 입력해 보면 `read the fine manual rtfm`으로 자동완성됩니다.

### normal 모드의 활용

`<Esc>`를 사용하면 NORMAL 모드로 들어갈 수 있습니다.

```viml
:abbr _cmt /* */<Esc>hhi
```

위와 같이 등록한 다음, `_cmt`를 입력하면 `/* */`가 자동으로 완성되고, 커서가 가운데의 스페이스 부분으로 이동해 있게 됩니다.

(`_cmt` 앞에 `_`를 붙인 이유는 `cmt`만 써도 멋대로 자동 완성이 되어서 골치가 아프기 때문입니다.)

이 기능을 활용하면 `import`, `if`, `for` 문처럼 괄호가 많고 줄바꿈이 있는 형태의 템플릿을 만들어 두고 사용할 수 있습니다.

### expr로 vimscript 실행하기

`<expr>`을 사용하면 vimscript 실행 결과로 완성해 줍니다.

다음은 제가 사용하고 있는 abbr 입니다.

```viml
iabbr __email abcd@efgh.com
iabbr <expr> __time strftime("%Y-%m-%d %H:%M:%S")
iabbr <expr> __file expand('%:p')
iabbr <expr> __name expand('%')
iabbr <expr> __pwd expand('%:p:h')
iabbr <expr> __branch system("git rev-parse --abbrev-ref HEAD")
```

* `__time`
    * vim 내장 함수인 strftime을 실행하여 나온 결과(현재 시간)로 완성해 줍니다.
    * 예: `__time`을 입력하면 `2018-11-23 09:25:07`와 같이 나옵니다.
* `__file`
    * vim 내장 함수인 `expand`를 실행하여 나온 결과(현재 편집중인 파일의 전체 경로)로 완성해 줍니다.
* `__branch`
    * 현재 git branch를 완성해 준다.
* 그 외 생략

특히 마지막의 `system` 함수를 사용하면 셸 명령어를 실행한 결과를 가져올 수 있어 편리합니다.

## 참고 자료
* http://vim.wikia.com/wiki/Using_abbreviations
* [vim 자동완성 기능 사용하기](https://johngrib.github.io/wiki/vim-auto-completion/ )
