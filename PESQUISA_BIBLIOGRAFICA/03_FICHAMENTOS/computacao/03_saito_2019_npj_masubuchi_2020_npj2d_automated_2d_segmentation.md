# Fichamento 03 — Segmentação Automatizada de Materiais 2D por Aprendizado Profundo: Saito et al. (2019) e Masubuchi et al. (2020)

> **Nível de leitura declarado (Seção 8 — `PROMPT_MESTRE.md`):**
> - **Saito et al. (2019):** **Texto completo lido** via extração integral (`_scratch/textos_extraidos/Saito_2019_Deep_Learning_Quality_Filtering_2D_Crystals.md`, 259 linhas, incluindo referências e detalhes experimentais/arquiteturais).
> - **Masubuchi et al. (2020):** **Texto completo lido** diretamente do artigo publicado (`ARTIGOS_PDF/Masubuchi_2020_Deep_Learning_Image_Segmentation_2D_Materials.pdf`, 9 páginas, pp. 1–9, e texto extraído correspondente).

---

## 1. Identificação bibliográfica

### Obra A — Saito et al. (2019) `[Extraído do artigo]`
- **Autores:** Yu Saito, Kento Shin (indexado como *Shin Kento* em metadados), Kei Terayama, Shaan A. Desai, Masaru Onga, Yuji Nakagawa, Yuki M. Itahashi, Yoshihiro Iwasa, Makoto Yamada, Koji Tsuda.
- **Ano:** 2019.
- **Título completo:** *Deep-learning-based quality filtering of mechanically exfoliated 2D crystals*.
- **Periódico:** *npj Computational Materials*, vol. 5, artigo 124 (2019).
- **DOI:** `10.1038/s41524-019-0262-4`
- **Link oficial:** <https://doi.org/10.1038/s41524-019-0262-4>
- **Repositório de código/dados informado:** <https://github.com/xinkent/mos2_segmentation>
- **Nível de leitura:** Texto completo.

### Obra B — Masubuchi et al. (2020) `[Extraído do artigo]`
- **Autores:** Satoru Masubuchi, Eisuke Watanabe, Yuta Seo, Shota Okazaki, Takao Sasagawa (T. Sasagawa), Kenji Watanabe, Takashi Taniguchi, Tomoki Machida.
- **Ano:** 2020.
- **Título completo:** *Deep-learning-based image segmentation integrated with optical microscopy for automatically searching for two-dimensional materials*.
- **Periódico:** *npj 2D Materials and Applications*, vol. 4, artigo 3 (2020).
- **DOI:** `10.1038/s41699-020-0137-z`
- **Link oficial:** <https://doi.org/10.1038/s41699-020-0137-z>
- **Repositório de código/dados/pesos informado:** <https://github.com/tdmms/>
- **Nível de leitura:** Texto completo.

---

## 2. Problema investigado

### Obra A — Saito et al. (2019) `[Extraído do artigo]`
- A esfoliação mecânica (*Scotch-tape method*) produz flocos de materiais bidimensionais ($\text{MoS}_2$, grafeno, entre outros) dispersos aleatoriamente sobre substratos $\text{SiO}_2/\text{Si}$ com ampla variação de espessura (monocamada, bicamada, multicamada espessa) e área útil reduzida.
- A triagem visual por microscopia óptica (MO) consome tempo elevado de especialistas e apresenta subjetividade em operadores inexperientes; métodos clássicos de processamento de imagens (como *Bag-of-Visual-Words* — BoVW) e CNNs pixel a pixel anteriores requeriam ajuste manual ou apresentavam perda de contexto espacial e baixa precisão em condições heterogêneas de contraste.

