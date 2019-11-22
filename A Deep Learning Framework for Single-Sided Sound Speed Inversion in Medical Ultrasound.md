# A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound (Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).)
### Reference
- Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).
A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound. IEEE Transactions on Biomedical Engineering.
- https://ieeexplore.ieee.org/abstract/document/8772124

<br />

## どんなものか
<img src="https://github.com/Kotatsun/papers/blob/image/ground_result.png" width="220">

- RF信号からFCNNによって媒質の音速分布を推定するDNNアーキテクチャを構築した．

- RF信号から組織性状を求めるアプローチにDNNを用いたものとしては初．

- リアルタイム性あり．
<br />

## 研究背景，先行研究に対する新規性
- 超音波によって生体組織性状を定量的に評価する手法として組織の硬さ分布を画像化する超音波エラストグラフィがあるが，高出力が必要なためハイエンドモデルにしか搭載されておらず，フレームレートも低い．  
	　→ 生体情報を得るalternativeとして縦波音速分布を求めたい．


- 音速分布の繰り返し計算は計算コストが高く，リアルタイム性に欠ける．  
	　→DNNによるpredictionならリアルタイム(高フレームレート)な処理が可能．
<br />

## 手法
- Simulation:
	- リニアプローブを模した64素子で送信受信を行った．
	-  k-waveで6826パターンのシミュレーションを行い，6026パターンをTraining dataとし，800パターンをテストデータとした．
		- バリデーションデータは使ってなさそう．validation Lossがbestのものを採用するとかの発想ではなく，200epoch固定で回したらしい．
	- ランダムスペックルを密度のdomainで加算した．  
	- single plane waveとthree plane waveの2種類で結果を比較してみた．
	<img src="https://github.com/Kotatsun/papers/blob/image/plane_wave.png" width="420"> <img src="https://github.com/Kotatsun/papers/blob/image/medium_condition.png" width="320">  

- ネットワーク構造:  
	 ・Network for single plane wave:		　　　　　・Network for three plane wave:  
	<img src="https://github.com/Kotatsun/papers/blob/image/single_network.png" width="220"> <img src="https://github.com/Kotatsun/papers/blob/image/middle_network.png" width="220">

- Test in Real data:
<img src="https://github.com/Kotatsun/papers/blob/image/Real_leg.png" width="320">
<br />

## 技術や手法の肝は



<br />

## 議論はある
- 中が均一なポリウレタンファントムは上手く音速分布が出力されなかった．
	- 学習時にランダムスペックルを加算しているからデータ性状が異なるためか．
<br />

## 次に読むべき論文は
- GANを初めて超音波に使った論文とか．音響媒質からB-mode Likeな画像を出力するものらしい．

[[57]](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8363780) F. Tom and D. Sheet, “Simulating patho-realistic ultrasound images using deep generative networks with adversarial learning,” in Biomedical Imaging (ISBI 2018), 2018 IEEE 15th International Symposium on. IEEE, 2018, pp. 1174–1177.

