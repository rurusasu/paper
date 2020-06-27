# BB8: A Scalable, Accurate, Robust to Partial Occlusion Method for Predicting the 3D Poses of Challenging Objects without Using Depth

# 備考
## 著者
Mahdi Rad, Vincent Lepetit

## 掲載
"BB8: A Scalable, Accurate, Robust to Partial Occlusion Method for Predicting the 3D Poses of Challenging Objects without Using Depth," Proc. The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 3828-3836, 2017.

# Abstract
カラー画像のみからの3Dオブジェクト検出と姿勢推定のための新しい方法を紹介します。最初にセグメンテーションを使用して、部分的なオクルージョンと雑然とした背景が存在する場合でも、2Dで対象のオブジェクトを検出します。最近のパッチベースの方法とは対照的に、「ホリスティック」アプローチに依存しています。3D境界のコーナーの2D投影の形で3Dポーズを予測するようにトレーニングされた畳み込みニューラルネットワーク（CNN）を検出されたオブジェクトに適用しますボックス。ただし、これは最近のT-LESSデータセットのオブジェクトを処理するのに十分ではありません。これらのオブジェクトは回転対称の軸を示し、2つの異なる姿勢でのそのようなオブジェクトの2つの画像の類似性により、CNNのトレーニングが困難になります。この問題を解決するには、トレーニングに使用するポーズの範囲を制限し、ポーズを推定する前に実行時にポーズの範囲を識別する分類子を導入します。また、予測されるポーズを調整するオプションの追加ステップを使用します。 LINEMODデータセットの最新技術を73.7％[2]から正しく登録されたRGBフレームの89.3％に改善します。また、カラー画像のみを使用して、オクルージョンデータセット[1]の結果を最初に報告しました。 T-LESSデータセットのいくつかのシーケンスで、平均してポーズ6D基準を通過するフレームの54％を取得します。これに対して、色と深度の両方を使用する同じシーケンスでの最新の[10]の67％と比較します。 。単一のネットワークを複数のオブジェクトに対して同時にトレーニングできるため、完全なアプローチもスケーラブルです。