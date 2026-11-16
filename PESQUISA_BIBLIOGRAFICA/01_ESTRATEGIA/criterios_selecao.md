# Critérios de Seleção, Exclusão e Auditoria de Preprints — Missão 02 (PPGCEM/UFCA)

**Projeto:** Viabilidade de ferramenta computacional para caracterização de grafeno e materiais relacionados (DRX, MEV, AFM, PDI e ML/VC)  
**Data da auditoria:** 16/11/2026 (`2026-11-16`)  
**Tipo de revisão:** Revisão crítica narrativa estruturada (Seção 5 do [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md))

---

## 1. Critérios de Inclusão (Elegibilidade)

Em alinhamento estrito com a Seção 6 do [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md), foram priorizados trabalhos que atendam aos seguintes critérios cumulativos ou temáticos:

1. **Rigor e revisão científica:** artigos publicados em periódicos revisados por pares, revisões científicas reconhecidas (*Reviews of Modern Physics*, *Nature Materials*, *Nature Nanotechnology*, *Chemical Society Reviews*, *2D Materials*, *Nanoscale Horizons*, *Micron*, *Metallurgical and Materials Transactions A*), padrões metrológicos/normativos (ex.: Iwashita et al. 2004; NPL/VAMAS TWA 41 2023) e anais conferidos por pares.
2. **Equilíbrio entre obras seminais e literatura recente (até novembro de 2026):** inclusão explícita de trabalhos fundacionais (Novoselov et al. 2004; Geim & Novoselov 2007; Castro Neto et al. 2009; Ferrari et al. 2006; Villarrubia 1997; Otsu 1979) lado a lado com estudos de 2020–2026 (Backes et al. 2020; Holm et al. 2020; Huang & Gan 2024; Chemello et al. 2025; Pan et al. 2026). **Contagem de citações e fator de impacto não foram utilizados como critério único de qualidade.**
3. **Pertinência física e metodológica ao problema do PPGCEM/UFCA:**
   - **Eixo A (Grafeno e derivados):** estrutura cristalina hexagonal $sp^2$, bandas de Dirac, empilhamento/número de camadas, defeitos, química de GO/rGO e rotas de **esfoliação eletroquímica** (relevante para o laboratório local da UFCA).
   - **Eixo B (Caracterização experimental):** princípios físicos, resolução, artefatos e limites de **DRX**, **MEV** e **AFM**, além de técnicas complementares indispensáveis (**Raman**, **TEM**, **XPS**) para confirmação de número de camadas ($N$) e densidade de defeitos ($sp^3$/vacâncias).
   - **Eixos C e D (Computação científica, PDI, VC e ML):** algoritmos clássicos de processamento de imagens e ajuste de perfis, bibliotecas abertas consolidadas (`scikit-image`, `Fiji`, `Gwyddion`, `GSAS-II`, `Profex`) e modelos de ML/DL com validação experimental explícita, análise de incerteza e controle de vazamento de dados.
4. **Preprints:** aceitos apenas quando aportam evidência metodológica singular e recente (2025–2026) ainda sem equivalente publicado, **com identificação explícita** do status de preprint não revisado por pares e sujeitos à auditoria descrita na Seção 4.
5. **Verificabilidade integral de metadados:** existência confirmada por DOI/arXiv ID em pelo menos duas fontes oficiais (Crossref/DataCite + OpenAlex/arXiv), com correspondência exata entre título, autores, ano e periódico.

---

## 2. Critérios de Exclusão e Motivos de Descarte

Foram sistematicamente descartados registros recuperados pelas buscas brutas quando incorreram em qualquer um dos critérios abaixo:

