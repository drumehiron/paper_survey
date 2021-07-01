# Pay Attention to MLPs

## 1. Abstract

> Transformers [1] have become one of the most important architectural innovations in deep learning and have enabled many breakthroughs over the past few years.

* ここ数年 Transformers モデルは多くのブレイクスルーを生み出してきた

    * 上手く行っている要因として inductive bias があるのではないか？

    * > It therefore remains an open question whether the inductive bias in self-attention is essential to the remarkable effectiveness of Transformers.

> Here we propose a simple attention-free network architecture, gMLP, based solely on MLPs with gating, and show that it can perform as well as Transformers in key language and vision applications.

* gMLP

    * ゲート付きのMLP(全結合層)

    * アテンションがないシンプルなネットワーク構造

    * 言語と画像タスクでトランスフォーマーと同程度の性能を示す


> Our comparisons show that self-attention is not critical for Vision Transformers, as gMLP can achieve the same accuracy.

*  自分たちの比較だと ViT で使用されている self-attention は　critical ではない．(gMLP でも達成できる．)

> For BERT, our model achieves parity with Transformers on pretraining perplexity and is better on some downstream tasks.

* pretraining の perplexity は Transformers と同等の精度，いくつかのタスクでは上回った．

> On finetuning tasks where gMLP performs worse, making the gMLP model substantially larger can close the gap with Transformers.

* gMLP が悪かった finetuning tasks では，gMLP モデルを大きくするとTransformers との差を埋められる．

> In general, our experiments show that gMLP can scale as well as Transformers over increased data and compute.

* 一般的に，私達の実験では，データと計算資源が増えるにつれて，Transformers と同様にスケールすることを示します．

gMLP の概要

![](2021-05-26-13-22-32.png)

* input/output の形式は BERT や ViT と同じ．

    * 我々のモデルは、BERT（NLP用）やViT（視覚用）と全く同じ入出力フォーマットを使用しています。例えば、言語タスクの微調整を行う際には、複数のセグメントを連結した後にパディングを行い、予測値は予約された<cls>記号の最後の層の表現から推測されます。これらのプロトコルの多くはTransformer用に導入されたものであるため、gMLPには最適ではありませんが、これらのプロトコルに厳密に従うことで、実験における交絡因子を回避し、既存のTransformerの実装との互換性を高めています。

* gMLPs は positional encodings とか，paddings がいらない．

## 5. Conclution

> Our work studies this question in depth and suggests that we generally don’t need much attention. We show that gMLPs, a simple variant of MLPs with gating, can be competitive with Transformers in terms of BERT’s pretraining perplexity and ViT’s accuracy. gMLPs are also comparable with Transformers in terms of the scalability over increased data and compute. As for BERT finetuning, we find gMLPs can achieve appealing results on challenging tasks such as SQuAD without attention, and can significantly outperform Transformers in certain cases. We also find the inductive bias in Transformer’s multi-head self-attention useful on downstream tasks that require cross-sentence alignment. However in those cases, making gMLP substantially larger closes the gap with Transformers. More practically, blending a tiny bit of single-head attention into gMLP allows for an even better architecture without the need for increasing model size.

我々の研究では，この問題を徹底的に研究し，一般的にはあまり注意を払う必要がないことを示唆しています。我々は、ゲーティングを用いたMLPの単純な変形であるgMLPが、BERTの事前学習パープレキシティとViTの精度の点でTransformerと競合できることを示しました。

gMLPは、データや計算量の増加に対するスケーラビリティの点でもTransformerと比較できます。BERTの微調整に関しては、gMLPは、SQuADのような困難なタスクにおいて、注意せずに魅力的な結果を得ることができ、特定のケースではTransformerを大幅に上回ることができることがわかりました。また、Transformerのマルチヘッドの自己注意における inductive bias は、文横断的なアライメントを必要とする下流のタスクにおいて有用であることがわかりました。しかし、そのような場合には、gMLPを大幅に大きくすることでTransformerとの差を縮めることができます。より現実的には、gMLPにほんの少しのシングルヘッドアテンションを混ぜることで、モデルサイズを大きくすることなく、より優れたアーキテクチャを実現することができます。
