# A Generative Adversarial Neural Network for Beamforming Ultrasound Images (Nair, A. A., Tran, T. D., Reiter, A., & Bell, M. A. L. (2019, March).)
### Reference
- Nair, A. A., Tran, T. D., Reiter, A., & Bell, M. A. L. (2019, March).
A Generative Adversarial Neural Network for Beamforming Ultrasound Images: Invited Presentation. In 2019 53rd Annual Conference on Information Sciences and Systems (CISS) (pp. 1-6). IEEE.
- https://ieeexplore.ieee.org/document/8692835

<br />

## どんなものか
- 従来の超音波画像再構成手法の代用としてDNNが機能することを主張している.

- DNNは超音波RF信号からB-mode画像とCystのセグメンテーション画像を出力するよう学習された．

- DNNアーキテクチャにはGANが用いられた．


<br />

## 研究背景，先行研究に対する新規性
- 複数の平面波音波照射を組み合わせ画質を向上させる従来の手法は，画像品質とフレームレートの間にトレードオフが存在する．

- ビームフォーミングのパラメータ抽出や，ノイズ除去，音速分布の推定[[1](https://ieeexplore.ieee.org/abstract/document/8772124)]にDNNを用いる先行研究とは異なる．

- ビームフォーミングを施していない単一平面波によるRaw RF信号からend-to-endで情報抽出が行われる．


<br />

## 手法
- Field IIで 50,000パターンのシミュレーションを行ない，40,000件をトレーニングデータ，10,000件をバリデーションデータとし，GANのネットワークを学習．

- トレーニングデータのConditionの中からランダムに選択し，100パターンのシミュレーションからテストデータを作成．  
 - (→ これはトレーニングデータの中に全く同じ条件のデータが含まれている可能性があるのでテストデータによる検証として適切と言えるのか？)
 
- CIRS 054GSファントムの円形断面を画像化し，シミュレーションでのテストデータとして用いた．

- ネットワークの構造は以下  
  - ジェネレータ： U-net(backbone: VGG13+BatchNorm)でRF信号を入力とし， B-mode画像[出力1]とセグメンテーション画像[出力2]を出力する． 損失関数は出力1のL1誤差， 出力2のDise係数， ディスクリミネータのBinaryCrossEntropy×0.5．   
  - ディスクリミネータ： VGG13+BatchNormで２値分類を行う． 損失関数はRealとFakeのBinaryCrossEntropy．

- テストデータの出力の評価はB-mode画像のPSNR(Peak Signal-to-Noise Ratio)と， セグメンテーション画像のDise係数で行なった．

<br />

## 技術や手法の肝は
・


<br />

## 議論はある
・

<br />

## 次に読むべき論文は
・


