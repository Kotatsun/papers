# Beamforming and Speckle Reduction Using Neural Networks (Dongwoon Hyun, Leandra L. Brickson, et al. 2018, IEEE)
### Reference
- Beamforming and Speckle Reduction Using Neural Networks [Dongwoon Hyun, Leandra L. Brickson, Kevin T. Looby, and Jeremy J. Dahl. IEEE Transactions on Ultrasonics, Ferroelectrics, and Frequency Control, vol. 66, no. 5, pp. 898-910, May 2019.]
- https://ieeexplore.ieee.org/document/8663450

<br />

## どんなものか
・超音波チャネルデータから、超音波画像の画質低下の原因となる多重反射によるクラッターノイズを選択的に除去するための3D完全畳み込みニューラルネットワーク（3D-FCNN）を提案した。

・モデルの学習において、生体を模したモデルにおける超音波シミュレーションで得られたBモード画像を用いるのではなく、一般的な画像データを用いており、画像に対して各ピクセルの輝度値をその点における散乱体の反射率だと考えたモデルを考え、超音波シミュレーションを行って得られたBモード画像を用いている。

・このため、Bモード画像の多重反射によるノイズの除去に対して高い汎化性能を有していることが考えられる。


<br />

## どうやって有効だと検証したか
Field II Proシミュレーションパッケージによるシミュレーションと、ATS 549ファントムを使って実験による検証もした。

<br />

## 先行研究と比べて何がすごいか
ノイズの除去の手法には、

- 高周波パルスを低周波搬送波に結合する(Nasholm, et al. 2009)
- 相互相関による多相APDフィルター{中心部の透過率は高く、周辺部に向かって透過率が低くなるフィルター}(Shin, et al. 2016)
- 周波数空間予測フィルタリング(Shin, et al. 2017)
- 周波数領域を利用したDNN(Luchies, et al. 2018)

などがあるが、本手法では再構成画像の高さ、幅、素子の受信信号(画素1つに対応する128個の素子信号って何?)(64×64×128)を入力に3D-FCNNを用いてクラッターノイズを除去した。

<br />

## 技術や手法の肝はどこか
一般的な画像処理の手法であるCNNをクラッターノイズ除去に応用し、再構成画像の高さ、幅、素子の受信信号(これは何？)を入力とする3D-FCNNを用いてみたところ、いい感じにノイズが低減された。

<br />

## 議論はあるか
ネットワークはトランスデューサーの素子入力のカーネルサイズが大きくなるように学習され、素子間における受信信号の局所的な比較がクラッターノイズの同定・除去に重要であると示唆された。

<br />

## 次に読むべき論文は
Luchies, et al 2018 あたり

<br />

## 参照
1. [Transmit beams adapted to reverberation noise suppression using dual-frequency SURF imaging](https://ieeexplore.ieee.org/document/5306759) (Nasholm, et al. 2009)
2. [Ultrasonic Reverberation Clutter Suppression Using Multiphase Apodization With Cross Correlation ](https://ieeexplore.ieee.org/document/7529167) (Shin, et al. 2016)
3. [Spatial Prediction Filtering of Acoustic Clutter and Random Noise in Medical Ultrasound Imaging](https://ieeexplore.ieee.org/document/7570215) (Shin, et al. 2017)
4. [Deep Neural Networks for Ultrasound Beamforming](https://ieeexplore.ieee.org/document/8092159) (Luchies, et al. 2018)
