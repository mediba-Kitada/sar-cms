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

#### chef及びopswokrs_cookbooksの導入

#### yii2導入

- bower及びnpmの依存性をcomposerで解決

    ```bash
    $ composer global require "fxp/composer-asset-plugin:~1.1.1"
    ```

- yii2をアプリケーションディレクトリにインストール

    ```bash
    $ composer create-project --prefer-dist yiisoft/yii2-app-basic cms.sar.mediba.jp 
    ```
