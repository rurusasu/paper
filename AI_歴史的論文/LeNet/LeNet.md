Multilayer Neural Networks trained with the backpropagation algorithrn consitute the best example of a successful Gradient-Based Learning technique.
Given an appropriate network archtecture, Gradient-Based Learning algorithms can be used to synthesize a complex decision surface that can classify high-dimensional patterns such as handwritten characters, with minimal preprocessing.
This paper reviews various methods applied to handwritten character recognition and compares them on a standard handwritten digit recognition task.
Convolutional Neural Networks, that are specifically designed to deal with the variability of 2D shapes, are shown to outperform all other techniques.

> バックプロパゲーションアルゴリズムでトレーニングされたマルチレイヤーニューラルネットワークは、勾配ベースの学習手法の成功例として最適です。
> 適切なネットワークアーキテクチャがあれば、勾配ベースの学習アルゴリズムを使用して、最小限の前処理で手書き文字などの高次元のパターンを分類できる複雑な決定面を合成できます。
> このペーパーでは、手書き文字認識に適用されるさまざまな方法をレビューし、標準の手書き数字認識タスクでそれらを比較します。
> 2D形状の変動性に対処するように特別に設計された畳み込みニューラルネットワークは、他のすべての手法よりも優れていることが示されています。

Real-life document recognition systems are composed of multiple modules including firld extraction, segmentation, recognition, and language modeling.
A new learning paradigm, called Graph Transformer Networks (GTN), allows such multi-module systems to be trained globally using Gradient-Based methods so as to minimize an overall preformance measure.

> 実際のドキュメント認識システムは、フィールド抽出、セグメンテーション、認識、言語モデリングなどの複数のモジュールで構成されています。
> Graph Transformer Networks（GTN）と呼ばれる新しい学習パラダイムにより、このようなマルチモジュールシステムは、全体的なパフォーマンス測定を最小限に抑えるために、勾配ベースの方法を使用してグローバルにトレーニングできます。

Two systems for on-line handwriting recognition are described. 
Experiments demonstrate the advantage of global training, and the flexibility of Graph Transformer Networks.

> オンライン手書き認識のための2つのシステムについて説明します。
> 実験は、グローバルトレーニングの利点と、グラフトランスフォーマーネットワークの柔軟性を示しています。

A Graph Transformer Network for reading bank check is also described.
It uses Convolutional Neural Network character recognizers combined with global training techniques to provides record accuracy on business and personal checks.
It is deployed commercially and reads several million checks per day.

> 銀行小切手を読み取るためのグラフ変換ネットワークについても説明します。
> 畳み込みニューラルネットワークの文字認識機能をグローバルトレーニングテクニックと組み合わせて使用​​することで、ビジネスチェックと個人チェックの記録の正確性を提供します。
> 商業的に配備され、1日に数百万の小切手を読み取ります。

# Introduction
Over the last several years, machine learning techniques, particularly when applied to neural networks, have played an increasingly important role in the design of pattern recognition systems.
In fact, it could be argued that the availability of learning techniques has been a crucial factor in the recent success of pattern recognition applications such as continuous speech recognition and handwriting recognition.

> 過去数年にわたって、特にニューラルネットワークに適用される機械学習技術は、パターン認識システムの設計においてますます重要な役割を果たしてきました。
> 実際、連続音声認識や手書き認識などのパターン認識アプリケーションの最近の成功において、学習技術の利用可能性が重要な要素であると主張することができます。

The main message of this paper is that better pattern recognition systems can be built by relying more on automatic learning, and less on hand-designed heuristics.
This is made possible by recent progress in machine learning and computer technology. 
Using character recognition as a case study, we show that hand-crafted feature extraction can be advanctageously replaced by carefully designed learning machines that operate directly on pixel images.
Using document understanding as a case study, we show that the traditional way of building recognition systems by manually integrating individually designed modules can be replaced by a unified and well-principled design paradigm, called Graph Transformer Networks, that allows training all the modules to optimize a global performance criterion.

