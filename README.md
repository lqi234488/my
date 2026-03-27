#  Transformer Architecture: From Scratch to Inference Optimization

本專案記錄了 Transformer 核心架構的完整手刻實作過程。不僅涵蓋了底層的數學邏輯，更進一步實作了現代 LLM 必備的 **KV Cache** 推論優化技術。

---

##  核心實作模組

* **Positional Encoding**: 利用 Sinusoidal 函數為 Token 賦予空間資訊。
* **Manual Multi-Head Attention**: 
    * 手動處理 Tensor 的維度變換（Batch, Heads, Seq, Dim）。
    * 實作 **Causal Mask** 防止模型在生成時「偷看未來」。
* **Feed-Forward Network (FFN)**: 兩層線性層搭配 GELU 激活函數。
* **Residual Connection & LayerNorm**: 採用現代主流的 **Pre-Norm** 架構。
* **KV Cache Logic**: 實作動態拼接邏輯，將推論複雜度從 $O(n^2)$ 降低至 $O(n)$。

---

##  效能測試：KV Cache 的威力

針對「全量重算」與「KV Cache」兩種模式進行生成壓力測試（Sequence Length = 512）：

* **全量重算**: 隨序列增長，生成時間呈 **二次方 (Quadratic)** 增長。
* **KV Cache**: 無論序列長度，生成單一 Token 的時間保持 **恆定 (Constant)**。

---

##  目錄結構

```text
.
├── README.md
├── notebooks/
│   └── Transformer_&_KV_Cache.ipynb
└── slides/
    └── Transformer_&_KV_Cache.pptx
