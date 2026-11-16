# Fichamento 05 — Produção Mundial de Flocos de Grafeno e Protocolos de Caracterização Estatística (Kauling et al., 2018; Backes et al., 2020)

## 1. Identificação bibliográfica

### Referência Principal
- **Título:** The Worldwide Graphene Flake Production
- **Autores:** Alan P. Kauling, Andressa Thais Seefeldt, Diego P. Pisoni, Roshini C. Pradeep, Ricardo Bentini, Ricardo V. B. Oliveira, Kostya S. Novoselov, A. H. Castro Neto
- **Ano:** 2018 (publicado online em 13 set. 2018; edição impressa nov. 2018)
- **Periódico:** *Advanced Materials*, v. 30, n. 44, art. e1803784 (`article-number: 1803784`)
- **DOI:** `10.1002/adma.201803784`
- **URL oficial:** <https://doi.org/10.1002/adma.201803784> *(repositório institucional Green OA da Universidade de Manchester indexado, porém sem PDF direto recuperado nesta etapa)*
- **Citações verificadas (OpenAlex):** 381

### Referência Complementar de Padronização e Metrologia
- **Título:** Production and processing of graphene and related materials
- **Autores:** Claudia Backes, Amr M. Abdelkader, et al. *(consórcio amplo de coautores incluindo Andrea C. Ferrari e M. García-Hernández)*
- **Ano:** 2020 (29 jan. 2020)
- **Periódico:** *2D Materials*, v. 7, n. 2, art. 022001 (283 p.)
- **DOI:** `10.1088/2053-1583/ab1e0a`
- **URL oficial:** <https://doi.org/10.1088/2053-1583/ab1e0a> (PDF de acesso aberto CC-BY: <https://iopscience.iop.org/article/10.1088/2053-1583/ab1e0a/pdf>)
- **Citações verificadas (OpenAlex):** 517
- **Arquivo local lido:** `PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md`

---

## 2. Problema investigado

### Fatos extraídos dos artigos
- **Kauling et al. (2018):** A rápida expansão comercial do grafeno gerou dispersões e pós comercializados como "grafeno" sem verificação padronizada de espessura, distribuição de tamanho lateral, pureza química e grau de defeitos. O artigo audita a produção real de flocos por **60 produtores** em escala mundial, avaliando se os materiais vendidos correspondem efetivamente a grafeno (ou grafeno de poucas camadas) e demonstrando que a classificação comercial vigente é inadequada por ignorar a natureza estatística da esfoliação em fase líquida (LPE).
- **Backes et al. (2020):** Em consonância com essa lacuna metrológica (e visando orientar rotas industriais e normas como o consórcio *Graphene Flagship*), o documento de 283 páginas sistematiza os métodos de produção em massa (esfoliação líquida, oxidação/redução, esfoliação eletroquímica), o fracionamento pós-síntese e os **protocolos experimentais padronizados** de microscopia (AFM, TEM), espectroscopia (Raman, XPS) e difração (XRD) capazes de produzir **estatísticas confiáveis de tamanho lateral ($L, W$) e espessura ($N$)** sem viés amostral.

### Análise crítica
- Este par forma o **núcleo motivador direto da dissertação**: enquanto Kauling et al. (2018) comprovam empiricamente que o mercado global entrega majoritariamente *microplaquetas grafíticas* de baixa qualidade rotuladas incorretamente como grafeno — e exigem classificação por **funções de distribuição** de camadas e tamanho de floco —, Backes et al. (2020) definem exatamente **quantos flocos contar ($\ge 100\text{–}150$)**, como evitar vieses de secagem e como ponderar médias estatísticas. É exatamente esse gargalo de contagem manual laboriosa em microscopia que justifica a automatização via MEV + processamento de imagens/visão computacional.

---

## 3. Fundamentação

