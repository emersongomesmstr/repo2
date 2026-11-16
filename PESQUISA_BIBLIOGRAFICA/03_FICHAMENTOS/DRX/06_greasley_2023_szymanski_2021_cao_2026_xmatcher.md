# Fichamento 06 — ML Clássico vs. Deep Learning Probabilístico e Busca Transparente Baseada em Evidências em DRX (Greasley & Hosein, 2023; Szymanski et al., 2021; Cao, 2026)

> **Status de Leitura e Verificação:** **Texto completo lido integralmente para os três trabalhos:**
> - **Greasley & Hosein (2023):** Texto integral lido via versão *preprint* idêntica de submissão (`_scratch/textos_extraidos/Greasley_Hosein_2023_Supervised_ML_Powder_XRD.md` e `ARTIGOS_PDF/Greasley_Hosein_2023_Supervised_ML_Powder_XRD.pdf`, `arXiv:2211.08591v1`), com publicação final revisada por pares verificada via OpenAlex (`10.1007/s10853-023-08343-4`, *Journal of Materials Science*, 2023).
> - **Szymanski et al. (2021):** Texto integral lido via manuscrito oficial *Green OA* (`_scratch/agente-b/Szymanski_2021_arXiv_2103.16664.pdf`, `arXiv:2103.16664v1`, incluindo *Supplementary Information*), com publicação revisada por pares verificada via OpenAlex (`10.1021/acs.chemmater.1c01071`, *Chemistry of Materials*, 2021).
> - **Cao (2026):** Texto integral lido (`_scratch/textos_extraidos/Cao_2026_XMatcher_Open_Source_Framework_XRD_Phase_Identification.md` e `ARTIGOS_PDF/Cao_2026_XMatcher_Open_Source_Framework_XRD_Phase_Identification.pdf`), **explicitamente identificado como *preprint* (`arXiv:2607.17162v1`) sem revisão por pares confirmada até 16/11/2026**.
>
> **Nota de Auditoria Documental (`arXiv:2608.22400v2` — DESCARTADO):** Verificou-se via API oficial do arXiv (`_scratch/agente-b/arxiv_check.json`) que o *preprint* `arXiv:2608.22400v2` (*"Diagnosing and narrowing the simulation-to-real gap in powder X-ray diffraction with a wet-dry agentic loop"*, Shaoguang Wang et al., agosto de 2026) foi **oficialmente retirado (*withdrawn*) pelos autores** com a justificativa pública: *"The authors have determined that the manuscript in its current form has not yet reached the level of completeness and refinement intended for public dissemination. We therefore request withdrawal of the current submission."* Em conformidade com o rigor científico exigido, `arXiv:2608.22400v2` **foi descartado e NÃO é utilizado como evidência ativa** nesta pesquisa, sendo substituído pelo corpo publicado revisado por pares acima e pelo *preprint* ativo e auditável de Cao (2026).

---

## 1. Identificação bibliográfica

### Artigo 1 — Greasley & Hosein (2023) *(revisado por pares)*
- **Título:** Exploring supervised machine learning for multi-phase identification and quantification from powder X-ray diffraction spectra
- **Autores:** Jaimie Greasley, Patrick A. Hosein
- **Ano:** 2023 (publicação final em março de 2023; *preprint* `arXiv:2211.08591v1` depositado em 16 de novembro de 2022)
- **Periódico:** *Journal of Materials Science*, Volume 58, Número 12, Páginas 5334–5348
- **DOI:** `10.1007/s10853-023-08343-4`
- **URL oficial:** <https://doi.org/10.1007/s10853-023-08343-4> (Versão *Green OA* lida: <https://arxiv.org/pdf/2211.08591>)
- **Citações verificadas (OpenAlex):** 40 (`W4324316850`)

### Artigo 2 — Szymanski et al. (2021) *(revisado por pares)*
- **Título:** Probabilistic Deep Learning Approach to Automate the Interpretation of Multi-phase Diffraction Spectra
- **Autores:** Nathan J. Szymanski, Christopher J. Bartel, Yan Zeng, Qingsong Howard Tu, Gerbrand Ceder
- **Ano:** 2021
- **Periódico:** *Chemistry of Materials*, Volume 33, Número 11, Páginas 4204–4215
- **DOI:** `10.1021/acs.chemmater.1c01071`
- **URL oficial:** <https://doi.org/10.1021/acs.chemmater.1c01071> (Versão *Green OA* lida: <https://arxiv.org/pdf/2103.16664>; Repositório de código: <https://github.com/njszym/XRD-AutoAnalyzer>)
- **Citações verificadas (OpenAlex):** 116 (`W3165475162`)

