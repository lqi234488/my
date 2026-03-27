Transformer Architecture: From Scratch to Inference Optimization

本專案記錄了 Transformer 核心架構的完整手刻實作過程。不僅涵蓋了底層的數學邏輯（位置編碼、自注意力機制），更進一步實作了現代 LLM（如 Llama 3）必備的 KV Cache 推論優化技術。

核心實作模組本專案將 Transformer Block 拆解並逐一實作，確保每個組件的維度變換與物理意義均符合原始論文與工業標準
Positional Encoding: 利用 Sinusoidal 函數為 Token 賦予空間資訊，並透過 Heatmap 驗證位置相關性。Manual Multi-Head Attention:手動處理 Tensor 的 reshape 與 transpose 維度變換（Batch, Heads, Seq, Dim）。實作 Causal Mask 防止模型在生成時「偷看未來」。
Feed-Forward Network (FFN): 兩層線性層搭配 GELU 激活函數，實作特徵空間的非線性投影。
Residual Connection & LayerNorm: 採用現代主流的 Pre-Norm 架構，確保深層網路的梯度流動穩定性。
KV Cache Inference Logic: 實作動態拼接（Concatenation）邏輯，將推論複雜度從 $O(n^2) 降低至 $O(n)。

效能測試：KV Cache 的威力針對「全量重算 (Full Recomputation)」與「KV Cache」兩種模式進行了生成壓力測試（Sequence Length = 512）：全量重算: 隨序列增長，生成時間呈 二次方 (Quadratic) 增長，延遲感隨長度明顯增加。KV Cache: 無論序列長度，生成單一 Token 的時間保持 恆定 (Constant)，實現流暢的流式輸出。

目錄結構
├── README.md
├── notebooks/
│   └── Transformer_&_KV_Cache.ipynb  
└── slides/
    └── Transformer_&_KV_Cache.pptx   
