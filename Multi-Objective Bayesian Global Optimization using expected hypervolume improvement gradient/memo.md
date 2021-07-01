# Multi-Objective Bayesian Global Optimization using expected hypervolume improvement gradient

## Abstract

> The Expected Hypervolume Improvement (EHVI) is a frequently used infill criterion in Multi-Objective Bayesian Global Optimization (MOBGO), due to its good ability to lead the exploration.

EHVI は MOBO でよく使われてきた．

> Recently, the computational complexity of EHVI calculation is reduced to O(n log n) for both 2-D and 3-D cases.

最近，2目的, 3目的のケースでは$O(n \log{n})$まで計算量削減された．

> However, the optimizer in MOBGO still requires a significant amount of time, because the calculation of EHVI is carried out in each iteration and usually tens of thousands of the EHVI calculations are required.

毎 iteration EHVI を計算するのは時間がかかる，(通常数万回の計算を行うため)

> This paper derives a formula for the Expected Hypervolume Improvement Gradient (EHVIG) and proposes an efficient algorithm to calculate EHVIG.

この論文では Expected Hypervolume Improvement Gradient (EHVIG) を定式化し，効率的にに計算するアルゴリズムを提案

> The new criterion (EHVIG) is utilized by two different strategies to improve the efficiency of the optimizer discussed in this paper.

2つの異なる戦略で，最適化器の効率性を向上している．

> Firstly, it enables gradient ascent methods to be used in MOBGO.

MOBO にて勾配降下法を可能にしている．

> Moreover, since the EHVIG of an optimal solution should be a zero vector, it can be regarded as a stopping criterion in global optimization, e.g., in Evolution Strategies.

もっというと，EHVIG が 0 になる点が最適解になるので，評価の終了点としてみなすことができる．

> Empirical experiments are performed on seven benchmark problems.

> The experimental results show that the second proposed strategy, using EHVIG as a stopping criterion for local search, can outperform the normal MOBGO on problems where the optimal solutions are located in the interior of the search space.
> For the ZDT series test problems, EHVIG still can perform better when gradient projection is applied.

## Conclution

> This paper introduced an efficient algorithm to exactly calculate the 2-D EHVIG and applied EHVIG in MOGBO using two different strategies in the process of searching for the optimal solution: using EHVIG as a stopping criterion in the original CMA-ES and applying it in a GAA (CMA-ES used here to initialize the starting points).The empirical, experimental results show that MOBGO based algorithms perform much better than EMOAs, when a small amount of evaluations is considered. Among the different strategies of the optimizer in MOBGO, the GAA is much faster than original CMA-ES, but it has an obvious drawback: it gets easily stuck at stationary points, that are local optima or saddle points. Compared to the original CMA-ES, the GAA fails to outperform CMA-ES in most test problems because it is very easy to get stuck at stationary points and the parameters of GAA are not well tuned in this paper. Another strategy proposed in this paper, is taking EHVIG as the stopping criterion in CMA-ES. The experimental results show that this method can improve the quality of the final Pareto front and reduce some execution time, compared to the original CMA-ES on problems whose optimal points are not at the boundaries in the search space. This strategy does not work on the ZDT series of problems because EHVIG cannot be calculated at the boundaries of the search space. However, a useful remedy to these problems is the projection of EHVIG. Considering the good performance of the second strategy, for the optimizer in MOBGO, it is recommended to use EHVIG as a stopping criterion in EAs (like CMA-ES, GA). For future works, extending EHVIG from the 2-D case to higher dimensional cases is highly recommended, and the GAA in MOBGO based algorithms using EHVIG should be improved.

この論文では、2D EHVIG を正確に計算する効率的なアルゴリズムを紹介し、最適解を探す過程で 2 つの異なる戦略を使用して MOGBO に EHVIG を適用しました。 GAA (ここでは、開始点を初期化するために使用される CMA-ES)。経験的な実験結果は、少量の評価を考慮した場合、MOBGO ベースのアルゴリズムは EMOA よりもはるかに優れたパフォーマンスを発揮することを示しています。 MOBGO のオプティマイザーのさまざまな戦略の中で、GAA は元の CMA-ES よりもはるかに高速ですが、明らかな欠点があります。つまり、ローカル最適点または鞍点である静止点で簡単にスタックしてしまいます。元の CMA-ES と比較すると、GAA はほとんどのテスト問題で CMA-ES を上回ることができません。これは、静止点で非常に簡単にスタックし、GAA のパラメーターがこのペーパーでは適切に調整されていないためです。この論文で提案されているもう 1 つの戦略は、CMA-ES の停止基準として EHVIG を採用することです。実験結果は、この方法が、最適点が探索空間の境界にない問題に関する元の CMA-ES と比較して、最終的なパレート フロントの品質を改善し、実行時間をいくらか短縮できることを示しています。 EHVIG は探索空間の境界で計算できないため、この戦略は ZDT の一連の問題では機能しません。ただし、これらの問題に対する有効な解決策は、EHVIG の投影です。 2 番目の戦略の優れたパフォーマンスを考慮して、MOBGO のオプティマイザーでは、EA (CMA-ES、GA など) の停止基準として EHVIG を使用することをお勧めします。今後の作業では、EHVIG を 2 次元のケースから高次元のケースに拡張することが強く推奨され、EHVIG を使用する MOBGO ベースのアルゴリズムの GAA を改善する必要があります。

GAA: 勾配降下法