| Categoria de Exclusão | Motivo Científico / Metodológico | Exemplos Empíricos Encontrados nas Consultas de 16/11/2026 |
| :--- | :--- | :--- |
| **Falso positivo semântico / fora de escopo** | Presença dos termos `"graphene"`, `"SEM"`, `"XRD"` ou `"machine learning"` em aplicações sem relação com caracterização microestrutural ou física de materiais 2D (ex.: concreto/cimento, biomedicina, entrega de fármacos, espectroscopia agrícola). | `Q-OA-07` (`10.1016/j.conbuildmat.2016.11.083` GO-cimento; `10.1088/0957-4484/27/31/315105` hidrogéis); `Q-OA-21` (`10.1016/j.compag.2022.107027` *wolfberries* por 2D-COS); `Q-EPMC-01/02` (`PMC10200802` macrófagos; `PMC10212980` barreira hematoencefálica). |
| **Uso puramente rotineiro das técnicas** | Artigos de síntese ou dispositivos que apenas listam DRX, MEV ou AFM na seção de materiais sem investigar fundamentos físicos da medição, artefatos ou métodos computacionais de extração. | Grande fração dos `7.300` registros de `Q-OA-03` e dos `570` registros em português de `Q-OA-13` (ex.: `10.18540/jcecvl3iss8pp1118-1130`, `10.51891/rease.v7i7.1670`). |
| **Literatura não científica / sem revisão** | Materiais didáticos, blogs ou apostilas comerciais sem revisão por pares nem rastreabilidade acadêmica. | `Data Science Academy (2022)` — herdado de `IVEFAC333.pptx` (slide 15) e formalmente descartado. |
| **Referências com DOI corrompido ou trocado** | Identificadores presentes em apresentações anteriores que apontavam para obra distinta ou continham erro tipográfico. | `10.1007/s11837-020-04347-6` (Mohammed et al., *JOM*, filmes de $\text{TiO}_2$ — erro atribuído a Holm et al. 2020; corrigido para `10.1007/s11661-020-06008-4`). |
| **Preprints oficialmente retirados (*withdrawn*)** | Manuscritos removidos pelos próprios autores por incompletude ou revisão metodológica impeditiva. | **`Wang et al. (2026)` (`arXiv:2608.22400v2`)** — descartado obrigatoriamente (ver Seção 4.3). |
| **Escopo periférico / falta de validação experimental** | Preprints recentes de engenharia de *frameworks* ou modelagem puramente teórica sem vínculo direto com caracterização experimental por DRX/MEV/AFM (mantidos apenas em observação ou contexto histórico quando citados anteriormente). | `Ba Alawi (2025)` (`arXiv:2508.04035v1` — mantido apenas para contextualizar o antecedente PyTorch/TensorFlow de `IVEFAC333.pptx`, fora do núcleo de Materiais); `Costa et al. (2026)` (`arXiv:2609.19191v1`) e `Dabrowski et al. (2026)` (`arXiv:2609.37827v1`) mantidos como referência secundária/não prioritária. |

---

## 3. Síntese Quantitativa do Funil de Seleção

- **Total de registros retornados nas consultas exploratórias brutas (OpenAlex `Q-OA-01`–`Q-OA-22` com sobreposição entre strings + arXiv + Europe PMC):** milhares de registros brutos (ex.: `7.300` em `Q-OA-03` DRX+grafeno amplo; `1.130` em `Q-OA-02` esfoliação eletroquímica; `786` em `Q-OA-05` AFM+espessura; `418` em `Q-OA-04` DRX por título; `173` em `Q-OA-22` MEV+tamanho lateral; `133` em `Q-OA-21` ML+2D por título; `87` em `Q-OA-06` convolução de ponta; `34` em `Q-OA-08` MEV+contraste/camadas; `570` + `85` + `106` nas consultas em português `Q-OA-13..15`).
- **Triagem de relevância e remoção de duplicatas / ruído semântico:** inspeção dos primeiros resultados por relevância/citações, encadeamento bibliográfico e auditoria de histórico produziu o conjunto verificado central da Missão 02.
- **Catálogo verificado consolidado (`verified_catalog.json`):** **59 obras/datasets/padrões verificados** com DOIs ativos no Crossref/DataCite e metadados no OpenAlex.
- **Textos completos legalmente baixados e extraídos para leitura aprofundada:** **27 PDFs** em `ARTIGOS_PDF/` (incluindo `Backes et al. 2020`, `NPL VAMAS 2023`, e 29 arquivos em `_scratch/textos_extraidos/` considerando fontes complementares).
- **Novos achados promissores identificados na Passagem 2 das consultas (16/11/2026):**
  - `Martins et al. (2025)` — *Dimensional analysis of graphene oxide using a computational segmentation model applied to microscopy images*, *Química Nova*, `10.21577/0100-4042.20250243` (descoberto em `Q-OA-18`; estudo brasileiro LNCC/UFBA/ABNT integrando SEM, AFM e segmentação computacional para GO).
  - `MaskTerial` (`arXiv:2412.09333v1` / *Digital Discovery*, `10.1039/D5DD00156K`, descoberto em `Q-ARX-02`) — candidato de Passagem 2 para o estado da arte em detecção automatizada de flocos 2D.
