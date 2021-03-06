# Vim

Date: 2014-09-30 15:10
Tags: []
Categories: []

---

## Commands

### Helps

- 特殊文字について :

        :h keycodes

- 正規表現 :

        :h atom
        :h regexp

    - 最短一致

            {-}
            \s{-}

- 改行含む文字クラス :

        :h \_

- デフォルトで割り当てられているキーマップ :

        :h index

- EXコマンドヘルプ :

        :h :index

- Exコマンド用の特別な文字

        :h cmdline-special

- 式の文法

        :h expression-syntax

- 同名のオプション/コマンド/関数の切り分け方
    - オプション

        :h 'foldopen'

    - コマンド

        :h :foldopen

    - 関数

        :h soundfold()

### Useful

#### Normal mode

- 代替ファイルと切り替える :

        <C-^>

- 折りたたみ
    - カーソルの下の折りたたみを開く :

            zo

    - カーソルの下の折りたたみを閉じる :

            zc

    - カーソルの下の全ての折りたたみを開く :

            zO

    - カーソルの下の全ての折りたたみを閉じる :

            zC

    - 全ての折りたたみを開く :

            zR

    - 全ての折りたたみを閉じる :

            zM

- 変更リスト中の[count] 個前の位置に移動します

        g;

- 変更リスト中の[count] 個後の位置に移動します

        g,

- キーマップ確認
    - `:map`     : " すべて確認
    - `:imap`    : " インサートモードだけ
    - `:nmap`    : " ノーマルモードだけ
    - `:vmap`    : " ヴィジュアルモードだけ
    - `:verbose` : nmap " 定義元ファイル情報も表示

- ウィンドウを分割し、カーソル位置のファイル名のファイルを編集する。

        <C-w>f

##### Diff - 差分モード

- 差分モード開始:

        :diffs[plit]

- カレントウィンドウの差分モードを終了(#nはバッファ上の番号を指定):

        :diffo[ff] #n

- 現在のウィンドウを差分ウィンドウの1つにする。比較したいバッファに対し実行することで任意のバッファ間のdiffをとれる

        :difft[his]

- 差分情報を更新

        :dif[fupdate][!]

- 次の差分へ移動:

        ]c