### Trabalho 3 — Cao (2026) *(Preprint — sem revisão por pares confirmada até 16/11/2026)*
- **Título:** XMatcher: An Open-Source Framework for X-Ray Diffraction Phase Identification
- **Autor:** Bin Cao
- **Ano:** 2026 (submetido em 19 de julho de 2026)
- **Repositório:** arXiv (`arXiv:2607.17162v1`, categoria `cond-mat.mtrl-sci`) — **Preprint não revisado por pares até 16/11/2026**
- **DOI / Identificador:** `10.48550/arXiv.2607.17162` (`arXiv:2607.17162v1`)
- **URL oficial:** <https://arxiv.org/abs/2607.17162v1> (Código aberto: <https://github.com/Asterbin/Asterbin-XMatcher>; Pacote de lançamento: `10.6084/m9.figshare.32812985`)
- **Citações verificadas (OpenAlex):** 1 (`W7169854724`)

---

## 2. Problema investigado

### Fatos extraídos dos artigos
- **Greasley & Hosein (2023):** Modelos de *Deep Learning* exigem milhões de padrões simulados e longos tempos de treinamento, além de baixa interpretabilidade, enquanto algoritmos tradicionais de aprendizado supervisionado são frequentemente preteridos sem justificativa empírica. O estudo testa se **algoritmos clássicos de ML** (SVM, Naive Bayes, k-NN, Árvores) igualam ou superam uma rede neural (ANN) tanto na **identificação multi-rótulo** quanto na **estimativa quantitativa de frações mássicas** em dados reais escassos ($N = 52$ e $N = 46$ espectros experimentais de cálculos urinários com até 4 fases simultâneas), avaliando ainda o impacto de treinar apenas com simulações vs. dados experimentais reais.
- **Szymanski et al. (2021):** Como superar simultaneamente três gargalos críticos das abordagens anteriores de DL em DRX: (1) a **explosão combinatória** de Lee et al. (2020), (2) a incapacidade de métodos *single-shot* (Maffettone et al., 2021) distinguirem similaridade entre duas fases únicas de uma mistura real contendo ambas, e (3) a falha generalizada de modelos treinados apenas em fases estequiométricas quando confrontados com **materiais não estequiométricos (soluções sólidas)** e artefatos experimentais intensos (deslocamento por altura da amostra, fundo amorfo, baixa cristalinidade/alargamento e textura)?
- **Cao (2026):** Softwares comerciais de *search-match* (JADE, HighScore Plus, Match!, DIFFRAC.EVA, PDXL) são proprietários e opacos, enquanto sistemas baseados em IA frequentemente sofrem de *domain shift* e retornam apenas um rótulo ou escore único sem expor o raciocínio cristalográfico. Como construir uma **infraestrutura aberta, local, reproduzível e orientada a evidências** que mostre explicitamente **quais picos suportam, quais contradizem e quais permanecem não explicados** em análises monofásicas e multifásicas?

### Análise crítica — Agente B
- Este trio encerra perfeitamente a evolução metodológica de DRX computacional (2021–2026), respondendo diretamente ao mandato do `PROMPT_MESTRE.md` (Seção 3-E): **não presumir que IA profunda é sempre superior a métodos convencionais**, confrontar modelos físicos e estatísticos transparentes com *Deep Learning* e evidenciar a persistência do *simulation-to-real gap*.

---

## 3. Fundamentação

