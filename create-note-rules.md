# Create note rules

Date: 2014-11-25 16:42
Tags: []
Categories: []

---

## About this

ノート、メモの作成ルール。
対象は以下3種類。

- Work note : 作業ノート
- Study note : 学習ノート
- PC memo : pcでの作業メモ

## Rules

### Common

- 紙と電子で記号の意味とか分けない(統一する)。
- 句読点はつける。箇条書きの場合でもつけるが、簡単な名詞句のみの場合つけなくても良い。
- 色は三色
    - 黒 : 本文
    - 赤 : 強調
    - 青 : 注釈、雑学、質問事項?
- 記号の意味
    - ☆ : 重要
    - ◎ : 宿題事項、タスク
    - ＠ : ＠場所 を表す

- 記号は日本語文の中なら全角、英語文の中なら半角。(数字は必ず半角) -> 必ず半角のほうがよいかも。(根拠探す -> Redpen, textlintあたり)
- 英単語と和語の単語区切りはスペースを入れない。(correct -> Jonh Doeは言った。 incorrect -> Jonh Doe は言った。) -> TODO: space入れた方が良い？ (根拠探す -> Redpen, textlintあたり)
- 人名の書き方
    - 紙 : ○内にカタカナ1 or 2文字
    - 電子 : ()内に名前。(メモでは先頭2文字をアルファベットで。e.g. (hiro), (taha)
- 訂正は一重取消し線
- 絵を多用すること(図解)
- 原則 markdown で書く
    - 用語集は定義リストとして書く
    - 定義リストは、以下のフォーマットとする(TODO: 微妙かも。主要パーサーの実装に合わせたい)
            Hoge
            : hogehoge
            : hogehoge
            Fuga
            : fugafuga
            : fugafuga
- 議事録は基本箇条書き。(回答は以下の書き方とする。)
        - 夕飯は何にするか？
            - -> 林檎！
- 日付形式。以下どれか。変える
    - 曜日あり: Fri, Jan. 26, 2015
    - 曜日なし: Jan. 26, 2015
    \* めんどくさいとき
    - 曜日あり: 2015/1/26 Fri.
    - 曜日なし: 2015/1/26
- よく使う英語
    - TODO
    - Caution:
    - Refs:

### Work note

- ノートの構成は、「メインペイン」と「サブペイン」とする
- サブペインはノートの右端にする。-> コーネルメソッドとは合わないが。
- サブペインは「メモ欄」or「タイムトラック欄」 -> どっちにするか保留中
- メモは無理して漢字つかわない。ひらがなのほうが早い

Refs: [stationery](stationery)

### Study note

Refs: [stationery](stationery)

### PC memo

- 原則 vim - memolist でとる。
- 見出しは大文字始まり

## References

[document-format-rules](document-format-rules)

