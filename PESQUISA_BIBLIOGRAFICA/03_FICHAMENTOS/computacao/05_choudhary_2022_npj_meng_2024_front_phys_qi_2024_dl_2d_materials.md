# Fichamento 05 — Aprendizado Profundo em Ciência dos Materiais, Materiais 2D e Espectroscopia Raman Assistida por Difusão: Choudhary et al. (2022), Meng et al. (2024) e Qi et al. (2024)

> **Nível de leitura declarado (Seção 8 — `PROMPT_MESTRE.md`):**
> - **Choudhary et al. (2022):** **Texto completo lido** via extração integral (`_scratch/textos_extraidos/Choudhary_2022_Deep_Learning_Methods_Materials_Science.md`, linhas 1–1200 cobrindo todo o corpo do artigo, discussões e declarações até *Data/Code Availability*; apenas referências bibliográficas finais nas linhas 1201–1684 não foram lidas).
> - **Meng et al. (2024):** **Texto completo lido** via extração integral (`_scratch/textos_extraidos/Meng_2024_Deep_Learning_Two_Dimensional_Materials.md`, 920 linhas completas).
> - **Qi et al. (2024):** **Texto completo do preprint correspondente (`arXiv:2312.01389`) lido integralmente** (`_scratch/textos_extraidos/Qi_2024_Deep_Learning_Raman_Spectroscopy_2D_Materials.md`, 394 linhas), **cruzado com os metadados verificados do artigo publicado** em *Applied Materials Today* (`verified_catalog.json`, DOI `10.1016/j.apmt.2024.102499`).
> - **Verificação *preprint $\rightarrow$ publicado*:** `Qi et al. (2024)` (`arXiv:2312.01389`) foi publicado em **Applied Materials Today** (`10.1016/j.apmt.2024.102499`), sendo esta a referência principal adotada. Registra-se explicitamente divergência na autoria indexada: o periódico (ScienceDirect/`verified_catalog.json`) lista 5 autores (Yaping Qi, Dan Hu, Ming Zheng, Yu-Cheng Jiang, Yong P. Chen), enquanto o manuscrito preprint `arXiv:2312.01389` lido localmente lista 7 autores (incluindo Zhenping Wu e Guanghui Cheng).

---

## 1. Identificação bibliográfica

### Obra A — Choudhary et al. (2022) `[Extraído do artigo]`
- **Autores:** Kamal Kumar Choudhary, Brian DeCost, Chi Chen, Anubhav Jain, Francesca Tavazza, Ryan Cohn, Cheol Woo Park, Alok Choudhary, Ankit Agrawal, Simon J. L. Billinge, Elizabeth A. Holm, Shyue Ping Ong, Chris M. Wolverton.
- **Ano:** 2022.
- **Título completo:** *Recent advances and applications of deep learning methods in materials science*.
- **Periódico:** *npj Computational Materials*, vol. 8, artigo 59 (2022).
- **DOI:** `10.1038/s41524-022-00734-6`
- **Link oficial:** <https://doi.org/10.1038/s41524-022-00734-6>
- **Nível de leitura:** Texto completo (corpo integral até *Data/Code Availability*).

### Obra B — Meng et al. (2024) `[Extraído do artigo]`
- **Autores:** Xinqin Meng, Chengbing Qin, Xilong Liang, Guofeng Zhang, Ruiyun Chen, Jianyong Hu, Zhichun Yang, Jianzhong Huo, Liantuan Xiao, Suotang Jia.
- **Ano:** 2024.
- **Título completo:** *Deep learning in two-dimensional materials: Characterization, prediction, and design*.
- **Periódico:** *Frontiers of Physics*, vol. 19, n.º 5, 53601 (2024).
- **DOI:** `10.1007/s11467-024-1394-7`
- **Link oficial:** <https://doi.org/10.1007/s11467-024-1394-7>
- **Nível de leitura:** Texto completo.