- 前の差分へ移動:

        [c

- 相手バッファの内容を取り込む(obtain):

        do

- 自バッファの内容をput:

        dp

##### Spell - スペルチェック

- 正しい単語として辞書登録 :

        zg

- 誤った単語として辞書登録(すでに辞書にあった場合コメントアウトされる) :

        zw

- 間違ったたん度に対しての提案を調べる :

        z=

#### Others (technique)

- 改行コードを入力 :

        <C-v><C-m>

- 文字コード指定して開く :

        :e ++enc=utf8

- ヘルプファイル作成 :

        :helptags %:h (ヘルプファイルがあるディレクトリに移動して)

- 否定先読み

        /\vhoge(fuga)@!
        \* 注意!以下はやりたいことができない。(:help @!参照)
        /\vfoo.*(bar)@!
        ↓はよく使う
        /\v^\%(.*BAR)@!.*\zsFOO

    - バッファ内、 PATTERN にマッチしない行を REPLACEMENT で置き換える

            :%s/\(PATTERN\)\@!.*/REPLACEMENT/

    - 実用的な例: "bar" を含んでいない行から "foo" を探す: >

            /^\%(.*bar\)\@!.*\zsfoo

- 否定後読み - "foobar" 以外の "bar"

        /\v(foo)@<!bar

- シェル実行結果を読み込む

        :read! ls | grep hoge

- カラムを指定してソート

        :'<,'>sort /.*\%2v/

    - 外部コマンドでソート

            :'<,'>!sort -k 2
            :'<,'>!sort -k 2 -k 3

- バージョンで判定

        if v:version > 700

- 特定のパッチで判定

        if has("patch-7.4.399")

- 行末尾の空白(スペース)削除

        %s/ *$//

- 空行削除

        :v/\S/d

### Rare

- カレントファイルの名前を出力 :

        :echo expand("%") :

- カレントファイルのフルパスを出力 :

        :echo expand("%:p")

- ヘッド(ディレクトリ)

        :echo expand("%:h")

- テイル(ファイル名だけ)

        :echo expand("%:t")

- カレントファイルの名前、拡張子抜きを出力 :

        :echo expand("%:r")

- カレントファイルの拡張子を出力 :

        :echo expand("%:e")

- ファイルを暗号化する

        :X

- 次に検索パターンにマッチするもの表すテキストオブジェクト

        gn
        gN

    - マッチするものをヤンク

            ygn
            ygN

- 外部コマンドへバッファの内容を渡す

        :write !{cmd}
        :help :write_c

### サブモード補完(CTRL-X補完)

- ファイル名補完:

        <C-x><C-f>

- ユーザ定義補完(e.g. プラグインの補完):

        <C-x><C-u>

## Startup option

- vimrc やプラグインを無効にする

        vim -u NONE
        vim -u NORC
        vim --noplugin

- 詳細表示する

        vim -V

- 起動時間を出力する

        vim --startuptime result.log

    - すぐ終了する

            vim --startuptime result.log -c :q

    - 結果を加工する

            vim --startuptime /dev/stderr -c q 2> >(tail -1)

- 差分モード(vimdiff)

        vim -d foo.txt bar.txt
        # 以下と同様
        vimdiff foo.txt bar.txt

Refs:

    :help starting

## Options

- 最後に設定された箇所も表示

        verbose set expandtab?
        " これは特定のオプション名が指定されたときのみ機能する。 :h set-verbose

- 改行コード

        set fileformats?

- BOM

        set bomb

## Plug-ins

.vimrc参照。

### Alignta

- 単純にパターンの開始位置だけを揃える整列方式

        :Alignta <- hoge

- 空白区切りの要素を整列

        :'<,'>Alignta <<0 \s\S

- 適用回数を指定

        :'<,'>Alignta v/^" <<0 \s\S/2

- 適用範囲をフィルタ

        :'<,'>Alignta v/^" <<0 \s\S

### Emmet for Vim

- リンクタイトル取得

        <C-y>a

- コメントアウトトグル

        <C-y>/

### Neosnippet

`neosnippet-snippets`でよく使うもの

- `df`, `datetime_iso8601` : 2016-10-26T12:41:24
- `dd`, `date_iso8601`     : 2016-10-26
- `dt`, `time_colon`       : 12:40:58
- `fname`, `filename`      : vim.md
- `bname`, `basename`      : vim
- `path`                   : /d/admin/.ghq/github.com/assout/memolist.wiki/vim.md

### Unite

#### Key-mapping

##### Normal mode

- リフレッシュ

        <C-l>

- 一単語削除(Backspace)(階層を浅くする)

        <C-h>

- 候補選択時、narrow する(階層を深くする)

        e

- 挿入モードに入る

        i

- 挿入モードで先頭にカーソル移動

        I

### Vimfiler

- ソート

        S

### easytags.vim

- 編集中のファイルのtagsを作成

        :UpdateTags

- ディレクトリを再帰的に探索しtagsを作成

        :UpdateTags -R .

### quickrun

- 実行時にコマンドオプション指定

        :QuickRun -cmdopt "-hoge fuga"

## Vim script

### Key-mapping - キーマッピング

<http://vimblog.hatenablog.com/entry/vimrc_key_mapping>

| モード                                 | 再割当有り | 再割当無し |
|----------------------------------------|------------|------------|
| ノーマルモード＋ビジュアルモード       | `noremap`  | `map`      |
| コマンドラインモード＋インサートモード | `noremap!` | `map!`     |
| ノーマルモード                         | `nnoremap` | `nmap`     |
| ビジュアル(選択)モード                 | `vnoremap` | `vmap`     |
| コマンドラインモード                   | `cnoremap` | `cmap`     |
| インサート(挿入)モード                 | `inoremap` | `imap`     |

## Others - その他

- Windowsの右クリックメニューに"Edit in GVim", "Read in GVim"を追加 :

        [HKEY_CLASSES_ROOT] - [*] - [shell]

    Refs: [なんでもかんでも Vim で開く (コンテキストメニューの設定) - 腹八分目。](http://d.hatena.ne.jp/masaking/20070803/1186105654)

- モードライン modeline:

        vim:tw=78:norl:
        <!-- vim:set filetype=markdown: -->
        " vim:filetype=sh:

- :ls結果の記号の見方 TODO: ちゃんと書く
    - `a` : alternate
    - `%` : カレントバッファ?
- Ctrlを使うキーバインドまとめ
    Refs: [Vim で使える Ctrl を使うキーバインドまとめ - 反省はしても後悔はしない](http://cohama.hateblo.jp/entry/20121023/1351003586)
- vimファイルのコメントでの`Hoge:`表記はハイライトグループVimCommentTitleが適用され強調表示される。
