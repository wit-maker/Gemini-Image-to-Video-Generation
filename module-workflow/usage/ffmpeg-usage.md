# FFmpeg・FFprobe使用方法ガイド

## 概要
FFmpegは動画・音声の変換・編集・処理を行うコマンドラインツールです。FFprobeは動画・音声の情報取得に特化したツールです。動画コンテンツ処理で広く使用されています。

## 基本コマンド

### ffmpeg コマンド
動画・音声の変換・編集の統合コマンド。

```bash
ffmpeg -i input.mp4 [処理オプション] output.mp4
```

### ffprobe コマンド
動画・音声の情報取得専用コマンド。

```bash
ffprobe [オプション] input.mp4
```

## FFprobe - 情報取得機能

### 1. 基本情報の確認

```bash
# 基本的なメディア情報表示
ffprobe input.mp4

# バナー情報を非表示にして表示
ffprobe -hide_banner input.mp4

# 詳細情報を非表示にして最小限の情報のみ表示
ffprobe -v quiet -show_format -show_streams input.mp4
```

### 2. JSON形式での出力

```bash
# JSON形式で詳細情報を出力
ffprobe -v quiet -print_format json -show_format -show_streams input.mp4

# 特定の情報のみをJSON形式で出力
ffprobe -v quiet -print_format json -show_entries format=duration,bit_rate input.mp4
```

### 3. 動画の基本情報取得

```bash
# 動画の解像度（幅x高さ）を取得
ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of default=noprint_wrappers=1:nokey=1 input.mp4

# 動画の長さ（秒）を取得
ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 input.mp4

# 動画のビットレートを取得
ffprobe -v error -select_streams v:0 -show_entries stream=bit_rate -of default=noprint_wrappers=1:nokey=1 input.mp4

# フレームレートを取得
ffprobe -v error -select_streams v:0 -show_entries stream=r_frame_rate -of default=noprint_wrappers=1:nokey=1 input.mp4
```

### 4. 音声の基本情報取得

```bash
# 音声ストリームの情報を取得
ffprobe -v quiet -select_streams a -show_entries stream=codec_name,sample_rate,channels input.mp4

# 音声のサンプルレートを取得
ffprobe -v error -select_streams a:0 -show_entries stream=sample_rate -of default=noprint_wrappers=1:nokey=1 input.mp4

# 音声のチャンネル数を取得
ffprobe -v error -select_streams a:0 -show_entries stream=channels -of default=noprint_wrappers=1:nokey=1 input.mp4
```

### 5. 詳細情報・メタデータ取得

```bash
# フォーマット情報のみ表示
ffprobe -v quiet -show_format input.mp4

# ストリーム情報のみ表示
ffprobe -v quiet -show_streams input.mp4

# メタデータを取得
ffprobe -v quiet -show_entries format_tags:stream_tags input.mp4

# 特定のメタデータを取得
ffprobe -v quiet -show_entries format_tags=title,artist,album input.mp4
```

## FFmpeg - 動画・音声変換・編集機能

### 1. 基本的なフォーマット変換

```bash
# MP4からAVIに変換
ffmpeg -i input.mp4 output.avi

# WebMからMP4に変換（互換性向上）
ffmpeg -i input.webm output.mp4

# 複数形式を同時変換
ffmpeg -i input.mp4 output.avi output.mkv output.webm
```

### 2. 動画から音声抽出

```bash
# 動画からMP3音声を抽出
ffmpeg -i input.mp4 output.mp3

# 動画からWAV音声を抽出
ffmpeg -i input.mp4 output.wav

# 音声のみ抽出（動画ストリームを除外）
ffmpeg -i input.mp4 -vn output.mp3

# 高品質音声抽出（192kbpsで抽出）
ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -ab 192k -f mp3 output.mp3
```

### 3. 音声品質・設定の調整

```bash
# 音声品質を指定して変換（0=最高品質、9=最低品質）
ffmpeg -i input.mp4 -q:a 2 output.mp3

# 音声ビットレートを指定
ffmpeg -i input.mp4 -b:a 128k output.mp3

# サンプルレートを指定
ffmpeg -i input.mp4 -ar 22050 output.mp3

# チャンネル数を指定（モノラル=1、ステレオ=2）
ffmpeg -i input.mp4 -ac 1 output.mp3
```

### 4. 動画サイズ・解像度の変更

