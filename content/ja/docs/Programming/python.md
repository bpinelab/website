---
title: "Python"
date: 2022-04-03
weight: 3
description: >
  Pythonプログラミングに関するコンテンツ
---

## 実行環境

- Pyenv を使用して、複数バージョンの Python を利用可能とする。
- Python3.3 以降で標準モジュールとなっている**venv**を使用して、プロジェクト毎の python 仮想環境を作成、使用する。

### 仮想環境を使用する理由

- Python のバージョンはプロジェクト毎に異なる
- 使用する（インストールする）Python ライブラリはプロジェクト毎に異なる

### 実行環境構築

#### Pyenv のインストール

<!-- https://github.com/pyenv/pyenv#basic-github-checkout -->

Pyenv の取得

```
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

環境変数の設定 `~/.bashrc`

```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```

環境変数の設定 `~/.profile`

```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
$ echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
$ echo 'eval "$(pyenv init -)"' >> ~/.profile
```

シェルの再起動

```
$ exec $SHELL
```

Pyenv がインストールされたことの確認

```
$ pyenv -v
pyenv 2.2.2-10-g943c5f99
```

#### Python のインストール

インストールできる Python バージョンの確認

```
$ pyenv install -l
```

バージョン指定した Python のインストール(3.10.1 の場合)

```
$ pyenv install 3.10.1
```

バージョン指定した Python のアンインストール(3.10.1 の場合)

```
$ pyenv uninstall 3.10.1
```

インストールされた Python バージョンの確認

```
$ pyenv versions
  system
* 3.10.1 (set by PYENV_VERSION environment variable)
  3.8.12
```

使用する Python バージョンの変更

- `pyenv shell <version>` -- 現在のシェルセッションのみ有効なバージョンを設定する。
- `pyenv local <version>` -- 現在のディレクトリ(サブディレクトリ含む)に来た時に使用するバージョンを設定する。
- `pyenv global <version>` -- 現在のアカウントで常に使用されるバージョンを設定する。

### 仮想環境作成手順

コマンドラインにて、プロジェクトのルートディレクトリに移動する。

```
$ cd python-project-template
```

`pyenv shell`コマンドで、現在のシェルセッションの Python バージョンを、希望のもの(以下は 3.8.12)に指定する。

```
$ pyenv shell 3.8.12
$ pyenv versions
  system
  3.10.1
* 3.8.12 (set by PYENV_VERSION environment variable)
```

プロジェクトのルートディレクトリ配下の`.venv`に仮想環境を作成する。

```
$ python -m venv .venv
```

作成した仮想環境に接続（有効化）する。

```
$ source .venv/bin/activate
(.venv)$ python --version
Python 3.8.12
(.venv)$
```

仮想環境を切断（無効化）する。

```
(.venv)$ deactivate
$
```

## ソースコード

参照するルール：[Kenneth Reitz recommended in 2013](https://kennethreitz.org/essays/2013/01/27/repository-structure-and-python)

### パッケージ構成

ライブラリ・アプリケーションのどちらとしても利用できるプログラム

```

(project)
├──.venv ............ Python 仮想環境
│ ├── bin
│ ├── include
│ ├── lib
│ ├── lib64
│ └── pyvenv.cfg
├── (project) ....... プログラムのソースコードディレクトリ
│ ├── __init__.py
│ ├── __main__.py
│ └── *.py
├── tests ............ 単体テストのソースコードディレクトリ
│ ├── __init__.py
│ └── *.py
├── .gitignore
├── LICENSE
├── README.md
└── setup.py

```

### 実行方法

main()を直接実行したい場合(project のルートディレクトリで実行)。モジュール(パッケージ)を実行するために使う`m`オプションを使用する。

```
(.venv)$ python -m (project)

```

### pytest方法

main()を直接実行したい場合(project のルートディレクトリで実行)。モジュール(パッケージ)を実行するために使う`m`オプションを使用する。

```
(.venv)$ pytest

```

## コードのスタイルガイド

[PEP8](http://pep8-ja.readthedocs.io/ja/latest/)に記載されている。

|    対象    |                  ルール                   |          例          |
| :--------: | :---------------------------------------: | :------------------: |
| パッケージ | 全小文字 なるべく短くアンダースコア非推奨 |  tqdm, requests ...  |
| モジュール |   全小文字 なるべく短くアンダースコア可   |     sys, os,...      |
|   クラス   |         最初大文字 + 大文字区切り         |   MyFavoriteClass    |
|    例外    |         最初大文字 + 大文字区切り         |    MyFuckingError    |
|   型変数   |         最初大文字 + 大文字区切り         |    MyFavoriteType    |
|  メソッド  |      全小文字 + アンダースコア区切り      |  my_favorite_method  |
|    関数    |      全小文字 + アンダースコア区切り      | my_favorite_funcion  |
|    変数    |      全小文字 + アンダースコア区切り      | my_favorite_instance |
|    定数    |      全大文字 + アンダースコア区切り      |  MY_FAVORITE_CONST   |
