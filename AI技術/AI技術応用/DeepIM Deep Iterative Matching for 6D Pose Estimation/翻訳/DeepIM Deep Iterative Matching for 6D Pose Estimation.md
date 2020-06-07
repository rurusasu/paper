# DeepIM: Deep Iterative Matching for 6D Pose Estimation

# 備考
## 著者
Yi Li, Gu Wang, Xiangyang Ji, Yu Xiang, Dieter Fox

## 掲載
"DeepIM: Deep iterative matching for6D pose estimation," In: European Conference on Computer Vision (ECCV), pp. 1-16, 2018.

# Abstract
画像からオブジェクトの6Dポーズを推定することは、ロボット操作や仮想現実などのさまざまなアプリケーションで重要な問題です。画像からオブジェクトポーズへの直接回帰では精度が制限されますが、レンダリングされたオブジェクトの画像を入力画像と照合すると、正確な結果が得られます。この作業では、DeepIMという名前の6Dポーズマッチング用の新しいディープニューラルネットワークを提案します。初期姿勢推定が与えられた場合、ネットワークは、レンダリングされた画像を観察された画像と照合することにより、姿勢を反復的に調整することができます。ネットワークは、3Dの位置と3Dの向きの絡まりのない表現と反復トレーニングプロセスを使用して、相対ポーズ変換を予測するようにトレーニングされます。 6Dポーズ推定に一般的に使用される2つのベンチマークでの実験は、DeepIMが最新の方法よりも大幅に改善されていることを示しています。さらに、DeepIMが以前に表示されなかったオブジェクトと一致できることを示します。