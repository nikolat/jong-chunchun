# これは何なの？

テキサスホールデムで便利…かもしれない機能を持つSAORIです。


## 機能説明

2つの機能があります。

estimate: ランダムハンドを相手にしたときの勝率をモンテカルロ法で推定する
hand: 手札(とコミュニティカード)で作れるもっとも強い役を調べる

## estimate

### 使用例

#### その1

自分のハンドとコミュニティカードでランダムハンドを相手にした時の勝率を求める。

estimate,3,D7,C11,S4,3,H1,D1


#### その2

上記に加え相手のハンドを{S4,C4}と仮定したときの勝率を求める。

estimate,3,D7,C11,S4,3,H1,D1,S4,C4


### 引数説明

estimate  - estimate機能を使うよ
3         - コミュニティカードの数
D7        - コミュニティカードの種類(ダイヤの7)
C11       - コミュニティカードの種類(クラブのJ)
S4        - コミュニティカードの種類(スペードの4)
3         - ベットに参加している人数(自分を含む)
H1        - 自分の種類(ハートの1)
D1        - 自分の種類(ダイヤの1)
S4        - 相手(1人目)のカードの種類
C4        - 相手(1人目)のカードの種類


### 戻り値

推定した勝率(%)。
例として、30.0や23,4等。
引数にミスがあったりした場合は-1を返す。


### 注意

estimateの直後の数字はプリフロップ、フロップ、ターン、リバーで数字が違うので注意。
相手のカードを片方だけ指定したい場合は
estimate,0,2,S9,H9,D2,N0
のようにN0を指定する。
これを利用すれば、例えば相手2人のカードを片方ずつ指定することも出来る。
estimate,0,3,S9,H9,D2,N0,C13,N0


## hand

### 使用例

引数に指定したカードで作れる役の中で一番強いものを返す。
例ではストレート。

hand,S4,H5,C7,S6,D8,H4,C12

### 戻り値

強さに応じた数字をResultとして、キッカーの情報をValue*に入れて返す。
Resultはそれぞれ
1 - ハイカード
2 - ワンペア
3 - ツーペア
4 - スリーカード
5 - ストレート
6 - フラッシュ
7 - フルハウス
8 - フォーカード
9 - ストレートフラッシュ
のいずれか。

### 注意事項
キッカーの勝負をするときに比較演算子で簡単に比較するため、
キッカーの数字はA(エース)のみ「14」としてValue*に入っている。
他は元の数字と一緒。
また、カードの枚数は2枚〜7枚の間で変えられます。
例えば、プリフロップなら
hand,S7,S8
フロップで
hand,S7,S8,H2,D13,S10
のように。
