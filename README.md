## CV
- 5-Fold KFold
- OOF RMSE: 8.696
- Public LB 8.654

Huber+XGBに変更した。変化なし

## Overview

過去のpsの傾向から、線形回帰とその残差を非線形モデルで予測するのが強いと分かった。

Model: リッジ回帰 + 残差をXGBoostで予測

- リッジ回帰
パラメータ探索はしておらず、「デフォルト寄りのパラメータとEarly Stoppingで過学習抑制」
alpha = 1.0

- XGB
float64, int64をfloat32, int32に変換する。
パラメータ探索はしておらず、学習率を下げて、木を多めにする。

One-hotをCVの外で固定した

## Features
- Base features (11)
- ORIG mean / count features (22)
- カテゴリを全てOne-hotエンコーディングすることで、リッジ回帰が強くなった。