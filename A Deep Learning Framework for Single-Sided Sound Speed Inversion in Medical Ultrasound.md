
# A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound (Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).)
### Reference
- Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).
A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound. IEEE Transactions on Biomedical Engineering.
- https://ieeexplore.ieee.org/abstract/document/8772124

<br />

## どんなものか
- RF信号からFCNNによって媒質の音速分布を出力するDNNアーキテクチャを構築した．

- RF信号から組織性状を求めるアプローチにDNNを用いたものとしては初．

- リアルタイムで動く．
<br />

## 研究背景，先行研究に対する新規性
- 超音波によって生体組織性状を定量的に評価する手法として組織の硬さ分布を画像化する超音波エラストグラフィがあるが，高出力が必要なためハイエンドモデルにしか搭載されておらず，フレームレートも低い．

- 生体情報を持つalternativeとして縦波音速分布を求めたい．
- 
<br />

## 手法
- Simulation:
	- リニアプローブを模した64素子で送信受信を行った．
	-  k-waveで6826パターンのシミュレーションを行い，6026パターンをTraining dataとし，800パターンをテストデータとした．
		- バリデーションデータは使ってなさそう．validation Lossがbestのものを採用するとかの発想ではなく，200epoch固定で回したらしい．
	- ランダムスペックルを密度のdomainで加算した．  
	- single plane waveとthree plane waveの2種類で結果を比較してみた．
	<img src="https://github.com/Kotatsun/papers/blob/image/plane_wave.png" width="320">
<br />

## 技術や手法の肝は
・


<br />

## 議論はある
・

<br />

## 次に読むべき論文は
