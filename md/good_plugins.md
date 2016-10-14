# 추천 플러그인 모음

* [NerdTree](#nerdtree)
* [ctrlp](#ctrlp)
* [fzf](#fzf)
* [vim-airline](#vim-airline)
* [surround.vim](#surround.vim)

 repeat.vim
 matchit.vim
 snipmate.vim
 a.vim
 ragtag.vim (formerly allml.vim)

## NerdTree

* [Github](http://vimawesome.com/plugin/nerdtree-red) / [VimAwesome](http://vimawesome.com/plugin/nerdtree-red)
* 화면 옆쪽에 file explorer 를 만들어 줍니다.
* 다소 투박한 모양새가 마음에 들지 않는다면 [VimR](http://vimr.org/)을 사용하는 쪽을 추천합니다.
    * VimR은 키보드 커맨드로 작동할 수 있는 유려한 file explorer 를 내장하고 있습니다.
* ctrlp 나 fzf 가 있으면 잘 안 쓰게 된다는 단점이 있습니다.

## ctrlp

* [Github](https://github.com/kien/ctrlp.vim) / [VimAwesome](http://vimawesome.com/plugin/ctrlp-vim-everything-has-changed)
* 하위 디렉토리의 파일명을 fuzzy 검색해 줍니다.
* 파일 경로/이름을 일부만 입력해도 찾아주기 때문에 매우 편리합니다.
* VIM을 IDE 같이 사용하고 싶다면 필수 플러그인이라 할 수 있습니다.
* 도움말은 `:help 'ctrlp'`로 볼 수 있습니다.

![ctrlp](http://i.imgur.com/aOcwHwt.png)

## fzf

* [Github](https://github.com/junegunn/fzf.vim) / [VimAwesome](http://vimawesome.com/plugin/fzf)
* ctrlp 를 대체할 수 있는 강력한 fuzzy 검색 플러그인입니다. 장점은 엄청난 속도. 무시무시하게 빠릅니다.
* VIM 을 넘어서, 터미널에서도 수시로 사용하게 되는 유용한 프로그램이기도 합니다.

![fzf](https://camo.githubusercontent.com/0b07def9e05309281212369b118fcf9b9fc7948e/68747470733a2f2f7261772e6769746875622e636f6d2f6a756e6567756e6e2f692f6d61737465722f667a662e676966)

* 본래 터미널 전용 프로그램이다보니 MacVim 같은 gui vim 에서 사용하려면 gui VIM 에서 터미널을 호출할 수 있도록 설정해 주어야 합니다.
* 터미널 VIM을 많이 쓴다면 fzf, gui VIM 을 많이 쓴다면 ctrlp 를 사용하는 쪽을 추천합니다.

## vim-airline

* [Github](https://github.com/vim-airline/vim-airline) / [VimAwesome](http://vimawesome.com/plugin/vim-airline)
* vim 화면을 다음과 같이 예쁘게 꾸며줍니다.

![airline](https://github.com/vim-airline/vim-airline/wiki/screenshots/demo.gif)

* 도움말은 `:help airline`으로 볼 수 있습니다.
* airline 을 설치하고 버퍼 목록 보기 옵션을 주면 버퍼간 이동이 좀 더 편리해집니다. 다음 설정을 추천합니다.

```viml
    let g:airline#extensions#tabline#enabled = 1              " vim-airline 버퍼 목록 켜기
    let g:airline#extensions#tabline#fnamemod = ':t'          " vim-airline 버퍼 목록 파일명만 출력
    let g:airline#extensions#tabline#buffer_nr_show = 1       " buffer number 를 보여준다
    let g:airline#extensions#tabline#buffer_nr_format = '%s:' " buffer number format 을 설정할 수 있습니다
```

* 폰트/터미널에 따라 하단의 화살표 등이 조금씩 어긋나 보이는 문제가 발생한다면, 다음 링크를 참고하세요.
    * [airline 픽셀 문제 해결](fixlog.md#픽셀-문제)

## surround.vim

* [Github](https://github.com/tpope/vim-surround) / [VimAwesome](http://vimawesome.com/plugin/surround-vim)
* surround.vim 은 문자열을 감싸는 괄호, 인용부호, html tag 등을 편하게 수정할 수 있게 도와줍니다.
* 명령어는 `cs`, `ds`, `ysiw` 가 있습니다.
* html/xml 태그의 경우 `cst`, `dst` 로 수정과 삭제를 할 수 있습니다.
* 도움말은 `:help surround`로 볼 수 있습니다.

다음은 사용 예입니다.

* `"Hello world!"` 에 `cs"'`를 입력하면 `'Hello world!`로 변경됩니다.

* `'Hello world!'` 에 `cs'<q>`를 입력하면 `<q>Hello world!</q>`로 변경됩니다.

* `<q>Hello world!</q>` 에 `cst"` 를 입력하면 다시 `"Hello world!"`로 변경됩니다.

* `"Hello world!"` 안쪽에 커서를 놓고 `ds"` 를 입력하면 `Hello world!` 로 변경됩니다.

* `Hello world!` 에서 Hello 위에 커서를 놓고 `ysiw]` 를 입력하면 `[Hello] world!` 로 변경됩니다.

* `[Hello] world!` 에서 Hello 위에 커서를 놓고 `cs]{` 하면 `{ Hello } world!` 로 `{`,`}` 와 스페이스가 추가됩니다.

* 라인 전체에 괄호를 적용하려면 `yss)` 하면 됩니다. 그 결과로 `({ Hello } world!)` 가 됩니다.

* visual 모드에서도 사용 가능합니다. `Hello world!` 를 선택한 다음 `S<p>`를 입력하면 `<p>Hello world!</p>`가 됩니다.

* 삭제는 `ds`로 합니다. `"Hello world!"` 에서 `ds"` 하면 `Hello world!` 가 됩니다.

* 태그 삭제는 `dst`로 합니다. `<p>Hello world!</p>` 에서 `dst` 하면 `Hello world!` 가 됩니다.