### Fatos extraídos dos artigos
- **Kauling et al. (2018):** Fundamenta-se na **natureza estatística da esfoliação em fase líquida (LPE)**, segundo a qual qualquer processo escalável de esfoliação gera um *ensemble* polidisperso de espessuras e dimensões laterais, impossibilitando descrever o produto por um número único nominal de camadas e requerendo funções de distribuição estatística para $N$ e tamanho de floco.
- **Backes et al. (2020):**
  - Na esfoliação em fase líquida (`II.2`, pp. 24–27), a polidispersidade típica abrange comprimentos laterais de dezenas de nanômetros a dezenas de micrômetros (`10s nm–10s µm`) e espessuras $N$ variando de monocamada a centenas de camadas (`1–100s`), com rendimento mássico sem seleção ($Y_M$) frequentemente inferior a $1\%$.
  - Para amostras de área específica medida por BET ($S_{\text{BET}}$), relaciona-se o número médio de camadas à área superficial teórica do grafeno ($N \approx 2630 / S_{\text{BET}}$, p. 37).
  - Na metrologia estatística (`IX.1.2.1`, pp. 188–192), diferencia a média aritmética simples de número de camadas da **média ponderada pela fração volumétrica**:
    $$\langle N \rangle_{Vf} = \frac{\sum N^2 L W}{\sum N L W}$$
    evitando que flocos finos e pequenos superestimem artificialmente a qualidade de um lote onde a maior parte da massa está em microplaquetas espessas.

### Análise crítica
- A formulação de $\langle N \rangle_{Vf}$ em Backes et al. (2020) e o diagnóstico estatístico de Kauling et al. (2018) demonstram por que métricas simples (como média aritmética de diâmetros ou inspeção visual de $5\text{–}10$ flocos em MEV) são metodologicamente insuficientes: análises automatizadas por visão computacional precisam extrair distribuições completas (frequentemente log-normais) de $L$ e $W$ sobre grandes populações de flocos para evitar interpretações distorcidas.

---

## 4. Metodologia

### Fatos extraídos dos artigos
- **Kauling et al. (2018):** Conforme reportado no resumo verificado, amostras comerciais de **60 produtores globais** foram caracterizadas sistematicamente combinando microscopia eletrônica / MEV (EM/SEM), microscopia de força atômica (AFM), espectroscopia Raman, análise elementar, espectroscopia de fotoelétrons excitados por raios X (XPS) e microscopia eletrônica de transmissão (TEM).
- **Backes et al. (2020) — Seções selecionadas analisadas no texto completo:**
  - **Produção e fracionamento:** Comparação de LPE (`II.2`, pp. 24–27), óxido de grafeno / óxido de grafeno reduzido (`II.3`, pp. 34–37; monitoramento por XRD da queda do pico `(001)` do GO e emergência de `(002)` do rGO, p. 37), esfoliação eletroquímica (`II.5–II.6`, pp. 42–46; comparação por AFM em HOPG na Fig. II.21) e seleção pós-síntese por centrifugação em cascata líquida (*Liquid Cascade Centrifugation* — LCC) e ultracentrifugação por gradiente de densidade isopicnica (DGU) (`III.1`, pp. 48–51, Tabela III.1).
  - **Protocolo AFM (`IX.1.2.1`, pp. 188–192):** Deposição por gotejamento (*drop-cast*) sobre substratos aquecidos a $50\text{–}70\ ^\circ\text{C}$ acima do ponto de ebulição do solvente; medição rápida ($<10\ \text{min}$/varredura) considerando que monocamadas apresentam altura aparente de $1\text{–}2\ \text{nm}$ por solvente/substrato; calibração interna por degraus de terraços (*terrace step-height*) combinada a confirmação por Raman/fotoluminescência (PL); contagem estatística mínima de **$\ge 100\text{–}150$ flocos**; verificação de ajuste a histograma log-normal para detectar viés amostral.
  - **Protocolo TEM (`IX.1.3`, pp. 198–200):** Contagem de comprimento e largura em **$\sim 150$ flocos**; determinação de camadas por franjas `(0002)` em bordas dobradas via HREM; operação abaixo de $80\ \text{kV}$ para evitar dano balístico (*knock-on damage*) no grafeno.
  - **Protocolo Raman e XPS (`IX.2.1`, pp. 210–213; `IX.2.3`, pp. 220–221):** Quantificação de densidade de defeitos $n_D$ corrigida para dopagem (Eqs. IX.9–IX.10) e análise química superficial por XPS (profundidade $<10\ \text{nm}$), separando componentes `C 1s` $sp^2$ ($\sim 284{,}5\ \text{eV}$) e $sp^3$ ($\sim 285{,}0\ \text{eV}$).

