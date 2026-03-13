# このツールでできること（ver1.06）

このツールは、選手データ管理・能力調整・装備管理をまとめて行えるデスクトップアプリです。  
主な機能は以下のとおりです。

## 1. 能力調整
- 条件を指定して、対象選手の能力を一括で増減できます。
- 日本人/助っ人、リーグ、投手/野手の条件指定に対応しています。
- 実行前にプレビューで件数や変更内容を確認できます。
- 条件プリセットの保存・適用・削除ができます。

## 2. 引退した選手削除
- 現在は保留中の機能です。

## 3. 選手名鑑（Markdown出力）
- 選手IDを指定して選手情報の Markdown ファイルを作成できます。
- お気に入り選手を選んでID入力欄へ反映できます。
- 出力先は `doc/` フォルダです（`doc/選手名.md`）。

## 4. 名前検索
- 選手名からID・ポジション・状態を検索できます。
- 検索結果からお気に入り登録/解除ができます。

## 5. 能力確認
- 選手IDで能力値を表示できます（投手/野手で表示内容を切替）。
- お気に入り選手を選んでID入力欄へ反映できます。
- 表示中の選手をお気に入り登録/解除できます。

## 6. CSV作成
- 対象年度を選んで成績CSVを出力できます。
- 出力先は `doc/` フォルダです（`doc/XXXX年_成績.csv`）。

## 7. 過去選手復活
- 引退選手を指定して復活できます。
- 復活前に年齢・所属先チームの条件でプレビュー確認ができます。
- お気に入り選手を選んでID入力欄へ反映できます。

## 8. コメントあり選手一覧
- コメント（outline）が登録されている選手だけを一覧表示できます。
- 画面内でコメントの編集・更新ができます。

## 9. 装備設定
- 選手を読み込んで、装備の変更・解除ができます。
- 装備候補の絞り込み（名前/レア度）に対応しています。
- 装備変更による能力差分プレビューを確認できます。
- 読み込み状態が表示されます（未読込/読込済/再読込必要）。
- お気に入り選手を選んでID入力欄へ反映できます。

## 10. 装備一覧
- 装備名・レア度・所持数・効果・コメント・現在の装備者を一覧表示できます。
- レア度フィルタで絞り込みできます。

## 11. 装備ガチャ
- 所持金を使って装備ガチャを1回ずつ実行できます（1回10000）。
- ガチャ画面から所有装備一覧へ移動できます。

## 12. 装備データ運用（system / user）
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

## 13. 装備メンテナンス（運用者向け）
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