### Obra B — Masubuchi et al. (2020) `[Extraído do artigo]`
- A fabricação de heteroestruturas de van der Waals demanda localização sistemática de flocos esfoliados (grafeno/grafite, h-BN, $\text{MoS}_2$, $\text{WTe}_2$) em áreas centimétricas ($\sim 1 \times 1\ \text{cm}^2$) sob microscópio óptico motorizado.
- Algoritmos baseados em regras heurísticas (limiarização por contraste/cor relativa ao substrato) exigem busca manual prévia de um floco de referência ($\ge 30\ \text{min}$) e recalibração a cada batelada de esfoliação, além de colapsarem completamente sob variações de intensidade de iluminação — atrasando o fluxo e degradando cristais sensíveis ao ar (como $\text{BSCCO}$).
- Segmentadores puramente semânticos não distinguem instâncias individuais quando múltiplos flocos distintos (ou camadas contíguas) compartilham a mesma classe.

### `[Análise crítica — Agente E]`
Os dois trabalhos marcam a transição metodológica da **segmentação semântica em pequeno porte** (U-Net para triagem de qualidade em Saito et al., 2019) para a **segmentação de instâncias integrada ao hardware do microscópio em escala de chip** (Mask R-CNN com *ResNet101* em Masubuchi et al., 2020). Ambos expõem, contudo, uma tensão central para caracterização científica rigorosa: na caracterização de materiais 2D, a microscopia óptica atua primordialmente como **triagem de região de interesse (ROI)** por contraste interferométrico no substrato $\text{SiO}_2/\text{Si}$ — não substituindo medições metrológicas físicas diretas de espessura e estrutura cristalina (AFM, espectroscopia Raman, MEV ou DRX).

---

## 3. Fundamentação

### `[Extraído dos artigos]`
1. **Contraste interferométrico óptico em $\text{SiO}_2/\text{Si}$:** Em microscopia óptica de campo claro (*bright-field*), a interferência múltipla na camada dielétrica de $\text{SiO}_2$ (tipicamente $290$–$300\ \text{nm}$ ou $90\ \text{nm}$) modula o contraste RGB de acordo com a espessura atômica (1L, 2L, poucas camadas, espesso), permitindo rotulagem física assistida por AFM como referência (Saito et al., 2019).
2. **Segmentação semântica via U-Net (Ronneberger et al., 2015) com função de perda ponderada:** Saito et al. (2019) empregam arquitetura codificador-decodificador simétrica com *skip connections* e introduzem ponderação de entropia cruzada via *median frequency balancing* ($w_k$) para compensar o desbalanceamento extremo entre pixels de substrato/flocos espessos e pixels raros de monocamada/bicamada.
3. **Segmentação de instâncias via Mask R-CNN com backbone ResNet101:** Masubuchi et al. (2020) combinam a detecção de regiões propostas (*Region Proposal Network* — RPN), alinhamento subpixel (*ROI Align*) e três cabeçotes paralelos (classificação, regressão de *bounding box* e máscara FCN por instância), com perda multitarefa ponderada $(\alpha, \beta, \gamma) = (0{,}6,\ 1{,}0,\ 1{,}0)$.
4. **Aprendizado por transferência em dois estágios:** Inicialização em pesos pré-treinados no MS-COCO, seguida por treinamento no conjunto misto de materiais 2D e ajuste fino (*fine-tuning*) específico por material, reduzindo o número de anotações exigidas e acelerando a convergência frente ao treinamento direto a partir do MS-COCO (Masubuchi et al., 2020, Fig. 4).

### `[Análise crítica — Agente E]`
Do ponto de vista computacional, a fundamentação de Saito et al. (2019) ilustra bem a relação custo-benefício em cenários de escassez extrema de dados ($24$–$30$ imagens): a U-Net já codifica contexto multiescala sem exigir um *backbone* profundo de 101 camadas, mas o *median frequency balancing* pode inflar falsos positivos da classe minoritária (monocamada) sobre ruído de fundo do *wafer*. Já Masubuchi et al. (2020) justificam o uso de Mask R-CNN (em vez de U-Net ou limiar de Otsu) pela necessidade operacional de separar instâncias individuais em um sistema ciberfísico de varredura automática — onde variações globais de luminância invalidam limiares fixos de intensidade.

