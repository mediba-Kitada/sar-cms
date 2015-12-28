sar-cms
====

CMS for SAR with Yii2

## Install

### 初期構築

#### Ruby及びgem導入

- Rubyのインストール

    ```bash
    $ rbenv install 2.1.5
    $ rbenv local 2.1.5
    ```

- gemのインストール

    ```bash
    $ rbenv exec gem install bundle
    $ rbenv exec bundle init
    $ vi Gemfile
    $ rbenv exec bundle install --path ./vendor
    ```

#### chef及びTest Kitchenの導入

- [opsworks_cookbooks](https://github.com/aws/opsworks-cookbooks)を拡張する

    ```bash
    $ mkdir -p ./opsworks-cookbooks
    ```

- CMS用cookbookの作成

    ```bash
    $ cd ./opsworks-cookbooks
    $ chef generate cookbook cms.sar.mediba.jp
    ```

- [Test Kitchen](http://kitchen.ci/)の導入

    ```bash
    $ kitchen init --driver=kitchen-vagrant
    ```

#### yii2導入

- bower及びnpmの依存性をcomposerで解決

    ```bash
    $ composer global require "fxp/composer-asset-plugin:~1.1.1"
    ```

- yii2をアプリケーションディレクトリにインストール

    ```bash
    $ composer create-project --prefer-dist yiisoft/yii2-app-basic cms.sar.mediba.jp 
    ```
