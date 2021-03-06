# Docker

Date: 2015-08-10 11:28
Tags: []
Categories: []

---

## 初回起動

- サービス登録

        systemctl start docker.service
        systemctl enable docker.service
        sudo docker ps

- sudo不要にする

        sudo groupadd docker
        sudo usermod -aG docker oji

## Commands

### Docker

- ホストからIPアドレスを確認

        docker inspect --format '{ { .NetworkSettings.IPAddress } }' mysql
    TODO: ブラケット(`{`)が2こ連続するとGitBookでのビルドがエラーになるのでWorkaroundで空白入れている

- build - イメージを作成する
    - ビルド成功後タグをつける

            docker build -t <tagName> <dockerFileDirectory>

- run - 実行する
    - コンテナ作成

            docker run

    - コンテナに名前をつける

            docker run --name mysql mysql

    - 起動して開きっぱなし(STDINを開きっぱなし)

            docker run -i mysql

    - 終了時にコンテナ破棄する

            docker run --rm -t -i ubuntu /bin/bash

- start - コンテナ起動

        docker start

- stop - コンテナ停止

        docker stop <CONTAINER>

    - すべて停止

            docker stop $(docker ps -a -q)

- restart - コンテナ再起動

        docker restart

- exec - コンテナに入る

        docker exec -it <Names> bash

- rm - コンテナ削除

        docker rm <CONTAINER>

    - すべて削除

            docker rm $(docker ps -a -q)

- rmi - イメージ削除

        docker rmi <ImageID>

    - タグを打ってないイメージを削除

            # コンテナ削除(ステータスがexitedのもののみ)
            docker rm $(docker ps -q -f status=exited)
            # イメージ削除(タグが<none>のもののみ)
            docker rmi $(docker images -q -f dangling=true)

    - 全てのイメージを削除

            docker rmi $(docker images -a -q)

- ps - コンテナ一覧表示
    - 停止中も含め全て表示

            docker ps -a

### Docker Compose

- 起動(linksの依存関係に沿った順番でコンテナを起動)

        docker compose up

    - デタッチドモード(バックグラウンド)で実行

            docker compose up -d

- 関係するコンテナをまとめて終了

        docker-compose stop

- 関係するコンテナをまとめて削除

        docker-compose rm

## Docker Hub Images

### Ubuntu-sshd

Refs. <https://hub.docker.com/r/rastasheep/ubuntu-sshd/>

    # run
    docker run -d -p 22:22 --name test_sshd rastasheep/ubuntu-sshd:14.04
    # login (password=root)
    ssh root@localhost

### MySQL

コマンド

    docker pull mysql
    docker run --name mysql -e MYSQL_ROOT_PASSWORD=mysql -d -p 3306:3306 mysql

ホストからアクセスする(ip addres)

    ip=172.17.0.2
    mysql -h $ip -u root -p test_db
    - mycli
    ip=172.17.0.2
    mycli -h $ip -u root test_db

永続化

    docker pull busybox
    \# 永続化のためのデータ領域を作成
    docker run -v /var/lib/mysql --name mysql_data busybox
    \# マウントして起動
    docker run --volumes-from mysql_data --name mysql -e MYSQL_ROOT_PASSWORD=mysql -d -p 3306:3306 mysql

### GitLab

    wget https://raw.githubusercontent.com/sameersbn/docker-gitlab/master/docker-compose.yml.dist -O docker-compose.yml
    docker-compose up

Refs: [sameersbn/docker-gitlab · GitHub](https://github.com/sameersbn/docker-gitlab)

Caution. 起動できない場合メモリ不足が怪しい!

Refs: [git#GitLab](git#GitLab)

## TODOs

- DBの文字コード変換

