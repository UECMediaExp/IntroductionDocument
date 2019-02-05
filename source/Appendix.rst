追加情報
=====================================================================




演習1-5 の MNIST　データセットダウンロード
---------------------------------------------------------------------

MNIST を大学でダウンロードする場合には， proxy を設定する必要があります．

.. code-block:: python
              
   import os

   #proxy 設定
   os.environ['http_proxy'] = 'http://proxy.uec.ac.jp:8080/'
   os.environ['https_proxy'] = 'http://proxy.uec.ac.jp:8080/'


なお，CED と IED でダウンロードすると，両方のハードディスクにデータセットのファイルが残る場合あるので注意が必要です．



2019/01/22 の資料
---------------------------------------------------------------------

下記から資料をダウンロードできるはずです．

`資料 PDF <20190122.pdf>`_


Github で実験資料が更新された場合の対処
---------------------------------------------------------------------

github では課題資料の更新がしばしば行われます．
そのため，以下のコマンドを git レポジトリ上で実行して適宜，更新を行ってください．

* 課題2 の場合
  
.. code-block:: sh

    git pull https://github.com/UECMediaExp/Kadai2 master


* 課題3 の場合                

.. code-block:: sh

    git pull https://github.com/UECMediaExp/Kadai3 master



学外からの CED の GPU サーバーアクセス
---------------------------------------------------------------------   

VPN サーバーを用いる（基盤センターのVPNの項を参照）

https://www.cc.uec.ac.jp/ug/ja/remote/vpn/

ただし，proxy の除外リストに以下をいれて，除外しておくこと

* proxy.uec.ac.jp:8080

* 172.21.0.0/16

* *ied.inf.uec.ac.jp

* *ced.cei.uec.ac.jp