### Análise crítica
- Nota-se uma lacuna significativa na literatura revisada em Backes et al. (2020): os protocolos detalhados de contagem estatística ($\ge 100\text{–}150$ flocos) foram formalizados explicitamente para **AFM** e **TEM**, ambos de baixo rendimento e custo operacional elevado, enquanto **MEV** aparece apenas como ferramenta qualitativa/complementar na auditoria de Kauling et al. (2018). Isso abre espaço original e bem delimitado para investigar protocolos semiautomáticos ou automáticos baseados em **MEV + visão computacional** capazes de atingir ou superar $N \ge 150$ flocos em fração do tempo de AFM/TEM.

---

## 5. Resultados

### Fatos extraídos dos artigos
- **Kauling et al. (2018):**
  - Demonstrou-se que **a maioria dos 60 produtores globais fornece microplaquetas grafíticas de baixa qualidade** em vez de grafeno genuíno.
  - Evidenciou-se que a taxonomia comercial vigente é incorreta, propondo-se a substituição por classificação baseada em **funções de distribuição do número de camadas e do tamanho lateral dos flocos**, acompanhada de apelo por normas rigorosas de qualidade.
- **Backes et al. (2020):**
  - **Esfoliação eletroquímica (`II.5–II.6`, pp. 42–46):** Pode atingir rendimentos em peso ($Y_w$) de até **$80\%$**, mas enfrenta desafios persistentes de polidispersidade e reempilhamento (*restacking*).
  - **Óxido de grafeno / rGO (`II.3`, pp. 34–37):** O GO atinge razão atômica `C:O` de até `2:1`, exigindo redução acompanhada pela evolução de XRD (`(001)` $\to$ `(002)`).
  - **Fracionamento por tamanho e espessura (`III.1`, pp. 48–51, Tabela III.1):** A centrifugação em cascata líquida separa frações de grafeno de poucas camadas (FLG): em colato de sódio (SC), aceleração de $550\ g$ seleciona flocos com $360\ \text{nm}$ e $8{,}1$ camadas médias, enquanto $21{.}000\ g$ isola flocos menores e mais finos ($90\ \text{nm}$, $3{,}3$ camadas); em NMP, $80\ g$ retém flocos de $\sim 1000\ \text{nm}$ versus $160\ \text{nm}$ a $1800\ g$. Por ultracentrifugação isopicnica (DGU), obtém-se fração enriquecida de $\sim 80\%$ de monocamada (SLG).
  - **Metrologia estatística (`IX.1.2.1`, `IX.1.3`):** Histogramas de dimensões laterais e espessura seguem tipicamente distribuições log-normais, requerendo amostragem de $\ge 100\text{–}150$ objetos no AFM e $\sim 150$ objetos no TEM para reprodutibilidade.

### Análise crítica
- Os dados da Tabela III.1 de Backes et al. (2020) ilustram concretamente o acoplamento físico tamanho–espessura na LPE: frações maiores ($360\ \text{nm}$ a $1000\ \text{nm}$) tendem a conter maior número de camadas ($8{,}1\ \text{L}$), enquanto frações muito finas ($3{,}3\ \text{L}$) possuem tamanho lateral pequeno ($90\ \text{nm}$). Essa correlação reforça a necessidade de avaliar distribuições bidimensionais conjuntas de tamanho lateral e morfologia em amostras reais.

---

## 6. Limitações

