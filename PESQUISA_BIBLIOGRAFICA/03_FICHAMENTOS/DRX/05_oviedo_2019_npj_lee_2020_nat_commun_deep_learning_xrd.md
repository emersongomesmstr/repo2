# Fichamento 05 — Redes Neurais Convolucionais, Augmentação Informada pela Física e Interpretabilidade em DRX com Dados Limitados ou Sintéticos (Oviedo et al., 2019; Lee et al., 2020; Wang et al., 2020)

> **Status de Leitura e Verificação:** **Texto completo lido integralmente para os três artigos.**
> - **Oviedo et al. (2019):** PDF integral (`ARTIGOS_PDF/Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.pdf`) e texto extraído (`_scratch/textos_extraidos/Oviedo_2019_Fast_Interpretable_Classification_Small_XRD_Datasets.md`).
> - **Lee et al. (2020):** PDF integral (`ARTIGOS_PDF/Lee_2020_Deep_Learning_Phase_Identification_XRD.pdf`) e texto extraído (`_scratch/textos_extraidos/Lee_2020_Deep_Learning_Phase_Identification_XRD.md`).
> - **Wang et al. (2020):** Texto integral extraído (`_scratch/textos_extraidos/Wang_2020_Rapid_Identification_XRD_Patterns_Limited_Data_CNN.md`) e PDF local catalogado.

---

## 1. Identificação bibliográfica

### Artigo 1 — Oviedo et al. (2019)
- **Título:** Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks
- **Autores:** Felipe Oviedo, Zekun Ren, Shijing Sun, Charles M. Settens, Zhe Liu, Noor Titan Putri Hartono, Savitha Ramasamy, Brian L. DeCost, Siyu Isaac Parker Tian, Giuseppe Romano, Aaron Gilad Kusne, Tonio Buonassisi
- **Ano:** 2019 (publicado online em 17 de maio de 2019)
- **Periódico:** *npj Computational Materials*, Volume 5, Número 1, Artigo 60 (9 páginas)
- **DOI:** `10.1038/s41524-019-0196-x`
- **URL oficial:** <https://doi.org/10.1038/s41524-019-0196-x> (PDF Gold OA: <https://www.nature.com/articles/s41524-019-0196-x.pdf>; Repositório de código e dados experimentais: <https://github.com/PV-Lab/AUTO-XRD/>)
- **Citações verificadas (OpenAlex):** 347 (`W2940802411`)

### Artigo 2 — Lee et al. (2020)
- **Título:** A deep-learning technique for phase identification in multiphase inorganic compounds using synthetic XRD powder patterns
- **Autores:** Jin-Woong Lee, Woon Bae Park, Jin Hee Lee, Satendra Pal Singh, Kee-Sun Sohn
- **Ano:** 2020 (publicado em 3 de janeiro de 2020)
- **Periódico:** *Nature Communications*, Volume 11, Número 1, Artigo 86 (11 páginas)
- **DOI:** `10.1038/s41467-019-13749-3`
- **URL oficial:** <https://doi.org/10.1038/s41467-019-13749-3> (PDF Gold OA: <https://www.nature.com/articles/s41467-019-13749-3.pdf>)
- **Citações verificadas (OpenAlex):** 230 (`W2997208716`)

### Artigo 3 — Wang et al. (2020)
- **Título:** Rapid Identification of X-ray Diffraction Patterns Based on Very Limited Data by Interpretable Convolutional Neural Networks
- **Autores:** Hong Wang, Yunchao Xie, Dawei Li, Heng Deng, Yunxin Zhao, Ming Xin, Jian Lin
- **Ano:** 2020
- **Periódico:** *Journal of Chemical Information and Modeling*, Volume 60, Número 4, Páginas 2004–2011
- **DOI:** `10.1021/acs.jcim.0c00020`
- **URL oficial:** <https://doi.org/10.1021/acs.jcim.0c00020> (Green OA arXiv: <https://arxiv.org/pdf/1912.07750>; Código/dados: <https://github.com/javenlin/MOFs>)
- **Citações verificadas (OpenAlex):** 122 (`W3013216111`)

