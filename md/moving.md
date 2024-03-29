# 커서 이동 방법
* [방향키](#방향키)
* [상하좌우 이동](#상하좌우-이동)
    * [왼쪽으로 이동](#왼쪽으로-이동)
    * [오른쪽으로 이동](#오른쪽으로-이동)
    * [위로 이동](#위로-이동)
    * [아래로 이동](#아래로-이동)
* [특수 이동](#특수-이동)
* [이동 예제](#이동-예제)
* [검색 예제](#검색-예제)
* [JUMPS](#jumps)

* [참고 자료](#참고-자료)

------

* 참고 : `<C-키>`는 `CTRL`과 해당 키를 함께 누르는 것을 의미합니다.

## 방향키
* 방향키로는 NORMAL 모드에서 hjkl 을 사용합니다.

`h`     | `j`     | `k`     | `l`
------  | ------  | ------  | ------
&#8592; | &#8595; | &#8593; | &#8594;

## 상하좌우 이동
* 기본적인 이동은 NORMAL 모드에서 수행합니다.

### 왼쪽으로 이동

키        | 설명
--------- | :---------------------------------------------------------------------------
`0`       | 현재 라인의 가장 왼쪽으로 커서 이동. HOME 키와 같다.
`^`       | 현재 라인의 첫 번째 글자로 커서 이동. `0` 과 비슷하지만 인덴트(공백)를 무시하므로 더 유용하다.
`F문자`   | 왼쪽으로 문자를 검색하여 해당 문자 위로 커서 이동.
`T문자`   | 왼쪽으로 문자를 검색하여 해당 문자 뒤로 커서 이동.
`;`       | 다음 검색 결과로 이동.
`,`       | 이전 검색 결과로 이동.
`b`       | 커서 왼쪽 단어의 첫 글자로 이동.
`B`       | 커서 왼쪽 단어의 첫 글자로 이동. 단 특수문자도 단어의 일부로 친다.
`ge`      | 커서 왼쪽 단어의 마지막 글자로 이동.
`gE`      | 커서 왼쪽 단어의 마지막 글자로 이동. 단 특수문자도 단어의 일부로 친다.

### 오른쪽으로 이동

키        | 설명
--------- | :--------------------------------------------------------------------
`$`       | 현재 라인의 가장 마지막으로 커서 이동. END 키와 같다.
`f문자`   | 오른쪽으로 문자를 검색하여 해당 문자 위로 커서 이동.
`t문자`   | 오른쪽으로 문자를 검색하여 해당 문자 앞으로 커서 이동.
`;`       | 다음 검색 결과로 이동.
`,`       | 이전 검색 결과로 이동.
`W`       | 커서 오른쪽 단어의 첫 글자로 이동. 단 특수문자도 단어의 일부로 친다.
`w`       | 커서 오른쪽 단어의 첫 글자로 이동.
`E`       | 커서 오른쪽 단어의 마지막 글자로 이동. 단 특수문자도 단어의 일부로 친다.
`e`       | 커서 오른쪽 단어의 첫 글자로 이동.

### 위로 이동

키        | 설명
--------- | :----------------------------------------------
`gg`      | 첫 번째 라인으로 이동.
`<C-b>`   | 페이지 up.
`<C-u>`   | 반 페이지 up.
`H`       | 현재 화면에 보이는 첫 번째 라인으로 이동.
`{`       | 현재 커서가 위치한 문단의 시작 지점으로 이동.
`(`       | 현재 커서가 위치한 문장의 시작 지점으로 이동.
`M`       | 현재 화면의 중간 라인으로 이동.

### 아래로 이동

키        | 설명                                            |
--------- | :---------------------------------------------- |
`G`       | 마지막 라인으로 이동.                           |
`<C-f>`   | 페이지 down.                                    |
`<C-d>`   | 반 페이지 down.                                 |
`L`       | 현재 화면에 보이는 마지막 라인으로 이동.        |
`}`       | 현재 커서가 위치한 문단의 마지막 지점으로 이동. |
`)`       | 현재 커서가 위치한 문장의 마지막 지점으로 이동. |
`M`       | 현재 화면의 중간 라인으로 이동.                 |

## 특수 이동

키           | 설명
---------    | :----------------------------------------------
`숫자gg`     | 해당 라인 넘버로 이동.
`:숫자`      | 해당 라인 넘버로 이동.
`/정규식`    | 현재 파일 내 검색 후 커서를 옮겨준다.
`?정규식`    | 현재 파일 내 검색 후 커서를 옮겨준다.(역방향)
`*`          | 현재 커서가 있는 위치의 단어를 검색한다.
`#`          | 현재 커서가 있는 위치의 단어를 검색한다.(역방향)
`n`          | 다음 검색 결과로 커서 이동.
`N`          | 이전 검색 결과로 커서 이동.
`%`          | 현재 커서가 위치한 괄호(`(), {}, []` 등)의 짝으로 이동한다.
``` `문자``` | 일종의 북마크 기능. 자세한 내용은 [marks](mark.md) 문서를 참고.
``` '문자``` | 일종의 북마크 기능. 자세한 내용은 [marks](mark.md) 문서를 참고.
`<C-e>`      | 위로 스크롤.
`<C-y>`     | 아래로 스크롤.
`zz`         | 현재 커서가 있는 위치를 화면 중간으로 스크롤 한다.

## 이동 예제

키            | 설명
---------     | :----------------------------------------------
`10<C-f>`    | 페이지 down을 10 회 한다.
`100k`        | 100 줄 위로 간다.
`7l`          | 7칸 오른쪽으로 간다.
`{v}`         | 현재 문단 전체를 선택한다.
`{v}y`        | 현재 문단 전체를 복사한다.
`{v}d`        | 현재 문단 전체를 삭제한다.
`3w`          | 오른쪽으로 3 단어 이동한다.
`d3w`         | 오른쪽으로 3 단어를 삭제한다.
`2ft`         | 오른쪽의 두 번째 t 로 이동한다.
`d2ft`        | 오른쪽의 두 번째 t 까지 삭제한다.
`y2ft`        | 오른쪽의 두 번째 t 까지 복사한다.
`"ay2ft`      | 오른쪽의 두 번째 t 까지 a 레지스터로 복사한다.
`v2ft`        | 오른쪽의 두 번째 t 까지 선택한다.
`dt'`         | 현재 커서 위치부터 ' 앞까지 삭제한다.
`yt'`         | 현재 커서 위치부터 ' 앞까지 복사한다.
`vt'`         | 현재 커서 위치부터 ' 앞까지 선택한다.
`44gg`        | 44번 라인으로 이동한다.
`d44gg`       | 현재 커서 위치부터 44번 라인까지 삭제한다.
`%v%"by`      | 현재 커서가 있는 문장을 감싸는 괄호 내 전체를 선택하고 b 레지스터에 복사한다.

## 검색 예제

키           | 설명
---------    | :----------------------------------------------
`/asdf`      | 문자열 asdf 를 검색한다.
`/asdf/s`    | 문자열 asdf 를 검색하고, asdf 의 첫번째 문자 a 로 커서를 이동한다.(디폴트 값)
`/asdf/e`    | 문자열 asdf 를 검색하고, asdf 의 마지막 문자 f 로 커서를 이동한다.
`/asdf/e+2`  | 문자열 asdf 를 검색하고, asdf 의 마지막 문자 f 이후 2 번째 위치로 커서를 이동.
`2/asdf`     | 문자열 asdf 를 검색한 결과 두 번째 asdf 로 커서를 이동한다.
`2/asdf/e-3` | 문자열 asdf 를 검색한 결과 두 번째 asdf 의 마지막 문자 f 이전 3 번째 위치로 커서 이동.
`/asdf/+7`   | 문자열 asdf 를 검색하고, 검색 결과의 7 줄 아래로 커서 이동.
`/^\n\{3}`   | 빈 라인 3 줄을 찾는다.
`/^[a-t]`    | a 에서 t 사이의 알파벳으로 시작하는 라인을 찾는다.
`/aaa\_s*bbb` | aaa 와 bbb 사이에 여러 줄의 공백 라인이 있어도 찾는다.

* 참고: highlight 된 검색 결과는 `:noh` 또는 `:nohlsearch` 를 입력하면 highlight 를 끌 수 있습니다.

# JUMPS
* 위의 이동 명령들 중 단순 좌우이동이 아닌 것은 모두 `JUMP` 라고 부릅니다. 즉, 다음 명령들이 점프에 속합니다.
* `'`, `'`, ``` ` ```, `G`, `/`, `?`, `n`, `N`, `%`, `(`, `)`, `[[`, `]]`, `{`, `}`, `:s`, `:tag`, `L`, `M`, `H`
* 점프 히스토리를 보려면 `:ju` `:jumps` 를 입력합니다.

키        | 설명
--------- | :----------------------------------------------
`<C-o>`  | 점프 히스토리의 이전 점프로 이동한다.
`<C-i>`  | 점프 히스토리의 다음 점프로 이동한다.

# 참고 자료
* http://vimdoc.sourceforge.net/htmldoc/motion.html#jump-motions
