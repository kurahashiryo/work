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
```
ovsdb-1.2.3-Beryllium-SR2  | mvn:org.opendaylight/netvirt/feature-netvirt/1.2.3-Beryllium-SR2/xml/features
:
```
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

####**3.3. 機能追加**

###**4. 開発**
 
####**4.1. ソースコード**
ソースコードはGitHub上で管理
https://github.com/opendaylight
 
OVSDB
netvirt
Neutron
Controller

>Note 開発はTrelloを使ってタスク管理しているプロジェクトもある
>https://trello.com/opendaylightproject
 
####**4.2. コーディング**
既存の機能を修正する場合はGitHubのリポジトリからソースコードをcloneして修正する
 
 > git clone {プロジェクトのURL} 

####**4.3. ビルド**
 
**インストールモジュール**
> maven 3.3.9
> JDK 1.8系

**ODL用のsettings.xmlを取得**
>https://github.com/opendaylight/odlparent/blob/master/settings.xml
 >~/.m2/settings.xmlと置き換える
 >プロキシーを使っている場合はプロキシー情報もsettings.xmlに記載する
 
修正したプロジェクト(モジュール)のルートディレクトリ(pom.xmlがあるディレクトリ)で以下のコマンドを実行

>mvn clean install -D skipTests

ビルドに成功するとtargetディレクトリが作成され、そのフォルダ配下に修正モジュール(jarファイル)が作成される
 
####**4.4. 配備**


 
 

 


 
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
 
 
 ####**6. Q&A**
 
Q. ODL起動時の初期化の流れは？
A. ODLの起動はイコールkarafの起動のみなのでODLの初期化処理というのはありません。各モジュール(bundle)ごとにBundleActivatorを実装したクラスが用意されており、bundle:installされたタイミングでstartメソッドが、uninstallされたタイミングでstopメソッドが呼ばれます
 
 
