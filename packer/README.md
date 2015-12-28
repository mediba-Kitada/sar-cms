Packer for SAR
====

[Packer](https://www.packer.io)の活用方法について記載

## Description

### Packer

>Packerは、複数の仮想化環境・クラウド環境に対応した仮想マシン・イメージを作成、起動するためのツールです。それぞれの環境に合わせてマシン・イメージを迅速に自動生成するため、複数の環境に対応したイメージを用意する手間が省けます。AWSのAMI（マシン・イメージ）だけでなく、VMwareやOracle VM VirtualBoxの形式にも対応しています。

* [コード化でDevOpsを支えるHashiCorpのツールと開発背景](https://thinkit.co.jp/story/2015/03/05/5671)

### Atlas

>Atlasというプラットフォームを使うことにより、誰がどのようなイメージを管理しているか、インフラに対してどのような変更を行ったかなどを容易に確認できます。また変更時の記録（ログ）はAtlas上に一括して保管されるので、どこに記録を残すべきか迷うこともありません。

* [開発から運用に至るフローを一体化するAtlas](https://thinkit.co.jp/story/2015/10/01/6443)

## Usage

### テンプレートファイルの文法確認

```
[local]$ cd /path/to/sar-cms
# AtlasのAPIトークンを環境変数に代入  
[local]$ export ATLAS_TOKEN="hogefoobar"
# Packerによるvalidate
[local]$ packer validate -var 'atlas_token=${ATLAS_TOKEN}' -var 'version=`date +%Y%m%d`' packer-template.json
Template validated successfully.
```

### ローカルビルド

```
[local]$ cd /path/to/sar-cms
# AtlasのAPIトークンを環境変数に代入  
[local]$ export ATLAS_TOKEN="hogefoobar"
# Packerによるbuild
## boxファイルがカレントディレクトリにビルドされる
[local]$ packer build -var "atlas_token=${ATLAS_TOKEN}" -var "version=`date +%Y%m%d%h`" -only=virtualbox-iso,vagrant packer-template.json
# Vagrantによる仮想環境構築
[local]$ vagrant box add sar ./sar_centos-6-7-x64-virtualbox.box; vagrant up
```

### リモートビルド

```
[local]$ cd /path/to/sar-cms
# AtlasのAPIトークンを環境変数に代入  
[local]$ export ATLAS_TOKEN="hogefoobar"
# Packerによるpush
## boxファイルがビルドされる
[local]$ packer push -var "atlas_token=${ATLAS_TOKEN}" -var "version=`date +%Y%m%d`" packer-template.json
# Vagrantによる仮想環境構築
## Vagrantfileとboxファイルがダウンロードされ、仮想環境が構築される
[local]$ vagrant init mediba-kitada/sar; vagrant up --provider virtualbox
```

## Install

```
[local]$ PAKER_VERSION=0.8.6
[local]$ [! -d $HOME/packer ] && mkdir -p $HOME/packer && cd $HOME/Downloads && wget -O https://releases.hashicorp.com/packer/${PAKER_VERSION}/packer_${PAKER_VERSION}_darwin_amd64.zip && unzip packer_${PAKER_VERSION}_darwin_amd64.zip -d $HOME/packer && echo 'export PATH=$HOME/packer:$PATH' >> ~/.bashrc'
```

## Licence

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

## Author

[Tsubasa Kitada](https://github.com/mediba-kitada)
