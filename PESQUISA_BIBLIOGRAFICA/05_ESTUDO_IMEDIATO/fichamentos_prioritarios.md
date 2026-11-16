# Fichamentos Prioritários — Os 7 Blocos Essenciais (Missão 02 · PPGCEM/UFCA)

Este documento reúne o resumo científico detalhado e verificável dos **7 blocos essenciais** selecionados em [`artigos_essenciais.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/artigos_essenciais.md) para estudo imediato antes do Seminário I (`17/11/2026`).

> [!IMPORTANT]
> **Padrão de Rastreabilidade e Honestidade Científica (Seções 7 e 8 do `PROMPT_MESTRE.md`):**
> - Cada referência declara explicitamente seu **Status de Leitura** (`Texto completo lido` vs. `Resumo e metadados verificados`).
> - Nos trabalhos de acesso fechado (`Shearer et al., 2016`; `Kauling et al., 2018`; `Li, Lu & Xia, 2007`; `Holzwarth & Gibson, 2011`; `Huang & Gan, 2024`), são relatados **exclusivamente** os dados constantes nos resumos oficiais, pré-visualizações públicas e metadados verificados em [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json), sem invenção de páginas, equações ou figuras não inspecionadas.
> - Em cada bloco, fatos **extraídos dos artigos** são separados da **análise crítica para a dissertação**.

---

## Bloco 1 — AFM e Anomalia de Espessura em Grafeno

### 1.1 Nemes-Incze, Osváth, Kamarás & Biró (2008) — *Carbon*
- **Status de leitura:** **Texto completo lido** (cópia autorizada `arXiv:0812.0690`, 16 pp., 7 figuras, em [`Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.md)).
- **Identificação bibliográfica:** Nemes-Incze, P., Osváth, Z., Kamarás, K., & Biró, L. P. (2008). *Anomalies in thickness measurements of graphene and few layer graphite crystals by tapping mode atomic force microscopy.* *Carbon*, 46(11), 1435–1442. DOI: `10.1016/j.carbon.2008.06.022`.

#### Problema investigado *(extraído do artigo)*
Embora o espaçamento interplanar do grafite seja $\sim 0{,}335\text{ nm}$ e a microscopia de força atômica em modo *tapping* (TAFM) seja amplamente usada para estimar espessura de grafeno sobre $\text{SiO}_2/\text{Si}$, a literatura relatava valores discrepantes entre **$0{,}35\text{ nm}$ e $1{,}6\text{ nm}$** para monocamadas sobre $\text{SiO}_2$, incluindo saltos aleatórios de altura durante uma mesma varredura. O estudo investiga o mecanismo físico desse erro instrumental em função da amplitude livre ($A_0$) e do *setpoint* do cantilever.

#### Fundamentação e Metodologia *(extraídas do artigo)*
- **Amostras e referência:** grafite HOPG (`SPI-1`) esfoliado mecanicamente sobre *wafers* de Si com $\text{SiO}_2$ de $300\text{ nm}$; seleção óptica e validação independente de $1, 2, 3, 5, 10$ camadas por **espectroscopia Raman ($488\text{ nm}$, laser $\text{Ar}^+$, *spot* $\sim 2\ \mu\text{m}$)** pela assinatura da banda $2D$ (`~2700 cm⁻¹`).
- **Instrumentação AFM:** *Multimode Nanoscope IIIa* (Veeco) em ar ambiente, modos TAFM e contato (CAFM), pontas de silício `Nanosensors PPP-NCHR` ($R < 10\text{ nm}$, $k \approx 42\text{ N/m}$, $f_0 \sim 300\text{ kHz}$, acionamento $5\%$ abaixo de $f_0$).
- **Ensaios:** aquisição de imagens variando $A_0$ ($16\text{–}30\text{ nm}$) em *setpoint* fixo ($15\text{ nm}$) e levantamento de **curvas amplitude–distância (AD)** sobre o substrato de $\text{SiO}_2$ e sobre o floco FLG, reduzindo a amplitude até $\sim 10\%$ de $A_0$.

#### Resultados observados *(extraídos do artigo)*
1. **Salto abrupto de espessura aparente (Figs. 1 e 4):** medindo cristais FLG (`C1` e `C2`) sobre $\text{SiO}_2$, ao aumentar $A_0$ mantendo *setpoint* de $15\text{ nm}$, a espessura aparente de um cristal FLG caiu bruscamente de **$4{,}5\text{ nm}$ para $2{,}25\text{–}2{,}3\text{ nm}$ ($\sim 7$ camadas)** em $A_0 \approx 25\text{–}26\text{ nm}$ (e exibiu salto prévio em $\sim 21\text{ nm}$ correspondente à transição no óxido). Já o degrau **grafite sobre grafite** (`C2` sobre `C1`, triângulos verdes da Fig. 1c) permaneceu **constante** ao longo de toda a faixa de $A_0$.
2. **Biestabilidade nas curvas AD (Figs. 2a–c e 3):** em $A_0 = 25{,}8\text{ nm}$, a curva AD sobre FLG exibe um salto descontínuo em $16\text{ nm}$ de amplitude separando **dois deslocamentos piezoelétricos estáveis distantes de $\sim 1\text{ nm}$**: o **regime atrativo líquido** (forças de longo alcance dominadas por **forças capilares histeréticas** da película de água ambiente) e o **regime repulsivo líquido** (contato mecânico intermitente). Quando o *setpoint* coincide com o ponto de instabilidade, o *feedback* comuta aleatoriamente entre os dois ramos, gerando estrias/saltos de $\sim 1\text{ nm}$ entre linhas de varredura (Figs. 2b–c).
3. **Validação cruzada com Raman (Figs. 5–6):** monocamadas confirmadas pelo pico $2D$ Raman mediram **$\sim 1\text{ nm}$** no regime atrativo (baixa $A_0$) e concordaram com a espessura esperada apenas quando $A_0$ e *setpoint* colocavam **tanto o óxido quanto o grafeno no regime repulsivo** (alta $A_0$).
4. **Modo Contato vs. TAFM (Fig. 7):** no CAFM a espessura ($\sim 2\text{ nm}$, $6$ camadas) não variou com a força normal de deflexão, mas apresentou diferença de **$\sim 0{,}2\text{ nm}$** entre varredura esquerda$\rightarrow$direita e direita$\rightarrow$esquerda devido à diferença de atrito lateral entre FLG e $\text{SiO}_2$ (efeito ausente em TAFM).

