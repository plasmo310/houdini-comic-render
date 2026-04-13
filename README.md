<a href="/README.ja.md">日本語版ドキュメントはこちら</a>
# houdini-comic-render
* This repository contains HDAs and a sample project for creating comic-style renders from Houdini scene data.</br>Note: this is a cleaned-up public version of a work originally created for Mardini 2026.</br>
  <img src="/ReadMeContents/00_title.png" width=600/>
* The explanatory article is available below. (Japanese)
  * <a href="https://elekibear.com/post/20260413_01_houdini_comic_render">【Houdini21.0】Copernicusで漫画風描画・吹き出し作成を行う</a>

## Version
* Houdini Indie
    * 21.0.512

## Scene Overview

* The project includes settings for two comic panels and a compositing setup for combining them.</br>Post-processing is handled inside each `copnet`.
   <img src="/ReadMeContents/01_node_sop.png" width=600/>
   
   | Name | Description |
   | -- | -- |
   | SCENE1 | Panel for Scene 1 (full view)</br><img src="/ReadMeContents/99_render_scene_01.png" width=280/> |
   | SCENE2 | Panel for Scene 2 (bottom-left view)</br><img src="/ReadMeContents/99_render_scene_02.png" width=280/> |
   | COMPOSITE | Composite result of Scene 1 and Scene 2</br><img src="/ReadMeContents/99_render.png" width=280/> |

* Inside each `copnet`, the main parts are the comic-style rendering process and the speech bubble generation process.
    * Comic-style rendering section</br>
      <img src="/ReadMeContents/02_node_comic_post.png" width=600/>
    * Speech bubble generation section</br>
      <img src="/ReadMeContents/03_node_speech_bubble.png" width=400/>
* A simple sample for rendering in Solaris is also included.</br>It is configured so you can inspect it by enabling `slapcomp`.</br>
  <img src="/ReadMeContents/06_node_solaris.png" width=600/>


## Included HDAs

* This project includes several HDAs that can be used in COPs.

| Name | Description |
| -- | -- |
| Comic Post Process | HDA for generating comic-style renders from color and normal information |
| Comic Tones | Sample library HDA of comic-style tone images |
| Comic Speech Bubble | HDA for creating comic-style speech bubbles |

### Comic Post Process

* This HDA creates a comic-style render from color and normal information.
  * The input tone images can be either your own images or the outputs from the `Comic Tones` HDA described below.
      * Up to five tone inputs can be configured.
  * For cleaner output, pass the color input in an unlit state.

###### Input

| Name | Description |
| -- | -- |
| Cd | Image color information |
| N | Image normal information |
| Tone1 | Tone image 1 |
| Tone2 | Tone image 2 |
| Tone3 | Tone image 3 |
| Tone4 | Tone image 4 |
| Tone5 | Tone image 5 |

###### Parameter

<img src="/ReadMeContents/04_hda_comic_post_process.png" width=400/>

| Category | Name | Description |
| -- | -- | -- |
| Toon | Toon Ramp | Thresholds for toon shading based on color information |
| | Normal Ramp | Thresholds for toon shading based on normal information |
| | Normal Light Direction | Light direction used to calculate Lambert shading from normal information |
| Comic | Enable Comic | Enables comic-style rendering |
| Comic - Tones | ToneN | Enables tone image N |
| | Tone1 Ratio Min | Threshold used to apply the tone image |
| Comic - Outline | Add Outline | Adds an outline |

### Comic Tones

* This HDA is a sample library of comic-style tone images.
  * Use these outputs as inputs for the `Comic Post Process` HDA.

###### Output

| Name | Description |
| -- | -- |
| black | Solid black</br><img src="/ReadMeContents/99_tone_black.png" width=120 /> |
| dot1 | Dot 1</br><img src="/ReadMeContents/99_tone_dot_1.png" width=120 /> |
| dot2 | Dot 2</br><img src="/ReadMeContents/99_tone_dot_2.png" width=120 /> |
| dot3 | Dot 3</br><img src="/ReadMeContents/99_tone_dot_3.png" width=120 /> |
| line | Vertical lines</br><img src="/ReadMeContents/99_tone_line.png" width=120 /> |
| noise | Noise</br><img src="/ReadMeContents/99_tone_noise.png" width=120 /> |
| white | Solid white</br><img src="/ReadMeContents/99_tone_white.png" width=120 /> |


### Comic Speech Bubble

* This HDA creates comic-style speech bubbles.
  * Two types are provided: ellipse and explosion.

###### Parameter

<img src="/ReadMeContents/05_hda_comic_speech_bubble.png" width=400/>

| Category | Name | Description |
| -- | -- | -- |
| Base | Speech Bubble Type | Speech bubble type</br>Circle: Ellipse</br><img src="/ReadMeContents/99_speech_bubble_circle.png" width=120 /></br>Bomb: Explosion</br><img src="/ReadMeContents/99_speech_bubble_bomb.png" width=120 /> |
| | Outline Width | Outline width |
| | Translate | Speech bubble position |
| | Rotate | Speech bubble rotation |
| | Scale | Speech bubble size |
| | Uniform Scale | Uniform speech bubble scale |
| Circle | Triangle Scale | Size of the speech bubble tail |
| | Triangle Offset | Offset of the tail from the ellipse portion |
| | Triangle Rotate | Position of the tail around the ellipse portion |
| Bomb | Total Number | Number of bomb segments |
| | Translate | Position of the circle used to cut the bomb shape |
| | Radius | Size of the circle used to cut the bomb shape |
| Distort | Distort Scale | Distortion strength |
| | Distort Noise Amplitude | Noise amplitude for distortion |
| | Distort Noise Element | Element size of the distortion noise |
| Lines | Font | Dialogue font |
| | Text | Dialogue text |
| | Font Size | Font size |
| | Outline Width | Font outline width |