- **Excluído após auditoria crítica de preprints:** `1` preprint retirado oficialmente (`Wang et al. 2026`, `arXiv:2608.22400v2`).

---

## 4. Auditoria Sistemática de Preprints (Preprint-to-Journal & Retiradas)

Em conformidade com a exigência de controle de qualidade da Missão 02, todos os preprints arXiv levantados na Missão 01 e na Passagem 1 da Missão 02 foram auditados em **16/11/2026** cruzando `search_arxiv.py --id_list`, OpenAlex (`preprint_to_journal_check.json`) e Crossref (`crossref_preprint_check.json`).

### 4.1 Preprints Confirmados como Publicação Definitiva Revisada por Pares (Promovidos)

Nos casos abaixo, a referência ativa da revisão bibliográfica passa a ser **obrigatoriamente a versão definitiva publicada em periódico/anais**, utilizando o respectivo DOI oficial:

| Trabalho | Identificador Preprint Original | Status no arXiv (`doi` / `journal_ref`) | Publicação Definitiva Verificada (Crossref + OpenAlex) | DOI Oficial Adotado |
| :--- | :--- | :--- | :--- | :--- |
| **Leger et al. (2024)** | `arXiv:2406.16211v1` | Campo `doi` vazio no arXiv (`21 pages, 6 figures`) | *Scientific Reports*, v. 14, n. 1, art. 27808, 2024 (*Machine learning enabled fast optical identification and characterization of 2D materials*) | `10.1038/s41598-024-79386-z` |
| **Qi et al. (2024)** | `arXiv:2312.01389v1` (e SSRN `10.2139/ssrn.4930953`) | Campo `doi` vazio no arXiv | *Applied Materials Today*, v. 41, art. 102499, 2024 (*Deep learning assisted Raman spectroscopy for rapid identification of 2D materials*) | `10.1016/j.apmt.2024.102499` |
| **Pan et al. / Wang et al. (2026)** | `arXiv:2509.26548v1` (como *Pan, Wang & Cai 2025*) | Campo `doi` vazio no arXiv | *npj Computational Materials*, v. 12, n. 1, 2026 (*Automated and Scalable SEM Image Analysis of Perovskite Solar Cell Materials via a Deep Segmentation Framework*; autores finais: Lin Wang, Tianxiang Hu, Jianguo Pan, Hao Zhang, Yiqiang Zhan, Xia Cai) | `10.1038/s41524-026-02211-w` |
| **Greasley & Hosein (2023)** | `arXiv:2211.08591v1` | `doi: 10.1007/s10853-023-08343-4` presente no arXiv | *Journal of Materials Science*, v. 58, n. 12, p. 5334–5348, 2023 (*Exploring supervised machine learning for multi-phase identification and quantification from powder X-ray diffraction spectra*) | `10.1007/s10853-023-08343-4` |
| **Harris et al. (2025)** | `arXiv:2507.13527v1` | `doi: 10.1117/12.3067427` presente no arXiv | *Proceedings of SPIE — Low-Dimensional Materials and Devices*, p. 35, 2025 (*Sparse C-AFM: a deep learning method for fast and accurate characterization of MoS2 with conductive atomic force microscopy*) | `10.1117/12.3067427` |

