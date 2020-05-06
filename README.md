# nuxt_serverless

> Nuxt + Lambda template

## 概要
- Nuxt.jsをLambdaにデプロイするテンプレート
- `npm run deploy:xxx`でデプロイできる
- Lambda + S3 + API Gatewayまでを自動化しており，継続的にデプロイする場合はCloudFrontの手動設定が必要

## AWSの設定など
- 公式ドキュメントを参考にawscliをセットアップする
  - https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

## 各プロジェクト固有の設定
- serverless.ymlの設定を書き換える

```yaml
# 任意のサービス名を設定する
service: nuxt-serverless

provider:
  name: aws
  runtime: nodejs10.x
  stage: ${opt:stage, 'dev'}
  # 利用するリージョンを選択する
  region: ap-northeast-1

custom:
  # リソースの命名に利用するIDに適当な値を設定．上記URLにアクセスして取得した値でok
  stackId: cn7y8x
```

## デプロイ手順

```shell
# 関連パッケージのインストール
npm install

# プロジェクトのビルド
npm run build

# デプロイ
npm run deploy:prod
# or 
npm run deploy:stage
# or
npm run deploy:dev
```

## その他

`package.json`のdependenciesとdevDependenciesはLambda上で動かす都合上少し異なる
- dependencies
  - nuxt自身と@nuxtjsで始まるパッケージ
- devDependencies
  - その他パッケージ

## Build Setup

``` bash
# install dependencies
$ npm run install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