### Fatos extraídos dos artigos
- **Greasley & Hosein (2023):**
  - Modelos paramétricos/metódicos (SVM com hiperplano ótimo, Naive Bayes com probabilidades condicionais — especialmente **Complement Naive Bayes, CNB**, projetado para classes desbalanceadas —, e **k-NN** não paramétrico) impõem suposições estruturais explícitas, aprendendo com poucos exemplos e com custo de treinamento de milissegundos.
  - Em regressão de frações de fase $\alpha$ ($\sum_j \alpha_j = 1$, $\alpha_j \ge 0$), modelos não restritos como SVR e MLP/ANN violam naturalmente positividade e normalização, exigindo restrições pós-predição, ao passo que métodos baseados em vizinhos (`k-NN`) e árvores preservam combinações convexas dos alvos de treinamento. Propõem a métrica normalizada $\rho = 1 - \|\alpha - \hat{\alpha}\|_2 / \sqrt{2}$ junto a MAE e similaridade por cosseno (CS).
- **Szymanski et al. (2021):**
  - **Soluções sólidas hipotéticas via Hume-Rothery + Lei de Vegard:** Pares estruturalmente isomorfos (`pymatgen structure matcher`) com diferença de raios iônicos $\le 15\%$ têm parâmetros de rede e posições interpolados linearmente, cobrindo não estequiometria contínua.
  - **Augmentação física escalando linearmente $O(N_{\text{fases}})$:** Modela três fenômenos físicos: (i) tensor de deformação preservando grupo espacial ($\pm 4\%$), (ii) alargamento de pico pela **equação de Scherrer** ($\tau = K\lambda / (\beta\cos\theta)$, $K=1$, $\tau \in [1, 100]\ \text{nm}$) e (iii) textura via produto escalar com $(hkl)$ aleatório ($\pm 50\%$).
  - **Incerteza probabilística por *Monte Carlo Dropout* + Algoritmo de Ramificação (`B-CNN`):** 1.000 inferências estocásticas com *dropout* (60%) estimam uma distribuição de probabilidade/confiança; para misturas, uma árvore explora todos os ramos com probabilidade $\ge 10\%$, alinha perfis simulados por **Dynamic Time Warping (DTW, $\Delta 2\theta = 1{,}5^\circ$)** e **subtrai iterativamente cada fase identificada** (*profile stripping*) até todo o sinal residual cair abaixo de 5% do máximo inicial, selecionando o ramo com maior probabilidade média.
- **Cao (2026):**
  - Fundamenta-se na **Lei de Bragg** ($2\theta_{hkl} = 2\arcsin(\lambda / 2d_{hkl})$), fatores de estrutura/Lorentz-polarização (`pymatgen XRDCalculator`), otimização de **atribuição linear um-para-um (*linear sum assignment*)** sob deslocamento angular global limitado $\delta \in [-\Delta, \Delta]$ e tolerância $\tau$, e decomposição de misturas por **mínimos quadrados não negativos (NNLS)**: $\hat{w} = \arg\min_{w\ge 0}\|Aw - y\|_2^2$.
  - Explicita rigorosamente que intensidades calculadas ideais **não** igualam intensidades medidas (por textura, absorção, extinção, tamanho de cristalito, fluorescência, fundo, microdeformação e resposta instrumental) e que os pesos $\rho_\ell$ do NNLS são **contribuições relativas às evidências de pico**, **não** frações mássicas ou volumétricas do método de Rietveld.

---

## 4. Metodologia

### Fatos extraídos dos artigos
- **Greasley & Hosein (2023) *(texto completo)*:**
  - *Dados experimentais:* **52 espectros** de cálculos urinários humanos (classificação; 46 para regressão com média de 2,2 fases/amostra, até 4 fases em 13%, cobrindo 7 fases minerais: whewellita, weddellita, hidroxiapatita carbonatada, estruvita, ácido úrico, urato ácido de amônio, brushita), coletados em Bruker D2 Phaser ($2^\circ \le 2\theta \le 55^\circ$, passo $0{,}02^\circ$). Rótulos de referência (*ground truth*) validados por DIFFRAC.EVA (ICDD PDF-2) + **refinamento Rietveld no MAUD**.
  - *Dados sintéticos:* Pymatgen + protocolo de Szymanski et al. (2021) + **GSAS-II** (para replicar picos largos sobrepostos de fases nanométricas), gerando 105 espectros monofásicos (`s`) e 184 mono+multifásicos (`m`). Normalização pelo máximo de cada espectro.
  - *Modelos:* k-NN, SVM, Decision Tree (Gini/Entropia), GNB, MNB, CNB, Random Forest (70 estimadores), Extra Trees (70 estimadores) e ANN rasa (1 camada oculta, 1.000 nós, logística, Adam), ajustados por `GridSearchCV` em Scikit-Learn.
  - *Quatro cenários de avaliação:* `[1]` Sim $\to$ Sim (5-fold CV); `[2]` Exp $\to$ Exp (5-fold CV na classificação; LOOCV na regressão); `[3]` Sim $\to$ Exp ($N=184 \to T=52$); `[4]` Sim+Exp $\to$ Exp (10 repetições aleatórias).