> このホワイトペーパーの主なメッセージは、自動学習に依存することで、より優れたパターン認識システムを構築できることです。
> これは、機械学習とコンピューター技術の最近の進歩によって可能になりました。
> ケーススタディとして文字認識を使用して、手作りの特徴抽出を、ピクセル画像を直接操作する慎重に設計された学習マシンに有利に置き換えることができることを示します。
> ドキュメントの理解をケーススタディとして使用して、個別に設計されたモジュールを手動で統合することで認識システムを構築する従来の方法は、グラフトランスフォーマーネットワークと呼ばれる、グローバルなパフォーマンス基準として統一された優れた原理の設計パラダイムに置き換えることができ、
すべてのモジュールをトレーニングして最適化できることを示します。

Since the early days of pattern recognition it has been known that the variability and richness of natural data, be it speech, glyphs, or other types of patterns, make it almost impossible to build an accurate recognition system entirely by hand.
Consequently, most pattern recognition systems are built using a combination of automatic learning techniques and hand-crafted algorithms.
The usual method of recognizing individual patterns consists in dividing the system into two main modules shown in figure 1.
The first module, called the feature extractor, transforms the input patterns so that they can be represented by lowdimensional vectors or short strings of symbols that (a) can be easily matched or compared, and (b) are relatively invariant with respect to transformations and distortions of the input patterns that do not change their nature.
The feature extractor contains most of the prior knowledge and is rather specific to the task.
It is also the focus of most of the design effort, bcause it is often entirely hand-crafted.
The classifier, on the other hand, is often general-propose and trainable.
One of the main problems with this approach is that the recognition accuracy is largely determined by the ability of the designer to come up with an appropriate set of features. 
This rurns out to be a daunting task which, unfortunately, must be redone for each new problem.
A large amount of the pattern recognition literature is devoted to describing and comparing the relative merits of different feature sets for particular tasks.

> パターン認識の初期の頃から、音声、グリフ、その他の種類のパターンなどの自然データの変動性と豊富さにより、正確な認識システムを完全に手作業で構築することはほとんど不可能であることが知られています。
> その結果、ほとんどのパターン認識システムは、自動学習技術と手作りアルゴリズムの組み合わせを使用して構築されています。
> 個々のパターンを認識する通常の方法は、システムを図1に示す2つのメインモジュールに分割することです。
> 最初のモジュールは特徴抽出と呼ばれ、入力パターンを変換して、（a）簡単に照合または比較でき、（b）変換に関して比較的不変であるその性質を変更しない入力パターンの歪みを、低次元ベクトルまたはシンボルの短い文字列で表すことができるようにします。
> 特徴抽出には、ほとんどの事前知識が含まれており、タスクにかなり固有のものです。
> それはまた、多くの場合完全に手作りであるため、ほとんどの設計作業の焦点でもあります。
> 一方、分類子は、一般的に提案され、トレーニング可能です。
> このアプローチの主な問題の1つは、認識の精度が、適切な一連の機能を考案する設計者の能力によって大きく左右されることです。
> これは、残念ながら、新しい問題ごとにやり直さなければならない困難な作業であることが判明しました。
> パターン認識に関する文献の多くは、特定のタスクのさまざまな機能セットの相対的なメリットを説明および比較するために使用されています。

Historically, the need for appropriate feature extractors was due to the fact that the learning techniques used by the classifiers were limited to low-dimensional spaces used by the classes.
A combination of three factors have changed this vision over the last decade.
First, the availability of low-cost machines with fast arithmetic units allows to rely more on brute-force "numerical" methods than on algorithmic refinements.
Second, the availability of large databases for problems with a large market and wide interest, such as handwriting recognition, has enabled designers to rely more on real data and less on hand-crafted feature extraction to build recognition systems.
The third and very important factor is the availability of powerful machine learning techniques that can handle high-dimensional inputs and can generate intricate decision functions when fed with these large data sets.
It can be argued that the recent progress in the accuracy of speech and handwriting recognition sysytems can be attributed in large part to an increased reliance on learning techniques and large training data sets.
As evidence to this fact, a large proportion of modern commercial OCR(Optical character recognition) systems use some form of multi-layer Neural Network trained with back-propagation.

