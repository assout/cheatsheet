# Travis CI

Date: 2015-08-22 19:28
Tags: []
Categories: []

---

## Tips

travis.ymlを試す

[Validate your .travis.yml file](http://lint.travis-ci.org/)

---

shellcheck使う

    before_install:
      - sudo add-apt-repository -y "deb http://archive.ubuntu.com/ubuntu/ trusty-backports restricted main universe"
    install:
      - sudo apt-get -qq install shellcheck

### キャッシュして高速化する

apt,pipのキャッシュを利用する

    cache:
      apt: true
      pip: true

bundlerのキャッシュを利用する

    cache:
      bundler: true

ディレクトリをキャッシュする

    cache:
      directories: opencv-2.4.5/build/zip

Refs:.

- [Caching Dependencies and Directories - Travis CI](http://docs.travis-ci.com/user/caching/)
- [【TravisCI】【まとめ】高速化のためにした８つの工夫 - Qiita](http://qiita.com/oh_rusty_nail/items/6d709f48443b6c474392)

