# Banco de Questões Técnicas para Defesa e Estudo — Seminário I (`17/11/2026`)

Este guia reúne perguntas técnicas difíceis que professores de Ciência e Engenharia de Materiais (e de Computação Científica) do **PPGCEM/UFCA** provavelmente farão na apresentação de `17/11/2026`, com respostas diretas, fundamentadas na literatura verificada e **sem ocultação de limitações**.

---

## 1. Escopo do Projeto, Multimodalidade e Fase Investigativa

### P1. *Por que vocês não escolhem apenas uma técnica (ex.: só MEV ou só DRX) em vez de citar DRX, MEV e AFM? Elas não dão a mesma resposta sobre o grafeno?*
- **Resposta direta:** **Não — DRX, MEV e AFM não são intercambiáveis.** Elas sondam interações físicas, escalas e grandezas distintas:
  - **DRX** é uma sonda **volumétrica (média de conjunto)** de periodicidade cristalina 3D e empilhamento ao longo de $c$ ($d_{002}$, domínios coerentes $L_c, L_a$, fases residuais de grafite/GO/rGO), mas **não enxerga flocos individuais isolados** nem mede dimensões laterais reais de nanoplaquetas polidispersas (Li, Lu & Xia, 2007; Holzwarth & Gibson, 2011).
  - **MEV** é uma sonda **planar de superfície em alta vazão** ($\sim 10\text{ nm}$ de resolução de borda — Zhou et al., 2016), padronizada internacionalmente (`ISO/TS 21356-1`, `VAMAS TWA 41`) para medir a **distribuição estatística de tamanho lateral e morfologia de $\ge 200$ flocos isolados**; contudo, sua intensidade de elétrons secundários não fornece espessura absoluta universal sem calibração estrita de tensão, `WD`, detector `InLens` e substrato (Zhou et al., 2016; Huang & Gan, 2024).
  - **AFM** é uma sonda **topográfica/mecânica local** de alta resolução vertical ($<1\text{ nm}$), sendo a única das três a medir diretamente perfis de altura e rugosidade de flocos individuais ($\ge 20$ flocos no protocolo VAMAS), mas tem baixa vazão e sofre **erro sistemático de espessura aparente ($0{,}4\text{–}1{,}7\text{ nm}$ para monocamada)** por adsorvatos e regime de interação ponta–amostra (Nemes-Incze et al., 2008; Shearer et al., 2016; Backes et al., 2020).
- **Conclusão prática:** Somente o acoplamento criterioso define o que é mensurável em amostras reais (especialmente dispersões heterogêneas de esfoliação eletroquímica).

---

