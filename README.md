# M1 Mac上でPythonの開発環境構築やっていきます

## これはYouTube動画の資料です
- M1 MacにPythonインストールして開発環境構築してみた https://youtu.be/dqw4aAgEwoQ

---

## はじめに
- なるべく、プログラミング初学者向けにもわかりやすく解説していきます
- いっしょに やっていきましょう
- 2021年1月時点の情報です
  - M2のMacが出る頃(いつ?)には 古い情報になってるはずなのでお気をつけください

## 自己紹介：オサミー
- ソフトウェアエンジニア。株式会社プレジニア代表取締役。
- iPhoneアプリ開発歴10年。企画開発したiPhoneアプリ160万ダウンロード以上。
- 新規事業立上げ支援など。

## 動画(Python環境構築)の目次
- 理論編: M1 Macの罠とは
- 実践編
  - ①Webアプリ(django)
  - ②データ分析(jupyter, pandas, numpy, matplotlib)
  - ③ディープラーニング(tensorflow)

---

# 理論編：M1 Macの罠とは
## 理論編 目次
1. 「M1 Mac」の環境は 「Intel Mac」のPython開発環境と大きく違うことに注意しよう！
2. Pythonにはバージョンがあることに注意しよう！
3. Pythonの仮想環境がたくさんあることに注意しよう！
4. Rosseta上なのかARMアーキテクチャ上なのか意識しよう！

## 1.「M1 Mac」の環境は 「Intel Mac」のPython開発環境と大きく違うことに注意しよう！
- これは、「M1 Macでプログラミングする上で注意すべき」ポイント①
- 例えば、progateの記事「Pythonの開発環境を用意しよう！（Mac）」だと、
  - https://prog-8.com/docs/python-env
  - HomeBrewとpyenv使おう、と買いてあるが、、、「M1 Mac」では動かない！
  - これは「Intel Mac」の情報！
- 「Intel Mac」の古い情報に注意しよう！
  - Intel Macとは：
    - Intelのチップ(CPU)が搭載されたMac
    - 古い
  - M1 Macとは：
    - Apple社が設計したM1チップが搭載されたMac
      - ARM社がApple社へチップの回路図を提供してる
      - ので、M1チップのアーキテクチャ(設計方法)を「ARMアーキテクチャ」と呼ぶ
    - M1チップを「Apple Silicon」とも呼ぶ
    - 2020年11月に発売！（新しい）
- M1 Macでは
  - Homebrewは使わないで！（動くけど難易度高い）
  - pyenvは使わないで！（動かない=2021年2月時点）

## 2. pythonにはバージョンがあることに注意しよう！
- これは、pythonの開発環境でハマりがちなポイント①
- python2系とpython3系は 全然違う！
  - 「文法」が大きく違う
    - 文法とは 書き方の話
    - python2系では `print "Hello world!"`
    - python3系では `print("Hello world!")`
- これからはpython3系を使おう！
  - python2系は 開発が終了している
  - python2系の廃止日(End Of Life)は2020年1月1日だった

- 「Intel Mac」と「M1 Mac」の違い
  - Intel Macでは
    - pyenv 使って、いろんなバージョンいれてた
      - `2.7`, `3.4`, `3.7` etc..
  - M1 Macでは
    - pyenvは使わない

## 3. pythonの仮想環境がたくさんあることに注意しよう！
- これは、pythonの開発環境でハマりがちなポイント②
- 仮想環境がいろいろあって よくわからない！
  - venv
  - virtualenv
  - anaconda
  - miniconda
  - miniforge
  - ...

- 仮想環境とは:
  - Python を使って開発や実験を行うときは、用途に応じて専用の実行環境を作成し、切り替えて使用するのが一般的。
  - こういった、一時的に作成する実行環境を「仮想環境」と呼ぶ
    - https://www.python.jp/install/macos/virtualenv.html
  - 例）
    - プロジェクトAでは, Python3.7 で Django1.10 使う
    - プロジェクトBでは, Python3.8 で Django1.11 使う
  - 最近は Docker 使って、コンテナイメージ化するのが流行り
    - でも 自分はあんまりDockerつかったことないので、すいません解説できずm(_ _)m
    - Dockerも、M1 MacではIntel Macと違う！（らしい）　ご注意ください

- 「Intel Mac」と「M1 Mac」の違い
  - Intel Macでは
    - anacondaでもvirtulenvでもなんでも！
    - オサミーは pyenv + virtualenv派だった
  - M1 Macでは
    - anacondaやminiconda, virtualenvは使わない！
    - miniforgeを使おう！（詳細は後述）

