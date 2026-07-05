# CLAUDE.md — サロンリール（SALON REEL）プロジェクト

美容サロン（ネイル・エステ・アイラッシュ・非医療）向けAI動画制作DFY事業。事業計画はSPEC.md（§0〜14）を必ず最初に読むこと。
最終更新: 2026-07-05

## 現状サマリー

- **フェーズ**: Phase1（実績客3〜5件の獲得）。集客はInstagram Reels主軸のSNS投稿（アウトバウンドDM・人脈・広告は使わない。SPEC §9・§11＝2026-07-05改訂）
- **Higgsfield**: Plus月払い加入済み（アカウント: hirstjuice1669）。商用利用可の確認記録済み（2026-07-05・SPEC §12ゲート完了）。MCP接続済み（OAuth認証済・generate_video等が直接使用可）
- **クレジット**: 残高822cr／7月消化32%（Ultra移行トリガー非該当）。詳細は docs/実効原価ログ.md
- **LP**: https://salon-reel.pages.dev にデプロイ済み（**noindex＝限定公開中**）。GitHub `Kimagure3737/salon-reel` main→Cloudflare Pages自動デプロイ

## 完了済みの主要成果物

| 領域 | 成果物 |
|------|--------|
| コンプラ | docs/表現ガイド.md v1.1（qa-criticレビュー高4・中12反映済み。**弁護士監修は未実施**＝「監修済み」と絶対に言わない。附録に監修時確認11論点） |
| 制作実績 | トライアル3本（エステ/ネイル/アイラッシュ）＋音楽動画1本＋SNS用6本。素材フォルダに保存（gitからは除外） |
| 制作知見 | docs/プロンプト知見集.md（標準設定・モデル使い分け・NG仕様） |
| SNS | docs/SNS戦略リサーチ.md（②AI公開型70%＋①改30%のハイブリッド確定）／アカウント設計／投稿テンプレ3型／数値管理シート／Week1_投稿原稿（6本分・動画生成済み） |
| LP | src/lp/（設計: docs/LP_設計書.md、compliance一次チェック済み・高中4件反映済み） |

## 生成の標準設定【確定・必ず適用】

- **Kling 3.0**: sound off・std・5秒・9:16 ＝ **7.5cr**（静物マクロ向き）
- **Seedance 2.0**: std・720p・5秒・generate_audio:false・9:16 ＝ **22.5cr**（空間・インテリア向き。**Klingは空間系で煙が出る**）
- steam / vapor / mist はプロンプトに入れない＋ネガティブへ（確定NG仕様）
- フロー: `get_cost:true`でプリフライト→生成→`transactions`で実消費確認→実効原価ログに記録（自己申告値を信じない。過去に誤報告あり）

## コンプラ絶対ルール（表現ガイドv1.1）

- 全投稿・全生成物にAI表示（「AIにより生成されたイメージです」）
- ビフォーアフター構図は実写・AIとも全面禁止／AI人物を客・スタッフとして見せない／アイラッシュのAI目元アップ禁止
- 「制作費0円」「必ず」「No.1」等の絶対表現禁止。根拠ある相対表現のみ
- BGMはInstagramアプリ内ライブラリから選曲（Suno等AI生成曲は不使用）
- 薬機法は「何人も」規制＝当社自身が摘発対象になりうる（顧客保護でなく自己防衛）

## 運用ルーチン

- **docs/ 更新後はrcloneでDrive同期**: `"C:\Users\tanaka\AppData\Local\Microsoft\WinGet\Packages\Rclone.Rclone_Microsoft.Winget.Source_8wekyb3d8bbwe\rclone-v1.74.3-windows-amd64\rclone.exe" copy docs gdrive:higgsfield/docs --include "*.md"`
- **LP変更**: 編集→commit→push（Cloudflare Pagesが自動再デプロイ）
- **毎週月曜**: BGMリサーチ（IG急上昇→TikTok→Spotifyバイラル日本版）→数値管理シートのBGM列に記録
- ffmpegはimageio-ffmpeg同梱の静的バイナリを使用（システム未インストール）。Demucs導入済み（GPU可）
- 素材/ フォルダはgit管理外（.gitignore。大容量WAV・ライセンス考慮）

## 未完了タスク（優先順）

1. **Week1投稿の実行**（7/6月〜7/11土・各日18〜20時。docs/Week1_投稿原稿.md 参照。B型は工程カード＋動画の結合編集が必要）＋投稿48時間後の数値記録
2. **LP公開ブロッカー2件**: 運営者情報（src/lp/index.html 500〜502行目）・Instagramユーザー名（CTAリンク2箇所 `__YOUR_ACCOUNT__`）→反映後に実機最終確認（docs/LP_公開前チェックリスト.md）
3. **料金確定**: トライアルの人時データ（未回収）→原価計算→料金反映→noindex削除で本公開＋料金セクションのみcompliance再確認
4. **DM見積り基準の作成**（料金質問への返信テンプレ。公開運用の前提）
5. **弁護士監修の手配**（表現ガイドv1.1＋附録の11論点。予算¥50,000〜300,000（推定）＝SPEC §8計上済み）
6. 未回収データ: Plus月額実額（$）／トライアル各本の人時（実効原価ログの（要記入）欄）
7. HTML10行目の古いOGPコメント掃除（次のLP編集時に）

## 撤退ライン（SNS・数値管理シート参照）

30日: 平均再生500未満＋保存率1%未満→フォーマット改訂／90日: 問い合わせ3件未満→DM併用へ回帰／180日: 成約1件未満→SNSを補助チャネルへ
