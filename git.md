# Git

Date: 2015-02-02 22:13
Tags: []
Categories: []

---

## Basic usage

### add - ステージングする

- ファイルごとに対話的に選択する

        git add -i

    - 対象を範囲指定

            Update>> 1,2,4
            Update>> 1-4

- 部分的に追加する

        git add -p

    Refs: [Gitで部分的にコミットする方法 - Qiita](http://qiita.com/miyohide/items/79ab0ff3b3852289a6be)

- 変更のみ追加する(新規追加はしない)

        git add -u

    Refs: [git add -A と git add . と git add -u の違い - nekovaの日記](http://nekova.hatenablog.com/entry/2013/02/20/013909)

- 無視されるファイルを強制的にインデックスに追加する

        git add -f

### commit - コミットする

- 簡易コメントでコミット

        git commit -m "commit reason"
        git commit -m "commit reason" -m "seconds reason"

- 作業ツリーの変更をすべてコミットする

        git commit -a

- ファイルを指定してコミット

        git commit somefile

- コミット内容を訂正

        git commit -m "コメント" -a
        # 修正しステージング
        git commit --amend -a

- コミットコメントを修正(amend)

        git commit --amend -m "修正後コメント"

- 詳細(diff)を表示してコミット

        git commit -v

- 以前のコミットメッセージを利用する

        git commit -c HEAD
        git commit -c HEAD^

### diff - 差分を見る

見る対象

- 作業ツリーとステージングエリア間

        git diff

- ステージングエリアとリポジトリ間

        git diff --cached

- 作業ツリーとリポジトリ間

        git diff HEAD

- ローカルブランチとリモートブランチの間

        git diff origin (リモート設定名による？)

- バージョン間の差分を見る

        git diff <revision>
        git diff HEAD^

表示オプション

- ファイル名のみ

        git diff --name-only

- パス指定

        git diff *main*

### branch, checkout - ブランチを操作する

- ブランチを作成する

        git branch new-feature

- ブランチを切り替える

        git checkout new-feature

- ブランチを削除する

        git branch -d <branchname>

- 別の名前に変更する

        git branch -m master master_after

- ブランチ作成とチェックアウトを同時にする

        git checkout -b alternate master

    - 別のブランチで作業してしまい、途中でブランチ作成する場合

            git checkout -b working

        Refs: [ブランチを作り忘れた時 - Qiita](http://qiita.com/kkabetani/items/edc69a806095e4fc489c)

- リモートのブランチをcheckoutする

        git checkout -b new-feature origin/new-feature

- マージでコンフリクトした際にどちらかのブランチの内容を適用 (Git merge, conflict, checkout, --ours, --theirs)
    - マージ先を優先する場合:

            git checkout --ours hoge.txt

    - マージ元を優先する場合:

            git checkout --theirs hoge.txt

### merge - マージする

- マージには三種類ある
    - 直接マージ(定番)

            git checkout master
            git merge alternate

    - 圧縮コミット(squash)

            git checkout master
            git merge --squash alternate
            git commit -m "reson"

    - チェリーピック(つまみ食い)
            割愛
- 競合を解消する

        git merge alternate
        git mergetool
        git commit
        \* 簡単ならmergetool使わなくても良い
        \* commitメッセージは勝手に入れてくれる

- conflictするか確かめるだけ

        git merge ${branch} --no-commit
        # git merge origin/master --no-commit
        git merge --abort

### log - コミットログを見る

- 変更のあったファイル名を表示する

        git log --stat

- 一行で表示

        git log --oneline
        git log --pretty=oneline # ちょっと↑と表示は違う。

- 特定のコミッターのログを見る

        git log --committer=hoge

- 特定のリビジョンから始まるログを見る

        git log <revision>

- パッチ形式のコミットログを表示する

        git log -p

- 過去のコミットから対象文字列を含むコミットを検索

        git log -S hoge
        git log -Shoge

    - パッチ形式で表示

            git log -Shoge -p

- Git logでコミットメッセージを検索する方法(コミットログでフィルタリング)

        git log --grep hoge
        git log --grep hoge -p

- 特定のパス(ファイル、ディレクトリ)の履歴を見る

        git log -- ./foo ./bar
        git log -- .
        git log -- *.xml

### show - コミットログと変更点を確認

    git show HEAD

- 特定のリビジョンのファイルを見たい

        git show REVESION_HASH:FILE_PATH

### blame - 誰のコミットか確認する

- 行番号を指定

        git blame -L 12,13 somefile

### revert - コミットを取り消す(訂正をコミットする)

    git revert HEAD

- 複数取り消し、まとめてコミットする

        git revert -n HEAD
        git revert -n <rev>
        git revert -n <rev>
        git commit

### reset - 変更をリセットする

- 以前のコミットをすべてステージングエリアに戻す(i.e. 直前のコミットを取り消したい(コミットのみ取り消し)

        git reset --soft

- リポジトリおよび作業ツリーからコミットを消し去る(要注意)
    - 直前のコミットを取り消したい(マルっと消したい)

            git reset --hard HEAD^

    - コミット後の変更を全部消したい

            git reset --hard HEAD

- addを取り消したい

        git reset --mixed HEAD
        or
        git reset HEAD

- リセットを取り消したい

        git reset --hard ORIG_HEAD

    Refs: [\[git reset (--hard/--soft)\]ワーキングツリー、インデックス、HEADを使いこなす方法 - Qiita](http://qiita.com/shuntaro_tamura/items/db1aef9cf9d78db50ffe)

### rebase - 履歴を書き換える

- pick - コミットの順番を変える

        git rebase -i HEAD~3
        pick xx..
        pick yy..
        pick zz..
        -> change
        pick zz..
        pick xx..
        pick yy..
        保存して終了

- squash - コミットを圧縮

        git rebase -i HEAD~3
        pick xx..
        pick yy..
        pick zz..
        -> change
        pick xx..
        squash yy..
        pick zz..
        保存して終了(xxとyyが圧縮)

- edit - コミット内容を変更する

        git rebase -i HEAD^^
        // 対象をedit
        // 変更内容をadd
        git commit --amend
        git rebase --continue

    Refs: [Git ふたつ以上前のコミットにはcommit--amend できないの-Qiita](http://qiita.com/YumaInaura/items/4f00367fc1a140b61bc7)

- reword - コミットメッセージを変える

        git rebase -i HEAD~3
        reword xx..

- 元に戻す(rebase直後の場合のみ!)

        git reset --hard ORIG_HEAD

- 自動fix(--autofixup)を使う

        git commit --fixup=HEAD~1 # 既存コミットを指定する
        git rebase -i --autosquash HEAD~4

### stash - 作業を隠す

- 未追跡(untracked)ファイルも対象にする

        git stash -u

### clean - 追跡対象外ファイルの削除

#### clean - 追跡対象外ファイルの削除

- 確認

        git clean -n

- 削除

        git clean -f

- ディレクトリも対象

        git clean -d

## Remote

- remote - リモート操作する
    - リモートリポジトリ一覧を確認

            git remote
            git remote -v

- clone - クローンする

        git clone git@github.com:assout/dotfiles.git

    - ディレクトリを指定する

            git clone git@github.com:assout/dotfiles.git hoge

    - ブランチを指定する

            git clone -b foo_branch git@github.com:assout/dotfiles.git

- fetch - 取得する

        git fetch

    - すべてのリモートを取得

            git fetch --all

    - ブランチの削除情報も取得

            git fetch --prune

- push - 更新する

        git push

    - 強制

            git push -f

    - 強制(最後に fetch したタイミング以降に他人が push していたら失敗する)

            git push --force-with-lease

## Technique

- 初回push - Refs: [githubのレポジトリに初回pushするとき - MEMOcho-](http://jsapachehtml.hatenablog.com/entry/2014/03/14/205721)

        touch README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:username/hoge.git
        git push -u origin master

- git addを取り消す

        git reset HEAD foo.txt

- originの再登録方法

        git remote rm origin
        git remote add origin git@github.com:(githubのid)/(リポジトリ).git
        git push -u origin master

- GitのリモートリポジトリoriginのURLを変更する

        git remote set-url origin git@git.example.com:foo/bar.git

- remote設定
    - HTTPS

            https://github.com/USERNAME/OTHERREPOSITORY.git
    - SSH

            git@github.com:USERNAME/OTHERREPOSITORY.git

- ある特定のファイルを前のバージョンに戻す

        git checkout HEAD^ path/to/file.java

- 相対でリビジョンを指定する
    - ヘッドの1つ前のコミットを見る

            git show HEAD^

    - ヘッドの3つ前のコミットを見る

            git show HEAD~3
            git show HEAD^^^
            git show HEAD~~~

- リモートのGitブランチをローカルにチェックアウトする

        git branch -a
        git fetch
        git checkout -b other_branch origin/other_branch

- Gitの歴史に残っているユーザー名やメールアドレスを書き換える

        git filter-branch -f --commit-filter '
        GIT_AUTHOR_NAME="assout"
        GIT_AUTHOR_EMAIL="assout@users.noreply.github.com"
        GIT_COMMITTER_NAME="assout"
        GIT_COMMITTER_EMAIL="assout@users.noreply.github.com"
        git commit-tree "$@"
        ' HEAD
        git push -f

    Refs: [gitの歴史に残っているユーザー名やメールアドレスを書き換える deadwood](http://www.d-wood.com/blog/2013/10/22_4900.html)

- Forkしたリポジトリを本家リポジトリに追従、追跡する
    - 追従するFork元を追加

            git remote add upstream git://github.com/foo/bar.git

    - Fork元の変更を取得

            git fetch upstream

    - 自分のリポジトリに反映

            git merge upstream/master

- Conflict を解消する

        git mergetool

- Git diffで新規追加したファイルをdiff結果に含める

        git add -N foo.txt
        git diff HEAD

    Refs: [git diffで新規追加したファイルをdiff結果に含める RainbowDevilsLand](http://rainbowdevil.jp/?p=1247)

- Gitでリモート(remote)のブランチにローカルを強制一致させたい時

        git fetch origin
        git reset --hard origin/${branch}
        # masterブランチの場合
        # git reset --hard origin/master

    Refs: [gitでリモートのブランチにローカルを強制一致させたい時 - Qiita](http://qiita.com/ms2sato/items/72b48c1b1923beb1e186)

- detached HEAD状態から元に戻すコマンド

        git checkout master

    Refs: [detached HEAD状態から元に戻すコマンド (git, checkout, fix a detached HEAD, .git/HEAD, refs/heads/master) - いろいろ備忘録日記](http://devlights.hatenablog.com/entry/20130417/p1)

- 1ファイルだけ別のブランチから持ってくる

        git checkout <ブランチ名> -- <ファイル名>

    Refs: [Git 1ファイルだけ別のブランチから持ってくる - Qiita](http://qiita.com/oret/items/b646fcada9d89ed308c4)

- 派生元ブランチの変更

        git rebase --onto master(正しい派生元) develop(誤った派生元) topic(適用先ブランチ)

    Refs: [git rebase \-\-onto で派生元ブランチの変更 - northaven](http://yamayo.github.io/blog/2013/12/01/git-rebase-onto/)

- git の履歴とワークツリーの両方から削除

        git filter-branch -f --index-filter 'git rm --ignore-unmatch filename' HEAD

- git の履歴を削除してワークツリーには残す

        git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch filename' HEAD

## Configuration

- 日本語のファイル名を表示できるようにする

        git config --global core.quotepath false

## Git hook management

- Overcommit            : Star 1164: : [GitHub - brigade/overcommit: A fully configurable and extendable Git hook manager](https://github.com/brigade/overcommit/)
- pre-commit by Yelp    : Star 774 : だめ。pipでhomeにbin入るし : [pre-commit by Yelp](http://pre-commit.com/)
- pre-commit(jish)      : Star 607 : [GitHub - jish/pre-commit: A slightly improved pre-commit hook for git](https://github.com/jish/pre-commit)
    - -> これにする(シンプル)
- Git-hooks (Meyer)     : Star 661 : メンテされてないっぽい: [Meta Magic: Managing project, user, and global git hooks](http://benjamin-meyer.blogspot.jp/2010/06/managing-project-user-and-global-git.html)
- Git-hooks (git-hooks) : Star 121 : : [Git-hooks by git-hooks](http://git-hooks.github.io/git-hooks/)

## Github

### Search

- ファイル名(パス)を検索

        .travis.yml in:path

- 特定ファイル名(パス)を対象にファイル内検索

        filename:.travis.yml checkbashisms

Refs:. [Searching code - User Documentation](https://help.github.com/articles/searching-code/)

### Other

- メールアドレスを非公開にする
    - <https://github.com/settings/emails> - Keep my email address private : checked
- プロキシを超える
    - [各種コマンド類でプロキシサーバを越えるための設定 - iwasakimsの日記](http://d.hatena.ne.jp/iwasakims/touch/20120726/1343322297)
    - [Git - プロキシの指定方法 - Qiita](http://qiita.com/tunepolo/items/296c2639e0b750de41c6)
- Pull Request送信後に修正があった場合の作法について
    Refs: [Pull Request送信後に修正があった場合の作法について - QA@IT](http://qa.atmarkit.co.jp/q/2894)
- wikiからファイルへリンク

        [I'm a relative reference to a repository file](../blob/master/LICENSE)

    Refs: [Markdown Cheatsheet · adam-p/markdown-here Wiki · GitHub](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)

## GitLab

Refs: [docker#GitLab](docker#GitLab)

リポジトリ取得

    git clone ssh://git@localhost:10022/root/sandbox.git

### Special GitLab References

| input                | references                 |
|----------------------|----------------------------|
| @user_name           | specific user              |
| @group_name          | specific group             |
| @all                 | entire team                |
| #123                 | issue                      |
| !123                 | merge request              |
| $123                 | snippet                    |
| ~123                 | label by ID                |
| ~bug                 | one-word label by name     |
| ~"feature request"   | multi-word label by name   |
| 9ba12248             | specific commit            |
| 9ba12248...b19a04f5  | commit range comparison    |
| [README](doc/README) | repository file references |

Refs: [GitLab Documentation](http://doc.gitlab.com/ce/markdown/markdown.html)

### Notes

merge requestとpull request の違い

-> 結論から言うと全く同じ(位置づけが違うためあえて変えてるっぽい)

- Refs: [GitLab flowから学ぶワークフローの実践 開発手法・プロジェクト管理 POSTD](http://postd.cc/gitlab-flow/)
- Refs: [git - Pull request vs Merge request - Stack Overflow](http://stackoverflow.com/questions/22199432/pull-request-vs-merge-request)
