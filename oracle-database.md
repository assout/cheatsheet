# Oracle database

Date: 2014-11-27 10:42
Tags: []
Categories: []

---

## Reference

- 権限付与 :
    [ORACLE／権限編 - オラクルちょこっとリファレンス](http://luna.gonna.jp/oracle/ora_auth.html)
- SETシステム変数 :
    [SQL*Plusコマンド・リファレンス](http://otndnld.oracle.co.jp/document/products/oracle10g/102/doc_cd/server.102/B19277-01/ch12.html#39458)

## Useful commands

- 接続 :

        connect user/pass@host/sid

- ユーザ一覧参照 :

        select username from all_users;

- テーブル一覧参照 :

        select table_name from user_tables;

- sqlファイルの実行 :

        SQL> @/tmp/hoge.sql

- システム権限付与 :

        grant [システム権限名] to [ロール名];

- バッファリスト表示 :

        list [n]

- バッファ内SQLを実行 :

        run [n]

- バッファ内SQLを実行(表示せず) :

        /

- Backspace :

        Ctrl-Backspace

- インポート :

        imp user/pass@sid file=data.dmp

    - ユーザ指定 :

            imp user/pass@sid file=data.dmp fromuser=tanaka touser=sato