## 4. Rosseta上なのかARMアーキテクチャ上なのか意識しよう！
- これは、「M1 Macでプログラミングする上で注意すべき」ポイント②
- いま動かそうとしてるプログラムは、「Rosseta上なのか」「ARMアーキテクチャ上なのか」意識すべし！
  - Rosetta上では動くが、ARMネイティブで動かないプログラムがある

- Rosettaって何？
  - M1 Macの特徴：Rosetta を使ってIntel Mac用のソフトウェアを使うことができる(例外あり)
  - Rosetta とは
    - 従来のインテル用のMacアプリを Apple Silicon Mac上で自動的に変換して実行できるようにする仕組み
    - 「Rosettaを使用してひらく」チェックボックスつけてアプリ起動すると、Rosetta上で動く
      - 例) ターミナル, Xcode, iTerm2 など
  - Rosetta使えば動くのか ARMネイティブ対応(M1最適化されてる)なのか ソフトウェア一覧まとめサイト
    - Is Apple silicon ready?
    - https://isapplesiliconready.com/

- いま「Rosseta上なのか」「ARMアーキテクチャ上なのか」確認できるコマンドは後述

---

# 実践編
## 実践編 目次
- 前提
- ①Webアプリ(Django)
- ②データ分析(jupyter, pandas, numpy, matplotlib)
- ③ディープラーニング(tensorflow)

## 前提
### インストール環境
- macOS BigSur 11.1
- MacBook Air(M1, 2020)
- Python 初期状態

### Python初期状態(デフォルト)とは
- ターミナル.appで叩いたコマンドと結果
  - ターミナルの場所：Finderでアプリケーション>ユーティリティ>ターミナル.app
- `python -V` -> `Python 2.7.16`
- `which python` -> `/usr/bin/python`

- `python3 -V` -> `Python 3.8.2`
- `which python3` -> `/usr/bin/python3`
  - `missing xcrun at :/Library/Developer/CommandLineTools/usr/bin/xcrun`
  - というエラーになったら、それはXcode Command Line Toolsがインストールされてないようなので
  - コマンド `xcode-select --install` を叩いて まずCommand Line Toolsをインストールしてみてください

- `conda` -> `zsh: command not found: conda`

### Pythonの文法だけ試したい人はコチラががおすすめ！
- 文法だけ色々試したい場合は、「ブラウザで動く環境」がおすすめ！　
  - Pythonの開発環境を構築するだけでも 大変なので
  - ブラウザで動く環境（例）:
    - https://skulpt.org/
    - https://trinket.io/python
    - 「文法学びたいだけの人」はこっちがおすすめ

- インタラクティブモードもあるよ
  - ターミナルで、 `python3` 打つと 実行するとはじまる
  - Control + D で終了
  - pythonってM1 Macの初期状態で、すでにMacにインストール済み.
    - 文法だけ学びたい人 や ちょっとしたスクリプト書きたい人にとっては...
    - これから説明するcondaとか必要なし

### いま 「Rosetta上なのか」「ARMアーキテクチャ上なのか」意識することが重要！
- 確認コマンド:ターミナルで `uname -m` 打つ
  - `arm64`と出力 : ARMアーキテクチャ で実行中
  - `x86_64`と出力 : Rosetta利用 または ネイティブIntelアーキテクチャ で実行中

- オサミーの場合：
  - ARMアーキテクチャで実行したい場合「ターミナル.app」で実行
  - Rosettaで実行したい場合「iTerm2.app」で実行
  - VSCode上では適宜 `$ arch -x86_64 zsh` や `$ arch -arm64 zsh` で切り替えする

## ---------ここまで実践編の前提---------

## ①Djangoを使ったWebアプリ開発
### 目次: Webアプリ開発
- 1-1. Visual Studio Codeをインストールしよう
- 1-2. miniforgeでcondaをインストールしよう
- 1-3. condaでWebアプリ開発用の環境をつくろう
- 1-4. Djangoでローカルサーバーを起動しよう

### 1-1. Visual Studio Codeをインストールしよう
- https://code.visualstudio.com/
  - オサミーバージョンは 1.52.1

### 1-2. miniforgeでcondaをインストールしよう
- M1 Macでは：anaconda🙅‍♂️ や miniconda🙅‍♂️ や homebrew🙅‍♂️ や pyenv🙅‍♂️ は使わないで！🙅‍♂️🙅‍♂️🙅‍♂️🙅‍♂️🙅‍♂️🙅‍♂️
- ARMアーキテクチャに最適化してるのは miniforgeだけ(オサミーの知りうる情報 & 2021年1月末時点)
- miniforge(conda)は、もともとデータ分析用に用意されてる環境だけど、Webアプリ開発にも使えるお！

