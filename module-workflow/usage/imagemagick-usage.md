# ImageMagick使用方法ガイド

## 概要
ImageMagickは画像の編集・変換・処理を行うコマンドラインツールです。自律修正バナー生成で画像後処理に使用します。

## 基本コマンド

### magick コマンド
ImageMagick v7の統一コマンド。すべての操作で使用します。

```bash
magick input.png [処理オプション] output.png
```

## 主要な画像調整機能

### 1. 明度・彩度・色相調整

```bash
# 明度・彩度・色相を調整（modulate brightness,saturation,hue）
magick input.png -modulate 120,130,100 output.png
# 明度120%、彩度130%、色相100%（変更なし）

# 個別調整
magick input.png -brightness-contrast 10x15 output.png  # 明度+10、コントラスト+15
magick input.png -gamma 1.3 output.png                  # ガンマ補正（明るく）
magick input.png -gamma 0.8 output.png                  # ガンマ補正（暗く）
```

### 2. コントラスト調整

```bash
# レベル調整（黒点20%、白点80%に設定）
magick input.png -level 20%,80% output.png

# 自動レベル調整
magick input.png -auto-level output.png

# シグモイダルコントラスト（より自然な調整）
magick input.png -sigmoidal-contrast 3,50% output.png
```

### 3. シャープネス・ぼかし

```bash
# アンシャープマスク（シャープネス向上）
magick input.png -unsharp 0x1+1.0+0.05 output.png

# より強いシャープネス
magick input.png -unsharp 0x2+2.0+0.1 output.png

# ぼかし
magick input.png -blur 0x1 output.png
magick input.png -gaussian-blur 0x2 output.png
```

### 4. ノイズ除去・画質向上

```bash
# ノイズ除去
magick input.png -despeckle output.png

# 全体的な画質向上
magick input.png -enhance output.png

# ノイズ除去（より高度）
magick input.png -noise 0 output.png
```

### 5. 色調補正

```bash
# 色温度調整（暖色系に）
magick input.png -modulate 100,100,105 output.png

# 色温度調整（寒色系に）
magick input.png -modulate 100,100,95 output.png

# 色の置換
magick input.png -fuzz 10% -fill red -opaque blue output.png
```

### 6. サイズ・形状変更

```bash
# リサイズ
magick input.png -resize 800x600 output.png
magick input.png -resize 50% output.png

# 切り取り
magick input.png -crop 400x400+100+100 output.png

# 回転
magick input.png -rotate 90 output.png

# 反転
magick input.png -flip output.png    # 上下反転
magick input.png -flop output.png    # 左右反転
```

### 7. 特殊効果・フィルタ

```bash
# エンボス効果
magick input.png -emboss 2 output.png

# エッジ検出
magick input.png -edge 2 output.png

# 油絵効果
magick input.png -paint 3 output.png

# 水彩画効果
magick input.png -blur 0x1 -paint 2 output.png

# セピア調
magick input.png -sepia-tone 80% output.png

# モノクロ（グレースケール）
magick input.png -colorspace Gray output.png

# ポスタライゼーション（階調数を減らす）
magick input.png -posterize 8 output.png
```

### 8. 色彩・トーン調整

```bash
# 色チャンネルの調整
magick input.png -channel Red -evaluate multiply 1.2 output.png

# 白黒の閾値処理
magick input.png -threshold 50% output.png

# 色の反転（ネガ）
magick input.png -negate output.png

# 透明度の調整
magick input.png -alpha set -channel A -evaluate multiply 0.8 output.png

# 色相の回転
magick input.png -modulate 100,100,120 output.png

# 自動色調補正
magick input.png -auto-gamma output.png
magick input.png -normalize output.png
```

### 9. 合成・レイヤー処理

