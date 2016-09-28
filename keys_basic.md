# 키 조합에 대하여
* 키 조합에 대한 기본 정보는 `:help key-notation`으로 볼 수 있습니다.

키 표기  | 의미                            | 예제
------   | :------------------------------ | ---
`<C-키>` | `Ctrl+키`                       | `<C-v>` : `CTRL`을 누른 상태에서 `v`를 누른다.
`<A-키>` | `Alt+키`                        | `<A-Space>` : `ALT`를 누른 상태에서 `Space`키를 누른다.
`<M-키>` | `Meta+키`                       | `<M-CR>` : `META`키를 누른 상태에서 `Enter`키를 누른다.
`<S-키>` | `Shift+키`                      | `<S-BS>` : `Shift`키를 누른 상태에서 `backspace`키를 누른다.
`<D-키>` | `Command+키` (mac에서만 가능)   | `<D-F1>` : `command`키를 누른 상태에서 `F1`키를 누른다.

### 이 문서를 처음 읽는 VIM 초심자라면
* `<C-a>`가 `CTRL`키와 `a`키를 함께 누르는 의미라는 정도만 알고 넘어가도 됩니다.
* 아래부터는 VIM에 좀 익숙해지고, 자신만의 설정 파일이 필요할 때 읽으셔도 됩니다.

------

### [`META`](https://en.wikipedia.org/wiki/Meta_key) 키에 대하여
* `META`키는 오래전에 터미널 제조사에 따라 `ALT`키 개념이 통일되지 않았을 때 나온 키 값으로, 요즘은 그냥 `ALT`키라고 생각하면 됩니다.
* 만약 `META` 키가 없는 터미널에서 `META` 키를 입력하려면 `<ESC>`키를 누르면 됩니다.
> `M-c`를 입력하고 싶다면 `<ESC>`를 누르고, `c`를 누릅니다.

* `option`키 조합이 특수문자 입력인 mac 터미널에서는 `<ESC>`를 사용하면 됩니다.
* iTerm2 에서 `META`키를 사용하고 싶다면 `Preferences > Profiles > Keys`에서 `option`키를 `+Esc`로 매핑해줍니다.
> 하지만 이렇게 하면 VIM에서 `option`키를 사용하기 난감해집니다. MacVIM에서 `macmeta`를 쓰거나 다른 방식으로 `option`키를 쓰고 있다면 `+Esc` 설정이 더 불편할 수 있기 때문에, 차라리 `$ set -o vi` 사용이 낫다고 봅니다.

### key-notation 일람
* `키 표기`는 VIM 문서나 `.vimrc`같은 설정 파일에서 사용하는 것으로, 잘 알아두면 여러모로 도움이 됩니다.
* `추가 입력 방법`은 키보드에서 해당 키를 입력해 입력하는 방법 외의 다른 방법으로 입력하는 방법을 의미합니다.
* 예를 들어 `backspace`의 경우 추가 입력 방법이 `<C-h>`인데, 키보드에서 키가 망가졌거나 입력 상황에 따라 불가능하다거나 하는 이유로 `backspace`키를 입력할 수 없다면 `<C-h>`를 통해 `backspace`를 입력할 수 있습니다.
* 추가 입력 방법을 몰라도 VIM을 사용하는 데에는 큰 문제가 없습니다. 그러나 VIM을 고급스럽게 사용하려 할 때 좋은 힌트가 되는 지식들이라 할 수 있습니다.

    >가령 `<C-[>`가 `<Esc>`입력을 발생시킨다는 것을 알고 있다면, `<Esc>`입력이 곤란한 상황이 되었을 때 도움이 될 수 있습니다.

    >또한 `:map`을 통해 새로운 단축키를 지정할 때에도 사용할 수 있는데, `:map <NL> ...`는 `:map <C-j> ...`와 동일하게 작동합니다.

키 표기          | 설명                                            | 추가 입력 방법
---------------  | :---------------------------------------------- | ---------
`<BS>`           | backspace                                       | `<C-h>`
`<Tab>`          | tab                                             | `<C-i>`
`<NL>`           | linefeed. 현대적으로는 `<ENTER>`로 보면 된다.   | `<C-j>`
`<FF>`           | formfeed                                        | `<C-l>`
`<CR>`           | carriage return. `<ENTER>`로 보면 된다.         | `<C-m>`
`<Return>`       | `<CR>`과 같다.                                  |
`<Enter>`        | `<CR>`과 같다.                                  |
`<Esc>`          | escape                                          | `<C-[>`
`<Space>`        | space
`<lt>`           | less-than                                       | <
`<Bslash>`       | backslash                                       | \
`<Bar>`          | vertical bar                                    | &#124;
`<Del>`          | delete                                          |
`<Up>`           | cursor-up                                       |
`<Down>`         | cursor-down                                     |
`<Left>`         | cursor-left                                     |
`<Right>`        | cursor-right                                    |
`<F1>` - `<F12>` | function keys 1 to 12                           |
`<Insert>`       | insert key                                      |
`<Home>`         | home                                            |
`<End>`          | end                                             |
`<PageUp>`       | page-up                                         |
`<PageDown>`     | page-down                                       |
`<kHome>`        | keypad home                                     |
`<kEnd>`         | keypad end                                      |
`<kPlus>`        | keypad +                                        |
`<kMinus>`       | keypad -                                        |
`<kMultiply>`    | keypad *                                        |
`<kDivide>`      | keypad /                                        |
`<kEnter>`       | keypad Enter                                    |
`<kPoint>`       | keypad Decimal point                            |
`<k0>` - `<k9>`  | keypad 0 to 9                                   |

#### 사용 예제
* 참고: `map`은 새로운 단축키를 설정하는 명령입니다.

키              | 설명
--------------- | :----------------------------------------------
`:nmap <F2> :w<CR>` | `NORMAL`모드에서 `<F2>`를 누르면 `:w`명령을 입력하고 `<Enter>`키를 입력한다.
`:nmap <C-j> i<CR><ESC>` | `NORMAL`모드에서 `<NL>`, 즉 `<C-j>`를 입력하면 현재 커서 오른쪽의 모든 문자열을 다음 라인으로 내려준다.
`:nmap <NL> i<CR><ESC>` | `<C-j>`와 `<NL>`이 같으므로 위와 똑같다.
`:imap email johngrib82@gmail.com<Esc>` | `INSERT`모드에서 `email`을 타이핑하면 `johngrib82@gmail.com`을 입력하고 `<Esc>`를 입력하여 `NORMAL`모드로 돌아간다.
`:imap email johngrib82@gmail.com<C-]>` | 위와 똑같다.

