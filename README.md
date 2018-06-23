# Rails5 簡易ブログの作成 環境構築ガイド

下記の記事を参考に、Rails5系でブログを作成します。

[Railsを始めたばかりの人向け！Railsの仕組みを一から理解しながらブログを作成する](http://ruby-rails.hatenadiary.com/entry/20140813/1407915718)

## 手順
Ruby on Rails最新版とRubyをインストールします。
Railsは2018/6/23時点で version `5.2.0` が最新版のため、こちらを利用します。

githubのrailsリポジトリを参照↓
https://github.com/rails/rails/releases
`.rc .beta` とついていないものが、バグがない安定したversion(Stable)です。

Rails5では、Ruby 2.2.2 以降が必要になりますが、今回は現時点で最新安定板の `2.5.1` を利用します。
https://www.ruby-lang.org/en/downloads/releases/

**実行環境**
- ruby 2.5.1
- rails 5.2.0
- bundler 1.16.1
- macOS High Sierra
なお、DBはsqliteを利用

### 1. 各種ツールをインストール

```
# ブログ作成用ディレクトリ作成
$ mkdir ~/rails_blog
$ cd ~/rails_blog

# Homebrew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# rbenv (ついでにgitも)
$ brew install rbenv git

# PATHの設定 (.bash_profileが存在しない場合)
$ echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' > ~/.bash_profile

# 上記を適用
$ source ~/.bash_profile
```

### 2. rubyインストール

```
# rubyのバージョン一覧確認
$ rbenv install -l

# rubyインストール
$ rbenv install 2.5.1

# 現在のディレクトリで利用するrubyバージョンを設定
$ echo '2.5.1' > .ruby-version
$ rbenv rehash
$ rbenv version
# => 2.5.1
$ ruby -v
# => 2.5.1
```

### 3. Railsインストール

```
$ rbenv exec gem install bundler '1.16.1'
$ rbenv exec gem install rails '5.2.0'
```

### 4. rails new でプロジェクトを作成

rails newで現在のディレクトリにrailsプロジェクトを作成します

```
$ pwd
# => ~/rails_blog
$ rails new .
# => 各種ファイル・ディレクトリが作成される

# 上記で作成されたGemfile内に記述されたgemをインストール
$ bundle install --path=vendor/bundle
# => ~/rails/blog/vendor/bundle内にgemがインストールされる
```

## ブログを作成

ブログを作成していきます。

[Railsを始めたばかりの人向け！Railsの仕組みを一から理解しながらブログを作成する](http://ruby-rails.hatenadiary.com/entry/20140813/1407915718)

`scaffold` コマンドという、モデル・ビュー・コントローラを一括で作成してくれるコマンドも存在しますが、今回は学習のために `generate` コマンドで進めます。
[覚えておくと超便利！Ruby on Railsのscaffoldの使い方【初心者向け】](https://techacademy.jp/magazine/7204)

