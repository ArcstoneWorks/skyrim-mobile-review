# Skyrim 音声レビュー iPhone試験版 v0.1.0

状態: **CANDIDATE / 正式採用前**。本リポジトリに音声・台詞・判定CSVは保存しません。

## iPhoneで使う準備
1. リポジトリの **Settings → Pages** を開く。
2. **Build and deployment → Source: Deploy from a branch** を選ぶ。
3. Branchを **main**、フォルダを **/(root)** に設定して **Save**。
4. 公開後、Safariで `https://arcstoneworks.github.io/skyrim-mobile-review/` を開く。
5. Google Drive上の既存レビューZIPをiPhoneの「ファイル」アプリにダウンロードする。
6. 画面の **レビューZIPを選択** からZIPを選んでレビューする。
7. 判定結果を必ずCSV書き出しし、「ファイル」アプリ経由でDriveに保存する。

## 注意
- 公開サイトはレビュー起動用HTML/JavaScriptのみ。ユーザー指定ZIPはブラウザ内で処理し、GitHubにアップロードしない。
- 正式共通Review Tool v0.1.5 READMEFIXの派生起動ツール。正本のロジック、既存採用判定、Frozen、Raw、Productionは変更しない。
- **iPhone Safari実機での自動再生・CSV保存・大容量ZIP動作は未検証**。
- ZIPを開いたら画面に結果が残っていても、作業終了時は必ずCSVを保存する。Google Driveへの自動同期は未実装。
- 複数PJのZIPや未検証の形式のZIPでの動作は保証していない。
- 第三者が作成した不明なZIPは読み込まないこと。ZIP内のレビューJavaScriptを実行するため、信頼できるレビューZIPに限定する。
- JSZip v3.10.1 のライセンスは [JSZIP_LICENSE.markdown](JSZIP_LICENSE.markdown) に収録。

## 正本との区分
Google Drive: Skyrim_AI/00_音声制作_共通管理/02_TOOLS_LOCKED_AND_CANDIDATES

本リポジトリはモバイル起動試験用。正式共通ツールへの昇格は行わない。

## v0.1.1 — CSV判定空レコード復元（2026-10-14）
- iPhone試験版の起動HTMLだけを変更。ZIP内の共通LOCKED Review Toolとその音声・既存CSVは変更しません。
- CSVの有効な判定があり、ブラウザ側には未判定のレコードしかない場合に限り復元を許可します。
- 既存の採用／不採用／保留など判定済みレコードを保護し、既存の個別メモ・場面・reuseの情報を残します。
- 元のcsv_restore.jsと一致しない構造を検出した場合、安全側で起動を止めます。
- Node.js実コード検証 PASS（10項目）、Chromium統合試験は環境のローカルページ通信遮断によりNOT_RUN。iPhone実機v0.1.1は再検証待ち。
- 保存済みCSVのバックアップを維持してから、通常SafariでレビューZIPを選択し、保留1 CSVを読み込み、「CSV復元1件／保留1件」を確認します。

## v0.1.3 — iPhone画面の主要操作を上部1画面へ集約（2026-10-15）
- **主操作**：進捗、前/次、連続再生/停止、自動進行/自動採用、判定一覧、字幕、加工後WAV再生、判定6種、メモを最初の画面に配置。
- **ファイル欄は下部**：最初の画面の「↓ ファイル・詳細（CSV保存／読込）」から、CSV保存/読込・ZIP変更・比較用Raw MP3・末尾/TTS・場面/reuse情報にアクセス可能。元のボタンやDOMを移動するだけで、ファイル読込・判定・CSV実装は変更しない。
- 既存CSV復元v0.1.1限定修正はバイト同一。共通LOCKED正本・音声・既存判定CSVは無改変。
- Chromium 390×844 / 390×667 / 375×600レイアウト、Lydia50 ZIP、判定、36列CSV書出、空レコードからCSV保留1復元、下部移動/戻る、ZIP変更：PASS。ページ試験ではモックlocalStorageを使用。iPhone Safari v0.1.3実機：NOT_RUN。
- Google Driveの候補保管先：`Skyrim_AI/00_音声制作_共通管理/02_TOOLS_LOCKED_AND_CANDIDATES/Skyrim_Mobile_Review_iPhone_CANDIDATE_v0.1.3_20261015.zip`。

## v0.1.5 — V4中心・TTS入力常時表示と不良理由メニュー（2026-10-15）
- v0.1.4候補の変更を含む：メイン画面で実際のTTS入力を常時表示し、「加工後採用」ボタンは「採用」と簡潔に表示。旧方式「末尾加工不良」は下部の詳細欄に移し、既存の判定値とCSV列順は変更しない。
- v0.1.5：iPhoneレビュー画面に「不良理由」のプルダウンを追加（誤読／発音／アクセント・抑揚／演技・感情／声質・生成ブレ／速度・間／無音・欠損／ノイズ／その他）。複数の理由を繰り返し選べ、既存メモ欄へ `【TTS不良：理由】` を追記。同じ理由は重複しない。
- **理由だけを選んでも不良判定にしない**。元の「TTS不良・再生成」ボタンで判定する。理由は元の `note` 変更保存処理に乗せ、従来のCSVの `note` 列に格納。自由記述と既存判定を保護。
- Chromium（モックlocalStorage）でLydia50 ZIPを使った390×844、390×667、375×600の試験PASS：理由の選択／重複なし／自由記述保護／TTS不良判定／移動後の保持／36列CSV50件出力／別セッションCSV復元1件。正式LOCKED Review Tool・原本ZIP・既存CSVの変更なし。iPhone Safari v0.1.5実機は未確認。
- Drive候補：`Skyrim_AI/00_音声制作_共通管理/02_TOOLS_LOCKED_AND_CANDIDATES/Skyrim_Mobile_Review_iPhone_CANDIDATE_v0.1.5_20261015.zip`。既存レビューCSVは上書きせずバックアップを維持すること。
