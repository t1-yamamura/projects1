## プロジェクトの目次
プロジェクトの一覧です。詳しくはリンク先をご覧ください。

**1. 因果探索の気象現象の分析への応用**

[causal_discovery_meteo] (<a href="https://github.com/t1-yamamura/causal_discovery_meteo" target="_blank" rel="noopener noreferrer">
https://github.com/t1-yamamura/causal_discovery_meteo
</a>)

**[Python/convLSTM/PINN]** MSMの数値データから気象現象の因果律をAIモデルで学習し、特定の気象イベントのトリガーの探索を試みています。詳しくはリンク先をご参照ください。

**2. LSTや日射量の計算のための雲マスクの作成**

[cloudmask_meteo] (https://github.com/t1-yamamura/cloudmask_meteo)

**[Python/ひまわり/K-means/OpenCV]** 衛星ひまわりのデータに対し、画像処理と機械学習を組み合わせて雲マスク生成を試みています（LST/日射量計算の前処理）。詳しくはリンク先をご参照ください。

**3. 大船渡林野火災の分析**

(https://public.tableau.com/app/profile/t.yamamura/vizzes)

**[QGIS/Tableau/Sentinel-2/オリジナルインデックス]** 林床の含水量ではなく森林の乾燥度から林野火災のリスクを見積もっています。NDWIにかわるオリジナルインデックスを用いています。

**4. AWSを用いた天気図等の配信API**

(https://bqvtbhq7po2cfhdnfmu7bflbzq0pcvga.lambda-url.ap-northeast-1.on.aws/weather-map)

**[AWS/FastAPI/Docker]** 気象庁が公開している天気図画像（SPAS_COLOR）を取得し(存在する最新の時刻のファイルを探索)、FastAPI経由でHTMLページとして配信（出典：気象庁を明記）しています。アプリケーションはDockerコンテナ化し、AWS ECRにイメージをpushした後、そのイメージをベースにAWS Lambda（コンテナイメージ対応）としてデプロイしています。Lambda Function URLから直接APIを公開しています。

今後やりたい拡張（現在勉強中）ひまわりの雲画像を別のLambdaとS3で定期取得し、API側で「最新の天気図+雲画像」を重ね合わせて配信する処理
