# Fichamento 06 — Carracedo-Cosme et al. (2022, QUAM-AFM) & Harris et al. (2025, SparseC-AFM): Bases de Dados e Deep Learning em AFM — Análise Crítica Obrigatória do Piloto `IVEFAC333.pptx`

> **Nível de leitura declarado (Seção 7 do `PROMPT_MESTRE.md`):**
> - **Carracedo-Cosme *et al.* (2022) — QUAM-AFM:** **TEXTO COMPLETO LIDO E AUDITADO** (`Carracedo-Cosme_2022_QUAM-AFM.txt` + texto completo HTML verificado no `PMC9942089`, incluindo Figuras 1–6 e 57 referências).
> - **Carracedo-Cosme *et al.* (2021) — QUAM-AFM Lite:** **Metadados completos (DataCite API + OpenAlex) e descrição oficial integral verificados**.
> - **Harris *et al.* (2025) — SparseC-AFM:** **TEXTO COMPLETO LIDO E AUDITADO** (`Harris_2025_SparseC-AFM_Deep_Learning_Characterization_MoS2.md` + PDF `Harris_2025_SparseC-AFM_Deep_Learning_Characterization_MoS2.pdf` com Figuras 1–6), além dos **metadados publicados nos anais SPIE verificados via Crossref** (`10.1117/12.3067427`) e do repositório oficial `UNITES-Lab/sparse-cafm`.
> - **Piloto local `IVEFAC333.pptx`:** **CONTEÚDO INTEGRAL DOS 15 SLIDES LIDO E AUDITADO** diretamente a partir do arquivo XML interno da apresentação.

---

## 1. Identificação bibliográfica

