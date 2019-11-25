# A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound (Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).)
### Reference
- Feigin-Almon, M., Freedman, D., & Anthony, B. W. (2019).
A Deep Learning Framework for Single-Sided Sound Speed Inversion in Medical Ultrasound. IEEE Transactions on Biomedical Engineering.
- https://ieeexplore.ieee.org/abstract/document/8772124

<br />

## どんなものか
<img src="https://github.com/Kotatsun/papers/blob/image/RF_from_three.png" width="220" style="float:right"> <img src="https://github.com/Kotatsun/papers/blob/image/ground_result.png" width="420" style="float:right">

- RF信号から媒質の音速分布を推定するDNNアーキテクチャを初めて構築した． 

- リアルタイム性あり．

- 応用を見据えた医学的な検討も充実していてGANの論文[*1](https://ieeexplore.ieee.org/document/8692835)よりもインパクトは大きそう．
<br />

## 研究背景，先行研究に対する新規性
- 超音波によって生体組織性状を定量的に評価する手法として組織の硬さ分布を画像化する超音波エラストグラフィがあるが，高出力が必要なためハイエンドモデルにしか搭載されておらず，フレームレートも低い．  
	　→ 生体情報を得るalternativeとして縦波音速分布を求めたい．


- 音速分布の繰り返し計算は計算コストが高く，リアルタイム性に欠ける．  
	　→DNNによるpredictionならリアルタイム(高フレームレート)な処理が可能．
<br />

## 手法・結果
- Simulation:

<img src="https://github.com/Kotatsun/papers/blob/image/plane_wave.png" width="420"> <img src="https://github.com/Kotatsun/papers/blob/image/medium_condition.png" width="320">  
	- リニアプローブを模した64素子で送信受信を行った．
	-  k-waveで6826パターンのシミュレーションを行い，6026パターンをTraining dataとし，800パターンをテストデータとした．
		- バリデーションデータは使ってなさそう．validation Lossがbestのものを採用するとかの発想ではなく，200epoch固定で回したらしい．
	- ランダムスペックルを密度のdomainで加算した．  
	- single plane waveのみのものと，three plane waveを用いて画像再構成を行ったものの結果を比較してみた．

- ネットワーク構造:  
・Network for single plane wave: ・Network for three plane wave:  
	<img src="https://github.com/Kotatsun/papers/blob/image/single_network.png" width="130">   <img src="https://github.com/Kotatsun/papers/blob/image/middle_network.png" width="130">
	- 異なる方向からの信号を複数入力とした場合に結果が向上するかを確認した．

- Test in Real data:

<img src="https://github.com/Kotatsun/papers/blob/image/neck.png" width="150"> <img src="https://github.com/Kotatsun/papers/blob/image/leg.png" width="150">
	
Cephasonics 128ch リニアプローブ(5MHz)を用いて，1)ポリウレタンphantom，2)首の結合部，3)ふくらはぎ のRF dataを取得し，テストを行った．
<br />

## 技術や手法の肝(有用な知見)
- 3方向からのplane waveによるRF信号を元に画像再構成を行うネットワークの検討を行なっており，異なる方向からの複数信号を統合して情報抽出を行う際の参考になりそう．
- 下の画像だとmiddleとendはほぼ等程度の性能を示した．startでも再構成ができないわけではない．
- 単純に特徴量抽出部分のパラメータ数の問題のような気もする．
<img src="https://github.com/Kotatsun/papers/blob/image/network_study.png" width="320">
<br />

## 議論はある
- 構築されたネットワークによって推定された音速分布は，深い領域ほど音速を低く見積もる傾向がある模様．
<br />

## 次に読むべき論文は
- GANを初めて超音波に使った論文とか．音響媒質からB-mode Likeな画像を出力するものらしい．

[[57]](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8363780) F. Tom and D. Sheet, “Simulating patho-realistic ultrasound images using deep generative networks with adversarial learning,” in Biomedical Imaging (ISBI 2018), 2018 IEEE 15th International Symposium on. IEEE, 2018, pp. 1174–1177.

## 参考文献
[[1]](https://ieeexplore.ieee.org/document/8692835)Nair, A. A., Tran, T. D., Reiter, A., & Bell, M. A. L. (2019, March). A Generative Adversarial Neural Network for Beamforming Ultrasound Images: Invited Presentation. In 2019 53rd Annual Conference on Information Sciences and Systems (CISS) (pp. 1-6). IEEE.