#### Limitações e Evidências
- **Limitações reconhecidas:** os autores observam que o deslocamento exato do ponto crítico entre óxido e grafeno depende fortemente da umidade relativa (forças capilares) e de gradientes de molhabilidade, e que o mecanismo detalhado do deslocamento do ponto de instabilidade ainda demandava simulação/investigação adicional; recomendam explicitamente cruzar AFM com Raman/outras técnicas.
- **Evidências:** `Abstract` (p. 1), `Introduction` (pp. 1–2), `Experimental` (pp. 2–3), `Results and Discussion` (pp. 3–6), `Conclusions` (pp. 6–7), `Figs. 1–7` (pp. 8–13).

---

### 1.2 Shearer, Slattery, Stapleton, Shapter & Gibson (2016) — *Nanotechnology*
- **Status de leitura:** **Resumo e metadados verificados** (periódico fechado / *bronze OA* sem extração local em [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json); PDF completo pendente via CAPES/UFCA).
- **Identificação bibliográfica:** Shearer, C. J., Slattery, A. D., Stapleton, A. J., Shapter, J. G., & Gibson, C. T. (2016). *Accurate thickness measurement of graphene.* *Nanotechnology*, 27(12), 125704. DOI: `10.1088/0957-4484/27/12/125704`.

#### Síntese fiel ao resumo verificado
- **Problema:** A literatura reporta variação de **$0{,}4\text{ a }1{,}7\text{ nm}$** para espessura de monocamada de grafeno por AFM, atribuída a interações ponta–superfície, parâmetros de *feedback* e química superficial.
- **Abordagem e resultado:** Utilizando pontas padrão e pontas modificadas com nanotubos de carbono (CNT) no modo **`PeakForce tapping`**, os autores estabelecem um protocolo que reduz o erro de medição da primeira camada de **$0{,}1\text{–}1{,}3\text{ nm}$ para $0{,}1\text{–}0{,}3\text{ nm}$**, demonstrando que a **camada de adsorvato entre grafeno e substrato** e a **força/pressão exercida pela ponta** são fatores determinantes para acurácia em materiais 2D.

#### Contribuição integrada do Bloco 1 para a dissertação *(Análise crítica)*
Prova que nenhum módulo computacional de AFM pode converter altura em nanômetros em número de camadas por regra fixa ($N = h / 0{,}335\text{ nm}$). Uma ferramenta útil deve: (i) registrar metadados do modo de operação (*tapping* vs. *PeakForce*, *setpoint*, $A_0$, ponta), (ii) detectar degraus internos *grafeno–sobre–grafeno* quando disponíveis (onde o *offset* se cancela), e (iii) exibir a **incerteza física ($0{,}1\text{–}0{,}3\text{ nm}$ no melhor caso; até $\sim 1\text{ nm}$ sem controle de regime)** recomendando validação por Raman.

---

## Bloco 2 — Visão Computacional e ML em Microestruturas

### 2.1 Holm, Cohn, Gao, Kitahara, Matson, Lei & Yarasi (2020) — *Metallurgical and Materials Transactions A*
- **Status de leitura:** **Texto completo lido** (15 pp., 9 figuras, 128 referências em [`Holm_2020_Overview_CV_ML_Microstructural_Characterization.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Holm_2020_Overview_CV_ML_Microstructural_Characterization.md); tabela suplementar `Table SI` com códigos não compõe o arquivo principal).
- **Identificação bibliográfica:** Holm, E. A. et al. (2020). *Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis.* *Metallurgical and Materials Transactions A*, 51(12), 5985–5999. DOI: **`10.1007/s11661-020-06008-4`** *(DOI corrigido na auditoria; o identificador `10.1007/s11837-020-04347-6` herdado no histórico pertencia a outro artigo)*.

#### Problema investigado *(extraído do artigo)*
A caracterização microestrutural quantitativa esbarra em dois gargalos históricos (Sec. I, pp. 5985–5986): **(1) *o que medir*** (selecionar métricas relevantes dentre morfologias complexas) e **(2) *como medir*** (segmentar contornos difusos ou *"missing boundaries"* sem subjetividade humana nem baixa reprodutibilidade). A revisão avalia como Visão Computacional (CV) e Aprendizado de Máquina (ML) convertem micrografias em vetores de atributos para automatizar e ampliar a análise microestrutural.

#### Fundamentação e Metodologia *(extraídas do artigo)*
- **Codificação numérica (Sec. II.A, Fig. 2):** substituição de descritores manuais por ativação de camadas convolucionais via ***transfer learning*** (ex.: `VGG16` pré-treinada no `ImageNet`, truncada antes das camadas densas, opcionalmente reduzida com `PCA`/`VLAD`) e vetores de pixel em **hipercolunas** (`PixelNet`, empilhando ativações de todas as camadas na posição espacial do pixel). Camadas rasas capturam detalhes locais; camadas profundas capturam texturas multiescala — mas CNNs são **invariantes à translação e NÃO à rotação nem à escala**, exigindo padronização de magnificação ou aumento de dados.
- **Algoritmos ML (Sec. II.B):** comparação entre **SVM** (bom em alta dimensão se separável por hiperplanos), **Random Forest** (interpretável, menos adequado a representações brutas complexas), **ANN** (flexível, porém caixa-preta) e métodos não supervisionados (**k-means** e **t-SNE** — ressaltando que t-SNE exige recálculo global e **não classifica novos dados diretamente**).
- **Boas práticas de dados (Sec. II.C):** micrografias são ricas em informação (uma micrografia pode conter ~100 precipitados, permitindo resultados úteis com $<10\text{–}30$ imagens originais); recomendam **campos de visão redundantes e não sobrepostos**, padronização de aquisição, *data augmentation* (que facilita o treino, mas **não cria nova informação física**) e **inclusão de metadados multimodais**.

#### Resultados observados *(extraídos do artigo — Taxonomia em 4 níveis, Sec. III e Figs. 3–8)*
1. **Classificação e regressão sem segmentação (Sec. III.A, Figs. 4–5):**
   - SVM linear em 961 micrografias de aço UHCS atingiu **$99 \pm 1\%$** de acurácia;
   - CNN com camada de regressão treinada em `15.213` microestruturas sintéticas `SPPARKS` estimou tamanho de grão com erro padrão de **$2{,}3\%$** (e **$3{,}9\%$** com fração `0,4` de contornos apagados, dentro da precisão ASTM E112 de $\pm 0{,}5$ unidades);
   - CNN pré-treinada em `2.543` patches MEV de inclusões em aço (testada em `509` inéditas) alcançou **$76\%$** de acurácia na identificação composicional apenas por contraste/morfologia MEV (chance aleatória: $20\%$).
2. **Segmentação semântica (Sec. III.B, Figs. 6–7):**
   - `PixelNet` obteve **$93\%$** de acurácia em UHCS (20 imagens treino / 4 teste) e **$99{,}6\%$** em fatias tomográficas Al–Zn (30 treino / 10 teste), ignorando defeitos de polimento e *beam spot*;
   - Em 17 imagens MEV (ECCI) de superliga de Ni (15 treino / 2 teste), `U-Net` sozinha não diferenciou linhas de discordância de contornos $\gamma\text{–}\gamma'$ em anotações de 1 pixel, exigindo fusão com uma segunda CNN treinada para máscara regional de deformação (Fig. 7).
3. **Detecção de objetos e segmentação de instâncias (Sec. III.C–D, Fig. 8):**
   - Em 5 imagens MEV densamente anotadas de pós metálicos (3 treino / 2 teste), *Faster R-CNN* obteve **revocação $80\%$** e **precisão $94\%$**; *Mask R-CNN* obteve **precisão $97{,}5\%$ e revocação $95{,}4\%$** nas partículas principais (e $69{,}2\% / 54{,}5\%$ em partículas satélites ambíguas).
4. **Métricas visuais avançadas (Sec. IV.A, Fig. 9):** PCA + `k-means` ($k=8$) + `t-SNE` em ~1.100 partículas de `Inconel-718` produziu "impressões digitais" quantitativas da morfologia do pó.

#### Limitações e Contribuição para a dissertação
- **Limitações reconhecidas (Sec. II.C, IV.B–C):** dependência do par *(camada da CNN, escala da microestrutura)* por tentativa e erro; dificuldade de inferir estrutura 3D a partir de imagens 2D (estereologia); escassez de bancos com histórico completo processamento–estrutura–propriedade (PSP); e desafio aberto da interpretabilidade em modelos caixa-preta.
- **Contribuição *(Análise crítica)*:** Guia metodológico direto para o software do PPGCEM: define por que **segmentação semântica não separa flocos em contato** (exigindo instância/pós-processamento), justifica coleta sem sobreposição e registro de metadados de magnificação, e alerta que redes profundas exigem validação sem vazamento quando aplicadas a bancos pequenos.

---

## Bloco 3 — Produção Heterogênea e Padronização de Grafeno/GRMs

### 3.1 Backes et al. (2020) — *2D Materials*
- **Status de leitura:** **Texto completo lido nas seções-alvo** (monografia de 283 pp. em [`Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md); inspecionadas Seções `II.1–II.6` [precursores, LPE, GO/rGO, esfoliação eletroquímica], `IX.1.2` [AFM], `IX.1.3` [TEM], `IX.2.1` [Raman], `IX.2.3` [XPS] e buscas direcionadas para DRX/MEV).
- **Identificação bibliográfica:** Backes, C. et al. (2020). *Production and processing of graphene and related materials.* *2D Materials*, 7(2), 022001. DOI: `10.1088/2053-1583/ab1e0a`.

