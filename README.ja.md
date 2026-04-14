# houdini-comic-render
* Houdiniシーン情報から漫画風描画を行うHDAとサンプルプロジェクトになります。</br>※Mardini2026の作成物を公開用に整備したものです。</br>
  <img src="/ReadMeContents/00_title.png" width=600/>
* 解説記事は以下になります。
  * <a href="https://elekibear.com/post/20260413_01_houdini_comic_render">【Houdini21.0】Copernicusで漫画風描画・吹き出し作成を行う
</a>

## バージョン
* Houdini Indie
    * 21.0.512

## シーン内容

* 2コマ分の設定と、その合成処理を用意しています。</br>それぞれのcopnetの中でポスト処理を行なっています。</br>
   <img src="/ReadMeContents/01_node_sop.png" width=600/>
   
   | Name | Description |
   | -- | -- |
   | SCENE1 | シーン1(全体)のコマ</br><img src="/ReadMeContents/99_render_scene_01.png" width=280/> |
   | SCENE2 | シーン2(左下)のコマ</br><img src="/ReadMeContents/99_render_scene_02.png" width=280/> |
   | COMPOSITE | シーン1、シーン2の合成結果</br><img src="/ReadMeContents/99_render.png" width=280/> |

* 各copnet内の「漫画風描画を行う処理」と「吹き出しを作成する処理」がメインになります。
    * 漫画風描画部分</br>
      <img src="/ReadMeContents/02_node_comic_post.png" width=600/>
    * 吹き出し作成部分</br>
      <img src="/ReadMeContents/03_node_speech_bubble.png" width=400/>
* Solarisで描画を行う場合の簡易サンプルも用意しています。</br>こちらはslapcompを有効にすることで確認できるよう設定しています。</br>
  <img src="/ReadMeContents/06_node_solaris.png" width=600/>


## HDA内容

* COPで使用できる各HDAを用意しています。

| Name | Description |
| -- | -- |
| Comic Post Process | カラー、法線情報を元に漫画風の描画を行うHDA |
| Comic Tones | 漫画風トーン画像のサンプルライブラリHDA |
| Comic Speech Bubble | 漫画風吹き出しを作成するHDA |

### Comic Post Process

* カラー、法線情報を元に漫画風の描画を行うHDAです。
  * 入力するトーン画像は、自身で用意した画像でも後述の「Comic Tones」HDAを使用しても問題ありません。
      * 5段階の入力情報として設定できるようにしています。
  * 入力するカラー情報は、Unlitの状態で渡すと綺麗に描画できます。

###### Input

| Name | Description |
| -- | -- |
| Cd | 画像のカラー情報 |
| N | 画像のノーマル情報 |
| Tone1 | トーン画像1 |
| Tone2 | トーン画像2 |
| Tone3 | トーン画像3 |
| Tone4 | トーン画像4 |
| Tone5 | トーン画像5 |

###### Parameter

<img src="/ReadMeContents/04_hda_comic_post_process.png" width=400/>

| Category | Name | Description |
| -- | -- | -- |
| Toon | Toon Ramp | カラー情報からトゥーン描画を行うためのしきい値 |
| | Normal Ramp | 法線情報からトゥーン描画を行うためのしきい値 |
| | Normal Light Direction | 法線情報からランバート反射を計算するためのライト方向 |
| Comic | Enable Comic | 漫画風描画を有効にするか？ |
| Comic - Tones | ToneN | トーン画像Nを有効にするか？ |
| | Tone1 Ratio Min | トーン画像を設定するしきい値 |
| Comic - Outline | Add Outline | アウトラインを追加するか？ |

### Comic Tones

* 漫画風トーン画像のサンプルライブラリHDAです。
  * Comic Post Process HDAへの入力としてご使用ください。

###### Output

| Name | Description |
| -- | -- |
| black | 黒単色</br><img src="/ReadMeContents/99_tone_black.png" width=120 /> |
| dot1 | ドット1</br><img src="/ReadMeContents/99_tone_dot_1.png" width=120 /> |
| dot2 | ドット2</br><img src="/ReadMeContents/99_tone_dot_2.png" width=120 /> |
| dot3 | ドット3</br><img src="/ReadMeContents/99_tone_dot_3.png" width=120 /> |
| line | 縦線</br><img src="/ReadMeContents/99_tone_line.png" width=120 /> |
| noise | ノイズ</br><img src="/ReadMeContents/99_tone_noise.png" width=120 /> |
| white | 白単色</br><img src="/ReadMeContents/99_tone_white.png" width=120 /> |


### Comic Speech Bubble

* 漫画風吹き出しを作成するHDAです。
  * 楕円型、爆発型の2種類を用意しています。

###### Parameter

<img src="/ReadMeContents/05_hda_comic_speech_bubble.png" width=400/>

| Category | Name | Description |
| -- | -- | -- |
| Base | Speech Bubble Type | 吹き出しの種類</br>Circle：楕円型</br><img src="/ReadMeContents/99_speech_bubble_circle.png" width=120 /></br>Bomb：爆発型</br><img src="/ReadMeContents/99_speech_bubble_bomb.png" width=120 /> |
| | Outline Width | アウトライン幅 |
| | Translate | 吹き出しの位置 |
| | Rotate | 吹き出しの回転情報 |
| | Scale | 吹き出しの大きさ |
| | Uniform Scale | 吹き出しの大きさ |
| Circle | Triangle Scale | 吹き出し三角部分の大きさ |
| | Triangle Offset | 吹き出し三角部分の楕円部分からの位置 |
| | Triangle Rotate | 吹き出し三角部分の楕円部分上の位置 |
| Bomb | Total Number | Bomb部分の数 |
| | Translate | Bomb部分の切り抜きに使用するCircleの位置 |
| | Radius | Bomb部分の切り抜きに使用するCircleの大きさ |
| Distort | Distort Scale | Distortの強さ |
| | Distort Noise Amplitude | Distortのノイズの強さ |
| | Distort Noise Element | DistortのノイズのElement大きさ |
| Lines | Font | セリフのフォント |
| | Text | セリフのテキスト |
| | Font Size | フォントサイズ |
| | Outline Width | フォントアウトライン幅 |
