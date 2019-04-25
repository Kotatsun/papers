# Reverberation Noise Suppression in the Aperture Domain Using 3D Fully Convolutional Neural Networks (Leandra, et al 2018, IEEE)
[Reverberation Noise Suppression in the Aperture Domain Using 3D Fully Convolutional Neural Networks](https://ieeexplore.ieee.org/document/8579995)
## ・どんなものか
超音波チャネルデータから、超音波画像の画質低下の原因となる残響ノイズを選択的に除去するための3D完全畳み込みニューラルネットワーク（3D-FCNN）を提案した。

## ・どうやって有効だと検証したか
Field II Proシミュレーションパッケージによるシミュレーションと、ATS 549ファントムを使って実験による検証もした。


## ・先行研究と比べて何がすごいか
残響ノイズの除去の手法には、
高周波パルスを低周波搬送波に結合する(Nasholm, et al 2009)、相互相関による多相APDフィルター{中心部の透過率は高く、周辺部に向かって透過率が低くなるフィルター}(Shin, et al 2016)、周波数空間予測フィルタリング(Shin, et al 2017)、周波数領域を利用したDNN(Luchies, et al 2018)などがあるが、本手法では再構成画像の高さ、幅、素子の受信信号(64×64×128)を入力に3D-FCNNを用いて残響ノイズを除去した。


## ・技術や手法の肝はどこか
一般的な画像処理の手法であるCNNを残響ノイズ除去に応用する際に、再構成画像の高さ、幅、素子の受信信号を入力とする3D-FCNNを用いた。


## ・議論はあるか
局所的なトランスデューサーの素子間における受信信号の比較が残響ノイズの同定・除去に重要であると示唆された。


## ・次に読むべき論文は
Luchies, et al 2018 あたり