#### Problema investigado e Fundamentação *(extraídas do artigo)*
O artigo oferece um compêndio prático ("*hands-on*") para reproduzir rotas de produção, processamento e caracterização de grafeno e materiais relacionados (GRMs), atacando o principal gargalo industrial dos métodos *top-down*: a **extrema polidispersidade em tamanho lateral e espessura ($N$)** e a variabilidade química entre rotas de síntese (esfoliação em fase líquida [LPE], oxidação/redução [GO/rGO] e **esfoliação eletroquímica [EE]**).

#### Resultados e Protocolos Observados *(extraídos do artigo)*
1. **Esfoliação Eletroquímica e rotas *top-down* (Seções II.2–II.6, pp. 25–46, Figs. II.20–II.21):**
   - **LPE padrão:** gera flocos de dezenas de nm a dezenas de $\mu\text{m}$ e $N$ de $1$ a centenas de camadas, com rendimento inicial de monocamada $Y_M < 1\%$ sem centrifugação em cascata (p. 25).
   - **EE aquosa anódica:** em $\text{H}_2\text{SO}_4$ $0{,}1\text{ M}$ ($10\text{ V}$) atinge $\sim 80\%$ de 1–3LG ($C/O = 12{,}3$); substituindo por sais de sulfato atinge $>85\%$ de 1–3LG (até $40\ \mu\text{m}$, $C/O \sim 17{,}2$); com *scavenger* radicalar `TEMPO` alcança $C/O \sim 25{,}3$ ($5\text{–}10\ \mu\text{m}$, mobilidade até $405\ \text{cm}^2\,\text{V}^{-1}\,\text{s}^{-1}$); em $\text{H}_2\text{SO}_4$ concentrado/diluído em duas etapas produz GO ($C/O < 2$, $95\%$ 1L) (p. 42). O trade-off central (Sec. II.6, Fig. II.21) contrapõe velocidade/rendimento contra preservação estrutural, formação de defeitos e reempilhamento.
2. **Protocolo AFM em GRMs (Seção IX.1.2, pp. 188–197, Figs. IX.11–IX.19):**
   - **LPE/dispersões (IX.1.2.1):** *drop-casting* em *wafers* $\text{SiO}_2\ (200\text{–}300\text{ nm})/\text{Si}$ pré-aquecidos $50\text{–}70\ ^\circ\text{C}$ acima do ponto de ebulição do solvente; lavagem exaustiva de surfactantes ou transferência NMP$\rightarrow$IPA. A altura aparente de `1L` é tipicamente **$1\text{–}2\text{ nm}$** por solvente residual/forças capilares e *crosstalk* eletrostático. Recomenda calibrar o degrau 1L usando flocos com terraços internos + Raman/PL, medir **$100\text{–}150$ flocos** para construir histogramas **lognormais** (desvios na cauda grossa acusam reagregação; na cauda fina acusam resíduos) e calcular $\langle N \rangle_{V_f} = \sum N^2 LW / \sum NLW$.
   - **Crescimento/isolantes (IX.1.2.2):** em quartzo, a espessura em modo dinâmico chegou a **$\sim 3\text{ nm}$** — quase o dobro do modo contato (Fig. IX.15) — por forças eletrostáticas não compensadas; contraste de fase inverte conforme o *setpoint* (Fig. IX.14); *tip sweeping* ($>100\text{ nN}$) danifica irreversivelmente a ponta (Fig. IX.18); KPM sofre triagem por adsorvatos ambientais revertida por recozimento $>150\ ^\circ\text{C}$ (Fig. IX.19).
