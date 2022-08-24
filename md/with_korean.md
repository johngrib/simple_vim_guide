# 한국어 키보드로 VIM 사용하기

처음 한국어 키보드로 VIM을 사용하다보면 다음과 같은 문제들을 마주하게 됩니다.

1. `<Esc>`를 입력하여 NORMAL 모드로 돌아오고 `j`를 눌러 아랫줄로 이동하려 하는데 `ㅓ`가 입력되어 커서가 움직이지 않는 문제.
1. 한글로 타이핑하고 파일을 저장하기 위해 `<Esc>:w`를 입력하였으나, 실제로는 `<Esc>:ㅈ`가 입력되어 저장되지 않는 문제.

이 문제들은 모드를 전환할 때마다 직접 영문으로 전환해주면 해결됩니다.
그러나 몹시 불편합니다.
`<Esc>`를 누를 때마다 현재 한글 모드인지 영문 모드인지를 생각하면서 `한/영`전환 키를 일일이 눌러주는 일만은 피하고 싶습니다.

## 방법 : 입력기 변경
맥이라면 [구름 입력기](http://gureum.io/)를 사용하는 방법이 있습니다. 구름 입력기에는 `<Esc>`를 누를 때마다 영문으로 전환해주는 옵션이 있습니다.

* 제가 쓰고 있는 방법입니다. 가장 추천하는 방법이며, 맥이라면 가장 심플한 방법이라 생각합니다.
* 리눅스에도 해당 기능을 지원하는 한글 입력기가 있을 것으로 봅니다.

## 방법 : `noimd`를 설정
다음과 같이 `.vimrc`에 설정해 줍니다.

```viml
set noimd
```

* 한글 입력을 하다 NORMAL 모드로 돌아갔을 때 아무런 문제 없이 NORMAL 모드의 명령어들을 사용할 수 있습니다.
* `:`명령줄로 가보면 아직 한영전환 키를 입력하지 않았는데도 영문이 기본으로 입력됩니다.
* 다시 INSERT 모드로 돌아와보면 한글이 그대로 나옵니다. 영문을 사용하려면 한영전환 키를 입력해야 합니다.
* 단점 : MacVim 에서는 잘 되지만, 터미널 VIM 에서는 안 됩니다.

## 방법 : `langmap` 설정 사용
다음과 같이 설정하면 NORMAL 모드에서 한글을 입력해도 작동합니다.

```viml
set langmap=ㅁa,ㅠb,ㅊc,ㅇd,ㄷe,ㄹf,ㅎg,ㅗh,ㅑi,ㅓj,ㅏk,ㅣl,ㅡm,ㅜn,ㅐo,ㅔp,ㅂq,ㄱr,ㄴs,ㅅt,ㅕu,ㅍv,ㅈw,ㅌx,ㅛy,ㅋz
```

* `ㅁ`을 `a`로, `ㅠ`를 `b`로 인식하게 하는 기능입니다. 본래는 그리스어 키보드 같은 좀 특별한 키보드를 위한 기능이라 할 수 있습니다.
* 문제점 : 한글이 조합형 글자이다 보니 한글 자음 다음에 한글 모음을 입력할 때 키를 한 번 더 눌러야 명령어가 인식됩니다.


## 방법 : input-source-switcher 설치
[input-source-switcher](https://github.com/vovkasm/input-source-switcher)를 설치해서 쓰는 방법이 있습니다.

* 자세한 내용은 [이상욱님의 블로그](https://sangwook.github.io/2015/01/01/vim-insert-mode-keyboard-switch.html)를 참고하시면 됩니다.

## 방법 : Karabiner
맥이라면 [Karabiner](https://pqrs.org/osx/karabiner/) 의 프리셋을 사용할 수도 있고, Karabiner의 설정 파일인 `private.xml`에서 다음과 같이 설정해 주는 방법도 있습니다.

```xml
<vkchangeinputsourcedef>
    <name>KeyCode::VK_CHANGE_INPUTSOURCE_TO_ENGLISH</name>
    <inputsourceid_equal>com.apple.keylayout.ABC</inputsourceid_equal>
</vkchangeinputsourcedef>
<item>
    <identifier>esc_abc_escape</identifier>
    <name>영문으로 inputsource 전환 후, ESC 입력</name>
    <autogen>
        __KeyOverlaidModifier__
        KeyCode::ESCAPE,
        KeyCode::VK_MODIFIER_EXTRA1,
        KeyCode::VK_CHANGE_INPUTSOURCE_TO_ENGLISH,
        KeyCode::ESCAPE,
    </autogen>
</item>
```
위와 같이 설정해주면 `<Esc>`키를 누를 때마다 영문 전환이 됩니다.

* 치명적인 문제 : OSX에서는 잘 돌아가지만, OSX의 다음 버전인 macOS에서는 입력 관련 변경 사항이 있어서 Karabiner가 제대로 동작하지 않습니다.
macOS를 위한 Karabiner-Elements가 현재 개발중이긴 한데, 아직까지는 단순 키 맵핑만 가능해서 원하는 기능을 위해 사용하기에는 부족한 점이 많습니다.

업데이트된 Karabiner-Elements에서 위 룰을 Complex Modifications를 사용하여 json 파일로 추가가 가능합니다.
`~/.config/karabiner/assets/complex_modifications/` 에 새로운 json 파일을 추가하고 (ex. `escape_to_en.json`) 다음 내용을 추가해줍니다.

```
{
  "title": "Convert to en when ESC",
  "rules": [
    {
      "description":"Convert to en when ESC",
      "manipulators": [
        {
          "type": "basic",
          "from": {
            "key_code": "escape",
            "modifiers": {
              "optional": [
                "any"
              ]
            }
          },
          "to": [
            {
              "key_code": "escape"
            }
          ],
          "to_after_key_up": [
            {
              "select_input_source": {
                "language": "en"
              }
            },
            {
              "key_code": "escape"
            }
          ],
          "conditions": [ 
            { 
              "type": "frontmost_application_if",
              "bundle_identifiers": [
                "^com\\.apple\\.Terminal$",
                "^com\\.googlecode\\.iterm2$",
                "^co\\.zeit\\.hyperterm$",
                "^co\\.zeit\\.hyper$",
                "^io\\.alacritty$",
                "^net\\.kovidgoyal\\.kitty$" 
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

이후 Karabiner-Elements 환결설정 -> Complex Modifications -> Add rule 에서 해당 rule을 Enable 해줍니다.
이후 conditions에 추가된 터미널 앱들 안에서 `<Esc>`를 입력할 때마다 영문으로 전환됩니다.

## 방법 : AutoHotkey
Windows 라면 AutoHotkey 를 쓰는 방법이 있습니다. 다음과 같은 코드를 Ahk로 실행하면 `<Esc>`를 입력할 때마다 영문으로 전환됩니다.
* 아래의 IME_CHECK 코드 출처는 다음과 같습니다.
* http://autohotkey.co.kr/b/1-357
* 특정 프로그램(ex: VSCode)에서만 실행을 원할 경우, IfWinActive 기능을 사용합니다.
```autohotkey
$Esc::
    if(IME_CHECK("A"))
        Send, {VK15}    ;영문이라면 한영전환 키를 입력해준다.
    Send, {Escape}
    return

/*
  IME check 
*/
IME_CHECK(WinTitle) {
  WinGet,hWnd,ID,%WinTitle%
  Return Send_ImeControl(ImmGetDefaultIMEWnd(hWnd),0x005,"")
}
Send_ImeControl(DefaultIMEWnd, wParam, lParam) {
  DetectSave := A_DetectHiddenWindows
  DetectHiddenWindows,ON
   SendMessage 0x283, wParam,lParam,,ahk_id %DefaultIMEWnd%
  if (DetectSave <> A_DetectHiddenWindows)
      DetectHiddenWindows,%DetectSave%
  return ErrorLevel
}
ImmGetDefaultIMEWnd(hWnd) {
  return DllCall("imm32\ImmGetDefaultIMEWnd", Uint,hWnd, Uint)
}
```

## 방법 : 최후의 수단
한글을 아예 사용하지 않고 영문으로만 컴퓨터를 사용하는 방법이 있습니다.

