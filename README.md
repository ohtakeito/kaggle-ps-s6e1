## CV
- 5-Fold KFold
- OOF RMSE: 8.703
- Public LB 8.672

## Overview
Baseline solution for Kaggle Playground Series S6E1.

過去のpsの傾向から、線形回帰とその残差を非線形モデルで予測するのが強いと分かった。

Model: リッジ回帰 + 残差をXGBoostで予測

- リッジ回帰
パラメータ探索はしておらず、「デフォルト寄りのパラメータとEarly Stoppingで過学習抑制」
alpha = 1.0

- XGB
パラメータ探索はしておらず、学習率を下げて、木を多めにする。

使用パラメータ（固定）：
- n_estimators: 5000（上限。実際は early stopping で止まる）
- learning_rate: 0.02（低めで安定）
- max_depth: 4（浅めで過学習抑制）
- subsample: 0.8（行サンプリングで正則化）
- colsample_bytree: 0.8（列サンプリングで正則化）
- eval_metric: rmse
- early_stopping_rounds: 200
- random_state: 42

## Features
- Base features (11)
- ORIG mean / count features (22)
- Targetエンコーディング
・ユニーク数が３つ以上のものに適応。
・testにしか存在しないカテゴリが多すぎない
