# Fichamento 02 — Arquiteturas Fundacionais de Deep Learning para Visão Computacional: U-Net (Ronneberger et al., 2015) e ResNet (He et al., 2016)

---

## 1. Identificação bibliográfica

1. **Ronneberger, Fischer & Brox (2015) — Arquitetura codificador-decodificador para segmentação semântica com poucos dados**
   - **Título:** *U-Net: Convolutional Networks for Biomedical Image Segmentation*
   - **Autores:** Olaf Ronneberger, Philipp Fischer e Thomas Brox
   - **Ano:** 2015
   - **Publicação / Anais:** *Medical Image Computing and Computer-Assisted Intervention – MICCAI 2015* (*Lecture Notes in Computer Science*, Springer), p. 234–241
   - **DOI:** `10.1007/978-3-319-24574-4_28`
   - **Link oficial:** <https://doi.org/10.1007/978-3-319-24574-4_28> (texto completo local em `_scratch/textos_extraidos/Ronneberger_2015_U-Net_Convolutional_Networks_Segmentation.md` e `ARTIGOS_PDF/Ronneberger_2015_U-Net_Convolutional_Networks_Segmentation.pdf`)
   - **Nível de leitura:** **Texto completo lido** (8 páginas integrais em Markdown/PDF).

2. **He et al. (2016) — Aprendizado residual profundo para redes muito profundas**
   - **Título:** *Deep Residual Learning for Image Recognition*
   - **Autores:** Kaiming He, Xiangyu Zhang, Shaoqing Ren e Jian Sun
   - **Ano:** 2016
   - **Publicação / Anais:** *2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, p. 770–778
   - **DOI:** `10.1109/CVPR.2016.90`
   - **Link oficial:** <https://doi.org/10.1109/CVPR.2016.90> (acesso aberto como preprint `arXiv:1512.03385`: <https://arxiv.org/html/1512.03385v1>)
   - **Nível de leitura:** **Texto completo lido** (versão integral HTML em `arXiv:1512.03385v1`, incluindo apêndices A–C de detecção e localização).

---

## 2. Problema investigado

- **[Extraído — Ronneberger et al., 2015]:** Redes convolucionais clássicas exigiam milhares de imagens rotuladas e, quando adaptadas via janela deslizante (*sliding-window* sobre *patches*, como Ciresan et al., 2012), eram lentas por computação redundante e impunham um conflito entre contexto amplo (mais *max-pooling* reduz localização) e precisão espacial (Seção 1, p. 1–3). Como treinar uma rede de ponta a ponta (*end-to-end*) capaz de obter segmentação pixel a pixel precisa, separar objetos tocantes da mesma classe e processar imagens arbitrariamente grandes a partir de **muito poucas imagens anotadas** (dezenas, não milhares)?
- **[Extraído — He et al., 2016]:** Por que empilhar mais camadas em redes convolucionais profundas não melhora automaticamente o aprendizado? Os autores identificam o **problema da degradação**: após a resolução parcial de gradientes evanescentes/explosivos via inicialização normalizada e *Batch Normalization* (BN), redes muito profundas (*plain nets*, ex. 34 camadas vs. 18 camadas na ImageNet; 56 vs. 20 no CIFAR-10) passam a exibir **erro de treinamento mais alto** — fenômeno distinto de *overfitting*, revelando dificuldade fundamental dos otimizadores em aproximar mapeamentos identidade com camadas não lineares empilhadas (Seção 1 e Seção 3.1).

---

## 3. Fundamentação

- **[Extraído — Ronneberger et al., 2015]:**
  - Evolução das *Fully Convolutional Networks* (FCNs, Long et al., 2014): substituição de camadas totalmente conectadas por operadores de *upsampling* e combinação de mapas de características de alta resolução com mapas contextualmente ricos.
  - **Simetria em U com *skip connections*:** A U-Net propaga contexto para camadas de alta resolução mantendo grande número de canais no ramo expansivo (*up-convolution* 2×2 concatenada com mapas recortados — *copy and crop* — do ramo contrativo), conciliando contexto global e localização precisa de bordas.
  - **Perda ponderada por separação morfológica:** Função de energia via *softmax* pixel a pixel + entropia cruzada ponderada por mapa espacial pré-computado $w(\mathbf{x})$ para compensar desbalanceamento de classes e forçar o aprendizado das finas bordas de fundo entre objetos adjacentes (Seção 3, Eqs. 1–2).
  - **Invariância via deformações elásticas:** Simulação de variações morfológicas realistas em amostras limitadas via grade grosseira $3\times 3$ com interpolação bicúbica.