### Obra C — Qi et al. (2024) `[Extraído do artigo / metadados publicados]`
- **Autores (versão publicada — *Applied Materials Today*):** Yaping Qi, Dan Hu, Ming Zheng, Yu-Cheng Jiang, Yong P. Chen *(na versão preprint `arXiv:2312.01389` lida localmente constam também Zhenping Wu e Guanghui Cheng)*.
- **Ano:** 2024 (vol. 41, dezembro de 2024).
- **Título completo:** *Deep learning assisted Raman spectroscopy for rapid identification of 2D materials*.
- **Periódico (referência principal publicada):** *Applied Materials Today*, vol. 41, artigo 102499 (2024).
- **DOI:** `10.1016/j.apmt.2024.102499`
- **Link oficial:** <https://doi.org/10.1016/j.apmt.2024.102499>
- **Preprint (apenas acesso aberto — base da leitura integral):** `arXiv:2312.01389`
- **Código informado no manuscrito:** <https://github.com/Naduhi/Raman_DL>
- **Nível de leitura:** Texto completo do preprint `arXiv:2312.01389` + metadados verificados da versão publicada.

---

## 2. Problema investigado

### Obra A — Choudhary et al. (2022) `[Extraído do artigo]`
- Mapear criticamente o panorama, os fundamentos arquiteturais e os gargalos de transferência prática do aprendizado profundo (*Deep Learning* — DL) em Ciência dos Materiais — abrangendo representações atomísticas/químicas, **caracterização experimental por espectros (DRX, PDF, XAS, Raman)** e **imagens (MO, MEV, STEM, SPM)**, NLP científico, *Scientific Machine Learning* (SciML) e quantificação de incerteza (UQ).

### Obra B — Meng et al. (2024) `[Extraído do artigo]`
- Sistematizar o estado da arte da aplicação de arquiteturas profundas (CNNs, GANs, U-Net e redes de grafos/invertíveis) exclusivamente no domínio de **materiais bidimensionais (2D)**, cobrindo três eixos: (1) caracterização de defeitos atômicos (STEM/TEM) e identificação óptica/espessura (MO); (2) predição de propriedades; e (3) design inverso.

### Obra C — Qi et al. (2024) `[Extraído do artigo]`
- Classificação rápida e automatizada de materiais 2D e heteroestruturas a partir de espectros Raman experimentais obtidos em diferentes substratos, enfrentando escassez severa de amostras anotadas (classes com apenas $6$ a $8$ espectros) e desbalanceamento acentuado por meio de geração sintética com modelos de difusão (*Denoising Diffusion Probabilistic Model* — DDPM) combinada a CNN 1D.

### `[Análise crítica — Agente E]`
Os três trabalhos compõem um arco complementar: duas revisões panorâmicas (Choudhary et al., 2022, transversal a toda a Ciência dos Materiais e explicitamente atenta a baselines clássicos como NMF e a falhas como vazamento de dados no ICSD; Meng et al., 2024, focalizada em materiais 2D) e um estudo experimental aplicado recente (Qi et al., 2024) que ilustra tanto o potencial de modelos generativos (DDPM) em espectroscopia quanto **os riscos metodológicos críticos** quando *augmentation* generativa encontra conjuntos pequenos e desbalanceados sem isolamento rigoroso de dobras (*folds*).

---

## 3. Fundamentação

### `[Extraído dos artigos]`
1. **Taxonomia de caracterização em Ciência dos Materiais (Choudhary et al., 2022):**
   - **Espectroscopia e difração (DRX, PDF, XAS, Raman):** Contrasta redes convolucionais 1D/ensembles para classificação de simetrias e fases cristalinas em DRX (Park et al., 2017; Oviedo et al., 2019; Lee et al., 2020; Wang et al., 2020; Maffettone et al.; Dong et al. PQ-Net; Liu et al., 2019 para PDF) com métodos matriciais interpretáveis não profundos, em especial **Fatoração de Matrizes Não-Negativas (NMF)** para decomposição espectral.
   - **Microscopia (MO, MEV, STEM, SPM):** Segmentação semântica e de instâncias (Modarres et al. em MEV; Azimi et al. FCNN em aços — $94\%$; DeCost & Holm PixelNet; Cohn & Holm Mask R-CNN para pós metálicos e satélites), super-resolução/aceleração via GANs (De Haan et al. em MEV com redução de $4\times$ no tempo de varredura; Ede et al. em STEM parcial) e controle autônomo de ponta em SPM/STM (Rashidi & Wolkow — $99\%$).
   - **Quantificação de Incerteza (UQ):** Distingue **incerteza epistêmica** (redutível com mais dados/modelos) e **incerteza aleatória** (ruído intrínseco de medida), revisando *Monte Carlo Dropout*, *Deep Ensembles*, *Quantile Regression*, *Deep Gaussian Processes* e a **opção de rejeição** para amostras fora da distribuição (*out-of-distribution* — OOD).