---

## 2. Problema investigado

### Fatos extraídos dos artigos
- **Oviedo et al. (2019):** Na triagem de novos materiais em **filmes finos**, a aquisição em alta resolução (~1 h) e o refinamento Rietveld (~1–2 h) constituem gargalos críticos. Além disso, o refinamento de Rietveld falha ou é restrito quando faltam padrões de referência na base de dados e quando os filmes possuem **orientação preferencial (textura) e deformação (*strain*) desconhecidas**, que fazem os padrões experimentais de filmes finos divergirem substancialmente dos padrões simulados de pó aleatório da ICSD. Como classificar rapidamente dimensionalidade cristalina (0D/2D/3D) e grupo espacial a partir de **conjuntos experimentais muito pequenos** ($\sim 10^2$ amostras) mantendo **interpretabilidade** para o experimentalista?
- **Lee et al. (2020):** Em síntese combinatória de compostos inorgânicos (sistema quaternário $\text{Sr–Li–Al–O}$), amostras reais frequentemente contêm **misturas multifásicas** (até 3 fases). Métodos convencionais baseados em regras sofrem com sobreposição de picos, enquanto CNNs anteriores (como Park et al., 2017) só classificavam simetria de fase única. Como treinar uma CNN apenas com **padrões sintéticos** para identificar múltiplas fases simultaneamente e estimar grosseiramente suas frações relativas em amostras experimentais reais?
- **Wang et al. (2020):** Enquanto trabalhos anteriores agrupavam padrões em poucas classes de simetria (7 sistemas cristalinos ou grupos espaciais), a **identificação um-para-um (*one-to-one*)** de compostos individuais (aqui, **1.012 Metal-Organic Frameworks — MOFs**) a partir de padrões teóricos e **dados experimentais extremamente escassos** permanecia em aberto, além da necessidade de abrir a "caixa-preta" da CNN por mapas de ativação de classe (CAMs) e redução dimensional (NCA).

### Análise crítica — Agente B
- Esses três trabalhos representam o trio seminal (2019–2020) que inaugurou o paradigma moderno de *Deep Learning* aplicado a DRX 1D, respondendo a três regimes de dados distintos e complementares: (i) **filmes finos texturizados e pequenos datasets** (Oviedo et al., 2019), (ii) **misturas multifásicas via explosão combinatória sintética** (Lee et al., 2020) e (iii) **identificação um-para-um de >1000 compostos com injeção de ruído experimental real** (Wang et al., 2020). Essa comparação direta é decisiva para avaliar o que é transferível (e o que não é) para grafeno e derivados lamelares.

---

## 3. Fundamentação

### Fatos extraídos dos artigos
- **Oviedo et al. (2019):**
  - *Física de filmes finos vs. pó aleatório:* Em pós ideais, orientações aleatórias produzem intensidades relativas proporcionais ao fator de estrutura e multiplicidade. Em filmes finos (processamento em solução ou deposição a vapor), a **orientação preferencial** induzida pelo substrato e crescimento amplia periodicamente picos de planos preferenciais e reduz ou **elimina** reflexões não preferenciais; simultaneamente, substituições químicas e **deformação epitaxial/residual** deslocam os picos ao longo do eixo $2\theta$.
  - *Descritores-alvo:* **Dimensionalidade cristalina** (0D, 2D, 3D — ligada ao transporte de portadores) e **grupo espacial** (entre os 230 grupos cristalográficos; observam explicitamente que a compressão 3D $\to$ 1D no DRX pode tornar certos grupos de baixa simetria ambíguos).
  - *Interpretabilidade:* Uso de camada **Global Average Pooling (GAP)** na *all convolutional neural network* (`a-CNN`), permitindo projetar os pesos $w_k^C$ da camada final sobre os mapas de ativação espacial $f_k(x)$ para gerar **Class Activation Maps (CAMs)** e **Average CAMs** por classe ($\overline{M}_C(x)$).
