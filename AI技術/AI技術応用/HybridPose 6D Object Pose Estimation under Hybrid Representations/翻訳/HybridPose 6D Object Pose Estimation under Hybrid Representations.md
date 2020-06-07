# HybridPose 6D Object Pose Estimation under Hybrid Representations

# 備考


## 著者
Chen Song, Jiaru Song, Qixing Huang

## 掲載
Hybridpose: 6d object pose estimation under hybridrepresentations, arXiv:2001.01869, 2020.

# Abstract
新しい6Dオブジェクトポーズ推定アプローチであるHybridPoseを紹介します。 HybridPoseは、ハイブリッド中間表現を利用して、キーポイント、エッジベクトル、対称性の対応など、入力画像のさまざまな幾何学的情報を表現します。ユニタリ表現と比較すると、ハイブリッド表現では、1つのタイプの予測表現が不正確な場合（たとえば、オクルージョンのため）、ポーズ回帰でより多様な機能を利用できます。 HybridPoseで使用されるさまざまな中間表現は、すべて同じ単純なニューラルネットワークで予測でき、予測された中間表現の外れ値は、堅牢な回帰モジュールによってフィルター処理されます。最先端のポーズ推定アプローチと比較して、HybridPoseは実行時間において同等であり、はるかに正確です。たとえば、Occlusion Linemod [3]データセットでは、このメソッドは30 fpsの予測速度を79.2％の平均ADD（-S）精度で達成します。これは、現在の最先端のアプローチから67.4％の改善を表します。 HybridPoseの実装は、https://github.com/chensong1995/HybridPose で入手できます。