> 歴史的に、適切な特徴抽出器の必要性は、分類子によって使用される学習手法がクラスによって使用される低次元空間に制限されていたという事実によるものでした。
> 3つの要因の組み合わせにより、この10年間でこのビジョンが変わりました。
> 第一に、高速演算ユニットを備えた低コストのマシンを利用できることで、アルゴリズムの改良よりも、総当たりの「数値」手法を利用することができます。
> 第二に、手書き認識などの大きな市場と幅広い関心のある問題に対応する大規模なデータベースの可用性により、設計者は、認識システムを構築するために、手作りの特徴抽出に頼ることなく、実際のデータに頼るようになりました。
> 3番目の非常に重要な要素は、高次元の入力を処理でき、これらの大規模なデータセットを入力したときに複雑な決定関数を生成できる強力な機械学習技術が利用できることです。
> 音声および手書き認識システムの正確さにおける最近の進歩は、主に、学習技術および大規模なトレーニングデータセットへの依存度の増加に起因する可能性があると主張できます。
> この事実の証拠として、現代の商用OCR（光学式文字認識）システムの大部分は、バックプロパゲーションでトレーニングされた何らかの形の多層ニューラルネットワークを使用しています。

In this study, we consider the tasks of handwritten character recognition (Sections I and II) and compare the performance of several learning techniques on a benchmark data set for handwritten digit recognition (Section III).
While more automatic learning is beneficial, no learning technique can succed without a minimal amount of oprior knowledge about the task.
Convolutional Neural Networks introduced in Section II are an example of specialized neural network archtectures which incorporate knowledge about the invariances of 2D shapes by using local connection patterns, and by imposing constraints on the weights.
A comparison of several methods for isolated handwritten digit recognition is presented in section III.
To go from the recognition of words and sentences in documents, the idea of combining multiple modules trained to reduce the overall error is introduced in Section IV. 
Recognizing variable-length objects such as handwritten words using multi-module systems is best done if the modules manipulate directed graphs.
This leads to the concept of trainable *Graph Transformer Network* (GTN) also introduced in section IV.
Section V describes the now classical method of heuristic over-segmentation for recognizing words or other character strings.
Discriminative and non-discriminative gradient-based techniques for training a recognizer at the word level without requring manual segmentation and labeling are presented in Section VI.
Section VII presents the promising Space-Displacement Neural Network approach that eliminates the need for segmentation heuristics by scanning a recognizer at all possible locations on the input.
In section VIII, it is shown that trainable Graph Transformer Networks can be formulated as multiple generalized transductions, based on a general graph composition algorithm. 
The connections between GTNs and Hidden Markov Models, commonly used in speech recognition is also treated.
Section IX describes a globally trained GTN system for recognizing handwriting entered in a pen computer.
This problem is known as "on-line" handwriting recognition, since the machine must produce immediate feedback as the user writes.
The core of the system is a Convolutional Neural Network.
The results clearly demonstrate the advantages of training on pre-segmented, hand-labeled, isolated characters.
Section X describes a complete GTN-based system for reading handwritten and machine-printed bank checks.
The core of the system is the Concolutional Neural Network called LeNet-5 described in Section II.
This system is in commerical use in the NCR Corporation line of check recognition systems for the banking industry.
It is reading millions of checks per month in several banks across the United States.

