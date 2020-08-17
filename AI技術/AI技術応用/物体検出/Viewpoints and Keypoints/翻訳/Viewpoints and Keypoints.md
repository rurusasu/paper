# Viewpoints and Keypoints

# 備考

## 著者
Shubham Tulsiani，Jitendra Malik

## 掲載

"Viewpoints and keypoints", InComputerVision and Pattern Regognition (CVPR), 2015.

# Abstract
剛体オブジェクトのポーズ推定の問題を、粗いポーズを説明するための視点を決定することと、より細部をキャプチャするためのキーポイント予測の点で特徴付けます。 これらの両方のタスクに対処するには、2つの異なる設定、既知のバウンディングボックスによる制約付き設定、およびオブジェクトのポーズを同時に検出して正しく推定することを目的とする、より困難な検出設定を使用します。 これらのたたみ込み型ニューラルネットワークに基づくアーキテクチャを提示し、視点の推定を活用することで、局所的な外観に基づくキーポイント予測を大幅に改善できることを示します。 上記のタスクで最先端の技術を大幅に改善することに加えて、エラーモードとオブジェクト特性がパフォーマンスに及ぼす影響を分析して、この目標に向けた今後の取り組みを導きます。

# 3. Viewpoint Estimation
## 3.1. Formulation
剛体カテゴリのグローバルポーズ推定を定式化ポーズに対する視点を予測するものとして公式化します。 これは、方位角
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\phi" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\phi" title="\phi" /></a>
、仰角
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\varphi" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\varphi" title="\varphi" /></a>
、およびサイクロローテーション
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\psi" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\psi" title="\psi" /></a>
に対応する3つのオイラー角を決定することと同じです。 このオイラー角の予測を、クラス
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\{1,&space;\cdots&space;N_\theta&space;\}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;\{1,&space;\cdots&space;N_\theta&space;\}" title="\{1, \cdots N_\theta \}" /></a>
が
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_\theta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_\theta" title="N_\theta" /></a>
の不連続な角度ビンに対応する分類問題とする。オイラー角、つまりすべての視点は、回転行列によって同等に記述できることに注意してください。 視点、オイラー角、回転行列の概念を交換可能に使用します。

## 3.2. Network Architecture and Training

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c" title="N_c" /></a>
をオブジェクトクラスの数、
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a" title="N_a" /></a>
をインスタンスごとに予測される角度の数とします。クラスごとの出力単位の数は
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a&space;\ast&space;N_\theta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a&space;\ast&space;N_\theta" title="N_a \ast N_\theta" /></a>
であり、合計出力は
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c&space;\ast&space;N_a&space;\ast&space;N_\theta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c&space;\ast&space;N_a&space;\ast&space;N_\theta" title="N_c \ast N_a \ast N_\theta" /></a>
になります。ガーシックらと同様のアプローチを採用しています。 [11]そして、その重みがImagenet [5]分類タスクで事前トレーニングされたモデルから初期化されるCNNモデルを微調整します。 Krizhevskyら [23]（TNetと表示）およびSimonyanら [33]（ONetと表示）のアーキテクチャを実験しました。。私たちのネットワークのアーキテクチャは、
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c&space;\ast&space;N_a&space;\ast&space;N_\theta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_c&space;\ast&space;N_a&space;\ast&space;N_\theta" title="N_c \ast N_a \ast N_\theta" /></a>
出力ユニットを持つ追加の完全に接続されたレイヤーを備えた、対応する事前トレーニング済みネットワークと同じです。補足資料では、ネットワークアーキテクチャの代替の詳細な視覚化を提供しています。クラスごとに個別のCNNをトレーニングする代わりに、トレーニングレイヤーのクラスに対応する
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a&space;\ast&space;N_\theta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;N_a&space;\ast&space;N_\theta" title="N_a \ast N_\theta" /></a>
出力を選択的に考慮し、各角度予測のロジスティック損失を計算する損失レイヤーを実装します。これにより、すべてのクラスの視点を共同で予測できるCNNをトレーニングできるため、すべてのカテゴリで共有される特徴表現を学習できます。 Caffeフレームワーク[20]を使用して、上記のCNNから機能をトレーニングおよび抽出します。
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;IoU&space;>&space;0.7" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;IoU&space;>&space;0.7" title="IoU > 0.7" /></a>
の注釈付きバウンディングボックスとオーバーラップするジッターのあるグラウンドトゥルースバウンディングボックスでトレーニングデータを補強します。 Xiangら [37] PASCAL VOC 2012検出トレインのすべてのインスタンスに対応する
<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;(\phi,\varphi,\psi)" target="_blank"><img src="https://latex.codecogs.com/png.latex?\inline&space;\dpi{100}&space;\bg_white&space;\fn_jvn&space;(\phi,\varphi,\psi)" title="(\phi,\varphi,\psi)" /></a>
の注釈、検証セット、およびImageNet画像を提供します。 PASCALトレインセットとImageNetアノテーションを使用して上記のネットワークをトレーニングし、PASCAL VOC 2012検証セットアノテーションを使用してパフォーマンスを評価します。