---

## 4. Metodologia

### Obra A — Saito et al. (2019) `[Extraído do artigo]`
- **Aquisição e verdade de referência (*ground truth*):** Imagens de campo claro em $\text{SiO}_2(300\ \text{nm})/\text{Si}$ (microscópio Olympus BX51, objetiva $100\times$); espessuras confirmadas por AFM e contraste óptico.
- **Conjunto de dados e classes:**
  - $\text{MoS}_2$: $24$ imagens de treino e $11$ de teste.
  - Grafeno: $30$ imagens de treino e $14$ de teste.
  - Três classes pixel a pixel: monocamada (azul), bicamada (verde) e demais/substrato/espesso (preto).
- **Aumento de dados (*data augmentation*):** As $24$ imagens de treino de $\text{MoS}_2$ foram expandidas para $960$ recortes de $512 \times 512 \times 3$ por recorte aleatório (*random crop*), espelhamentos, rotação ($-90^\circ$ a $+90^\circ$), perturbação de matiz HSV ($\text{Hue} \pm 10$) e escalonamento de contraste ($\times 0{,}7$ a $1{,}3$). Testou-se ablação em $2 \times 2$: com/sem conversão para escala de cinza e com/sem ajuste de contraste.
- **Arquitetura U-Net detalhada (Fig. 4):** Entrada $512 \times 512 \times 3$; codificador com $14$ camadas ($4$ blocos de convoluções $3 \times 3$ + ReLU + *max pooling* $2 \times 2$ com *stride* $2$, progressão de canais $64 \rightarrow 128 \rightarrow 256 \rightarrow 512 \rightarrow 1024$ até mapa latente $16 \times 16 \times 1024$); decodificador com $18$ camadas ($4$ estágios de convolução de *upsampling* $2 \times 2$ + concatenação via *skip connection* + convoluções $3 \times 3$ + ReLU, com *dropout* de $50\%$ após os três primeiros *upsamplings*, finalizando com convolução $1 \times 1$ e *softmax*).
- **Treinamento e validação:** Otimizador Adam em *mini-batches*; busca em grade por validação cruzada *3-fold* (taxas de aprendizado $\{10^{-5}, 10^{-4}, 10^{-3}\}$, tamanhos de *batch* $\{1, 5, 10, 50, 100\}$, épocas $\{10, 30, 50, 100, 500\}$). Comparação com BoVW e CNN pixel a pixel (Fig. 2m–p, Supp. Table 3) e com $12$ avaliadores humanos não especialistas após treinamento rápido de $3\ \text{min}$.

### Obra B — Masubuchi et al. (2020) `[Extraído do artigo]`
- **Hardware e arquitetura de software:** Microscópio com platina motorizada $XY$ e autofoco (Chuo Precision), orquestrado em C++/Python/ROS com drivers HALCON, conectado em arquitetura cliente-servidor a GPU NVIDIA Tesla V100 ($32\ \text{GB}$) realizando inferência em $200\ \text{ms/imagem}$ (vazão efetiva integrada $\sim 1\ \text{fps}$).
- **Conjunto de dados (Fig. 3b):** Total de **$2.102$ imagens** ($1024 \times 1024\ \text{px}^2$, razão de aspecto preservada com *zero-padding*) contendo **$7.153$ objetos anotados**:
  - BN-$290\ \text{nm}$: $232$ imagens / $274$ objetos espessos;
  - BN-$90\ \text{nm}$: $121$ imagens / $182$ objetos ($13$ monocamadas, $111$ poucas camadas, $58$ espessos);
  - Grafite-$290\ \text{nm}$: $862$ imagens / $4.805$ objetos ($1.858$ monocamadas, $2.081$ poucas camadas, $866$ espessos);
  - $\text{MoS}_2$-$290\ \text{nm}$: $569$ imagens / $839$ objetos ($239$ monocamadas, $523$ poucas camadas, $77$ espessos);
  - $\text{WTe}_2$-$290\ \text{nm}$: $318$ imagens / $1.053$ objetos ($148$ monocamadas, $582$ poucas camadas, $323$ espessos).
  - Total por espessura: **$2.258$ monocamadas (1L)**, **$3.297$ poucas camadas (2–10L)** e **$1.598$ espessos (10–40L)**.
