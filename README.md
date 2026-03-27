# PenaUtilityTool（ver1.0.7）
『ペナントシミュレーション3』のセーブデータを外部から自由自在に編集し、理想の球界を作り上げるためのデスクトップアプリです。<br>
**注意： 本ツールの逆コンパイル・改変・再配布などは禁止です。**

# このツールでできること
「ゲーム本体だけでは時間がかかる作業」や「あったら嬉しい拡張機能」を凝縮しています。<br>
- AIで分析<br>
<img width="582" height="365" alt="image" src="https://github.com/user-attachments/assets/355448b3-d10a-42a1-b8b5-cf9d12756dbc" /> <br>
- ブックメーカで勝利予想
<img width="226" height="500" alt="HELbJ08aMAAic5h" src="https://github.com/user-attachments/assets/442d7bdf-6dae-406f-9a18-db9591aa252e" />
<img width="226" height="500" alt="HELbLrha0AA7WbX" src="https://github.com/user-attachments/assets/877bca23-a309-4b88-ae0a-ab0f118e8790" />

- 他にも色々な機能あり

<img width="326" height="600" alt="スクリーンショット 2026-03-27 193128" src="https://github.com/user-attachments/assets/166bb87d-488b-4953-a77f-3eb9d4b93f05" />



# 目次
- [導入方法](#導入方法)
- [フォルダ構成のイメージ](#フォルダ構成のイメージ)
- [機能紹介](#機能紹介)
- [1. 助っ人調整](#1-助っ人調整)
- [2. 引退選手削除](#2-引退選手削除)
- [3. 選手紹介出力](#3-選手紹介出力)
- [4. 選手ID検索](#4-選手id検索)
- [5. 能力確認](#5-能力確認)
- [6. CSV作成](#6-csv作成)
- [7. 引退選手復活](#7-引退選手復活)
- [8. コメントあり選手一覧](#8-コメントあり選手一覧)
- [9. 装備設定](#9-装備設定)
- [10. 装備一覧](#10-装備一覧)
- [11. 装備ガチャ](#11-装備ガチャ)
- [12. 再建モード](#12-再建モード)
- [13. 監督ビルダー](#13-監督ビルダー)
- [14. SOUGOU再計算](#14-sougou再計算)
- [15. ブックメーカー](#15-ブックメーカー)
- [16. 収支グラフ](#16-収支グラフ)
- [17. 装備メンテナンス](#17-装備メンテナンス)
- [補足: 装備データ運用（system / user）](#補足-装備データ運用system--user)

# 導入方法
1. **[Releases](https://github.com/Munchi369/PenaUlitilyTool/releases) から最新の `PenaUtilityToolzip.zip` をダウンロードします。**
2. ダウンロードした ZIP ファイルを解凍します。
3. 解凍して出てきた`PenaUtilityTool`フォルダを、**「penanto3」フォルダがある階層**へコピーしてください。
```text
ペナントシミュレーションのフォルダ/
├── penanto3/             <-- セーブデータフォルダ
├── ペナントシミュレーション.exe
└── PenaUtilityTool       <-- 【本ツール】ここに追加！
```
※ペナントシミュレーションの本体は、がらくた様のホームページよりダウンロードください。
**[がらくたのペナントシミュレーション](http://garakutapsg.web.fc2.com/)**


# 機能ガイド

## 1. 助っ人調整
- 条件（リーグ・投手/野手など）を指定し、能力を一括増減。
- 能力を派手にいじると本体が進行できなくなったりするので気をつけて。

## 2. 引退選手削除
- 現在は保留中の機能です。

## 3. 選手紹介出力
- 選手IDを指定して選手情報の Markdown ファイルを作成できます。
- 出力先は `doc/` フォルダです（`doc/選手名.md`）。

## 4. 選手ID検索
- 選手名からID・ポジション・状態を検索できます。

## 5. 能力確認
- 選手の能力を表示できます。

## 6. CSV作成
- 対象年度を選んで成績CSVを出力できます。
- 出力先は `doc/` フォルダです（`doc/XXXX年_成績.csv`）。
- Geminiのカスタマイズ機能（Gem）を利用して、CSVデータからチームの戦力分析を行うAIを作成しました。
  - UtilityToolで作成したCSVファイルを添付するだけで分析可能です
  - **[ペナントアナライザー](https://gemini.google.com/gem/1xP2v2rdmKMHDbgBi32vhxhaXjpyG7ixg?usp=sharing)**
  - 利用にはGoogleアカウントが必要です。使用してもチャットの内容は私には見えませんのでご安心を。

## 7. 引退選手復活
- 引退選手を指定して復活できます。

## 8. コメントあり選手一覧
- コメント（outline）が登録されている選手だけを一覧表示できます。

## 9. 装備設定
- 選手を読み込んで、装備の変更・解除ができます。

## 10. 装備一覧
- 装備名・レア度・所持数・効果・コメント・現在の装備者を一覧表示できます。

## 11. 装備ガチャ
- 所持金を使って装備ガチャを回せます（1回10000）
- 装備に応じて能力が変化します。
- レア度：コモン・レア・エピック・レジェンダリー

## 12. 再建モード
- 1年目86日目、かつ所持金0以上のセーブに対して、100億円の借金状態を設定できます。縛りプレイにどうぞ。
- 能力低下を使う場合は、投手・野手それぞれの総合値しきい値を指定して対象候補を事前確認できます。
- 弱体化量は `軽め / 標準 / 厳しめ` のプリセットから選べます。

## 13. 監督ビルダー
- 監督データの新規作成を、基本情報・能力・プロフィールをまとめて入力して実行できます。
- 作成前にプレビューで、監督タイプ、起用法、打順傾向、詳細プロフィール、就任設定を確認できます。
- `候補一覧に出す` を有効にすると、監督候補一覧に表示される監督として登録します。
- `作成後にチームへ就任させる` を有効にすると、選択したチームの現年度 `1軍 / 2軍` の両方へ自動反映します。

## 14. SOUGOU再計算
- 現役選手を対象に、本体準拠の計算式で`総合`を再計算できます。
- squirrelで選手の能力を修正した時、他のテーブル間の同期取りなどに使用ください。

## 15. ブックメーカー
- リーグ開始前にペナントレースの結果に対して賭けを設定できます。
- リーグごとに予想タイプ、対象チーム、掛け金を入力して保存できます。
- 最終日に払戻可能な日になり、結果確定と払戻処理を実行できます。
- 保存済みの予想内容、オッズ、的中状況、払戻金を画面で確認できます。

## 16. 収支グラフ
- ブックメーカーの利益・損失・収支を年度ごとに確認できます。
- `直近5年 / 直近10年 / 全期間` のプリセットで表示範囲を切り替えできます。
- グラフはドラッグで表示年度を移動し、ホイールやスライダーで表示幅を調整できます。
- `戦績レポート` 出力ボタンから、`doc/` フォルダにブックメーカー収支レポートを作成できます。

## 17. 装備メンテナンス
- 障害復旧用のメンテナンス機能です。
- system装備の有効/無効切替、全解除、装備関連テーブル全削除（DROP・再作成なし）、テーブル再構築などを実行できます。
- メニュー画面で `Ctrl + Shift + E` から開けます。

### どんなときに使うか
- 通常運用では不要です。装備まわりで問題が出たときだけ使ってください。
- `system装備を対象外化`: user装備だけで運用したいとき、またはsystem装備を一時的に一覧/ガチャから外したいとき。
- `system装備を再有効化`: 対象外化したsystem装備を元に戻したいとき。
- `装備全解除`: 装備効果を全選手から外して、装備状態だけリセットしたいとき。
- `全解除 + インベントリ全0`: 検証前に装備所持状況も含めて初期化したいとき。
- `装備関連テーブル全削除（DROP）`: 装備効果を全選手から外したうえで、装備関連テーブルをDROPしてツール利用前に近い状態へ戻したいとき。
- `装備テーブル完全再構築`: 装備テーブル不整合や深刻なエラー時の最終手段です。
- 実行前は `penanto3` フォルダのバックアップを推奨します。

# 補足: 装備データ運用（system / user）
ここから下は自分で装備を追加したい人用。

装備は次の3テーブルで管理されています。

- `EQUIPMENT_MASTER`: 装備マスタ（名前、レア度、効果、表示設定など）。装備設定/装備一覧を開いた時、または装備ガチャ実行時に自動作成・補完されます。
- `EQUIPMENT_INVENTORY`: 所持数
- `EQUIPMENT_DATA`: 誰が何を装備しているか

`EQUIPMENT_MASTER.SOURCE` は装備の種類を表します。

- `system`: ツール標準装備
- `user`: ユーザー追加装備

### アップデート時の挙動
- ツールは装備設定/装備一覧を開いた時、または装備ガチャを実行した時に `system` 装備定義を同期します。
- 同期で更新されるのは `SOURCE='system'` の行だけです。
- `SOURCE='user'` の行は、ツール更新で更新・削除されません。
- `EQUIPMENT_KEY` は主キーです。`user` 装備は `system` とキー重複しない名前にしてください（例: `user_...`）。

### `IS_HIDDEN` と `IS_GACHA_ENABLED` の意味
- `IS_HIDDEN=false`: 装備一覧・装備設定に表示され、装備候補になります。
- `IS_HIDDEN=true`: 装備一覧・装備設定・ガチャ対象から除外されます。
- `IS_GACHA_ENABLED=true`: ガチャ抽選対象になります（ただし `IS_HIDDEN=false` の場合のみ）。
- `IS_GACHA_ENABLED=false`: ガチャ抽選対象外になります（表示・装備可否は `IS_HIDDEN` に依存）。
- すでに装備中の装備を `IS_HIDDEN=true` にしても、自動解除はされません。

### オリジナル装備（user装備）を追加する手順
1. `EQUIPMENT_MASTER` に `SOURCE='user'` で登録  
2. `EQUIPMENT_INVENTORY` に所持数を登録（0だと装備候補に出ません）

```sql
-- 1) user装備を追加
INSERT INTO EQUIPMENT_MASTER (
  EQUIPMENT_KEY, EQUIPMENT_NAME, RARITY, MODIFIERS, COMMENT_TEXT,
  SOURCE, IS_HIDDEN, IS_GACHA_ENABLED
) VALUES (
  'user_sample_bat',
  'サンプルバット',
  'RARE',
  'POWER:3,KOUDA:2',
  'ユーザー追加のテスト装備',
  'user',
  FALSE,
  TRUE
);

-- 2) 所持数を付与（例: 1個）
INSERT INTO EQUIPMENT_INVENTORY (EQUIPMENT_KEY, OWNED_COUNT)
VALUES ('user_sample_bat', 1);
```

※ `EQUIPMENT_INVENTORY` はアプリ側で自動補完されるため、すでに行がある場合は `INSERT` ではなく `UPDATE` を使ってください。

```sql
UPDATE EQUIPMENT_INVENTORY
SET OWNED_COUNT = 1
WHERE EQUIPMENT_KEY = 'user_sample_bat';
```

補足:
- `RARITY` は `COMMON / RARE / EPIC / LEGENDARY` を推奨します。
- `MODIFIERS` は `能力コード:数値` をカンマ区切りで指定します。
  例: `SEIKYUU:2,SUTAMINA:-1`
- 主な能力コード: `HEN, MAXMAX, SEIKYUU, SUTAMINA, KAIHUKU, SEISIN, QUICK, KOUDA, POWER, SOURYOKU, KENRYOKU, HOKYUU, SOUKYUU, SENKYUU, KOWAZA, TAIRYOKU, RIDO, TOURUIGIJUTU`

### 既存装備の表示/ガチャ切替（例）
```sql
-- 非表示（装備候補・一覧・ガチャから外す）
UPDATE EQUIPMENT_MASTER
SET IS_HIDDEN = TRUE
WHERE EQUIPMENT_KEY = 'user_sample_bat';

-- 表示に戻し、ガチャ対象にする
UPDATE EQUIPMENT_MASTER
SET IS_HIDDEN = FALSE, IS_GACHA_ENABLED = TRUE
WHERE EQUIPMENT_KEY = 'user_sample_bat';

-- 表示はするがガチャ対象から外す
UPDATE EQUIPMENT_MASTER
SET IS_GACHA_ENABLED = FALSE
WHERE EQUIPMENT_KEY = 'user_sample_bat';
```


