# Chapter-104-

Chapter 104: 連続エントリーモデルの構造化

プロンプト

Prompt: How can an automated trading bot manage multiple entries independently and ethically while preserving its state?

既定コンテキス:
	•	SMAクロスBot (永続性あり)が一度のポジションのみを負担
	•	M15尺度での動作を実現
	•	リスクマネジメントはこのBotの主題

⸻

1. 連続エントリーに必要な「状態管理」の負担

自動売買Botにおける「状態」とは？
	•	「いつ」どのような条件で「エントリーしたか」のログ
	•	各ポジションの別ID化（跡継ぎも可）
	•	別々の判断結果を状態ファイル (e.g. positions.json) に記録

例: positions.json の中身

{
  "entries": [
    {
      "id": "entry_20250617_001",
      "timestamp": "2025-06-17T03:15:00",
      "price": 50200.0,
      "tp": 51000.0,
      "sl": 49900.0,
      "active": true
    },
    ...
  ]
}


⸻

2. 再エントリーの許可条件
	•	最新クロスが前回のエントリーよりも “x bar”越している
	•	それにより “wave structure” の中の別の波と判断される
	•	これにより 3波 / 5波 の別々の内定に対応

⸻

3. エントリーロジック
	•	相対的に簡単:
	•	SMAクロスでシグナル発生
	•	positions.json に新しいエントリー情報を追加
	•	各エントリーを独立に判断、TP/SL 設定

⸻

4. 理想のBotに向けた展望
	•	SMAや時間軸によらない 波動の認識力と階層性
	•	多重入場の発生部位を 非同期に認識
	•	後のChapter105では「フィルター階層」の投入により 意思性の投影を実装

⸻

結論

「複数回エントリー」は、単なる自動売買を超えて、Botが態度と記憶をもって別々の動作を繰り返すための最初の手立てである。

⸻

次のChapter105では「エントリー前の予防主义」として、別のインディケータ (例: RSI, MACD, Volatility)を投入するフィルター階層の設計に進みます。
