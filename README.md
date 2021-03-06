# これは何？
とあるゲームのミニゲームとなっている「モノリス」をプレイ補助してSランクを目指すツールです。  

ツール起動は[こちら](https://black-wolfwood.github.io/Monolith-Tool/)から    
使い方は[こちら](https://github.com/Black-Wolfwood/Monolith-Tool/issues/1)から    

Webブラウザで動くツールになっています。  
(Chrome,FireFox & Windows,MacOS 両方確認済。)  

- ツールは「Unity Web Player」で作られています。
- 「Unity Web Player」のインストールを促されたらインストールをしてください。
- あれ、画面が固まって起動しない？ > 少し時間かかるのでページ開いたままお待ちを。
- ボタンが効かない？ > ゲームモードが合ってるか確認を。

必ずSランククリア出来るとは言ってない。  
少しでもクリアの助けになれば、と思う。 

# バグったら
ごめんなさい。わざとじゃないんです。    
なんかメチャったら  

Load > Reset History

でなんとかなる。はず。  


# 各ボタンの説明

### ModeChange
このツールには二つのモードがあります。
- GAME : 実際にモノリスパズルをプレイするモードです
- CREATE : モノリスパズルの盤面をエディットするモードです

### CreateMap
初期マップを生成します。全部青で一旦塗りつぶしていますので、必要な色を塗ってください  
キーボード対応していまして

- 1キー : 青色
- 2キー : 白色
- 3キー : 桃色
- 4キー : 黄色

となっており、一度フォーカスした箇所から  
次へ次へと進んでいくようになっています。  
間違えたら該当箇所をクリックして頂くと、フォーカスを移動できます。  

### Save
現在のマップを保存できます。  
保存出来るのは一つだけです。  
二回目からは上書きになります。  
実際にブラウザにデータ保存しているわけではないです、ご安心ください。  
このツール内だけで保存している、といえば分かりますでしょうか。  
よって  
Save > ブラウザを閉じる > 改めてツールを開く > Load  
とやってもロードはできません。ご了承ください。　　

### Load
Saveしたマップを呼び出します。  
途中までマップを編集していた場合は全て破棄されてしまうのでご注意ください。  

### Auto 1
プログラムが自動でモノリスをプレイをします。  
消せるものが無くなったら止まります。  
これを実行した後、Historyでどう消したか確認するのが基本操作になります。  

### Auto 100
自動プレイを100回試行します。  
そして、その内最も残り個数の少なかったものを採用します。  
これを何度も実行して、最後の盤面を見つつ、残り個数が少なく広く開いているものを  
実際のゲームに反映させるのが良さそうです。  

### History
四つのボタンは左から

- 一手目まで戻す
- 一手前に戻す
- 一手先に進める
- 最後まで進める

となっています。

そして、Reset Historyは上の履歴を全て消去します。

# 使い方

まずは適当に触ってみてほしい。  

### 前提
ゲームを立ち上げて、モノリスのイジワルモードを起動します。  
起動したら画面をスマホなりなんなりで写真を撮ります。  
PSキー押下するなりなんなりでゲームを止めておきます。  
(時間制限があるので)  

### 1.ツールを起動する
起動まで少し時間がかかるのでしばらく待機。  
Chromeで開けないって人はFireFoxとかだと安定するかも。  
Unity Web Player使ってるのでインストールしろって言われたら  
インストールしてください。  

### 2.パズルマップを作る
画面左にある「Create Map」ボタンを押下します。  
するとパズル基盤で青一色のブロックが表示されます。  
これは22x11のモノリスと同じ数になっています  

### 3.ブロック色を付けていく
一番面倒な箇所。  
前提で取得した写真を見ながらブロックに色を付けていきます。  
キーボードに対応していて、次へ次へとフォーカスが移るようになっているので  
慣れれば少しずつ早くなっていくはず。  
左下からブロック色を付けていくのがおススメ。  
最初が白一色の方がいい？  

写真を取り込んで自動で作るのに挑戦していましたが、  
カメラの差異や状況の差異(部屋が暗いなど)を乗り越えることが出来ず、  
不安定なので、一旦消してます。  
せめてスクリーンショット機能が使えれば。  

### 4. セーブ
3が終わったら、セーブしておくのをお勧めします。  

### 5. モードチェンジ
「ModeChange」ボタンを押下して、Gameモードに切り替えます  

### 6. プレイ
ブロックをクリックして消してみて挙動を確認したり、  
AUTOでプログラムに消させてみたりしてください。  

実際のゲーム画面と同じように進め、絵柄を見つけたらポーズして  
ツール側で取れるか検証して、手順を確立させてからゲームに戻るのがおススメです。  


# 自動プレイの考え方

まず、プレイ状況を考えてみます。  

- 盤面がある
- 開いていく
- 下にボーナスがあればスコア加算
- 一定以上ボーナスを取得することが出来ればクリア

この内  
「下にボーナスがあればスコア加算」  
これは開いてみないとわかりません。  
なので、「最もスコアを稼ぐ」というのは一旦保留としました。  

そこで  
「最もブロックが少ない状況にすればボーナス絵柄を取得出来ている可能性が高いだろう」  
と考えました。  

以上から  
自動プレイは、とにかくランダムで適当に消しています。  
そして、試行回数を稼いで最も残り個数の少ないものを採用しています。  
後は自動プレイ通りにプレイしてみて、ボーナス絵柄が多めに取れていれば  
Sランクも夢ではありません。  

### 追記
自動プレイだけではちょっと厳しいかも。  
盤面次第ですが残り個数35 - 45だとほぼ絶望的みたいです。  
たまに凄い取り方をしているのがあるので、その取り方を  
参考にするぐらいがいいかも。  