### Fatos extraídos dos artigos
- **Kauling et al. (2018):** *(Baseado apenas no resumo e metadados verificados)* Os resultados detalhados por produtor individual, distribuições quantitativas de razão `C/O` em XPS e valores específicos de $I(D)/I(G)$ por fornecedor não constam no resumo público; ademais, o texto integral não está disponível em acesso aberto imediato no acervo local.
- **Backes et al. (2020):**
  - Na deposição de dispersões para AFM (`IX.1.2.1`, pp. 188–192), a evaporação lenta do solvente induz agregação e viés de tamanho/espessura se o substrato não for mantido $50\text{–}70\ ^\circ\text{C}$ acima do ponto de ebulição do solvente; além disso, a altura aparente da monocamada por AFM ($1\text{–}2\ \text{nm}$) excede a espessura cristalográfica ($0{,}34\ \text{nm}$) devido a filmes residuais e interações ponta–substrato.
  - No TEM (`IX.1.3`, pp. 198–200), tensões de aceleração $\ge 80\ \text{kV}$ provocam defeitos por dano balístico (*knock-on*), exigindo operação abaixo de $80\ \text{kV}$ e tornando o preparo e a contagem de $\sim 150$ flocos demorados.
  - O documento não consolida um protocolo automático padronizado baseado exclusivamente em segmentação computacional de imagens MEV para contagem de distribuição lateral em larga escala.

### Análise crítica
- O custo de leitura manual de $\ge 150$ flocos em AFM ou TEM explica por que muitos trabalhos experimentais ainda reportam médias de poucos flocos selecionados subjetivamente ("viés de escolha"), perpetuando o cenário criticado por Kauling et al. (2018). Na dissertação, superar essa limitação usando segmentação automatizada em MEV (sem inferir espessura diretamente do brilho de imagem MEV sem calibração/Raman/AFM) precisa manter explícita a fronteira física entre o que o MEV mede (distribuição lateral $L, W$, área, fator de forma, aglomeração) e o que exige AFM/Raman ($N$, defeitos).

---

## 7. Contribuição para a dissertação

### Fatos extraídos dos artigos
- Fornece a evidência empírica global (auditoria de 60 produtores por Kauling et al., 2018) de que a caracterização padronizada por **funções de distribuição estatística** de flocos é urgente e incontornável.
- Entrega parâmetros metrológicos concretos de Backes et al. (2020): tamanho amostral mínimo ($\ge 100\text{–}150$ flocos), forma esperada das distribuições (log-normal), métrica ponderada por volume ($\langle N \rangle_{Vf}$), temperaturas de deposição sem agregação por solvente e limites de calibração XPS (`C 1s` $sp^2 \approx 284{,}5\ \text{eV}$ vs. $sp^3 \approx 285{,}0\ \text{eV}$) e Raman corrigido por dopagem.

### Análise crítica
- Este fichamento ancora o **Capítulo de Revisão Bibliográfica e Justificativa Metodológica** da dissertação: permite formular a hipótese de que protocolos de visão computacional aplicados a micrografias MEV podem reproduzir os requisitos de amostragem populacional de Backes et al. (2020) ($n \ge 150$ flocos por amostra) para caracterização lateral estatística reprodutível, servindo como ferramenta de triagem alinhada às exigências de controle de qualidade industrial apontadas por Kauling et al. (2018).

---

## 8. Possíveis aplicações

### Fatos extraídos dos artigos
- Criação de protocolos de certificação de pós e dispersões comerciais de grafeno e grafeno de poucas camadas baseados em distribuições estatísticas completas de tamanho lateral e número de camadas; fracionamento controlado de dispersões LPE via LCC/DGU para tintas condutoras, compósitos poliméricos, eletrodos e revestimentos de barreira.