```bash
# 画像の合成
magick background.png overlay.png -composite output.png

# 画像を並べる
magick image1.png image2.png +append output.png  # 横並び
magick image1.png image2.png -append output.png  # 縦並び

# 境界線を追加
magick input.png -bordercolor black -border 5x5 output.png

# フレームを追加
magick input.png -mattecolor gray -frame 10x10+3+3 output.png

# 影を追加
magick input.png \( +clone -background black -shadow 80x3+3+3 \) +swap -background none -layers merge output.png
```

### 10. テキスト・注釈

```bash
# テキストを追加
magick input.png -font Arial -pointsize 30 -fill white -annotate +50+100 'Hello World' output.png

# 透かし文字
magick input.png -font Arial -pointsize 50 -fill 'rgba(255,255,255,0.5)' -gravity center -annotate 0 'DRAFT' output.png

# 囲み文字
magick input.png -font Arial -pointsize 30 -fill white -stroke black -strokewidth 2 -annotate +50+100 'Outlined Text' output.png
```

### 11. 歪み・変形

```bash
# 遠近法変換
magick input.png -distort Perspective '0,0 0,0  100,0 90,10  100,100 110,90  0,100 10,90' output.png

# 樽型歪み補正
magick input.png -distort Barrel '0.1 0.0 0.0 1.0' output.png

# 波形変形
magick input.png -wave 10x50 output.png

# 渦巻き効果
magick input.png -swirl 90 output.png
```

### 12. ノイズ生成・除去

```bash
# ノイズ追加
magick input.png -noise Gaussian output.png
magick input.png -noise Uniform output.png

# モーションブラー
magick input.png -motion-blur 0x20+30 output.png

# 放射状ブラー
magick input.png -radial-blur 5 output.png
```

### 13. 形状・マスク処理

```bash
# 円形に切り取り
magick input.png \( +clone -threshold -1 -negate -fill white -draw 'circle %[fx:w/2],%[fx:h/2] %[fx:w/2],0' \) -alpha off -compose copy_opacity -composite output.png

# 角丸四角形
magick input.png -alpha set \( +clone -alpha extract -draw 'fill black polygon 0,0 0,15 15,0 fill white circle 15,15 15,0' \( +clone -flip \) -compose Multiply -composite \( +clone -flop \) -compose Multiply -composite \) -alpha off -compose CopyOpacity -composite output.png
```

### 14. 統計・分析

```bash
# 画像統計
magick input.png -format "Mean: %[mean]\nStd Dev: %[standard-deviation]" info:

# 色数カウント
magick input.png -format "%k colors" info:

# ヒストグラム統計
magick input.png -define histogram:unique-colors=false histogram:- | magick - -format "%c" histogram:info:
```

### 15. 背景・透明度処理

```bash
# 背景を透明に
magick input.png -fuzz 10% -transparent white output.png

# 背景色を変更
magick input.png -background red -flatten output.png

# チェッカーボード背景を追加
magick input.png -background 'pattern:checkerboard' -flatten output.png

# グラデーション背景
magick -size 400x300 gradient:blue-white background.png
magick input.png background.png -composite output.png
```

### 16. フォーマット変換・圧縮

```bash
# 形式変換
magick input.png output.jpg
magick input.jpg -quality 85 output.jpg  # JPEG品質指定

# PNG最適化
magick input.png -strip -define png:compression-level=9 output.png

# WebP変換
magick input.png -quality 80 output.webp

# PDF生成
magick image1.png image2.png output.pdf
```

### 17. 高度な合成モード

```bash
# 乗算合成
magick base.png overlay.png -compose Multiply -composite output.png

# スクリーン合成
magick base.png overlay.png -compose Screen -composite output.png

# オーバーレイ合成
magick base.png overlay.png -compose Overlay -composite output.png

# 差分合成
magick base.png overlay.png -compose Difference -composite output.png
```

### 18. 動的なエフェクト

```bash
# 渦巻きアニメーション（複数フレーム）
magick input.png -duplicate 9 -virtual-pixel tile -distort SRT '%[fx:360*t/n]' anim_%02d.png

# カラーサイクル
magick input.png -duplicate 11 -virtual-pixel tile -distort SRT '0,0 1,1 %[fx:360*t/n]' -modulate 100,100,%[fx:100+50*sin(2*pi*t/n)] cycle_%02d.png

# フェードイン・アウト
magick input.png -duplicate 9 -alpha set -channel A -evaluate multiply %[fx:t/n] fade_%02d.png
```

