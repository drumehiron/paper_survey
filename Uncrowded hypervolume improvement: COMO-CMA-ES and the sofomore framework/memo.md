###### tags: `Paper Notes` `MMO`

# Uncrowded hypervolume improvement: COMO-CMA-ES and the sofomore framework

## 論文情報

Cheikh Touré, Nikolaus Hansen, Anne Auger, and Dimo Brockhoff. 2019. Uncrowded hypervolume improvement: COMO-CMA-ES and the sofomore framework. In Proceedings of the Genetic and Evolutionary Computation Conference (GECCO '19). Association for Computing Machinery, New York, NY, USA, 638–646. DOI:https://doi.org/10.1145/3321707.3321852


## 内容の説明

この論文の貢献は次の3つである．

* 単目的最適化アルゴリズムから多目的最適化アルゴリズムへ拡張するSofomore フレームワークの提案
* ある解集合に対する解の評価指標として Uncrowded Hypervolume Improvement (UHVI) の提案
* 多目的最適化アルゴリズムであるCOMOCMA-ESの提案

### 多目的最適化問題

多目的最適化問題は次のように定式化される．

多目的最適化問題とは，目的関数$f_{1}(\boldsymbol{x}), \ldots, f_{M}(\boldsymbol{x})$ : $X \subseteq \mathbb{R}^{N} \rightarrow \mathbb{R}$を用いて次のように定義される．

\begin{equation}
    \begin{array}{l}
    \text { minimize } \boldsymbol{f}(\boldsymbol{x}):=\left(f_{1}(\boldsymbol{x}), \ldots, f_{M}(\boldsymbol{x})\right) \\
    \text { subject to } \boldsymbol{x} \in X\left(\subseteq \mathbb{R}^{N}\right)
    \end{array}
\end{equation}


多目的最適化では，トレードオフな関係$f_{i}(\boldsymbol{x})<f_{i}(\boldsymbol{y})$  $f_{j}(\boldsymbol{x})>f_{j}(\boldsymbol{y})$ である2つの解$\boldsymbol{x}, \boldsymbol{y} \in$ $X$について考える必要がある，そのためにはパレート順序を導入する．

\begin{equation}
    \begin{aligned}
    \boldsymbol{f}(\boldsymbol{x}) \prec \boldsymbol{f}(\boldsymbol{y}) \stackrel{\text { def }}{\Longleftrightarrow} &f_{m}(\boldsymbol{x}) \leq f_{m}(\boldsymbol{y}) \text { for all } m=1, \ldots, M\\
    \text { and } &f_{m}(\boldsymbol{x})<f_{m}(\boldsymbol{y}) \text { for some } m=1, \ldots, M
\end{aligned}
\end{equation}

多目的最適化問題はパレート最適解集合 $X^{*}$と

\begin{equation}
    X^{*}(\boldsymbol{f}):=\{\boldsymbol{x} \in X \| f(\boldsymbol{y}) \nprec f(\boldsymbol{x}) \text { for all } \boldsymbol{y} \in X\}
\end{equation}

パレートフロント$\boldsymbol{f} X^{*}(\boldsymbol{f})$を
\begin{equation}
    \boldsymbol{f} X^{*}(\boldsymbol{f}):=\left\{\boldsymbol{f}(\boldsymbol{x}) \in \mathbb{R}^{M} | \boldsymbol{x} \in X^{*}(\boldsymbol{f})\right\}
\end{equation}

を獲得することを目標としている．

### Uncrowded Hypervolume Improvement (UHVI)

多目的最適化問題における解集合を評価する指標として Hypervolume というのがある．hypervolume はある解集合$X$と参照点 $\mathbf{r}\in \mathbb{R}^M$に対して次のように定義される．

\begin{equation}
HV_{\mathbf{r}}(X)=\lambda_{M}\left(\left\{z \in \mathbb{R}^{M} ; \exists \boldsymbol{y} \in X, \mathbf{f}(\boldsymbol{y})<z<\mathbf{r}\right\}\right)
\end{equation}

$\lambda_M$は目的空間$\mathbb{R}^M$上のルベーグ測度を指す．

ある解 $\boldsymbol{x} \in X$ がどれだけ が hypervolume に貢献しているかという指標として がどれだけHypervolume Contribution がある．これは次のように定義される．

\begin{equation}
HVC_{\mathbf{r}}(\boldsymbol{x},X) = HV_{\mathbf{r}}(X) - HV_{\mathbf{r}}(X\backslash\{\boldsymbol{x}\})
\end{equation}

ある解集合 $X$ と参照点 $\mathbf{r}$ に対して，解 $\boldsymbol{x}$がどれだけhypervolume を上昇させたかという指標として Hypervolume Inprovement があり，次のように定義される．

\begin{equation}
HVI_{\mathrm{r}}(\boldsymbol{x}, X)=HV_{\mathrm{r}}(X \cup\{\boldsymbol{x}\})-HV_{\mathrm{r}}(S)
\end{equation}

Uncrowded Hypervolume Inprovement (UHVI) は次のように定義される．

\begin{equation}
\mathrm{UHVI}_{\mathrm{r}}(\boldsymbol{x}, X)=\left\{\begin{array}{ll}
\mathrm{HVI}_{\mathrm{r}}(\boldsymbol{x}, X) & \text { if } \mathrm{HVI}_{\mathrm{r}}(\boldsymbol{x}, X) > 0\\
-d_{\mathrm{r}}(\boldsymbol{x}, X) & \text { if }
\mathrm{HVI}_{\mathrm{r}}(\boldsymbol{x}, X) = 0
\end{array}\right.
\end{equation}

$d_{\mathrm{r}}(\boldsymbol{x}, X)$は $\boldsymbol{x}$の$X$に含まれる非劣解フロントとの距離の最小値である．

### Sofomore Framework

Sofomore Framework とは，単目的最適化を用いて $p$ 個の解である解集合を獲得するものである．$\mathrm{UHVI}$ を用いたアルゴリズムを次に乗せる．

![](https://i.imgur.com/NghbNl1.png)

概要としては，ある解を1つ選択し，$p-1$個の解を固定する．$\mathrm{UHVI}$が大きくなるように
解を更新し，それを他の解についても繰り返していき解集合を獲得する．

### COMO-CMA-ES

単目的最適化アルゴリズムとしてCMA-ESを使用し，Sofomore Frameworkを用いた多目的最適化アルゴリズムを次に乗せる．

![](https://i.imgur.com/Yv0dDuV.png)

#### テスト関数

テスト問題として，bi-sphere, elli-one, cigtab-sep-1, elli-two[1]を用いた．

#### 実験結果

![](https://i.imgur.com/TLL4T30.png)

COMO-CMA-ESはMO-CMA-ES、SMS-EMOA、NSGA-IIと比較して、収束ギャップとアーカイブギャップの点で概ね良好な結果を示した．COMO-CMA-ESは収束ギャップの最適化のみを目的として設計されていた．アーカイブガップがなぜ良好な結果を残したかというと(i)非エりート進化戦略で得られる定常分散が大きいこと、(ii)優勢解のフィットネス割り当てが、非優勢解の間の混雑していない空間を有利にするため、UHVIがクラウディング距離ペナルティ尺度として機能することによるものであると推測した。


## 参考文献

[1] Cheikh Toure, Anne Auger, Dimo Brockhoff, and Nikolaus Hansen. 2019. On BiObjective convex-quadratic problems. In International Conference on Evolutionary
Multi-Criterion Optimization. Springer, Lansing, Michigan, USA, 3–14.

## Abstract

単一目的のアルゴリズムから多目的アルゴリズムを構築するためのフレームワークを提示する。このフレームワークは、n次元の探索空間でp個の解を見つけ、動的部分空間最適化によって指標を最大化するというp×n次元の問題を扱う。各単目的アルゴリズムは、p - 1の固定解を与えられた指標関数を最適化する。重要なことに、支配的な解は、これらのp - 1解によって定義される経験的パレート戦線への距離を最小化する。我々は、単目的オプティマイザとしてCMA-ESを用いてフレームワークをインスタンス化する。新しいアルゴリズムであるCOMO-CMA-ESは、経験的に二目的凸二次問題に対して線形に収束することが示され、MO-CMA-ES、NSGA-II、SMS-EMOAと比較された。

## Introduction

多目的最適化問題は、実際には頻繁に解かなければなりません。単一目的の最適化とは対照的に、多目的問題を解くには、目的関数間のトレードオフや比較可能性を処理しなければなりません。パレート集合（パレート最適解または非支配解の集合）を近似することを目的としています。進化的多目的最適化（Evolutionary Multi Objective Optimization: EMO）アルゴリズムは、このような近似を1回のアルゴリズム実行で得ることを目的としていますが、より古典的なアプローチ、例えば、重みを変えて目的物の加重和を最適化する場合は、複数回の実行で動作します。

最初に導入されたEMOアルゴリズムは、全く同じ探索演算子を維持したまま、既存の単一目的進化アルゴリズムの選択を単純に変更したものでした。与えられた反復における母集団は、パレート集合の近似を提供していました。このアイデアは、2段階のフィットネス割り当てを採用した、実用的に非常に成功したNSGA-IIアルゴリズム[8]につながっています：最初の非ドミナント順位[11]の後、等しい非ドミナント順位を持つ解は、客観空間内の隣人に対する各解の距離に基づいて、そのクラウディング距離によってさらに区別されます。しかし、NSGA-IIでは、ある時点でアルゴリズムの母集団のすべてのメンバーが非ドミニオンになった場合、アルゴリズムにパレート集合への探索方向を示すことなく、クラウディング距離だけが最適化され、数学的な意味でパレート集合に収束しないことが指摘されている。その結果、ある時点で非支配的な解であった解が、最適化の間に以前に支配的であった解と入れ替わる可能性があり、周期的ではあるが収束的な挙動にはならないという結果に終わる[3]。

> NSGA-II では，(1)フロントレベル(2)クラウディングディスタンスをもちいて解に優劣をつけている．
> 全ての解のフロントレベルが同じになったときに上の問題が起きる．

EMOアルゴリズムの収束特性を改善するために、異なるアプローチが後に導入されてきました。これらはNSGA-IIのクラウディング距離を(ハイパーボリューム)指標の寄与で置き換えるもので、例えば[4, 17]を参照してください。ハイパーボリューム指標を使用すると、それが唯一知られている厳密に単調な品質指標[19]であるという利点があります（次のセクションも参照）。

SMSEMOA [4]やMO-CMA-ES [17]のような指標ベースのアルゴリズムの最適化目標は、与えられた品質指標（サイズpのすべての集合の中で最大の品質指標値を持つ集合）に関して、最適なp個の解の集合を見つけることである。この最適なp個の解の集合は、最適p分布[1]として知られています。原理的には、最適p分布の探索は、p - n次元の最適化問題として形式化することができます。

後述するように、この最適化問題は、実際には次元が高すぎるだけでなく、ハイパーボリューム指標が基本的な品質指標である場合には、検索空間の広い領域でフラットになることがわかっています。SMS-EMOAやMOCMA-ESのように、非ドミナントランキングとハイパーボリュームの寄与を組み合わせることで、この問題の平坦性を補正することができるが、同時に、パレート集合の未カバー領域ではなく、既に存在する非ドミナント解に向けた探索方向を導入することもできる。本論文では、経験的な非ドミネーションフロントへの距離を加えることで、パレート集合のまだカバーされていない領域への探索バイアスを導入することで、ハイパーボリューム指標の平坦領域を修正できることを示し、それがUncrowded Hypervolume Improvementという新しい概念につながることを示す。そして、単目的アルゴリズムで最適化できる（動的な）フィットネス関数を定義する。そこから、EMOアルゴリズムを構築するために単目的オプティマイザを使用するというEMOアルゴリズムの元々の考えに戻り、我々は、エレガントな方法で、p個の単目的オプティマイザのセットから多目的アルゴリズムを構築するためのSingle-objective Optimization FOr Optimizing Multiobjective Optimization pRoblEmsフレームワーク(Sofomore)を定義します。各単目的アルゴリズムは、他のp - 1オプティマイザの出力に依存する動的フィットネスを（反復または並列に）最適化します。

我々は、Sofomoreフレームワークを、最新の単目的アルゴリズムCMA-ESを用いてインスタンス化する。その結果、COMO-CMA-ES (Comma-Selection Multi Objective CMA-ES)が、様々な二目的凸二次関数に対して最適なp分布に線形収束することを実験的に示す。対照的に、基準点を固定したSMS-EMOAとNSGA-IIのデフォルト実装では、この線形収束は示さない。また、COMO-CMA-ESと以前のMATLAB実装のエリート派MO-CMA-ESとの比較でも、二重球関数を除いてCOMO-CMA-ESでは同じか改善された収束速度を示している。本論文は以下のように構成されています。次のセクションでは、多目的最適化と品質指標に関連する前置きから始める。第3節では、指標、特にハイパーボリュウムベースの品質指標のフィットネスについて議論し、最終的に我々のSofomoreフレームワークを紹介する。第4節では、CMA-ESを用いたSofomoreのインスタンスとして、新しいCOMO-CMA-ESアルゴリズムの詳細を述べる。第5節では、実験的に新しいアルゴリズムを検証し、既存の3つのアルゴリズムとの比較を行い、第6節ではその結果について議論し、本論文を締めくくる。

## Conclusion

我々は、(i)単一目的のオプティマイザから多目的のオプティマイザを定義するためのSofomoreフレームワーク、(ii)経験的なパレートフロントへの距離である支配解へのフィットネス(Uncrowded Hypervolume Improvement UHVI)、(iii)フレームワークをインスタンス化するための非エリチストの "カンマ "CMA-ES(COMOCMA-ES)を提案してきた。我々は、COMO-CMA-ESが、いくつかの二目的凸二次問題において、ハイパーボリューム指標のp最適分布に線形に収束することを観察した。COMO-CMAESは、凸2次問題のヘシアン行列を独立に回転させても、そのような回転によってパレート集合が線分から曲がった曲線に変化しても、ロバストであるように見える。我々の限られた実験では、COMO-CMA-ESはMO-CMA-ES、SMS-EMOA、NSGA-IIと比較して、収束ギャップとアーカイブギャップの点で概ね良好な結果を示したが、COMO-CMA-ESは収束ギャップの最適化のみを目的として設計されていた。本論文では、アーカイブギャップに関する優位性は、(i)非エリチスト進化戦略で得られる定常分散が大きいこと、(ii)優勢解のフィットネス割り当てが、非優勢解の間の空白空間(混雑していない空間)を有利にするため、暗黙のクラウディング距離ペナルティ尺度として機能することによるものであると推測した。 