- **Lee et al. (2020):**
  - Trata o difratograma 1D como uma "imagem unidimensional" ($4501 \times 1$) submetida a CNNs sem engenharia manual de características (*handcrafted features*), substituindo a ativação *softmax* (mutuamente exclusiva) por um sistema de **vetor *three-hot* com ativação sigmoide** e entropia cruzada binária para permitir predição multi-rótulo de até 3 fases simultâneas a partir de $38$ nós de saída (ou $114$, $152$, $190$ nós para quantificação discreta em 3, 4 e 5 faixas).
  - Define pragmaticamente **"fração de fase"** como **fração de altura** (*height fraction* — razão entre as alturas máximas dos picos de cada fase), reconhecendo explicitamente que ela **não equivale à fração mássica nem molar** sem calibração adicional ou Rietveld.
- **Wang et al. (2020):**
  - Combina extração de características no domínio espectral/frequência (**FFT / iFFT** para filtragem de ruído branco de alta frequência acima de $200\ \text{Hz}$), aumento de dados pela recombinação de **picos teóricos dominantes com ruído real extraído da linha de base experimental**, visualização em espaço latente por **Neighborhood Components Analysis (NCA)** e explicabilidade via **CAMs** da 14ª camada.

### Análise crítica — Agente B
- Do ponto de vista físico de DRX em materiais bidimensionais e grafeno, **Oviedo et al. (2019)** acertam em um ponto crítico ignorado por Lee et al. (2020): **textura (escalonamento e eliminação de picos)** é regra, não exceção, em filmes depositados sobre substratos! Em filmes de grafeno/GO/rGO orientados paralelamente ao substrato (ex.: *drop-cast* ou membranas filtradas), as reflexões basais `(00l)` podem ser amplificadas enquanto reflexões `(hkl)` oblíquas desaparecem — exatamente o fenômeno modelado pelas transformações $\Phi^1_{S,c}$ e $\Phi^2_S$ de Oviedo et al. (2019). Por outro lado, nenhum dos três artigos modela **desordem turboestrática, alargamento assimétrico de bandas 2D `(hk)` ou ausência de periodicidade 3D** (como ocorre em grafeno mono/poucas camadas), pois todos assumem redes cristalinas tridimensionais periódicas indexadas na ICSD ou CCDC.

---

## 4. Metodologia

### Fatos extraídos dos artigos
- **Oviedo et al. (2019):**
  - *Dados:* **164 padrões simulados** da ICSD (haletos de Pb e materiais inspirados em perovskitas sem Pb; Panalytical HighScore v4.7, método Rietveld Hill–Howard com grãos aleatórios) + **115 padrões experimentais únicos** de filmes finos sintetizados (75 rotulados para 3 dimensionalidades: 0D, 2D, 3D; 88 rotulados para 7 grupos espaciais: $Pm\bar{3}m$, $I4/mcm$, $Fm\bar{3}m$, $P\bar{3}m1$, $Pc$, $P2_1/a$, $P6_3/mmc$). Aquisição: Rigaku SmartLab em feixe paralelo simétrico, $2\theta = 5^\circ\text{–}60^\circ$, passo $0{,}04^\circ$.
  - *Pré-processamento:* Subtração de linha de base e suavização por filtro **Savitzky–Golay**.
  - *Augmentação informada pela física (Eqs. 1–3):* (1) escalonamento periódico aleatório de picos ($\Phi^1_{S,c}$), (2) eliminação periódica aleatória de picos ($\Phi^2_S$) e (3) deslocamento angular aleatório $\varepsilon$ ($\Phi^3_\varepsilon = f(2\theta - \varepsilon)$), gerando 2.000 espectros simulados aumentados e 2.000 experimentais aumentados.
  - *Modelos testados:* Naive Bayes, k-NN, k-NN com **Dynamic Time Warping (DTW)**, Regressão Logística, Random Forest, Decision Tree, SVM, Gradient Boosting, Rede Neural Densa e **a-CNN** (entrada $1200 \times 1$; 3 camadas `Conv1D` com 32 filtros, kernels/strides 8, 5, 3, ReLU, sem *max pooling* e sem camadas densas intermediárias, + GAP + Softmax; Keras/TensorFlow, Adam, *batch* 128, *early stopping*).
  - *Protocolos de avaliação (5-fold CV):* Caso 1 (só simulado), Caso 2 (treino simulado $\to$ teste experimental), Caso 3 (100% simulado + 80% experimental $\to$ teste 20% experimental), além de análise de sensibilidade ao tamanho aumentado e ao passo angular ($0{,}04^\circ$ a $0{,}40^\circ$).
