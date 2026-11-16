# Fichamento 06 — Ecossistemas de Aprendizado Profundo (Ba Alawi, 2025) e Síntese Metodológica Comparativa: PDI Clássico e Modelos Físicos vs. ML/DL, Interpretabilidade, Incerteza e Validação Antivazamento (`GroupKFold`)

> **Nível de leitura declarado (Seção 8 — `PROMPT_MESTRE.md`):**
> - **Ba Alawi (2025):** **Texto completo lido** (`_scratch/textos_extraidos/Ba_Alawi_2025_Comparative_Survey_PyTorch_vs_TensorFlow.md`, 608 linhas completas).
> - **Aviso explícito de status editorial (*preprint $\rightarrow$ publicado*):** Até **16/11/2026**, `Ba Alawi (2025)` (`arXiv:2508.04035`, DOI `10.48550/arXiv.2508.04035`) **permanece exclusivamente como preprint no arXiv, SEM versão publicada homônima revisada por pares confirmada** (`preprint_to_journal_check.json`: entrada vazia `"Ba Alawi 2025": []`; registros retornados no Crossref correspondem a trabalhos distintos de outros autores em 2024/2026). Ademais, o próprio texto integral contém marcações de rascunho inacabado (`Fig. 2 ... (placeholder chart)` e legendas genéricas `Illustration related to...` nas Figs. 1, 3–6 e 8–16), impondo uso estritamente crítico e secundário.
> - **Fontes da Síntese Metodológica Comparativa (PDI/Física vs. ML/DL para DRX, MEV, AFM, UQ e *GroupKFold*):** Baseada exclusivamente nos textos integrais já lidos e catalogados nesta investigação (`Otsu 1979`, `van der Walt 2014`, `Schindelin 2012`, `Ronneberger 2015`, `Saito 2019`, `Masubuchi 2020`, `Han 2020`, `Leger 2024`, `Choudhary 2022`, `Meng 2024`, `Qi 2024`, `Holm 2020`, `Gerçek 2025`, `Cao 2026`, `Wang 2020`, `Nemes-Incze 2008`, `Chemello 2025`, `NPL VAMAS 2023`, `Nečas & Klapetek 2012`, `Villarrubia 1997`, `Yao 2016`, `Harris 2025` e `Wang et al. 2026`).

---

## 1. Identificação bibliográfica

### Obra principal analisada — Ba Alawi (2025) `[Extraído do manuscrito / catálogo verificado]`
- **Autor:** Zakariya Ba Alawi (indexado como `Alawi, Zakariya Ba` no catálogo bibliográfico).
- **Ano:** 2025.
- **Título completo:** *A Comparative Survey of PyTorch vs TensorFlow for Deep Learning: Usability, Performance, and Deployment Trade-offs*.
- **Veículo / Status:** Preprint não arbitrado — arXiv (Cornell University), identificador `arXiv:2508.04035` (**sem publicação homônima em periódico confirmada até 16/11/2026**).
- **DOI:** `10.48550/arXiv.2508.04035`
- **Link oficial:** <https://doi.org/10.48550/arxiv.2508.04035> (e <https://arxiv.org/abs/2508.04035>)
- **Nível de leitura:** Texto completo do preprint.

### Obras complementares verificadas que sustentam a Síntese Metodológica `[Extraído dos textos/catálogo]`
- **PDI & Metrologia em MEV/AFM/DRX:** `van der Walt et al. (2014)` (`10.7717/peerj.453`), `Schindelin et al. (2012)` (`10.1038/nmeth.2019`), `Nečas & Klapetek (2012)` — Gwyddion (`10.2478/s11534-011-0096-2`), `Villarrubia (1997)` (`10.6028/jres.102.030`), `Nemes-Incze et al. (2008)` (`10.1016/j.carbon.2008.06.022`), `Yao et al. (2016)` (`10.1016/j.jmst.2016.07.020`), `Chemello et al. (2025)` (`10.1088/2632-959x/adae28`), `NPL VAMAS (2023)` (`10.47120/npl.as103`), `GSAS-II` (`10.1107/s0021889813003531`), `Profex` (`10.1107/s1600576715014685`), `Cao (2026)` — XMatcher (`10.48550/arxiv.2607.17162`).
- **ML/DL, UQ, Interpretabilidade e Validação em Materiais:** `Holm et al. (2020)` (`10.1007/s11661-020-06008-4`), `Wang et al. (2020)` (`10.1021/acs.chemmater.0c01907`), `Choudhary et al. (2022)` (`10.1038/s41524-022-00734-6`), `Gerçek et al. (2025)` (`10.48550/arxiv.2511.11485`), `Harris et al. (2025)` (`10.1117/12.3067427`), `Lin Wang et al. (2026)` — PerovSegNet (`10.1038/s41524-026-02211-w`).

