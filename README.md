# RPSFG (Raw PES Stream File Generalization)

**日本語** | [English](README.en.md)

PES (Packetized Elementary Stream) ファイルを標準的なメディアファイル形式に変換するツールです。

## 概要

特定の録画機器で生成されたPESファイルは、一般的なメディアプレイヤーでは正常に再生できない場合があります。  
RPSFGは、これらのPESファイルからH.264ビデオストリームとA-LAW音声ストリームを抽出し、  
FFmpegを使用してMKVコンテナに変換します。

## 特徴

- **PES解析**: ISO/IEC 13818-1準拠のPESパケット境界検出
- **複数ストリーム対応**: H.264ビデオ + A-LAW音声の同時処理
- **ビデオオンリー対応**: 音声トラックがないファイルにも対応
- **ドラッグ&ドロップ**: 「送る」に登録等で複数ファイルの一括処理
- **UTF-8対応**: 日本語対応

## 技術仕様

### 対応形式

- **入力**: 生PESファイル (コンテナなしMPEG-PS相当)
- **ビデオ**: H.264 (ITU-T H.264/ISO 14496-10)
- **音声**: A-LAW PCM (ITU-T G.711 A-law, 8kHz モノラル)
- **出力**: MKV (Matroska Video)

## 必要環境

- .NET 8.0 Runtime
- FFmpeg (PATH環境変数に設定済み)

## ビルド方法

### 通常ビルド

```bash
dotnet build --configuration Release
```

### WSL環境用ビルド

```bash
dotnet build --configuration Debug-WSL
```

## 使用方法

### コマンドライン

```bash
# 単一ファイル処理
RPSFG.exe "input.pes"

# 複数ファイル処理
RPSFG.exe "file1.pes" "file2.pes" "file3.pes"
```

### ドラッグ&ドロップ

実行ファイルに直接PESファイルをドラッグ&ドロップして使用可能

## 出力ファイル

各PESファイルに対して以下のファイルが生成されます：

- `{filename}_complete.mkv` - 最終的なMKVファイル
- `{filename}_complete.h264` - 抽出されたH.264ストリーム（処理後削除）
- `{filename}_complete.alaw` - 抽出されたA-LAWストリーム（音声がある場合のみ、処理後削除）

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。  
詳細は[LICENSE.txt](LICENSE.txt)を参照してください。

## 免責事項

このツールは防御的セキュリティ目的での使用を想定しております。  
本ツールの使用によって生じた如何なる損害や被害についても、作者は一切の責任を負いません。  
使用者の自己責任においてご利用ください。
