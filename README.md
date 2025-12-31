## プロジェクトの目次
プロジェクトの一覧です。詳しくはリンク先をご覧ください。

**1. 因果探索の気象現象の分析への応用**

[causal_discovery_meteo] (https://github.com/t1-yamamura/causal_discovery_meteo)

**[Python/convLSTM/PINN]** MSMの数値データから気象現象の因果律をAIモデルで学習し、特定の気象イベントのトリガーの探索を試みています。詳しくはリンク先をご参照ください。

**2. LSTや日射量の計算のための雲マスクの作成**

[cloudmask_meteo] (https://github.com/t1-yamamura/cloudmask_meteo)

**[Python/ひまわり/K-means/OpenCV]** 衛星ひまわりのデータに対し、画像処理と機械学習を組み合わせて雲マスク生成を試みています（LST/日射量計算の前処理）。詳しくはリンク先をご参照ください。

**3. 大船渡林野火災の分析**

(https://public.tableau.com/app/profile/t.yamamura/vizzes)

**[QGIS/Tableau/Sentinel-2/オリジナルインデックス]** 林床の含水量ではなく森林の乾燥度から林野火災のリスクを見積もっています。NDWIにかわるオリジナルインデックスを用いています。

**4. AWSを用いた天気図と気象衛星ひまわり（赤外画像・水蒸気画像）の重ね合わせ画像の配信API**

(https://uypig4uvv7itiq6ciexpfxtrzm0zpgmh.lambda-url.ap-northeast-1.on.aws/)

**[AWS/FastAPI/Docker]** 気象庁が公開している天気図画像（SPAS_COLOR）を取得し(存在する最新の日時のファイルを探索)、FastAPI経由でHTMLページとして配信しています。その際、天気図画像日時の気象衛星ひまわりの赤外画像・水蒸気画像を別のLambdaとS3で定期取得（EventBridgeを使用）し保存しておき配信時に天気図に重ね合わせる処理を行っています。アプリケーションはDockerコンテナ化し、AWS ECRにイメージをpushした後、そのイメージをベースにAWS Lambda（コンテナイメージ対応）としてデプロイしています。Lambda Function URLから直接APIを公開しています。

(1)EventBridgeで定期的にLambdaを起動し、気象庁から赤外画像・水蒸気画像を取得後に必要な加工（＊）を行った後、S3のバケットに日時ごとのプリフィックスの下に保存します。これらのオブジェクトは配信に不要となるようなタイミングでS3のライフサイクルで自動的に削除されていきます。

(2)Lambdaの関数URLから別のLambdaを起動し、気象庁から最新の日時の天気図を取得後にS3に保存しておいた画像と重ね合わせ処理等をした後、HTMLページ内に表示しています。このLambdaは合成画像を保存しないため起動するたびに同じ処理が行われます。

（＊）気象庁が公開している衛星画像は、あらかじめWebメルカトルに投影されたタイル画像として配信されているため、それらを縦横必要な枚数取得後に連結し、天気図の投影座標系（北緯60度、東経140 度を基準としたポーラーステレオ図法(https://www.data.jma.go.jp/suishin/shiyou/pdf/no12201) に変換し、天気図の表示範囲に対応させて切り取る加工