---

## 2. Problema investigado

### Obra A — Ba Alawi (2025) `[Extraído do manuscrito]`
- Comparar as duas principais plataformas de *deep learning* da última década — **PyTorch** e **TensorFlow (TF 2.x / Keras)** — quanto a modelo de execução (grafos dinâmicos *define-by-run* vs. grafos híbridos *eager* + `@tf.function`/XLA), facilidade de depuração e usabilidade em pesquisa, desempenho computacional em treino e inferência, gerenciamento de memória em GPU e ecossistema de implantação em produção (*deployment*).

### Síntese Metodológica — Eixo Computacional da Dissertação (PPGCEM/UFCA) `[Análise crítica — Agente E]`
- Responder a uma questão metodológica central para a caracterização de grafeno e materiais 2D por **DRX, MEV e AFM**: **quando métodos clássicos de processamento digital de imagens (PDI) e modelos físico-matemáticos superam ou equivalem a métodos de ML/DL**, e quais critérios técnicos (custo computacional, volume de dados anotados, interpretabilidade, quantificação de incerteza e prevenção de *data leakage* via `GroupKFold`) devem orientar a escolha da pilha computacional na dissertação.

---

## 3. Fundamentação

### Obra A — Ba Alawi (2025) `[Extraído do manuscrito]`
1. **Arquiteturas de execução e compilação:**
   - **PyTorch:** Execução imperativa dinâmica (*define-by-run*) nativa em Python, facilitando controle de fluxo arbitrário e depuração; otimização e exportação via `torch.compile`, **TorchScript**, **ONNX** (*Open Neural Network Exchange*) e **TorchServe**.
   - **TensorFlow 2:** Execução *eager* por padrão combinada à compilação para grafos estáticos via decorador `@tf.function` (*AutoGraph*) e compilador **XLA** (*Accelerated Linear Algebra*); ecossistema de implantação estruturado via **SavedModel**, **TFLite** (dispositivos móveis/borda), **TF.js** (navegador) e **TF-Serving**.
2. **Adoção científica vs. industrial (citações secundárias do levantamento):** A pesquisa aponta preferência maciça pelo PyTorch na literatura acadêmica (PapersWithCode, 2023: $\sim 80\%$ das implementações em conferências como NeurIPS em PyTorch), frente à presença histórica equilibrada em desenvolvimento geral (StackOverflow Developer Survey, 2023: $8{,}41\%$ TensorFlow vs. $7{,}89\%$ PyTorch).

### Síntese Metodológica `[Análise crítica — Agente E]`
A decisão de *framework* (PyTorch vs. TensorFlow vs. `scikit-image`/`SciPy`/`Gwyddion`) deve derivar **do problema físico e do regime de dados**, jamais de moda acadêmica:
- Em **caracterização científica de materiais com $N$ pequeno a moderado** (dezenas a poucas centenas de amostras de DRX/MEV/AFM), grande parte do trabalho ocorre no ecossistema NumPy/SciPy/`scikit-image`/`scikit-learn` (PDI clássico, ajuste físico-matemático de picos, morfologia matemática e ML tabular/espectral com SVM/RF/NMF), no qual PyTorch e TensorFlow só entram quando há justificativa empírica de ganho sobre os *baselines* determinísticos.
- Quando redes profundas são necessárias (por exemplo, U-Net leve para segmentação de MEV como em Gerçek et al., 2025), **PyTorch** alinha-se mais naturalmente ao ecossistema Python científico (`scikit-image`, `numpy`, `scikit-learn`) já previsto no pré-projeto do PPGCEM/UFCA, enquanto **TensorFlow/Keras** mantém presença relevante em *pipelines* legados de materiais 2D (como Mask R-CNN de Masubuchi et al., 2020) e implantação em borda via TFLite.

---

## 4. Metodologia