- **[Extraído — He et al., 2016]:**
  - **Reformulação residual:** Em vez de forçar um bloco de camadas a ajustar diretamente um mapeamento subjacente $\mathcal{H}(\mathbf{x})$, o bloco aprende a função residual $\mathcal{F}(\mathbf{x}) := \mathcal{H}(\mathbf{x}) - \mathbf{x}$, reescrevendo a saída como $\mathbf{y} = \mathcal{F}(\mathbf{x}, \{W_i\}) + \mathbf{x}$ (Eq. 1). Se o mapeamento ótimo estiver próximo da identidade, é mais fácil para o otimizador empurrar os pesos residuais para zero do que aprender a identidade através de múltiplas não linearidades (Seção 3.1–3.2).
  - **Conexões de atalho (*identity shortcuts*):** Conexões livres de parâmetros extras e sem custo computacional relevante (exceto soma elemento a elemento), recorrendo a projeção linear $W_s\mathbf{x}$ (Eq. 2, convoluções $1\times 1$) apenas quando há mudança de dimensionalidade entre estágios (Opção B) ou *padding* com zeros (Opção A).
  - **Blocos *bottleneck*:** Pilhas de $1\times 1 \rightarrow 3\times 3 \rightarrow 1\times 1$ reduzem e restauram dimensões de canais para viabilizar profundidades de 50, 101 e 152 camadas mantendo FLOPs inferiores aos da família VGG (Seção 3.3 e 4.1).

---

## 4. Metodologia

- **[Extraído — Ronneberger et al., 2015]:**
  - **Arquitetura (23 camadas convolucionais, Fig. 1):** Ramo contrativo com blocos repetidos de duas convoluções $3\times 3$ *sem padding* (*valid convolutions*) + ReLU + *max pooling* $2\times 2$ (*stride* 2), dobrando canais a cada escala ($64 \rightarrow 128 \rightarrow 256 \rightarrow 512 \rightarrow 1024$). Ramo expansivo simétrico com *up-convolution* $2\times 2$ (reduzindo canais pela metade), concatenação (*copy and crop*) com os mapas do ramo contrativo, duas convoluções $3\times 3$ + ReLU, e convolução final $1\times 1$ mapeando 64 canais para $K$ classes.
  - **Estratégia *overlap-tile* (Fig. 2):** Como convoluções *unpadded* reduzem a dimensão espacial (ex.: entrada $572\times 572$ produz saída $388\times 388$), imagens grandes são fatiadas em ladrilhos sobrepostos, extrapolando o contexto ausente nas bordas por espelhamento (*mirroring*) e exigindo dimensões pares antes de cada *max-pooling* $2\times 2$.
  - **Treinamento (Caffe, SGD):** *Batch size* de 1 imagem (priorizando ladrilhos grandes na GPU de 6 GB) compensado por *momentum* alto ($0{,}99$); inicialização gaussiana dos pesos com $\sigma = \sqrt{2/N}$ ($N =$ conexões de entrada por neurônio, citando He et al., 2015); mapa de pesos $w(\mathbf{x}) = w_c(\mathbf{x}) + w_0 \cdot \exp\left(-\frac{(d_1(\mathbf{x})+d_2(\mathbf{x}))^2}{2\sigma^2}\right)$ com $w_0 = 10$ e $\sigma \approx 5$ px, onde $d_1, d_2$ são distâncias às duas células mais próximas (Eq. 2).
  - **Data augmentation:** Deslocamentos, rotações, variações de níveis de cinza e **deformações elásticas aleatórias** (vetores gaussianos $\sigma=10$ px em grade $3\times 3$, interpolação bicúbica), somados a *dropout* no fim do ramo contrativo.