- **Rotulagem semiautomática e divisão:** Cerca de $80$ imagens iniciais de grafeno foram rotuladas manualmente para treinar uma Mask R-CNN preliminar usada como assistente de pré-anotação, corrigida via plataforma LabelBox ($20$–$30\ \text{s/imagem}$). Divisão aleatória $8:2$ treino/teste.
- **Treinamento (Keras/TensorFlow):** *Data augmentation* *online* (multiplicação de canais, rotações, espelhamentos e deslocamentos H/V). SGD (*momentum* $0{,}9$, *weight decay* $10^{-4}$), $4$ estágios $\times 30$ épocas ($500$ iterações/época; LRs $10^{-3}, 10^{-3}, 10^{-4}, 10^{-5}$; $\sim 12\ \text{h}$ em $4 \times$ NVIDIA V100).

### `[Análise crítica — Agente E]`
1. **Risco de vazamento de dados (*data leakage*) na divisão de splits:**
   - Em Saito et al. (2019), o conjunto de $\text{MoS}_2$ possui apenas $24$ imagens de treino e $11$ de teste, sendo o *tuning* feito em *3-fold CV* dentro das $24$ imagens (provavelmente antes de separar ou sem agrupamento explícito por chip/esfoliação no artigo). Se flocos da mesma fita/wafer aparecem em treino e teste, a métrica de contraste de substrato é otimista.
   - Em Masubuchi et al. (2020), o split $8:2$ é **aleatório em nível de imagem** (*random train/test split*), não agrupado por amostra física, chip ou sessão de microscopia (*GroupKFold*). Como imagens de um mesmo wafer compartilham espectro da lâmpada, balanço de branco, resíduos de fita adesiva e espessura exata de $\text{SiO}_2$, a avaliação $8:2$ interna tende a superestimar a acurácia em comparação a um ensaio verdadeiramente externo — embora os autores compensem parcialmente essa limitação testando em 3 microscópios inéditos e no escaneamento cego de $>2.300$ imagens de chip real.
2. **Desproporção computacional vs. métodos clássicos:** Masubuchi et al. exigiram $4\times$ V100 por $12\ \text{h}$ para treino e GPU V100 ($32\ \text{GB}$) dedicada para inferência em $200\ \text{ms}$. Em contraste, segmentação clássica via `scikit-image` (Otsu + morfologia + *watershed*) roda em milissegundos em CPU, desde que a iluminação seja controlada — exatamente a hipótese violada na varredura automática de longos períodos ($I=220 \rightarrow 90$).

---

## 5. Resultados

### Obra A — Saito et al. (2019) `[Extraído do artigo]`
- **Ablação em *3-fold CV* (Tabela 1 — acurácia média por classe em nível de pixel):**
  - Sem escala de cinza e sem ajuste de contraste: $0{,}584$ (U-Net padrão) / $0{,}643$ (U-Net ponderada);
  - Com escala de cinza (sem contraste): $0{,}46$ (U-Net) / $0{,}56$ (U-Net ponderada);
  - Sem escala de cinza + com ajuste de contraste: $0{,}678$ (U-Net) / **$0{,}789$ (U-Net ponderada)**;
  - Com escala de cinza + ajuste de contraste: $0{,}633$ (U-Net) / $0{,}723$ (U-Net ponderada).
  - *Achado físico-computacional:* remover informação cromática (escala de cinza) degrada severamente o desempenho, comprovando que a assinatura de cor por interferência é sinal discriminativo essencial, enquanto o aumento por variação moderada de contraste/matiz elevou a robustez de $0{,}643$ para $0{,}789$.