### Obra A — Ba Alawi (2025) `[Extraído do manuscrito]`
- **Revisão bibliográfica comparativa qualitativa e compilação de benchmarks publicados:** O autor sintetiza arquitetura de grafos, ferramentas de implantação e resultados experimentais reportados em trabalhos comparativos terceiros (especialmente Yapıcı & Topaloğlu, 2021; Novac et al., 2022; Bećirović et al., 2025), sem executar novos experimentos originais próprios em *hardware* controlado e deixando figuras ilustrativas como *placeholders* no manuscrito.

### Metodologia de Síntese e Protocolo Experimental Proposto para a Dissertação `[Análise crítica — Agente E]`
Estabelece-se um protocolo metodológico em **quatro camadas hierárquicas** contra complexidade injustificada e vazamento de dados:
1. **Camada 1 — Baselines Físicos e PDI Clássico (obrigatórios como referência inicial):**
   - **DRX:** Refinamento de perfil/Rietveld (GSAS-II, Profex) ou casamento transparente de picos com quantificação física via mínimos quadrados não-negativos (XMatcher, Cao 2026) + NMF (Choudhary et al., 2022);
   - **MEV:** Correção de fundo/iluminação, filtragem determinística de ruído, limiarização (Otsu/adaptativa), morfologia matemática e *watershed* em `scikit-image` / `Fiji` (`SimpleITK`/top-hat/Otsu como em Gerçek et al., 2025; protocolo interlaboratorial `NPL VAMAS 2023` / `Chemello 2025`);
   - **AFM:** Nivelamento polinomial, remoção de ruído de linha/cicatrizes, deconvolução geométrica de ponta (`Villarrubia 1997`, `Gwyddion` — `Nečas & Klapetek 2012`), histogramas de altura para espessura de grafeno (`Yao et al., 2016`) e verificação física do regime atrativo vs. repulsivo na curva amplitude-distância (`Nemes-Incze et al., 2008`).
2. **Camada 2 — ML Clássico sobre Descritores Físicos e Geométricos:** Extração explícita de descritores (área, excentricidade, circularidade, solidez, largura a meia altura — FWHM, posição $2\theta$, razão de intensidades) alimentando SVM, Regressão Logística ou Random Forest com interpretabilidade direta.
3. **Camada 3 — DL Apenas Quando Justificado Empiricamente:** Redes leves (ex.: U-Net 30,7M como Gerçek et al., 2025, CNN 1D para espectros complexos ou Mask R-CNN para flocos sobrepostos) treinadas apenas se superarem consistentemente as Camadas 1–2 em validação rigorosa fora da amostra.
4. **Camada 4 — Validação Antivazamento com `GroupKFold` / `StratifiedGroupKFold` + UQ:**
   - **Unidade de agrupamento obrigatória:** identificador físico da **amostra / lote de síntese / wafer / sessão de microscopia** (jamais por *patch/tile* recortado, espectro aumentado ou imagem aleatória do mesmo substrato).
   - **Isolamento estrito dentro de cada dobra (*fold*):** Normalização por estatísticas do treino, ajuste de limiares, *data augmentation* e eventual geração sintética (DDPM/GAN) devem ocorrer **exclusivamente dentro do conjunto de treino de cada dobra**, mantendo a dobra de validação inteiramente virgem — evitando tanto o otimismo de *split* por *tiles* observado em Gerçek et al. (2025) quanto o colapso por vazamento generativo identificado em Qi et al. (2024).

---

## 5. Resultados

### Obra A — Ba Alawi (2025) — Benchmarks Compilados (Fontes Secundárias Citadas) `[Extraído do manuscrito]`
- **Yapıcı & Topaloğlu (2021):** TensorFlow apresentou menor tempo em imagens pequenas (MNIST), enquanto PyTorch foi mais rápido e demonstrou gerenciamento mais eficiente de VRAM em imagens maiores.
- **Novac et al. (2022):** PyTorch concluiu treinamento em **$16{,}98\ \text{h}$** vs. **$21{,}95\ \text{h}$** no TensorFlow, e inferência em **$1{,}174\ \text{s}$** vs. **$2{,}667\ \text{s}$** no TensorFlow.
- **Bećirović et al. (2025) — BloodMNIST:** Em $28 \times 28$, PyTorch atingiu **$0{,}3032\ \text{s}$** vs. Keras **$0{,}8985\ \text{s}$**; em $64 \times 64$, JAX registrou **$1{,}2692\ \text{s}$**, PyTorch **$1{,}5961\ \text{s}$** e Keras **$2{,}0182\ \text{s}$**.