2. **Arquiteturas em Materiais 2D (Meng et al., 2024):**
   - **STEM/TEM (Seção 3.1):** FCNs e U-Nets para detecção de vacâncias e dopantes (Ziatdinov et al., 2017; Madsen et al., 2018; Maksov et al., 2019 combinando FFT+GMM+FCN; Yang et al., 2021; Yang et al., 2024 2DIP-Net; Lee et al., 2020 para mapeamento de deformação; Chu et al., 2023 $\text{U}^2$-net).
   - **MO (Seção 3.2):** SegNet, U-Net, Mask R-CNN, $\text{2DU}^2$-net (Zhang et al., 2022), deblurring via GAN+U-Net (Dong et al., 2022/2023), ANNs sobre RGB+HSV (Zhu et al., 2022) e treinamento ancorado em *ground truth* físico AFM+Raman (Mahjoubi et al., 2023).
   - **Predição e Design Inverso (Seções 4–5):** RCGAN, redes invertíveis (MatDesINNe INN), CGCNN.
3. **DDPM 1D + CNN 1D para Raman (Qi et al., 2024):**
   - Modelo de difusão probabilística de remoção de ruído (DDPM, arquitetura residual inspirada em *DiffWave*: $8$ blocos residuais, $128$ canais, $T = 50$ passos de difusão, esquema de ruído linear $\beta_t \in [0{,}0001,\, 0{,}02]$) para sintetizar espectros Raman condicionados por classe.
   - Classificador CNN 1D de $4$ camadas convolucionais ($32, 64, 128, 256$ filtros, *kernel* $3$, *stride* $2$, ativação LeakyReLU).

### `[Análise crítica — Agente E]`
Um contraste valioso emerge do cruzamento entre Choudhary et al. (2022) e Meng et al. (2024):
- Enquanto revisões entusiastas de DL às vezes tratam IA como substituta universal da análise clássica, Choudhary et al. (2022) destacam que métodos clássicos como **NMF** permanecem superiores em interpretabilidade física para misturas espectrais e que modelos de DL enfrentam a **lacuna simulação-experimento (*sim-to-exp*)**, pois ruído experimental estruturado (fundo de fluorescência em Raman, fluorescência/desalinhamento em DRX, *charging* em MEV, deriva/ponta em AFM) difere de ruído gaussiano idealizado.
- Em Meng et al. (2024, Seção 3.2), fica explícito o papel crítico da qualidade do rótulo: Mahjoubi et al. (2023) obtiveram $>99\%$ de acurácia com **MIoU de $59\%$** mesmo usando AFM+Raman como *ground truth*, confirmando novamente a distância entre acerto de classificação global e fidelidade geométrica de contornos.

---

## 4. Metodologia

### Obras A e B — Choudhary et al. (2022) e Meng et al. (2024) `[Extraído dos artigos]`
- **Revisões sistemáticas / narrativas de literatura:** Levantamento estruturado por modalidade de representação de dados (grafos atômicos, séries 1D espectrais, imagens 2D de microscopia, texto), análise comparativa de arquiteturas, consolidação de tabelas de desempenho reportado, discussão de bases de dados abertas e formulação de desafios em aberto (Seção de Desafios em Choudhary et al., 2022; Seção 6 em Meng et al., 2024).

### Obra C — Qi et al. (2024) `[Extraído do artigo]`
- **Base experimental:** **$594$ espectros Raman experimentais** distribuídos em **$10$ classes** adquiridas em $>1$ substrato:
  - *Black phosphorus* (BP): $35$;
  - Grafeno: $209$;
  - $\text{MoS}_2$: $8$;
  - $\text{ReS}_2$: $15$;
  - Telúrio (Te): $270$;
  - $\text{WSe}_2$: $6$;
  - $\text{WTe}_2$: $28$;
  - Heteroestruturas empilhadas S1 ($8$), S2 ($7$), S3 ($8$).
