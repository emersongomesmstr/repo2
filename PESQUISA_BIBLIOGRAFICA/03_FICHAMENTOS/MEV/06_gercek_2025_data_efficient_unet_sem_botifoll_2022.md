# Fichamento 06 — Gerçek et al. (2025) & Trabalhos Correlatos de Segmentação Profunda em MEV: Botifoll et al. (2022), Azimi et al. (2018) e Wang/Pan et al. (2026)

> **Status de Leitura e Verificação (Documento Integrado de 4 Fontes):**
> 1. **Gerçek et al. (2025):** **Texto completo lido integralmente** em `_scratch/textos_extraidos/Gercek_2025_Data_Efficient_U-Net_Segmentation_SEM_Microstructures.md`. **Aviso de revisão por pares:** trata-se de **preprint** (`arXiv:2511.11485v1`) apresentado no *39th NeurIPS 2025 Workshop: Machine Learning and the Physical Sciences*, **ainda não publicado em periódico revisado por pares**, embora o dataset e os pesos estejam publicados com DOI próprio no repositório RODARE (`10.14278/rodare.4123`).
> 2. **Botifoll, Pinto-Huguet & Arbiol (2022):** **Texto completo lido integralmente** via PDF *Open Access* CC BY 3.0 no repositório institucional da UAB ([`ddd.uab.cat/.../nanhor_a2022m12v7n12p1427.pdf`](https://ddd.uab.cat/pub/artpub/2022/270837/nanhor_a2022m12v7n12p1427.pdf)), publicado em *Nanoscale Horizons* 7(12), 1427–1477 (`10.1039/d2nh00377e`).
> 3. **Azimi et al. (2018):** **Texto completo lido integralmente** em `_scratch/textos_extraidos/Azimi_2018_Advanced_Steel_Microstructural_Classification_DL.md` (*Scientific Reports* 8:2128, `10.1038/s41598-018-20037-5`, Gold OA CC BY 4.0).
> 4. **Wang / Pan et al. (2026) (*PerovSegNet*):** **Texto completo da versão manuscrita aceita/anterior lido** em `_scratch/textos_extraidos/Pan_2026_Automated_Scalable_SEM_Analysis_Perovskite_npj.md` + **metadados, resumo e trechos da versão publicada final verificados** em `_scratch/verified_catalog.json` e Nature (`10.1038/s41524-026-02211-w`). *Nota bibliográfica de rastreabilidade:* o texto extraído em `_scratch` corresponde a uma submissão anterior (*"Preprint submitted to Elsevier"*, autores `Jian Guo Pan, Lin Wang, Xia Cai`, `40` imagens rotuladas base), enquanto o artigo publicado final em *npj Computational Materials* (2026, vol. 12, `10.1038/s41524-026-02211-w`) lista `Lin Wang, Tianxiang Hu, Jianguo Pan, Hao Zhang, Yiqiang Zhan, Xia Cai`, `46` imagens rotuladas expandidas para as mesmas `10.994` imagens e avaliações adicionais interlaboratoriais e *zero-shot*.

---

## 1. Identificação bibliográfica

1. **Gerçek et al. (2025) [Preprint + Dataset RODARE]:**
   - **Título:** Data-efficient U-Net for Segmentation of Carbide Microstructures in SEM Images of Steel Alloys
   - **Autores:** Alinda Ezgi Gerçek, Till Korten, Paul Chekhonin, Maleeha Hassan, Peter Steinbach
   - **Ano:** 2025 (NeurIPS 2025 Workshop on Machine Learning and the Physical Sciences)
   - **Repositório / Identificadores:** `arXiv:2511.11485v1` (`10.48550/arxiv.2511.11485`); Dataset/modelos no RODARE: `10.14278/rodare.4123` (`https://rodare.hzdr.de/record/4124`); Código: `https://github.com/thawn/carde/`
2. **Botifoll, Pinto-Huguet & Arbiol (2022):**
   - **Título:** Machine learning in electron microscopy for advanced nanocharacterization: current developments, available tools and future outlook
   - **Autores:** Marc Botifoll, Ivan Pinto-Huguet, Jordi Arbiol
   - **Ano:** 2022 | **Periódico:** *Nanoscale Horizons*, Vol. 7, No. 12, pp. 1427–1477
   - **DOI:** `10.1039/d2nh00377e` | **Link:** [https://doi.org/10.1039/d2nh00377e](https://doi.org/10.1039/d2nh00377e) (152 citações em `verified_catalog.json`)
3. **Azimi et al. (2018):**
   - **Título:** Advanced Steel Microstructural Classification by Deep Learning Methods
   - **Autores:** Seyed Majid Azimi, Dominik Britz, Michael Engstler, Mario Fritz, Frank Mücklich
   - **Ano:** 2018 | **Periódico:** *Scientific Reports*, Vol. 8, `2128`
   - **DOI:** `10.1038/s41598-018-20037-5` | **Link:** [https://doi.org/10.1038/s41598-018-20037-5](https://doi.org/10.1038/s41598-018-20037-5) (517 citações em `verified_catalog.json`)
4. **Wang / Pan et al. (2026):**
   - **Título:** Automated and Scalable SEM Image Analysis of Perovskite Solar Cell Materials via a Deep Segmentation Framework
   - **Autores (publicação final *npj*):** Lin Wang, Tianxiang Hu, Jianguo Pan, Hao Zhang, Yiqiang Zhan, Xia Cai *(versão manuscrita extraída: Jian Guo Pan, Lin Wang, Xia Cai)*
   - **Ano:** 2026 | **Periódico:** *npj Computational Materials*, Vol. 12, No. 1
   - **DOI:** `10.1038/s41524-026-02211-w` | **Link:** [https://doi.org/10.1038/s41524-026-02211-w](https://doi.org/10.1038/s41524-026-02211-w) | Código: `https://github.com/wlyyj/PerovSegNet/tree/master`

---

## 2. Problema investigado

- **[Extraído dos artigos]:**
  - **Gerçek et al. (2025):** Em aços de vasos de pressão de reatores (RPV), carbonetos controlam escoamento e nucleação de trincas (especialmente acima de `~0,5 µm` ECD), mas no MEV os níveis de cinza de carbonetos e matriz ferrítica **sobrepõem-se** e bordas ficam borradas, fazendo pipelines clássicos (limiarização + morfologia) fragmentarem ou gerarem falsos positivos; simultaneamente, anotar pixel a pixel manualmente milhares de carbonetos é inviável. *Pergunta:* qual a menor quantidade de imagens MEV anotadas capaz de treinar uma `U-Net` confiável, com quantificação de incerteza calibrada e superior ao processamento clássico?
  - **Azimi et al. (2018):** Como classificar automaticamente subestruturas complexas e multiescala de segunda fase em aços (martensita, martensita revenida, bainita, perlita sobre ferrita) em micrografias MEV e ópticas (LOM), superando descritores morfológicos manuais (~48,89% de acurácia) e evitando a perda de textura causada pelo redimensionamento (*warping*) exigido por CNNs baseadas em objetos recortados?
  - **Wang / Pan et al. (2026):** Como segmentar e quantificar automaticamente em alta escala fases coexistentes em filmes finos de perovskita no MEV (perovskita, `PbI2` residual e defeitos pequenos de baixo contraste) com invariância de magnificação, baixa sobrecarga computacional e ligação direta entre descritores geométricos e eficiência fotovoltaica (PCE)?
  - **Botifoll et al. (2022):** Como sistematizar os gargalos atuais de análise, aquisição e anotação em microscopia eletrônica (com foco central em `(S)TEM`/espectroscopia e mapeamento explícito de ferramentas/bases para MEV e transferência interdisciplinar), destacando como incorporar restrições físicas e reduzir a dependência de rotulagem humana cara?

---

## 3. Fundamentação

- **[Extraído dos artigos]:**
  - **Fusão multicanal de detectores MEV (Gerçek et al., 2025):** combina simultaneamente **dois canais físicos distintos adquiridos em paralelo** no mesmo campo de visão — detector lateral `SE2` (sensível à topografia) e detector em coluna `InLens` (sensível a contraste de material/potencial) — como imagem de entrada de `2` canais na `U-Net`, explorando o contraste complementar que um limiar único perde.
  - **Arquitetura Encoder–Decoder U-Net + Calibração Pós-Hoc (Gerçek et al., 2025):** conexões de salto (*skip connections*) combinadas à função de perda *Dice Loss* (`L_Dice`). Para evitar previsões sobreconfiantes em bases pequenas, aplica **Temperature Scaling** (Guo et al., 2017): divide os *logits* `z_i` por um escalar `T` antes da sigmoide (`y_hat_i = sigma(z_i / T)`), otimizando `T` por minimização da verossimilhança negativa (NLL) na validação, e compara com *Mean-Variance Estimation* (MVE, Kendall & Gal, 2017).
  - **Segmentação pixel a pixel + Votação por Objeto (`MVFCNN`, Azimi et al., 2018):** substitui a classificação direta de objetos recortados/deformados (*warping* para `224×224 px`, que destrói o espaçamento físico de lamelas/agulhas da textura!) por **FCNN** (Long et al., 2015: `FCN-32s` -> `FCN-16s` -> `FCN-8s` sobre `VGG16` pré-treinada) aplicada em *patches* grandes de resolução nativa (`1000×1000 px`), seguida de *stitching* e **votação majoritária (*max-voting*)** dos pixels internos a cada objeto.
  - **Segmentação de instâncias multiescala em tempo real (`PerovSegNet`, Wang/Pan et al., 2026):** estende `YOLOv8x-seg` substituindo blocos `C2f` e *pooling* estático por dois módulos: (i) **ASDCB** (*Adaptive Shuffle Dilated Convolution Block*, 4 ramos paralelos — convolução padrão, dilatada, atenção *Squeeze-and-Excitation* e *depthwise separable* + *channel shuffle* + `ConvFFN` com `DropPath`) para campo receptivo adaptativo; e (ii) **SAD** (*Separable Adaptive Downsampling*, via dupla *depthwise* `stride=2` e `stride=1` seguida de `AdaptiveMaxPool` + `AdaptiveAvgPool`), evitando *aliasing* e preservando texturas finas de borda/defeito.
  - **ML Fisicamente Informado (*Physics-Aware ML*), Transferência entre Microscopias e *Compressed Sensing* (Botifoll et al., 2022):** propõe injetar condições experimentais (tensão, dose, defoco) como canais adicionais ou restrições estruturais (como `rVAEs` invariantes à rotação e redes em grafos `GNNs`), aponta que rotinas de segmentação de materiais 2D em microscopia óptica (grafeno, `MoS2`) transferem-se para **MEV e STEM de baixa magnificação** (Seção 4.1.2), e enfatiza simulações programáticas e formatos abertos (HDF5/USID) para evitar rotulagem manual massiva.

---

## 4. Metodologia

- **[Extraído dos artigos]:**
  - **Gerçek et al. (2025):**
    - *Dados (`RODARE 10.14278/rodare.4123`):* **13 pares** `SE2 + InLens` (`2048×1404 px`) de três aços RPV: `JFL` em `Zeiss NVision 40` (`14,3 µm` de largura) e `ANP-10` em `Zeiss Ultra 55` (`11,5 µm` de largura), além de `1` imagem completa do aço distinto `ANP-3` reservada como teste de generalização em sessão separada. Máscaras geradas por fusão 0,5 + thresholding inicial + correção manual (~`20 h` totais). `12` imagens divididas em `1.920` *tiles* sem sobreposição de `128×128 px` (`80%` treino [`10` imagens], `10%` val [`192` tiles], `10%` teste [`192` tiles]), com *augmentation* (rotações, flips, ruído e desfoque gaussianos).
    - *Baseline clássico (`SimpleITK`):* mistura `SE2/InLens` razão `0,5` -> desfoque Gaussiano (`sigma = 1,0 px`) -> *top-hat* (`r = 30 px`) -> limiarização de **Otsu** -> preenchimento de buracos internos e remoção de objetos `< 3 px`.
    - *U-Net & Treino:* encoder de `3` blocos (`128` *features* iniciais otimizadas por `Optuna`), `30,7 M` parâmetros, Adam (`lr = 0,0002`, patience `14` épocas, batch `32`), `~30 h` (`~12 kWh`) em `1× NVIDIA A100` incluindo busca Optuna. Teste estatístico de Wilcoxon pareado (`alpha = 0,001`). Calibração pós-hoc via L-BFGS (convergência em 7 passos para `T = 1,87117`).
  - **Azimi et al. (2018):**
    - *Dados:* **21 pares** registrados LOM + MEV (`~7000×8000 px`; `11` imagens de treino [`2.831` objetos], `10` de teste [`2.262` objetos]) em matriz ferrítica com `4` classes (martensita `11`, revenida `2`, bainita `4`, perlita `4`).
    - *Modelos comparados (Caffe / GPU K40m):* (a) *Object-based CNN* (máscara LOM binária para localizar -> recorte -> *warp* `224×224 px` -> `CIFARNet` do zero, `VGG19-DeCAF+SVM-RBF` e `VGG16` *fine-tuned*); (b) `MVFCNN` (`FCN-32s -> 16s -> 8s` em patches `1000×1000 px`, `batch=1`, *stride* ajustado por classe para balanceamento + rotações `90/180/270°`, `lr = 10^-10` a `3×10^-12`, `~4,5` dias de treino, `~600 ms` por patch na inferência).
  - **Wang / Pan et al. (2026):**
    - *Dados (`PerovData`):* `40` imagens rotuladas manualmente via `LabelMe` no manuscrito extraído (`46` imagens na versão publicada *npj*), particionadas `8:1:1` **antes** da ampliação para `10.994` imagens (`640×640` com *padding* adaptativo), checando separabilidade de classes por `UMAP`.
    - *Treino & Comparação (PyTorch 2.2.2, A100 80GB):* `300` épocas (`batch 4`, `AdamW`, `lr=0,01`, *warm-up* `3` épocas); comparado contra `YOLOv8x-seg` (ablação de SAD e ASDCB) e `Cascade Mask R-CNN (×101)`, `Mask R-CNN (Swin-T / ×101)`, `Cascade InternImage-XL` (via MMDet, `120` épocas). Pós-processamento extrai área (`µm²`), contagem e complexidade (perímetro/área), testando invariância em imagens MEV publicadas (`200 nm` a `2 µm`) e correlação de Pearson com PCE (~`25` artigos de 2022–2025).
  - **Botifoll et al. (2022):**
    - Revisão bibliográfica e guia prático em 3 eixos: (i) avanços de ML em imagem `(S)TEM`/`4D-STEM`/tomografia/`in situ` e espectroscopia `EELS`/`EDX`; (ii) ferramentas práticas e bases abertas (Tabela 1: simuladores como `abTEM`, `Dr. Probe`, `NIST DTSA-II`; Tabela 2: bases **CNR-IOM SEM `[22.000]`**, **Zelinsky SEM NPs `[1.000]`**, **DeCost–Holm SEM `[2.048]`**; Tabela 3: `PyTorch`, `TensorFlow`, `scikit-image`, `OpenCV`, `HyperSpy`, `Pycroscopy/AtomAI`, `ZeroCostDL4Mic`); (iii) fertilização cruzada (Cryo-EM, microscopia óptica 2D/aços, radiômica, SPM, astronomia/física de partículas, robótica/RL).

---

## 5. Resultados

- **[Extraído dos artigos]:**
  - **Gerçek et al. (2025) — Eficiência de dados com apenas 10 imagens:** no conjunto de teste (`192` tiles), a `U-Net` atingiu coeficiente Dice-Sørensen mediano de **`0,98` (IQR `0,964–0,991`)**, superando significativamente o baseline clássico `SimpleITK + Otsu` com mediana **`0,85` (IQR `0,522–0,919`; Wilcoxon `p < 0,001`)**. Na imagem inédita de outro aço em sessão distinta (`ANP-3`), manteve **`0,94`** vs. `0,90`. A calibração por *Temperature Scaling* (`T = 1,87117`) aproximou melhor as probabilidades da diagonal de calibração perfeita que MVE e que o modelo bruto, exibindo menor confiança exatamente nos pixels errados de borda.
  - **Azimi et al. (2018) — Preservação de textura e superioridade do MEV sobre LOM:**
    - Acurácia de classificação de objetos em MEV: `Pauly et al.` (manual+SVM) = **`48,89%`**; `CIFARNet` (objeto) = **`57,03%`**; `VGG19-DeCAF+SVM` = **`64,84%`**; `VGG16` *fine-tuned* = **`66,50%`**; **`MVFCNN` pixel-wise + max-voting = `93,94%`** (`95,23%` excluindo `48` objetos não segmentados, classificando corretamente `10/10` micrografias globais!).
    - Ablação crítica da `MVFCNN`: do zero sem balanceamento = **`55,50%`** -> *fine-tuning* = **`87,98%`** (+`32,48 p.p.`) -> balanceado = **`90,97%`** -> balanceado + aumentado = **`93,94%`** (`pixel acc. 93,92%`, `mean IU 67,84%`).
    - Comparação MEV vs. LOM: `MVFCNN` caiu de **`93,94%` (MEV)** para **`70,14%` (LOM)** devido à menor resolução óptica, artefatos de *stitching* e riscos.
  - **Wang / Pan et al. (2026) — Segmentação de instâncias multiescala (`PerovSegNet`):** atingiu **`mAP@0.5 = 87,25%`** (`87,3%` na Tab. 3) e **`mAP@0.5:0.95 = 79,96%`** (Precision `98,11%`, Recall `76,30%`), superando `YOLOv8x-seg` (`83,17%`, `+4,08%`) e concorrentes pesados como `Cascade InternImage-XL` (`81,9%`, `387 M` params) e `Mask R-CNN Swin-T` (`82,5%`), usando apenas **`79,10 M` parâmetros (`-24,43%`)** e **`265,4 GFLOPs` (`-25,22%`)**. O maior ganho ocorreu na classe mais difícil (**defeitos pequenos de baixo contraste**): acurácia subiu de **`33%` -> `64%`** (perovskita `82%->88%`, `PbI2` `84%->88%`). Em imagens de `200 nm` a `2 µm`, manteve acurácia `>75%` em regiões de sobreposição, e a correlação com literatura indicou `r = 0,78` (área de perovskita vs. PCE) e `r = -0,32` (contagem de defeitos vs. PCE).
  - **Botifoll et al. (2022):** consolida evidência de que a transferência *ImageNet* funciona até para nanomateriais de carbono em HRTEM (`VGG-16`), mostra que filtros aprendidos em `U-Net` convergem a combinações de filtros clássicos (Laplaciano/Gaussiano), documenta ganhos de **100×–300×** em velocidade e super-resolução com aprendizado fisicamente guiado, e mostra que supervisão esparsa em **`0,31%` dos pixels** pode equiparar-se a autoencoders completos (Kalinin et al., 2021).

---

## 6. Limitações

- **[Reconhecidas nos respectivos artigos]:**
  - **Gerçek et al. (2025):** permanece **preprint**; validação feita em poucos espécimes/lotes (`13` imagens totais); dependência de rótulos totalmente supervisionados (`~20 h`) **gerados inicialmente por thresholding**, o que introduziu **ruído aleatório intrínseco nas bordas** e gerou subconfiança (`0,1–0,5`) e sobreconfiança (`0,5–0,9`) mesmo após *Temperature Scaling* (Apêndice A.1). Além disso, exige **dois canais alinhados (`SE2 + InLens`)** e o treino/busca Optuna consumiu **`~30 h` / `12 kWh` em uma A100**.
  - **Azimi et al. (2018):** dependeu de **imagens LOM registradas sobre exatamente a mesma área do MEV** apenas para gerar a máscara binária localizadora de objetos (dependência multimodal cara!); classe minoritária e de menor tamanho (`bainita`) teve acurácia por pixel de apenas **`37,32%`**, e amostra de processo distinto (bainita transformada ausente no treino) degradou fortemente a predição; exige `1000×1000 px` em *sliding window* (com `<100×100 px`, cai o desempenho).
  - **Wang / Pan et al. (2026):** os autores reconhecem explicitamente (Seção 5) que **correlações descritor–PCE são meramente observacionais e não implicam causalidade**; erros de segmentação e desbalanceamento (sobretudo defeitos) propagam-se às métricas geométricas; **condições de aquisição MEV (tensão, magnificação, calibração)** afetam resultados quantitativos; ausência de quantificação de incerteza e custo ainda alto para *in situ / inline*; ademais, nossa comparação entre o manuscrito extraído (`40` imagens) e a versão *npj* (`46` imagens) evidencia evolução metodológica entre versões.
  - **Botifoll et al. (2022):** revisão aponta **ausência de benchmarks padronizados** em EM para ciência dos materiais (diferente de biologia celular), escassez de literatura sobre **MEV** comparada a `(S)TEM`, risco de *black box* sem restrições físicas e vulnerabilidade à falta de metadados padronizados (ex.: `USID/HDF5`).
- **[Críticas adicionais — Agente C]:**
  - **Nenhum dos quatro trabalhos testou diretamente flocos dispersos de grafeno/GO no MEV:** carbonetos em aço (Gerçek), fases em aço (Azimi) e grãos densos de perovskita (Wang/Pan) possuem contraste topográfico/composicional e densidades muito distintas de folhas monoatômicas de grafeno em `SiO2/Si`, onde há transparência eletrônica parcial, bordas dobradas e interferência de carregamento/carbono amorfo.
  - **Risco de vazamento metodológico no *augmentation* se mal aplicado:** em `Wang/Pan`, os autores tiveram o cuidado de dividir `8:1:1` **antes** do *augmentation*; já em `Gerçek`, os `1.920` *tiles* de `12` imagens foram sorteados aleatoriamente (`80/10/10%`), o que significa que *tiles* de treino e teste podem vir da **mesma micrografia original** (embora mitigado pelo teste adicional na imagem separada `ANP-3`!).

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Este bloco de 4 artigos fornece o **roteiro técnico realista** de computação científica/DL para o módulo MEV da dissertação:
  1. **Realismo sobre volume de dados e tempo de anotação (`Gerçek 2025`):** prova que `~10` micrografias MEV de alta resolução (`~20 h` de anotação bem feita, particionadas em *tiles*) já são suficientes para superar significativamente `Top-hat + Otsu` quando a sobreposição de tons de cinza quebra limiares simples — desarmando a objeção de que DL em MEV exige "milhares de imagens originais".
  2. **Lição arquitetural contra *warping* e favorável à resolução nativa (`Azimi 2018`):** adverte contra recortar flocos de grafeno e esticá-los para `224×224 px` (destrói razão de aspecto e escala métrica de rugas/dobras!), favorecendo redes totalmente convolucionais em *tiles* com preservação da escala física em `nm/pixel`, além de comprovar o salto crítico de *transfer learning/fine-tuning* (`+32,48 p.p.`).
  3. **Solução moderna para separação de instâncias + defeitos (`Wang/Pan 2026`):** apresenta uma arquitetura contemporânea baseada em `YOLOv8-seg` capaz de segmentar simultaneamente objetos principais e **defeitos pequenos de baixo contraste** enquanto extrai **área em `µm²`, contagem e razão perímetro/área** — exatamente o tipo de saída tabular requerida para flocos de grafeno, aglomerados e dobras!
  4. **Boas práticas de engenharia científica (`Botifoll 2022`):** fundamenta a escolha do ecossistema aberto (`PyTorch`, `scikit-image`, `OpenCV`, `LabelMe`), a necessidade de **quantificação de incerteza** (como *Temperature Scaling* em Gerçek) para que um software investigativo alerte quando a borda de um floco é duvidosa, e a incorporação de **metadados físicos do MEV** junto à imagem.

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Estruturar um experimento comparativo rigoroso na dissertação confrontando **3 níveis crescentes de complexidade** sobre micrografias MEV de grafeno/GO: (1) pipeline clássico transparente (`Gaussian + Top-hat/rolling-ball + Otsu/Canny` estilo Gerçek baseline / ImageJ); (2) `U-Net` leve com *Temperature Scaling* treinada em ~10–15 micrografias para máscaras e confiança de borda em flocos isolados; e (3) segmentador de instâncias leve (`Mask R-CNN` ou `YOLOv8-seg` estilo PerovSegNet) caso haja sobreposição frequente de flocos.
  - Sempre realizar o *split* treino/validação/teste **por imagem inteira ou sessão de microscópio** (e nunca apenas entre *tiles* da mesma imagem, corrigindo a limitação do teste interno de Gerçek) para medir generalização real entre amostras e dias de aquisição.

---

## 9. Evidências

- **Gerçek et al. (2025):** Fig. 1 (p. 2, fluxo `SE2+InLens -> U-Net`), Seção 2 (`13` pares `2048×1404`, `1920` tiles, `SimpleITK`, `Temperature Scaling` `T=1,87117`), Seção 3 & Figs. 3–4 (Dice `0,98` vs `0,85`, `p < 0,001`; `ANP-3` `0,94` vs `0,90`), Apêndice A.1–A.2 & Figs. 5–6 (`Optuna`, ruído de borda).
- **Botifoll et al. (2022):** Seções 2.1–2.2, Seção 3.1–3.3 & Tabelas 1–3 (pp. 1441–1448: datasets `CNR-IOM`/`DeCost-Holm`/`Zelinsky`, simuladores, bibliotecas `PyTorch`/`OpenCV`/`scikit-image`), Seção 4.1.2 & Fig. 7 (pp. 1449–1450: transferência 2D/óptica -> MEV baixa magnificação), Seção 4.4 (pp. 1455–1456: *physics-aware ML*).
- **Azimi et al. (2018):** Seções *Methods* e *Results* (pp. 4–12), Fig. 3 (pipeline MVFCNN), Tabela 1 (`48,89%` -> `93,94%`), Tabela 2 (ablation *fine-tuning* `+32,48 p.p.`), Tabela 3 (MEV `93,94%` vs LOM `70,14%`), Tabela 4 (matriz de confusão), Tabelas 5–6 (`mean IU 67,84%`; bainita `37,32%`).
- **Wang / Pan et al. (2026):** Seção 2.1–2.2 & Figs. 1–6 (PerovData `10.994` imagens, `UMAP`, módulos `ASDCB` e `SAD`), Tabelas 3–4 (`mAP@0.5 = 87,25%`, `mAP@0.5:0.95 = 79,96%`, `79,10 M` params, `265,4 GFLOPs`), Fig. 7 (defeitos `33% -> 64%`), Seção 5 & Figs. 9–11 (plataforma quantitativa, invariância `200 nm–2 µm`, heatmap PCE `r = 0,78 / -0,32`, limitações observacionais).

---

## 10. Prioridade de estudo

- **Prioridade:** **ALTA (`Gerçek 2025` e `Wang/Pan 2026` para pipeline DL; `Azimi 2018` para justificar pixel-wise vs. warping; `Botifoll 2022` como referência de consulta de ferramentas).**
- **Justificativa:** Para o seminário de 17/11/2026, `Gerçek et al. (2025)` tem apenas 9 páginas e responde objetivamente *"preciso de milhares de imagens MEV para usar U-Net?"* (`10` imagens bem anotadas já vencem `Otsu`), além de trazer calibração de incerteza; `Azimi et al. (2018)` explica por que não deformar objetos; `Wang/Pan et al. (2026)` exemplifica o estado da arte de 2026 em segmentação de instâncias multiescala no MEV com extração geométrica acoplada; e `Botifoll et al. (2022)` serve como mapa enciclopédico de ferramentas abertas, datasets e restrições físicas para a etapa de desenvolvimento na dissertação.
