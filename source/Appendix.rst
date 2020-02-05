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


なお，CED と IED でダウンロードすると，両方のハードディスクにデータセットの *ファイルが残る* 場合あるので注意が必要です．



2020/01/20 の資料
---------------------------------------------------------------------

下記から資料をダウンロードできるはずです．

`資料 PDF <2020121.pdf>`_



IED/CED の GPU サーバーアクセス
---------------------------------------------------------------------   

ただし，proxy の除外リストに以下をいれて，除外しておくこと

.. code-block:: bash

   `proxy.uec.ac.jp:8080`
   `172.21.0.0/16`
   `*ied.inf.uec.ac.jp`
   `*ced.cei.uec.ac.jp`


面倒であれば，学内の ホストは proxy を使わないという

* `*uec.ac.jp`

を入れるでもOKです．


学外からの GPU サーバーアクセス
---------------------------------------------------------------------   
 
VPN サーバーを用いる（基盤センターのVPNの項を参照）とできる（はず）です．

https://www.cc.uec.ac.jp/ug/ja/remote/vpn/


Errta
---------------------------------------------------------------------   

課題２
^^^^^^^^^^^^^^^^^
画像データセットのような大きなファイルをリポジトリに含めると（拡張子が `.h5` のようなファイル）
Github が拒否するケースがあります．この場合は `*.h5` のファイルをリポジトリの追跡リストから外してください．
`git add` で追加しなければ大丈夫ですが，既に追加してしまった場合は，

.. code-block:: bash
   
    git rm --cached ファイル名

とかで， `*.h5` なファイルを外してあげてください．
あとは `git add` で `*.h5` なファイルを追加しなければよいのですが，たぶん `git` はおせっかいに
`*.h5` なファイルが add していないよというメッセージを出してくるかと思います．
このメッセージを見たくなければ git の管理ファイルである `.gitignore` というファイルに `*.h5` という記述をしてあげてください．


課題３−３
^^^^^^^^^^^^^^^^^

セルに余計な i が入っているのでとってください．

.. code-block:: python

  for j in range(steps):
      inputs = np.vstack((inputs,start+step*(i+j)))

のようになっていますが， `i` は未定義変数なので，

.. code-block:: python

  for j in range(steps):
      inputs = np.vstack((inputs,start+step*j))

とするのが正解です．      
      

課題３−３
^^^^^^^^^^^^^^^^^
      
H264符号化による動画ファイル(MP4)の作成コマンドが，うまく行かない場合は
webM フォーマットを試してみてください．

課題のサンプルコードでは， `libx264` エンコーダを用いていますが，この部分を

.. code-block:: bash

   !ffmpeg -y -framerate 15 -i result/gan1/img_%04d.png -vcodec libx264 -pix_fmt yuv420p -r 60 result/gan1/gan_movie.mp4


`vp8` エンコーダに変えてください．   

.. code-block:: bash

   !/usr/local/anaconda3/bin/ffmpeg -y -framerate 15 -i result/gan1/img_%04d.png -vcodec vp8 -r 60 result/gan1/gan_movie.webm

で，WebM フォーマットになるはずで，firefox 標準で再生される（ハズ）です．
