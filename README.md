## Respository for the paper: From Intentions to Techniques: A Comprehensive Taxonomy and Challenges in Text Watermarking for Large Language Models ##

We present a curated taxonomy and collection of papers on text watermarking for Large Language Models (LLMs), grouped by intentions, methods, and evaluation datasets as described in [our paper](https://aclanthology.org/anthology-files/pdf/naacl/2025.naacl-findings.343.pdf).  

## Taxonomy

This taxonomy covers works on text watermarking for LLMs, systematically organized to help researchers:
- Navigate the field efficiently
- Identify research gaps
- Compare techniques across multiple dimensions
- Understand emerging trends

## For New Researchers

Getting started in text watermarking research can be overwhelming due to the diverse approaches and scattered literature. Our taxonomy is specifically designed to help you:

### **Quick Navigation Guide**
- **Start with [Intention](#1-intention)**: Understand what problems watermarking solves
- **Explore [Watermark Addition](#2-watermark-addition)**: See how different techniques work
- **Check [Evaluation Dataset](#3-evaluation-dataset)**: Find relevant benchmarks for your work
- **Review [Adversarial Attacks](#4-adversarial-attacks)**: Understand robustness challenges

### **Research Entry Points**
Based on your background and interests:

**For NLP Researchers:**
- Focus on **Text Quality** and **Semantic Relatedness** approaches
- Start with rule-based substitution methods
- Use established NLP datasets (C4, WikiText-2, CNN/Daily Mail)

**For Security Researchers:**
- Explore **Model Ownership Verification** techniques
- Study embedding-level addition methods
- Investigate adversarial attack strategies

**For ML/Systems Researchers:**
- Examine **Similar Output Distribution** approaches
- Focus on output logits modification techniques
- Work on evaluation benchmark standardization

### **Finding Your Research Gap**
Our [Open Challenges](#open-challenges) section identifies six critical areas where new research is needed:

1. **Resilience to Adversarial Attacks** - Most urgent need
2. **Standardization of Evaluation Benchmarks** - Infrastructure gap
3. **Impact on LLM Output Factuality** - Understudied area
4. **Compatibility with NLP Downstream Tasks** - Practical applications
5. **Enhanced Interpretability** - Transparency needs
6. **Human-Centered Watermarking** - User experience focus

### **Getting Started Checklist**
**Read the taxonomy table** to understand current approaches  
**Identify your research interest** from the four dimensions  
**Choose relevant papers** from our curated collection  
**Pick an open challenge** to address  
**Use our citation** when building on this work  

### **Recommended First Papers**
For beginners, we recommend starting with these foundational works:

- **Kirchenbauer et al. (ICML 2023)**: "Watermark for Large Language Models" - Classic green-red list approach
- **Zhao et al. (ICML 2023)**: "Protecting Language Generation Models via Invisible Watermarking" - Embedding-level techniques
- **Yoo et al. (ACL 2023)**: "Robust Multi-bit Natural Language Watermarking" - Multi-bit approaches

### **Join the Community**
- **Contact the authors** for collaboration opportunities
- **Add new papers** through pull requests
- **Suggest new challenges** or taxonomy improvements
- **Share your research** that builds on this taxonomy

## Abstract

With the rapid growth of LLMs, safeguarding textual content against unauthorized use is crucial. Watermarking offers a vital solution, protecting both - LLM-generated and plain text sources. This paper presents a unified overview of different perspectives behind designing watermarking techniques through a comprehensive survey of the research literature. Our work has two key advantages: (1) We analyze research based on the specific intentions behind different watermarking techniques, evaluation datasets used, and watermarking addition and removal methods to construct a cohesive taxonomy. (2) We highlight the gaps and open challenges in text watermarking to promote research protecting text authorship. This extensive coverage and detailed analysis sets our work apart, outlining the evolving landscape of text watermarking in Language Models.


## Table of Contents

- [Taxonomy](#taxonomy)
  - [1. Intention](#1-intention)
  - [2. Watermark Addition](#2-watermark-addition)
  - [3. Evaluation Dataset](#3-evaluation-dataset)
  - [4. Adversarial Attacks](#4-adversarial-attacks)
- [Taxonomy Table](#taxonomy-table)
- [Open Challenges](#open-challenges)
- [Citation](#citation)

## Taxonomy

We organize text watermarking for LLMs along four intersecting axes: **Intention**, **Watermark Addition**, **Evaluation Dataset**, and **Adversarial Attacks**. This multi-dimensional taxonomy helps researchers systematically navigate the field, recognize overlaps, and compare techniques across goals and application scenarios.

### 1. Intention

Watermarking methods are primarily designed around three user-driven intentions:

- **Text Quality**  
  Focuses on ensuring that the insertion of a watermark does not degrade the fluency, utility, or semantic integrity of the generated text.  
  Quality is often measured using perplexity (model confidence) and semantic relatedness between the watermarked and original outputs. Some techniques, such as green-red list rules, attempt to maintain high output utility while still achieving strong watermarking signals.  
  Semantic-preserving approaches use synonym substitutions, spelling variations, or latent representation tweaks to minimize perceptual and factual deviation.

- **Similar Output Distribution**  
  These approaches aim for watermarked text to match the statistical word/token distribution of non-watermarked outputs, making watermarking harder to detect and evade.  
  Stealthy watermarks adjust output probabilities or apply symmetric permutations to maintain the "naturalness" of text, balancing undetectability with robustness.

- **Model Ownership Verification**  
  Techniques in this bucket embed identifiers or triggers that can later be used to prove model or dataset ownership—even if the adversary tries to replicate or extract the LLM.  
  Methods include the use of trigger sets (inputs designed to activate the watermark), secret message injection, or special multi-bit encodings embedded at the output or embedding level.

### 2. Watermark Addition

Watermark embedding techniques generally fall into three categories (with overlap possible):

- **Rule-Based Substitution**  
  Replace words, phrases, or text segments using deterministic rules such as synonym swaps, spelling changes, or trigger set activation.  
  These approaches are typically reversible and focus on preserving both meaning and syntactic structure. Trigger sets (special words, styles, or structures) can activate embedded watermarks, and lexical substitutions maintain semantic coherence.

- **Embedding-Level Addition**  
  Watermarks are embedded by altering model internals—either during training (latent space/representation tweaks), through output logits modification (adjusting token probabilities to bias toward a green list, for example), or by message/signal injection in hidden spaces.  
  Some methods encode multi-bit messages, cryptographic signatures, or user/context information within the model's output distribution, often in a way that's hard to reverse without privileged knowledge.

- **Ad-Hoc Addition**  
  Task-specific or hybrid approaches, such as modifying whitespace with Unicode, inserting visual/textual variations, or code-specific tricks (variable renaming, AST rewrites).  
  These can include transformations at syntax, semantic, or visual levels—sometimes focusing on applications like code watermarking, multilingual text, or print media.

> **Note:** Some works span multiple categories, e.g., combining trigger sets and embedding-level changes, or targeting both quality and ownership. Our taxonomy is intentionally flexible to reflect such overlaps.

### 3. Evaluation Dataset

A wide variety of datasets are used to evaluate watermarking performance, reflecting the diversity of downstream tasks:

**Downstream Task descriptions**

- **Text Completion Task**  
  This task involves giving the LLM a portion of text from the dataset as a prompt and then asking it to complete the text. The generated completion is then compared with the human completion or the portion of the dataset not provided as the prompt.  
  *Example datasets:* C4, WikiText-2, Dbpedia.

- **Post-watermark text similarity analysis**  
  In this task, given an initial text $X$, watermarking is applied to $X$ to produce a modified text $X'$. An example could be a rule-based substitution with synonyms or spelling replacements. The comparison is then made between $X$ and $X'$, with $X$ and $X'$ based on distinctions in length, semantics, and other linguistic features.  
  *Example datasets:* WMT14, HC3, CNN/Daily Mail, IMDb, AgNews, literary corpora.

- **Other Downstream Tasks**  
  For these tasks, given the same initial prompt $X$, the LLM's generated response $Y$ (before watermarking) is compared with the response $Y'$ (after watermarking).  
  *Example datasets:*  
  - Summarization: CNN/Daily Mail, XSUM, DART, WebNLG  
  - Machine translation: WMT14, IWSLT14  
  - Code generation: CodeSearchNet, HUMANEVAL, MBPP, MBXP, DS-1000, APPS  
  - Question answering: OpenGen, LFQA, TruthfulQA  
  - Text classification: SST, AgNews, MIND, Enron Spam


### 4. Adversarial Attacks

To bypass or remove watermarks, adversaries employ:

- **Text insertion:** Adding new tokens or segments (possibly from unwatermarked sources) to dilute the watermark signal.
- **Text deletion:** Removing tokens—often those most responsible for the watermark (e.g., green-list tokens in green-red list approaches).
- **Text substitution:** Paraphrasing, synonym replacement, or introducing homoglyphs/unicode tricks to disrupt watermark patterns.

These attacks highlight the need for resilience in watermark design and for robust, standardized evaluation metrics.

---

## Taxonomy Table

| Paper | Authors | Conference/Journal | Code | Intention | Watermark Addition | Evaluation Dataset |
|-------|---------|--------------------|------|-----------|--------------------|-------------------|
| [Adversarial Watermarking Transformer: Towards Tracing Text Provenance with Data Hiding](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9519400) | Sahar Abdelnabi and Mario Fritz | S&P | [GitHub](https://github.com/S-Abdelnabi/awt) | Semantic Relatedness (Text Quality) | Ad Hoc | WikiText-2 |
| [Tracing Text Provenance via Context-Aware Lexical Substitution](https://ojs.aaai.org/index.php/AAAI/article/download/21415/21164) | Xi Yang, Jie Zhang, Kejiang Chen, Weiming Zhang, Zehua Ma, Feng Wang and Nenghai Yu | AAAI | - | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | Dracula, Pride and Prejudice, Wuthering Heights, WikiText-2, IMDB, AgNews |
| [Protecting Intellectual Property of Language Generation APIs with Lexical Watermark](https://ojs.aaai.org/index.php/AAAI/article/view/21321/21070) | Xuanli He, Qiongkai Xu, Lingjuan Lyu, Fangzhao Wu and Chenguang Wang | AAAI | [GitHub](https://github.com/xlhex/NLG_api_watermark) | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | WMT14, CNN/Daily Mail, MSCOCO |
| [DeepHider: A Covert NLP Watermarking Framework Basedon Multi-task Learning](https://arxiv.org/pdf/2208.04676) | Long Dai, Jiarong Mao, Xuefeng Fan and Xiaoyi Zhou | Preprint | - | Model Ownership Verification | Trigger (Rule-based substitution) | IMDB, AgNews, SST-2, OffensEval |
| [CATER: Intellectual Property Protection on Text Generation APIs via Conditional Watermarks](https://openreview.net/pdf?id=L7P3IvsoUXY) | Xuanli He, Qiongkai Xu, Yi Zeng, Lingjuan Lyu, Fangzhao Wu, Jiwei Li and Ruoxi Jia | NeurIPS | [GitHub](https://github.com/xlhex/cater_neurips) | Similar Output Distribution and Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | WMT14, CNN/Daily Mail |
| [Watermark for Large Language Models](https://arxiv.org/pdf/2301.10226) | John Kirchenbauer, Jonas Geiping, Yuxin Wen, Jonathan Katz, Ian Miers and Tom Goldstein | ICML | [GitHub](https://github.com/jwkirchenbauer/lm-watermarking) | Minimizing impact on Perplexity (Text Quality) | Output Logits Modification (Embedding level addition) | C4 |
| [Who Wrote this Code? Watermarking for Code Generation](https://aclanthology.org/2024.acl-long.268.pdf) | Taehyun Lee, Seokhee Hong, Jaewoo Ahn, Ilgee Hong, Hwaran Lee, Sangdoo Yun, Jamin Shin and Gunhee Kim | ACL | [GitHub](https://github.com/hongcheki/sweet-watermark) | Minimizing impact on Perplexity (Text Quality) | Output Logits Modification (Embedding level addition) | HUMANEVAL, MBPP |
| [Protecting Language Generation Models via Invisible Watermarking](https://arxiv.org/pdf/2302.03162) | Xuandong Zhao, Yu-Xiang Wang and Lei Li | ICML | [GitHub](https://github.com/XuandongZhao/Ginsew) | Model Ownership Verification | Output Logits Modification (Embedding level addition) | IWSLT14, WMT14, ROCstories |
| [Robust Multi-bit Natural Language Watermarking through Invariant Features](https://aclanthology.org/2023.acl-long.117.pdf) | KiYoon Yoo, Wonhyuk Ahn, Jiho Jang and Nojun Kwak | ACL | [GitHub](https://github.com/bangawayoo/nlp-watermarking) | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | IMDB, WikiText-2, Dracula, Wuthering Heights |
| [Watermarking Text Generated by Black-Box Language Models](https://arxiv.org/pdf/2305.08883) | Xi Yang, Kejiang Chen, Weiming Zhang, Chang Liu, Yuang Qi, Jie Zhang, Han Fang and Nenghai Yu | Preprint | [GitHub](https://github.com/Kiode/Text_Watermark) | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | Human ChatGPT Comparison Corpus (HC3), |
| [Are You Copying My Model? Protecting the Copyright of Large Language Models for EaaS via Backdoor Watermark](https://aclanthology.org/2023.acl-long.423.pdf) | Wenjun Peng, Jingwei Yi, Fangzhao Wu, Shangxi Wu, Bin Zhu, Lingjuan Lyu, Binxing Jiao, Tong Xu, Guangzhong Sun and Xing Xie | ACL | [GitHub](https://github.com/yjw1029/EmbMarker) | Model Ownership Verification | Trigger (Rule-based substitution) and Train Embeddings Modification (Embedding level addition) | SST2, MIND, Enron Spam, AG News |
| [Watermarking Text Data on Large Language Models for Dataset Copyright](https://arxiv.org/pdf/2305.13257) | Yixin Liu, Hongsheng Hu, Xuyun Zhang and Lichao Sun | Preprint | - | Model Ownership Verification | Trigger (Rule-based substitution) | IMDB, SST-5, Tweet Emot |
| [Provable Robust Watermarking for AI-Generated Text](https://openreview.net/pdf?id=SsmT8aO45L) | Xuandong Zhao, Prabhanjan Vijendra Ananth, Lei Li and Yu-Xiang Wang | ICLR | [GitHub](https://github.com/XuandongZhao/Unigram-Watermark) | Minimizing impact on Perplexity (Text Quality) and Watermark Replication | Output Logits Modification (Embedding level addition) | OpenGen and LFQA |
| [Watermarking Conditional Text Generation for AI Detection: Unveiling Challenges and a Semantic-Aware Watermark Remedy](https://arxiv.org/pdf/2307.13808) | Yu Fu, Deyi Xiong and Yue Dong | Preprint | [GitHub](https://github.com/FYYFU/semantic-watermark) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | CNN/DailyMail, XSUM, DART, WebNLG |
| [Robust Distortion-free Watermarks for Language Models](https://arxiv.org/pdf/2307.15593) | Rohith Kuditipudi, John Thickstun, Tatsunori Hashimoto and Percy Liang | Preprint | [GitHub](https://github.com/jthickstun/watermark) | Model Ownership Verification | Message/Signal Injection (Embedding level addition) | C4 |
| [Towards Tracing Code Provenance with Code Watermarking](https://arxiv.org/pdf/2305.12461) | Wei Li, Borui Yang, Yujie Sun, Suyu Chen, Ziyun Song, Liyao Xiang, Xinbing Wang and Chenghu Zhou | Preprint | [GitHub](https://tree-sitter.github.io/tree-sitter/) | Semantic Relatedness (Text Quality) | Message/Signal Injection (Embedding level addition) | CodeSearchNet-Java |
| [Towards Code Watermarking with Dual-Channel Transformations](https://arxiv.org/pdf/2309.00860) | Borui Yang, Wei Li, Liyao Xiang and Bo Li | Preprint | [GitHub](https://github.com/YBRua/SrcMarker) | Semantic Relatedness (Text Quality) | Message/Signal Injection (Embedding level addition) | C++, MBXP, CSN |
| [CodeMark: Imperceptible Watermarking for Code Datasets against Neural Code Completion Models](https://arxiv.org/pdf/2308.14401) | Zhensu Sun, Xiaoning Du, Fu Song and Li Li | ESEC/FSE | - | Semantic Relatedness (Text Quality) | Ad Hoc | CSN |
| [A Resilient and Accessible Distribution-Preserving Watermark for Large Language Models](https://arxiv.org/pdf/2310.07710) | Yihan Wu, Zhengmian Hu, Junfeng Guo, Hongyang Zhang and Heng Huang | ICML | [GitHub](https://github.com/yihwu/DiPmark) | Similar Output Distribution | Output Logits Modification (Embedding level addition) | OpenGen, LFQA |
| [An Unforgeable Publicly Verifiable Watermark for Large Language Models](https://openreview.net/pdf?id=gMLQwKDY3N) | Aiwei Liu, Leyi Pan, Xuming Hu, Shu'ang Li, Lijie Wen, Irwin King and Philip S. Yu | ICLR | [GitHub](https://github.com/THU-BPM/unforgeable_watermark) | Model Ownership Verification | Output Logits Modification (Embedding level addition) | C4, Dbpedia Class |
| [Electronic marking and identification techniques to discourage document copying.](https://ieeexplore.ieee.org/document/464718) | J. Brassil, S. Low, N. Maxemchuk and L. O'Gorman | IEEE | - | Model Ownership Verification | Ad Hoc | - |
| [UniSpaCh: A text-based data hiding method using Unicode space characters](https://dl.acm.org/doi/10.1016/j.jss.2011.12.023) | Lip Yee Por, KokSheik Wong and Kok Onn Chee | JSSO | - | Model Ownership Verification and Minimizing impact on Perplexity (Text Quality) | Ad Hoc | - |
| [Embarrassingly Simple Text Watermarks](https://arxiv.org/pdf/2310.08920) | Ryoma Sato, Yuki Takezawa, Han Bao, Kenta Niwa and Makoto Yamada | Preprint | [GitHub](https://github.com/amicus-veritatis/easydemark) | Minimizing impact on Perplexity (Text Quality) and  Model Ownership Verification | Ad Hoc | WMT14, C4, WMT16 |
| [The Hiding Virtues of Ambiguity: Quantifiably Resilient Watermarking of Natural Language Text through Synonym Substitutions](https://dl.acm.org/doi/10.1145/1161366.1161397) | Umut Topkara, Mercan Topkara and Mikhail J. Atallah | MM&Sec | - | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | Wordnet |
| [DeepTextMark: A Deep Learning-Driven Text Watermarking Approach for Identifying Large Language Model Generated Text](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10471537) | Travis Munyer, Abdullah Tanvir, Arjon Das and Xin Zhong | IEEE Access | - | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | Brown Corpus, Gutenberg Corpus |
| [Words Are Not Enough: Sentence Level Natural Language Watermarking](https://dl.acm.org/doi/10.1145/1178766.1178777) | Mercan Topkara, Umut Topkara and Mikhail J. Atallah | MCPS | - | Minimizing impact on Perplexity (Text Quality) | Lexical (Rule-based substitution) | Reuters corpus |
| [Natural language watermarking via morphosyntactic alterations](https://www.sciencedirect.com/science/article/abs/pii/S0885230808000284) | Hasan Mesut Meral,  Bülent Sankur,  A. Sumru Özsoy. Tunga Güngör and Emre Sevinç | CSL | - | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | - |
| [REMARK-LLM: A Robust and Efficient Watermarking Framework for Generative Large Language Models.](https://arxiv.org/pdf/2310.12362) | Ruisi Zhang, Shehzeen Samarah Hussain, Paarth Neekhara and Farinaz Koushanfar | Preprint | [GitHub](https://github.com/ruisizhang123/REMARK-LLM?utm_source=catalyzex.com) | Model Ownership Verification and Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | HC3, WikiText-2, ChatGPT Abstract, Human Abstract |
| [Did You Train on My Dataset? Towards Public Dataset Protection with Clean-Label Backdoor Watermarking](https://arxiv.org/pdf/2303.11470) | Ruixiang Tang, Qizhang Feng, Ninghao Liu, Fan Yang and Xia Hu | ACM SIGKDD Explorations Newsletter | - | Model Ownership Verification | Trigger (Rule-based substitution) | SST2, IMDB, SNLI |
| [Unbiased Watermark for Large Language Models.](https://openreview.net/pdf?id=uWVC5FVidc) | Zhengmian Hu, Lichang Chen, Xidong Wu, Yihan Wu, Hongyang Zhang and Heng Huang | ICLR | [GitHub](https://github.com/xiaoniu-578fa6bff964d005/UnbiasedWatermark) | Similar Output Distribution | Output Logits Modification (Embedding level addition) | CNN/Daily Mail, WMT14 |
| [Advancing Beyond Identification: Multi-bit Watermark for Language Models](https://aclanthology.org/2024.naacl-long.224.pdf) | KiYoon Yoo, Wonhyuk Ahn and Nojun Kwak | NAACL | [GitHub](https://github.com/bangawayoo/mb-lm-watermarking) | Minimizing impact on Perplexity and Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | C4, LFQA, WikiText-2 |
| [Necessary and sufficient watermark for large language models](https://arxiv.org/pdf/2310.00833) | Yuki Takezawa, Ryoma Sato, Han Bao, Kenta Niwa and Makoto Yamada | Preprint | - | Minimizing impact on Perplexity and Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | WMT14, WMT16 |
| [A Semantic Invariant Robust Watermark for Large Language Models](https://openreview.net/pdf?id=6p8lpe4MNf) | Aiwei Liu, Leyi Pan, Xuming Hu, Shiao Meng and Lijie Wen | ICLR | [GitHub](https://github.com/THU-BPM/Robust_Watermark) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | C4, WikiText-103 |
| [Publicly Detectable Watermarking for Language Models](https://arxiv.org/pdf/2310.18491) | Jaiden Fairoze, Sanjam Garg, Somesh Jha, Saeed Mahloujifar, Mohammad Mahmoody and Mingyuan Wang | Preprint | [GitHub](https://github.com/jfairoze/publicly-detectable-watermark) | Model Ownership Verification | Output Logits Modification (Embedding level addition) | C4 |
| [A Robust Semantics-based Watermark for Large Language Model against Paraphrasing](https://aclanthology.org/2024.findings-naacl.40.pdf) | Jie Ren, Han Xu, Yiding Liu, Yingqian Cui, Shuaiqiang Wang, Dawei Yin and Jiliang Tang | NAACL | [GitHub](https://github.com/renjie3/SemaMark) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | C4 |
| [SemStamp: A Semantic Watermark with Paraphrastic Robustness for Text Generation](https://aclanthology.org/2024.naacl-long.226.pdf) | Abe Bohan Hou, Jingyu Zhang, Tianxing He, Yichen Wang, Yung-Sung Chuang, Hongwei Wang, Lingfeng Shen, Benjamin Van Durme, Daniel Khashabi and Yulia Tsvetkov | NAACL | [GitHub](https://github.com/abehou/SemStamp) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | C4 |
| [Provably Robust Multi-bit Watermarking for AI-generated Text via Error Correction Code](https://openreview.net/pdf?id=SsmT8aO45L) | Wenjie Qu, Dong Yin, Zixin He, Wei Zou, Tianyang Tao, Jinyuan Jia and Jiaheng Zhang | ICLR | [GitHub](https://github.com/randomizedtree/segment-watermark) | Model Ownership Verification | Message/Signal Injection (Embedding level addition) | C4, OpenGen |
| [Towards Codable Watermarking for Injecting Multi-bits Information to LLMs](https://openreview.net/pdf?id=JYu5Flqm9D) | Lean Wang, Wenkai Yang, Deli Chen, Hao Zhou, Yankai Lin, Fandong Meng, Jie Zhou and Xu Sun | ICLR | [GitHub](https://github.com/lancopku/codable-watermarking-for-llm) | Model Ownership Verification | Output Logits Modification and Message/Signal Injection (Embedding level addition) | C4 |
| [CODEIP: A Grammar-Guided Multi-Bit Watermark for Large Language Models of Code](https://aclanthology.org/2024.findings-emnlp.541.pdf) | Batu Guan, Yao Wan, Zhangqian Bi, Zheng Wang, Hongyu Zhang, Pan Zhou and Lichao Sun | EMNLP | [GitHub](https://github.com/CGCL-codes/naturalcc/tree/main/examples/codeip) | Model Ownership Verification | Output Logits Modification and Message/Signal Injection (Embedding level addition) | CSN, MBPP |
| [Adaptive Text Watermark for Large Language Models](https://dl.acm.org/doi/10.5555/3692070.3693308) | Yepeng Liu and Yuheng Bu | ICML | [GitHub](https://github.com/yepengliu/adaptive-text-watermark) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | C4 |
| [WatME: Towards Lossless Watermarking Through Lexical Redundancy](https://aclanthology.org/2024.acl-long.496.pdf) | Liang Chen, Yatao Bian, Yang Deng, Deng Cai, Shuaiyi Li Peilin Zhao and Kam-fai Wong | ACL | [GitHub](https://github.com/ChanLiang/WatME) | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | TruthfulQA, C4 |
| [ACW: Enhancing Traceability of AI-Generated Codes Based on Watermarking](https://arxiv.org/pdf/2402.07518) | Boquan Li, Mengdi Zhang, Peixin Zhang, Jun Sun, Xingmei Wang and Zirui Fu | Preprint | [GitHub](https://github.com/boutiquelee/ACW) | Semantic Relatedness (Text Quality) | Lexical (Rule-based substitution) | MBPP, APPS |
| [Bileve: Securing Text Provenance in Large Language Models Against Spoofing with Bi-level Signature](https://arxiv.org/pdf/2406.01946) | Tong Zhou, Xuandong Zhao, Xiaolin Xu and Shaolei Ren | Preprint | [GitHub](https://github.com/Tongzhou0101/Bileve-official) | Model Ownership Verification | Message/Signal Injection (Embedding level addition) | OpenGen, WikiText-103, LFQA |
| [Cross-Attention Watermarking of Large Language Models](https://arxiv.org/pdf/2401.06829) | Folco Bertini Baldassini, Huy H. Nguyen, Ching-Chung Chang and Isao Echizen | Preprint | - | Semantic Relatedness (Text Quality) | Output Logits Modification (Embedding level addition) | - |

---

## Open Challenges

Despite recent progress, text watermarking for LLMs faces a number of fundamental open problems:

- **Resilience to Adversarial Attacks:**  
  Few techniques have been thoroughly stress-tested against a wide spectrum of de-watermarking strategies (e.g., paraphrasing, insertion/deletion, generative attacks, and unicode/homoglyph manipulations). Robustness remains a key hurdle.
  
- **Standardization of Evaluation Benchmarks:**  
  The field lacks common datasets and metrics for fair comparison. As different works use varied benchmarks and evaluation criteria (see the Taxonomy/Evaluation section), cross-paper comparison is currently difficult and can slow down progress.

- **Impact on Factuality and Utility:**  
  There is insufficient research on how watermarking—especially robust methods—affects the factual accuracy, truthfulness, or downstream utility of LLM outputs. Some robust watermarking may inadvertently increase hallucination or degrade answer quality.

- **Interpretability and Transparency:**  
  Users and practitioners often lack clear tools or standards to interpret or audit the presence and effect of watermarks. Inspired by the privacy/security field, there is a need for "model cards" or similar transparency artifacts to communicate watermarking properties.

- **Human-Centered Design:**  
  Watermarking must not negatively impact user experience or trust. Understanding human perception, user acceptance, and the broader societal impacts of watermarked content is crucial as adoption increases.

- **Personalised Watermarking:**  
  Developing personalized watermarking approaches that cater to individual user preferences, contexts, or specific organizational policies is important. This requires adaptive techniques that can embed user- or context-specific identifiers while respecting privacy, personalization preferences, and practical constraints.

- **Multi-agent Watermarking:**
  Current watermarking methods do not effectively support scenarios where multiple LLM agents sequentially or collaboratively contribute to generating text. Specifically, existing approaches fail to maintain watermark integrity and detectability when multiple distinct watermarks are stacked or embedded in succession. An unresolved challenge is developing watermarking techniques that enable each agent to reliably detect its own watermark and a collaboratively embedded watermark, even when multiple watermarks from different agents coexist within the same generated content.

---

## Citation

If you use this taxonomy table, please cite:

```bibtex
@inproceedings{lalai-etal-2025-intentions,
    title = "From Intentions to Techniques: A Comprehensive Taxonomy and Challenges in Text Watermarking for Large Language Models",
    author = "Lalai, Harsh Nishant  and
      Anantha Ramakrishnan, Aashish  and
      Shah, Raj Sanjay  and
      Lee, Dongwon",
    editor = "Chiruzzo, Luis  and
      Ritter, Alan  and
      Wang, Lu",
    booktitle = "Findings of the Association for Computational Linguistics: NAACL 2025",
    month = apr,
    year = "2025",
    address = "Albuquerque, New Mexico",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.findings-naacl.343/",
    doi = "10.18653/v1/2025.findings-naacl.343",
    pages = "6147--6160",
    ISBN = "979-8-89176-195-7",
    abstract = "With the rapid growth of Large Language Models (LLMs), safeguarding textual content against unauthorized use is crucial. Watermarking offers a vital solution, protecting both - LLM-generated and plain text sources. This paper presents a unified overview of different perspectives behind designing watermarking techniques through a comprehensive survey of the research literature. Our work has two key advantages: (1) We analyze research based on the specific intentions behind different watermarking techniques, evaluation datasets used, and watermarking addition and removal methods to construct a cohesive taxonomy. (2) We highlight the gaps and open challenges in text watermarking to promote research protecting text authorship. This extensive coverage and detailed analysis sets our work apart, outlining the evolving landscape of text watermarking in Language Models."
}
```

## **Contribute!**
We welcome contributions to expand and improve this taxonomy! If you find papers that should be included, please help us maintain this comprehensive resource.

### **How to Add Missing Papers**

#### **Option 1: Open an Issue**
1. Go to the [Issues](https://github.com/Harsh-Lalai/Stamped-Secured-NAACL-2025-A-Taxonomy-of-Text-Watermarking-for-LLMs/issues) tab
2. Click "New Issue"
3. Use the template: **"Add Missing Paper: [Paper Title]"**
4. Include the following information:

```markdown
**Paper Title:** [Full title]
**Authors:** [Author list]
**Conference/Journal:** [Venue and year]
**ArXiv/PDF Link:** [Direct link]
**Code Repository:** [GitHub link if available]

**Proposed Classification:**
- **Intention:** [Text Quality / Similar Output Distribution / Model Ownership Verification]
- **Watermark Addition:** [Rule-based / Embedding-level / Ad-hoc]
- **Evaluation Dataset:** [List of datasets used]

**Brief Description:** [2-3 sentences about the paper's contribution]

**Why it should be included:** [Explain how it fits into our taxonomy]
```

#### **Option 2: Submit a Pull Request**
1. Fork this repository
2. Add the paper to the taxonomy table in `README.md`
3. Follow the existing table format
4. Submit a pull request with a clear description

### **Paper Inclusion Criteria**

We include papers that:
- Focus on **text watermarking for language models**
- Present **novel watermarking techniques or evaluations**
- Are **peer-reviewed** (conferences, journals) or **high-quality preprints**
- Contribute to the **research landscape**