### 19. カスタムフィルタ・畳み込み

```bash
# カスタム畳み込みフィルタ
magick input.png -morphology Convolve '3x3:-1,-1,-1,-1,8,-1,-1,-1,-1' output.png  # シャープニング

# エッジ強調
magick input.png -morphology Convolve '3x3:0,-1,0,-1,5,-1,0,-1,0' output.png

# ぼかしフィルタ
magick input.png -morphology Convolve '3x3:1,1,1,1,1,1,1,1,1' output.png
```

### 20. 色空間・プロファイル

```bash
# 色空間変換
magick input.png -colorspace HSL output.png
magick input.png -colorspace LAB output.png

# ICCプロファイル適用
magick input.png -profile sRGB.icc output.png

# プロファイル情報確認
magick identify -verbose input.png | grep -i profile
```

## 組み合わせ処理

### 複数の調整を同時実行
```bash
# 明度・コントラスト・シャープネスを同時調整
magick input.png \
  -modulate 110,120,100 \
  -sigmoidal-contrast 2,50% \
  -unsharp 0x1+1.0+0.05 \
  output.png
```

### パイプライン処理
```bash
# 段階的に処理を適用
magick input.png -auto-level temp1.png
magick temp1.png -enhance temp2.png
magick temp2.png -unsharp 0x1+1.0+0.05 output.png
```

## 自律修正での使用例

### 評価結果に基づく調整判定

```bash
# 「暗すぎる」場合
magick input.png -gamma 1.2 -modulate 110,100,100 output.png

# 「コントラストが低い」場合
magick input.png -sigmoidal-contrast 3,50% output.png

# 「ぼやけている」場合
magick input.png -unsharp 0x1+1.0+0.05 output.png

# 「色が薄い」場合
magick input.png -modulate 100,130,100 output.png

# 「ノイズが多い」場合
magick input.png -despeckle -enhance output.png
```

### 品質向上の組み合わせ
```bash
# 一般的な品質向上処理
magick input.png \
  -auto-level \
  -enhance \
  -unsharp 0x1+0.8+0.05 \
  -modulate 105,110,100 \
  output.png
```

## 画像情報の確認

### 画像の詳細情報取得
```bash
# 基本情報
magick identify input.png

# 詳細情報
magick identify -verbose input.png

# サイズのみ
magick identify -format "%wx%h" input.png
```

### ヒストグラム生成
```bash
# 色分布の確認
magick input.png -define histogram:unique-colors=false histogram:histogram.png
```

## パフォーマンス最適化

### メモリ効率
```bash
# 大きな画像の処理時
magick -limit memory 256MB -limit disk 1GB input.png -resize 50% output.png
```

### マルチスレッド処理
```bash
# スレッド数を指定
magick -limit thread 4 input.png -enhance output.png
```

## エラー対処

### よくあるエラーと対処法

1. **メモリ不足**
   ```bash
   magick -limit memory 512MB input.png -resize 2048x2048 output.png
   ```

2. **ファイル形式エラー**
   ```bash
   magick input.jpg PNG:output.png  # 明示的な形式指定
   ```

3. **権限エラー**
   ```bash
   # 一時ファイルのパス確認
   magick -debug configure input.png output.png
   ```

## 注意事項

- ImageMagick v7では`magick`コマンドを使用（`convert`は非推奨）
- 処理によってファイルサイズが変わる場合があります
- 大きな画像の処理には時間がかかります
- 品質向上処理は画像の特徴に依存します

## 参考リンク

- [ImageMagick公式サイト](https://imagemagick.org/)
- [コマンドラインオプション](https://imagemagick.org/script/command-line-options.php)
- [画像処理の例](https://imagemagick.org/Usage/)