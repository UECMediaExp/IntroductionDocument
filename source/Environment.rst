実験環境の解説
==================================================

1. UEC VPN 環境の準備
------------------------------------------

この実験では，IED/CED の GPU マシンを使います．
(Google Colab とかでも演習はできると思いますが，Colab は使うほど遅いTPUに割り当てられる傾向が見れるので
無料使用の枠での実行はお勧めしません)

IED/CEDにつなぐには大学側のネットワークにホストを入れておく必要があります．
このため大学側と Virtual Private Network (VPN) を形成する必要があります．
IED/CED の計算機で作業する場合は必要ないですが，自宅などから繋いで演習実験を
行う場合は必須ですので情報基盤センターの指示にしたがって VPN を構築する必要があります．
詳細は下記を参照してください．

https://www.cc.uec.ac.jp/ug/ja/remote/vpn/index.html

なお，前期のプログラミング言語実験でやったように，
トンネルを掘って IED のホストそのものをGUIとして使うことは
必須ではなく，Web ブラウザと端末ソフトウェアがあれば，実験遂行は可能です．


1. IED/CEDでJupyterHub を使うための準備
------------------------------------------

この実験では，Webブラウザを介して ``python`` での実験を行います．
そのための環境は ``Jupyter`` を用います．
前期のプログラミング言語実験 python で行った環境とほぼ一緒です．

ちょっと違うのは Jupyter を提供してくれるのが計算機サーバになっている点で
GPU も使えます．このため CED の GPU サーバーをホストとして JupyterHub と呼ばれるサービスにアクセスします．


IED/CED で JupyterHub を使うためには，まず，Jupyter のノートの保管場所を作る必要があります．
これは，各アカウントホームディレクトリ下にある． `~/notebook` フォルダが指定されています．

まず ``sol.edu.cc.uec.ac.jp`` へログインして， `IED_HOME` の下に
`notebook` ディレクトリを作ります．

.. code-block:: sh

   $ ssh sol.edu.cc.uec.ac.jp

この時点で， `~/IED_HOME/notebook` が在るかを確認してください．
なければ，

.. code-block:: sh

   $ cd IED_HOME
   $ mkdir notebook

のようにして，空のディレクトリを作ってもらえるようにしてもらえればOKです．
次に CED 側の GPU でも使えるようおまじないをかけておきます．
（CED側のホストで，`notebook` ディレクトリが所定位置に見えるように細工をしています）

.. code-block:: sh

   $ ln -s ~/IED_HOME/notebook ~/.ced_ubuntu/notebook

これで Jupyter を使う準備が整いました．

CED 標準の CentOS で計算作業をすることはないと思いますが，もしそのような状況になる場合は，

   $ ln -s ~/IED_HOME/notebook ~/.ced_centos/notebook

としておくと共通の `notebook` ディレクトリを使用できます．(`.ced_ubuntu` と `.ced_cenntos`) の部分が違います．


2. Jupyter による実験
------------------------------------------

こんどは，GPU サーバへ，Web を解してアクセスします．
アクセスには Web ブラウザを用いてください．
いずれの課題もGPUを数時間専有することが必要ですので， IEDの32個のGPUのみだけでなく，

http://gpu1.ied.inf.uec.ac.jp/

CEDの34個のGPU (1GPUサーバ * 34台(ただし2台故障中))

http://gpu01.ced.cei.uec.ac.jp/

も活用してください．どちらも同じように利用可能です．

繋げない場合は，VPN設定とプロキシ設定を確認してください．


上手く繋げたら，ここで GPU があいているサーバーを選びます．

すると，Sign in ウィンドウが開きますので，ここで，
大学アカウントのユーザー名とパスワードを入れてください．

このとき，前述の `notebook` ディレクトリがないとエラーが起きます．

適当に Jupyter notebook を作ると `notebook` ディレクトリにファイルができるので
確認してください．


3. Github との接続
------------------------------------------   

課題に関しては github から提供されます．
github アカウントを作成してください(前期プログラミング言語実験 python 参照)．

Jupyter 側で `Terminal` を開くか，remote 環境で `git` の設定を行ってください．
以下，プログラミング言語実験からの抜粋です．前期で IEDで設定した場合は
そのまま引き継がれます．CED で使う場合は再度設定が必要かもしれません．

ユーザー名の設定
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: sh

    git config --global user.name "Hayaru SHOUNO"
    git config --global user.email "shouno@uec.ac.jp"


Proxyの設定
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

また大学の端末を使って作業する場合には，以下の proxy の設定も必要になってきます．
proxy 関連は，学内から通信をする場合に多分必要です．
(参照 https://www.cc.uec.ac.jp/ug/ja/network/proxy/proxy.html)

.. code-block:: sh

    git config --global http.proxy http://proxy.uec.ac.jp:8080
    git config --global https.proxy http://proxy.uec.ac.jp:8080