3. **TEM, Raman e XPS como referências (Seções IX.1.3, IX.2.1 e IX.2.3, pp. 198–222):**
   - **TEM:** contagem de $\sim 150$ flocos para média lateral; franjas `(0002)` em bordas dobradas e difração SAED para $N$; operação $\le 80\text{ kV}$ (ou $20\text{–}40\text{ kV}$ `Cc/Cs`-corrigido) para evitar dano *knock-on*.
   - **Raman:** $2D$, $C$/LBM para $N$ e Eqs. (IX.7)–(IX.10) para distância interdefeitos $L_D$ e densidade $n_D$ corrigidas por energia do laser $E_L^4$ e dopagem $E_F$.
   - **XPS:** decomposição de $C1s$ ($sp^2 \sim 284{,}4\text{ eV}$, $sp^3 \sim 284{,}7\text{ eV}$, $\text{C–OH } 285{,}4\text{ eV}$, $\text{C–O } 286{,}7\text{ eV}$, $\text{C=O } 288{,}5\text{ eV}$, Tabela IX.2) para medir razão $C/O$ e distinguir contaminação de GO/rGO.

---

### 3.2 Kauling et al. (2018) — *Advanced Materials*
- **Status de leitura:** **Resumo e metadados verificados** (periódico fechado em [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json); texto integral pendente via CAPES/UFCA).
- **Identificação bibliográfica:** Kauling, A. P., Seefeldt, A. T., Pisoni, D. P., Pradeep, R. C., Bentini, R., Oliveira, R. V. B., Novoselov, K. S., & Castro Neto, A. H. (2018). *The Worldwide Graphene Flake Production.* *Advanced Materials*, 30(44), e1803784. DOI: `10.1002/adma.201803784`.

#### Síntese fiel ao resumo verificado
Avaliação sistemática de amostras comerciais de "grafeno" de **60 produtores mundiais** utilizando microscopia eletrônica (SEM/TEM), AFM, espectroscopia Raman, análise elementar e XPS. Os autores demonstraram a natureza estatística da esfoliação em fase líquida e comprovaram que a maioria das empresas produz **microplaquetas de grafite** com baixa qualidade e ampla dispersão, propondo substituir rótulos comerciais simplistas por **funções de distribuição estatística para número de camadas e tamanho de floco**, além de padrões rigorosos de caracterização.

---

### 3.3 Despotelis, Pollard, Clifford & Paton — NPL Report AS 103 / VAMAS TWA 41 (2022/2023)
- **Status de leitura:** **Texto completo lido integralmente** (24 pp., 17 figuras em [`NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.md)).
- **Identificação bibliográfica:** Despotelis, K., Pollard, A., Clifford, C., & Paton, K. (2022/2023). *VAMAS TWA 41 - Graphene and Related 2D Materials Project 12 - Distribution of lateral size and thickness of few-layer graphene flakes using SEM and AFM. SEM and AFM measurement protocol.* NPL Report AS 103 (`10.47120/npl.as103`; dataset Zenodo: `10.5281/zenodo.10119370`).

#### Metodologia e Regras Metrológicas Extraídas
Protocolo interlaboratorial internacional vinculado à **`ISO/TS 21356-1:2021`** e ao projeto EMPIR `19NORM04 ISO-G-SCoPe`:
1. **Substratos separados (Sec. 2 & 4.1, pp. 1–6):** usa *wafer* de Si com **óxido nativo fino** no MEV (para conduzir carga e evitar *charging*) e *wafer* com **$\text{SiO}_2\ (300 \pm 5\text{ nm})/\text{Si}$** no AFM (para visibilidade óptica). **Regra crítica:** como a varredura eletrônica no MEV deposita contaminação carbonácea na superfície, **as medições MEV e AFM devem ser realizadas em amostras separadas**, e o ajuste de foco/estigmador no MEV deve ocorrer em feição vizinha fora do floco de interesse.
2. **Protocolo MEV (Sec. 4.2–4.4, pp. 6–12, Figs. 5–7):** $V_{\text{acc}} \le 5\text{ kV}$, detector SE; mapa a `~10.000×` seguido de alta magnificação (`>20.000×`, tamanho de pixel **`< 10 nm`**); medir **$\ge 200$ flocos isolados** (todos os elegíveis de cada campo, excluindo toques, sobreposições parciais ou flocos cortados pela borda, para eliminar viés do operador por flocos grandes); definir comprimento $L$ (maior eixo do menor retângulo/elipse envolvente) e largura $W$ (**segmento perpendicular bissetor de $L$**, Fig. 5); calibrar após a sessão com grade `Pelcotec G-1T um` em 3 áreas (5 quadrados X/Y); plotar histograma com **$\ge 20$ *bins*** e ajustar **distribuição lognormal**.
3. **Protocolo AFM (Sec. 5, pp. 13–22, Figs. 8–17):** modo *tapping* em *closed-loop*, cantilever $k \sim 40\text{ N/m}$, $f_0 \sim 240\text{ kHz}$, raio $5\text{–}15\text{ nm}$, *setpoint* $40\% < \text{sp} \le 70\%$, velocidade $<10\ \mu\text{m/s}$, `512×512 px` em janelas de $(0{,}5\ \mu\text{m})^2$ a $(2\ \mu\text{m})^2$ cobrindo a mesma faixa de tamanhos laterais do MEV; **$\ge 20$ flocos primários planos** livres de dobras, resíduos, *double-tip* ou *flying tip* (Figs. 13 e 15); salvar dados brutos; aplicar correção de plano 1ª/2ª ordem **mascarando os flocos**; extrair média de 3 perfis transversais paralelos à varredura rápida + RMS do substrato + gráfico **espessura vs. tamanho lateral ($R^2$)** (Fig. 17).
- **Nota:** O relatório especifica o protocolo ILC e formatos de reporte, sem publicar ainda os resultados consolidados dos laboratórios participantes.

#### Contribuição integrada do Bloco 3 *(Análise crítica)*
Ancora o projeto exatamente nos procedimentos aceitos pela comunidade internacional para amostras polidispersas (como as de esfoliação eletroquímica da UFCA), explicando a divisão de trabalho MEV (estatística lateral $\ge 200$ flocos) vs. AFM (espessura $\ge 20$ flocos em substrato separado) e fornecendo os parâmetros exatos que o módulo computacional deverá implementar.

---

## Bloco 4 — Física e Limites da DRX em Carbono, Grafite e GO

### 4.1 Li, Lu, Xia, Zhou & Luo (2007) — *Carbon*
- **Status de leitura:** **Metadados e síntese secundária verificada** (periódico fechado em [`oa_li_2007.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-b/oa_li_2007.json), `oa_status: closed`, sem resumo no OpenAlex; síntese pública consultada via busca web verificada; texto integral pendente via CAPES/UFCA).
- **Identificação bibliográfica:** Li, Z. Q., Lu, C. J., Xia, Z. P., Zhou, Y., & Luo, Z. (2007). *X-ray diffraction patterns of graphite and turbostratic carbon.* *Carbon*, 45(8), 1686–1695. DOI: `10.1016/j.carbon.2007.03.038`.

