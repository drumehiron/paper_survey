# Multiobjective Tree-structured Parzen Estimator for Computationally Expensive Optimization Problems

## Abstract

- expensive moo は，実世界に多く登場する．

- 多くの評価を必要としない，サロゲートモデルを提案
  - MOTPE

## INTRODUCTION

- expensive 設定の例

    - One example is the design of a tractor’s air intake
ventilation system. This problem requires expensive computational
fluid dynamics simulations to evaluate the objectives.

    - NAS

- 収束するまでに何千回もの評価が必要なNSGA-II, MOEA/D
    - だから expensive MOPが必要

- Tree-structured Parzen Estimator. The tree-structured Parzen estimator
(TPE) [3, 5] is a single-objective Bayesian optimization
algorithm for the hyperparameter optimization (HPO) of machine
learning algorithms and NAS.

## TPE


## Concluding Remarks

In this study, we extended TPE to multiobjective optimization to solve computationally expensive MOPs. Our empirical results demonstrate that, in most cases, the proposed MOTPE converges faster than existing methods while maintaining a sufficient diversity of solutions on several benchmark problems. These results prove that MOTPE is a potential solution to address computationally expensive MOPs, and to guarantee good performance for a set of real-world problems that are similar to the benchmark problems. We also empirically investigated the effects of the quantile parameter of the method. Our results demonstrate that this quantile parameter plays an important role in controlling the pressure to produce diversity. In the future, we will perform further numerical experiments to verify the performance of the method on problems with more complex search spaces that include continuous, discrete, categorical, and conditional variables that frequently appear in important real-world problems, e.g. NAS, and are difficult to handle using Kriging-based surrogates. Then, we will apply MOTPE to realworld problems to demonstrate its capability and performance in practical applications.

本研究では，TPEを多目的最適化に拡張し，計算量の多いMOPを解くことを目的とした．実証実験の結果，いくつかのベンチマーク問題において，提案したMOTPEは十分な解の多様性を維持しながら，ほとんどの場合，既存の手法よりも速く収束することがわかった．これらの結果は，MOTPEが計算量の多いMOPsに対処するための潜在的なソリューションであり，ベンチマーク問題に類似した実世界の問題群に対して良好な性能を保証することを証明している．また，本手法の分位点パラメータの効果を実証的に調べました。その結果，この分位点パラメータが，多様性を生み出す圧力を制御する上で重要な役割を果たしていることがわかった。今後は、NASなどの現実世界の重要な問題に頻繁に登場し、Krigingベースのサロゲートでは取り扱いが困難な、連続、離散、カテゴリー、条件付き変数を含む、より複雑な探索空間を持つ問題で、本手法の性能を検証するために、さらなる数値実験を行います。そして、MOTPEを実世界の問題に適用し、実用上の能力と性能を実証します。