- **Curva precisão-revocação (Fig. 3b):** Precisão acima de $90\%$ obtida abaixo de *recall* $= 0{,}76$ para monocamada ($24\%$ de taxa de perda) e abaixo de *recall* $= 0{,}94$ para bicamada ($6{,}0\%$ de taxa de perda).
- **Teste independente ($11$ imagens de $\text{MoS}_2$, avaliadas pela classe majoritária na região-alvo):** A U-Net ponderada atingiu **$0{,}733$**, superando a média de **$12$ avaliadores humanos não especialistas ($0{,}67 \pm 0{,}11$)** e também os baselines BoVW e CNN pixel a pixel (Fig. 2m–p, Supp. Table 3).

### Obra B — Masubuchi et al. (2020) `[Extraído do artigo]`
- **Varredura automática em chip real ($\text{WTe}_2$, $1 \times 1\ \text{cm}^2$, objetiva $50\times$):** Varredura completa em **$1\ \text{h}$**, detectando $\sim 25$ flocos utilizáveis.
- **Avaliação manual em $>2.300$ imagens varridas (nível de imagem):**
  - $\text{WTe}_2$: Precisão $\sim 0{,}53$, Revocação (*Recall*) **$\sim 0{,}93$** (falsos negativos restringiram-se a flocos pequenos e fraturados, inutilizáveis para dispositivos);
  - Grafeno: Precisão **$\sim 0{,}95$**, Revocação **$\sim 0{,}97$**.
- **Segmentação pixel/instância no conjunto de teste:** $\text{mAP@IoU50\%} = 0{,}49$ (grafeno) e $0{,}52$ ($\text{WTe}_2$).
- **Comparação direta contra algoritmo baseado em regras (Fig. 2):** Quando a intensidade de iluminação caiu de $I = 220$ para $200$ e $180$, o método clássico baseado em regras falhou completamente na detecção; a Mask R-CNN manteve detecção invariante para $I = 220$, $180$ e $90$.
- **Generalização *zero-shot* entre instrumentos e materiais (Fig. 5):** O modelo treinado no sistema principal generalizou sem retreinamento para $3$ microscópios inéditos (Asahikogaku AZ10-T/E, Keyence VHX-900 e Keyence VHX-5000), e os pesos treinados em $\text{WTe}_2$ detectaram monocamadas inéditas de $\text{WSe}_2$ e $\text{MoSe}_2$.

### `[Análise crítica — Agente E]`
A discrepância em Masubuchi et al. (2020) entre métricas em nível de imagem/detecção (Recall de $0{,}93$–$0{,}97$ e precisão em grafeno de $0{,}95$) e métricas estritas de segmentação de bordas ($\text{mAP@IoU50\%} = 0{,}49$–$0{,}52$) é altamente instrutiva para a dissertação:
- Como **filtro de busca/triagem** para apontar "onde há um floco candidato na imagem", a Mask R-CNN funciona de modo excepcional e praticamente não perde flocos grandes úteis;
- Contudo, como **medida morfológica precisa de área, contorno e perímetro**, um $\text{mAP@IoU50\%}$ de $\approx 0{,}50$ indica que os contornos preditos apresentam desvio geométrico considerável em bordas finas ou flocos sobrepostos — reforçando que medições quantitativas rigorosas (ex.: espessura em nm, razão de aspecto submicrométrica, rugosidade) ainda requerem **MEV e AFM com pós-processamento clássico ou híbrido calibrado**.

---

## 6. Limitações

