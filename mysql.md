# MySQL

Date: 2015-08-10 16:35
Tags: []
Categories: []

---

## Commands

- ログイン

        mysql -h 172.17.0.1 -u root -p mysql

- データベース一覧表示

        SHOW DATABASES

- データベース作成

        CREATE DATABASE db_name;

- テーブル一覧表示

        SHOW TABLES FROM データベース名

- テーブルの列の情報を表示

        SHOW COLUMNS FROM テーブル名

- バージョン確認

        mysql> select version();

- 文字コードを確認

        show variables like "char%";

        show create database test_db;

## Mycli

- ログイン

        mycli -h localhost -u root test_db