- **Szymanski et al. (2021) *(texto completo)*:**
  - *Espaço químico:* $\text{Li–Mn–Ti–O–F}$ (1.216 entradas ICSD $\to$ **140 fases estequiométricas únicas** + **115 soluções sólidas hipotéticas** de 43 pares solúveis).
  - *Dataset simulado:* 150 variações/fase = 21.000 estequiométricas + 17.250 soluções sólidas = **38.250 espectros** ($2\theta = 10^\circ\text{–}80^\circ$, vetor 4.501, $\text{Cu } K\alpha$, FWHM base $0{,}015^\circ$), mais conjuntos de teste com fundo de sílica amorfa (100–300%), ruído gaussiano (1–5%), 20 soluções sólidas reais da ICSD e 3.000 misturas multifásicas simuladas. Pré-processamento experimental com algoritmo *rolling ball* (raio $4^\circ$, OpenCV) e filtro IIR (SciPy).
  - *Arquitetura CNN:* 6 camadas `Conv1D` (kernels 35, 30, 25, 20, 15, 10; 64 filtros; *pooling*), 2 camadas densas (3.100 e 1.200; *dropout* 60%), saída de 140 ou 255 nós, 2 épocas, 5-fold CV.
  - *Validação experimental real (76 espectros):* Rigaku MiniFlex 600 ($\text{Cu } K\alpha$, $10^\circ\text{–}100^\circ$, passo $0{,}01^\circ$, $3^\circ/\text{min}$) sob condições controladas: 10 amostras prístinas, 10 cobertas com **fita Kapton** (fundo difuso até 200%), 10 varreduras rápidas ($30^\circ/\text{min}$), 6 pastilhas espessas (deslocamento até $0{,}4^\circ$), 5 moídas em moinho de bolas (FWHM até $1{,}5^\circ$), 6 desordenadas por têmpera/resfriamento ($\text{LiMnTiO}_4$), 4 *rocksalts* não estequiométricos, 10 misturas binárias e 15 fases em misturas ternárias (10 espectros binários+ternários: 5 binários = 10 fases + 5 ternários = 15 fases). Comparado contra **MDI JADE** automático.
