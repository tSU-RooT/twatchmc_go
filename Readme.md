#ReadMe

twatchmcはMinecraftのサーバログをTwitterに自動投稿するプログラムです。  
主にプレイヤーの死亡時のログを自動的に投稿します。  
いわゆるバニラ(MOD)が入っていない状態の主要な死因に対応しています。  
主に自分で使って楽しむために作りました。  
最初C++で作っていましたが、冬休みにGo言語で書きなおしました。  
````
(執筆及び最終更新:2015/1/4 作者:tSU-RooT ,<tsu.root@gmail.com>)  
````  
twatchmc(Golang) version:0.1beta(2015/1/4)
## コンパイルについて  
Go言語のビルド環境は前提です、これはOSによって異なります。  
src/twatchmc/key.go にTwitterクライアントのコンシューマーキーとシークレットキーを入れてください。  
その後コンソールから
````
$ go build ./src/twatchmc
````
で実行ファイルが生成できます。  
使用するライブラリの関係上、あらかじめ以下のライブラリのインストールが多分必要です。  

* anaconda  
* go-oauth

通常以下のようにインストールできます。
````
$ go get github.com/ChimeraCoder/anaconda
````  
依存するライブラリも一緒に入ります。  
動作確認環境: ubuntu 14.04 LTS 64bit
## 使い方について
コンパイルした後、まず使用する時にアカウントの認証を行う必要があります。  

認証情報は $HOME/.twatchmc/.keyに保存されます、認証が終了したあと、もう一回起動させると開始できます。  
認証をやり直したい場合 $HOME/.twatchmc/.keyを消すか、-aオプションをつけて起動してください。

## オプションについて(追加)
.twatchmc_configに例えば次のように記述すると、一部のオプションを起動毎に指定する必要がなくなります。  
````
MINECRAFT_JAR_FILE=minecraft_server_1.7.9.jar
````  
またDETECTIONという項目を設定することができます、  
このアプリケーションは通常バニラでは出力からサーバが起動したことを検知しそこからログのwatchを行いますが、MODサーバではMODが様々なログを出力するためうまく動きません。  
このためDETECTIONに正規表現を書いておくとそちらを代わりに使用します。  
推奨としては  
````
DETECTION=.*Server thread/INFO.*There are 0/20 players online.*
````  
という風に記述しておき、Minecraftサーバ起動直後にコンソールからlistを入力し  
プレイヤーリストを確認することでサーバが正しく動作することを確認しそれを検知するようにすることをオススメします。  
またJavaコマンドのオプションを指定したいとき(ヒープの初期サイズを指定したい場合など)は  
OPTION=-Xmx8129M -Xms8129M  
というふうに書いて下さい。(例)

## License  
MIT License  
