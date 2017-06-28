---
title: '[Note] 人類行為大數據分析: 資料科學如何應用在教育及醫療領域'
date: 2016-11-14 
tags: 
- note
- big data
---
### 講者：李祈均

**What is BEHAVIORAL SIGNAL PROCESSING (BSP) ?  
**_Compute Human Behavior Traits and States for Domain Experts Decision Making_

*   _Help experts to do things they know in a more efficient manner at scale_
*   _Develop novel behavioral analytics framework for possible scientific discovery_

人類行為分析方式

*   訊號產生 — -> 訊號擷取 — -> 訊號分析 — -> 決策(行為判定)
*   單向：

![BSP01.png](./imgs/BSP01.png)
行為產生機制 → 外顯行為 →內在狀態 行為認知機制 → 主觀量測 → 決策

* * *

![BSP02.png](./imgs/BSP02.png)
行為產生機制 → 外顯行為 — -> 內在狀態 行為認知機制 → Self Report → 決策

*   雙向：
![BSP03.png](./imgs/BSP03.png)
行為產生機制 → 外顯行為 — -> 行為認知機制 → 行為產生機制 → 外顯行為 — -> 行為認知機制 → 主觀量測 → 決策

#### COMPUTING BEHAVIORAL TRAITS & STATES FOR DECISION MAKING & ACTION

*   QUANTITATIVE
*   EFFICIENCY
*   SUPPLMENTARY
*   POSSIBILITY

#### ELEMENTS OF BSP

1.  Fetching
2.  Pre-processing
3.  Modeling
4.  Assessment

![BSP04.png](./imgs/BSP04.png)

### 資料代表性

*   辨識目標的評分  
    1\. 運用 _established instrument_  
    2\. _Scientific-rigor_  
    3\. Ensure _domain-applicable analytics_ 產出
*   如何找出有用的資料  
    1\. 討論、討論、討論  
    2\. 收的過程影響後面預處理  
    3\. 想像未來應用  
    4\. 領域專家意見太重要
*   ADOS (Autism Diagnostic Observation Schedule)  
    1\. Subject interacts with a psychologist for ~45 minutes  
    2\. Current gold standard, research-level observational coding  
    3\. Psychologists are trained using stringent training protocol  
    4\. Semi-structured assessment in eliciting socio-communicative behavior of the ASD children for diagnostics  
    5\. Multiple subparts events (14) on rating of a wide range number of socio-communicative behavior (28)

### 充分預處理

#### **訊號預處理**

#### **Label 預處理**

*   **Voice Activity Detector  
    **Speech signal  
    _1\. Energy every frame_  
     frame = 25ms  
     standard deviation (normalize D.C. offset)  
    _2\. 閥值Threshold_  
    speech percentage in the wav  
    _3\. Speech Segments_  
    Energy > Threshold Energy
*   **建議  
    **1\. 資料收集過程重要、重要、重要  
    2\. 熟悉資料是必要、必要、必要  
    3\. 有些真的太錯、知道錯、不要用  
    4\. 要被學的label需要被分析徹底  
    5\. domain experts 很厲害  
    6\. 跨領域閱讀

### 電腦如何「聽」、「讀」及「看」懂人類行為

![低階描述值(low-level descriptors) -> 編碼/Profile -> Machine learning -> 行為分析結果](./imgs/BSP05.png)