```bash
# 解像度を指定してリサイズ
ffmpeg -i input.mp4 -s 1280x720 output.mp4

# パーセンテージでリサイズ
ffmpeg -i input.mp4 -vf scale=iw*0.5:ih*0.5 output.mp4

# アスペクト比を維持してリサイズ
ffmpeg -i input.mp4 -vf scale=800:-1 output.mp4

# 予定義サイズでリサイズ
ffmpeg -i input.mp4 -s 480x320 -c:a copy output.mp4
```

### 5. 動画の切り出し・トリミング

```bash
# 開始時刻から指定秒数を切り出し
ffmpeg -i input.mp4 -ss 00:00:30 -t 00:00:10 output.mp4

# 開始時刻から終了時刻まで切り出し
ffmpeg -i input.mp4 -ss 00:01:00 -to 00:02:30 output.mp4

# 高速切り出し（再エンコードなし）
ffmpeg -i input.mp4 -ss 00:00:30 -t 00:00:10 -c copy output.mp4

# 複数セグメントを切り出し
ffmpeg -i input.mp4 -ss 00:00:10 -t 00:00:05 segment1.mp4 -ss 00:01:00 -t 00:00:10 segment2.mp4
```

### 6. 動画品質・エンコード設定

```bash
# H.264コーデックで高品質エンコード
ffmpeg -i input.mp4 -c:v libx264 -crf 18 -c:a aac output.mp4

# H.265（HEVC）で圧縮効率重視
ffmpeg -i input.mp4 -c:v libx265 -crf 23 -c:a aac output.mp4

# VP9コーデックで高圧縮
ffmpeg -i input.mp4 -c:v libvpx-vp9 -crf 30 -c:a libvorbis output.webm

# ビットレートを指定してエンコード
ffmpeg -i input.mp4 -b:v 1000k -b:a 128k output.mp4
```

### 7. フレームレートの変更

```bash
# フレームレートを30fpsに変更
ffmpeg -i input.mp4 -r 30 output.mp4

# フレームレートを半分に（フレーム間引き）
ffmpeg -i input.mp4 -filter:v fps=15 output.mp4

# スムーズなフレームレート変換
ffmpeg -i input.mp4 -vf fps=24 output.mp4

# 入力と出力のフレームレートを明示的に指定
ffmpeg -r 60 -i input.mp4 -r 30 output.mp4
```

### 8. 動画の回転・反転

```bash
# 90度時計回りに回転
ffmpeg -i input.mp4 -vf "transpose=1" output.mp4

# 180度回転
ffmpeg -i input.mp4 -vf "transpose=2,transpose=2" output.mp4

# 90度反時計回りに回転
ffmpeg -i input.mp4 -vf "transpose=2" output.mp4

# 水平反転（左右反転）
ffmpeg -i input.mp4 -vf hflip output.mp4

# 垂直反転（上下反転）
ffmpeg -i input.mp4 -vf vflip output.mp4
```

### 9. 動画フィルタ・エフェクト

```bash
# ブラー（ぼかし）効果
ffmpeg -i input.mp4 -vf "boxblur=5:1" output.mp4

# シャープネス効果
ffmpeg -i input.mp4 -vf "unsharp=5:5:1.0:5:5:0.0" output.mp4

# 明度・コントラスト調整
ffmpeg -i input.mp4 -vf "eq=brightness=0.1:contrast=1.2" output.mp4

# 彩度調整
ffmpeg -i input.mp4 -vf "eq=saturation=1.5" output.mp4

# ガンマ補正
ffmpeg -i input.mp4 -vf "eq=gamma=1.2" output.mp4
```

### 10. 音声フィルタ・エフェクト

```bash
# 音声のボリューム調整（2倍）
ffmpeg -i input.mp4 -af "volume=2.0" output.mp4

# 音声のボリューム調整（デシベル）
ffmpeg -i input.mp4 -af "volume=10dB" output.mp4

# 音声の再生速度変更（2倍速）
ffmpeg -i input.mp4 -af "atempo=2.0" output.mp4

# 音声のピッチ変更（半音上げる）
ffmpeg -i input.mp4 -af "asetrate=48000*2^(1/12),aresample=48000" output.mp4

# ノイズ除去
ffmpeg -i input.mp4 -af "highpass=f=300,lowpass=f=3000" output.mp4
```

### 11. 動画の合成・結合