#### Síntese verificada (restrita às fontes acessíveis)
Investiga por modelagem computacional baseada na **equação geral de Debye** e densidade numérica de distâncias interatômicas (NDID) como defeitos e desordem microestrutural alteram os difratogramas de raios X do grafite hexagonal ($h$-grafite) em comparação ao carbono turboestrático ($t$-carbono). Mostra que distorções como **rotações e translações aleatórias entre camadas, curvatura de planos, flutuações no espaçamento interplanar $d_{002}$ e deslocamentos atômicos** deslocam as posições angulares e alargam a `FWHM` dos picos de difração, fazendo com que parâmetros aparentes derivados de forma direta pela equação de Scherrer não reflitam linearmente o tamanho real de cristalito ou grau de grafitização em carbonos turboestráticos.

---

### 4.2 Holzwarth & Gibson (2011) — *Nature Nanotechnology*
- **Status de leitura:** **Metadados e síntese pública verificada** (correspondência histórica de 1 página em periódico fechado [`oa_holzwarth_2011.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-b/oa_holzwarth_2011.json), PubMed PMID `21873991`, sem *abstract* formal por tratar-se de carta/correspondência; texto integral pendente via CAPES/UFCA).
- **Identificação bibliográfica:** Holzwarth, U., & Gibson, N. (2011). *The Scherrer equation versus the 'Debye-Scherrer equation'.* *Nature Nanotechnology*, 6(9), 534. DOI: `10.1038/nnano.2011.145`.

#### Síntese verificada (restrita às fontes acessíveis)
Esclarece dois pontos metrológicos essenciais sobre análise de largura de picos em DRX:
1. A equação $\tau = K\lambda / (\beta\cos\theta)$ foi derivada isoladamente por **Paul Scherrer (1918)** — chamá-la de *"equação de Debye–Scherrer"* é um equívoco histórico (Debye e Scherrer desenvolveram juntos o método/câmara de pó, não a fórmula de tamanho de cristalito).
2. A equação estima a dimensão média dos **domínios de difração coerente** (e não diretamente o tamanho físico de partículas/agregados), exigindo correção explícita do **alargamento instrumental** e consideração da **microdeformação (*microstrain*)** antes de qualquer cálculo quantitativo.

#### Contribuição integrada do Bloco 4 *(Análise crítica)*
Blindagem conceitual para a seção de DRX da dissertação: impede afirmar que desaparecimento ou alargamento do pico `(002)` é sinônimo de grafeno monocamada ou que $L_c$ calculado por Scherrer sem padrão instrumental ($\text{LaB}_6$/Si) mede diretamente espessura de flocos polidispersos ou turboestráticos.

---

## Bloco 5 — Contraste Quantitativo em MEV de Grafeno

### 5.1 Zhou et al. (2016) — *Scientific Reports*
- **Status de leitura:** **Texto completo lido integralmente** (8 pp., 4 figuras, 37 referências em [`Zhou_2016_Quantitative_SE_Imaging_Work_Function_Graphene.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Zhou_2016_Quantitative_SE_Imaging_Work_Function_Graphene.md); Material Suplementar `S1–S10` não incluso no arquivo extraído).
- **Identificação bibliográfica:** Zhou, Y. et al. (2016). *Quantitative secondary electron imaging for work function extraction at atomic level and layer identification of graphene.* *Scientific Reports*, 6, 21045. DOI: `10.1038/srep21045`.

#### Problema, Fundamentação e Metodologia *(extraídas do artigo)*
- **Problema:** Estabelecer um método de contraste por elétrons secundários (SE) em MEV (e HIM) que seja quantitativo, reprodutível entre instrumentos e capaz de identificar número de camadas ($N$) e extrair a função trabalho ($\Phi$) com resolução nanométrica.
- **Modelo físico — Eqs. (1)–(4):** o sinal SE do grafeno suportado soma a emissão intrínseca do grafeno (excitado pelo feixe primário e pelos BSEs do substrato $\eta_s$) e os SEs do substrato transmitidos com atenuação exponencial $\alpha \exp(-N d/\lambda)$, onde $d = 0{,}335\text{ nm}$ e $\lambda$ é o livre caminho médio inelástico (IMFP). Para $N \ge 4$, $\Phi(N)$ satura e o contraste cai linearmente por atenuação; para $1 \le N \le 3$, o desvio não linear frente à reta extrapolada de `4–8L` conecta-se à função trabalho via modelo espectral de Chung & Everhart ($\partial\delta/\partial E_K \propto E_K / (E_K + \Phi)^n$, Eq. 3–4). *(Nota textual: na p. 2 há erro tipográfico na fórmula impressa `I_g/I_g - 1`, devendo ser lida como `(I_g/I_s - 1)*100%`.)*
- **Protocolo experimental:** esfoliação mecânica sobre $\text{SiO}_2\ (285\text{ nm})/p\text{-Si}$ (validada previamente por contraste óptico e Raman) + transferência para `Au/Cu/Ni` e buracos suspensos de $2\ \mu\text{m}$. Imagens obtidas em **dois MEVs** (`Carl Zeiss Supra` e `FEI Strata DB235`) com detector **`InLens`**, abertura $10\ \mu\text{m}$, $5\text{–}20\text{ pA}$, `WD = 4 mm`, `2500×`, `1024×768 px`, tempo $26\text{ s}$, vácuo $\sim 2\times 10^{-5}\text{ mbar}$, variando $E_p$ de $0{,}5\text{ a }20\text{ keV}$, além de microscópio iônico de hélio (`Carl Zeiss Orion Plus`, $30\text{ keV He}^+$ com *flood gun* $500\text{ eV}$ em $10\ \mu\text{s}$). Validação direta dos espectros de energia SE por filtro passa-alta em grade TEM ($0\text{ a }-10\text{ V}$).

