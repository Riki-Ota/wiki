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

## CLI設定
### 参考
- [初期設定①](https://qiita.com/reflet/items/e4225435fe692663b705)
- [初期設定②](https://qiita.com/n0bisuke/items/1ea245318283fa118f4a)
- [スイッチロールの設定](https://dev.classmethod.jp/articles/cli-switch-role/
)

defaultのユーザーを設定
アクセスキーは以前高須さんが送ってくれた
'''
aws config
'''
あとは打ち込んで設定

devやprodも`~/.aws/config`の中を変えて登録
プロファイルを確認
'''
aws sts get-caller-identity --profile dev
'''