- **Lee et al. (2020):**
  - *Dados sintéticos:* 170 entradas da ICSD no espaço $\text{Sr–Li–Al–O}$ agrupadas em **38 classes únicas** (duplicatas/variantes com pequenas diferenças de parâmetro de rede mantidas dentro de cada classe, ex.: 74 variantes de $\text{Al}_2\text{O}_3$). Simulação com parâmetros de perfil pseudo-Voigt/Caglioti aleatórios ($u,v,w,\eta,x$), polinômio de fundo de 6ª ordem e ruído branco (orientação preferencial e efeito de tamanho **não** incluídos). Mistura combinatória de 1, 2 ou 3 fases ($_{38}C_3 \times 21 + _{38}C_2 \times 9 + _{38}C_1 = 183{.}521$ misturas distintas), gerando 3 conjuntos: `Dataset_800k_org` (800.942 espectros: 600.942 treino, 100.000 validação, 100.000 teste), `Dataset_800k_rand` (800.942 com frações aleatórias) e `Dataset_180k_rand` (183.521 sem repetição).
  - *Dados experimentais de teste:* **100 misturas reais** preparadas em laboratório (50 de $\text{Li}_2\text{O–SrO–Al}_2\text{O}_3$ e 50 de $\text{SrAl}_2\text{O}_4\text{–SrO–Al}_2\text{O}_3$), além de testes sintéticos com intrusos externos ($\text{BaO}$, $\text{CaO}$).
  - *Arquiteturas:* CNNs 1D (`CNN_2`, `CNN_3` com *pooling/stride* não convencional de redução rápida; e `CNN_2F`–`CNN_6F`, `CNN_3I`/`CNN_6I` tipo Inception para frações em 3, 4 e 5 níveis), treinadas por 2 épocas (identificação) ou 10 épocas (fração), Adam, comparadas a k-NN, SVM e Random Forest.
- **Wang et al. (2020):**
  - *Dados:* Biblioteca teórica do CCDC convertida em padrões de DRX para $2\theta = 5^\circ\text{–}50^\circ$ (descrita como **1.012 MOFs** na classe de saída e nos testes; o texto também menciona 832/823 nas seções sobre subconjuntos da biblioteca). Augmentação total de **72.864 espectros** (divisão 4:1: **58.292 treino** e **14.572 validação**), extraindo os **400 maiores pontos dos picos teóricos** e concatenando com **ruído de linha de base real extraído e embaralhado** dos espectros experimentais (após remoção dos picos principais).
  - *Teste experimental e filtragem:* Coleta em Bruker D8 Discover ($\text{Cu } K\alpha$, $\lambda = 0{,}15406\ \text{nm}$) de **24 espectros** de 8 tipos de MOFs (com referência a 30 amostras *hold-out* na avaliação Top-k). Quando o valor médio do ruído branco acima de $200\ \text{Hz}$ no espectro FFT supera $1$, aplica-se **iFFT nos primeiros $200\ \text{Hz}$** para redução de ruído antes da CNN.
  - *Arquitetura e comparação:* CNN inspirada em LeNet5/VGG16 (4 camadas `Conv1D` com 6, 16, 32, 64 filtros de $5\times 1$, ReLU, *max pooling* 2 com *stride* 2, *dropout* 0,2, *flatten* + 3 camadas densas de 120, 84, 1.012; Adam, entropia cruzada categórica, *early stopping* em 40 épocas; Keras/TensorFlow) comparada a NB, KNN, Regressão Logística, RF e SVM (Scikit-Learn).

