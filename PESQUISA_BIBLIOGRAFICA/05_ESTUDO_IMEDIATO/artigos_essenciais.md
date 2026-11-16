# Plano de Estudo Imediato — Artigos Essenciais (Seminário I · 17/11/2026)

**Pesquisador:** Emerson de Sousa Gomes | **Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
**Programa / Disciplina:** PPGCEM / UFCA — Seminários I  
**Data do plano de leitura:** 16/11/2026 (véspera da apresentação de 17/11/2026)  
**Tema investigado:** Viabilidade de ferramenta computacional para apoiar a caracterização de grafeno e materiais relacionados via **DRX**, **MEV** e **AFM** (fase investigativa).

> [!IMPORTANT]
> **Rigor Editorial e Auditoria de Preprints:**  
> 1. O preprint **`Wang et al. (2026)` (`arXiv:2608.22400v2`)** foi **oficialmente retirado (*withdrawn*) pelos autores** em função de incompletude metodológica ([`arxiv_2608_22400v2.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_2608_22400v2.json)) e foi **integralmente excluído** deste guia. A discussão sobre aprendizado de máquina em DRX e limitação *simulation-to-real* baseia-se exclusivamente em artigos revisados por pares (**`Oviedo et al., 2019`** e **`Greasley & Hosein, 2023`**).  
> 2. O DOI de **`Holm et al. (2020)`** foi corrigido de `10.1007/s11837-020-04347-6` (corrompido no legado) para **`10.1007/s11661-020-06008-4`**.  
> 3. Cada bloco declara explicitamente se a leitura baseia-se em **Texto completo lido** (com seções/figuras/páginas verificadas) ou em **Resumo/metadados verificados** (casos de periódicos fechados sem acesso aberto na estação local).

---

## Visão Geral do Roteiro de Hoje (`16/11/2026`)

| Ordem | Bloco Temático | Artigos / Documentos Essenciais | Status de Leitura | Tempo Sugerido |
| :---: | :--- | :--- | :--- | :---: |
| **1** | **AFM e Anomalia de Espessura** | `Nemes-Incze et al. (2008)` + `Shearer et al. (2016)` | Completo + Resumo | ~45 min |
| **2** | **Visão Computacional e ML em Microestruturas** | `Holm et al. (2020)` | Completo | ~45 min |
| **3** | **Produção Heterogênea e Padronização de Grafeno/GRMs** | `Backes et al. (2020)` [seções-alvo] + `Kauling et al. (2018)` + `NPL/VAMAS (2023)` | Completo (seções/protocolo) + Resumo | ~60 min |
| **4** | **Física e Limites da DRX em Carbono/Grafite/GO** | `Li, Lu & Xia (2007)` + `Holzwarth & Gibson (2011)` | Resumos/sínteses verificadas | ~30 min |
| **5** | **Contraste Quantitativo em MEV de Grafeno** | `Zhou et al. (2016)` + `Huang & Gan (2024)` | Completo + Preview/Resumo | ~45 min |
| **6** | **Pipelines Automatizados de Segmentação em 2D** | `Masubuchi et al. (2020)` + `Saito et al. (2019)` | Completos | ~45 min |
| **7** | **ML/DL em DRX e Limitação Sim-to-Real** | `Oviedo et al. (2019)` + `Greasley & Hosein (2023)` | Completos | ~50 min |
| **Total** | **7 blocos indispensáveis (14 referências verificadas)** | — | **10 textos integrais + 4 resumos/metadados** | **~5h20** |

> [!TIP]
> Se o tempo disponível hoje for mais curto (~2h30), priorize a leitura imediata dos blocos **1, 3 (`NPL/VAMAS` + `Backes IX.1.2/IX.2.1`), 5 (`Zhou 2016`) e 7 (`Oviedo 2019` + `Greasley & Hosein 2023`)**, complementando com os resumos já sintetizados em [`fichamentos_prioritarios.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/fichamentos_prioritarios.md) e as respostas diretas em [`questoes_para_estudar.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/questoes_para_estudar.md).

---

## Bloco 1 — AFM e Anomalia de Espessura em Grafeno

- **Referência 1.1 (Texto completo lido):** Nemes-Incze, P., Osváth, Z., Kamarás, K., & Biró, L. P. (2008). *Anomalies in thickness measurements of graphene and few layer graphite crystals by tapping mode atomic force microscopy.* *Carbon*, 46(11), 1435–1442. DOI: `10.1016/j.carbon.2008.06.022` | Texto extraído: [`Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.md)
- **Referência 1.2 (Resumo e metadados verificados — acesso fechado):** Shearer, C. J., Slattery, A. D., Stapleton, A. J., Shapter, J. G., & Gibson, C. T. (2016). *Accurate thickness measurement of graphene.* *Nanotechnology*, 27(12), 125704. DOI: `10.1088/0957-4484/27/12/125704` (já citado no piloto [`IVEFAC333.pptx`](file:///C:/Users/emer/dissertacao/Artigos/Apresentacoes_passadas/IVEFAC333.pptx), mas sem DOI no slide 15)

### 1. Por que estudar
Estes dois trabalhos derrubam o mito de que "basta medir a altura do degrau no AFM para saber o número de camadas de grafeno". Em um seminário de Ciência e Engenharia de Materiais, qualquer afirmação ingênua de que monocamada mede sempre $0{,}335\text{ nm}$ no AFM será imediatamente contestada pela banca. Nemes-Incze et al. (2008) explicam o mecanismo físico da distorção de até $\sim 1\text{ nm}$ no modo *tapping* convencional, e Shearer et al. (2016) definem o protocolo moderno em *PeakForce tapping* capaz de reduzir o erro da primeira camada, destacando também o limite de confiança de medidas diretas por AFM.

### 2. Que seções merecem atenção
- **Em `Nemes-Incze et al. (2008)` (`Texto completo lido`):**
  - *Introduction* (pp. 1–2): variação histórica relatada ($0{,}35\text{–}1{,}6\text{ nm}$ para monocamada sobre $\text{SiO}_2$).
  - *Results and Discussion* (pp. 3–6) e **Figuras 1, 2a–c, 3, 4, 5, 6 e 7**: salto de altura ($0{,}8\text{–}1\text{ nm}$) em função da amplitude livre ($A_0$), curvas amplitude-distância (AD) exibindo biestabilidade e trocas aleatórias de altura linha a linha, comparação TAFM vs. Raman ($488\text{ nm}$) e efeito de atrito lateral no modo contato (CAFM).
  - *Conclusions* (pp. 6–7): recomendação operacional de operar no **regime repulsivo** tanto sobre o $\text{SiO}_2$ quanto sobre o grafeno e validar contra Raman.
- **Em `Shearer et al. (2016)` (`Resumo e metadados verificados` — texto completo fechado):**
  - Quando obtiver o PDF via Portal de Periódicos CAPES/UFCA, buscar especificamente a seção experimental comparando **pontas padrão vs. pontas modificadas com nanotubos de carbono (CNT)**, a **calibração de força/pressão aplicada em *PeakForce tapping*** e a quantificação da **camada de adsorvato grafeno–substrato** que justifica a faixa literária de $0{,}4\text{–}1{,}7\text{ nm}$ e a redução do erro para $0{,}1\text{–}0{,}3\text{ nm}$.

### 3. Que conceitos físicos precisam ser dominados
- Regimes de interação ponta–amostra em AFM dinâmico (*tapping*): **regime atrativo** (longo alcance: van der Waals, forças eletrostáticas e principalmente **forças capilares histeréticas** da película de água ambiente) vs. **regime repulsivo** (contato mecânico intermitente de curto alcance).
- **Biestabilidade e salto nas curvas Amplitude–Distância (AD):** dois deslocamentos piezoelétricos distintos ($\Delta z \sim 1\text{ nm}$) correspondem à mesma amplitude de *setpoint*, causando chaveamento aleatório na malha de *feedback*.
- **Diferença de molhabilidade / amortecimento grafeno vs. $\text{SiO}_2$:** o regime repulsivo inicia em amplitudes livres distintas sobre óxido ($\sim 21\text{ nm}$) e sobre grafeno ($\sim 25\text{–}26\text{ nm}$), gerando *offset* instrumental de altura.
- **Fricção lateral em modo contato (CAFM)** causando discrepância ($\sim 0{,}2\text{ nm}$) entre varredura ida/volta, e **pressão da ponta + camada de adsorvato** em *PeakForce tapping*.

### 4. Que resultado é relevante
- **`Nemes-Incze et al. (2008)`:** uma mesma folha FLG caiu de $4{,}5\text{ nm}$ para $2{,}25\text{–}2{,}3\text{ nm}$ ($\sim 7$ camadas) quando $A_0$ ultrapassou $\sim 26\text{ nm}$ com *setpoint* $15\text{ nm}$ (Fig. 4); monocamadas confirmadas por Raman $2D$ mediam $\sim 1\text{ nm}$ em baixa amplitude livre e aproximavam-se do valor real somente no regime repulsivo em ambas as superfícies (Fig. 6). Degraus *grafeno sobre grafeno* mantiveram altura constante independente de $A_0$ (Fig. 1c).
- **`Shearer et al. (2016)` (resumo verificado):** documentam a faixa de $0{,}4\text{–}1{,}7\text{ nm}$ relatada para SLG na literatura e mostram que o protocolo com *PeakForce tapping* + controle de pressão/pontas CNT reduz o erro de medição da primeira camada de **$0{,}1\text{–}1{,}3\text{ nm}$ para $0{,}1\text{–}0{,}3\text{ nm}$**.

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Se uma monocamada de grafeno tem $0{,}335\text{ nm}$ de espessura interplanar, por que o AFM mede frequentemente $0{,}8\text{–}1{,}2\text{ nm}$?"*
- *"Um algoritmo de visão computacional pode ler uma imagem AFM bruta e converter a altura em nanômetros diretamente em número de camadas dividindo por $0{,}335\text{ nm}$?"* (Resposta: **Não**, sem controle do regime de aquisição, calibração de *offset* por adsorvato/substrato e validação complementar.)
- *"Por que o piloto anterior em `QUAM-AFM Lite` não tem relação com esse problema físico?"* (Porque `QUAM-AFM` simula nc-AFM submolecular com ponta de CO em UHV, não *tapping*/*PeakForce* em flocos suportados com menisco capilar e adsorvatos.)

### 6. Tempo aproximado de leitura
- **45 min** (~35 min para revisão das figuras e discussão de `Nemes-Incze et al., 2008`; ~10 min para fixação dos parâmetros e limites do resumo de `Shearer et al., 2016`).

---

## Bloco 2 — Visão Computacional e Aprendizado de Máquina em Microestruturas

- **Referência 2.1 (Texto completo lido):** Holm, E. A., Cohn, R., Gao, N., Kitahara, A. R., Matson, T. P., Lei, B., & Yarasi, S. R. (2020). *Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis.* *Metallurgical and Materials Transactions A*, 51(12), 5985–5999. DOI: **`10.1007/s11661-020-06008-4`** | Texto extraído: [`Holm_2020_Overview_CV_ML_Microstructural_Characterization.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Holm_2020_Overview_CV_ML_Microstructural_Characterization.md) | Fichamento: [`05_holm_2020_mmta_overview_cv_ml_microstructural_characterization.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/05_holm_2020_mmta_overview_cv_ml_microstructural_characterization.md)

### 1. Por que estudar
É a referência estruturante herdada do pré-projeto ([`pre-projeto-da-selecao.md`](file:///C:/Users/emer/dissertacao/Artigos/Pr%C3%A9%20projeto/pre-projeto-da-selecao.md)) e da apresentação anterior, além de corrigir o DOI errado herdado no histórico. O artigo estabelece exatamente a **taxonomia computacional** que organiza o problema de pesquisa da dissertação (classificação, segmentação semântica, detecção de objetos e segmentação de instâncias) e explica por que imagens microscópicas funcionam com bancos menores do que imagens naturais — mas também onde redes neurais falham sem conhecimento de domínio.

### 2. Que seções merecem atenção
- **Texto completo lido — foco prioritário:**
  - *Section I — Introduction* (pp. 5985–5986): os dois problemas fundamentais (*what to measure* vs. *how to measure it*) e *missing boundaries* (Fig. 1).
  - *Section II.A–C — Methods* (pp. 5986–5989, **Fig. 2**): extração de vetores de características via CNNs pré-treinadas (transferência da VGG16/ImageNet), conceito de **hipercolunas por pixel**, comparação SVM / Random Forest / ANN / k-means / t-SNE e regras de coleta de dados (**redundância sem sobreposição**, padronização, *data augmentation* e **metadados multimodais**).
  - *Section III.A–D — Results: A Taxonomy of Microstructural Analysis* (pp. 5989–5995, **Figs. 3–8**): casos de uso reais em MEV e microscopia óptica (aços UHCS, pós metálicos, superligas de Ni).
  - *Section IV.A–C — Next Steps* (pp. 5995–5997, **Fig. 9**): novas métricas visuais, conexão PSP (*Processing–Structure–Property*) e interpretabilidade ("abrir a caixa-preta").

### 3. Que conceitos físicos precisam ser dominados
- **Taxonomia de tarefas em visão computacional (Fig. 3):** diferença rigorosa entre *classificação da imagem inteira*, *segmentação semântica* (classe por pixel, não separa objetos que se tocam), *detecção de objetos* (caixas delimitadoras) e *segmentação de instâncias* (máscara individual por partícula/floco mesmo em sobreposição).
- **Invariância de CNNs:** convoluções são invariantes à **translação**, mas **não são invariantes à rotação nem à escala/magnificação** — crucial ao misturar micrografias de diferentes ampliações.
- **Riqueza de informação e limite físico:** *data augmentation* facilita o treinamento, mas **não cria nova informação física** além das imagens originais; e características 3D raramente são totalmente capturadas por projeções ou seções 2D.

### 4. Que resultado é relevante
- Classificação SVM sobre vetores CNN atingiu **$99 \pm 1\%$** de acurácia no banco UHCS (961 imagens); regressão profunda em 15.213 microestruturas sintéticas SPPARKS estimou tamanho de grão com erro padrão de **$2{,}3\%$** (e **$3{,}9\%$** mesmo com $40\%$ de contornos apagados).
- Segmentação semântica via transferência (*PixelNet*) atingiu **$93\%$** com apenas **20 imagens** anotadas de aço UHCS (4 de teste) e **$99{,}6\%$** com **30 imagens** de dendritas Al–Zn (10 de teste).
- Na segmentação de instâncias de pós metálicos em MEV (apenas 3 imagens de treino / 2 de teste com centenas de partículas), Mask R-CNN alcançou **precisão $97{,}5\%$ e revocação $95{,}4\%$** para partículas principais (caindo para $69{,}2\% / 54{,}5\%$ em partículas satélites ambíguas).
- Em contraste, em superligas de Ni (17 imagens ECCI), a rede U-Net sozinha **não conseguiu distinguir** discordâncias de contornos $\gamma\text{–}\gamma'$ com anotações de 1 pixel, exigindo combinação explícita com máscara regional guiada por especialista (Fig. 7).

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Se você só tem dezenas de micrografias no laboratório do PPGCEM, é inviável treinar visão computacional ou redes neurais?"* (Explica por que imagens de microscopia são estatisticamente ricas e como *transfer learning* + hipercolunas funcionam com 5–30 imagens anotadas, desde que sem *data leakage* e com validação rigorosa.)
- *"Qual a diferença entre usar uma segmentação semântica (como U-Net) e uma segmentação de instâncias (como Mask R-CNN) para medir flocos de grafeno?"* (Semântica funde flocos em contato; instância separa flocos individuais para distribuição de tamanho lateral.)
- *"Por que não confiar cegamente em uma rede neural sem interpretação física?"* (Caso das superligas da Fig. 7 e Seção IV.C sobre caixa-preta.)

### 6. Tempo aproximado de leitura
- **45 min** (revisão focada nas Seções I, II.A–C, III.B–D e IV.C; ~15 páginas densas em duas colunas).

---

## Bloco 3 — Produção Heterogênea e Padronização Metrológica de Grafeno/GRMs

- **Referência 3.1 (Texto completo lido nas seções-alvo):** Backes, C. et al. (2020). *Production and processing of graphene and related materials.* *2D Materials*, 7(2), 022001. DOI: `10.1088/2053-1583/ab1e0a` | Texto extraído: [`Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md) (monografia de 283 pp.; lidas Seções `II.1–II.6`, `IX.1.2`, `IX.1.3`, `IX.2.1` e `IX.2.3`)
- **Referência 3.2 (Resumo e metadados verificados — acesso fechado):** Kauling, A. P., Seefeldt, A. T., Pisoni, D. P., Pradeep, R. C., Bentini, R., Oliveira, R. V. B., Novoselov, K. S., & Castro Neto, A. H. (2018). *The Worldwide Graphene Flake Production.* *Advanced Materials*, 30(44), e1803784. DOI: `10.1002/adma.201803784`
- **Referência 3.3 (Texto completo lido):** Despotelis, K., Pollard, A., Clifford, C., & Paton, K. (2022/2023). *VAMAS TWA 41 - Graphene and Related 2D Materials Project 12 - Distribution of lateral size and thickness of few-layer graphene flakes using SEM and AFM. SEM and AFM measurement protocol.* NPL Report AS 103 (nov. 2022; indexado OpenAlex 2023; projeto EMPIR `19NORM04 ISO-G-SCoPe`). DOI: `10.47120/npl.as103` | Texto extraído: [`NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.md)

### 1. Por que estudar
Conecta diretamente a **realidade experimental do grafeno produzido por esfoliação líquida e eletroquímica** (rota utilizada na UFCA segundo [`IVEFAC333.pptx`](file:///C:/Users/emer/dissertacao/Artigos/Apresentacoes_passadas/IVEFAC333.pptx)) com a **metrologia normativa internacional** (`ISO/TS 21356-1`, `VAMAS TWA 41`). Em vez de amostras ideais de grafeno esfoliado por fita adesiva (*Scotch tape*), a produção escalável gera dispersões altamente polidispersas em tamanho lateral, número de camadas ($N$), oxidação ($C/O$) e defeitos — e o mercado global sofre com "falso grafeno" (microplaquetas de grafite), exigindo protocolos estatísticos padronizados que uma futura ferramenta computacional deve automatizar.

### 2. Que seções merecem atenção
- **Em `Backes et al. (2020)` (`Texto completo lido nas seções-alvo`):**
  - *Section II.5 & II.6* (pp. 42–46, **Fig. II.20–II.21**): esfoliação eletroquímica aquosa (ácido sulfúrico vs. sais de sulfato vs. *scavengers* como TEMPO), não aquosa e comparação entre sonicação, oxidação química (GO/rGO) e esfoliação eletroquímica.
  - *Section IX.1.2.1–IX.1.2.2* (pp. 188–197, **Figs. IX.11–IX.19**): protocolo AFM para dispersões LPE (substrato pré-aquecido, lavagem de surfactante, calibração por degraus de terraço + Raman, $100\text{–}150$ flocos, altura aparente de $1\text{–}2\text{ nm}$ para SLG), comparação dinâmico vs. contato em isolantes (**Fig. IX.15**), contraste de fase reversível (**Fig. IX.14**), *tip sweeping* e KPM.
  - *Section IX.1.3* (pp. 198–201, **Fig. IX.21–IX.23**): TEM para estatística de tamanho lateral ($\sim 150$ contagens), franjas `(0002)` em bordas dobradas e HRTEM de baixa energia ($\le 80\text{ kV}$).
  - *Section IX.2.1 & IX.2.3* (pp. 210–222, **Figs. IX.35–IX.40, IX.49, Tabela IX.2**): espectroscopia Raman ($2D$, $I(D)/I(G)$ corrigido por dopagem) e XPS ($C1s$ $sp^2/sp^3$ e grupos oxigenados).
- **Em `NPL/VAMAS (2023)` (`Texto completo lido` — 24 pp. integrais):**
  - *Section 2 & 3* (pp. 1–5): separação obrigatória de substratos (`Si` com óxido nativo para MEV vs. `SiO2 300 ± 5 nm` para AFM/OM) e triagem óptica prévia evitando resíduos.
  - *Section 4* (pp. 6–12, **Figs. 5–7**): protocolo MEV completo ($\le 5\text{ kV}$, pixel $<10\text{ nm}$, $\ge 200$ flocos isolados sem sobreposição, comprimento $L$ + largura bissetriz perpendicular $W$, grade de calibração `Pelcotec G-1T um`, histograma lognormal $\ge 20$ *bins*).
  - *Section 5* (pp. 13–22, **Figs. 10–17**): protocolo AFM completo (*tapping* *closed-loop*, *setpoint* $40\% < \text{sp} \le 70\%$, $512 \times 512\text{ px}$, exclusão de ponta dupla/*flying tip*, nivelamento com mascaramento, $\ge 20$ flocos cobrindo a faixa do MEV e gráfico espessura vs. tamanho lateral).
- **Em `Kauling et al. (2018)` (`Resumo e metadados verificados` — texto completo fechado):**
  - No PDF completo (quando acessado via CAPES/UFCA), verificar a **matriz de qualidade dos 60 produtores**, os critérios limiares entre grafeno, FLG e microplaquetas de grafite e as funções de distribuição propostas para $(N, L)$.

### 3. Que conceitos físicos precisam ser dominados
- **Polidispersidade e distribuições lognormais:** processos de esfoliação líquida/eletroquímica geram populações assimétricas em tamanho lateral ($L$) e espessura ($N$), tornando médias simples insuficientes; importa também a média ponderada por fração volumétrica $\langle N \rangle_{V_f} = \sum N^2 LW / \sum NLW$ (Backes Sec. IX.1.2.1).
- **Troca entre rendimento/velocidade e oxidação/defeitos na esfoliação eletroquímica:** radicais $\text{HO}^\bullet / \text{O}^\bullet$ da eletrólise da água oxidam as folhas, reduzindo $C/O$, enquanto sais neutros/sequestrantes preservam melhor a rede $sp^2$ (Backes Sec. II.5).
- **Contaminação carbonácea induzida por feixe no MEV e carregamento elétrico:** o feixe eletrônico deposita carbono amorfo sobre a área varrida, **proibindo fazer AFM depois de MEV na mesma área** (VAMAS Sec. 4.1).
- **Morfometria padronizada:** distinção entre o método da bissetriz perpendicular ($L, W$ na `ISO/TS 21356-1` / VAMAS) e medidas por área/Feret, além do viés humano de seleção de flocos grandes.

### 4. Que resultado é relevante
- **`Backes et al. (2020)`:** mostra que dispersões LPE não fracionadas têm rendimento de monocamada $Y_M < 1\%$, enquanto esfoliação eletroquímica aquosa em sais de sulfato alcança $>85\%$ de $1\text{–}3\text{LG}$ com $C/O \sim 17{,}2$ (e até $C/O \sim 25{,}3$ com TEMPO), embora altamente polidispersa; no AFM de amostras LPE, a altura aparente de `1L` varia tipicamente de **$1\text{ a }2\text{ nm}$** por solvente/surfactante residual (p. 191), e sobre isolantes como quartzo a espessura em modo dinâmico pode parecer o dobro da obtida em modo contato por *crosstalk* eletrostático (Fig. IX.15).
- **`Kauling et al. (2018)` (resumo verificado):** avaliando 60 produtores comerciais com suíte multimodal (SEM, TEM, AFM, Raman, XPS, análise elementar), comprovaram que a maioria comercializa **microplaquetas de grafite**, não grafeno verdadeiro, propondo classificação estatística por distribuições de $N$ e tamanho.
- **`NPL/VAMAS (2023)`:** fixa os limiares metrológicos concretos para intercomparação internacional: **$\ge 200$ flocos isolados no MEV** (pixel $<10\text{ nm}$, histograma lognormal $\ge 20$ *bins*, calibração pós-ensaio em 3 regiões) acoplados a **$\ge 20$ flocos planos no AFM** distribuídos na mesma faixa lateral e analisados por 3 perfis transversais + RMS do substrato.

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Quantos flocos preciso medir no MEV e no AFM para que a caracterização estatística de uma amostra esfoliada seja aceita metrológica e estatisticamente?"* ($\ge 200$ no MEV, $\ge 20$ no AFM cobrindo toda a faixa lateral, conforme NPL/VAMAS 2023; $\sim 100\text{–}150$ no AFM/TEM em Backes 2020.)
- *"Por que não posso simplesmente medir os mesmos flocos primeiro no MEV e depois no AFM para correlacionar diâmetro lateral e espessura um a um?"* (Deposição carbonácea pelo feixe de elétrons + exigência de substratos distintos: óxido nativo para MEV vs. $\text{SiO}_2\ 300\text{ nm}$ para AFM — NPL/VAMAS Sec. 2 e 4.1.)
- *"Se a amostra da UFCA vem de esfoliação eletroquímica, por que não basta analisar 3 ou 5 flocos como em esfoliação por fita?"* (Porque rotas eletroquímicas e líquidas produzem distribuições polidispersas de grafite residual, FLG, SLG e eventual oxidação — Backes II.5–II.6 e Kauling 2018.)

### 6. Tempo aproximado de leitura
- **60 min** (~25 min para o protocolo completo `NPL/VAMAS 2023`, ~30 min para as Seções `II.5–II.6` e `IX.1.2–IX.2.1` de `Backes et al., 2020`, ~5 min para fixação dos pontos de `Kauling et al., 2018`).

---

## Bloco 4 — Física e Limites da DRX em Carbono, Grafite e Materiais Relacionados

- **Referência 4.1 (Metadados e síntese secundária verificada — acesso fechado):** Li, Z. Q., Lu, C. J., Xia, Z. P., Zhou, Y., & Luo, Z. (2007). *X-ray diffraction patterns of graphite and turbostratic carbon.* *Carbon*, 45(8), 1686–1695. DOI: `10.1016/j.carbon.2007.03.038`
- **Referência 4.2 (Metadados e síntese pública verificada — correspondência de 1 p. fechada):** Holzwarth, U., & Gibson, N. (2011). *The Scherrer equation versus the 'Debye-Scherrer equation'.* *Nature Nanotechnology*, 6(9), 534. DOI: `10.1038/nnano.2011.145` (PubMed PMID `21873991`)

### 1. Por que estudar
Na dissertação, a DRX aparece como a técnica volumétrica mais acessível em qualquer laboratório de materiais, mas é justamente onde ocorrem os maiores equívocos conceituais em trabalhos de grafeno/GO/rGO: confundir ausência ou alargamento do pico `(002)` com prova de monocamada, usar o nome errado ("equação de Debye-Scherrer") ou aplicar a equação de Scherrer sem corrigir alargamento instrumental, microdeformação e desordem turboestrática.

### 2. Que seções merecem atenção
- **Atenção — Status de acesso fechado:** nenhum dos dois PDFs encontra-se acessível localmente em Open Access (`oa_status: closed`). A preparação de hoje apoia-se em metadados oficiais (Crossref/OpenAlex/PubMed) e sínteses científicas públicas verificadas.
- **O que buscar ao acessar os PDFs integrais (via CAPES/UFCA):**
  - Em **`Li, Lu & Xia (2007)` (pp. 1686–1695):** buscar a formulação pela **equação geral de Debye** e densidade numérica de distâncias interatômicas (NDID), bem como os gráficos de sensibilidade da posição de `(002)` e da largura à meia altura (`FWHM`) frente a: (i) rotações e translações aleatórias entre planos basais (empilhamento turboestrático), (ii) curvatura de camadas, (iii) flutuações do espaçamento interplanar $d_{002}$ e (iv) deslocamentos atômicos.
  - Em **`Holzwarth & Gibson (2011)` (p. 534):** conferir o argumento histórico de atribuição exclusiva a Paul Scherrer (1918), o significado do fator de forma $K$ e a delimitação entre **domínio de difração coerente** ($\tau$ / $L_c, L_a$) e **tamanho físico de partícula**, bem como as restrições de alargamento instrumental e microdeformação.

### 3. Que conceitos físicos precisam ser dominados
- **Lei de Bragg e periodicidade ao longo de $c$:** a reflexão `(002)` do grafite hexagonal ($d_{002} \approx 0{,}335\text{ nm}$, $2\theta \approx 26{,}5^\circ$ em radiação Cu $K\alpha$) exige empilhamento periódico coerente de múltiplas camadas ao longo do eixo $c$; uma monocamada isolada não possui periodicidade em $c$ para gerar reflexão `(002)`.
- **Desordem turboestrática:** empilhamento paralelo (ou quase paralelo) sem registro cristalográfico ABAB regular, com rotações/translações aleatórias entre camadas — expande $d_{002}$ ($> 0{,}34\text{ nm}$), desloca `(002)` para ângulos menores, assimetriza bandas `(hk)` bidimensionais e alarga fortemente os picos.
- **Equação de Scherrer ($\tau = K\lambda / (\beta\cos\theta)$):** mede o tamanho médio do **domínio cristalino coerente** perpendicular aos planos $(hkl)$ (ex.: $L_c$ pelo pico `(002)` e $L_a$ pelas reflexões no plano), e **não** o diâmetro lateral de flocos esfoliados nem a espessura exata de um floco individual; além disso, $\beta$ deve descontar o alargamento instrumental ($\beta_{\text{inst}}$) e sofre interferência de microdeformação (*microstrain*).
- **Nomenclatura correta:** escrever **Equação de Scherrer** (não *"equação de Debye-Scherrer"*).

### 4. Que resultado é relevante
- **`Li, Lu & Xia (2007)` (síntese pública verificada):** simulações pela equação geral de Debye demonstram que distorções turboestráticas (rotações/translações aleatórias, curvatura de planos, variação de $d_{002}$ e deslocamento atômico) alteram simultaneamente a posição angular $2\theta$ e a `FWHM` dos picos de difração, invalidando interpretações simplistas de tamanho aparente de cristalito via Scherrer em carbonos desordenados.
- **`Holzwarth & Gibson (2011)` (síntese pública verificada):** estabelecem que a fórmula de alargamento de picos foi derivada unicamente por Paul Scherrer (1918) — distinguindo-a do método/câmara de Debye–Scherrer — e reiteram que ela quantifica domínios coerentes após correção de alargamento instrumental e microdeformação.

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Se o pico `(002)` desaparecer ou ficar muito largo e fraco no difratograma de um pó produzido na UFCA, isso prova que obtivemos grafeno monocamada?"* (Não: pode refletir perda de coerência de empilhamento por desordem turboestrática, esfoliação incompleta muito desordenada, baixa massa cristalina ou curvatura/oxidação parcial.)
- *"Por que chamar a fórmula de Scherrer de 'equação de Debye-Scherrer' é impreciso, e quais os cuidados para aplicar Scherrer em $L_c$ de grafite/rGO?"*
- *"Um algoritmo para DRX pode prever diretamente 'número de camadas' de uma amostra de grafeno?"* (No máximo estima espessura média de empilhamento coerente $L_c/d_{002}$ em agregados cristalinos reempilhados ou residuais, jamais conta camadas de flocos dispersos individuais.)

### 6. Tempo aproximado de leitura
- **30 min** (leitura e fixação dos conceitos físicos e limitações em [`conceitos_fundamentais.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/conceitos_fundamentais.md) e no fichamento correspondente, reservando 20 min extras caso obtenha os dois PDFs via CAPES antes do seminário).

---

## Bloco 5 — Contraste Quantitativo em MEV de Grafeno

- **Referência 5.1 (Texto completo lido):** Zhou, Y. et al. (2016). *Quantitative secondary electron imaging for work function extraction at atomic level and layer identification of graphene.* *Scientific Reports*, 6, 21045. DOI: `10.1038/srep21045` | Texto extraído: [`Zhou_2016_Quantitative_SE_Imaging_Work_Function_Graphene.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Zhou_2016_Quantitative_SE_Imaging_Work_Function_Graphene.md) | Fichamento: [`03_zhou_2016_scirep_quantitative_se_imaging_work_function_graphene.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/03_zhou_2016_scirep_quantitative_se_imaging_work_function_graphene.md)
- **Referência 5.2 (Resumo, introdução pública e metadados verificados — acesso fechado):** Huang, L., & Gan, Y. (2024). *A review on SEM imaging of graphene layers.* *Micron*, 187, 103716. DOI: `10.1016/j.micron.2024.103716` | Fichamento existente: [`01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md)

### 1. Por que estudar
Responde à pergunta central sobre o **alcance físico do MEV**: se um floco de grafeno tem menos de $1\text{ nm}$ de espessura, por que aparece em imagens MEV, por que seu contraste pode **inverter** (ficar mais claro ou mais escuro que o substrato) e em que condições restritas é possível — ou impossível — usar o tom de cinza para estimar número de camadas?

### 2. Que seções merecem atenção
- **Em `Zhou et al. (2016)` (`Texto completo lido` — 8 pp.):**
  - *Páginas 1–3 e Eq. (1)* + **Figura 1**: comparação óptica vs. MEV vs. HIM em metais e $\text{SiO}_2(285\text{ nm})/\text{Si}$; inversão de contraste de `0,5 keV` ($+9\%$) para `1,5 keV` ($+1\%$) e `5 keV` ($-20\%$); efeito de carregamento abaixo de `1 keV`.
  - *Páginas 3–4* + **Figura 2**: resolução de borda de **`~10 nm`** (contra `~680 nm` na microscopia óptica) e separação gaussiana inter-flocos e inter-instrumentos (`Zeiss Supra` vs. `FEI Strata DB235`).
  - *Páginas 4–6, Eqs. (2)–(4)* + **Figuras 3–4**: modelo de atenuação exponencial (IMFP $\lambda \approx 5{,}7\text{ nm}$), saturação em $\sim 14$ camadas e extração da função trabalho $\Phi(1\text{–}4\text{L})$ via espectro de Chung & Everhart.
  - *Methods* (p. 7): parâmetros exatos (`InLens`, abertura `10 µm`, `5–20 pA`, `WD = 4 mm`, `2500×`, dose controlada).
- **Em `Huang & Gan (2024)` (`Resumo/introdução pública e metadados verificados` — corpo completo fechado):**
  - Ao obter o PDF via CAPES/UFCA, focar nas Seções de **comparação quantitativa entre detector lateral Everhart-Thornley (E-T) e detector em coluna (*in-lens*)**, **papel da distância de trabalho (`WD`) elevada** e **contraste de canalização eletrônica (ECC) / redução de óxido interfacial em folhas de Cu policristalino**.

### 3. Que conceitos físicos precisam ser dominados
- **Elétrons Secundários (SE1, SE2, SE3) e Retroespalhados (BSE):** contraste depende tanto dos SEs emitidos diretamente pelo grafeno (excitados pelo feixe primário e pelos BSEs do substrato) quanto dos SEs do substrato que atravessam o grafeno com atenuação exponencial $\exp(-N d/\lambda)$ ($\lambda \approx 5{,}7\text{ nm}$, $d = 0{,}335\text{ nm}$).
- **Função trabalho ($\Phi$):** barreira de potencial que os SEs de baixa energia precisam vencer para escapar ao vácuo; varia de $\sim 4{,}26\text{ eV}$ (1L) até saturar em $\sim 4{,}60\text{ eV}$ ($N \ge 4$).
- **Inversão de contraste com $V_{\text{acc}}$ e papel do detector:** detector *InLens* a baixa tensão e curta `WD` filtra BSEs/SE3 da câmara e gera contraste reprodutível, mas a tensão padrão ($15\text{–}20\text{ kV}$) reduz drasticamente o contraste de 1L; o ajuste combinado `(V_acc, WD)` reabilita até o detector `E-T` convencional (Huang & Gan, 2024).
- **Carregamento elétrico e ECC:** abaixo de $1\text{ keV}$ em $\text{SiO}_2$ espesso ocorre *charging*; em metais policristalinos (Cu), a orientação dos grãos gera ECC de fundo competindo com o sinal do grafeno.

### 4. Que resultado é relevante
- **`Zhou et al. (2016)`:** sob protocolo estrito (`5 keV`, detector *InLens*, `WD = 4 mm`, `10 µm`, `5–20 pA`) em `>100` flocos sobre $\text{SiO}_2(285\text{ nm})/\text{Si}$ (validados por OM e Raman), o contraste absoluto apresentou distribuições gaussianas sem sobreposição de **$(18 \pm 1)\%$ para monocamada (`1L`)** e **$(26 \pm 2)\%$ para bicamada (`2L`)**, reproduzidas em um segundo MEV diferente; identificou até `10` camadas (saturando próximo a `14L` em $\sim -0{,}60$); e extraiu $\Phi(1) = 4{,}26 \pm 0{,}05\text{ eV}$ até $\Phi(4) = 4{,}60 \pm 0{,}07\text{ eV}$ com precisão relativa $<10\text{ meV}$.
- **`Huang & Gan (2024)` (preview/introdução verificados):** mostram que condições convencionais de MEV (`15–20 kV`, `WD = 8–12 mm`) falham para grafeno fino, mas aumentar `WD` (com ou sem baixa `V_acc`) melhora o contraste mesmo em detectores **E-T comuns** e neutraliza o ruído de fundo por ECC em Cu policristalino.

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Por que um software de MEV não pode simplesmente medir a intensidade de cinza de qualquer micrografia e dizer quantas camadas existem?"* (Porque a `1,5 keV` a monocamada quase some [$+1\%$], a `0,5 keV` fica clara [$+9\%$], a `5 keV` fica escura [$-18\%$], e o resultado muda totalmente com detector `E-T` vs. `InLens`, `WD`, carregamento, contaminação e substrato.)
- *"Se meu laboratório tiver apenas um MEV com detector E-T comum (sem InLens) e amostras em substrato condutor ou silício nativo, o MEV ainda serve para grafeno?"* (Sim! Serve de forma padrão e normalizada para **dimensões laterais e morfologia** per VAMAS 2023, e o contraste pode ser otimizado ajustando `V_acc` baixa e `WD` conforme Huang & Gan 2024.)

### 6. Tempo aproximado de leitura
- **45 min** (~35 min em `Zhou et al., 2016` com foco nas Figs. 1–3 e Methods; ~10 min no fichamento verificado de `Huang & Gan, 2024`).

---

## Bloco 6 — Pipelines Automatizados de Segmentação em Materiais 2D

- **Referência 6.1 (Texto completo lido):** Masubuchi, S. et al. (2020). *Deep-learning-based image segmentation integrated with optical microscopy for automatically searching for two-dimensional materials.* *npj 2D Materials and Applications*, 4, 3. DOI: `10.1038/s41699-020-0137-z` | Texto extraído: [`Masubuchi_2020_Deep_Learning_Image_Segmentation_2D_Materials.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Masubuchi_2020_Deep_Learning_Image_Segmentation_2D_Materials.md)
- **Referência 6.2 (Texto completo lido):** Saito, Y. et al. (2019). *Deep-learning-based quality filtering of mechanically exfoliated 2D crystals.* *npj Computational Materials*, 5, 124. DOI: `10.1038/s41524-019-0262-4` | Texto extraído: [`Saito_2019_Deep_Learning_Quality_Filtering_2D_Crystals.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Saito_2019_Deep_Learning_Quality_Filtering_2D_Crystals.md)

### 1. Por que estudar
São os dois trabalhos de referência direta em **visão computacional aplicada especificamente a materiais 2D (incluindo grafeno)** que demonstram por que métodos clássicos baseados em regras quebram diante de mudanças de iluminação/instrumento e comparam as duas famílias centrais de segmentação profunda: **segmentação de instâncias (*Mask R-CNN*)** vs. **segmentação semântica (*U-Net*)** com poucos dados anotados. Nota fundamental de domínio: ambos operam sobre **microscopia óptica (OM)** em $\text{SiO}_2/\text{Si}$ (onde o contraste interferencial de cor auxilia a triagem inicial), servindo de paradigma arquitetural — porém não substituindo a validação necessária em **MEV** e **AFM**.

### 2. Que seções merecem atenção
- **Em `Masubuchi et al. (2020)` (`Texto completo lido` — 9 pp.):**
  - *Introduction* & *Results — System architectures* (pp. 1–4, **Figs. 1–2**): fragilidade do algoritmo baseado em regras frente à variação de intensidade de luz ($I = 220 \to 180$, Fig. 2d–f) vs. estabilidade do Mask R-CNN ($I = 220 \to 90$, Fig. 2a–c).
  - *Model training*, *Transfer learning* & *Generalization ability* (pp. 4–8, **Figs. 3–5**): pré-treinamento em 2 etapas (`MS-COCO` $\rightarrow$ mistura de 4 materiais 2D $\rightarrow$ ajuste fino por material), *data augmentation online*, fluxo semiautomático de anotação (~80 imagens iniciais -> correção em 20–30 s/imagem) e teste em **três microscópios inéditos** (Fig. 5).
- **Em `Saito et al. (2019)` (`Texto completo lido` — 6 pp.):**
  - *Results & Table 1* (pp. 2–4, **Figs. 1–3**): treinamento com apenas **24 imagens de $\text{MoS}_2$** e **30 imagens de grafeno/grafite** aumentadas para 960; impacto da **entropia cruzada ponderada** (*median frequency balancing*) e da perda de desempenho quando se converte para escala de cinza (`0.789` $\to$ `0.723` / `0.560`!).
  - *Discussion & Methods* (pp. 4–5, **Fig. 4**): comparação contra `BoVW` clássico, CNN pixel-a-pixel e **12 humanos não especialistas** (`0.67 ± 0.11`), além do erro conhecido de confundir fundo com monocamada quando há poucos dados.

### 3. Que conceitos físicos precisam ser dominados
- **Contraste interferencial em $\text{SiO}_2\ (\sim 290\text{–}300\text{ nm})/\text{Si}$:** a identificação de `mono` (1L) vs. `few` (2–10L) vs. `thick` nesses artigos explora cor e contraste óptico específicos dessa espessura de óxido; quando `Saito et al.` removeram a cor (escala de cinza), o escore de validação cruzada caiu significativamente — alerta direto para imagens **MEV e AFM**, que são monocromáticas!
- **U-Net vs. Mask R-CNN:** U-Net classifica pixel a pixel preservando bordas finas via *skip connections* com poucos exemplos; Mask R-CNN detecta caixas (RPN + ROI Align) e gera máscaras individuais por objeto, separando instâncias e tolerando resíduos (fita adesiva, dobras).
- **Desbalanceamento extremo de classes:** monocamadas ocupam fração mínima dos pixels; sem função de perda ponderada (*weighted cross-entropy*), a rede tende a prever tudo como fundo/"outros".

### 4. Que resultado é relevante
- **`Masubuchi et al. (2020)`:** com 2.102 imagens (7.153 objetos, sendo 862 imagens / 4.805 objetos de grafeno), Mask R-CNN inferiu em **200 ms** por imagem `1024×1024 px²`, varreu $1 \times 1\text{ cm}^2$ em 1 hora, obteve **precisão $\sim 0{,}95$ e revocação $\sim 0{,}97$** no nível de imagem para grafeno (`mAP@IoU50% = 0,49`) e generalizou sem retreinamento para **3 microscópios ópticos distintos** (Fig. 5) e materiais não vistos ($\text{WSe}_2$, $\text{MoSe}_2$).
- **`Saito et al. (2019)`:** partindo de apenas **24 imagens originais ($\text{MoS}_2$) e 30 imagens (grafeno)** confirmadas por AFM/contraste óptico, U-Net com entropia cruzada ponderada e aumento de contraste atingiu escore de validação cruzada de **`0,789`** e acurácia de teste **`0,733`** (70–80% em $\text{MoS}_2$ e grafeno), igualando ou superando humanos não especialistas (`0,67 ± 0,11`) e superando *Bag of Visual Words* e CNN pixel-a-pixel.

### 5. Que perguntas de professores o artigo ajuda a responder
- *"O que evita que o nosso projeto 'reinvente a roda' em relação ao que Masubuchi (2020) e Saito (2019) já fizeram?"* (Eles resolveram **triagem óptica** em substratos $\text{SiO}_2/\text{Si}$ de esfoliação mecânica; ainda há lacuna clara para **MEV e AFM** com calibração metrológica `ISO/VAMAS`, onde não há informação de cor RGB e as amostras eletroquímicas são polidispersas e sobrepostas.)
- *"Por que algoritmos simples de limiarização (como Otsu) não bastam?"* (Masubuchi Fig. 2 mostra que leve queda de iluminação quebra o detector baseado em regras, exigindo recalibração manual de $\ge 30\text{ min}$ por amostra.)
- *"Como anotar rapidamente imagens sem gastar meses?"* (Fluxo *human-in-the-loop* de Masubuchi: treinar em ~80 imagens e corrigir predições em 20–30 s/imagem.)

### 6. Tempo aproximado de leitura
- **45 min** (~25 min para `Masubuchi et al., 2020` e ~20 min para `Saito et al., 2019`).

---

## Bloco 7 — Aprendizado de Máquina/Profundo em DRX e Limitação *Sim-to-Real*

- **Referência 7.1 (Texto completo lido):** Oviedo, F. et al. (2019). *Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks.* *npj Computational Materials*, 5, 60. DOI: `10.1038/s41524-019-0196-x` | Texto extraído: [`Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.md)
- **Referência 7.2 (Texto completo lido via manuscrito arXiv `2211.08591v1` correspondente):** Greasley, J., & Hosein, P. (2023). *Exploring supervised machine learning for multi-phase identification and quantification from powder X-ray diffraction spectra.* *Journal of Materials Science*, 58(12), 5334–5348. DOI: `10.1007/s10853-023-08343-4` | Texto extraído: [`Greasley_Hosein_2023_Supervised_ML_Powder_XRD.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Greasley_Hosein_2023_Supervised_ML_Powder_XRD.md)

### 1. Por que estudar
Estes dois estudos revisados por pares enfrentam exatamente o dilema computacional da nossa dissertação em **DRX**: no laboratório real do PPGCEM não existem milhões de difratogramas experimentais rotulados, e treinar modelos apenas em padrões teóricos simulados (ICSD/COD) sofre severa queda de desempenho no mundo real (**lacuna *simulation-to-real***). Juntos, `Oviedo et al. (2019)` e `Greasley & Hosein (2023)` provam tanto **como fazer aumento de dados fisicamente informado e interpretável (CAMs)** quanto **quando modelos clássicos leves (SVM, Naive Bayes, k-NN) igualam ou superam redes neurais** em bancos pequenos!

### 2. Que seções merecem atenção
- **Em `Oviedo et al. (2019)` (`Texto completo lido` — 9 pp.):**
  - *Data augmentation based on domain knowledge* (pp. 3–4, **Fig. 2**, Eqs. 1–3): as 3 perturbações físicas (escalamento periódico de picos, eliminação periódica por textura/orientação preferencial e deslocamento em $2\theta$ por deformação/composição).
  - *Classification results and a-CNN* & **Table 1** (pp. 4–6, **Fig. 3–4**): comparação direta dos **Casos 1, 2 e 3** (evidenciando a queda do Caso 1 simulado $\rightarrow$ Caso 2 *sim-to-real* $\rightarrow$ recuperação no Caso 3 híbrido) e tolerância ao passo angular até $0{,}16^\circ\ 2\theta$.
  - *Interpretability using CAMs* (pp. 6–8, **Fig. 5**): diagnóstico de erros por Mapas de Ativação de Classe médios (mistura de fases, $<5$ amostras em classes raras, picos ausentes).
- **Em `Greasley & Hosein (2023)` (`Texto completo lido` — 12 pp. do manuscrito correspondente `2211.08591v1`):**
  - *Experimental Methods* (pp. 3–5, **Fig. 1**): banco experimental pequeno ($N = 52$ classificação / $N = 46$ regressão com Rietveld MAUD) + simulação via `pymatgen`/COD e `GSAS-II` para picos largos nanocristalinos.
  - *Results & Analysis* (**Tables 2, 3 e 4**, **Figs. 2–3**): comparação sistemática das **Instâncias [1] Sim-only, [2] Exp-only, [3] Sim-treino / Exp-teste e [4] Sim+Exp-treino / Exp-teste** entre `k-NN`, `SVM`, `DTr`, `GNB/MNB/CNB`, `RF`, `ExTr` e `ANN`.
  - *Discussion & Conclusion* (pp. 8–10): por que **SVM, CNB e k-NN** competem com ou superam a ANN em bancos pequenos com fração do tempo de treino (`0,03 s` vs. `67 s`).

### 3. Que conceitos físicos precisam ser dominados
- **Lacuna *Simulation-to-Real* (*sim-to-real gap*):** difratogramas teóricos ideais de pó assumem grãos aleatoriamente orientados, sem deslocamento de altura de porta-amostra (*zero offset*), sem microdeformação nem textura preferencial e sem fundo amorfo/instrumental; modelos treinados só em simulações degradam sobre dados reais.
- **Textura / orientação preferencial em materiais laminares/filmes:** essencial em grafite/GO/rGO depositados em porta-amostra plano, onde reflexões `(00l)` ficam desproporcionalmente intensificadas em relação às `(hk0)`.
- **Métricas rigorosas para classificação multirrótulo e regressão de fases:** `ELA` (*Exact-Label Accuracy*), `MPA` (*Majority Phase Accuracy*), F1 micro vs. F1 macro (em classes desbalanceadas), `MAE`, similaridade de cosseno (`CS`) e imposição de restrições físicas de não negatividade e soma unitária ($\sum \hat{\alpha}_j = 1$) nas frações de fase.
- **Interpretabilidade via *Class Activation Maps* (CAMs):** permite ao pesquisador auditar *quais regiões de $2\theta$* determinaram a decisão da CNN 1D.

### 4. Que resultado é relevante
- **`Oviedo et al. (2019)`:** em 115 padrões experimentais + 164 simulados ICSD, o aumento de dados fisicamente informado elevou a acurácia da `a-CNN` em $+23\%$ (dimensionalidade) e $+19\%$ (grupo espacial) em relação ao treino sem aumento, superando aumento apenas com ruído em $>12\%$ absolutos. Na **Tabela 1**: no Caso 1 (sim$\rightarrow$sim) a `a-CNN` atingiu `99,1% / 99,1%`; no **Caso 2 (sim$\rightarrow$exp)** caiu para `83,7% / 80,2%` (enquanto `k-NN` despencou para `21,2%` e `Naive Bayes` para `25,5%` em grupo espacial!); e no **Caso 3 (sim+exp$\rightarrow$exp)** recuperou **`92,9%` e `89,3%`** (micro F1 `0,929 / 0,893`), com passos até $0{,}16^\circ\ 2\theta$ reduzindo em 75% o tempo de aquisição (`<5,5 min`).
- **`Greasley & Hosein (2023)`:** usando apenas $N = 52$ difratogramas experimentais reais (e $N = 46$ para regressão), na **Instância [2] (só experimental)** o classificador **Complement Naive Bayes (`CNB`)** obteve **`88,8%`** de acurácia total (`F1 avg = 0,812`, `MPA = 96,4%`) treinando em **`0,03 s`**, empatando ou superando a `ANN` (`88,3%`, `F1 = 0,810`, `67 s`) e `SVM` (`87,3%`, `MPA = 98,2%`). Na **Instância [3] (só simulado $\rightarrow$ experimental)**, **`SVM` (`87,9%`, `MPA = 100%`) e `CNB` (`87,6%`) superaram a `ANN` (`87,1%`)**, e na regressão de frações de fase o **`k-NN` (`\rho = 0,8462`, `MAE = 0,0479`, Instância [4])** obteve o melhor desempenho global!

### 5. Que perguntas de professores o artigo ajuda a responder
- *"Se você tiver poucos difratogramas reais no PPGCEM, Deep Learning é mesmo a melhor escolha ou é um exagero?"* (Greasley & Hosein 2023 provam empiricamente que `SVM`, `CNB` e `k-NN` são competitivos ou superiores a redes neurais em $N \sim 50$ amostras, além de serem instantâneos e interpretáveis; já se usar CNN 1D, Oviedo et al. 2019 mostram que é obrigatório usar *data augmentation* físico e auditar com CAMs.)
- *"Posso baixar padrões CIF de grafite/GO, simular mil difratogramas e rodar direto nas amostras do laboratório sem calibrar dados reais?"* (Não: Caso 2 de Oviedo e Instância 3 de Greasley demonstram a queda real do *sim-to-real gap*, que exige inclusão de dados experimentais reais e modelagem de alargamento nanocristalino/deslocamento/textura.)
- *"Por que descartaram `Wang et al. (2026)` da lista principal?"* (Porque foi oficialmente retirado pelos autores no arXiv antes de revisão por pares; a literatura revisada por pares já sustenta solidamente toda a discussão.)

### 6. Tempo aproximado de leitura
- **50 min** (~25 min em `Oviedo et al., 2019` focando Figs. 1–2, Tabela 1 e Fig. 5; ~25 min em `Greasley & Hosein, 2023` focando Métodos e Tabelas 2–4).
