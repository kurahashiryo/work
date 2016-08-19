**Table of contents**
 
[TOC]
 
###**1. 公式サイト**
####**1.1. トップページ**
[https://www.opendaylight.org/](https://www.opendaylight.org/)
####**1.2. ODLのダウンロード**
[https://www.opendaylight.org/downloads](https://www.opendaylight.org/downloads)
####**1.3. バグ管理**
[https://bugs.opendaylight.org](https://bugs.opendaylight.org)
####**1.4. wiki**
 https://wiki.opendaylight.org/view/Main_Page
####**1.5. CI(Jenkins)**
https://jenkins.opendaylight.org/
####**1.6. Code Review(gerrit)**
[https://git.opendaylight.org/gerrit](https://git.opendaylight.org/gerrit)
commitされたソースコードが見れる。コア開発者のレビューとjenkinsによる自動テストを
クリアしたらGitHubにマージされる。
####**1.7. リポジトリ**
https://nexus.opendaylight.org/
 
###**2. 問い合わせ**
####**2.1. メール**
**・Controller**
controller-dev@lists.opendaylight.org
**・OVSDB**
 ovsdb-dev@lists.opendaylight.org
**・NetVirt**
 netvirt-dev@lists.opendaylight.org
 
####**2.2 Q&A Forum**
https://ask.opendaylight.org/questions/
投稿する場合はアカウントが必要
 
####**2.3 IRC**
https://webchat.freenode.net/
「Channels:」に「#opendaylight」を入力してログイン
「Nickname:」は任意の名前
IRCのクライアント(LimeChatなど)がある場合はそれを使ってもOK

###**3. ODLコマンド関連**
####**3.1. ODLの起動**
解凍したODLディレクトリのbinにあるkarafもしくはstartを実行して起動します

> {ODLデイレクトリ}/bin/karaf 
>または
> {ODLデイレクトリ}/bin/start 

ODLはkarafを使用しており、起動直後は何も動作しません
feature:installコマンドを実行することで、ODLの各モジュールがインストールされ、動作する機能が追加されます
>etc/org.apache.karaf.features.cfgのfeaturesBootに初回起動時にインストールするモジュールを記載することが可能

####**3.2. 機能追加**
3.1で記載したように、ODLはfeature:installというコマンドを使用して、各モジュールをインストールして使用することが可能
>feature:install {feature名}

追加可能な機能は以下のコマンドで確認可能
>feature:list

オプションの"-i"を付けるとインストール済の一覧が見れる
feature:listにはリポジトリに登録されているfeatureが表示される
登録されているリポジトリは以下のコマンドで確認可能
>feature:repo-list

以下のような書式のリストが表示される

>ovsdb-1.2.3-Beryllium-SR2  | mvn:org.opendaylight/netvirt/feature-netvirt/1.2.3Beryllium-SR2/xml/features
>:

左側はfeatures名、右側はfeaturesのmvnパスが表示される
{KARAF_HOME}/system/org/opendaylight/netvirt/feature-netvirt/1.2.3-Beryllium-SR2/xml/features
配下にxmlファイルがあり、featuresの設定が記載されている
xmlの中身には以下のようなパラメータが記載されている
>featuresタグ - ODLに登録するfeatures;name属性に指定した名前がfeature:repo-listの左側の名前が表示
>repositoryタグ - 依存関係のあるリポジトリ
>featureタグ - osgiのfeature設定;nameに指定した名前がfeature:listに表示される
>featureタグ - featureタグの中にあるfeatureは依存関係のあるfeatureを指定;同時にfeature:installされる
>bundleタグ - featureインストール時にインストールされるモジュール(jar)
>configfileタグ - featureで使用するコンフィグファイル

karafのfeature:install(厳密にはbundle:install)時に参照するリポジトリは以下のファイルで設定

>**{KARAF_HOME}/etc/org.ops4j.pax.url.mvn.cfg**
> 
>ODLでは{KARAF_HOME}/systemディレクトリをデフォルトリポジトリとして設定し、このディレクトリ内でモジュールが見つからない場合はセントラルリポジトリに検索しにいっている

####**3.3. よく使うコマンド**
指定したfeatureの依存関係やインストールされるバンドル(モジュール)情報を表示(xmlの中身を簡素にしたものが表示される)
>feature:info {feature名}

指定したfeatureをインストール
>feature:install {feature名}

featureの一覧を表示
>feature:list

リポジトリ登録されているfeaturesの一覧を表示
>feature:repo-list

featuresをリポジトリに登録する
>feature:repo-add

featuresをリポジトリから削除する
>feature:repo-remove

インストール済featureのwebサービス情報一覧を表示
>web:list

インストール済のバンドル(jar)一覧を表示
>bundle:list

指定したリポジトリのパスにあるバンドルモジュールをインストールする
>bundle:install {リポジトリパス}

指定したバンドルIDのモジュールを現在のリポジトリにあるモジュールに更新する
>bundle:update {バンドルID}

###**4. 開発**
 
####**4.1. ソースコード**
ソースコードはGitHub上で管理
https://github.com/opendaylight
 
**odlparent**
機能はないが、全てのプロジェクトのルートプロジェクトになっているため、各プロジェクトの共通設定などは全てこのプロジェクトで定義される
https://github.com/opendaylight/odlparent
**OVSDB**
https://github.com/opendaylight/ovsdb
**netvirt**
https://github.com/opendaylight/netvirt
**Neutron**
https://github.com/opendaylight/neutron
**Controller**
https://github.com/opendaylight/controller
**OpenFlowPlugin**
https://github.com/opendaylight/openflowplugin
**OpenFlowJava**
https://github.com/opendaylight/openflowjava

>開発はTrelloを使ってタスク管理しているプロジェクトもある
>https://trello.com/opendaylightproject
 
####**4.2. コーディング**
既存の機能を修正する場合はGitHubのリポジトリからソースコードをcloneして修正する
 
 > git clone {プロジェクトのURL} 

####**4.3. ビルド**
 
**事前インストール**
> maven 3.3.9
> JDK 1.8系

**ODL用のsettings.xmlを取得**
>https://github.com/opendaylight/odlparent/blob/master/settings.xml~/.m2/settings.xmlと置き換える
 >プロキシーを使っている場合はプロキシー情報もsettings.xmlに記載する
 
修正したプロジェクト(モジュール)のルートディレクトリ(pom.xmlがあるディレクトリ)で以下のコマンドを実行

>mvn clean install -D skipTests

ビルドに成功するとtargetディレクトリが作成され、そのフォルダ配下に修正モジュール(jarファイル)が作成される
 
####**4.4. 配備**

作成(修正)したモジュールは以下の手順で配備します
>beryllium以降では試してないのでだめだったら教えてください

・バージョン等、モジュール情報に変更がある場合
>1. feature:installで既にインストール済の場合はfeature:uninstallでアンインストールする
>2. feature:repo-listで該当モジュールのリポジトリパスを取得
>3. feature:repo-remove {リポジトリパス}でfeaturesをODLから削除
>4. systemディレクトリ配下に作成したモジュールを配置
>5. feature:repo-add {新しく配置したリポジトリパス}でリポジトリ登録
>6. feature:installでインストールする

・ソースコードだけ修正した場合
>1. bundle:listで置換したいモジュールのバンドルIDを取得
>2. systemディレクトリ配下の該当するjarファイルを修正したjarファイルに置き換える
>3. bundle:update {バンドルID}でモジュールを更新 
 
###**5. 外部発信向け**
 
####**5.1. OSS開発コミュニティサイト**
https://www.openhub.net/
OSSのコード規模やDeveloper数など、開発に関連する情報が見れる(ODLの紹介資料を作る時などに使用している)
 
####**5.2. Facebook**
「OpenDaylight TokyoUserGroup」で検索
メンバーからの紹介か申請して承認を得る必要あり
 
####**5.3 Meetup**
http://www.meetup.com/ja-JP/OpenDaylight-Tokyo-User-Group/
勉強会やユーザ会などの告知や募集はこのページから行う(イントラ不可)
 
### **6. Q&A**
Q1. ODLのmainはどこでどのような流れで各種featureが起動されているのか？
 >A. ODLの各プロジェクトは全てOSGIフレームワーク上でbundle(jar)単位で独立して動作しています。各feature(複数のbundleをグループ化したもの)はkarafが起動したタイミングでそれぞれ順不同で起動します(OSGIのパラメータでStartLevelという属性を指定すると順番を決めることが可能なようですが、使ってないように見えました)。が、OSGIの仕様に従った場合、依存関係があるプロジェクトがODLにはあるため、起動順によっては正常に起動しない可能性があります。例えば、OVSDB、NetVirtなどのほとんどのアプリケーションはMD-SALが起動していないと正常に初期化できません。このため、ODLではOSGIの初期化とは別に独自にfeatureの初期化順を定義しています。
>etc/opendaylight/karafフォルダ配下にある各アプリケーションが使用するxmlファイルの先頭の数字が若い順に初期化処理を行うようにしています。
 
Q2. ODL起動時の初期化の流れは？
 >A. OSGIの仕様として、モジュールがインストールされた時の初期化処理としてorg.osgi.framework.BundleActivatorインタフェースのstart()メソッドが実行されます。ODLではモジュールごとにこのインタフェースを実装したクラスが存在し(存在しないものもある)、start()メソッドを実装することで初期化を行っています。Q1の回答でも記載しましたが、これらの処理はbundleの起動順で処理されるので、依存関係がある場合は起動順によっては正常に動作しない可能性があります。そのため、独自の初期化処理も実装しているようです。細かいロジックまではソースを追ってないので分かりません。

Q3. featureの起動方法(スレッド/プロセス)は？数は？
>A. featureはインストール時に自動で起動します。プロセスはjava１つのみでfeatureごとにスレッドが複数作成されて動作します

Q4. 各種処理時の流れは？(ポイントはopenstack, openstack db, odl, odl db)

Q5. 欲しいプロジェクトの情報

>A.
>**neutron**
/neutron
　├─northbound-api 
　│　　　OpenStackからのリクエストを受け付けるREST APIインタフェース
　│　　　REST APIはjerseyライブラリを使って実装
　│　　　実処理は同プロジェクト内のneutron-spiで行う
　├─
└─
　netvirt, controller, mdsal, ovsdb,openflowplugin, openflowjava 

Q6. 調査した関数のまとめ 

OSVDB

Netvirt
 
Neutron

controller



Q7. 知っているfeatureについて利用方法や使い方等 

Q8. YANGについて
>A. 以前展開した安田さんの資料が一番分かりやすいです。私もソース読むときは必ずこの資料を見ながら読んでいます。逆にこれ以上のことは分かりません。
 \\ibkfs15.nsl.ad.nec.co.jp\a03161-01\21.入手資料\20160419_MD-SAL資料\ODLUG-Tokyo-1-1-MD-SAL.pdf
 
