# Java

Date: 2014-12-10 19:01
Tags: []
Categories: []

---

## Prelude

- CDI/Weld : Refs: [cdi-weld](cdi-weld)
- Maven : Refs: [Maven](maven)

## Coding Standard - コーディング規約

規約                                                                                                                                                             | 著作者               | 備考
-----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|:--
[Writing Robust Java Code](http://www.ambysoft.com/downloads/javaCodingStandards.pdf)                                                                            | Scott W. Ambler      |
[オブジェクト倶楽部版 Javaコーディング標準](http://objectclub.jp/community/codingstandard/CodingStd.pdf)                                                         | オブジェクト倶楽部   |
[電通国際情報際サービス版 Javaコーディング規約2004](http://objectclub.jp/community/codingstandard/JavaCodingStandard2004.pdf)                                    | 電通国際情報サービス |
[JJGuideline （Java - J2EE Conventions and Guidelines）](http://www.fedict.belgium.be/sites/default/files/downloads/Java_J2EE_conventions_and_guidelines_EN.pdf) | Stephan.J & JCS Team |
[Google Java Style (非公式和訳)](https://kazurof.github.io/GoogleJavaStyle-ja/)                                                                                  | Google               |
[Acroquest Technology Javaコーディング規約](https://www.acroquest.co.jp/webworkshop/javacordingrule/Acroquest_JavaCodingStandard_6_7.pdf)                        | Acroquest Technology |
[Future Enterprise Coding Standards](https://future-architect.github.io/articles/20160902/)                                                                      | Future Architect     | Java 8対応版

## Java SE

### Code idiom

- {}をただのブロックとして使用可能。テストケースとかで、同じ変数名をコピー&ペーストしたいとかの時に重宝する。
    ただ、ややこしいし、無駄に複雑に見えるのでプロダクトコードでは使わないこと！

        // 以下は変数名重複とならない
        { int a = 1;}
        { int a = 2;}

- ゼロ埋め :

        String.format("%03d", number); // 001, 002…

- メソッド名取得

        Thread.currentThread().getStackTrace()[0].getMethodName()

- Mapのインスタンス作成時に値も挿入するイディオム

        Map<String, Integer> map = new HashMap<String, Integer>() {
            {
                put("one", 1);
            }
        };

- オブジェクトのディープコピー

        private static <T> T deepCopy(T target) {
            if (target == null) {
                return null;
            }
            try (ByteArrayOutputStream bos = new ByteArrayOutputStream(1024);
                    ObjectOutputStream oos = new ObjectOutputStream(bos);) {
                oos.writeObject(target);
                try (ByteArrayInputStream byteIn = new ByteArrayInputStream(bos.toByteArray());
                        ObjectInputStream ois = new ObjectInputStream(byteIn)) {
                    return (T) ois.readObject();
                }
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
        }

- ランダムなバイト配列取得

        byte[] b = new byte[20];
        new Random().nextBytes(b);

- 乱数(ランダム値)取得

        // コンストラクタとかでRandomをnewしておいて、それを使ってnextIntを呼び出すのが一番よい。
        new Random().nextInt(n)

    \* (int)Math.random()×(n+1)は効率が悪いので基本↑でやる。  
    Refs: [Math.random()×n か それともRandom.nextInt(n)か - いろいろがんばりたいブログ](http://pushl.hatenablog.com/entry/2012/11/03/004027)

- CPU論理コア数取得

        int core = Runtime.getRuntime().availableProcessors();

- クラスパス上のファイル読み込み

        TestMain.class.getClassLoader().getResources("foo/bar/test.properties"));
        TestMain.class.getResources("/foo/bar/test.properties"));
        TestMain.class.getResources("test.properties"));
        // getResourceAsStreamも同様
        // 基本位置に依存したくないのでgetClassLoaser().getResource()を使えばよさそう

    Refs: [あるプログラマーのワークスペース: getResourceAsStream()でリソースが読み込めない](http://aarkiton.blogspot.jp/2011/09/getresourceasstream.html)

### Java 8

java.io.UncheckedIOException

Stream処理におけるException Tunnelingのために追加された例外。
UncheckedIOException例外クラスは、従来からある検査例外java.io.IOExceptionをラップする目的で、java.lang.RuntimeExceptionから派生した非検査例外(unchecked exception)である。

### Javadoc

- @since, @version
    - @since : 導入されたバージョン
    - @version : 現在のバージョン
        - メソッドに対しては指定不可

### Test

- コンストラクタ
    - コンストラクタをpackage privateスコープにする
    - テストソースの同一パッケージにファクトリユーテリティ作る

## Other command

- `jar`: jar圧縮、解凍など
- `javadoc`: Javadoc生成など
- `jcmd`: スレッドダンプ取得などのユーティリティ
- `jps`: JavaのプロセスID表示(JDK7以降はjcmd推奨)
- `jstack`: スレッドダンプ取得(JDK7以降はjcmd推奨)

## Memo

- 無名内部クラスでは、そのクラスのコンストラクターを定義することは出来ない。
    - Refs: [Javaクラス使用メモ(Hishidama's Java Class use Memo)](http://www.ne.jp/asahi/hishidama/home/tech/java/class_use.html#anonymous_class)
- GlassFish:
    GlassFishは、サンを中心としたオープンソース・コミュニティと、同コミュニティで開発されたJava EE準拠のアプリケーションサーバの名称である。
- WildFly
    JBossが開発するOSSのJava EEアプリケーションサーバ
- JAAS（Java Authentication and Authorization Service）。
    認証を実現するための標準API
    - JAAS認証    ・IDやパスワードなどを利用して認証を行うことで、ユーザーの正当性を判定
        Javaを実行しているユーザーに正当性があることを確認
    - JAAS承認    ・アプリケーションによって、リソースへのアクセス要求が許可できるのかを判定
        ユーザーに対するアクセス権の保持を判定

### Version - 実行可能バージョンについて

> javacでコンパイルするとclassファイルが作られるが、classファイルの中には「どのバージョンのJavaVMで実行できるか」という“Javaクラスの形式”のバージョンが書かれる。[2007-05-15]  
> JavaVM（javaコマンド）では実行できるバージョンが限られており、自分より新しいバージョンで作られたclassファイルは実行することが出来ない （古すぎてもダメ）。

Refs: [Javaアプリケーション メモ(Hishidama's Java-Application Memo)](http://www.ne.jp/asahi/hishidama/home/tech/java/application.html#Java-version)

クロスコンパイルオプション

-target version

> 指定されたバージョンの VM をターゲットにしたクラスファイルを生成します。このクラスファイルは、指定されたターゲット**以降**のバージョンでは動作しますが、それより前のバージョンの VM では動作しません。

\* 太字引用者

Refs: [javac - Java プログラミング言語コンパイラ](http://docs.oracle.com/javase/jp/7/technotes/tools/solaris/javac.html)

### パッケージ名登録サービス

[Package Registration Page](http://www.java-conf.gr.jp/Package/naming/index.html)

`jp.gr.java_conf.assout`

## JUnit

- Classクラスを比較(意外とめんどい)
    - org.hamcrest.CoreMatchers.theInstance(T) を使う
        - 一番よいかも
    - assertEqualsを使う(簡単だが非推奨)
            assertEquals(factory.getMessageType(), Integer.class); // TODO: wrapper classでよいか
    - assertThatを使う
        - かんたん(これでいけるっぽい)
                assertThat(Class, is((Object) Class));
        - がんばる(失敗したときわかるようにdescriptionつけたほうがよい)
                assertThat("actual is " + factory.getMessageType(), factory.getMessageType() == Integer.class, is(true));
        - hamcrest.object.IsCompatibleTypeを使う(coreには入ってないっぽい。。)
                assertThat("クラスから型を検査", ArrayList.class, is(typeCompatibleWith(List.class)));
    - Refs:
        - [実はJUnit4のassertThat()ってしっくりこないんです！（特に、メタプログラミングするレイヤでは） - 達人プログラマーを目指して](http://d.hatena.ne.jp/ryoasai/20110502/1304339487)
        - [hamcrestのMatcherメモ - 都元ダイスケ IT-PRESS](http://d.hatena.ne.jp/daisuke-m/20090710/1247181113)
- `equalTo` と `is`
    > is は equalTo の構文糖であるため、以下は全て等価です。
    >
    > assertThat(actual, equalTo(expected));
    > assertThat(actual, is(equalTo(expected)));
    > assertThat(actual, is(expected));
    > 英語として読み下し易くするために、is に matcher を渡すのが普通です。
- 指定したパッケージのテストをすべて実行するTestSuite :
    標準では無理らしい(ライブラリはありそう) Refs: [java - JUnit4 run all tests in a specific package using a testsuite - Stack Overflow](http://stackoverflow.com/questions/7331214/junit4-run-all-tests-in-a-specific-package-using-a-testsuite)