- **Pré-processamento 1D:** Interpolação por *spline* para exatamente **$571$ pontos** ($50$–$1750\ \text{cm}^{-1}$), *zero-padding* e normalização.
- **Geração sintética e treinamento:** O DDPM gerou $1.000$ espectros sintéticos por classe (**$10.000$ espectros no total**). O classificador CNN 1D foi treinado com Adam ($\text{LR} = 0{,}0002$), $100$ épocas, *batch size* $32$, em GPU NVIDIA RTX 3060Ti, e avaliado por validação cruzada **10-fold** comparando-se com SVM, Regressão Logística (LR), KNN, ANN e Random Forest (RF) tanto nos $594$ dados brutos quanto no conjunto expandido por DDPM.

### `[Análise crítica — Agente E — Auditoria metodológica de Qi et al. (2024)]`
1. **Desbalanceamento extremo não trivial:** Cinco das dez classes ($\text{MoS}_2$, $\text{WSe}_2$, S1, S2, S3) possuem apenas **$6$ a $8$ espectros reais**, frente a $209$ de grafeno e $270$ de telúrio (razão $\approx 45:1$).
2. **Risco severo de vazamento de dados (*data leakage*) na avaliação *10-fold CV* pós-DDPM:** O manuscrito não documenta o isolamento estrito do treinamento do DDPM dentro de cada dobra de treinamento antes de gerar espectros sintéticos e avaliar a *10-fold CV* no conjunto de $10.000$ espectros. Como resultado, **CNN 1D, ANN, RF, SVM e LR alcançaram simultaneamente $1{,}000$ ($100\%$) de acurácia, precisão e revocação** após o DDPM! Quando um modelo linear simples (LR) e uma árvore aleatória (RF) saltam ambos para $1{,}000$ exato sobre amostras sintéticas geradas a partir de apenas $6$–$8$ espectros originais, isso constitui forte indício de **vazamento de informação gerativa entre treino e teste** e colapso de diversidade intraclasse (*memorização/interpolação de poucos espectros reais*).
3. **Ausência de validação cruzada agrupada (*GroupKFold*) por amostra ou substrato:** Embora o texto mencione múltiplos substratos, não há relato de *holdout* cego separando substratos ou amostras físicas inéditas entre treino e teste.

---

## 5. Resultados

### Obra A — Choudhary et al. (2022) `[Extraído do artigo]`
- **Sistematização de benchmarks:**
  - *Imagens MEV/SPM:* FCNN de Azimi et al. ($94\%$ em microestrutura de aço); Mask R-CNN de Cohn & Holm para partículas metálicas; GAN de De Haan et al. reduzindo em $4\times$ o *dwell time* de varredura em MEV; algoritmo RL/DL de Rashidi & Wolkow com $99\%$ em condicionamento de ponta SPM.
  - *Espectros:* Evidencia o avanço de CNNs 1D e *ensembles* em DRX e PDF, mas ressalta a necessidade de métodos de UQ e prevenção de duplicatas em bases como o ICSD.

### Obra B — Meng et al. (2024) `[Extraído do artigo]`
- **Sistematização quantitativa em materiais 2D:**
  - *STEM/TEM (Seção 3.1):* Yang et al. (2021) atingiram **$98\%$** na detecção de átomos individuais/defeitos em **$3\ \text{s}$** (vs. $1\ \text{h}$ humano); Yang et al. (2024, 2DIP-Net) $>97{,}87\%$; Lee et al. (2020) precisão de $0{,}2\ \text{pm}$ em mapas de deformação; Chu et al. (2023, $\text{U}^2$-net) $96{,}8\%$ / $99{,}4\%$.
  - *MO (Seção 3.2):* Wu et al. (2019, SegNet) $97{,}17\%$; Zhang et al. (2022, $\text{2DU}^2$-net) **$99{,}03\%$ / MIoU $94{,}18\%$** nos dados de Saito et al. (2019); Zhu et al. (2022, ANN RGB+HSV) $>90\%$ vs. $49\%$ por pesquisadores humanos; Mahjoubi et al. (2023, *ground truth* AFM+Raman) $>99\%$ acurácia global / **MIoU $59\%$**.

### Obra C — Qi et al. (2024) `[Extraído do artigo]`
- **Tabela 2 — Validação cruzada *10-fold* nos dados brutos ($594$ espectros):**
  - CNN 1D: **$98{,}8\%$** acurácia (precisão $94{,}5\%$, revocação $93{,}7\%$);
  - SVM: **$96{,}6\%$**;
  - Regressão Logística (LR): **$96{,}0\%$**;
  - KNN: $95{,}3\%$; ANN: $94{,}6\%$; Random Forest: $90{,}6\%$.
