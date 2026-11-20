# FocusTrain

鉄道で集中する、シングルファイルの集中タイマーアプリです。出発駅と到着駅を選ぶと、区間の距離から集中時間が決まります。乗車中は、線路に沿って列車が進みます。

- 関東の主要路線の駅データ入り（東武東上線・越生線、副都心線、有楽町線、東急東横線、みなとみらい線、JR山手線・中央線・京浜東北線・東海道線・横須賀線・横浜線ほか）
- 国土地理院の空中写真タイルの地図、進行方向が上の追従表示、車窓ビュー
- Suica風カード / オリジナルのFocusCard / きっぷの3種類から選べて、改札はタッチ・きっぷ投入のアニメーション
- 列車の種類(普通・快速・特急)、ホームで待つ→電車に乗る→車内で作業する演出、乗り換えの演出
- 実際の線路データ(OpenStreetMap)に沿って列車が走る(乗車前にOverpass APIから取得。取得できない区間は直線)
- 履歴・トレンド（端末内に保存）
- ベントグリッド × グラスモーフィズムのデザイン

## ファイル構成

```
public/index.html          アプリ本体(HTML/CSS/JS すべて入り)
.github/workflows/pages.yml  GitHub Pages への自動公開
firebase.json              Firebase Hosting の設定
```

## ローカルで開く

`public/index.html` をブラウザで直接開くか、次のコマンドで起動します。

```sh
cd public && python3 -m http.server 8000
# http://localhost:8000
```

## GitHub に載せる

```sh
git init -b main
git add .
git commit -m "FocusTrain 初回コミット"
git remote add origin https://github.com/<ユーザー名>/focus-train.git
git push -u origin main
```

`gh` コマンドを使う場合は、`gh repo create focus-train --public --source=. --push` でも作成できます。

## GitHub Pages で公開する

1. リポジトリの **Settings → Pages** を開く
2. **Source** を **GitHub Actions** にする
3. `main` に push すると、自動で公開されます（URL: `https://<ユーザー名>.github.io/focus-train/`）

## Firebase Hosting で公開する

```sh
npm i -g firebase-tools
firebase login
firebase init hosting   # public ディレクトリは "public"、SPA は "No"
firebase deploy
```

## 出典・注意

- 線路の形状: © OpenStreetMap contributors（Overpass API、ODbL）
- 地図: 国土地理院（シームレス空中写真・標準地図・淡色地図）、OpenStreetMap contributors、CARTO
- 駅の緯度経度は概算です。乗車時は、OpenStreetMapの駅の位置で補正します
- 初回の乗車前に、線路データを取得するため数秒〜数十秒かかります。Overpass APIが混雑していると失敗することがあります
- Suica風のカードは、このアプリ用の簡易な描き起こしです。「Suica」の名称・ロゴ・ペンギンはJR東日本の商標・キャラクターです。公開する場合は名称やデザインにご注意ください（`index.html` 内の `CARD` で名称を変更できます）