- **[Extraído — He et al., 2016]:**
  - **Arquiteturas testadas:** Redes *plain* e *ResNet* de 18, 34, 50, 101 e 152 camadas na ImageNet (1,28M imagens de treino, 50k validação, 100k teste em 1.000 classes; *crops* $224\times 224$, BN após cada convolução e antes da ativação, SGD com *mini-batch* 256, *weight decay* $10^{-4}$, *momentum* $0{,}9$, sem *dropout*); e redes de $6n+2$ camadas ($20, 32, 44, 56, 110, 1202$) no CIFAR-10 (50k treino, 10k teste em imagens $32\times 32$).
  - **Avaliação diagnóstica:** Comparação controlada entre arquiteturas *plain* e *ResNet* com exatamente os mesmos parâmetros e FLOPs (Opção A com *zero-padding* nos atalhos), comparação entre opções A/B/C de atalho, análise do desvio-padrão das respostas das camadas residuais (Fig. 7) e transferência como *backbone* em detecção/segmentação via Faster R-CNN no PASCAL VOC 2007/2012 e MS COCO (Seção 4.3 e Apêndices A–C).

---

## 5. Resultados

- **[Extraído — Ronneberger et al., 2015]:**
  - **ISBI 2012 EM Segmentation Challenge** (30 imagens TEM de $512\times 512$ px de cordão nervoso ventral de *Drosophila*; média sobre 7 rotações da entrada, sem pós-processamento adicional): **1º lugar** com *warping error* de **0,0003529** (superando o melhor *sliding-window* anterior de Ciresan et al., 0,000420), *Rand error* de **0,0382** (vs. 0,0504) e *pixel error* de **0,0611** (Tabela 1).
  - **ISBI Cell Tracking Challenge 2015:**
    - *PhC-U373* (35 imagens parcialmente anotadas de treinamento, microscopia de contraste de fase): IoU médio de **0,9203** (vs. 0,83 do segundo melhor, Tabela 2).
    - *DIC-HeLa* (20 imagens parcialmente anotadas de treinamento, microscopia DIC): IoU médio de **0,7756** (vs. 0,46 do segundo melhor, Tabela 2).
  - **Custo computacional:** Treinamento em ~10 horas numa GPU NVIDIA Titan (6 GB) e inferência inferior a **1 segundo** para imagens $512\times 512$.
- **[Extraído — He et al., 2016]:**
  - **Eliminação da degradação na ImageNet:** Na versão *plain*, 34 camadas pioraram frente a 18 camadas (erro *top-1* de validação 28,54% vs. 27,94%); na versão *ResNet*, 34 camadas caíram para **25,03%** (ganho de 3,5 pontos percentuais sobre a *plain-34* e melhora sobre a ResNet-18 de 27,88%; Tabela 2).
  - **Escalabilidade até 152 camadas:** ResNet-152 ($11{,}3\times 10^9$ FLOPs, menor que VGG-16/19 com $15{,}3/19{,}6\times 10^9$ FLOPs) alcançou **4,49%** de erro *top-5* em validação com modelo único (19,38% *top-1*, Tabela 4), e um *ensemble* de 6 ResNets atingiu **3,57%** de erro *top-5* no conjunto de teste — **1º lugar** na ILSVRC 2015 (Tabela 5).
  - **CIFAR-10 e análise das ativações:** Erro de teste caiu monotonicamente de 8,75% (ResNet-20) para **6,43%** (ResNet-110, apenas 1,7M parâmetros, Tabela 6). A ResNet-1202 convergiu para $<0{,}1\%$ de erro de treino, mas subiu para 7,93% de erro de teste por *overfitting* num conjunto pequeno (19,4M parâmetros sem *dropout*). A Fig. 7 confirmou que funções residuais possuem desvios-padrão de resposta menores que redes *plain* equivalentes, corroborando o efeito de pré-condicionamento.
  - **Transferência para localização/detecção:** Substituir VGG-16 por ResNet-101 no Faster R-CNN elevou o `mAP@[.5, .95]` no MS COCO de 21,2% para **27,2%** (+6,0 pontos absolutos; melhoria relativa de 28%, Tabela 8), garantindo 1º lugar em detecção/localização/segmentação no ILSVRC & COCO 2015.