```bash
# 動画を横に並べて結合
ffmpeg -i left.mp4 -i right.mp4 -filter_complex hstack output.mp4

# 動画を縦に並べて結合
ffmpeg -i top.mp4 -i bottom.mp4 -filter_complex vstack output.mp4

# 動画を順番に結合（同じ解像度・フレームレート必須）
ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4

# ピクチャーインピクチャー合成
ffmpeg -i main.mp4 -i overlay.mp4 -filter_complex "[1:v]scale=320:240[pip];[0:v][pip]overlay=W-w-10:10" output.mp4
```

### 12. 字幕・テキストの追加

```bash
# テキストを動画に追加
ffmpeg -i input.mp4 -vf "drawtext=text='Hello World':fontsize=24:fontcolor=white:x=10:y=10" output.mp4

# 時間指定でテキスト表示
ffmpeg -i input.mp4 -vf "drawtext=text='Sample Text':enable='between(t,5,10)':fontsize=30:fontcolor=yellow:x=100:y=100" output.mp4

# 外部字幕ファイルを追加
ffmpeg -i input.mp4 -i subtitles.srt -c copy -c:s mov_text output.mp4

# フォントファイルを指定してテキスト追加
ffmpeg -i input.mp4 -vf "drawtext=fontfile=arial.ttf:text='Custom Font':fontsize=36:fontcolor=red:x=50:y=50" output.mp4
```

### 13. 画像からの動画作成

```bash
# 画像から動画を作成（5秒間）
ffmpeg -loop 1 -i image.jpg -t 5 -pix_fmt yuv420p output.mp4

# 複数画像からスライドショー動画作成
ffmpeg -r 1 -i img%03d.jpg -c:v libx264 -r 30 -pix_fmt yuv420p slideshow.mp4

# 画像にズーム効果を付けて動画作成
ffmpeg -loop 1 -i image.jpg -vf "scale=1280:720,zoompan=z='min(zoom+0.0015,1.5)':d=125" -t 5 output.mp4

# 画像をフレームとして使用（指定フレームレート）
ffmpeg -framerate 24 -i frame%04d.png -c:v libx264 -pix_fmt yuv420p output.mp4
```

### 14. 動画から画像抽出

```bash
# 1秒ごとに画像を抽出
ffmpeg -i input.mp4 -vf fps=1 output_%03d.jpg

# 指定時刻のフレームを画像として抽出
ffmpeg -i input.mp4 -ss 00:00:15 -vframes 1 screenshot.jpg

# 高品質で画像抽出
ffmpeg -i input.mp4 -vf "select=eq(n\,0)" -q:v 2 first_frame.jpg

# 動画全体から等間隔で画像抽出
ffmpeg -i input.mp4 -vf "select='not(mod(n\,300))'" -vsync 0 frame_%04d.jpg
```

### 15. 音声の合成・ミキシング

```bash
# 複数音声ファイルをミックス
ffmpeg -i audio1.mp3 -i audio2.mp3 -filter_complex amix=inputs=2:duration=longest output.mp3

# 動画に別の音声を追加（オーバーレイ）
ffmpeg -i video.mp4 -i audio.mp3 -filter_complex "[0:a][1:a]amix=inputs=2:duration=shortest[a]" -map 0:v -map "[a]" output.mp4

# 音声のフェードイン・フェードアウト
ffmpeg -i input.mp3 -af "afade=in:st=0:d=3,afade=out:st=27:d=3" output.mp3

# 音声を指定時間で結合
ffmpeg -i audio1.mp3 -i audio2.mp3 -filter_complex "[0:a][1:a]concat=n=2:v=0:a=1[a]" -map "[a]" output.mp3
```

### 16. ライブストリーミング

```bash
# YouTube Liveにストリーミング
ffmpeg -i input.mp4 -c:v libx264 -b:v 2500k -c:a aac -b:a 128k -f flv rtmp://a.rtmp.youtube.com/live2/YOUR_STREAM_KEY

# Twitchにストリーミング
ffmpeg -i input.mp4 -c:v libx264 -b:v 3000k -c:a aac -b:a 160k -f flv rtmp://live.twitch.tv/live/YOUR_STREAM_KEY

# RTMPサーバーにストリーミング
ffmpeg -re -i input.mp4 -c copy -f flv rtmp://server/app/streamkey
```

### 17. 高速処理・無劣化変換

```bash
# コーデック変換なしの高速処理
ffmpeg -i input.mp4 -c copy output.mkv

# 動画ストリームのみコピー（音声は再エンコード）
ffmpeg -i input.mp4 -c:v copy -c:a aac output.mp4

# 音声ストリームのみコピー（動画は再エンコード）
ffmpeg -i input.mp4 -c:v libx264 -c:a copy output.mp4

# 形式変更のみ（エンコードなし）
ffmpeg -i input.avi -c copy output.mp4
```