- **Cao (2026) *(texto completo)*:**
  - *Biblioteca:* `MP500.db` (**100.315** estruturas do Materials Project em formato ASE) convertida offline via `pymatgen XRDCalculator` ($\text{Cu } K\alpha$, $10^\circ\text{–}90^\circ$, $d_{\min} = 0{,}5\ \text{Å}$, 30 reflexões mais intensas por fase) em `MP500_xrd_database.pkl` com índices exatos e invertidos de elementos.
  - *Motor de busca:* Pré-processamento ($I'_i = \max(0, \tilde{I}_i - B_i)$), busca de deslocamento global $\delta \in [-\Delta, \Delta]$, atribuição um-para-um minimizando custo $C_{ij}(\delta) = w_x |e_i - (t_{qj}+\delta)|/\tau + w_I |a_i^{(\%)} - b_{qj}^{(\%)}|/100$, escore híbrido $H$ combinando qualidade $Q$, coberturas experimentais/teóricas $C_E, C_T$, precisão $P$ e revocação $R$.
  - *AutoMix e Validação PDF:* Enumeração controlada até $p$ fases sobre *pool* de $n$ candidatos (padrão $n=8, p=3 \implies 92$ combinações) com modo restrito por conjuntos elementares exatos ou MPIDs (AND lógico) e ajuste NNLS; validação completa de padrão por CIF via `pysimxrd` com alargamento gaussiano (FWHM) e pesos relativos definidos pelo usuário.

---

## 5. Resultados

### Fatos extraídos dos artigos
- **Greasley & Hosein (2023) *(Tabelas 2–4, Figs. 2–3)*:**
  - *Classificação — `[2]` Exp-only ($N=52$):* **CNB** alcançou o melhor $F_1\ \text{avg} = 0{,}812$ e acurácia total $= 88{,}8\%$ (em **$0{,}03\ \text{s}$** vs. **$67\ \text{s}$** da ANN com $F_1\ \text{avg}=0{,}810$, total $88{,}3\%$); **SVM** e ANN empataram na maior acurácia de fase majoritária (**MPA $= 98{,}2\%$**) e acurácia exata de rótulo (**ELA $= 47{,}3\%$**).
  - *Classificação — `[3]` Sim $\to$ Exp:* SVM e ANN obtiveram **MPA $= 100\%$**, mas **SVM superou a ANN** em $F_1\ \text{avg}$ ($0{,}787$ vs. $0{,}763$) e acurácia total ($87{,}9\%$ vs. $87{,}1\%$); MNB e CNB tiveram a melhor ELA ($44{,}2\%$ e $42{,}3\%$).
  - *Classificação — `[4]` Sim+Exp $\to$ Exp:* ANN ($F_1\ \text{avg}=0{,}809$, total $88{,}9\%$) e **SVM** ($F_1\ \text{avg}=0{,}806$, total $88{,}8\%$) lideraram; no simulado multifásico, SVM treinou em **$0{,}08\ \text{s}$** contra **$88\ \text{s}$** da ANN. Árvores (DTr, RF, ExTr) obtiveram desempenho consistentemente inferior.
  - *Regressão de frações mássicas ($N=46$):* **k-NN ($k=2$, ponderado por distância)** superou todos os modelos em `[1]` ($\rho=0{,}7756$, MAE $0{,}0682$), `[3]` (MAE $0{,}0827$) e `[4]` ($\rho=0{,}8462$, MAE $0{,}0479$, CS $0{,}9539$); em `[2]` (LOOCV experimental), ANN atingiu $\rho=0{,}8582$, MAE $0{,}0491$, seguida de perto por k-NN ($\rho=0{,}8369$, MAE $0{,}0520$). **Treinar apenas com dados simulados (`[3]`) piorou a regressão em comparação a usar apenas os poucos dados experimentais reais (`[2]`)**, mesmo modelando todos os artefatos principais.
- **Szymanski et al. (2021) *(Tabela 1, Figs. 3–5)*:**
  - *Simulado estequiométrico:* CNN atingiu **94%** (artefatos isolados) e **92%** (artefatos mistos) vs. JADE **78%** e **68%**. Quando filtradas por confiança probabilística $>70\%$ (84% das amostras), a acurácia subiu para **96%** (e a fase verdadeira esteve no Top-3 em **99%** dos casos). Erros concentraram-se em **deslocamento de picos por deformação (48% dos erros)** entre isomorfos e **alargamento de picos (27% dos erros)** em estruturas monoclínicas/triclínicas (82 de 113 erros).
  - *Não estequiométricos (20 soluções sólidas ICSD):* A adição das 115 soluções sólidas hipotéticas elevou a acurácia estrutural da CNN de **55% (11/20) para 95%** (vs. JADE de 35% para 70% citado no texto / 75% grafado na Fig. 4a) e reduziu pela metade o erro composicional médio (de $0{,}38$ para $0{,}18$ em fração molar).
  - *Misturas simuladas (Fig. 5):* **B-CNN** atingiu **87%** (2 fases) e **78%** (3 fases), superando S-CNN (70%/54%), M-CNN estilo Lee et al. (65%/58%) e JADE (59%/49%). Em misturas desiguais (70–90% vs. 10–30%), acertou **92%** na fase majoritária e **64%** na minoritária (detectando a existência da segunda fase em **93%** dos casos, com 9% de falsos positivos de segunda fase em monofásicos).
  - *76 espectros experimentais reais (Tabela 1):* **CNN/B-CNN acertou 71/76 (93,4%) vs. JADE 53/76 (71,4%)**, com destaque em amostras espessas com deslocamento de $2\theta$ (**5/6 vs. 2/6**), varreduras rápidas ruidosas (**10/10 vs. 7/10**), misturas binárias (**10/10 vs. 7/10**) e ternárias (**13/15 vs. 9/15**). Tempo para treinar todo o espaço de 140 fases: ~1 dia em 16 CPUs (escala linear).
- **Cao (2026) *(texto completo)*:**
  - Apresenta a arquitetura de software v1.1.0 completa e validada programaticamente (`XMatcher` + `AutoMix` + comparação PDF/CIF via `pysimxrd` + GUI local e API Python), expondo tabelas explícitas de interpretação de evidências favoráveis e contrárias (Tabela 1) e garantindo rastreabilidade e execução totalmente local. *(Nota: o preprint foca na engenharia, formulação algorítmica e interface do software, **sem incluir um benchmark quantitativo comparativo** de acurácia em conjuntos públicos contra JADE, Profex ou B-CNN).*

---

## 6. Limitações

### Fatos extraídos dos artigos e análise crítica — Agente B
1. **Greasley & Hosein (2023):** Conjunto experimental restrito a 7 fases minerais de cálculos renais em um único difratômetro; modelos tradicionais operam sobre o vetor bruto de intensidades sem redução de dimensionalidade prévia (que poderia falhar caso houvesse dezenas/centenas de fases); mesmo com modelagem física via pymatgen+GSAS-II, o treinamento puramente sintético (`[3]`) ainda degradou frente ao treino experimental real (`[2]`).
2. **Szymanski et al. (2021):** Limite de deslocamento por deformação ($\pm 4\%$: ampliar para $\pm 6\%$ causou degenerescência entre fases e caiu de 92% para 86% na Fig. S1); predição composicional em soluções sólidas ainda limitada porque ocupâncias de sítios (ex.: inversão catiônica em espinélios) alteram intensidades relativas sem seguir a Lei de Vegard; acurácia ainda moderada para **fases minoritárias/impurezas (64%)** por imperfeições da subtração por DTW; não substitui Rietveld e **não cobre materiais turboestráticos/2D sem célula periódica 3D completa**.
3. **Cao (2026):** **Status de preprint (julho de 2026, sem revisão por pares confirmada até 16/11/2026)**; ausência de benchmark estatístico quantitativo de desempenho no manuscrito; limitado às estruturas presentes em `MP500.db` (100.315 entradas — que tipicamente representam cristais 3D estequiométricos perfeitos, não GO hidratado variável ou carbono turboestrático); o deslocamento angular global único $\delta$ não modela *strain* não uniforme nem mudanças de parâmetro de rede; e o próprio autor ressalta que NNLS/AutoMix não realiza quantificação de fases.

---

## 7. Contribuição para a dissertação

- **Análise — Agente B:**
  1. **Justificativa científica direta para não forçar Deep Learning onde não cabe (Greasley & Hosein, 2023):** Demonstra empiricamente que, com dezenas de espectros reais e poucas classes (ex.: distinguir grafite, GO, rGO, carbono amorfo e contaminantes usuais de síntese), **SVM, CNB e k-NN** igualam ou superam redes neurais treinando em **centésimos de segundo**, com hiperparâmetros auditáveis e menor risco de *overfitting*.
  2. **Modelo arquitetural para lidar com *artifacts* e incerteza (Szymanski et al., 2021):** Ensina como transformar uma rede ou classificador em sistema **ciente da incerteza** (sinalizando *red flag* abaixo de 70% de confiança para intervenção humana), além de fornecer protocolo consolidado de perturbação física de espectros sintéticos (inclusive via GSAS-II / Scherrer) e de subtração iterativa (*profile stripping*).
  3. **Filosofia de projeto "evidência em primeiro lugar" (Cao, 2026):** Inspira o padrão de interface da ferramenta da dissertação: **nunca entregar apenas um rótulo ("é grafeno/rGO")**, mas expor **evidências favoráveis e contra-evidências explícitas** (picos explicados, deslocamentos observados, picos esperados ausentes como falta de `(002)` ou `(101)`, e alertas sobre limitações físicas como textura e necessidade de Raman/AFM/TEM).

---

## 8. Possíveis aplicações

- **Proposições — Agente B (sem extrapolar resultados não lidos):**
  - Construir um benchmark comparativo honesto na dissertação avaliando **SVM / CNB / k-NN** (estilo Greasley & Hosein, 2023) vs. **a-CNN leve com CAMs** (estilo Oviedo et al., 2019) vs. **busca baseada em evidências/regras físicas** (estilo XMatcher, Cao, 2026) sobre um conjunto curado de difratogramas de grafite, GO, rGO e nanoplaquetas grafíticas (incluindo simulações pela equação de Debye).
  - Incorporar um módulo de **"evidências e contra-evidências"** inspirado no XMatcher adaptado a carbonos lamelares: em vez de buscar 100 mil fases inorgânicas cegamente, verificar sistematicamente posição e FWHM de `(001)` (GO), `(002)` (grafite/rGO), presença de `(101)`/`(102)` (ordem 3D `ABAB` vs. ausência = desordem turboestrática) e assimetria da banda `(10)`, reportando o diagnóstico com nível de confiança e recomendações de validação por MEV/AFM/Raman.

---

## 9. Evidências

- **Greasley & Hosein (2023) (`10.1007/s10853-023-08343-4` / `arXiv:2211.08591v1`) — texto completo:**
  - *Experimental Methods* (pp. 3–5): $52/46$ amostras reais (Bruker D2 Phaser, MAUD Rietveld), $105/184$ simulações (pymatgen + Szymanski + GSAS-II), métrica $\rho$ (Eq. 4).
  - *Results & Analysis* (Tabelas 2–4, pp. 5–9): CNB ($F_1=0{,}812$, $88{,}8\%$, $0{,}03\ \text{s}$) e SVM ($F_1=0{,}786\text{–}0{,}806$, MPA $98{,}2\%\text{–}100\%$, $0{,}08\ \text{s}$) vs. ANN ($67\text{–}88\ \text{s}$); regressão k-NN superior em `[1]`, `[3]` e `[4]` ($\rho=0{,}8462$, MAE $0{,}0479$).
- **Szymanski et al. (2021) (`10.1021/acs.chemmater.1c01071` / `arXiv:2103.16664v1`) — texto completo:**
  - *Methods* e *Supplementary Notes 1–6* (pp. 4–10, 42–48): 140 fases + 115 soluções sólidas hipotéticas; 38.250 espectros ($\pm 4\%$ *strain*, Scherrer $1\text{–}100\ \text{nm}$, textura $\pm 50\%$); *MC dropout* (1.000 amostras) + B-CNN + DTW ($\Delta 2\theta = 1{,}5^\circ$, corte 5%).
  - *Results* e *Table 1* (pp. 10–22): 94%/92% simulado vs. 78%/68% JADE; 96% para confiança $>70\%$; 55% $\to$ 95% em não estequiométricos; B-CNN 87%/78% em 2/3 fases simuladas (92% majoritária, 64% minoritária); **71/76 (93,4%) vs. JADE 53/76 (71,4%)** em experimentos reais.
- **Cao (2026) (`arXiv:2607.17162v1`) — texto completo:**
  - *Features* e *Methods* (pp. 4–15): `MP500_xrd_database.pkl` (100.315 estruturas, 30 picos principais), Eqs. 1–12 (Bragg, custo $C_{ij}(\delta)$, escore híbrido $H$, NNLS $w \ge 0$, contribuição $\rho_\ell$, validação gaussiana CIF), Tabela 1 (p. 9) e seção *Limitations* (p. 10).
- **Auditoria de descarte (`arXiv:2608.22400v2`) — API arXiv (`_scratch/agente-b/arxiv_check.json`):**
  - Confirmação do campo `comment` oficial declarando retirada (*withdrawal*) pelos autores; item excluído do corpo bibliográfico ativo.

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta (todos os três trabalhos já lidos integralmente).**
- **Justificativa:** Este conjunto define diretamente a estratégia computacional da dissertação: **Szymanski et al. (2021)** para simulação física escalável $O(N)$ e inferência com limiar de confiança; **Greasley & Hosein (2023)** para justificar empiricamente o uso de modelos supervisionados leves (SVM/CNB/k-NN) quando há poucos dados experimentais; e **Cao (2026)** — respeitando seu status de *preprint* não revisado por pares — como referência moderna de transparência algorítmica e interface orientada a evidências.
