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


課題 `kadai2-3.ipynb` 更新
---------------------------------------------------------------------

更新方法がうまくできないようですので　`kadai2-3.ipynb` の差分部分を貼り付けます

.. code-block:: python

    num_epoch=30
    batch_size=100

    show_graph2=ShowGraph(num_epoch)

    reduce_lr2 =keras.callbacks.ReduceLROnPlateau(monitor='val_loss', factor=0.1,patience=5, min_lr=0.0001)
    # ImageDataGeneratorを使った場合は，学習には fit でなくて，generatorから画像を読む fit_generator を使います．
    # 第一引数は，datagen.flow(x_train, Y_train, batch_size=100) などとします．
    history2 = model2.fit_generator(datagen.flow(x_train, Y_train, batch_size=batch_size), epochs=num_epoch+1, steps_per_epoch=len(x_train)//batch_size,
                                validation_steps=len(x_test)//batch_size, validation_data=test_datagen.flow(x_test,Y_test,batch_size=batch_size), 
                                verbose=0, callbacks=[show_graph2, reduce_lr2])
    del show_graph2


課題 `kadai2-4.ipynb` 更新
---------------------------------------------------------------------

`kadai2-4.ipynb` の差分部分を貼り付けます． proxy の部分を書き換えてください

.. code-block:: python

  os.environ["http_proxy"] = "http://proxy.uec.ac.jp:8080/"
  os.environ["https_proxy"] = "http://proxy.uec.ac.jp:8080/"



課題 `kadai2-5.ipynb` 更新
---------------------------------------------------------------------

`kadai2-5.ipynb` の差分部分を貼り付けます
Animaldataset のディレクトリまでのパスを指定することが必要なので，

.. code-block:: python

  # CED/IEDを自動判定して，datadir をセット．
  cdir=os.getcwd()
  if '/IED_HOME/' in cdir or '/.ced_ubuntu/' in cdir:
    datadir="/ced-home/staff/yanai/media/"
  else:
    datadir="/usr/local/class/object/media/"

  if '/yanai/' in cdir:
    datadir="/export/space/yanai/media/"




Github で実験資料が更新された場合の対処（うまく動かない）
---------------------------------------------------------------------

github では課題資料の更新がしばしば行われます．
そのため，以下のコマンドを git レポジトリ上で実行して適宜，更新を行ってください．

* 課題1 の場合
  
.. code-block:: sh

    git pull https://github.com/UECMediaExp/Kadai1Shouno master


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