### 1-2-1.用語説明：condaとは？miniforgeとは？
- miniforgeとは？
  - minicondaと同等に軽い Python 実行環境プラットフォーム。
  - minicondaとは？違いは？
    - miniforgeは コミュニティ。conda環境で必要最小限のパッケージ。
    - minicondaは anacondaの小さいバージョン。conda環境で必要最小限のパッケージ。
  - てか anacondaとは？
    - anacondaは、「データサイエンス向けのPythonパッケージなどを提供するプラットフォーム」
      - 科学技術計算などを中心とした、多くのモジュールやツールのコンパイル済みバイナリファイルを提供
      - 簡単にPythonを利用する環境を構築できる
    - anacondaとminiconda比較
      - anacondaは、パッケージ全部入り。とにかくデカイ。容量が大きい。
      - minicondaは、必要最小限のパッケージだけ。軽くてすぐはじめられる。
      - ただし両者とも M1 Mac(ARMアーキテクチャ)に非対応(2021年1月時点)
      - [classmethodさんの記事](https://dev.classmethod.jp/articles/difference-between-anaconda-and-miniconda/)参照  
  - miniforgeは、minicondaの「M1 Mac対応版」と考えてよい
    - まとめると、
    - 「M1 Mac(ARMアーキテクチャ)に対応している、
    - 必要最小限のパッケージが揃った、
    - データ分析用Python 実行環境プラットフォーム」
    - https://github.com/conda-forge/miniforge

### 1-2-2.miniforgeインストール方法
1. [githubリポジトリ](https://github.com/conda-forge/miniforge) から「Miniforge3-MacOSX-arm64」をダウンロード
2. ターミナルでコマンド `bash Miniforge3-MacOSX-arm64.sh` 叩く

- いろいろ聞かれるがすべて「yes」でOK

#### condaの初期化処理が ~/.zshrc に書き込まれる
- `~/.zshrc` とは ターミナルひらくときに最初に読み込まれるファイル
- 余談：シェルが zsh ではなく bashだったら `.bashrc` に該当する
  - シェルとは：ターミナルでコマンド実行するソフトウェア(みたいなもの)
  - macOS BigSurからデフォルトで シェルが zsh になった(いままではbash)

- コマンド `source ~/.zshrc` で .zshrc を読み込める
  - するとcondaのbase環境が有効化される
    - コマンドラインの頭に(base)がつく
  - ターミナル立ち上げるたびに、condaのbase環境が起動するのが鬱陶しかったら下記コマンド叩く
    - `conda config --set auto_activate_base false`

### 1-2-3.conda の基本的なコマンド
- まずは `conda deactivate` で 現在起動されてるconda環境を停止する

#### conda環境起動前のコマンド
- `conda activate` で デフォルト環境(base)の起動

- `conda create -n my_env python=3.9` で環境作る
  - `-n`オプションは、環境名
  - 今回は「webapp_env」と「ml_env」の、2つの環境をつくる（あとで）
  - `python=3.9` はpythonのバージョン指定
- `conda info -e` で作成済みのconda環境を確認する
- `conda activate my_env` で「my_env」というconda環境を起動する
  - 余談："my_env"は「俺の環境(my environment)」という意味。サンプルコードでよくでてくるね。

#### conda環境起動後のコマンド
- `conda list` で、その環境でインストール済みパッケージ表示
- `conda install ${package_name}` でその環境にパッケージをインストール
  - 例）conda install jupyter
  - `conda install python=x.x` で 他のバージョンのpythonをインストールできる
- `conda deactivate` で いま起動してるconda環境を停止
- 詳しくは[公式ドキュメント](https://docs.conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands)参照

### 1-3. condaでWebアプリ開発用の環境をつくろう
- `conda create -n webapp_env python=3.9`
  - webapp_env という名前の conda環境をつくる. pythonのバージョンは3.9で
- `conda activate webapp_env`
  - webapp_env という名前の conda環境を起動
- `conda install django`
  - その環境に Django パッケージをインストール
  - オプション`-c`つけてチャンネルを明示的にしてもよい 
    - `conda install -c conda-forge django`
  - https://anaconda.org/conda-forge/django
- `conda list`
  - その環境でインストール済みパッケージ表示. 

### 1-4. djangoでローカルサーバーを起動しよう
- `django-admin startproject helloworld`
  - 「helloworld」という名前のdjangoプロジェクトをつくる(フォルダが作成される)
- `cd helloworld`
  - ディレクトリ移動
- `python manage.py migrate`
  - マイグレート（おまじないみたいなもん. ここでは解説省きます🙇‍♂️）
- `python manage.py runserver`
  - サーバー起動
- http://127.0.0.1:8000/ へアクセス
  - ローカルサーバー起動してることを確認

---

## ②numpyやpandasを使ったデータ分析
- ①で使ったminiforgeのcondaを前提にすすめるので、見てない方は①の「1-2. miniforgeでcondaをインストールしよう」から先に見てね

### 目次: データ分析
- 2-1. condaでデータ分析用の環境をつくろう
- 2-2. Jupyter Notebookを立ち上げて試そう

### 2-1. condaでデータ分析用の環境をつくろう
- `conda create -n ds_env python=3.9`
  - ds_env という名前の conda環境をつくる. pythonのバージョンは3.9で
  - 余談：dsは "data science" の略。
  - `conda info -e` で 作成済みの環境を確認
- `conda activate ds_env`
  - ds_env という名前の conda環境を起動
  - `conda list` で その環境にすべてインストールされているパッケージ確認

#### その環境にjupyter, numpy, pandas, matplotlib をインストール
- `conda install jupyter`
  - ブラウザベースの対話形式実行環境「jupyter」のインストール
  - 余談：最近は「Jupyter Notebook」よりも「JupyterLab」が流行りつつある
    - JupyterLabは次世代のUI環境でNotebookより多機能. 色々できる.
    - 好みでJupyterLabインストールしてもよい -> `conda install jupyterlab`
- `conda install numpy`
  - 行列計算ライブラリ「numpy」のインストール
- `conda install pandas`
  - データ構造演算ライブラリ「pandas」のインストール
- `conda install matplotlib`
  - グラフ描画ライブラリ「matplotlib」のインストール
- `conda list`
  - その環境でインストール済みパッケージ表示. 

- その他パッケージは 下記サイトから検索してインストール  
  - https://anaconda.org/search
  - OpenCV, JupyterLab, scikit-learn etc..

### 2-2. Jupyter Notebookを立ち上げて試そう
- `jupyter notebook`
  - Jupyter Notebook立ち上げる -> 勝手にブラウザで開かれる
  - Jupyter Labの場合は コマンド`jupyter lab`

- 右上のNewボタン>Python3を選び、Python3のノートブックをつくる
- まずはそれぞれimport

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

- バージョン確認など

```
# jupyter上に画像表示したいとき
# %matplotlib inline

np.__version__
pd.__version__
plt.plot([1,3,4,6,6])
```

---

## ③TensorFlowを使ったディープラーニング
- 🙅‍♂️conda使わない (もちろんHomeBrewも pyenvも使わない 🙅‍♂️)
- M1 Mac(ARMアーキテクチャ)に最適化されたTensorFlow使っていく
  - https://blog.tensorflow.org/2020/11/accelerating-tensorflow-performance-on-mac.html

### 目次：ディープラーニング
- 3-1. tensorflow_macosでtensorflowをインストールしよう
- 3-2. venvの仮想環境"tensorflow_macos_venv"を起動しよう
- 3-3. kerasでmnist使って画像認識させてみよう

### 3-1. tensorflow_macosでtensorflowをインストールしよう
- [githubのリポジトリ](https://github.com/apple/tensorflow_macos) をcloneしてくる
  - `git clone https://github.com/apple/tensorflow_macos.git`
- インストールスクリプトを叩く
  - `cd tensorflow_macos`
  - `bash scripts/download_and_install.sh`
    - 色々聞かれるけどすべて[y] でOK
    - ホームディレクトリ `~/` に、`tensorflow_macos_venv` がダウンロードされている

### 3-2. venvの仮想環境"tensorflow_macos_venv"を起動しよう
- `. ~/tensorflow_macos_venv/bin/activate`
  - venvの仮想環境"tensorflow_macos_venv" を起動
    - どのディレクトリで実行してもOK
    - 起動したら コマンドラインの頭に(tensorflow_macos_venv) がつく
    - pythonのインタラクティブモードで `import tensorflow` が成功するか確認
    - `deactivate` でその環境を停止
- `pip freeze`
  - 現在の環境にインストール済みのパッケージを確認してみる
  - 余談：pip とは「PyPI:The Python Package Index」.　パッケージ管理ツール.
    - 読み方は「ぱいぴーあい」
    - https://pypi.org/
    - Pythonのパッケージ(ライブラリ)管理は、conda使うかpip使うかどっちか！みたいな感じだよね
    - https://docs.conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands

### 3-3. kerasでmnist使って画像認識させてみよう
- Keras の[サンプルコードサイト](https://keras.io/examples/vision/mnist_convnet/)にアクセス
  - CNNというニューラルネットワークを組んで, mnist(手書き数字のデータセット. 28x28が7万枚.)の書かれた数字を認識するタスク
- ファイルを適当につくる(今回は`simple_mnist_convnet.py`)
- コピーアンドペースト
- `python simple_mnist_convnet.py`
  - minist の「画像認識タスク（学習と検証）」実行

## お疲れ様でした！！！