### Resultados Comparativos Verificados nas Fontes Primárias da Dissertação (PDI/Física vs. ML/DL, UQ e Vazamento) `[Extraído dos artigos + Análise crítica — Agente E]`

| Técnica / Dimensão | Evidência de PDI Clássico / Modelo Físico | Evidência de ML / DL | Diagnóstico Objetivo (Quando usar cada um) |
| :--- | :--- | :--- | :--- |
| **DRX (Fases e Cristalinidade)** | `GSAS-II` / `Profex` (Rietveld físico); `XMatcher` (Cao, 2026): correspondência transparente 1-a-1 de picos + NNLS AutoMix; **NMF** (Choudhary, 2022) interpretável | **Wang et al. (2020)** (CNN + **pré-filtragem clássica FFT/iFFT**): Top-5 **$96{,}7\%$** em $1.012$ MOFs vs. **$<\!50\%$** ML clássico; `Oviedo (2019)`, `Szymanski (2021)` | **Físico/Clássico** para poucas fases conhecidas e quantificação estrutural rigorosa; **CNN + pré-filtro FFT** para triagem rápida em centenas de estruturas/misturas ruidosas ou orientação preferencial |
| **MEV (Morfologia de Flocos e Fases)** | `Otsu (1979)` + `scikit-image` + `Fiji`; **Gerçek et al. (2025):** `SimpleITK` + Gauss + *top-hat* + Otsu atingiu **Dice $0{,}85$** em *tiles* e **$0{,}90$** no aço inédito ANP-3; **Chemello (2025) / NPL VAMAS (2023):** CV entre operadores nas mesmas imagens de GO foi **$2\%$–$4{,}6\%$** vs. **$\sim 10\%$** da variabilidade de preparo da amostra | **Gerçek et al. (2025):** U-Net ($30{,}7\text{M}$) atingiu **Dice $0{,}98$** em *tiles*, caindo para **$0{,}94$** no aço inédito ANP-3 (ganho real de $+0{,}04$ sobre clássico); **Holm et al. (2020):** linha de 1 px em superliga falha sem máscara em 2 estágios guiada por domínio; Mask R-CNN em pó sobreposto: Prec $97{,}5\%$ / Rec $95{,}4\%$; **Lin Wang et al. (2026):** PerovSegNet | **PDI clássico** vence em custo zero de rotulagem quando o contraste é limpo (e já supera ou empata com variações de preparo de amostra); **U-Net/Mask R-CNN** só compensa quando há partículas sobrepostas, baixo contraste ou iluminação variável |
| **AFM (Topografia e Espessura 2D)** | `Gwyddion` (`Nečas & Klapetek, 2012`); deconvolução de ponta (`Villarrubia, 1997`); histograma de altura (`Yao et al., 2016`); **Nemes-Incze et al. (2008):** regime atrativo vs. repulsivo causa anomalia de até **$\sim 1\ \text{nm}$** na altura medida | `Rashidi & Wolkow` (Choudhary, 2022): condicionamento de ponta SPM ($99\%$); `Harris et al. (2025)` (*SparseC-AFM*): reconstrução esparsa para acelerar varredura lenta | **Física e PDI calibrado são insubstituíveis:** nenhum modelo de DL corrige viés físico de regime atrativo já gravado no mapa $z(x,y)$; DL ajuda apenas na reconstrução de varredura subamostrada ou triagem |
| **Interpretabilidade** | Parâmetros explícitos (limiar $k^*$, FWHM, área/circularidade, picos em $2\theta$, energia de separação intra/interclasse) | **Wang et al. (2020):** NCA + CAMs da 14.ª camada sobre picos físicos de DRX; **Han et al. (2020):** $21$ canais em Depth=5 (cor, borda, forma, tamanho + artefato de borda); **Holm et al. (2020)** Seção IV-C | Exigir mapas de ativação (CAMs/canais internos) para provar que a rede olha para picos/bordas físicas e não para artefatos de recorte ou fundo |
| **Quantificação de Incerteza (UQ)** | Propagação analítica de erro, intervalos de ajuste (Rietveld/R²), desvio inter-operador (`NPL VAMAS`: $2\%$–$4{,}6\%$) | **Choudhary et al. (2022):** epistêmica vs. aleatória, *MC Dropout*, *Deep Ensembles*, *Quantile Regression*, *Deep GP*, rejeição OOD; **Gerçek et al. (2025):** calibração pós-hoc por ***temperature scaling*** ($T = 1{,}87117$ via L-BFGS) + MVE mostrando baixa confiança exatamente nas bordas erradas | Jamais usar *softmax* bruto como probabilidade física; calibrar confiança ($T$-scaling / *ensembles*) e aplicar regra de rejeição OOD |
| **Vazamento de Dados (*Leakage*) & `GroupKFold`** | Risco mínimo em modelos sem ajuste paramétrico complexo (embora limiares manuais *ad hoc* possam sofrer *overfitting* ao lote) | **Wang et al. (2020):** alerta contra inflação de acurácia por *leakage*; **Choudhary (2022):** duplicatas no ICSD; **Gerçek (2025):** queda $0{,}98$ (*tiles*) $\rightarrow 0{,}94$ (aço inédito); **Qi (2024):** $1{,}000$ suspeito pós-DDPM sem isolamento de dobra | **`GroupKFold` / `StratifiedGroupKFold` por amostra física/lote/sessão** é obrigatório para reportar desempenho realista |