- **Tabela 2 — Pós-DDPM ($10.000$ espectros sintéticos):**
  - **CNN 1D, ANN, RF, SVM e LR: todos $1{,}000$** (precisão $1{,}000$, revocação $1{,}000$); KNN: $0{,}988$.

### `[Análise crítica — Agente E]`
Observe-se o resultado nos **dados brutos** de Qi et al. (2024): sem DDPM, modelos clássicos simples e interpretáveis (**SVM com $96{,}6\%$** e **Regressão Logística com $96{,}0\%$**) ficam a apenas **$2{,}2$–$2{,}8$ pontos percentuais** da CNN 1D ($98{,}8\%$), custando uma fração minúscula do tempo de treinamento e sem exigir GPU RTX 3060Ti nem modelo de difusão. Isso ilustra perfeitamente a tese central exigida nesta revisão: **em sinais espectrais 1D bem alinhados (Raman ou DRX em amostras puras), métodos clássicos/lineares devem sempre atuar como *baseline* obrigatório antes de justificar arquiteturas profundas ou generativas complexas**.

---

## 6. Limitações

### `[Extraído dos artigos]`
- **Choudhary et al. (2022):**
  1. Duplicatas estruturais em bancos cristalográficos (ex.: ICSD) provocam **vazamento de informação** e estimativas infladas entre treino e teste.
  2. Comportamento distinto de vazamento em regressão vs. classificação; escassez de dados experimentais anotados e rotulagem cara.
  3. Lacuna simulação-experimento devido a ruído experimental estruturado não reproduzido em padrões simulados.
  4. Opacidade (*black-box*) e ausência generalizada de UQ confiável fora do domínio de treino.
- **Meng et al. (2024 — Seção 6):**
  1. Escassez de dados experimentais rotulados para materiais 2D exóticos.
  2. Desvio sistemático entre simulações (STEM/óptica idealizada) e imagens reais com contaminação/deriva.
  3. Modelos puramente orientados a dados carecem de restrições físicas (*physics-informed priors*), restringindo interpretabilidade e extrapolação.
- **Qi et al. (2024):**
  1. Classes minoritárias com apenas $6$–$8$ espectros experimentais reais ($\text{WSe}_2$, $\text{MoS}_2$, S1–S3).
  2. Falta de separação documental entre treino do DDPM e validação *10-fold* sobre espectros gerados, bem como ausência de teste em amostras/substratos inteiramente retidos (*unseen holdout*).

### `[Análise crítica — Agente E]`
- Em Qi et al. (2024), a interpolação por *spline* + normalização + CNN/DDPM também ignora informações físicas explícitas de deslocamento de pico Raman por deformação (*strain*), dopagem ou acoplamento substrato-floco (ex.: razão $I_{2\text{D}}/I_{\text{G}}$ e deslocamento de banda G em grafeno), podendo falhar quando exposta a amostras com funcionalização química, defeitos estruturais ou óxido de grafeno (GO/rGO), cujos espectros alargam fortemente as bandas D e G.

---

## 7. Contribuição para a dissertação

### `[Análise crítica — Agente E]`
1. **Mapa completo de UQ e armadilhas de validação (Choudhary et al., 2022):** Fornece a fundamentação conceitual direta para a metodologia da dissertação (PPGCEM/UFCA) incluir: (a) separação entre incerteza epistêmica e aleatória; (b) opções práticas de UQ (*MC Dropout*, *Deep Ensembles*, regressão quantílica, detecção OOD); e (c) **auditoria contra vazamento por duplicatas/amostras correlacionadas**.
2. **Contraste de modalidades e relevância para grafeno/2D (Meng et al., 2024):** Conecta a caracterização computacional em MO, MEV/STEM e espectroscopia especificamente ao contexto de materiais 2D (grafeno e correlatos), reforçando a necessidade de modelos físicos ou rótulos multitécnica (AFM + Raman + DRX) e o alerta de que alta acurácia global pode coexistir com *MIoU* de apenas $59\%$ (Mahjoubi et al., 2023).
3. **Estudo de caso didático sobre *data leakage* generativo e força de *baselines* clássicos (Qi et al., 2024):** Demonstra na prática por que NUNCA se deve treinar um gerador sintético (DDPM/GAN/SMOTE) sobre o conjunto completo antes da validação cruzada e por que SVM/LR/NMF devem sempre figurar como linha de base em curvas 1D (Raman/DRX).

