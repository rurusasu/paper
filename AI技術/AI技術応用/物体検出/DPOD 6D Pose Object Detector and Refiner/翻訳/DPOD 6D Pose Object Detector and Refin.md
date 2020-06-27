# DPOD 6D Pose Object Detector and Refiner

# 備考

[元論文](https://github.com/rurusasu/paper/blob/master/AI%E6%8A%80%E8%A1%93/AI%E6%8A%80%E8%A1%93%E5%BF%9C%E7%94%A8/DPOD%206D%20Pose%20Object%20Detector%20and%20Refiner/%E5%85%83%E8%AB%96%E6%96%87/DPOD%206D%20Pose%20Object%20Detector%20and%20Refiner.pdf)

## 著者
Sergey Zakharov, Ivan Shugurov, Slobodan Ilic

## 掲載
"DPOD: 6D Pose Object Detector and Refiner," Proc. The IEEE International Conference on Computer Vision (ICCV), pp. 1941-1950, 2019.

# Abstract
この論文では、RGB画像からの3Dオブジェクト検出と6D姿勢推定のための新しい深層学習手法を紹介します。 DPOD（Dense Pose Object Detector）と名付けられた私たちの方法は、入力画像と利用可能な3Dモデル間の密なマルチクラス2D-3D対応マップを推定します。対応が与えられると、6DoFポーズがPnPとRANSACを介して計算されます。カスタムの深層学習ベースのリファインスキームを使用して、初期ポーズ推定の追加のRGBポーズリファインが実行されます。私たちの結果と関連する膨大な数の作品との比較は、多数の対応が洗練の前後の両方で高品質の6Dポーズを得るために有益であることを示しています。トレーニングに実際のデータを主に使用し、合成レンダリングをトレーニングしない他の方法とは異なり、合成および実際のトレーニングデータの両方で評価を行い、最新のすべての検出器と比較して、改良前後の優れた結果を示します。提示されたアプローチは正確ですが、依然としてリアルタイム対応です。