### 18. バッチ処理・スクリプト対応

```bash
# 複数ファイルを一括変換（bash）
for file in *.mp4; do
    ffmpeg -i "$file" -c:v libx264 -crf 23 "converted_${file}"
done

# ファイルリストから一括処理
while read line; do
    ffmpeg -i "$line" -c:v libx265 -crf 28 "compressed_$line"
done < filelist.txt

# 並列処理（バックグラウンド実行）
ffmpeg -i video1.mp4 -c:v libx264 output1.mp4 &
ffmpeg -i video2.mp4 -c:v libx264 output2.mp4 &
wait
```

## 高度な合成・編集

### 1. グリーンスクリーン（クロマキー）合成

```bash
# 緑背景を透明にして合成
ffmpeg -i greenscreen.mp4 -i background.mp4 -filter_complex "[0:v]chromakey=0x00FF00:0.3:0.2[ckout];[1:v][ckout]overlay[out]" -map "[out]" output.mp4

# より精密なクロマキー処理
ffmpeg -i greenscreen.mp4 -i background.mp4 -filter_complex "[0:v]chromakey=green:0.1:0.2[ckout];[1:v][ckout]overlay=0:0[out]" -map "[out]" -map 0:a output.mp4
```

### 2. 動画のモザイク・ブラー処理

```bash
# 全体にモザイク効果
ffmpeg -i input.mp4 -vf "scale=iw/10:ih/10,scale=iw*10:ih*10:flags=neighbor" output.mp4

# 特定領域にモザイク
ffmpeg -i input.mp4 -vf "split[main][tmp];[tmp]crop=100:100:50:50,scale=10:10,scale=100:100:flags=neighbor[mosaic];[main][mosaic]overlay=50:50" output.mp4

# 顔検出自動ブラー（要OpenCV）
ffmpeg -i input.mp4 -vf "boxblur=10:1" output.mp4
```

### 3. タイムラプス・スローモーション

```bash
# タイムラプス（10倍速）
ffmpeg -i input.mp4 -vf "setpts=0.1*PTS" output.mp4

# スローモーション（0.5倍速）
ffmpeg -i input.mp4 -vf "setpts=2.0*PTS" output.mp4

# 音声も含めたスピード調整
ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=0.5*PTS[v];[0:a]atempo=2.0[a]" -map "[v]" -map "[a]" output.mp4
```

### 4. 動画の色調補正・グレーディング

```bash
# セピア調に変換
ffmpeg -i input.mp4 -vf "colorchannelmixer=.393:.769:.189:0:.349:.686:.168:0:.272:.534:.131" output.mp4

# 白黒変換
ffmpeg -i input.mp4 -vf "hue=s=0" output.mp4

# ビンテージ風加工
ffmpeg -i input.mp4 -vf "eq=contrast=1.2:brightness=-0.1:saturation=0.8,curves=vintage" output.mp4

# カラーバランス調整
ffmpeg -i input.mp4 -vf "eq=gamma_r=0.9:gamma_g=1.0:gamma_b=1.1" output.mp4
```

## 実用的な応用例

### 1. SNS向け動画最適化

```bash
# Instagram用正方形動画（1080x1080）
ffmpeg -i input.mp4 -vf "scale=1080:1080:force_original_aspect_ratio=decrease,pad=1080:1080:(ow-iw)/2:(oh-ih)/2" output.mp4

# TikTok/YouTube Shorts用縦動画（1080x1920）
ffmpeg -i input.mp4 -vf "scale=1080:1920:force_original_aspect_ratio=decrease,pad=1080:1920:(ow-iw)/2:(oh-ih)/2" output.mp4

# Twitter用動画（最適化）
ffmpeg -i input.mp4 -c:v libx264 -crf 23 -c:a aac -b:a 128k -movflags +faststart output.mp4
```

### 2. プレゼンテーション動画作成

```bash
# スライド画像から動画作成（各スライド3秒表示）
ffmpeg -r 1/3 -i slide%03d.jpg -c:v libx264 -r 30 -pix_fmt yuv420p presentation.mp4

# 音声付きプレゼンテーション
ffmpeg -r 1/3 -i slide%03d.jpg -i narration.mp3 -c:v libx264 -c:a aac -shortest presentation.mp4

# 画面録画に音声追加
ffmpeg -i screen_recording.mp4 -i audio.mp3 -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 final_presentation.mp4
```