---

## 8. Possíveis aplicações

### `[Análise crítica — Agente E]`
- **DRX de materiais carbonosos/2D:** Adotar **NMF** (destacada por Choudhary et al., 2022) e métodos transparentes de ajuste de picos antes de recorrer a CNNs 1D, mantendo **SVM/LR/RF como *baselines* rigorosos**; caso se use aumento sintético em DRX (p. ex., mistura linear física de fases ou ruído instrumental), aplicá-lo **exclusivamente dentro da dobra de treino do *GroupKFold***.
- **MEV e AFM:** Empregar **quantificação de incerteza e opção de rejeição OOD** (Choudhary et al., 2022) para sinalizar quando um floco de grafeno/óxido de grafeno possui morfologia ou artefato fora do domínio treinado, acionando inspeção humana em vez de gerar estatísticas automáticas espúrias.
- **Triagem de espectroscopia complementar:** Reutilizar o *pipeline* leve de pré-processamento 1D (interpolação em grade fixa + normalização + modelos lineares/SVM) caso sejam incorporados espectros Raman de suporte aos dados de DRX, MEV e AFM.

---

## 9. Evidências

### `[Extraído dos artigos]`
| Trabalho | Tipo / Escopo | Evidências e Números Centrais Verificados | Riscos / Pontos Críticos Apontados |
| :--- | :--- | :--- | :--- |
| **Choudhary et al. (2022)** (*npj Comput. Mater.*) | Revisão abrangente DL em Ciência dos Materiais | MEV FCNN $94\%$ (Azimi); GAN $4\times$ menos *dwell* (De Haan); SPM $99\%$ (Rashidi & Wolkow); UQ (epistêmica vs. aleatória, MC Dropout, Ensembles, GP, OOD reject); NMF em espectros | Duplicatas ICSD causando *leakage*; diferença de *leakage* regressão vs. classificação; lacuna *sim-to-exp*; falta de interpretabilidade |
| **Meng et al. (2024)** (*Front. Phys.*) | Revisão DL em Materiais 2D | STEM U-Net $98\%$ em $3\ \text{s}$ vs. $1\ \text{h}$ (Yang 2021); deformação $0{,}2\ \text{pm}$ (Lee 2020); MO $\text{2DU}^2$-net $99{,}03\%$ / MIoU $94{,}18\%$ (Zhang 2022); AFM+Raman $>99\%$ / **MIoU $59\%$** (Mahjoubi 2023) | Escassez de dados experimentais; desvio simulação-experimento; ausência de *priors* físicos (Seção 6) |
| **Qi et al. (2024)** (*Appl. Mater. Today*, `10.1016/j.apmt.2024.102499`) | Artigo experimental Raman 2D (DDPM + CNN 1D) | $594$ espectros ($10$ classes, $571$ pts); **dados brutos (*10-fold CV*):** CNN **$98{,}8\%$**, SVM $96{,}6\%$, LR $96{,}0\%$; **pós-DDPM ($10.000$ sintéticos):** CNN/ANN/RF/SVM/LR $= \mathbf{1{,}000}$ | Classes com apenas **$6$–$8$ espectros**; provável **vazamento de dados** por DDPM antes da *10-fold CV*; sem *holdout* por substrato/amostra |

---

## 10. Prioridade de estudo

- **Classificação:** **ALTA (Prioridade 1 para Choudhary et al., 2022 e Meng et al., 2024; MÉDIA/CRÍTICA como estudo de caso negativo de validação para Qi et al., 2024)** `[Análise crítica — Agente E]`.
- **Justificativa:** Choudhary et al. (2022) e Meng et al. (2024) formam o alicerce bibliográfico de maior abrangência e autoridade para posicionar a dissertação tanto em metodologias gerais (DRX, MEV, SPM, UQ, *leakage*) quanto no recorte específico de materiais 2D; já Qi et al. (2024) fornecem um alerta metodológico contemporâneo e concreto sobre os perigos de aumento generativo (DDPM) sem separação rigorosa de dobras e sem *holdout* experimental independente.