---

## 5. Resultados

### Fatos extraídos dos artigos
- **Oviedo et al. (2019) *(Tabela 1, Figs. 3–5)*:**
  - No **Caso 3** (simulados + 80% experimentais no treino, 5-fold CV), a **a-CNN** superou todos os 9 métodos concorrentes com acurácia média de **92,9%** para dimensionalidade ($F_1$ micro $= 0{,}929$; $F_1$ macro $= 0{,}859$) e **89,3%** para grupo espacial ($F_1$ micro $= 0{,}893$; $F_1$ macro $= 0{,}714$), superando DNN densa (92,1%/84,1%), k-NN+DTW (86,6%/80,1%), SVM (88,1%/78,5%) e RF (83,3%/82,1%).
  - No **Caso 2** (treino exclusivamente simulado $\to$ teste experimental), a acurácia caiu para **83,7% / 80,2%** na a-CNN, confirmando a importância de incluir dados experimentais aumentados no treinamento.
  - A augmentação informada pela física elevou a acurácia em até **+23% (dimensionalidade)** e **+19% (grupo espacial)** frente à ausência de augmentação (e $>12\%$ absolutos frente à augmentação tradicional só com ruído na Tabela S6), atingindo platô crítico em torno de **~700 espectros aumentados**.
  - **Degradação angular (*data coarsening*, Fig. 4):** passos de $2\theta$ até **$0{,}16^\circ$** mantiveram acurácia $>85\%$, permitindo reduzir o tempo de aquisição em **75%** ($<5{,}5\ \text{min}$ por amostra).
  - **Average CAMs (Fig. 5):** revelaram três causas-raiz de erro: (1) mistura de fases, (2) escassez de exemplos por classe ($<5$ padrões) e (3) picos ausentes ou em número insuficiente.
