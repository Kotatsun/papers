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

- ビームフォーミングを施していないsingle plane waveによるRaw RF信号からend-to-endで情報抽出が行われる．


<br />

## 手法
- Data Set:
![sim_pattern](https://github.com/Kotatsun/papers/blob/image/GAN_paper_simulation_pattern.png)
  - Field IIで 50,000パターンのシミュレーションを行ない，40,000件をトレーニングデータ，10,000件をバリデーションデータとし，GANのネットワークを学習．

  - テストデータ1: トレーニングデータのConditionの中からランダムに選択し，100パターンのシミュレーションからを作成．  
     - (→ これはトレーニングデータの中に全く同じ条件のデータが含まれている可能性があるのでテストデータによる検証として適切と言えるのか？)
 
  - テストデータ2: CIRS 054GSファントムの円形断面を画像化し，シミュレーションでのテストデータとして用いた．

- ネットワーク構造:
  - ジェネレータ： U-net(backbone: VGG13+BatchNorm)でRF信号を入力とし，B-mode画像[出力1]とセグメンテーション画像[出力2]を出力する．  
              損失関数 = 出力1のL1誤差 + 出力2のDise係数 + ディスクリミネータのBinaryCrossEntropy×0.5．   
              
  - ディスクリミネータ： VGG13+BatchNormでRF信号，b-mode画像，セグメンテーション画像を入力とし，RealとFakeの２値分類を行う．  
                   損失関数 = RealとFakeのBinaryCrossEntropy．

- テストデータの評価:
  - B-mode画像のPSNR(Peak Signal-to-Noise Ratio)と，セグメンテーション画像のDise係数を評価．

<br />

## 技術や手法の肝(有用な知見)
- B-mode画像とセグメンテーション画像を出力するネットワークにおいて，encoder,decoder部分を共有(特徴量の共有)することが出力画像の画質向上に寄与している．
  - つまり別々で画像を出力するネットワークを学習するより，ネットワークを共有して同時に出力する方が特徴量抽出に対する学習が上手く進む．
  
- ディスクリミネータを用いた方が，つまりGANのフレームワークを用いた方が，とりわけセグメンテーションの結果が向上する．
  - ただしディスクリミネータのLossのみをジェネレータの学習に用いると，学習は上手くいかない．

- ディスクリミネータの学習において入力にRF信号を用いない場合，ジェネレータが毎回同じ画像を出力するモード破壊のような現象が生じた．

<br />

## 議論はあるか
- なんかRFから再構成画像へのend-to-endはできそうだよねという結論．

- 今回は円形の構造体しか扱っていないので，あとはどの程度複雑な構造をDNNは表現できるかという問題だろうか．

<br />

## 次に読むべき論文は
- 先行研究のところで紹介していた他のDNN論文とか．個人的に気になるのは[12]の[Sound speed inversionのやつ](https://arxiv.org/pdf/1810.00322.pdf)．  


[6]Arun Asokan Nair, Trac D Tran, Austin Reiter, and Muyinatu A Lediju
Bell, “A deep learning based alternative to beamforming ultrasound
images,” in 2018 IEEE International Conference on Acoustics, Speech
and Signal Processing (ICASSP). IEEE, 2018, pp. 3359–3363.

[7]Arun Asokan Nair, Mardava Rajugopal Gubbi, Trac Duy Tran, Austin
Reiter, and Muyinatu A Lediju Bell, “A fully convolutional neural network for beamforming ultrasound images,” in 2018 IEEE International
Ultrasonics Symposium (IUS). IEEE, 2018, pp. 1–4

[8]Adam C Luchies and Brett C Byram, “Deep neural networks for
ultrasound beamforming,” IEEE transactions on medical imaging, vol.
37, no. 9, pp. 2010–2021, 2018.

[9]Adam C Luchies and Brett C Byram, “Training improvements for ultrasound beamforming with deep neural networks,” Physics in medicine
and biology, 2019.

[10]Sanketh Vedula, Ortal Senouf, Grigoriy Zurakhov, Alex Bronstein, Oleg
Michailovich, and Michael Zibulevsky, “Learning beamforming in
ultrasound imaging,” arXiv preprint arXiv:1812.08043, 2018.

[11]Maxime Gasse, Fabien Millioz, Emmanuel Roux, Damien Garcia, Herve´
Liebgott, and Denis Friboulet, “High-quality plane wave compounding
using convolutional neural networks,” IEEE transactions on ultrasonics,
ferroelectrics, and frequency control, vol. 64, no. 10, pp. 1637–1639,
2017.

[12]Micha Feigin, Daniel Freedman, and Brian W Anthony, “A deep
learning framework for single sided sound speed inversion in medical
ultrasound,” arXiv preprint arXiv:1810.00322, 2018.

[13]Leandra L Brickson, Dongwoon Hyun, and Jeremy J Dahl, “Reverberation noise suppression in the aperture domain using 3d fully
convolutional neural networks,” in 2018 IEEE International Ultrasonics
Symposium (IUS). IEEE, 2018, pp. 1–4.

[14]Sanketh Vedula, Ortal Senouf, Alex M Bronstein, Oleg V Michailovich,
and Michael Zibulevsky, “Towards ct-quality ultrasound imaging using
deep learning,” arXiv preprint arXiv:1710.06304, 2017.

[15]Yeo Hun Yoon, Shujaat Khan, Jaeyoung Huh, and Jong Chul Ye, “Deep
learning in rf sub-sampled b-mode ultrasound imaging,” arXiv preprint
arXiv:1712.06096, 2017.

[16]Walter Simson, Magdalini Paschali, Nassir Navab, and Guillaume
Zahnd, “Deep learning beamforming for sub-sampled ultrasound data,”
in 2018 IEEE International Ultrasonics Symposium (IUS). IEEE, 2018,
pp. 1–4.