### `[Extraído dos artigos]`
- **Saito et al. (2019):**
  1. Falsos positivos em que o fundo do *wafer* de $\text{SiO}_2/\text{Si}$ é erroneamente classificado como monocamada devido ao tamanho reduzido do conjunto de treino ($24$ imagens em $\text{MoS}_2$, $30$ em grafeno).
  2. Granularidade limitada a apenas $3$ classes grossas (monocamada, bicamada e "outros").
  3. Uso exclusivo de substrato de $300\ \text{nm}$ de $\text{SiO}_2/\text{Si}$ e único microscópio (Olympus BX51, $100\times$).
- **Masubuchi et al. (2020):**
  1. Precisão relativamente modesta em $\text{WTe}_2$ no campo real ($\sim 0{,}53$), exigindo validação humana posterior dos candidatos filtrados.
  2. Valores moderados de $\text{mAP@IoU50\%}$ ($0{,}49$–$0{,}52$), indicando imperfeição na demarcação fina de máscaras e instâncias adjacentes.
  3. Dependência de um parque de hardware pesado para treinamento ($4\times$ V100) e servidor GPU dedicado ($32\ \text{GB}$ V100) para operação a $1\ \text{fps}$, além da fixação nos regimes de $\text{SiO}_2$ ($290\ \text{nm}$ e $90\ \text{nm}$).

### `[Análise crítica — Agente E]`
- **Ausência de quantificação de incerteza (UQ):** Nenhuma das duas arquiteturas fornece incerteza epistêmica ou probabilística calibrada (como *Monte Carlo Dropout*, *Deep Ensembles* ou *temperature scaling*); probabilidades *softmax* ou *scores* da RPN não são calibrados contra mudança de domínio (*out-of-distribution* — OOD).
- **Transferência de domínio para MEV e AFM:** Embora grafeno e materiais 2D sejam o foco comum, ambas as soluções operam sobre sinal **RGB interferométrico** de microscopia óptica. Imagens de **MEV** (elétrons secundários/retroespalhados em escala de cinza) e **AFM** (mapas topográficos 2D $z(x,y)$ com artefatos de ponta/deriva térmica) não possuem contraste cromático interferométrico de $\text{SiO}_2$; logo, pesos pré-treinados nesses artigos **não são transferíveis diretamente** sem adaptação física ou retreinamento específico para MEV/AFM.

---

## 7. Contribuição para a dissertação

### `[Análise crítica — Agente E]`
1. **Referencial comparativo entre paradigmas de segmentação:** Estabelece claramente quando escolher **segmentação semântica** (U-Net — Saito et al., 2019, adequada quando se deseja apenas fração de área ou máscara por classe de espessura) versus **segmentação de instâncias** (Mask R-CNN — Masubuchi et al., 2020, indispensável quando é preciso contar flocos individuais, extrair distribuição de áreas laterais e separar folhas sobrepostas ou aglomeradas em MEV/AFM).
2. **Lições sobre pré-processamento e preservação de sinal físico:** O experimento de ablação de Saito et al. (queda de $0{,}643 \rightarrow 0{,}56$ em escala de cinza) prova que *augmentations* ou pré-processamentos que apagam invariantes físicos reais prejudicam o modelo — lição diretamente análoga à preservação de valores quantitativos de altura $z$ em mapas de AFM ou níveis relativos de contraste em MEV (evitando equalização cega de histograma antes da quantificação).
3. **Justificativa empírica para uso híbrido e critérios de avaliação:** Demonstra que métodos baseados em regras sofrem sob deriva de iluminação, enquanto redes profundas ainda têm $\text{mAP@IoU50\%}$ limitado ($\sim 0{,}50$) e precisão variável ($0{,}53$ em $\text{WTe}_2$). Isso sustenta, na dissertação (PPGCEM/UFCA), o uso de PDI clássico calibrado quando o contraste é controlado e o uso de DL apenas como extrator/triador validado por métricas rigorosas de borda (Dice, IoU) e *GroupKFold* por amostra física.

---

## 8. Possíveis aplicações