> この研究では、手書き文字認識のタスク（セクションIおよびII）を検討し、手書き数字認識のベンチマークデータセット（セクションIII）でいくつかの学習手法のパフォーマンスを比較します。
> 自動学習の方が効果的ですが、タスクに関する最小限の知識がなければ、学習テクニックを成功させることはできません。
> セクションIIで紹介された畳み込みニューラルネットワークは、ローカル接続パターンを使用し、重みに制約を課すことにより、2D形状の不変性に関する知識を組み込んだ特殊なニューラルネットワークアーキテクチャの例です。
> 孤立した手書き数字認識のいくつかの方法の比較をセクションIIIに示します。
> 文書内の単語と文の認識から移行するために、全体的なエラーを削減するようにトレーニングされた複数のモジュールを組み合わせるというアイデアがセクションIVで紹介されています。
> マルチモジュールシステムを使用した手書き単語などの可変長オブジェクトの認識は、モジュールが有向グラフを操作する場合に最適です。
> これは、セクションIVでも紹介したトレーニング可能なグラフ変換ネットワーク（GTN）の概念につながります。
> セクションVでは、単語やその他の文字列を認識するための、今や古典的な発見的オーバーセグメンテーション方法について説明します。
> 手動のセグメンテーションとラベリングを必要とせずに、単語レベルで認識機能をトレーニングするための、差別的および非差別的な勾配ベースの手法をセクションVIに示します。
> セクションVIIでは、入力の可能なすべての場所で認識機能をスキャンすることにより、セグメンテーションヒューリスティックの必要性を排除する有望な空間変位ニューラルネットワークアプローチを紹介します。
> セクションVIIIでは、一般的なグラフ構成アルゴリズムに基づいて、トレーニング可能なグラフ変換ネットワークを複数の一般化された変換として定式化できることを示しています。
> GTNと音声認識で一般的に使用される隠れマルコフモデル間の接続も処理されます。
> セクションIXでは、ペンコンピュータに入力された手書き文字を認識するためのグローバルにトレーニングされたGTNシステムについて説明します。
> この問題は「オンライン」手書き認識として知られています。これは、ユーザーが書いているときにマシンが即座にフィードバックを生成する必要があるためです。
> システムの中核は、畳み込みニューラルネットワークです。
> 結果は、事前にセグメント化された、手でラベル付けされた、孤立したキャラクターのトレーニングの利点を明確に示しています。
> セクションXでは、手書きおよび機械印刷の銀行小切手を読み取るための完全なGTNベースのシステムについて説明します。
> システムの中核は、セクションIIで説明されているLeNet-5と呼ばれる協同ニューラルネットワークです。
> このシステムは、銀行業界向けのNCR Corporationの小切手認識システムのラインで商用利用されています。
> 全米のいくつかの銀行で毎月数百万の小切手を読んでいます。

# A. Learning from Data
There are several approaches to automatic machine learning, but one of the most successful approaches, popularized in recent years by the neural network community, can be called "numerical" or *gradient-based learning*.
The learning machine computes a function $Y^{p} = F(Z^p, W)$ where $Z^{p}$ is the p-th input pattern, and *W* represents the collection of adjustable parameters in the system.
In a pattern recognition setting, the output $Y^{p}$ may be interpreted as the recognition setting, the output $Z^{p}$, or as scores or probabilities associated with each class.
A loss function $E^{p} = D(D^{p}, F(W, Z^{p}))$, measures the discrepancy between $D^{p}$, the "correct" or desired output for pattern $Z^{p}$, and the output produced by the system.
The average loss function $E_{train}(W)$ is the average of errors $E^{p}$, over a set of labeled examples called the training set {$(Z^1, D^1), ....(Z^{p}, D^{P})$}.
In peactice, the performance of the system on a training set is of little interset.
The more relevant measure is the error rate of the system in the field, where it would be used in practice.
This performance is estimated by measuring the accuracy on a set of samples disjoint from the training set, called the test set.
Much theoretical and ecperimental work [3], [4], [5] has shown that the gap between the expected error rate on the test set $E_{test}$ and the error rate on the training set $E_{train}$ decreases with the number of training samples approximately as 
$$ E_{test}-E_{train} = k(h/P)^\alpha $$
where $P$ is the number of training samples, h is a measure of "effective capacity" or complexity of the machine [6], [7], $\alpha$ is a number between $0.5$ and $1.0$ and $k$ is a constant.
This gap always decreases when the number of training samples increas.
Furthermore, as the capacity h increases, $E_{train}$ decreases.
Therefore, when increasing the capacity h, there is a trade-off between the decrease of $E_{train}$ and the increase of the gap, with an optimal value of hte capacity $h$ that achieves the lowest generalizaiton error $E_{test}$.