---

## 6. Limitações

### Obra A — Ba Alawi (2025) `[Extraído do manuscrito]`
1. **Status de preprint não revisado por pares até 16/11/2026** e qualidade editorial incompleta (*placeholders* explícitos em praticamente todas as figuras: `Fig. 2 ... (placeholder chart)`, `Illustration related to...` nas Figs. 1, 3–6 e 8–16).
2. **Dependência exclusiva de benchmarks de terceiros:** Não apresenta medições reprodutíveis próprias em *hardware* idêntico sob versões recentes estabilizadas (`PyTorch 2.x` com `torch.compile` vs. `TF 2.x` XLA / `Keras 3`), tornando os ganhos pontuais de velocidade dependentes de versões históricas dos artigos citados.
3. **Ausência de escopo em computação científica clássica e materiais:** Não aborda bibliotecas essenciais para PDI e ajuste físico em ciência dos materiais (`scikit-image`, `SciPy`, `lmfit`, `Gwyddion`, `Fiji`).

### Limitações Estruturais na Integração Computacional para Materiais `[Análise crítica — Agente E]`
- A adoção acrítica de *deep learning* (em PyTorch ou TensorFlow) enfrenta três barreiras concretas em pesquisas experimentais de mestrado: (1) custo de anotação física confiável (especialmente quando a anotação exige correlacionar MEV/MO com AFM/Raman); (2) baixa reprodutibilidade entre microscópios/lotes quando *splits* aleatórios ignoram agrupamento físico; e (3) risco de **inversão de esforço**, gastando semanas treinando U-Nets para ganhos marginais ($+0{,}04$ de Dice em Gerçek et al., 2025) quando `scikit-image` + calibração física já resolvem o problema com transparência total e dentro da margem de variabilidade do preparo de amostras ($\sim 10\%$ em `Chemello 2025` / `NPL VAMAS 2023`).

---

## 7. Contribuição para a dissertação

### `[Análise crítica — Agente E]`
Este fichamento cumpre dupla função estruturante na dissertação (PPGCEM/UFCA):
1. **Posicionamento técnico de *stack* computacional:** Justifica de forma transparente por que a base computacional do trabalho deve priorizar **Python científico clássico (`NumPy`, `SciPy`, `scikit-image`, `scikit-learn`) + ferramentas metrológicas dedicadas (`Fiji/ImageJ`, `Gwyddion`)**, adotando **PyTorch** (não por viés acrítico do preprint de Ba Alawi, 2025, mas pela interoperabilidade nativa com `NumPy`/`scikit-image` e prevalência em arquiteturas recentes de segmentação científica como Gerçek et al., 2025) estritamente quando os *baselines* clássicos se mostrarem insuficientes.
2. **Diretriz metodológica rigorosa de avaliação experimental:** Estabelece os pilares que diferenciam uma pesquisa científica sólida de uma aplicação superficial de IA — **comparação contra PDI clássico e modelos físicos**, **interpretabilidade**, **quantificação de incerteza** e **validação cruzada agrupada (`GroupKFold`) contra *data leakage*** — atendendo integralmente às exigências da Seção 3-E do projeto de pesquisa.

---

## 8. Possíveis aplicações