### `[Análise crítica — Agente E]`
- **Morfologia quantitativa em MEV (distribuição de tamanho lateral de grafeno/óxido de grafeno):** O paradigma de segmentação de instâncias (Mask R-CNN, Masubuchi et al.) é o modelo de referência caso métodos clássicos baseados em `scikit-image` (Otsu + *watershed*) falhem na separação de folhas de grafeno empilhadas ou com bordas de baixo contraste em MEV.
- **Triagem automatizada de substratos antes de ensaios demorados:** O fluxo "varredura óptica rápida + filtragem por U-Net/Mask R-CNN + medição de alta resolução apenas nos candidatos" aplica-se diretamente para guiar a seleção de regiões representativas antes de varreduras lentas de AFM ou espectroscopia Raman pontual.
- **Protocolo de pré-anotação assistida (*human-in-the-loop*):** A estratégia de Masubuchi et al. (anotar $\sim 80$ imagens manualmente, treinar detector preliminar e corrigir predições em $20$–$30\ \text{s/img}$) reduz drasticamente o gargalo de rotulagem caso a dissertação crie um conjunto anotado próprio de flocos em MEV/AFM.

---

## 9. Evidências

### `[Extraído dos artigos — dados numéricos rastreáveis]`
| Estudo | Arquitetura / Tarefa | Dataset e Anotação | Desempenho Principal | Benchmark / Ablação Chave |
| :--- | :--- | :--- | :--- | :--- |
| **Saito et al. (2019)** | U-Net ($512\times 512\times 3$, perda ponderada por freq. mediana) / Semântica 3 classes | $\text{MoS}_2$: $24$ treino ($\rightarrow 960$ aug.), $11$ teste; Grafeno: $30$ treino, $14$ teste ($300\ \text{nm}\ \text{SiO}_2$) | **CV *3-fold* acc/classe:** $0{,}789$ (com contraste, RGB); **Teste $\text{MoS}_2$:** $0{,}733$ | Escala de cinza cai p/ $0{,}56$; humanos não-esp. ($n=12$): $0{,}67 \pm 0{,}11$; supera BoVW e CNN pixel a pixel |
| **Masubuchi et al. (2020)** | Mask R-CNN + ResNet101 / Instância 3 classes espessura + 4 materiais | $2.102$ imagens ($1024\times 1024$), $7.153$ objetos anotados ($290/90\ \text{nm}\ \text{SiO}_2$) | **Chip real:** Grafeno Prec $\sim 0{,}95$ / Rec $\sim 0{,}97$; $\text{WTe}_2$ Prec $\sim 0{,}53$ / Rec $\sim 0{,}93$; **$\text{mAP@IoU50\%}$:** $0{,}49$–$0{,}52$ | Regra heurística falha em $I \le 200$; Mask R-CNN invariante até $I=90$; *zero-shot* em 3 microscópios inéditos |

- **Links verificados de reprodutibilidade:** Código de Saito et al. (`https://github.com/xinkent/mos2_segmentation`); código, dados e pesos de Masubuchi et al. (`https://github.com/tdmms/`).

---

## 10. Prioridade de estudo

- **Classificação:** **ALTA (Prioridade 1 — Leitura essencial de referência arquitetural e metodológica)** `[Análise crítica — Agente E]`.
- **Justificativa:** Embora o domínio original de ambos seja a microscopia óptica (e não diretamente DRX/MEV/AFM), estes dois artigos definem os dois marcos inaugurais da segmentação profunda em materiais 2D — U-Net ponderada para poucos dados (Saito et al., 2019) e Mask R-CNN para separação de instâncias em escala industrial/laboratorial (Masubuchi et al., 2020) — fornecendo benchmarks quantitativos concretos contra algoritmos baseados em regras, critérios de validação e protocolos práticos de rotulagem semiautomática aplicáveis à etapa de análise de imagens da dissertação.
