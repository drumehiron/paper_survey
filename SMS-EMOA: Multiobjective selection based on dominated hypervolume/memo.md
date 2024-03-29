## Abstract

ハイパーボリューム（またはS metric）は，進化的多目的最適化アルゴリズム（EMOA）の結果を比較するために頻繁に適用される評価指標である．

新しいアイデアは，最適化プロセスにおいて，支配されたハイパーボリュームの最大化を明示的に目指すことである．

ハイパーボリューム測定に基づく選択演算子と非支配ソートの概念を組み合わせた定常的なEMOAを提案する．

このアルゴリズムの母集団は、十分に分散されたソリューションのセットへと進化し，それによってパレートフロントの興味深い領域に焦点が当てられる．

考案されたSメトリック選択EMOA（SMS-EMOA）の性能を、2目的および3目的のベンチマーク問題および航空の実世界応用において、最先端の手法と比較している。

## Summary and prospects

標準的なベンチマーク問題を用いた複数の結果から、SMS-EMOAは、2つまたは3つの目的を持つパレート最適化に適していることがわかった。SMS-EMOA は、SPEA2、MOEA、NSGA-II といった既存の技術を、収束性と受信した S メトリックの値の両方で明らかに上回っています。例題では、結果がパレートフロント上にうまく分散されていることが明らかになりました。パレートフロントの境界やニーポイント周辺の領域が好まれる。SMS-EMOA の特徴は、少数の個人でパレート集合を近似するのに適していることである。これは、実際にはしばしば望まれることである。

新しい選択基準が開発された。これは、母集団に支配された解が存在する場合、ハイパーボリュームに基づく選択に取って代わるものである。この新しい概念を用いると、ある解の評価は、その解を支配している解の数に依存する。これにより、進化的探索をパレートフロント付近のあまり探索されていない領域に集中させることができる。SMS-EMOA の両バージョン（基本アルゴリズムおよび支配された点の数の基準との結合）は、従来の戦略で得られた結果よりも良い結果をもたらした。これは、ハイパーボリュームの選択メカニズムが、選択スキームの特定の詳細に関係なく、良好に機能することを示している。これは、選択された特別な選択方法に関して、ある種のロバスト性を示している。

SMS-EMOAは、最先端のベンチマークでの比較に加えて、2つまたは3つの異なる飛行条件での翼型の最適化という、困難な実世界のアプリケーションでもテストされました。その結果、解の分布が改善されただけでなく、ベースライン設計を明らかに凌駕する解も発見されました。さらに、SMS-EMOAはメタモデリングツールと連携しています。このツールは、不利な領域でのコストのかかる厳密な評価を節約するために、高速なフィットネス関数の近似を提供します。SMS-EMOAは、常にベースラインのものを凌駕する解を生成する最初のアルゴリズムでした。さらに、このアルゴリズムは、ロバストに解を生成します。

今後の研究では、さらなるアルゴリズムの改良や、戦略パラメータの分析を深めることを想定しています。これまでのところ，3つ以上の目的を持つ場合，Sメトリック値を計算するための計算量は非常に大きい。そのため，SMS-EMOAは，通常，多数の関数評価を必要とする高次元問題にはほとんど適用できない。しかし、多くの実世界のアプリケーションでは、最適化プロセスの実行時間を支配する高価なシミュレーションのために、非常に限られた数の評価しかできません。このような場合、EMOAで実行される演算の実行時間はほとんど無視できるため、SMS-EMOAは最適なオプティマイザーであると言えます。