- **Lee et al. (2020) *(Tabelas 1 e 2, Fig. 1–2)*:**
  - **Identificação de fases:** `CNN_3` treinada com `Dataset_800k_org` obteve **100%** no teste simulado (100.000 padrões), **100%** nas 50 amostras reais $\text{Li}_2\text{O–SrO–Al}_2\text{O}_3$ e **98,67%** nas 50 amostras $\text{SrAl}_2\text{O}_4\text{–SrO–Al}_2\text{O}_3$ (a investigação por Rietveld em X'Pert/FullProf revelou que a fase "errada" $\text{Sr}_4\text{Al}_{14}\text{O}_{25}$ era na verdade uma **impureza real a 15% em peso** no pó comercial da Nemoto Co. Ltd., levando à conclusão de ~100% de acerto real em menos de 1 segundo vs. horas de um especialista). Resultados similares foram confirmados com `Dataset_800k_rand` (removendo risco de vazamento por composições fixas). Em `Dataset_180k_rand`, RF atingiu 87,63% no simulado (mas deteriorou no real), enquanto KNN e SVM falharam no espaço de 9.177 combinações em 4.501 dimensões.
  - **Quantificação de frações:** regressão contínua falhou (MSE $\ge 0{,}01$); discretizando em **3 níveis** ($0\text{–}0{,}33$; $0{,}33\text{–}0{,}66$; $0{,}66\text{–}1$), `CNN_5F` atingiu **86,00%** no experimental $\text{Li}_2\text{O–SrO–Al}_2\text{O}_3$ (`CNN_6F` teve 98,13% no simulado e 82,67% no experimental). Em **5 níveis**, o desempenho no experimental **deteriorou significativamente**.
  - **Detecção de novas fases:** o valor mínimo da função de custo atuou como índice de novidade ($10^{-6}$ quando todas as fases estão na biblioteca vs. $10^{-3}\text{–}10^{-1}$ na presença dos intrusos $\text{BaO}$ ou $\text{CaO}$).
- **Wang et al. (2020) *(Figs. 3–5)*:**
  - **Identificação um-para-um (1.012 MOFs):** A CNN alcançou **56,7% (Top-1)**, **76,7% (Top-2)**, **90,0% (Top-3)**, **93,3% (Top-4)** e **96,7% (Top-5)** — enquanto todos os 5 classificadores clássicos (NB, KNN, LR, RF, SVM) ficaram **abaixo de 50%** e perderam precisão drasticamente ao escalar a biblioteca de 189 para 1.012 MOFs (a CNN manteve 96,7% no Top-5).
  - **Interpretabilidade:** O mapa **NCA (Fig. 4)** agrupou amostras experimentais do mesmo MOF (com sobreposição apenas entre estruturas muito semelhantes) e os **CAMs da 14ª camada (Fig. 5)** concentraram-se sobre os picos principais mesmo quando razões de intensidade variaram severamente por preparação (ex.: razão `(220)/(222)` de $0{,}82$ a $0{,}45$ em MOF-199 e `(200)/(220)` de $0{,}29$ a $2{,}40$ em MOF-5).
  - **Caso de falha documentado:** ZIF-9 M1 não foi identificado devido à **baixa cristalinidade** e **alto ruído**, reduzindo o CAM a apenas um único pico dominante.

---

## 6. Limitações

### Fatos extraídos dos artigos e análise crítica — Agente B
1. **Explosão combinatória (Lee et al., 2020):** Reconhecida pelos autores — enumerar combinações de misturas exige ~1,8 milhão de padrões para apenas 38 classes em um espaço quaternário restrito ($\text{Sr–Li–Al–O}$), tornando a abordagem inviável para bibliotecas amplas ou sistemas de alta entropia.
2. **Desconexão simulação $\to$ real e ignorância de textura/tamanho (Lee et al., 2020):** A simulação omitiu orientação preferencial e efeito de tamanho de partícula; ademais, as misturas "reais" foram preparadas por mistura física simples de pós puros, sem defeitos de síntese nem deslocamentos severos de rede, e a quantificação em 5 níveis falhou nos dados reais.
3. **Top-1 ainda moderado e dependência de qualidade cristalina (Wang et al., 2020):** Embora o Top-5 atinja 96,7%, a acurácia **Top-1 é de 56,7%** e o conjunto de teste experimental é muito pequeno (24–30 espectros de 8 MOFs), falhando em amostras de baixa cristalinidade/alto ruído (ZIF-9 M1). Além disso, se a biblioteca de ruído experimental provier de um único difratômetro/geometria, pode ocorrer sobreajuste às características desse equipamento.
4. **Espaço de rótulos fechado e ausência de desordem não cristalina (todos os três):** Nenhum desses modelos identifica materiais fora do conjunto treinado (no máximo Lee et al. emitem um índice de anomalia), e **nenhum trata perfis difusos, empilhamento turboestrático ou picos largos de poucas camadas** característicos de grafeno, GO e rGO.

---

## 7. Contribuição para a dissertação

- **Análise — Agente B:**
  1. **Estratégias validadas para datasets pequenos em Ciência dos Materiais:** Oviedo et al. (2019) e Wang et al. (2020) fornecem duas receitas complementares diretamente aplicáveis a contextos de poucos dados experimentais (como um laboratório universitário no PPGCEM/UFCA): **(a)** *augmentação física explícita* (escalonamento/eliminação de picos por textura + deslocamento por *strain*/erro de zero) e **(b)** *injeção de ruído de linha de base experimental real* em picos simulados.
  2. **Arquitetura leve e interpretável por CAMs:** A **a-CNN com Global Average Pooling** de Oviedo et al. (2019) reduz drasticamente parâmetros (evitando *overfitting* em $<100$ amostras experimentais) e entrega **mapas de ativação (CAMs)** que permitem ao pesquisador auditar *quais regiões de $2\theta$* (ex.: $10^\circ\text{–}11^\circ$ do GO, $24^\circ\text{–}26{,}5^\circ$ do rGO/grafite, $42^\circ\text{–}45^\circ$ da banda `(10)`) determinaram a decisão do modelo.
  3. **Critério realista contra "exagero de IA":** Lee et al. (2020) mostram que, mesmo com 800 mil padrões sintéticos, CNNs não substituem Rietveld para quantificação precisa contínua (atingindo apenas 3 faixas grosseiras com 86% no experimental). Logo, a ferramenta da dissertação deve posicionar IA/ML como **triagem rápida ou suporte interpretativo**, e não como substituto absoluto da física da difração.

---

## 8. Possíveis aplicações

- **Proposições — Agente B (sem extrapolar resultados não lidos):**
  - Adaptar a pipeline de **a-CNN 1D + CAMs (Oviedo et al., 2019)** com **augmentação específica para carbonos lamelares** (simulação via Debye/Warren variando número de camadas $N$, $d_{002}$, desordem turboestrática, textura basal e ruído experimental de difratômetro local estilo Wang et al., 2020) para triagem automática de espectros entre classes estruturais (grafite cristalino, grafite desordenado/nanoplaquetas, GO, rGO, carbono amorfo e fases contaminantes/substrato).
  - Investigar o conceito de **otimização de velocidade de varredura** de Oviedo et al. (2019) (testar passos angulares mais grossos ou varreduras rápidas para triagem inicial de lotes de grafeno).

---

## 9. Evidências

- **Oviedo et al. (2019) (`10.1038/s41524-019-0196-x`) — texto completo:**
  - *Results and Discussion* (pp. 2–8): 164 simulados ICSD + 115 experimentais (75 dimensionalidade / 88 grupo espacial); Eqs. 1–3 de augmentação física (p. 8); Tabela 1 (p. 5: a-CNN Caso 3 = 92,9%/89,3%, $F_1$ micro 0,929/0,893, macro 0,859/0,714); Fig. 3 (p. 6: platô ~700 espectros, ganhos até +23% e +19%); Fig. 4 (p. 6: passo até $0{,}16^\circ$, $<5{,}5\ \text{min}$); Fig. 5 (p. 7: Average CAMs e 3 causas de erro).
- **Lee et al. (2020) (`10.1038/s41467-019-13749-3`) — texto completo:**
  - *Results* e *Methods* (pp. 2–10): 170 entradas ICSD $\to$ 38 classes; 1.785.405 padrões (`Dataset_800k_org`, `Dataset_800k_rand`, `Dataset_180k_rand`); Tabela 1 (p. 3: `CNN_3` 100% simulado, 100% $\text{Li}_2\text{O–SrO–Al}_2\text{O}_3$, 98,67% $\text{SrAl}_2\text{O}_4\text{–SrO–Al}_2\text{O}_3$ com detecção de impureza $\text{Sr}_4\text{Al}_{14}\text{O}_{25}$ a 15 wt%); Tabela 2 (p. 4: `CNN_5F` 86,00% em 3 níveis reais); definição de *height fraction* vs. peso/mol (p. 10); índice de novidade ($\sim 10^{-6}$ vs. $10^{-3}\text{–}10^{-1}$, p. 6).
- **Wang et al. (2020) (`10.1021/acs.jcim.0c00020`) — texto completo:**
  - *Results and Discussion* e *Methods* (pp. 4–15 do MD extraído): 1.012 MOFs (72.864 aumentados, 58.292/14.572 split); filtragem FFT/iFFT ($200\ \text{Hz}$); CNN 4 conv + 3 densas; Top-1 56,7% a Top-5 96,7% vs. $<50\%$ nos 5 métodos clássicos (Fig. 3); NCA (Fig. 4) e CAMs 14ª camada para MOF-74, ZIF-8, MOF-199, MOF-5 e falha em ZIF-9 M1 (Fig. 5).

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta (especialmente Oviedo et al., 2019 e Wang et al., 2020 para o desenho da arquitetura computacional).**
- **Justificativa:** Os três artigos já foram lidos na íntegra e trazem arquiteturas, códigos abertos (`AUTO-XRD`, `MOFs`) e métricas diretamente replicáveis. Oviedo et al. (2019) é a referência mais próxima do cenário real da dissertação (pequeno volume de amostras experimentais, efeitos de orientação preferencial e necessidade de explicabilidade visual via CAMs).