### Análise crítica
- Em laboratórios brasileiros de ciência e engenharia de materiais (como no âmbito do PPGCEM/UFCA), onde a disponibilidade de tempo em AFM/TEM de alta resolução é frequentemente restrita em comparação ao acesso a MEV e Raman, a integração de diretrizes estatísticas de Backes et al. (2020) com triagem automatizada de imagens MEV oferece uma rota prática e de baixo custo para auditoria de insumos comerciais de grafeno.

---

## 9. Evidências

- **Declarações explícitas de base de leitura:**
  - **Kauling et al. (2018):** **Análise realizada apenas a partir do resumo e metadados verificados** *(pendente recuperação do texto integral via acesso institucional Portal CAPES/UFCA; registro OpenAlex aponta apenas página institucional de repositório sem PDF direto)*.
  - **Backes et al. (2020):** **Análise realizada a partir do texto completo** *(leitura direta das seções relevantes do texto integral de 283 páginas extraído em `_scratch/textos_extraidos/Backes_2020_Production_and_Processing_of_Graphene_and_Related_Materials.md`)*.
- **Evidências verificadas em Kauling et al. (2018) [resumo e metadados]:**
  - Amostragem de **60 produtores** mundiais; técnicas reportadas (EM/SEM, AFM, Raman, análise elementar, XPS, TEM); identificação de natureza estatística da LPE; proposta de classificação por funções de distribuição de número de camadas e tamanho de floco; diagnóstico de predominância de microplaquetas grafíticas.
- **Evidências verificadas no texto completo de Backes et al. (2020):**
  - **Seção `II.2` (pp. 24–27):** Faixas de dimensões laterais (`10s nm–10s µm`), espessuras ($N = 1\text{–}100\text{s}$) e rendimento sem fracionamento ($Y_M < 1\%$) em LPE.
  - **Seção `II.3` (pp. 34–37):** Razão máxima `C:O` de `2:1` em GO; evolução dos picos de XRD `(001)` do GO e `(002)` do rGO (p. 37); relação $N \approx 2630/S_{\text{BET}}$.
  - **Seções `II.5–II.6` e Fig. II.21 (pp. 42–46):** Esfoliação eletroquímica com $Y_w$ até $80\%$, polidispersidade/reempilhamento e comparação por AFM em HOPG.
  - **Seção `III.1` e Tabela III.1 (pp. 48–51):** Fracionamento por LCC em SC (`550 g -> 360 nm, 8,1 L` vs. `21.000 g -> 90 nm, 3,3 L`) e NMP (`80 g -> 1000 nm` vs. `1800 g -> 160 nm`), além de DGU isopicnica ($\sim 80\%$ SLG).
  - **Seção `IX.1.2.1` (pp. 188–192):** Protocolo AFM ($<10\ \text{min}$, substratos aquecidos $50\text{–}70\ ^\circ\text{C}$ acima do ponto de ebulição do solvente, altura aparente SLG $1\text{–}2\ \text{nm}$, calibração em degraus + Raman/PL, contagem $\ge 100\text{–}150$ flocos, verificação log-normal, $\langle N \rangle_{Vf} = \sum N^2 L W / \sum N L W$).
  - **Seção `IX.1.3` (pp. 198–200):** Protocolo TEM ($\sim 150$ contagens, franjas `(0002)` em bordas dobradas, limite $< 80\ \text{kV}$ contra dano *knock-on*).
  - **Seções `IX.2.1` e `IX.2.3` (pp. 210–213, Eqs. IX.9–IX.10; pp. 220–221):** Cálculo de $n_D$ Raman corrigido para dopagem; XPS ($< 10\ \text{nm}$) com energias de ligação `C 1s` $sp^2 \sim 284{,}5\ \text{eV}$ e $sp^3 \sim 285{,}0\ \text{eV}$.

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta**
- **Justificativa:** Referência central para justificar o problema industrial e metrológico da caracterização de grafeno comercial e esfoliado. Recomenda-se fortemente obter o PDF integral de Kauling et al. (2018) via Portal CAPES/UFCA para extrair os critérios detalhados de classificação por produtor, complementando a base metrológica já obtida no texto completo de Backes et al. (2020).
