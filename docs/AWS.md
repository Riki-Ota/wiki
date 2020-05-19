# AWSの使用法に関しての情報

## AWS初回ログイン時
1. MFA登録→有効化
1. スイッチロール

[アカウント参照](https://github.com/monet-technologies-com/infra-common-design/blob/master/docs/AWS%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E4%B8%80%E8%A6%A7.md)

## 使用限度目安
- 月$100以内程度の運用ならOK
- S3からのDLも費用かかることに注意
- EC2やRDSの常時ONは特に注意
- EC2切ったときはElastic IPの切断も忘れずに!

## 設計関連
- AWSロゴの素材は[ココ](https://aws.amazon.com/jp/architecture/icons/)から