#### Resultados observados *(extraídos do artigo)*
- **Inversão de contraste em $\text{SiO}_2/\text{Si}$ (Fig. 1b–c):** `1L` aparece mais clara a `0,5 keV` ($C_g = +9\%$), quase invisível no interior a `1,5 keV` ($+1\%$, borda $7\%$) e mais escura acima de `2 keV`, atingindo máximo absoluto próximo a **`5 keV` ($|C_g| \approx 20\%$)**; abaixo de `1 keV`, carregamento suprime o rendimento SE. Em `Au`, o contraste mantém-se próximo a `~10%` independente de $E_p$; em HIM com *flood gun* otimizado (`10 µs`), `1L` atinge `~54%` (Fig. 1d).
- **Resolução lateral (Fig. 2d):** transição de borda `1L–2L` de **`~10 nm`** em SEM/HIM frente a **`~680 nm`** em microscopia óptica.
- **Reprodutibilidade estatística (`>100` flocos a `5 keV`, InLens, Fig. 2e):** distribuições gaussianas separadas de **$(18 \pm 1)\%$ (`1L`)** e **$(26 \pm 2)\%$ (`2L`)**, reproduzidas exatamente no segundo equipamento `FEI Strata DB235`.
- **Alcance em camadas e $\Phi$ (Figs. 3–4):** distinção até **`10` camadas**; ajuste linear `4–8L` fornece **$\lambda \approx 5{,}7 \pm 0{,}1\text{ nm}$**; saturação próximo a **`14` camadas** convergindo a $\sim -0{,}60 \pm 0{,}01$ em grafite espesso. Função trabalho extraída com $n = 4{,}6$ (MEV) evolui de **$\Phi(1) = 4{,}26 \pm 0{,}05\text{ eV}$** a **$\Phi(4) = 4{,}60 \pm 0{,}07\text{ eV}$** (precisão relativa $<10\text{ meV}$; corroborada por `4,33 eV` no espectro SE de monocamada suspensa, pico em $1{,}5\text{ eV}$, e por HIM $4{,}35 \to 4{,}56\text{ eV}$).

#### Limitações
- Válido somente até $N \le 4$ para $\Phi$ e $\sim 10\text{–}14$ camadas para contraste; sensível a carregamento ($<1\text{ keV}$), contaminação por feixe, substrato e calibração estrita de `InLens` + `WD = 4 mm` + ancoragem em $\Phi(4)$ — não sendo transferível automaticamente para amostras sujas/GO ou outros detectores sem recalibração.

---

### 5.2 Huang & Gan (2024) — *Micron*
- **Status de leitura:** **Resumo, Highlights, Introdução pública e snippets de seções verificados** (periódico fechado Elsevier, ScienceDirect preview e PubMed PMID `39276729`, registrados no fichamento [`01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md); texto completo pendente via CAPES/UFCA).
- **Identificação bibliográfica:** Huang, L., & Gan, Y. (2024). *A review on SEM imaging of graphene layers.* *Micron*, 187, 103716 (169 referências). DOI: `10.1016/j.micron.2024.103716`.

#### Síntese verificada (restrita às partes públicas inspecionadas)
- **Foco e diagnóstico instrumental:** revisão centrada principalmente em grafeno CVD; explica por que parâmetros convencionais de MEV (`V_acc = 15–20 kV`, `WD = 8–12 mm`) resultam em contraste fraco e sintetiza o papel de `SE1, SE2, SE3`, detectores **E-T vs. *in-lens*** e natureza do substrato.
- **Contribuição chave visível na pré-visualização:** demonstra que **o aumento de `WD`** (combinado ou não à baixa `V_acc`) gera contraste elevado de grafeno mesmo utilizando o **detector E-T convencional**, além de suprimir a heterogeneidade de fundo causada pelo **contraste de canalização eletrônica (ECC)** em grãos policristalinos de cobre (`Cu`) e revelar redução induzida por feixe de óxidos interfaciais.

---

## Bloco 6 — Pipelines Automatizados de Segmentação em 2D

### 6.1 Masubuchi et al. (2020) — *npj 2D Materials and Applications*
- **Status de leitura:** **Texto completo lido** (9 pp., 5 figuras em [`Masubuchi_2020_Deep_Learning_Image_Segmentation_2D_Materials.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Masubuchi_2020_Deep_Learning_Image_Segmentation_2D_Materials.md); tabelas/figuras suplementares citadas não inclusas no texto extraído).
- **Identificação bibliográfica:** Masubuchi, S. et al. (2020). *Deep-learning-based image segmentation integrated with optical microscopy for automatically searching for two-dimensional materials.* *npj 2D Materials and Applications*, 4, 3. DOI: `10.1038/s41699-020-0137-z`.

#### Problema, Metodologia e Arquitetura *(extraídas do artigo)*
- **Problema:** algoritmos convencionais baseados em regras (contraste de cor, bordas, entropia) exigem recalibração manual de $\ge 30\text{ min}$ por amostra sempre que muda a iluminação ou o microscópio.
- **Arquitetura e dados:** **Mask R-CNN** (`ResNet-101` + `RPN` + `ROI Align` + `FCN`, em Keras/TensorFlow) inicializada com pesos do `MS-COCO` e treinada em **duas etapas** (primeiro em conjunto misto de 2D, depois *transfer learning* por material) sobre **2.102 imagens ópticas anotadas** (**7.153 objetos**: grafeno `862 img / 4.805 obj`, $\text{MoS}_2$ `569 / 839`, $\text{WTe}_2$ `318 / 1.053`, hBN `353 / 456`) em $\text{SiO}_2(290/90\text{ nm})/\text{Si}$, divididas aleatoriamente em 8:2 e redimensionadas para `1024×1024 px²` com *data augmentation online* (multiplicação de cor, flips, rotações, deslocamentos) e fluxo semiautomático via `LabelBox` (pré-treino em ~80 imagens $\rightarrow$ correção humana em 20–30 s/imagem). Classes: `mono` (1L), `few` (2–10L), `thick` (10–40L).