> 自動機械学習にはいくつかのアプローチがありますが、ニューラルネットワークコミュニティによって近年普及している最も成功したアプローチの1つは、「数値」または勾配ベースの学習と呼ばれます。
> 学習マシンは次の関数を計算します。Z^Pはp番目の入力パターンで、Wはシステムないの調整可能なパラメータのコレクションを表します。
> パターン認識設定では、出力Y^{p}は認識設定、 出力Z^{p}、または各クラスに関連づけられたスコアもしくは確率として解釈される場合があります。
> 損失関数$E$はパターン$Z^{p}$の「正しい」または望ましい出力である$D^{p}$の間の不一致を測定します。
> 平均損失関数$E_{train}$は、トレーニングセットと呼ばれるラベル付けされた例のセットに対するエラー$E^{p}$の平均です。
> 実際には、トレーニングセットでのシステムのパフォーマンスは、ほとんど干渉しません。
> より適切な尺度は、実際に使用されるフィールドでのシステムのエラー率です。
> このパフォーマンスは、テストセットと呼ばれるトレーニングセットから切り離されたサンプルのセットの精度を測定することによって推定されます。
> 多くの理論的および実験的研究[3]、[4]、[5]は、テストセット$E_{test}$の予想エラー率とトレーニングセット$E_{train}$のエラー率のギャップを示しています。トレーニングサンプルの数がほぼ次のように減少します。$E_{test}-E_{train} = k(h/P)^\alpha$
> ここで、$P$はトレーニングサンプルの数、$h$は「有効容量」またはマシンの複雑さの尺度です[6]、[7]、$\alpha$は$0.5$から$1.0$および$k$の間の数値（定数）です。
> このギャップは、トレーニングサンプルの数が増えると常に減少します。
> さらに、容量hが増加すると、$E_{train}$は減少します。
> したがって、容量hを増やす場合、$E_{train}$の減少とギャップの増加の間にはトレードオフがあり、最小の一般化誤差$E_{test}$を達成する最適値容量$h$があります。


# A. Convolutional Networks
Convolutional Networks combine three architectureal ideas to ensure some degree of shift, scale, and distortion invariance: *local receptive fields, shared weights* (or weight replication), and spatial or temporal *sub-sampling*.
A typical convolutional network for recognizing characters, dubbed LeNet-5, is shown in gigure 2.
The input plane recives images of characters that are approcimately sizenormalized and centered.
Each unit in a layer receives inputs from a set of units located in a small neighborhood in the previous layer.
The idea of connecting units to local receptive fields on the input goes back to the Perceptron in the early 60s, and was almost simultaneous with Huble and Wiesel's discovery of locally-sensitive, orientation-selective neurons in the cat's visual system [30].
Local connections have been used many times in neural models of visual learning [31], [32], [18], [33], [34], [2].
With local receptive fields, neurons can extract elementary visual feat ures such as oriented edges, end-points, corners(or similar features in other signals such as speech spectrograms).
These features are then combined by the subsequent layers in order to detect higher-order features.
As stated earlier, distortions or shifts of the input can cause the position of salient features to vary.
In addition, elementary feature detectors that are useful on one part of the image are likely to be useful across the entire image.
This knowledge can be applied by forcing a set of units, whose receptive fields are located at different places on hte image, to have identical weight vectors [32], [15], [34].
Units in a layer are organized in planes within which all the units share the same set of weights.
The set of outputs of the units in such a plane is called a *feature map*.
Units in a feature map are all constrained to perform the same operation on different parts of the image.
A complete convolutional layer is composed of several feature maps (with different weight vectors), so that multiple features can be extracted at each location.
A concrete example of this is the first layer of LeNet-5 shown in Figure 2.
Units in the first hidden layer of LeNet-5 are organized in 6 planes, each of which is a feature map.
A unit in a feature map has 25 inputs connected to a 5 by 5 area in the input, called the *receptive filed* of the unit.
Each unit has 25 inputs, and therefore 25 trainable coefficients plus a trainable bias.
The receptive fields of contiguous units in a feature map are centered on correspondingly contiguous units in the previous layer.
Therefore receptive fields of neighboring units overlap.
For example, in the first hidden layer of LeNet-5, the receptive fields of horizontally contiguous units overlap by 4 columns and 5 rows.
As stated earlier, all the units in a feature map share the same set of 25 weights and the same bias so they detect the same feature at all possible locations on the input. 
The other feature maps in the layer use different sets of weights and biases, thereby extracting different types of local features.
In the case of LeNet-5, at each input location six different types of features are extracted by six units in identical locations in the six feature maps.
A sequential implementation of a feature map would scan the input image with a single unit that has a local receptive field, and store teh states of this unit at corresponding locations in the feature map.
This operation is equivalent to a convolution, followed by an additive bias and squashing function, hence the name *convolutional network*.
The kernel of the convolution is the set of connection weights used by the units in the feature map.
An interestin property of convolutional layers is that if the input image is shifted, the feature map output will be shifted by the same amount, but will be left unchanged otherwise.
This property is at the absis of the robustness of convolutional networks to shifts and distortions og the input.

