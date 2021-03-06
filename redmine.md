# Redmine

Date: 2014-09-09 13:44
Tags: []
Categories: []

---

## Update rules - 更新方針

### General - 全般的な方針

基本細かい単位で中間結果も注記に更新していく。

- 作業開始時 : 作業の方向性、予定作業項目、成果物イメージを記載
- 作業の区切り : 作業項目の中間結果(作業経過がわかるように)
- 作業終了時 : 最終結論を整理して記載

### ％ done - 進捗率

基本0,50,100％くらいしか使わない。
-> そもそも2,3時間で終わる粒度でチケットを切るためそこまで細かく進捗率を入れない。

細かく管理する場合(検討作業の例)(@Deprecated rule)

1. 作業の目的方向性を合意  : 10%
1. 第一版作成完了          : 25%
1. 第一版レビュー/指摘反映 : 50%
1. 最終版作成完了          : 75%
1. 最終版レビュー/指摘反映 : 100%

### About Notes - 注記の更新方針

以下の見出し構成で都度更新していく。

- 作業目的、進め方
    - 目的
    - 進め方
    - 作業項目
- 作業状況
    - 作業項目foo
    - 作業項目bar
    - …
- 結論
    - 結論
    - 残課題とか

## Custom query - カスタムクエリ

TODO: 整理

以下の軸でカスタムクエリ作る

- Filters
    - Tracker
    - Version※あれば
    - Status
- Options
    - Columns
        - Parent task ※表示しないと階層関係がみえないため
    - Group results by: Assignee \*ただし階層関係が見えなくなるためFilter条件によっては未指定

Examples

- All - New
- All - In Progress
- All - Resolved
- Feature - New
- Feature - In Progress
- Feature - Resolved
- Bugs - New
- Bugs - In Progress
- Bugs - Resolved

## Settings - 設定

- Administration - Settings
    - General
        - Application title : Any!
        - Text formatting: Markdown
        - Cache formatted text : Checked
    - Display
        - Users display format : 山田 太郎
        - Use Gravatar user icons : Checked
        - Default Gravatar image : Monster ids
    - API
        - Enable REST web service: Checked
    - Projects
        - Default enabled modules for new projects
            - Documents,Files: Unchecked
    - Email notifications
        - Emission email address: "Jonh do" <mail address>
        - Select actions for which email notifications should be sent.
            - Issue added
            - Issue updated
                - Status updated
            - News added
            - Message added
            - Wiki page added
            - Wiki page updated

## Wiki

### マクロ

チャイルドページ一覧を表示: `{{child_pages}}`