#### Resultados observados *(extraídos do artigo)*
- **Velocidade e escalabilidade:** inferência de **`200 ms`** por imagem `1024×1024` em GPU Tesla V100 ($\sim 1\text{ fps}$ incluindo captura/transferência), varrendo um substrato $1\times 1\text{ cm}^2$ ($50\times$) em 1 hora.
- **Desempenho e robustez à iluminação (Fig. 2, pp. 3–4):** no grafeno (nível de imagem), alcançou **precisão $\sim 0{,}95$ e revocação $\sim 0{,}97$** com **`mAP@IoU50% = 0,49`** (em $\text{WTe}_2$: precisão $\sim 0{,}53$, revocação $\sim 0{,}93$, `mAP@IoU50% = 0,52`). Sob redução da intensidade luminosa ($I = 220 \to 180 \to 90$, Fig. 2a–f), o detector baseado em regras falhou completamente em $I=180$, enquanto Mask R-CNN manteve as máscaras inalteradas.
- **Transferência e generalização (Figs. 4–5):** pré-treino em múltiplos materiais 2D + `MS-COCO` acelerou convergência (30 épocas igualaram 80 épocas só com `COCO`) e reduziu falsos negativos/positivos; a rede treinada em grafeno generalizou sem retreinamento para **3 microscópios ópticos diferentes** (Asahikogaku, Keyence VHX-900 e VHX-5000, Fig. 5), e o modelo $\text{WTe}_2$ detectou $\text{WSe}_2$ e $\text{MoSe}_2$ inéditos. Código, dataset e pesos liberados em `github.com/tdmms/`.

#### Limitações *(extraídas + análise crítica)*
Os autores observam que a classificação em 3 faixas (`mono/few/thick`) serve como **triagem inicial**, exigindo verificação posterior de espessura exata; criticamente, todo o método depende de **microscopia óptica RGB sobre $\text{SiO}_2/\text{Si}$** de flocos mecanicamente esfoliados e usou divisão aleatória 8:2 das imagens sem relatar agrupamento explícito por *wafer*.

---

### 6.2 Saito et al. (2019) — *npj Computational Materials*
- **Status de leitura:** **Texto completo lido** (6 pp., 4 figuras em [`Saito_2019_Deep_Learning_Quality_Filtering_2D_Crystals.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Saito_2019_Deep_Learning_Quality_Filtering_2D_Crystals.md)).
- **Identificação bibliográfica:** Saito, Y. et al. (2019). *Deep-learning-based quality filtering of mechanically exfoliated 2D crystals.* *npj Computational Materials*, 5, 124. DOI: `10.1038/s41524-019-0262-4`.

#### Metodologia e Resultados observados *(extraídas do artigo)*
- **Dados e arquitetura:** **U-Net** (`512×512×3`, 14 camadas no *encoder* + 18 no *decoder*, *dropout* de $50\%$ no *decoder*, `softmax`, otimizador `Adam`) treinada com um conjunto pequeno realista de imagens ópticas ($\text{SiO}_2\ 300\text{ nm}/\text{Si}$, $100\times$): **24 imagens treino / 11 teste para $\text{MoS}_2$** e **30 treino / 14 teste para grafeno/grafite**, confirmadas por AFM e contraste óptico, aumentadas para **960 imagens** (recortes, flips, rotação $\pm 90^\circ$, variação de matiz HSV $\pm 10$ e contraste `0,7–1,3×`).
- **Combate ao desbalanceamento (Tabela 1, p. 4):** comparou entropia cruzada padrão vs. **entropia cruzada ponderada (*median frequency balancing*)** na validação cruzada de 3 dobras em $\text{MoS}_2$: U-Net padrão (`0,584`) $\rightarrow$ U-Net ponderada + aumento de contraste (**`0,789`**); em teste cego obteve **`0,733`**, igualando/superando **12 humanos não especialistas (`0,67 ± 0,11`)**, `BoVW` clássico e CNN pixel-a-pixel (Fig. 2). Com taxa de erro de omissão (*miss rate*) de $24\%$ (1L) e $6\%$ (2L), a precisão superou $90\%$ (Fig. 3). Resultados semelhantes ($70\text{–}80\%$) foram obtidos em grafeno (Suplemento Sec. III). Código aberto em `github.com/xinkent/mos2_segmentation`.
- **Achado crítico para MEV/AFM:** ao converter as imagens ópticas para **escala de cinza**, o escore caiu drasticamente (`0,789` $\to$ `0,723` / `0,560`, Tabela 1), e com poucos dados a U-Net tendeu a confundir ocasionalmente o substrato limpo com monocamada.

#### Contribuição integrada do Bloco 6 *(Análise crítica)*
Mostra que U-Net com perda ponderada funciona em regime de poucos dados ($24\text{–}30$ imagens) e Mask R-CNN separa instâncias mesmo com mudança de equipamento, mas ambos exploraram **cor RGB interferencial em OM**. Ao migrar para **MEV e AFM** (imagens monocromáticas/topográficas), não há informação cromática — reforçando que segmentação em MEV/AFM exige calibração física de contraste/altura e pré-processamento rigoroso.

---

## Bloco 7 — ML/DL em DRX e Limitação *Sim-to-Real*

> [!NOTE]
> Este bloco substitui integralmente o preprint retirado `Wang et al. (2026)` (`arXiv:2608.22400v2`) por dois artigos revisados por pares com texto completo lido.

### 7.1 Oviedo et al. (2019) — *npj Computational Materials*
- **Status de leitura:** **Texto completo lido** (9 pp., 5 figuras, Tabela 1 em [`Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.md)).
- **Identificação bibliográfica:** Oviedo, F. et al. (2019). *Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks.* *npj Computational Materials*, 5, 60. DOI: `10.1038/s41524-019-0196-x`.

