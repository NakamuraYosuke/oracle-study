# 環境準備
## ソフトウェアインストール
[!CAUTION]
本勉強会で使用する環境はLinux（Ubuntu等）やMacOSを推奨します。
- ZeroSpaceではDocker Desktopをインストールする際に管理者権限を求められること
- Oracle Databaseのコンテナを作成する公式手順がbash利用のため（Windowsでbash利用することは可能だがZeroSpaceでは上記同様に管理者権限を必要とするため）

### Gitクライアント（Windows OS）
https://git-scm.com/download/win からインストールする。
![](images/git_download.png)
Standalone Installerの64-bit Git for Windows Setupを選択する。

### Gitクライアント（MacOS）
Homebrewを用いて下記コマンドからインストールする。
```
brew install git
```

### Docker Desktop（Windows OS）
https://www.docker.com/ja-jp/products/docker-desktop/ からインストール

### Docker Desktop（MacOS）
Homebrewを用いて下記コマンドからインストールする。
```
brew install --cask docker --force
```

## Oracle Databaseソフトウェアのダウンロード
Gitを用いて下記コマンドからインストールする。
```
git clone https://github.com/oracle/docker-images.git
```

[!TIPS]
Windowsで`git clone`した際に下記のようなエラーが出る場合があります。

```
git : Cloning into 'docker-images'...
発生場所 行:1 文字:1
+ git clone https://github.com/oracle/docker-images.git
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (Cloning into 'docker-images'...:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
 
fatal: unable to access 'https://github.com/oracle/docker-images.git/': SSL certificate problem: unable to get local issuer certifi
cate
```

その場合、SSLサーバ証明書の検証をOFFにしてから実行します。
```
git config --global http.sslVerify false
git clone https://github.com/oracle/docker-images.git
```

上記コマンドを実行したディレクトリに`docker-images`というディレクトリが作成され、下記のファイルがダウンロードされていれば成功です。
![](images/git_filelist.png)

## Oracle Database コンテナイメージの作成
シングルインスタンスのイメージを作成します。
上記`git clone`で取得した資材にはRACなども含まれていますので興味ある方はチャレンジしてみてください。

シングルインスタンスのイメージを作成する資材があるディレクトリへ移動
```
cd ./docker-images/OracleDatabase/SingleInstance
```

イメージ作成のシェルを実行します。
今回使用するバージョンは`19.3`なので、引数としてバージョンを付与します。
```
./buildContainerImage.sh -v 19.3.0 -e
```

実行後、下記のイメージが作成されていれば完了です。
```
docker images oracle/database
```
```
REPOSITORY        TAG         IMAGE ID       CREATED        SIZE
oracle/database   19.3.0-ee   efd629f521d3   21 hours ago   5.55GB
```