> 畳み込みネットワークは、3つのアーキテクチャのアイデア（局所受容野、共有重み（または重み複製）、および空間的または時間的サブサンプリング）を組み合わせて、ある程度のシフト、スケール、および歪みの不変性を確保します。
> 文字を認識するための典型的な畳み込みネットワーク（LeNet-5と呼ばれます）を図2に示します。
> 入力プレーンは、適切にサイズが正規化され、中央に配置された文字の画像を受け取ります。
> 層の各ユニットは、前の層の小さな近隣にある一連のユニットから入力を受け取ります。
> ユニットを入力のローカル受容野に接続するという考えは、60年代前半のパーセプトロンにまで遡り、ハブルとヴィーゼルが猫の視覚システムで局所的に敏感で向き選択的なニューロンを発見したこととほぼ同時期にありました[30]。
> ローカル接続は、視覚学習の神経モデルで何度も使用されています[31]、[32]、[18]、[33]、[34]、[2]。
> ニューロンは、局所的な受容野を利用して、方向付けされたエッジ、エンドポイント、コーナー（または音声スペクトログラムなどの他の信号における同様の機能）などの基本的な視覚的特徴を抽出できます。
> これらの機能は、高次の機能を検出するために、後続のレイヤーによって結合されます。
> 前述のように、入力の歪みまたはシフトにより、顕著な特徴の位置が変化する可能性があります。
> さらに、画像の一部で役立つ基本的な特徴検出器は、画像全体で役立つ可能性があります。
> この知識は、受容野が画像の異なる場所にあるユニットのセットに、同じ重みベクトルを強制することによって適用できます[32]、[15]、[34]。
> レイヤー内のユニットは、すべてのユニットが同じ重みのセットを共有する平面に編成されます。
> そのような平面内のユニットの出力のセットは、特徴マップと呼ばれます。
> 特徴マップの単位はすべて、画像の異なる部分で同じ操作を実行するように制限されています。
> 完全なたたみ込み層は、画像のさまざまな部分で同じ操作を行ういくつかの機能で構成されます。
> 完全なたたみ込み層は、さまざまな重みベクトルを持ついくつかの特徴マップで構成されているため、各場所で複数の特徴を抽出できます。
> この具体例は、図2に示すLeNet-5の最初の層です。
> LeNet-5の最初の非表示層にあるユニットは、6つの平面で構成されており、それぞれが特徴マップです。
> 特徴マップ内のユニットには25の入力があり、ユニットの受容フィールドと呼ばれる、入力内の5 x 5の領域に接続されています。
> 各ユニットには25の入力があるため、25のトレーニング可能な係数とトレーニング可能なバイアスがあります。
> フィーチャーマップ内の隣接するユニットの受容フィールドは、前のレイヤー内の対応する隣接するユニットに集中しています。
> したがって、隣接するユニットの受容野は重複しています。
> たとえば、LeNet-5の最初の非表示層では、水平方向に隣接するユニットの受容野は4列と5行で重なります。
> 前述のように、特徴マップのすべてのユニットは、25の重みと同じバイアスの同じセットを共有するため、入力のすべての可能な場所で同じ特徴を検出します。
> レイヤー内の他の特徴マップは、異なるセットの重みとバイアスを使用して、異なるタイプのローカル特徴を抽出します。
> LeNet-5の場合、各入力位置で、6つの異なるタイプの特徴が、6つの特徴マップの同じ位置にある6つのユニットによって抽出されます。
> 特徴マップの順次実装では、局所的な受容野を持つ単一のユニットで入力画像をスキャンし、このユニットの状態を特徴マップの対応する場所に保存します。
> この操作は畳み込みに相当し、その後に追加のバイアスとスカッシング関数(活性化関数？)が続くため、畳み込みネットワークと呼ばれます。
> コンボリューションのカーネルは、機能マップのユニットで使用される接続の重みのセットです。
> たたみ込み層の興味深い特性は、入力画像がシフトされると、フィーチャマップ出力は同じ量だけシフトされますが、それ以外の場合は変更されないままです。
> このプロパティは、入力のシフトと歪みに対する畳み込みネットワークの堅牢性の基本です。