#### Problema, Metodologia e Resultados observados *(extraídas do artigo)*
- **Problema e banco:** classificar dimensionalidade cristalina (0D, 2D, 3D; 75 espectros) e grupo espacial (7 grupos; 88 espectros) a partir de apenas **115 difratogramas experimentais únicos** de filmes finos de haletos metálicos ($2\theta = 5\text{–}60^\circ$, passo $0{,}04^\circ$) + **164 padrões de pó simulados do ICSD**, onde o refinamento de Rietveld falha por textura/orientação preferencial desconhecida.
- **Aumento de dados fisicamente informado (Fig. 2, Eqs. 1–3):** gera `2.000` padrões simulados aumentados + `2.000` experimentais aumentados via 3 transformações: (1) **escalamento periódico de picos** e (2) **eliminação periódica de picos** (simulando orientação preferencial de filmes finos), mais (3) **deslocamento em $2\theta$** (deformação/composição). Isso elevou a acurácia em **$+23\%$** (dimensionalidade) e **$+19\%$** (grupo espacial) frente a zero aumento, e superou aumento com ruído em **`>12%` absolutos**.
- **Comparação de 10 algoritmos e prova do *Sim-to-Real Gap* (Tabela 1, p. 5):**
  - **Caso 1 (simulado $\rightarrow$ simulado, 5-fold CV):** `a-CNN` 1D (3 camadas conv, *Global Average Pooling*, sem *max-pooling*/densas finais) atingiu **`99,1%` / `99,1%`**.
  - **Caso 2 (apenas simulado $\rightarrow$ experimental real):** `a-CNN` caiu para **`83,7%` / `80,2%`**, enquanto modelos clássicos sem dados reais despencaram em grupo espacial (`k-NN 21,2%`, `Naive Bayes 25,5%`, `Regressão Logística 13,9%`).
  - **Caso 3 (simulado + 80% exp $\rightarrow$ 20% exp):** `a-CNN` recuperou **`92,9%` (`micro F1 0,929`, `macro F1 0,859`)** para dimensionalidade e **`89,3%` (`micro F1 0,893`, `macro F1 0,714`)** para grupo espacial.
- **Interpretabilidade e velocidade (Figs. 4–5):** **Mapas de Ativação de Classe médios (CAMs)** identificaram 3 causas raiz de erro (mistura de fases, classes minoritárias com $<5$ padrões e picos ausentes); o passo pôde ser engrossado até **`0,16° 2θ`** mantendo acurácia $>85\%$ e reduzindo tempo de aquisição em $75\%$ ($<5{,}5\text{ min}$). Código/dados experimentais em `github.com/PV-Lab/AUTO-XRD/`.

---

### 7.2 Greasley & Hosein (2023) — *Journal of Materials Science*
- **Status de leitura:** **Texto completo lido** via manuscrito correspondente dos autores `arXiv:2211.08591v1` (12 pp., 3 figuras, 4 tabelas em [`Greasley_Hosein_2023_Supervised_ML_Powder_XRD.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Greasley_Hosein_2023_Supervised_ML_Powder_XRD.md)), publicado com revisão por pares em *Journal of Materials Science*, 58(12), 5334–5348 (`10.1007/s10853-023-08343-4`).
- **Identificação bibliográfica:** Greasley, J., & Hosein, P. (2023). *Exploring supervised machine learning for multi-phase identification and quantification from powder X-ray diffraction spectra.* *Journal of Materials Science*, 58(12), 5334–5348. DOI: `10.1007/s10853-023-08343-4`.

#### Metodologia e Resultados observados *(extraídas do manuscrito correspondente)*
- **Dados:** banco experimental pequeno de cálculos urinários ($N = 52$ difratogramas PXRD, `Bruker D2 Phaser`, $2\text{–}55^\circ$, passo $0{,}02^\circ$, 7 fases minerais com até 4 fases por amostra; $N = 46$ com frações de massa quantificadas por Rietveld em `MAUD`) + simulações via `pymatgen`/COD com perturbações físicas de Szymanski (*zero offset*, parâmetros de rede, orientação preferencial, fundo polinomial `4ª–7ª ordem` + ruído) e `GSAS-II` para fases nanocristalinas de picos largos ($105$ monofásicos / $184$ multifásicos).
- **Benchmark sistemático em 4 cenários (Tabelas 2–4, Figs. 2–3):**
  - **Instância [2] (só experimental — 5-fold CV / LOOCV):** **`CNB` (*Complement Naive Bayes*) alcançou `88,8%` de acurácia total (`F1 avg = 0,812`, `MPA = 96,4%`) treinando em apenas `0,03 s`**, superando ou empatando com a `ANN` (`88,3%`, `F1 = 0,810`, `67 s`) e `SVM` (`87,3%`, `MPA = 98,2%`, `ELA = 47,3%`). Na regressão quantitativa (LOOCV, $N=46$), `ANN` (`\rho = 0,8582`, `MAE = 0,0491`) e `k-NN` (`\rho = 0,8369`, `MAE = 0,0520`) lideraram após imposição de positividade e soma unitária ($\sum \hat{\alpha} = 1$).
  - **Instância [3] (só simulado $\rightarrow$ experimental — *sim-to-real*):** **`SVM` (`87,9%`, `F1 avg = 0,787`, `MPA = 100%`) e `CNB` (`87,6%`, `F1 = 0,783`) superaram a `ANN` (`87,1%`, `F1 = 0,763`)**, enquanto florestas (`RF 78,6%`, `MPA = 63,5%`) degradaram fortemente. Na regressão, o treino puramente simulado teve o pior desempenho médio ($\rho_{\text{avg}} = 0{,}712$ vs. $0{,}808$ na Instância [2]), com **`k-NN` (`\rho = 0,7535`, `MAE = 0,0827`)** superando a `ANN` em MAE (`0,0879`).
  - **Instância [4] (simulado + experimental $\rightarrow$ experimental):** `SVM` (`88,8%`) e `ANN` (`88,9%`) empataram na classificação; na regressão quantitativa de fases, **`k-NN` obteve o melhor resultado absoluto (`\rho = 0,8462`, `MAE = 0,0479`, `CS = 0,9539`)**.

#### Contribuição integrada do Bloco 7 *(Análise crítica)*
Para o estágio investigativo do PPGCEM/UFCA (com dezenas e não milhões de espectros de grafite/GO/rGO), este bloco oferece duas lições vitais: (1) **modelos clássicos interpretáveis (`SVM`, `CNB`, `k-NN`) devem ser sempre a linha de base antes de redes profundas**, pois igualam ou vencem redes neurais em dados escassos com fração mínima de custo; e (2) **nunca confiar em treino puramente simulado sem calibração e validação com padrões experimentais reais**, utilizando *data augmentation* fisicamente realista (textura, alargamento de cristalito, *zero offset*) e mapas de interpretabilidade (`CAMs`).