### 3. ポッドキャスト・音声コンテンツ

```bash
# 複数音声セクションを結合
ffmpeg -f concat -safe 0 -i podcast_segments.txt -c copy podcast_full.mp3

# 音声レベル正規化
ffmpeg -i input.mp3 -af "loudnorm=I=-16:TP=-1.5:LRA=11" normalized.mp3

# チャプター付き音声ファイル作成
ffmpeg -i input.mp3 -i chapters.txt -map 0 -map_metadata 1 -c copy podcast_with_chapters.m4a
```

## パフォーマンス最適化

### 1. ハードウェアアクセラレーション

```bash
# NVIDIA GPU使用（NVENC）
ffmpeg -hwaccel nvdec -i input.mp4 -c:v h264_nvenc -b:v 5M output.mp4

# Intel Quick Sync使用
ffmpeg -hwaccel qsv -i input.mp4 -c:v h264_qsv -b:v 5M output.mp4

# AMD GPU使用（AMF）
ffmpeg -hwaccel d3d11va -i input.mp4 -c:v h264_amf -b:v 5M output.mp4
```

### 2. 並列処理・マルチスレッド

```bash
# スレッド数を指定
ffmpeg -threads 8 -i input.mp4 -c:v libx264 -preset fast output.mp4

# タイル並列処理（AV1エンコード）
ffmpeg -i input.mp4 -c:v libaom-av1 -tiles 2x2 -threads 8 output.mp4
```

### 3. メモリ効率化

```bash
# バッファサイズを調整
ffmpeg -probesize 32M -analyzeduration 10M -i input.mp4 -c copy output.mp4

# 一時ファイルディスク使用
ffmpeg -f lavfi -i testsrc -t 10 -c:v libx264 -maxrate 1M -bufsize 2M output.mp4
```

## 品質設定とファイルサイズ最適化

### 1. 画質とファイルサイズのバランス

```bash
# 高品質（大きなファイルサイズ）
ffmpeg -i input.mp4 -c:v libx264 -crf 18 -c:a aac -b:a 192k output.mp4

# 標準品質（バランス型）
ffmpeg -i input.mp4 -c:v libx264 -crf 23 -c:a aac -b:a 128k output.mp4

# 低品質（小さなファイルサイズ）
ffmpeg -i input.mp4 -c:v libx264 -crf 28 -c:a aac -b:a 96k output.mp4
```

### 2. 二段階エンコーディング

```bash
# 1段階目（分析パス）
ffmpeg -i input.mp4 -c:v libx264 -b:v 1000k -pass 1 -f null /dev/null

# 2段階目（エンコードパス）
ffmpeg -i input.mp4 -c:v libx264 -b:v 1000k -pass 2 output.mp4
```

## エラー対処とトラブルシューティング

### 1. よくあるエラーと対処法

```bash
# コーデックがサポートされていない場合
ffmpeg -codecs | grep h264  # 利用可能コーデック確認

# 音声同期のずれを修正
ffmpeg -i input.mp4 -itsoffset 0.5 -i input.mp4 -map 0:v -map 1:a -c copy output.mp4

# 破損した動画ファイルの修復
ffmpeg -err_detect ignore_err -i broken.mp4 -c copy fixed.mp4
```

### 2. デバッグとログ出力

```bash
# 詳細ログ出力
ffmpeg -v verbose -i input.mp4 output.mp4

# プログレス情報表示
ffmpeg -progress progress.txt -i input.mp4 output.mp4

# ベンチマーク情報表示
ffmpeg -benchmark -i input.mp4 output.mp4
```

## 注意事項

- FFmpegは非常に多機能なため、適切なオプションの組み合わせが重要です
- 大きな動画ファイルの処理には時間とシステムリソースが必要です
- ハードウェアアクセラレーションは環境依存です
- 著作権保護されたコンテンツの処理は法的制限があります
- バッチ処理時はシステムの負荷に注意してください

## 参考リンク

- [FFmpeg公式サイト](https://ffmpeg.org/)
- [FFmpegドキュメント](https://ffmpeg.org/documentation.html)
- [FFprobe公式ドキュメント](https://ffmpeg.org/ffprobe.html)
- [コマンドライン例集](https://github.com/lbbedendo/ffmpeg-commands)