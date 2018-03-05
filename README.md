# EvaluationOfDiscriminationTask
Evaluation of discrimination task.

## 0
光点検出実験をYes/No課題を用いて行ったところ、hit rateが0.87、false alarm rateが0.23であった。信号刺激を与えなかった時と信号刺激を与えた時のそれぞれに対する主観的な刺激の強さ(講義スライドではrに相当)が等分散の正規分布に従うと仮定し、d'と判断基準(閾値)を推定して表示する。判断基準は信号刺激なしの分布からみたzスコアを表示する。

## 1
信号刺激無しの場合の主観的な刺激の強さ(講義スライドではrに相当)が分散1、平均0の正規分布に従うとする。この分布から乱数を生成し、0.3以上ならYes、0.3未満ならNoと判断したときのFalse alarm rateを表示する。

## 2
信号刺激ありの場合の主観的な刺激の強さが分散1、平均1の正規分布に従うとする。この分布から乱数を生成し、0.3以上ならYes、0.3未満ならNoと判断したときのHit rateを表示する。
## 3
信号刺激なし、ありに対する主観的な刺激の強さが1,2のように分布するとして、ROC曲線を表示する。

## 4
3のAUCを表示する。

## 5
信号刺激なしと信号刺激ありの場合の主観的な刺激の強さがそれぞれ正規分布に従うとし、その分散を1、平均の差をdとする(この時、d'=dとなる)。dの値を変更していった時のROC曲線とAUCを表示する。ただし、AUCが0.5から1.0付近まで近づくことが確認できるようdの範囲を設定する。

## 6
主観的な刺激の強さが5の分布に従うとし、2-alternative forced choice課題を行なった時の正答率を表示する。正答率は5で出したAUCとほぼ同じ値になる。
これらの課題を乱数生成によるシミュレーションではなく確率密度関数と積分を使って取り組んでもらっても大丈夫です。

## Tips

これらを実行していることを前提とします。

import numpy as np

import scipy as sp

import matplotlib.pyplot as plt

from sklearn import metrics

%matplotlib inline

d'は1-false alarm rateをzスコアにしたものから1-hit rateをzスコアにしたものを引くことで求められます。

p-valueからのzスコア化

sp.stats.norm.ppf

ROC

metrics.roc_curve

使用するの際の参考：http://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_curve.html

使用例：

truelabel = np.array([1, 1, 2, 2])

r = np.array([0.1, 0.4, 0.35, 0.8])

false_alarm, hit_rate, thresholds = metrics.roc_curve(truelabel, r, pos_label=2)

print false_alarm >>array([ 0. ,  0.5,  0.5,  1. ])

print hit_rate >>array([ 0.5,  0.5,  1. ,  1. ])

print thresholds >>array([ 0.8 ,  0.4 ,  0.35,  0.1 ])

AUC

metrics.auc

累積分布関数

sp.stats.norm.cdf

使用例：hr = 1 - sp.stats.norm.cdf(threshold,loc=mean)

