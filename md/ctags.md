# ctags 로 함수가 선언된 곳으로 점프하기

ctags 를 이용하면 소스코드 편집중에 다른 소스 파일에 있는  함수 선언부로 바로 점프할 수 있습니다.

## 설치 방법
mac의 경우 ctags가 이미 설치되어 있으나 `-R` 옵션을 인식하지 못하는 경우 `brew` 를 통해 설치합니다.
```sh
$ brew install ctags
```

`-R` 옵션 인식 문제를 해결하기 위해, 설치가 완료되면 `.bashrc` 나 `.bash_profile`에 다음과 같은 alias를 추가합니다.
```sh
alias ctags="`brew --prefix`/bin/ctags"
```

## 사용 방법

* tags 파일 생성 : 프로젝트 루트 디렉토리로 가서 다음과 같이 명령합니다. 완료되면 tags 파일이 생성됩니다.
```sh
$ ctags -R
```
    * 제외하고 싶은 파일 타입이 있다면 다음과 같이 지정해줍니다.
```sh
$ ctags -R --exclude=.git --exclude=log *
```

* 이후 tags 파일이 있는 곳(프로젝트 루트)에서 VIM을 실행하면 ctags를 사용할 수 있게 됩니다.

* VIM 실행시 태그로 검색해 파일 open 하기
    * `$ vim -t 태그명`
* VIM 실행 후 태그로 검색해 파일 open 하기
    * `:ta 태그명` : 정확한 태그명을 입력해야 찾아줍니다.
    * `:ta /태그명` : 일부만 일치해도 찾아줍니다.
    * `:tj 태그명`, `:tj /태그명` : 태그 검색 결과가 많으면 리스트로 보여줍니다.
    * `:tn` : 다음 태그로 이동합니다.
    * `:tp` : 이전 태그로 이동합니다. `:tN`도 됩니다.
* 커서 위치에서 점프하기
    * 점프하고 싶은 함수 호출부에 커서를 놓고, `<C-]>`로 함수 선언부로 점프할 수 있습니다.
    * 본래 위치로 돌아오고 싶다면, `<C-t>`를 입력하면 됩니다.
* outline 보기
    * [taglist.vim](http://vim-taglist.sourceforge.net/)을 설치하면 outline 을 보며 이동할 수 있습니다.
    * `:Tlist` 를 입력하면 왼쪽에 outline을 보여주는 새로운 window가 나타납니다.
    * 함수명이나 필드명으로 커서를 옮긴 다면 `<Enter>`를 입력하면 해당 위치로 이동합니다.
* 현재 버퍼의 변경사항을 업데이트하기
    * taglist.vim의 `:TlistUpdate`를 사용하면 됩니다.


> 참고 : 프로젝트 루트에서 VIM을 실행했기 때문에 편집할 파일을 찾기 어렵다면 fzf.vim 이나 CtrlP.vim 으로 파일을 찾아 편집하면 됩니다.

## tags 자동 갱신 플러그인의 사용

* Vim에서 tags를 사용할 때 가장 짜증나는 점은 수동으로 일일이 tags 파일을 갱신해줘야 한다는 것입니다.
* 게다가 바뀐 파일 정보만 갱신하면 될 텐데 멍청한 `-R` 옵션은 매번 전체 파일을 갱신합니다.
* 따라서 Vim에서 tags를 제대로 편리하게 사용하려면 tags 파일을 자동으로 갱신해주는 도구를 설치할 필요가 있습니다.

* [vim-gutentags](https://github.com/ludovicchabant/vim-gutentags)를 사용하면 tags 파일을 자동으로 갱신할 수 있습니다.
* vim-gutentags는 git status를 참고하여 변경된 파일의 tags 정보만 갱신하기 때문에 빠르며, 백그라운드에서 갱신 작업이 돌아가기 때문에 편리합니다.

## 참고 자료
* https://gist.github.com/nazgob/1570678
* https://johngrib.github.io/wiki/ctags/