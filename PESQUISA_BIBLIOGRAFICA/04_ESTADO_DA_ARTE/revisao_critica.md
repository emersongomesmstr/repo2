# Revisão Crítica do Estado da Arte: Síntese Integrada (Seção 10 do Protocolo)

> **Declaração de rigor epistêmico e status do projeto:** Esta síntese responde às **10 questões orientadoras da Seção 10** de [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md), separando explicitamente: **(a) conhecimento científico estabelecido**, **(b) resultados experimentais publicados**, **(c) métodos computacionais validados**, **(d) hipóteses da literatura**, **(e) possibilidades não demonstradas** e **(f) lacunas abertas**. O software da dissertação encontra-se em **fase estritamente investigativa**, sem protótipo validado em grafeno; citações e links remetem ao catálogo auditado em [`biblioteca_completa.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/biblioteca_completa.md) e aos fichamentos em [`03_FICHAMENTOS/`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/).

---

### Auditoria Prévia de Integridade Bibliográfica
- **Exclusão obrigatória registrada:** O preprint `Wang et al. (2026) — arXiv:2608.22400v2` foi **oficialmente retirado (*withdrawn*)** pelos próprios autores no arXiv ([`arxiv_2608_22400v2.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_2608_22400v2.json)) por não atingir o nível de completude pretendido; consequentemente, **não é utilizado como evidência científica nem consta nas referências ativas**.
- **Preprints mantidos sob ressalva explícita:** `Ba Alawi (2025)` (`arXiv:2508.04035`), `Gerçek et al. (2025)` (`arXiv:2511.11485`, NeurIPS ML4PS Workshop) e `Cao (2026)` (`arXiv:2607.17162`) ainda não possuem versão publicada em periódico revisado por pares confirmada até `16/11/2026`.
- **Correções aplicadas:** `Holm et al. (2020)` refere-se exclusivamente ao DOI `10.1007/s11661-020-06008-4`; cinco preprints da busca inicial (`Leger 2024`, `Qi 2024`, `Wang/Pan 2026`, `Harris 2025`, `Greasley & Hosein 2023`) e `Uslu et al. (2025)` (*MaskTerial*) foram promovidos às suas versões revisadas por pares ([`consultas_utilizadas.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/01_ESTRATEGIA/consultas_utilizadas.md)).

---

## Questão 1 — O que já sabemos cientificamente sobre caracterização de grafeno por DRX, MEV e AFM?

- **Conhecimento científico estabelecido:**
  - Materiais de grafeno obtidos por rotas escaláveis (esfoliação líquida — LPE, eletroquímica ou redução de óxido de grafeno — GO/rGO) constituem **distribuições estatísticas polidispersas** de tamanho lateral, número de camadas $N$, grau de oxidação e defeitos, e não um produto monodisperso (`Kauling_2018`, `Backes_2020`).
  - As três técnicas atuam em regimes físicos **não intercambiáveis** (`Geim_2007`, `Despotelis_2023`): **DRX** sonda coerência cristalina e espaçamento interplanar médios em volume; **MEV** resolve morfologia planar e dimensões laterais com resolução `~10 nm` (`Zhou_2016`), mas não fornece espessura absoluta universal; **AFM** mede topografia 3D nanométrica em área local restrita, porém sobre-estima monocamadas em ar (`0,4–2,0 nm` vs `0,335 nm` cristalográfico) devido a adsorbatos e bistabilidade ponta–amostra (`Novoselov_2004`, `Nemes_Incze_2008`, `Shearer_2016`).
- **Resultados experimentais publicados:**
  - `Kauling et al. (2018)` auditaram `60` produtores globais e provaram que a maioria entrega microplaquetas grafíticas, exigindo classificação por funções de distribuição.
  - `Backes et al. (2020)` estabeleceram amostragem estatística mínima de `>=100–150` flocos (AFM/TEM) e ponderação por fração volumétrica $\langle N \rangle_{Vf} = \sum N^2 L W / \sum N L W$.
  - `Despotelis et al. (2023)` (`VAMAS TWA 41 / NPL AS 103`, visando `ISO/TS 21356-1`) e `Chemello et al. (2025)` normatizaram no MEV contagem `>=200` flocos em `SiO2` nativo (`<=5 kV`, detector `InLens`), mostrando que a heterogeneidade de secagem (*coffee rings*) causa variações de até `~30%` — uma ordem de grandeza acima da divergência entre operadores nas mesmas imagens (`0%–4,6%`).
  - No Brasil, `Martins et al. (2025)` (Inmetro/LNCC/UFBA) validaram protocolo combinado SEM+AFM para GO destinado à ABNT/CRM usando segmentação C++ por entropia para delinear/contar folhas, registrando explicitamente que o modelo não resolve o número de camadas.

---

## Questão 2 — Que propriedades são mensuráveis por cada técnica?

| Técnica | Propriedades Diretamente Mensuráveis (Estabelecido / Publicado) | Escala & Amostragem Típica | O Que **Não** Mede Sozinha |
|---|---|---|---|
| **DRX** | Espaçamento basal médio $d_{002}$ (`~0,335 nm` grafite) ou $d_{001}$ (`>0,7–0,8 nm` GO), largura à meia altura (`FWHM`), assimetria de bandas turboestráticas `(10)/(11)` (`Li_2007`), fases cristalinas residuais de síntese/sais e tamanho de domínio coerente $L_c, L_a$ (`Iwashita_2004`, `Stobinski_2014`, `Holzwarth_2011`). | Miligramas (média volumétrica de todo o pó/filme). | Espessura ou distribuição individual de flocos; monocamada isolada (sem pico `(002)`). |
| **MEV** | Dimensões laterais ($L$, $W$, Área, `minFeret`, `maxFeret`, `ECD`), fatores de forma (`Feret ratio`, `AR = W/L`, circularidade), cobertura areal, dobras visíveis, bordas (`~10 nm`) e aglomeração (`Despotelis_2023`, `Chemello_2025`, `Zhou_2016`). | Centenas de flocos (`>=200` VAMAS) por sessão; campo de `~5–40 µm`. | Espessura atômica absoluta universal ou química superficial (`C/O`, $sp^2/sp^3$). |
| **AFM** | Topografia 3D ($x, y, z$), alturas relativas de degraus entre terraços grafeno–grafeno (`~0,34–0,4 nm`/camada em dobras limpas) ou substrato–floco (`0,8–2,0 nm` em ar), rugosidade RMS, trincas/dobras e propriedades condutivas locais em C-AFM (`Novoselov_2004`, `Backes_2020`, `Harris_2025`). | Dezenas de flocos (`>=20` VAMAS; `>=100–150` `Backes_2020`); varreduras `0,5–2 µm`. | Química de oxidação/dopagem ou estatística populacional rápida sem alto custo operacional. |

---

## Questão 3 — Quais inferências são indiretas e dependem de hipóteses?

- **Número de camadas $N$ no MEV a partir de níveis de cinza (`Hipótese condicional` / `Resultados sensíveis ao instrumento`):** Embora `Hiura et al. (2010)` (`-5,05%/camada` a `1,0 kV` externo, com anomalia em `1L`) e `Zhou et al. (2016)` (`InLens` `5 keV`, `WD = 4 mm`, saturação `10–14L` e extração de função trabalho $\Phi_N$) tenham demonstrado contraste quantitativo discreto, essa inferência **depende da hipótese estrita** de substrato uniforme, superfície livre de contaminação carbonácea/resíduo de solvente e constância absoluta de `V_acc`, `WD`, corrente e ganho de detector (`Huang_2024`). Sem curva de calibração na mesma sessão e confirmação Raman/AFM, inferir `N` por brilho de MEV é **possibilidade não demonstrada** em amostras eletroquímicas heterogêneas.
- **Conversão direta de altura AFM substrato–floco em $N$ (`Hipótese falha sem correção`):** Dividir a altura aparente por `0,335 nm` pressupõe ausência de adsorvato (`0,4–1,7 nm` segundo `Shearer_2016`), ausência de salto atrativo–repulsivo (`~0,8–1,0 nm` segundo `Nemes_Incze_2008`) e rigidez idêntica ponta–substrato vs. ponta–grafeno. A prática validada exige degraus entre terraços grafeno–grafeno, modo repulsivo controlado ou calibração por Raman (`Backes_2020`).
- **Equiparar $L_c$ / $L_a$ de Scherrer (DRX) ao tamanho físico do floco ou $N$ real (`Erro conceitual`):** `Holzwarth & Gibson (2011)` demonstram que Scherrer mede o domínio cristalino coerente médio afetado por defeitos, deformação e alargamento instrumental (`Iwashita_2004`). Inferir distribuição de camadas de flocos esfoliados apenas por `(002)` depende da hipótese não garantida de ausência de empilhamento aleatório/reempilhamento na secagem.
- **Correlações morfológicas -> desempenho/propriedade:** Mesmo com alta acurácia de segmentação (`Wang_2026`, `r = 0,78` área vs PCE), os próprios autores ressaltam tratar-se de correlação observacional, não relação causal validada.

---

## Questão 4 — Quais operações podem ser automatizadas por algoritmos tradicionais?

- **Métodos computacionais já validados ou consolidados em algoritmos clássicos (e plenamente executáveis em CPU modesta):**
  1. **Pré-processamento e morfometria 2D em MEV (`VanDerWalt_2014`, `Schindelin_2012`, `Otsu_1979`, `Chemello_2025`, `Martins_2025`):** calibração espacial (`nm/px` via barra de escala/grade `Pelcotec`), filtragem de ruído, normalização de fundo, limiarização adaptativa/Otsu/entropia, morfologia matemática, detecção de contornos fechados (`A1`), filtragem automática de bordas cortadas e resolução mínima (`px/ECD`), cálculo de Área, `ECD_A1`, `minFeret`, `maxFeret`, `Feret ratio`, ajuste log-normal (`>=20` *bins* conforme `Despotelis_2023`) e sinalização de zonas densas (*coffee rings*).
  2. **Processamento quantitativo em AFM (`Necas_2011`, `Villarrubia_1997`, `Yao_2017`, `Despotelis_2023`):** nivelamento polinomial (1ª/2ª ordem) **com mascaramento iterativo dos flocos**, extração automática de **histogramas de altura** (modas substrato vs. platôs segundo `Yao_2017`) ou múltiplos perfis ortogonais, correção geométrica de dilatação de ponta (`Villarrubia_1997`) e cálculo de métricas ponderadas ($\langle N \rangle_{Vf}$).
  3. **Pré-processamento e ajuste analítico em DRX (`Iwashita_2004`, `Toby_2013`, `Doebelin_2015`, `Cao_2026_arXiv`):** subtração de linha de base, calibração de deslocamento `2theta` por padrão interno, busca-casamento determinística (matching húngaro / NNLS para fases cristalinas residuais, como em `Cao_2026_arXiv` — preprint), deconvolução de perfis `(001)`/`(002)` com cálculo rastreável de $d_{002}$, `FWHM` e $L_c$ com incerteza instrumental declarada.

---

## Questão 5 — Onde aprendizado de máquina pode oferecer vantagem demonstrável?

- **Vantagens demonstráveis (com evidência empírica publicada) — apenas onde heurísticas clássicas falham:**
  1. **Microscopia com baixo contraste ou sobreposição de detectores/canais:** Em `Gerçek et al. (2025)` (preprint NeurIPS ML4PS), onde cinzas de carbonetos e matriz se sobrepunham no MEV, a `U-Net` bimodal (`SE2+InLens`) elevou o coeficiente Dice mediano de **`0,85` (`SimpleITK + Otsu`) para `0,98` (`p < 0,001`)** (e `0,94` vs `0,90` em aço inédito `ANP-3`). Em microscopia óptica 2D com iluminação variável entre equipamentos, `Mask R-CNN` (`Masubuchi_2020`), `2D U-Net/SegNet` (`Leger_2024`) e `MaskTerial` (`Uslu_2025`, com apenas `5–10` imagens) superaram limiares rígidos que quebram sob mudança de iluminação ou baixo contraste.
  2. **Preservação de textura complexa em microestruturas não separáveis por intensidade:** Em `Azimi et al. (2018)`, a `MVFCNN` pixel a pixel atingiu `93,94%` no MEV contra `48,89%` de descritores morfológicos manuais + SVM.
  3. **Aceleração de aquisição e triagem com poucas amostras rotuladas:** `Saito et al. (2019)` (`24–30` imagens com `U-Net` ponderada) e `Harris et al. (2025)` (`SwinIR` reduzindo tempo de C-AFM em `>11×`) demonstram ganho operacional claro quando há dados pareados de referência.
  4. **Classificação rápida e quantificação de incerteza em bancos pequenos de DRX:** `Oviedo et al. (2019)` mostraram que `AUTO-XRD` com aumento físico superou `KNN/RF/SVM` em filmes reais (`92,9%` vs `88,1%` SVM), enquanto **`Greasley & Hosein (2023)` provaram que, com ~`50` espectros reais, modelos clássicos (`CNB/SVM/k-NN`) igualam redes neurais (`F1 ~ 0,81`) em `0,03–0,08 s`** — indicando que, no cenário UFCA com poucos dados e sem GPU, **modelos clássicos/rasos ou híbridos com UQ** são mais defensáveis do que redes profundas pesadas.
- **Onde ML ainda NÃO demonstrou vantagem sobre métodos físicos:** regressão contínua direta de frações de fase em DRX sem Rietveld (`Lee_2020` falhou em regressão contínua); estimativa absoluta de camadas `N` diretamente de imagens MEV heterogêneas sem calibração física local (`Geim_2007`, `Huang_2024`).

---

## Questão 6 — Quais métodos já foram propostos na literatura?

1. **DRX:** refinamento Rietveld por mínimos quadrados e parâmetros fundamentais com defeitos de empilhamento (`GSAS-II`, `Profex/BGMN`), busca-casamento húngaro + NNLS (`XMatcher`, preprint `Cao_2026_arXiv`), CNNs 1D com aumento físico + `CAMs` (`Oviedo_2019`, `Wang_2020`), CNN combinatória sintética (`Lee_2020`), *ensembles* probabilísticos (`Szymanski_2021`) e comparativos `CNB/SVM/k-NN/RF/ANN` (`Greasley_2023`).
2. **MEV:** descritores locais `SIFT + BoVF + SVM` (`DeCost_2015`), `MVFCNN` em *patches* nativos (`Azimi_2018`), `U-Net` multicanal `SE2+InLens` + *Temperature Scaling* (`Gercek_2025_arXiv`, preprint), `PerovSegNet` (`YOLOv8x-seg` + `ASDCB` + `SAD`, `Wang_2026`), medição manual `A1/A2` no `Fiji` (`Despotelis_2023`, `Chemello_2025`) e segmentação por entropia C++ para GO (`Martins_2025`).
3. **AFM:** morfologia matemática de ponta (`Villarrubia_1997`), método de histogramas de platô (`Yao_2017`), análise modular no `Gwyddion` (`Necas_2011`), `Sparse C-AFM` com `SwinIR` (`Harris_2025`) e bases simuladas DFT/PPM (`QUAM-AFM` `Carracedo_Cosme_2022`).
4. **Materiais 2D em Microscopia Óptica / Espectroscopia:** `U-Net` ponderada (`Saito_2019`), `2DMOINet` (`Han_2020`), `Mask R-CNN` (`Masubuchi_2020`), `SegNet/U-Net` + `SLIC+DBSCAN` (`Leger_2024`), modelo fundacional `MaskTerial` (`Uslu_2025`) e `ResNet-DDPM + CNN 1D` para Raman (`Qi_2024`).

---

## Questão 7 — Quais softwares e ferramentas consolidadas existem?

Conforme detalhado em [`softwares_existentes.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/04_ESTADO_DA_ARTE/softwares_existentes.md): **`ImageJ/Fiji`** (`Schindelin_2012`), **`Gwyddion`** (`Necas_2011`), **`scikit-image` / `OpenCV`** (`VanDerWalt_2014`), **`GSAS-II`** (`Toby_2013`), **`Profex/BGMN`** (`Doebelin_2015`) e, em fase preprint aberta, **`XMatcher`** (`Cao_2026_arXiv`), além de repositórios de pipelines acadêmicos abertos (`tdmms`, `sparse-cafm`, `PerovSegNet`, `MaskTerial`, `carde`). **Nenhum deles integra DRX + MEV + AFM com calibração metrológica VAMAS/ISO para grafeno.**

---

## Questão 8 — Quais problemas permanecem abertos?

1. **Lacuna de datasets abertos anotados de grafeno eletroquímico/GO em MEV e AFM em ar** com verdade de campo (*ground truth*) pareada por Raman/TEM (`Botifoll_2022`, `Backes_2020`).
2. **Segmentação automatizada confiável de flocos parcialmente sobrepostos/dobrados e segregados em *coffee rings* no MEV**, superando o limite manual de `>=3` folhas sobrepostas (`Chemello_2025`) e substituindo `A2` por polígonos `A1`.
3. **Detecção automática de artefatos físicos em tempo de execução** (salto atrativo–repulsivo, ponta dupla, carga no MEV, contaminação carbonácea pós-feixe, ausência de padrão interno no DRX).
4. **Protocolos rigorosos anti-*leakage* em pequenas amostras experimentais**, evitando divisões aleatórias por *tiles* ou pós-*augmentation* (`IVEFAC333.pptx`, `Qi_2024`).
5. **Quantificação explícita de incerteza (UQ) e validação interlaboratorial** executável em hardware computacional modesto (`CPU` sem GPU dedicada).

---

## Questão 9 — Quais são as limitações de combinar técnicas experimentais diferentes?

- **Inviabilidade de medida sequencial no mesmo floco após MEV (`Despotelis_2023`):** O feixe eletrônico deposita carbono amorfo, invalidando medidas posteriores de altura AFM na mesma região; assim, o protocolo `VAMAS` impõe substratos fisicamente separados (`SiO2` nativo para MEV vs `300 nm SiO2/Si` em grade para AFM/OM), permitindo **integração estatística populacional em nível de amostra/lote**, não registro pixel a pixel.
- **Discrepância de volume amostral e viés de amostragem:** DRX integra miligramas em volume; MEV amostra `>=200` flocos bidimensionais dispersos (sujeitos a `~30%` de viés espacial por *coffee rings*, `Chemello_2025`); AFM mede tipicamente `20–150` flocos selecionados em áreas minúsculas (muitas vezes excluindo flocos muito espessos ou altamente agregados). Fundir médias simples de técnicas com funções de seleção distintas distorce $\langle N \rangle$ se não houver ponderação volumétrica ($\langle N \rangle_{Vf}$) e explicitação das distribuições completas.
- **Assimetria de grandezas físicas:** $L_c$ (DRX) $\neq$ altura aparente AFM $\neq$ contraste SE no MEV $\neq$ tamanho lateral $ECD$ no MEV. A combinação só é cientificamente válida como **evidência convergente complementar ancorada em *ground truth* (Raman/TEM/XPS)**, nunca por regressão direta cega de uma técnica sobre outra.

---

## Questão 10 — Qual direção de pesquisa parece mais promissora, considerando fundamentação, disponibilidade de dados e viabilidade?

Considerando o rigor físico da literatura, a ausência de GPU dedicada na infraestrutura local (Ryzen 3 7320U, ~3,24 GiB RAM disponíveis), o volume realista de amostras produzidas em bancada no mestrado e o estágio investigativo atual, a direção mais defensável e exequível consiste em:

1. **Priorizar uma arquitetura modular *physics-first* baseada em PDI determinístico auditável e ML clássico/leve (sem depender de Deep Learning pesado de início):**
   - **Módulo MEV (eixo de maior impacto imediato e menor barreira física):** implementar pipeline Python (`scikit-image`/`OpenCV`) aderente ao protocolo `VAMAS TWA 41 / Chemello 2025` para extrair **contorno `A1`** (`Area`, `ECD_A1`, `minFeret`, `maxFeret`, `Feret ratio`), imposto por guardas metrológicos (calibração `nm/px`, rejeição de flocos tocando borda, mínimo de pixels por floco, ajuste log-normal `>=20` *bins* e alerta de densidade/*coffee ring*).
   - **Módulo AFM (controle metrológico de espessura):** automatizar leitura via `Gwyddion/pygwy` ou Python puro com **nivelamento mascarado por floco + método de histograma multi-pico (`Yao_2017`) + filtro de artefatos** e cálculo da média ponderada por volume $\langle N \rangle_{Vf}$ (`Backes_2020`), explicitando a faixa de incerteza por adsorvato (`0,4–1,7 nm`) e sinalizando dependência de confirmação Raman/terraços.
   - **Módulo DRX (descritores estruturais com calibração):** ajustar perfis `(001)/(002)` e bandas assimétricas com registro de largura instrumental (`Iwashita_2004`), reportando $d_{002}/d_{001}$, índice de grafitização/redução relativa e $L_c$ com aviso explícito de que $L_c$ é domínio coerente (`Holzwarth_2011`).
2. **Introduzir ML apenas de forma incremental, interpretável e condicionada à disponibilidade de dados reais da UFCA com *ground truth*:**
   - Comparar **sempre** contra *baselines* clássicos (`Otsu`/entropia/histograma/RF/SVM/CNB, na linha comprovada por `Greasley_2023`), utilizando obrigatoriamente **particionamento agrupado por amostra/síntese (*sample/batch-level split*)**, quantificação simples de incerteza/rejeição de baixa confiança e **sem** misturar domínios incompatíveis (como `QUAM-AFM`).
3. **Integração multimodal em nível de relatório estatístico de lote (DRX + MEV + AFM + Raman auxiliar):** gerar um painel unificado de consistência físico-estatística por amostra — onde ninguém precisa inventar inferências que a física não garante, entregando à UFCA/PPGCEM uma ferramenta aberta, reproduzível, auditável e cientificamente irrefutável.