### P2. *Por que o software ainda está em fase investigativa se você já apresentou um piloto com redes neurais no IV EFAC (`IVEFAC333.pptx`) usando o `QUAM-AFM Lite`?*
- **Resposta direta e honesta:** O experimento em [`IVEFAC333.pptx`](file:///C:/Users/emer/dissertacao/Artigos/Apresentacoes_passadas/IVEFAC333.pptx) foi um **estudo exploratório didático de código/arquitetura** (`ResNet-18` em `PyTorch` vs. `TensorFlow`), **mas ele NÃO valida a caracterização de grafeno** por quatro razões técnicas objetivas identificadas na auditoria bibliográfica:
  1. **Incompatibilidade de domínio físico:** o dataset **`QUAM-AFM Lite`** (`10.21950/BFAU11`; Carracedo-Cosme et al., 2022) contém imagens **simuladas** de **nc-AFM em altura constante com ponta de CO em ultra-alto vácuo** resolvendo ligações intramoleculares de **3 pequenas moléculas orgânicas** (isômeros de bromoclorofenol: CIDs `16268`, `19859` e `69670`). Isso não tem relação física com AFM topográfico ambiente (*tapping* ou *PeakForce*) de flocos micrométricos de grafeno esfoliado eletroquimicamente em $\text{SiO}_2/\text{Si}$.
  2. **Incompatibilidade de tarefa:** classificar 3 classes moleculares fechadas não resolve segmentação de flocos, correção de plano, medida de altura de degrau ou contagem de camadas.
  3. **Vazamento de dados (*data leakage*) no protocolo de divisão:** conforme reconhecido no próprio slide 13 de `IVEFAC333.pptx`, a divisão aleatória `80/20` *por arquivo* ($576$ treino / $144$ validação) misturou diferentes alturas/amplitudes da **mesma pilha de simulação** entre treino e validação, explicando os $100\%$ de acurácia interna sem poder de generalização real.
  4. **Lacuna *sim-to-real* completa:** imagens ideais simuladas não contemplam adsorvatos, menisco capilar, deriva piezoelétrica, ponta dupla ou resíduos de eletrólito/solvente.
- **Por que estamos em fase investigativa:** Antes de escrever o software definitivo da dissertação, era indispensável estabelecer na literatura **o que cada técnica mede com rigor físico**, construir um **banco experimental próprio e padronizado do PPGCEM/UFCA** e definir protocolos de validação agrupada (`GroupKFold`) sem vazamento.

---

### P3. *Se o projeto trata de DRX, MEV e AFM, por que você afirma que técnicas como Raman, TEM e XPS continuam indispensáveis como referência (*ground truth*)?*
- **Resposta direta:** Porque **nenhuma das três técnicas principais confirma sozinha, de forma inequívoca e universal, todas as propriedades críticas do grafeno esfoliado**:
  - **Espectroscopia Raman** (`Ferrari & Basko, 2013`; `Backes et al., 2020`) é a referência rápida e não destrutiva para distinguir monocamada (`1L`, única lorentziana estreita em `2D`), bicamada (`2L`, 4 componentes) e poucas camadas (`<5–10L`), além de quantificar **densidade de defeitos** ($I(D)/I(G)$ nos Estágios 1 e 2) e dopagem/deformação — informação ausente no MEV morfológico e ambígua na altura aparente de AFM.
  - **TEM / HRTEM / SAED** (`Backes et al., 2020`, Sec. IX.1.3) fornece confirmação direta da cristalinidade hexagonal (SAED) e contagem absoluta de camadas por **franjas `(0002)` em bordas dobradas** (a baixa tensão $\le 80\text{ kV}$).
  - **XPS** (`Backes et al., 2020`, Sec. IX.2.3) é necessária na rota de **esfoliação eletroquímica** para quantificar a razão $C/O$ e grupos oxigenados ($\text{C–OH}, \text{C–O}, \text{C=O}$), distinguindo grafeno pouco oxidado de GO/rGO.
- **Uso no projeto:** No desenvolvimento de modelos computacionais para MEV, AFM ou DRX, **Raman/TEM/XPS atuam como padrão-ouro de rotulagem** das amostras de calibração; o software de rotina não precisa exigi-las em toda varredura se o protocolo estiver validado, mas a validação científica da dissertação depende delas.

---

## 2. Questões sobre DRX (Difração de Raios X)

### P4. *No laboratório, se o pico `(002)` do grafite ($\sim 26{,}5^\circ$) desaparecer ou ficar bem alargado e fraco após a esfoliação, podemos programar o software para classificar automaticamente a amostra como "grafeno monocamada"?*
- **Resposta direta:** **Absolutamente não.** Isso seria um erro físico grave. Como enfatizam o [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md) (Seção 3) e **Li, Lu & Xia (2007)**, o enfraquecimento, deslocamento ou desaparecimento do pico `(002)` pode resultar de:
  1. **Desordem turboestrática extrema** (empilhamento de múltiplas camadas sem coerência cristalográfica regular, com rotações/translações aleatórias e flutuações de $d_{002}$);
  2. **Baixa massa espalhadora / amostra muito diluída ou fina** no porta-amostra abaixo do limite de detecção do difratômetro;
  3. **Oxidação e esfoliação incompleta em GO/rGO** com formação de domínios amorfos ou curvados;
  4. **Efeitos de textura / geometria de incidência.**
- **O que o software pode medir em DRX com segurança:** posição e perfil do pico `(002)` (ou banda `(001)` em GO), espaçamento médio aparente $d_{002}$ via Lei de Bragg, largura corrigida (`FWHM` após subtração do alargamento instrumental), estimativa de tamanho de domínio coerente $L_c$ pela **Equação de Scherrer** (com ressalva explícita para microdeformação e desordem turboestrática) e detecção de grafite residual não esfoliado.

---

### P5. *Qual é a diferença entre "Equação de Scherrer" e "Equação de Debye-Scherrer", e por que a largura do pico `(002)` não dá diretamente o tamanho dos flocos que vemos no MEV?*
- **Resposta direta:**
  - Conforme **Holzwarth & Gibson (2011)** (`10.1038/nnano.2011.145`), a fórmula $\tau = K\lambda / (\beta\cos\theta)$ deve ser chamada exclusivamente de **Equação de Scherrer** (derivada por Paul Scherrer em 1918; Debye contribuiu para o método/câmara de pó, não para essa fórmula).
  - Ela mede o tamanho médio do **domínio de difração coerente** perpendicular aos planos `(hkl)` analisados: no pico `(002)` mede **$L_c$ (espessura média de empilhamento coerente ao longo do eixo $c$)**, não o diâmetro lateral dos flocos no plano basal! E mesmo $L_c$ fica subestimado se não descontarmos o **alargamento instrumental** ($\beta_{\text{inst}}$) e a **microdeformação / desordem turboestrática** (Li, Lu & Xia, 2007).

---

### P6. *Vocês vão treinar uma rede neural profunda simulando milhares de difratogramas CIF para identificar nossas amostras por DRX?*
- **Resposta direta:** **Não como única fonte nem com modelos pesados sem linha de base.** Dois artigos revisados por pares demonstram os limites dessa ideia:
  - **Oviedo et al. (2019)** comprovaram queda clara quando um modelo treinado apenas em difratogramas simulados é testado em padrões experimentais reais (**Caso 2 vs. Caso 3** na Tabela 1: a acurácia em grupo espacial da `a-CNN` cai de `99,1%` simulado para `80,2%` experimental sem dados reais, e métodos simples caem para `13–25%`), exigindo **aumento de dados fisicamente informado** (escalamento/eliminação periódica por orientação preferencial + deslocamento $2\theta$) e mistura com dados experimentais reais.
  - **Greasley & Hosein (2023)** mostraram que, com bancos experimentais pequenos ($N \approx 50$), algoritmos tradicionais leves como **SVM, Complement Naive Bayes (`CNB`) e `k-NN`** igualam ou superam redes neurais (`88,8%` vs. `88,3%` na Instância [2]; `87,9%` vs. `87,1%` na Instância [3] *sim-to-real*) treinando em **`0,03 s` vs. `67 s`** com maior interpretabilidade.
- *(Nota de transparência acadêmica: um preprint de 2026 sobre sim-to-real gap em PXRD, `Wang et al. arXiv:2608.22400v2`, constava na listagem exploratória inicial, mas foi **oficialmente retirado pelos autores** na auditoria de 16/11/2026 e descartado desta revisão.)*

---

## 3. Questões sobre MEV (Microscopia Eletrônica de Varredura)

### P7. *No MEV, se uma monocamada tem apenas um átomo de espessura, como conseguimos enxergá-la? Dá para determinar o número de camadas diretamente pelos níveis de cinza?*
- **Resposta direta:**
  - Enxergamos o grafeno no MEV porque os elétrons secundários (SE) têm energia cinética muito baixa (pico em $\sim 1{,}5\text{ eV}$), tornando seu escape extremamente sensível à **função trabalho superficial ($\Phi$)** e à **atenuação através das camadas superficiais** (IMFP $\lambda \approx 5{,}7\text{ nm}$), além dos elétrons retroespalhados (BSE) vindos do substrato (**Zhou et al., 2016**).
  - **Quanto a contar camadas pelo nível de cinza:** **não é universalmente automático.** Em `SiO2 (285 nm)/p-Si` com detector **`InLens`**, baixa corrente (`5–20 pA`), `WD = 4 mm` e `5 keV`, **Zhou et al. (2016)** distinguiram `1L` (`18 ± 1%`) de `2L` (`26 ± 2%`) até `~10` camadas (saturando próximo a `14L`). Porém, mudando a tensão para `1,5 keV` a monocamada quase desaparece (`+1%`), a `0,5 keV` o contraste **inverte** para claro (`+9%`), e em tensões convencionais (`15–20 kV`) quase não há contraste (**Huang & Gan, 2024**). Em substratos metálicos policristalinos (Cu), o contraste de canalização eletrônica (**ECC**) dos grãos ainda compete com o grafeno.
- **Implicação no software:** Qualquer ferramenta de análise MEV precisa ler/exigir metadados (`V_acc`, `WD`, tipo de detector `InLens` vs. `E-T`, substrato) e **não prometer contagem absoluta de camadas sem calibração local específica**. O uso metrológico universalmente validado do MEV é a **estatística de tamanho lateral e morfologia**.

---

### P8. *Por que não podemos simplesmente medir 10 ou 20 flocos bonitos no MEV para estimar o tamanho lateral, ou reutilizar a mesma lâmina no AFM em seguida?*
- **Resposta direta (protocolo `NPL/VAMAS TWA 41`, 2023 & `Chemello et al., 2025`):**
  1. **Viés de amostragem e distribuição lognormal:** flocos esfoliados seguem distribuições assimétricas **lognormais**; medir poucos flocos ou escolher visualmente os "mais fáceis/maiores" distorce drasticamente a média. O protocolo `VAMAS / ISO/TS 21356-1` exige medir **todos os flocos isolados elegíveis em cada campo até somar $\ge 200$ flocos** (pixel `< 10 nm`). Além disso, `Chemello et al. (2025)` provaram experimentalmente que a variação entre operadores na *mesma* imagem é apenas `2–4,6%`, mas trocar de região no mesmo *wafer* (ex.: perto vs. longe de *coffee rings*) gera **discrepância de até `~30%`**!
  2. **Proibição de MEV $\rightarrow$ AFM na mesma área:** o protocolo `NPL/VAMAS` (Sec. 4.1) explicita que **o feixe eletrônico do MEV deposita contaminação carbonácea na superfície**, alterando a espessura nanométrica medida posteriormente por AFM; além disso, MEV exige **Si com óxido nativo fino** (dissipar carga), enquanto AFM/óptica usa **$\text{SiO}_2\ (300 \pm 5\text{ nm})/\text{Si}$** (contraste interferencial).

---

## 4. Questões sobre AFM (Microscopia de Força Atômica)

### P9. *Por que um floco de grafeno monocamada ($d = 0{,}335\text{ nm}$) aparece frequentemente com $0{,}8\text{–}1{,}7\text{ nm}$ no AFM, e como evitar que o software erre o número de camadas?*
- **Resposta direta:**
  - **Nemes-Incze et al. (2008)** demonstraram que no modo *tapping* em ar ambiente há dois regimes distintos na curva amplitude–distância (atrativo, dominado por forças capilares de água adsorvida, e repulsivo). Como a transição ocorre em amplitudes livres diferentes sobre $\text{SiO}_2$ ($\sim 21\text{ nm}$) e sobre grafeno ($\sim 25\text{–}26\text{ nm}$), operar com amplitude livre baixa no regime atrativo introduz um **erro de $\sim 0{,}8\text{–}1{,}0\text{ nm}$**, fazendo uma monocamada medir $\sim 1\text{ nm}$ (e até causando saltos aleatórios dentro da mesma imagem).
  - Somam-se a isso a **camada de adsorvato interfacial** (solvente/surfactante/água aprisionada sob o floco — `Shearer et al., 2016`; `Backes et al., 2020`, que citam $1\text{–}2\text{ nm}$ em LPE) e o **efeito de convolução de ponta** nas bordas laterais (raio de ponta $5\text{–}15\text{ nm}$).
- **Mitigação experimental e computacional:** operar no regime repulsivo (ou *PeakForce tapping* reduzindo o erro da 1ª camada para $0{,}1\text{–}0{,}3\text{ nm}$, conforme `Shearer et al., 2016`), calibrar o degrau 1L usando **degraus internos grafeno–sobre–grafeno** (Nemes-Incze Fig. 1c; Backes Sec. IX.1.2.1), aplicar nivelamento de plano **mascarando os flocos** (NPL/VAMAS Sec. 5.3.2), excluir artefatos (*double-tip*, *flying tip*, dobras) e sempre reportar a altura em **nanômetros com incerteza** (histograma/3 perfis), mantendo a conversão para $N$ condicionada à calibração e à conferência por Raman.

---

## 5. Questões de Computação Científica, IA e Originalidade

### P10. *Por que usar Visão Computacional / Deep Learning se `OpenCV`/`scikit-image` já possuem limiarização de Otsu e Watershed, e já existem o `ImageJ/Fiji` e o `Gwyddion`?*
- **Resposta direta:**
  - **Onde algoritmos clássicos bastam vs. onde falham:** em imagens limpas, isoladas e com iluminação uniforme, Otsu + morfologia + `regionprops` (`scikit-image`) são rápidos, determinísticos e excelentes para extrair `Área`, `ECD`, `minFeret/maxFeret`, `L, W` e circularidade (como no fluxo manual de Chemello et al., 2025 no `Fiji`). Porém, **Masubuchi et al. (2020)** (Fig. 2) e **Holm et al. (2020)** mostram que regras fixas quebram facilmente diante de pequenas quedas de iluminação/contraste, gradientes de fundo, resíduos de solvente/fita adesiva e **flocos sobrepostos/encostados** (onde Otsu/componentes conexos fundem partículas e *Watershed* super-segmenta flocos irregulares).
  - **Onde DL/ML ajuda com cautela:** **U-Net** com perda ponderada (Saito et al., 2019) ou **Mask R-CNN** (Masubuchi et al., 2020) automatizam segmentação robusta sob variação de microscópio, enquanto **modelos clássicos de ML (`SVM`, `CNB`, `k-NN`)** superam ou igualam redes neurais quando há poucos dados rotulados (Greasley & Hosein, 2023).
  - **Originalidade realista da dissertação (sem reinventar a roda):** O papel do projeto **não** é competir com o `Gwyddion` como editor genérico de SPM nem com o `GSAS-II` para Rietveld cristalográfico completo, nem repetir triagem óptica RGB já resolvida por `Masubuchi et al. (2020)`. A oportunidade científica real identificada na revisão é:
    1. **Automatizar o protocolo metrológico padronizado `ISO/TS 21356-1` / `VAMAS TWA 41` em micrografias MEV** (leitura de barra de escala/metadados TIFF, segmentação de instâncias separando flocos isolados dos sobrepostos, cálculo simultâneo de `ECD_A1`, `Feret ratio`, bissetriz `L/W`, verificação de resolução mínima de pixel, ajuste automático de histogramas lognormais $\ge 20$ *bins* em dezenas de campos para eliminar o viés de amostragem de até $30\%$ e economizar horas de marcação manual no `Fiji`);
    2. **Integrar pré-processamento e extração padronizada de perfis em AFM** (mascaramento de flocos antes do *plane flattening*, detecção heurística/estatística de artefatos e histograma de degraus com incerteza) e **análise exploratória assistida em DRX** (ajuste de `(002)` com subtração de fundo/alargamento instrumental e classificadores interpretáveis calibrados para amostras locais de **esfoliação eletroquímica do PPGCEM/UFCA**);
    3. **Garantir rigor metodológico de validação (`GroupKFold` por amostra/lote, sem *data leakage*)** sobre dados experimentais reais do grupo.