### `[Análise crítica — Agente E]`
- **Desenho do *pipeline* reprodutível em MEV/AFM/DRX:** Estruturar os experimentos da dissertação em *pipelines* `scikit-learn` / Python onde todo pré-processamento (nivelamento, filtro, Otsu/normalização) esteja encapsulado em transformadores ajustados **apenas sobre as amostras de treino** de cada dobra do `GroupKFold(n_splits=...)` indexado pelo código da amostra física/síntese.
- **Relato transparente de variabilidade em métricas de morfologia:** Sempre reportar o desempenho de segmentação em MEV/AFM ao lado da variabilidade experimental de preparo e medição (referência `NPL VAMAS 2023` / `Chemello 2025`: $2\%$–$4{,}6\%$ inter-operador vs. $10\%$ inter-amostra) e, quando usar redes neurais, incluir mapa de erro/incerteza calibrada (ex.: *temperature scaling* ou *MC Dropout*).
- **Uso cauteloso da literatura recente de preprints:** Adotar política explícita de citação distinguindo periódicos revisados por pares de preprints não arbitrados (`Ba Alawi 2025` citado apenas para contextualização arquitetural de PyTorch/TF, nunca como prova isolada de superioridade de desempenho).

---

## 9. Evidências

### `[Extraído dos textos lidos e catálogo verificado]`
- **Ba Alawi (2025 — preprint `arXiv:2508.04035`, sem publicação revisada confirmada até 16/11/2026):**
  - *Benchmarks compilados:* Novac et al. (2022) — PyTorch $16{,}98\ \text{h}$ treino / $1{,}174\ \text{s}$ inferência vs. TF $21{,}95\ \text{h}$ / $2{,}667\ \text{s}$; Bećirović et al. (2025) BloodMNIST $28\times 28$ — PyTorch $0{,}3032\ \text{s}$ vs. Keras $0{,}8985\ \text{s}$, $64\times 64$ — JAX $1{,}2692\ \text{s}$, PyTorch $1{,}5961\ \text{s}$, Keras $2{,}0182\ \text{s}$; Yapıcı & Topaloğlu (2021) — TF mais rápido em MNIST pequeno, PyTorch superior em VRAM/tempo em imagens maiores.
  - *Evidência de rascunho:* Presença de `placeholder chart` e `Illustration related to...` nas figuras 1, 2, 3–6 e 8–16 do próprio preprint.
- **Evidências cruzadas PDI vs. ML/DL, UQ e *Leakage*:**
  - `Gerçek et al. (2025)`: U-Net $30{,}7\text{M}$ Dice **$0{,}98$** (*tiles*) $\rightarrow$ **$0{,}94$** (aço inédito ANP-3) vs. clássico `SimpleITK`+top-hat+Otsu Dice **$0{,}85$** (*tiles*) $\rightarrow$ **$0{,}90$** (ANP-3); *temperature scaling* $T = 1{,}87117$ via L-BFGS.
  - `Wang et al. (2020)`: CNN + FFT/iFFT atinge Top-5 **$96{,}7\%$** em $1.012$ MOFs vs. $<50\%$ ML clássico, com CAMs na 14.ª camada e alerta explícito contra *data leakage*.
  - `Chemello et al. (2025)` / `NPL VAMAS (2023)`: CV entre operadores em MEV de GO = $2\%$–$4{,}6\%$ vs. variação de preparo $\sim 10\%$.
  - `Nemes-Incze et al. (2008)`: erro físico de até $\sim 1\ \text{nm}$ em AFM de grafeno no regime atrativo.
  - `Qi et al. (2024)`: $1{,}000$ em 5 modelos após DDPM sobre classes de $6$–$8$ espectros ilustra risco de vazamento em CV não isolada.

---

## 10. Prioridade de estudo

- **Classificação:** **BAIXA para Ba Alawi (2025) isoladamente (preprint não arbitrado com *placeholders*) / ALTA (Prioridade 1) para a Síntese Metodológica PDI vs. ML/DL, UQ e `GroupKFold` antivazamento** `[Análise crítica — Agente E]`.
- **Justificativa:** O preprint de Ba Alawi (2025) serve apenas como panorama introdutório (e alerta editorial sobre citações de preprints com figuras *placeholder*); por outro lado, o arcabouço comparativo consolidado neste fichamento — contrapondo `scikit-image`/`Fiji`/`Gwyddion`/modelos físicos a U-Net/Mask R-CNN/CNN sob métricas de incerteza, interpretabilidade e validação rigorosa por `GroupKFold` — constitui a espinha dorsal metodológica da abordagem computacional da dissertação.
