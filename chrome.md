# Chrome

Date: 2014-11-13 11:54
Tags: []
Categories: []

---

## Extensions

### List

- `AutoPagerize`
- `Defenestrate`
- `Disable Extensions Temporarily`
- `Fire Shot` : 1ページ内スクロールしてきゃぷれる。1回毎に保存先聞かれるけど他にいいのも無さそうなので。
- `Github Toc`
- `IE Tab` : 印刷プレビューを見るためにも使用
- `Instant Translate`
- `JSONView`
- `LastPass`
- `LivePage`
- `Markdown Linker` : markdownでの[title]<url>形式を作成してくれる。
- `Moqups`
- `Octotree`
- `PlantUML Viewer`
- `Postman`
- `Save to Pocket`
- `Scrum for Trello`
- `Session Buddy`
- `Stylish`
- `Web Cliper for Trello`
- `Wiki Search for GitHub`
- `ZenHub` : 試験運用中
- `ato-ichinen`
- `cVim(chromium-vim)`
- `firenavi-addon`
- `japanese-search`
- `jsshell`
- `textlint`
- `μBlock Origin`
- `カラフル英語品詞分類`

### Display order

1. `Save to Pocket`
1. `Web Cliper for Trello`
1. `Session Buddy`
1. `Instant Translate`
1. `IE Tab`
1. `LivePage`
1. `ato-ichinen`
1. `japanese-search`
1. `PlantUML Viewer`
1. `Octotree`
1. `μBlock Origin`
1. `Defenestrate`
1. `AutoPagerize`
1. `cVim(chromium-vim)`
1. `JSONView`
1. `Markdown Linker`
1. `Wiki Search for GitHub`
1. `Github Toc`
1. `Stylish`
1. `カラフル英語品詞分類`
1. `LastPass`
1. `Scrum for Trello`
1. `Disable Extensions Temporarily`

### Unused

- `Disconnect` : @office での基本認証ダイアログ問題対策。-> ソーシャルウィジェットが原因ぽかったので入れたら一切でなくなったので最高っぽい。
    - TODO: 外しても出なくなったっぽい？
- `Google Translate`
    - 翻訳のポップアップ : すぐにポップアップを表示する。
- `IE Tab Multi (Enhance)` : 最新のchromeでは使えないためIE Tabに以降
- `Weblioポップアップ英和辞典` : Chromeのtask manager見ると常に通信が発生してそう。。。 : 重い
    - ポップアップのON/OFF : Shift+Eで表示.
- `Vichrome` : cVim に乗り換え
    - General
        - Disable auto focus when page is opend : checked
        - Use Migemo Search : checked
        - Wrap Scan : unchecked
    - Appearance
        - Use f-Mode Animation : unchecked
    - Key Mapping
        - setup from GitHub managed dotfiles.
- `Shortcut Manager` : Vichrome でのマッピングキーを無効にするため(誤爆防止) : Vichrome 使わなくなったので不要
    - Ctrl + F : 1ページ下へ
    - Ctrl + H : 左のタブを選択する
    - Ctrl + J : JavaScript:document.forms[0].submit()
    - Ctrl + K : disable
    - Ctrl + L : 右のタブを選択する
    - Ctrl + Shit + H : 左のタブを閉じる
    - Ctrl + Shit + L : 右のタブを閉じる
    - Ctrl + Shit + O : 他のタブを閉じる
- `Screencastify` : 画面キャプチャ(一部無料) : gif化が有料っぽいので

### Details

#### cVim(chromium-vim)

Keys

- Normal Mode - Miscellaneous
    - copy the URL of the current page to the clipboard

            yy

    - open the clipboard selection in a new tab

            P

- Visual/Caret Mode
    - copys the current selection

            y

    - open highlighted text in new tab

            P

- Sync : [cvim settings · GitHub](https://gist.github.com/assout/e4172ddf70f52f05abe2)
- chrome://extensions/ : Keyboard shortcuts
    - Let Chrome use <C-w> for the deleteBackWord insert mapping      : `Ctrl + W`
    - Let Chrome use <C-n> for cncpcompletion setting (see Help file) : `Ctrl + N`
    - Go to the next tab                                              : `Alt + L`
    - Go to the preview tab                                           : `Alt + H`

#### Fire Shot

- Hot key - ページ全体をキャプチャ - Ctrl + Alt + P と 保存
- Options - Capturing - Default file name - Specify template :

        %y%m%d_%H%M%S_FireShot_%t

#### Instant Translate

- Settings
    - `;`         : Automatic detection -> Japanese
    - `Shift + ;` : Japanese -> English
- Caution: TODO: chromeの認証ダイアログが閉じられちゃう？ @office

#### Octotree

- Settings
    - GitHub
        - Site access token: {GitHub Personal Access Token}
    - GitLab
        - GitLab Enterprise URLs: {Local GitLab URL}
        - Remember sidebar visibility : unchecked

#### PlantUML Viewer

- SVGにする(PNGよりちょっと早い気がする)
- (遅かったら)localにplantuml-server立ててseverに指定する -> ちょっと早くなった気がする。
    - Refs: <https://github.com/plantuml/plantuml-server>
    - Server: <http://localhost:8080/plantuml> (default: <http://plantuml.com/plantuml>)

Caution: 外に出したくないファイルはローカルにサーバ立てること!

## Apps

### List

- Postman
- Simple Docker UI

## Configuration

### Settings - 設定

- Web Contents - ウェブ コンテンツ
    - Customize fonts... - フォントをカスタマイズ
        - Font : メイリオ
        - Encode - エンコード : Unicode (UTF-8)
- Languages - 言語 : English(US)
- System - システム
    - Google Chrome を閉じた際に... : Unchecked (TODO: もしかしたらしなくてもパフォーマンス改善されてるかも)

### Tool bar

- Show apps shortcuts : unchecked.