---

## 6. Limitações

- **[Extraído — Ronneberger et al., 2015]:**
  - A estratégia *unpadded* reduz o campo de saída frente à entrada ($572\times 572 \rightarrow 388\times 388$), requerendo dimensões compatíveis com divisões pares por 2 em cada etapa de *pooling* e espelhamento artificial nas bordas (Fig. 2).
  - A separação de instâncias tocantes exige pré-computação de mapas de distância morfológica ($d_1, d_2$) e ajuste de $w_0, \sigma$ para objetos de mesma classe, não realizando por si só rotulagem de instâncias quando há forte oclusão/sobreposição tridimensional (papel assumido posteriormente por redes como Mask R-CNN).
  - Dependência de *augmentation* elástica (desenhada para células/tecidos deformáveis) e de máscaras manuais pixel a pixel, ainda que em pequeno número (20–35 imagens).
- **[Extraído — He et al., 2016]:**
  - A ResNet-1202 (19,4M parâmetros) apresentou degradação de generalização no CIFAR-10 (7,93% vs. 6,43% da ResNet-110) devido a *overfitting* por capacidade excessiva sem regularização forte (*dropout*/*maxout*) quando o conjunto de dados é pequeno (Seção 4.2).
  - Os próprios autores observam que a hipótese de aproximação assintótica de funções residuais permanece uma questão teórica aberta (nota de rodapé 2, Seção 3.1) e que, em tarefas de detecção/transferência sobre imagens pequenas ou lotes reduzidos, estatísticas de *Batch Normalization* precisam ser congeladas para economizar memória (Apêndice A).
- **[Análise crítica — Agente E]:**
  - Em caracterização de materiais (grafeno/2D, MEV, AFM), **deformações elásticas** da U-Net original devem ser aplicadas com extrema cautela: embora adequadas a tecidos biológicos ou membranas flexíveis, distorções elásticas arbitrárias alteram ângulos cristalográficos facetados, linearidade de degraus ou circularidade/esbeltez de flocos, podendo falsificar descritores morfológicos se o objetivo for metrologia geométrica.
  - Da mesma forma, *backbones* profundos como ResNet-101/152 trazem risco severo de sobreajuste em bancos laboratoriais típicos do PPGCEM (dezenas de micrografias), exigindo *transfer learning*, congelamento parcial de camadas, regularização ou variantes leves da U-Net (como demonstrado em Saito et al., 2019 e Gerçek et al., 2025).

---

## 7. Contribuição para a dissertação

- **[Análise crítica — Agente E]:**
  - **Referencial arquitetural indispensável:** Praticamente toda a literatura recente de segmentação de materiais 2D (Saito et al., 2019; Leger et al., 2024; Meng et al., 2024) e microestruturas em MEV (Gerçek et al., 2025) deriva diretamente da U-Net ou emprega *backbones* ResNet (como a ResNet-101 no Mask R-CNN de Masubuchi et al., 2020, ou blocos residuais na geração espectral de Qi et al., 2024).
  - **Justificativa para regimes de poucos dados:** Ronneberger et al. (2015) demonstram objetivamente que segmentação profunda pode operar com 20–35 imagens (contando com *skip connections*, perdas ponderadas e *augmentation* coerente), dado crucial para laboratórios de ciência dos materiais onde a rotulagem pixel a pixel de micrografias MEV/AFM é o principal gargalo.
  - **Alerta contra complexidade cega:** He et al. (2016) comprovam tanto a necessidade de conexões residuais para redes profundas quanto o risco de sobreparametrização (ResNet-1202 no CIFAR-10) quando a capacidade excede a diversidade amostral disponível.

---

## 8. Possíveis aplicações

- **[Análise crítica — Agente E (caminhos investigativos futuros)]:**
  1. **Segmentação de flocos em MEV com U-Net leve ou ResNet-18/34 pré-treinada como *encoder*:** Testar se uma U-Net compacta (ou com *backbone* ResNet-18/34 pré-treinado) oferece ganho estatisticamente significativo sobre o pipeline clássico de `scikit-image` (Otsu + morfologia + *watershed*) apenas nos casos em que o contraste fundo-floco falha por rugosidade do substrato, carregamento elétrico (*charging*) ou sobreposição de tons de cinza.
  2. **Perda ponderada nas bordas para flocos adjacentes:** Adaptar a Eq. (2) da U-Net ($w_0, \sigma$ calibrados para espessura de borda em pixels) para evitar a fusão de flocos próximos numa única máscara binária, mantendo porém preservação geométrica rígida na *augmentation* (rotações discretas, espelhamentos, variações de contraste/brilho, evitando distorções elásticas em métricas métricas de forma).
  3. **Processamento de micrografias MEV de alta resolução via *overlap-tile*:** Aplicar a estratégia *overlap-tile* com espelhamento de borda para segmentar micrografias MEV $2048\times 1536$ ou maiores sem *downsampling* destrutivo de flocos pequenos ou perda de memória de GPU.

---

## 9. Evidências

- **Ronneberger et al. (2015):**
  - Fig. 1 e Seção 2 (p. 2, 4): diagrama completo das 23 camadas convolucionais e dimensões dos mapas ($572^2 \rightarrow 388^2$).
  - Fig. 2 e Seção 2 (p. 3–4): estratégia *overlap-tile* com extrapolação por espelhamento.
  - Fig. 3, Eqs. (1)–(2) e Seção 3 (p. 4–6): mapa de pesos morfológico ($w_0=10$, $\sigma\approx 5$), *batch* unitário, *momentum* $0{,}99$, inicialização $\sqrt{2/N}$ e deformações elásticas em grade $3\times 3$.
  - Seção 4, Tabelas 1–2 e Fig. 4 (p. 6–8): resultados no ISBI 2012 EM (0,0003529) e ISBI 2015 Cell Tracking (`PhC-U373` IoU 0,9203; `DIC-HeLa` IoU 0,7756).
- **He et al. (2016):**
  - Seção 1 e Fig. 1 (`arXiv:1512.03385v1`): evidência empírica da degradação (erro de treino 56 vs. 20 camadas no CIFAR-10).
  - Seção 3.1–3.3, Eqs. (1)–(2) e Tabela 1: definição de $\mathcal{F}(\mathbf{x})+\mathbf{x}$, atalhos identidade vs. projeção e especificações das ResNets 18/34/50/101/152 (FLOPs $1{,}8\text{–}11{,}3\times 10^9$).
  - Seção 4.1, Tabelas 2–5: comparação controlada *plain* vs. *ResNet* (28,54% vs. 25,03% *top-1* na 34 camadas; 4,49% *top-5* único na ResNet-152; 3,57% no *ensemble*).
  - Seção 4.2, Tabela 6 e Fig. 7: CIFAR-10 até 1202 camadas (6,43% na ResNet-110 vs. 7,93% na 1202 por *overfitting*) e análise das amplitudes das respostas residuais.
  - Seção 4.3, Tabela 8 e Apêndices A–C: ganhos de +6,0 pontos em `mAP@[.5, .95]` no MS COCO com Faster R-CNN + ResNet-101.

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta**
- **Justificativa:** U-Net e ResNet constituem os dois blocos arquiteturais mais influentes da visão computacional científica moderna. O estudo integral desses dois artigos fornece o domínio conceitual necessário para compreender decisões de projeto (como *skip connections*, *overlap-tile*, perdas ponderadas em bordas, atalhos residuais e equilíbrio entre profundidade e tamanho amostral) diretamente replicadas ou adaptadas nos trabalhos de caracterização de materiais 2D e microestruturas em MEV (Saito et al., 2019; Masubuchi et al., 2020; Leger et al., 2024; Gerçek et al., 2025).