### Artigo 1 — QUAM-AFM e Dataset QUAM-AFM Lite
- **Título:** QUAM-AFM: A Free Database for Molecular Identification by Atomic Force Microscopy
- **Autores:** Jaime Carracedo-Cosme, Carlos Romero-Muñiz, Pablo Pou, Rubén Pérez
- **Ano:** 2022 (publicado em 2 de março de 2022)
- **Periódico:** *Journal of Chemical Information and Modeling* (*J. Chem. Inf. Model.*), Vol. 62, Nº 5, pp. 1214–1223
- **DOI:** `10.1021/acs.jcim.1c01323` | **PMCID:** `PMC9942089` | **PMID:** `35234034`
- **Links oficiais verificados:** [DOI / ACS](https://doi.org/10.1021/acs.jcim.1c01323) | [PMC9942089 (Texto completo OA)](https://pmc.ncbi.nlm.nih.gov/articles/PMC9942089/)
- **Dataset derivado analisado no piloto:** *QUAM-AFM Lite* (v1.1), Carracedo-Cosme *et al.* (2021), repositório *e-cienciaDatos*, DOI [`10.21950/BFAU11`](https://doi.org/10.21950/BFAU11) (licença CC BY-NC-SA 4.0).

### Artigo 2 — SparseC-AFM (Preprint arXiv já publicado nos anais SPIE)
- **Título:** SparseC-AFM: a deep learning method for fast and accurate characterization of $\text{MoS}_2$ with C-AFM *(título nos anais SPIE: "Sparse C-AFM: a deep learning method for fast and accurate characterization of MoS2 with conductive atomic force microscopy")*
- **Autores:** Levi Harris, Md Jayed Hossain, Mufan Qiu *(grafado "Mufan Qui" nos metadados Crossref/SPIE)*, Ruichen Zhang, Pingchuan Ma, Tianlong Chen, Jiaqi Gu, Seth Ariel Tongay, Umberto Celano
- **Ano:** 2025 (**Nota editorial verificada:** inicialmente depositado como preprint `arXiv:2507.13527v1` em 17/07/2025, **já publicado nos anais revisados/conferência da SPIE em 17/09/2025**)
- **Publicação oficial:** *Proceedings of SPIE*, Vol. 13582 — *Low-Dimensional Materials and Devices 2025* (San Diego, EUA, 4–6 ago. 2025; Eds. N. P. Kobayashi, A. A. Talin, A. V. Davydov, M. S. Islam), artigo `135820J` (p. 35 no registro Crossref)
- **DOIs:** `10.1117/12.3067427` (versão SPIE publicada) | `10.48550/arXiv.2507.13527` (preprint)
- **Links oficiais verificados:** [DOI SPIE](https://doi.org/10.1117/12.3067427) | [arXiv PDF](https://arxiv.org/pdf/2507.13527) | [Código GitHub](https://github.com/UNITES-Lab/sparse-cafm)

---

## 2. Problema investigado

- **Carracedo-Cosme *et al.* (2022):** Como viabilizar o treinamento de modelos de aprendizado profundo (*deep learning*) para **identificação química/estrutural de moléculas orgânicas individuais a partir de imagens de AFM de alta resolução (HR-AFM)**? Como obter experimentalmente milhões de imagens rotuladas em UHV com ponta funcionalizada com CO é fisicamente inviável, os autores propõem construir o maior banco sintético de pilhas 3D simuladas de HR-AFM cobrindo a diversidade da química orgânica.
- **Harris *et al.* (2025):** Como superar o gargalo de velocidade da **Microscopia de Força Atômica Condutiva (C-AFM)** na caracterização de materiais 2D (como $\text{MoS}_2$) em escala pré-industrial ("*lab-to-fab*")? Enquanto uma varredura densa ($512 \times 512$ px, $5\text{--}10\text{ nm/pixel}$) consome $10\text{--}30\text{ min}$ por imagem e acelera o desgaste da ponta condutiva, varreduras esparsas rápidas perdem resolução crítica para mapear defeitos, trincas e contornos de ilhas cristalinas; o trabalho investiga se uma arquitetura de super-resolução baseada em *Swin Transformers* consegue reconstruir mapas de altura e corrente completos a partir de entradas subamostradas.

---

## 3. Fundamentação

1. **Física do contraste em HR-AFM com ponta CO em UHV (Carracedo-Cosme *et al.*, 2022, Seções *Introduction* e *Methods*):**
   - Opera no modo **FM-NC-AFM (não-contato por modulação de frequência)** em altura constante com sensor rígido *qPlus* e ponteira metálica funcionalizada por uma **molécula de CO** no ápice.
   - O sinal registrado é o **deslocamento de frequência ($\Delta f$)** em função das forças conservativas de curto/longo alcance entre o oxigênio terminal do CO e a molécula adsorvida.
   - A simulação **FDBM@PPM** (*Full Density-Based Model* implementado no *Probe Particle Model*) decompõe a interação em quatro termos: (i) **repulsão de Pauli de curto alcance (SR)** proporcional à sobreposição das densidades eletrônicas sonda–amostra ($\alpha = 1$, $V_0 = 18\text{ eV}\cdot\text{\AA}^3$); (ii) **interação eletrostática (ES)** via convolução do potencial eletrostático da amostra $V_{\text{sample}}$ com a densidade diferencial multipolar da ponta $\Delta\rho_{\text{CO}}$; (iii) **atração de van der Waals (vdW)** pelo termo $r^{-6}$ de Lennard-Jones (e Grimme D3 na DFT); e (iv) **relaxação elástica por inclinação angular (*tilting*)** da molécula de CO via mola torsional ($\delta = 302\text{ pm}$, rigidez $\kappa$).
   - As imagens mostram estruturas intramoleculares, ordens de ligação e efeitos como $\sigma$-*hole* em halogênios em variação de apenas dezenas de picômetros ($z \in [2{,}80; 3{,}70]\text{ \AA}$).
2. **Física e compromisso de resolução-tempo em C-AFM (Harris *et al.*, 2025, Seção 1.1 e Fig. 1):**
   - O C-AFM opera em **modo contato** com ponta condutiva (ex.: revestida de Pt/Ir) sob tensão de polarização (*bias*), registrando simultaneamente **topografia ($z$)** e **corrente elétrica ($I$)** através da junção ponta–amostra.
   - Como a imagem resulta da **convolução geométrica entre o ápice da ponta ($\sim 10\text{ nm}$ de raio) e as feições da superfície**, resolver defeitos de $\sim 10\text{ nm}$ exige espaçamento de linha $\le 5\text{ nm/pixel}$, impondo $256\text{--}512$ linhas ($10\text{--}30\text{ min}$ por quadro) e agravando desgaste mecânico/elétrico da sonda.
   - Redes neurais de super-resolução baseadas em atenção por janelas deslocadas (*SwinIR / Swin Transformer*) combinam extração rasa convolucional ($H_{\text{SF}}$), extração profunda global/local ($H_{\text{DF}}$ com blocos residuais RSTB) e reconstrução ($H_{\text{REC}}$) com conexão residual longa para recuperar feições de alta frequência a partir de grades subamostradas.

---

## 4. Metodologia

### A. Carracedo-Cosme *et al.* (2022) [texto completo, *Methods* e *Results*]
- **Seleção molecular (PubChem3D):** $685.513$ moléculas orgânicas quasi-planares (variação em $z \le 1{,}83\text{ \AA}$, entre $8$ e $85$ átomos, cabendo em célula quadrada de $24\text{ \AA} \times 24\text{ \AA}$, contendo C, H, N, O, S, P, F, Cl, Br, I; excluindo sais e inorgânicos). As geometrias usadas são **conformações em fase gasosa** do PubChem (sem substrato explícito).
- **Cálculos DFT e PPM:** Densidade eletrônica e potencial eletrostático calculados no VASP (PBE + Grimme D3, PAW, *cutoff* $400\text{ eV}$), convertidos para formato `.xsf` e simulados via FDBM@PPM em passos $\Delta z = 0{,}1\text{ \AA}$.
- **Grade paramétrica de geração:** Para cada molécula, $4$ constantes elásticas de inclinação do CO ($\kappa = 0{,}40; 0{,}60; 0{,}80; 1{,}00\text{ N/m}$) $\times$ $6$ amplitudes de oscilação ($A = 0{,}40; 0{,}60; 0{,}80; 1{,}00; 1{,}20; 1{,}40\text{ \AA}$) $=$ **$24$ pilhas 3D**, cada uma com **$10$ alturas ponta–amostra** ($2{,}80$ a $3{,}70\text{ \AA}$) $= \mathbf{240}$ imagens $256 \times 256$ px por molécula ($\sim 165\text{ milhões}$ de imagens, $713\text{ GB}$, $2{,}5\text{ milhões}$ de horas de computação).
- **Versão reduzida *QUAM-AFM Lite* (`10.21950/BFAU11`):** Subconjunto idêntico em formato e parâmetros para $1.755$ moléculas ($421.200$ imagens, $2\text{ GB}$), organizado em 24 pastas $(A, \kappa)$ contendo subpastas por **número CID do PubChem**, com interface gráfica `QUAM.py` e descritores (nome IUPAC, fórmula química, coordenadas, mapa de altura atômica e modelo *ball-and-stick*). Os autores recomendam explicitamente particionar treino/validação/teste **por listas disjuntas de CIDs** (*Data Organization and Indexing*).

### B. Harris *et al.* (2025) [texto completo + repositório oficial]
- **Amostras e aquisição experimental:** Filmes de $\text{MoS}_2$ crescidos por PECVD sobre $\text{Si-SiO}_2$ (e safira no repositório GitHub). Coleta em sistema **Park NX-Hivac AFM** em **modo contato**, em alto vácuo ($10^{-5}\text{ torr}$) e ao ar, com sondas condutivas Nanosensors **PPP-CONTSCPt** ($k = 0{,}2\text{ N/m}$) e contato traseiro com pasta eutética de Ag.
- **Dados multiresolução:** Mapas duais (morfologia superficial e corrente superficial) de $2\text{ }\mu\text{m} \times 2\text{ }\mu\text{m}$ adquiridos em $512 \times 512$ (referência completa) e varreduras esparsas em $256 \times 256$ ($\sigma = 2$, redução $\times 4$), $128 \times 128$ ($\sigma = 4$, redução $\times 16$) e $64 \times 64$ ($\sigma = 8$, redução $\times 64$). *(Nota verificada no repositório `UNITES-Lab/sparse-cafm`: o conjunto bruto de $\text{MoS}_2$ contabiliza 4 amostras físicas / 19 pontos de varredura, ampliados por recortes aleatórios de $256\times 256$ ou $384\times 384$ e *data augmentation*).*
- **Modelo e treinamento:** Variantes para $\times 2, \times 4, \times 8$ baseadas no SwinIR ($6$ blocos RSTB, $6$ camadas STL, janela $8$, dimensão de canal $180$, $6$ cabeças de atenção), otimizadas com perda pixel-a-pixel $L_1$ ($\|\hat{y} - y\|_1$), Adam ($lr = 10^{-5}$), $200$ épocas ($1024$ passos/época) em GPU A6000.
- **Avaliação dupla:** (1) Métricas clássicas de restauração de imagem (**PSNR** e **SSIM**) frente a *Gaussian Process Regression* (GPR) e RNAN; e (2) *script* em Python/OpenCV ("*physics-informed*") para extrair propriedades físicas/elétricas do mapa de corrente reconstruído: corrente superficial média, porcentagem de cobertura, comprimento de contornos de grão/ilha e área total de defeitos.

---

## 5. Resultados

- **Carracedo-Cosme *et al.* (2022) [texto completo]:**
  - Entregou a maior base pública estruturada de HR-AFM simulado ($685.513$ moléculas; $\sim 165\text{ milhões}$ de imagens; versão *Lite* de $1.755$ moléculas) e validou qualitativamente que o modelo aproximado FDBM@PPM reproduz o contraste relativo sítio-a-sítio (ex.: átomos pesados como I, Br e Cl brilhantes pelo $\sigma$-*hole*, O e N de menor contraste relativo por densidade confinada, distorção de anéis por potencial ES e inclinação do CO) frente a cálculos DFT completos em *m*-DBPc e *clusters* halogenados (Figs. 1–2).
  - Demonstrou forte sensibilidade da imagem à distância $z$ em intervalos de poucos décimos de ångström (Fig. 4) e ao acoplamento $(A, \kappa)$ (Fig. 3).
- **Harris *et al.* (2025) [texto completo, Figs. 4–6]:**
  - Reduziu o tempo de aquisição de $\sim 15\text{ min}$ (ou $15\text{--}30\text{ min}$) para $< 5\text{ min}$ (e até $> 11\times$ de ganho reportado na combinação aquisição esparsa + extração automatizada).
  - Superou o método GPR em todos os regimes testados (e destacou que GPR tem complexidade $\mathcal{O}(N^3)$, tornando-se computacionalmente inviável em redução $\times 64$) e suportou *upsampling* $\times 8$ ($\times 64$ em área, PSNR $\sim 38\text{ dB}$ e SSIM $\sim 0{,}89$ na Fig. 6), enquanto o RNAN não suporta $\times 8$.
  - No *scorecard* de propriedades elétricas (Fig. 5), o SparseC-AFM melhorou acentuadamente a fidelidade de área de defeitos e comprimento de contornos em redução $\times 64$ (mais de $60\%$ de melhoria relativa em relação à entrada esparsa para propriedades geométricas estendidas).

---

## 6. Limitações

- **Em Carracedo-Cosme *et al.* (2022) [reconhecidas no artigo + crítica]:**
  - *Reconhecidas pelos autores:* Uso de geometrias de fase gasosa sem relaxação explícita sobre substratos reais (que podem induzir deformações ou inclinação molecular na adsorção); uso de parâmetros fixos aproximados no FDBM@PPM ($\alpha = 1, V_0 = 18\text{ eV}\cdot\text{\AA}^3$); restrição estrita a moléculas orgânicas quasi-planares ($z \le 1{,}83\text{ \AA}$, $\le 85$ átomos, $\le 24\text{ \AA}$).
  - *Crítica adicional:* Simulações ideais livres de ruído experimental, deriva térmica, histerese piezoelétrica ou contaminação; **o artigo descreve o banco de dados, mas não apresenta treinamento/benchmark de um modelo novo dentro do próprio texto de 2022** (apenas cita um trabalho anterior do grupo sobre 60 moléculas em *Nanomaterials* 2021).
- **Em Harris *et al.* (2025) [identificadas criticamente no PDF e repositório]:**
  1. **Escassez amostral real e dependência de *fine-tuning*:** Apesar da narrativa "lab-to-fab", o conjunto bruto de $\text{MoS}_2$ no repositório oficial conta com apenas **4 amostras / 19 varreduras brutas**, exigindo *random crops* intensivos e **ajuste fino (*fine-tuning*) com dados reais em resolução completa do novo material/substrato** antes da inferência (Seção 2.3).
  2. **Ganho marginal sobre RNAN em $\times 4$ e $\times 16$ e falha em cobertura a $\times 4$:** Na Fig. 6, em $\times 4$ e $\times 16$, PSNR e SSIM do SparseC-AFM são praticamente empatados com a CNN RNAN; mais crítico ainda, na Fig. 5 (*Scorecard*), na redução $\times 4$, a métrica ***coverage percent*** aparece em cor preta ($\sim -60\%$, **pior que o mapa esparso de referência**!), revelando que perdas $L_1$ pixel-a-pixel podem suavizar/distorcer limiares binários de cobertura mesmo com PSNR alto.
  3. **Risco de alucinação de defeitos em super-resolução $\times 64$:** Em subamostragem $64\times 64 \rightarrow 512\times 512$, feições estreitas (trincas $< 1$ pixel da grade esparsa) podem ser fisicamente não amostradas (teorema de Nyquist), de modo que a rede infere texturas estatisticamente plausíveis em vez de medir fisicamente o defeito naquele ponto. *(Nota editorial: no PDF p. 2 há referência errônea a "Figure 5a-c" / "Figure 5d" para a Fig. 1).*

---

## 7. Contribuição para a dissertação (incluindo Análise Crítica Obrigatória do Piloto `IVEFAC333.pptx`)

**[Análise técnica auditada diretamente nos 15 slides de `IVEFAC333.pptx` confrontados com o texto completo de `Carracedo-Cosme et al. (2022)`, `QUAM-AFM Lite` (`10.21950/BFAU11`) e `Harris et al. (2025)`]**

### 7.1 Diagnóstico factual do que foi executado no piloto `IVEFAC333.pptx`
- **Objeto do piloto:** Classificação supervisionada multiclasse ($3$ classes) de **3 isômeros posicionais de $\text{C}_6\text{H}_4\text{BrClO}$** extraídos do *QUAM-AFM Lite* (`10.21950/BFAU11`):
  - **Classe A — CID `16268`:** 2-bromo-6-clorofenol;
  - **Classe B — CID `19859`:** 4-bromo-2-clorofenol;
  - **Classe C — CID `69670`:** 2-bromo-4-clorofenol.
- **Volume e partição de dados (Slide 11):** $3\text{ moléculas} \times 240\text{ imagens/molécula} = 720\text{ imagens}$ ($256 \times 256$ px), submetidas a **divisão 80/20 por arquivo** ($576$ imagens de treino e $144$ imagens de validação).
- **Modelos e resultados reportados (Slides 9, 12 e 13):** Arquitetura **ResNet-18** comparando PyTorch vs. TensorFlow+Keras; no PyTorch, obteve **$100\%$ de acurácia na validação interna ($144$ imagens)** e $3/3$ nos exemplos mostrados (escores PyTorch: $89{,}12\%$, $82{,}34\%$, $88{,}37\%$ vs. TensorFlow: $40{,}72\%$, $41{,}31\%$, $37{,}31\%$).
- **Motivação declarada pelo autor (Slides 4 e 14):** Apoiar futuramente a *"caracterização de amostras de grafeno obtidos por esfoliação eletroquímica"* na UFCA.

### 7.2 Por que há *Domain Shift* extremo entre `QUAM-AFM Lite` e o grafeno da UFCA?
Ao confrontar os parâmetros físicos documentados em Carracedo-Cosme *et al.* (2022) com a caracterização real de grafeno esfoliado eletroquimicamente (documentada em Nemes-Incze 2008, Shearer 2016 e NPL AS 103), verifica-se uma ruptura simultânea em **cinco eixos físicos e computacionais**:

1. **Ruptura de modalidade física e observável de contraste:** O *QUAM-AFM Lite* simula exclusivamente mapas de **deslocamento de frequência ($\Delta f$)** adquiridos em modo **FM-NC-AFM a altura constante**, em **ultra-alto vácuo (UHV) e temperatura criogênica ($\sim 4\text{--}5\text{ K}$)** com sensor *qPlus* e **ponta funcionalizada com CO**, cujo contraste provém de repulsão de Pauli intramolecular e $\sigma$-*holes* de halogênios em variação de $2{,}80$ a $3{,}70\text{ \AA}$. Em contraste, a caracterização de grafeno esfoliado em laboratório de materiais opera rotineiramente em **modo *tapping* (AM-AFM), *PeakForce Tapping* ou contato ao ar (umidade ambiente)**, medindo **topografia $z(x,y)$** dominada por meniscos capilares, forças de van der Waals macroscópicas, camada interfacial de água/eletrólito e convolução por pontas de silício ($R \sim 5\text{--}15\text{ nm}$).
2. **Incompatibilidade de escala espacial ($\sim 10^2\text{--}10^4\times$):** Toda imagem $256 \times 256$ do QUAM-AFM representa uma **célula fixa de $24\text{ \AA} \times 24\text{ \AA}$** ($\sim 0{,}094\text{ \AA/pixel}$) com a molécula centrada. Imagens reais de flocos de grafeno em AFM cobrem campos de **$0{,}5\text{ }\mu\text{m}$ a $20\text{ }\mu\text{m}$** ($1\text{--}40\text{ nm/pixel}$) — três ordens de grandeza maiores — com múltiplos flocos irregulares, dobras, bordas sobrepostas e rugosidade de substrato ($\text{SiO}_2$).
3. **Ausência total de substrato, adsorvatos e química de processo:** As estruturas do QUAM-AFM vêm de **conformações isoladas em fase gasosa** (PubChem3D), sem qualquer substrato físico. Já o grafeno esfoliado eletroquimicamente sobre $\text{SiO}_2/\text{Si}$ apresenta aprisionamento de água/íons ($\text{SO}_4^{2-}$, grupos oxigenados), rugosidade de fundo $R_q$ e degraus heterogêneos de $0{,}4\text{--}1{,}7\text{ nm}$.
4. **Incompatibilidade de formulação da tarefa (Classificação fechada vs. Metrologia física quantitativa):** A ResNet-18 do piloto aprende a classificar 3 rótulos categóricos discretos (IDs de moléculas individuais em cinza normalizado); caracterizar flocos de grafeno exige **segmentação espacial de flocos/substrato e regressão/metrologia física calibrada em nanômetros** (espessura $h$, número de camadas $N$, tamanho lateral médio, rugosidade $R_q$, área de defeitos). Pesos treinados em imagens $\Delta f$ de fenol halogenado não possuem invariância física transferível para degraus topográficos nanométricos.
5. **Lacuna sintético–real (*sim-to-real gap*):** Mesmo dentro de HR-AFM, os dados do *QUAM-AFM Lite* não contêm ruído térmico/$1/f$, *bow* de scanner, *drift*, linhas corrompidas (*scars*) ou troca aleatória de ponta durante a varredura.

### 7.3 Análise crítica do risco de *Data Leakage* na divisão por arquivo/imagem (80/20)
- **Mecanismo exato do vazamento no piloto:** No `QUAM-AFM Lite`, cada um dos 3 CIDs possui $24$ pilhas correspondentes às combinações $(A, \kappa)$ e, dentro de cada pilha, **$10$ imagens consecutivas separadas por apenas $\Delta z = 0{,}1\text{ \AA}$** ($10\text{ pm}$) da **exata mesma geometria atômica na mesma posição fixa na grade $256 \times 256$**.
- Quando o piloto divide as $720$ imagens aleatoriamente **por arquivo** ($576$ treino / $144$ validação), para praticamente toda imagem de validação em uma combinação $(A_i, \kappa_j, z_k)$, suas **vizinhas imediatas na mesma pilha** $(A_i, \kappa_j, z_k \pm 0{,}1\text{ \AA})$ — ou com $\Delta A = 0{,}2\text{ \AA}$ mantendo idêntica orientação espacial dos átomos de Br, Cl e O — caem no conjunto de treino!
- Como Carracedo-Cosme *et al.* (2022) explicitam (Figs. 3–4), a variação de contraste com $A$ é suave e a evolução ao longo de $\Delta z = 0{,}1\text{ \AA}$ é contínua. Logo, uma ResNet-18 com $\sim 11\text{ milhões}$ de parâmetros memoriza facilmente assinaturas de pixels por CID (quase um problema de busca por vizinho mais próximo), **inflando artificialmente a acurácia de validação interna para $100\%$** sem comprovar qualquer capacidade de generalização física — limitação que o próprio autor do piloto reconheceu honestamente nos Slides 13–14 (*"A divisão por arquivo pode misturar imagens da mesma pilha"* / *"O próximo teste deve reservar condições inteiras de simulação"*).
- **Regra metodológica correta para a dissertação:**
  - Para identificação molecular no QUAM-AFM: particionar por **CIDs disjuntos** (como recomendam Carracedo-Cosme *et al.*, 2022) ou, para teste de robustez operacional sobre moléculas fixas, reter **grupos inteiros de $(A, \kappa)$ / blocos inteiros de altura $z$** (*GroupKFold* por condição experimental/pilha).
  - Para AFM real de grafeno (ou C-AFM como em Harris *et al.*, 2025): **nunca dividir por *crops* ou fatias de uma mesma varredura**, nem por varreduras repetidas da mesma região; o particionamento deve ser estritamente agrupado por **amostra/síntese independente ou floco/região espacial disjunta** (*Group split* por lote/substrato).

### 7.4 Síntese estratégica para a dissertação (PPGCEM/UFCA)
Este par de trabalhos somado à auditoria do piloto `IVEFAC333.pptx` define os **limites de validade e a estratégia correta de Inteligência Artificial** para a dissertação:
1. **Redirecionamento estratégico:** Mostra objetivamente por que o piloto com `QUAM-AFM Lite` deve ser enquadrado apenas como **estudo exploratório inicial de familiarização com PyTorch/CNNs** (e exemplo didático de *domain shift* e *data leakage*), e **não** como modelo transferível para caracterização de grafeno por AFM.
2. **Onde *Deep Learning* realmente agrega valor em AFM de materiais 2D (Harris *et al.*, 2025):** Em vez de tentar substituir medições físicas de altura por classificação cega de imagens RGB, o uso de IA em AFM de grafeno/2D mostra vantagem demonstrável em: (i) **aceleração por super-resolução de varreduras esparsas** (reduzindo tempo de $15\text{--}30\text{ min}$ para $<3\text{--}5\text{ min}$ e preservando a ponta, especialmente para mapas elétricos de C-AFM ou mapeamento de grande área); e (ii) **segmentação semântica robusta** de flocos, dobras, contornos e defeitos acoplada a extração métrica determinística em nm/nA (seguindo a arquitetura de avaliação física de Harris *et al.*, 2025, e o rigor metrológico de Yao, 2017 / NPL AS 103).

---

## 8. Possíveis aplicações

**[Análise do Agente D — proposições futuras sem confundir com resultados publicados]**  

- **Reprodutibilidade imediata de experimento corretivo no piloto:** Antes de descartar a comparação PyTorch vs. TensorFlow sobre *QUAM-AFM Lite*, pode-se re-executar o piloto com **particionamento agrupado por pilha / amplitude $(A, \kappa)$** e **aumento de dados por rotação/translação** para medir a queda real de acurácia quando o vazamento intra-pilha é eliminado.
- **Para o grafeno esfoliado eletroquimicamente da UFCA:** Investigar um *pipeline* híbrido em duas camadas: (1) módulo determinístico baseado em dados brutos (nível de plano mascarado, *scars*, histograma bimodal de alturas de Yao/NPL para contar camadas e rugosidade $R_q$); e (2) módulo opcional de IA inspirado em *SparseC-AFM* (SwinIR/U-Net) treinado sobre dados reais de grafeno/GO com **validação cruzada agrupada por amostra/floco** e auditoria explícita de erros em métricas físicas (cobertura, densidade de defeitos e distribuição de espessuras), e não apenas PSNR/SSIM.

---

## 9. Evidências

- **Carracedo-Cosme *et al.* (2022) [texto completo `PMC9942089`]:** Seção *Methods / AFM Simulation Method* (FDBM@PPM, $\alpha=1$, $V_0=18\text{ eV}\cdot\text{\AA}^3$, $\delta=302\text{ pm}$, $\Delta z = 0{,}1\text{ \AA}$); Seção *Set of Structures* ($685.513$ moléculas, $8\text{--}85$ átomos, célula $24\text{ \AA}$, $z \le 1{,}83\text{ \AA}$, geometrias em fase gasosa); Seção *Operational Parameters* ($\kappa \in \{0{,}4; 0{,}6; 0{,}8; 1{,}0\}\text{ N/m}$, $A \in \{0{,}4\text{--}1{,}4\}\text{ \AA}$, $10$ distâncias $2{,}80\text{--}3{,}70\text{ \AA}$, Figs. 1–5); Seção *Data Organization and Indexing* (divisão por lista de CIDs) e *Data Availability* ($713\text{ GB}$ vs. *Lite* $1.755$ moléculas / $2\text{ GB}$).
- **QUAM-AFM Lite (`10.21950/BFAU11`):** Registro DataCite v1.1 ($421.200$ imagens, CC BY-NC-SA 4.0).
- **Harris *et al.* (2025) [texto completo + SPIE `10.1117/12.3067427` + GitHub]:** Seção 2.1–2.2 (PECVD $\text{MoS}_2$, Park NX-Hivac contact C-AFM, PPP-CONTSCPt $k=0{,}2\text{ N/m}$, $512\times 512$ em $2\times 2\text{ }\mu\text{m}$, SwinIR 6 RSTB / 6 STL / loss $L_1$); Seção 2.3 (exigência de *fine-tuning* local); Seção 3.1–3.4 e Figs. 4–6 (*scorecard* mostrando falha em *coverage percent* a $\times 4$ e empate próximo ao RNAN em $\times 4$/$\times 16$, além de $>11\times$ ganho de tempo e inviabilidade $\mathcal{O}(N^3)$ do GPR em $\times 64$); tabela de dados brutos no GitHub (`UNITES-Lab/sparse-cafm`).
- **Piloto `IVEFAC333.pptx`:** Slides 2–3 (CIDs 16268, 19859, 69670 de $\text{C}_6\text{H}_4\text{BrClO}$), Slide 4 e 14 (motivação em grafeno esfoliado eletroquimicamente), Slide 11 (divisão 80/20 por arquivo: 576 treino / 144 validação), Slide 13 (100% validação PyTorch e ressalva sobre mistura de pilhas).

---

## 10. Prioridade de estudo

**Alta.** **Carracedo-Cosme *et al.* (2022)** tem prioridade **Alta (crítica/diagnóstica)** especificamente para fundamentar a autocrítica metodológica sobre o piloto `IVEFAC333.pptx` (*domain shift* e *data leakage*); **Harris *et al.* (2025)** tem prioridade **Média-Alta** como referência de fronteira do estado da arte (2025) sobre onde *deep learning* realmente resolve gargalos experimentais em AFM de materiais 2D (aceleração por subamostragem e reconstrução multimodal altura + corrente).