*(Observação adicional de `Q-ARX-01`/`Q-ARX-02`: na busca arXiv também emergiram `2506.20467v1` $\rightarrow$ `10.1021/acs.jpclett.5c00322`, `2412.09333v1` $\rightarrow$ `10.1039/D5DD00156K`, `2103.09449v1` $\rightarrow$ `10.1038/s41598-021-85159-9`, confirmando a importância de verificar sempre o campo `doi` e buscar o título no OpenAlex/Crossref.)*

### 4.2 Preprints Mantidos com Ressalva Explícita de Não Revisão por Pares em Periódico

| Trabalho | Identificador | Observação de Auditoria (16/11/2026) | Enquadramento no Projeto |
| :--- | :--- | :--- | :--- |
| **Gerçek et al. (2025)** | `arXiv:2511.11485v1` (`10.48550/arxiv.2511.11485`) | Possui `journal_ref` de *workshop* (*Machine Learning and the Physical Sciences Workshop @ NeurIPS 2025*, OpenReview `xYY5pn4f8N`) e dataset aberto associado com DOI `10.14278/rodare.4123` (RODARE, 13 pares SE2/InLens). | Aceito como evidência de eficiência amostral em segmentação SEM (U-Net em 10 imagens), identificando explicitamente status de *workshop*/preprint e domínio em aços (exige validação própria em grafeno). |
| **Cao (2026)** | `arXiv:2607.17162v1` (`10.48550/arxiv.2607.17162`) | Candidatos homônimos em Crossref (`Profex 2016`, `1967`) não correspondem à obra; permanece preprint arXiv sem revisão por pares em periódico. | Citado com ressalva explícita apenas como referência de ferramenta aberta recente para alinhamento/matching interpretável em DRX (`XMatcher`). |
| **Ba Alawi (2025)** | `arXiv:2508.04035v1` (`10.48550/arxiv.2508.04035`) | Candidatos em Crossref (`2026`, `2024`) são obras de outros autores; permanece preprint `cs.LG` (14 pp.). | Mantido somente na auditoria histórica do piloto `IVEFAC333.pptx` (PyTorch vs. TensorFlow), sem pertinência à física de materiais. |

### 4.3 Descarte Obrigatório por Retirada Oficial (*Withdrawn*)

> [!CAUTION]
> **Descarte de `Wang et al. (2026)` — `arXiv:2608.22400v2`:**  
> Durante a Missão 01 ([`05_plano_bibliografico.md`](file:///C:/Users/emer/dissertacao/Missao1/preparacao_ambiente/05_plano_bibliografico.md)), o preprint *Diagnosing and narrowing the simulation-to-real gap in powder X-ray diffraction with a wet-dry agentic loop* (`arXiv:2608.22400v2`, Shaoguang Wang et al., submetido em 2026-08-23) havia sido incluído como evidência preliminar sobre *simulation-to-real gap* em PXRD. Contudo, na auditoria sistemática de preprints executada em **16/11/2026** via `search_arxiv.py --id_list 2608.22400v2` (arquivo [`arxiv_2608_22400v2.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_2608_22400v2.json)), constatou-se no campo oficial `comment` a seguinte declaração dos autores:
> *"The authors have determined that the manuscript in its current form has not yet reached the level of completeness and refinement intended for public dissemination. We therefore request withdrawal of the current submission"*  
> **Decisão:** O trabalho foi **integralmente descartado** da biblioteca ativa, dos fichamentos e das evidências da Missão 02, não devendo ser citado no Seminário I nem na dissertação. A discussão sobre *sim-to-real gap* em DRX e deslocamento de picos apoia-se exclusivamente em literatura verificada e ativa (ex.: Oviedo et al. 2019 `10.1038/s41524-019-0196-x`; Lee et al. 2020 `10.1038/s41467-019-13749-3`; Wang et al. 2020 `10.1021/acs.jcim.0c00020`; Szymanski et al. 2021 `10.1021/acs.chemmater.1c01071`; Greasley & Hosein 2023 `10.1007/s10853-023-08343-4`).
