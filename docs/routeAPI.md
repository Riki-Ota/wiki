# Route APIの開発

## 達成目標
- AWSの簡易設計
- API化とサービスへの組み込み
- Google Map APIとの比較・検証

## 予定フロー
1. OSMの調査
1. OSRMの実装
1. OSRMの検証
1. 改善提案・検証
1. まとめ・発表

## OSMの調査
- ザクっと調査して一応完了
- 内容はOSM周辺のサービス調査とOSRMのドキュメント読み込み
- 競合APIの調査やAPI使用頻度見積など今後アップデートする必要あり

- [資料](https://docs.google.com/presentation/d/1pzrAYqSIeWX3as0jGGMnKuD_irQcHfbkumQ2E5qgwD4/edit#slide=id.g783aacf507_0_414)

## OSMの実装
### 参考
- [Gitのページ]()
- [詳しいまとめ]()

パッケージインストール
```
sudo apt install build-essential git cmake pkg-config \
libbz2-dev libxml2-dev libzip-dev libboost-all-dev \
lua5.2 liblua5.2-dev libtbb-dev
```
git clone
```
mkdir ~/osrm
cd osrm
git clone https://github.com/Project-OSRM/osrm-backend.git
```
build
```
mkdir -p build
cd build
cmake ..
cmake --build .
sudo cmake --build . --target install
```
地図データDL
```
mkdir ~/osm/kanto
cd ~/osm/kanto
wget http://download.geofabrik.de/asia/japan/kanto-latest.osm.pbf
```
地図データ準備&Run (Default port 5000)
```
osrm-extract   ../osm/kanto/kanto-latest.osm.pbf
osrm-partition ../osm/kanto/kanto-latest.osrm
osrm-customize ../osm/kanto/kanto-latest.osrm
osrm-routed --algorithm mld ../osm/kanto/kanto-latest.osrm
```

動くかテスト
ソフトバンク本社 35.663176 139.761180
ラーメン二郎 三田本店 35.648121 139.741633
```
curl 'http://3.112.58.43:5000/route/v1/driving/139.761180,35.663176;139.741633,35.648121?geometries=geojson'|jq 'def hexdec(i): "0123456789abcdef"[i:i+1]; {"type": "FeatureCollection", "features": [[.routes[].geometry] | [., keys] | transpose[] | {"geometry": .[0], "type": "Feature", "properties": {"stroke-width": 2, "stroke": ("#" + hexdec(15-.[1]*2) + hexdec(.[1]*2) + hexdec(.[1]*2))}}]}' > routes_jiro.json
```

出てきたjsonファイルを[ココ](http://geojson.io/)で可視化

### 詰まったところメモ
- ポートは5000がデフォルト
- Ubuntu側でもFWを設定できる(しなくてもよい)
'''
sudo systemctl start ufw
sudo systemctl is-active ufw
sudo ufw enable
sudo ufw add 5000
sudo ufw status
'''
- WindowsだとJSON文字化け
    - UTF-8へのフォーマット変更必要 `chcp 65001`
    - [参考](https://qiita.com/yamachan360/items/8c928738289cd518eec8)

## テスト

