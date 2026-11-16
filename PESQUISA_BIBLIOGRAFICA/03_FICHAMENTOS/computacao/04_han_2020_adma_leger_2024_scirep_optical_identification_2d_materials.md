# Fichamento 04 — Identificação Óptica de Materiais 2D por Aprendizado Profundo e Comparação de Arquiteturas/Pré-processamentos: Han et al. (2020) e Leger et al. (2024)

> **Nível de leitura declarado (Seção 8 — `PROMPT_MESTRE.md`):**
> - **Han et al. (2020):** **Texto completo lido** via extração integral (`_scratch/textos_extraidos/Han_2020_Deep_Learning_Fast_Optical_Identification_2D_Materials.md`, linhas 1–797 de 800, ~99,6% incluindo Informação Suplementar — apenas as 3 referências finais da SI não constavam do recorte).
> - **Leger et al. (2024):** **Texto completo lido** via extração integral do artigo publicado (`_scratch/textos_extraidos/Leger_2024_ML_Optical_Identification_2D_Materials_SciRep.md`, 382 linhas completas, acrescido da versão HTML oficial na *Nature/Scientific Reports*).
> - **Verificação *preprint $\rightarrow$ publicado*:** Tanto Han et al. (2020) quanto Leger et al. (2024) circularam originalmente no arXiv, **mas ambos possuem versões publicadas revisadas por pares**, adotadas abaixo como referências principais (citando os identificadores arXiv apenas como acesso aberto).

---

## 1. Identificação bibliográfica

### Obra A — Han et al. (2020) `[Extraído do artigo]`
- **Autores:** Bingnan Han, Yuxuan Cosmi Lin, Yafang Yang, Nannan Mao, Wenyue Li, Haozhe Wang, Kenji Yasuda, Xirui Wang, Valla Fatemi, Lin Zhou, Joel I-Jan Wang, Qiong Ma, Yuan Cao, Daniel Rodan-Legrain, Ya-Qing Bie, Efrén Navarro-Moratalla, Dahlia R. Klein, David MacNeill, Sanfeng Wu, Hikari Kitadai, Xi Ling, Pablo Jarillo-Herrero, Jing Kong, Jihao Yin, Tomás Palacios.
- **Ano:** 2020.
- **Título completo:** *Deep-Learning-Enabled Fast Optical Identification and Characterization of 2D Materials*.
- **Periódico (referência principal publicada):** *Advanced Materials*, vol. 32, n.º 29, e2000953 (2020).
- **DOI:** `10.1002/adma.202000953`
- **Link oficial:** <https://doi.org/10.1002/adma.202000953>
- **Preprint (apenas acesso aberto):** `arXiv:1906.11220`
- **Nível de leitura:** Texto completo (~99,6% do arquivo extraído).

### Obra B — Leger et al. (2024) `[Extraído do artigo]`
- **Autores:** Polina A. Leger, Aditya Ramesh, Talianna Ulloa, Yingying Wu.
- **Ano:** 2024 (publicado em 13 de novembro de 2024).
- **Título completo:** *Machine learning enabled fast optical identification and characterization of 2D materials*.
- **Periódico (referência principal publicada):** *Scientific Reports*, vol. 14, n.º 1, artigo 27808 (2024).
- **DOI:** `10.1038/s41598-024-79386-z`
- **Link oficial:** <https://doi.org/10.1038/s41598-024-79386-z>
- **Preprint (apenas acesso aberto):** `arXiv:2406.16211`
- **Nível de leitura:** Texto completo.

---

## 2. Problema investigado

### Obra A — Han et al. (2020) `[Extraído do artigo]`
- Métodos anteriores de aprendizado profundo para identificação óptica de materiais 2D (como U-Net ou Mask R-CNN em conjuntos restritos) concentravam-se em $1$–$4$ compostos adquiridos em condições laboratoriais uniformes. Na prática experimental multiusuário, imagens ópticas de $13$ ou mais materiais 2D diferem fortemente em microscópio, câmera, objetiva, temperatura de cor da lâmpada, tempo de exposição e foco.
- Além disso, faltava compreender *o que* as camadas profundas aprendem fisicamente (interpretabilidade) e se vetores latentes de classificação óptica carregam correlação com propriedades físicas intrínsecas (como *bandgap* e estrutura cristalina) de materiais inéditos.

### Obra B — Leger et al. (2024) `[Extraído do artigo]`
- Embora redes 2D (SegNet, U-Net) tenham alcançado alta precisão em identificação óptica de materiais 2D, persistem três questões práticas em aberto:
  1. Como diferentes arquiteturas se comparam sob o mesmo conjunto de dados e protocolo — especificamente **2D SegNet**, **2D U-Net** e **1D U-Net** (aplicada linha a linha para tentar acelerar a inferência)?
  2. Transformações clássicas de pré-processamento físico-óptico, especialmente a **Diferença Total de Cor ($\Delta E$ / TCD)** em espaço CIELAB mapeada para mapas de cores (*Plasma*, *HSV*, *Spectral*) ou conversão em escala de cinza/contraste, melhoram ou degradam o aprendizado profundo em relação à normalização simples de fundo?
  3. Quais artefatos surgem ao aplicar aumentos geométricos (*shear* afim com preenchimento preto nas bordas) e pré-rotulagem não supervisionada (superpixels SLIC + DBSCAN)?

### `[Análise crítica — Agente E]`
A leitura conjunta de Han et al. (2020) e Leger et al. (2024) é altamente reveladora porque Leger et al. reutilizam e estendem a base de código/dados derivada do grupo de Han/Yang para testar hipóteses que frequentemente são aceitas sem verificação na literatura: (i) que mapas cromáticos engenheirados como TCD ajudam CNNs; e (ii) que reduções 1D são mais rápidas e suficientes. Os resultados empíricos de Leger et al. refutam ambas as suposições e expõem, simultaneamente, vulnerabilidades metodológicas graves na construção de *ground truth* sem validação física independente (AFM/Raman).

---

## 3. Fundamentação

### `[Extraído dos artigos]`
1. **Espaço de cor CIELAB ($\text{L}^*\text{a}^*\text{b}^*$) e normalização de substrato:** Em vez de operar no espaço RGB acoplado à luminância, ambos os estudos utilizam o espaço perceptual $\text{L}^*\text{a}^*\text{b}^*$ normalizado pela mediana do substrato de referência ($L_{\text{ref}}, a_{\text{ref}}, b_{\text{ref}}$): $L \leftarrow 30\,L/L_{\text{ref}}$, $a \leftarrow a - a_{\text{ref}}$, $b \leftarrow b - b_{\text{ref}}$ (Han et al., 2020; adotado por Leger et al., 2024 com subamostragem $1/10$ para estimar o fundo).
2. **Diferença Total de Cor (TCD — $\Delta E$):** Leger et al. (2024) testam a métrica escalar clássica da óptica de filmes finos:
   $$\Delta E = \sqrt{(\Delta L^*)^2 + (\Delta a^*)^2 + (\Delta b^*)^2}$$
   mapeada para paletas falsas (*Plasma*, *HSV*, *Spectral*) antes da entrada nas redes.
3. **Arquitetura SegNet vs. U-Net (2D e 1D):**
   - **SegNet (Han et al., 2020; Leger et al., 2024):** Codificador VGG16 cujo diferencial em relação à U-Net é transferir apenas os **índices de *max-pooling*** (não os mapas completos de características) para o decodificador reconstruir a resolução espacial, reduzindo memória de ativações. Han et al. determinam **Depth = 5** como ótimo (Tabela S2).
   - **2D U-Net vs. 1D U-Net (Leger et al., 2024):** A 2D U-Net preserva contexto espacial bidimensional via *skip connections* completas; a 1D U-Net processa vetores unidimensionais (linhas horizontais da imagem) ignorando correlação vertical.
4. **Pré-rotulagem clássica com SLIC + DBSCAN (Leger et al., 2024):** Agrupamento por superpixels *Simple Linear Iterative Clustering* (SLIC) combinado a clusterização por densidade DBSCAN com dois limiares, seguido de refinamento visual humano.
5. **Interpretabilidade por mapas de ativação e projeção por similaridade:** Han et al. (2020) inspecionam os $21$ canais da última camada de características (Depth = 5) e projetam vetores de similaridade derivados da matriz de confusão de um *ensemble* de $16$ redes sobre materiais inéditos.

### `[Análise crítica — Agente E]`
Sob a ótica de processamento de imagens e ciência de materiais, a normalização aditiva/multiplicativa em $\text{L}^*\text{a}^*\text{b}^*$ ancorada na mediana do substrato é fisicamente muito superior à normalização z-score global por imagem, pois fixa o zero de referência exatamente no substrato $\text{SiO}_2/\text{Si}$ (que domina a imagem e define o contraste óptico diferencial). Já a tentativa de comprimir $(\Delta L^*, \Delta a^*, \Delta b^*)$ em um escalar $\Delta E$ recolorido por *colormap* (Leger et al., 2024) **destrói a direcionalidade cromática física** (por exemplo, flocos diferentes ou espessuras distintas podem apresentar mesma distância euclidiana $|\Delta E|$ com sinais opostos de $\Delta a^*$ ou $\Delta b^*$, além de introduzir descontinuidades artificiais na paleta *HSV*/*Spectral*), explicando perfeitamente por que a TCD degradou a 2D SegNet e a 2D U-Net.

---

## 4. Metodologia

### Obra A — Han et al. (2020) `[Extraído do artigo]`
- **Acervo experimental multi-institucional:** $13$ materiais em substratos $\text{SiO}_2/\text{Si}$ de $285\ \text{nm}$ e $90\ \text{nm}$, totalizando **$817$ imagens de flocos + $100$ imagens apenas de fundo ($917$ imagens)** coletadas ao longo de **$10$ anos por $\ge 30$ usuários, $8$ grupos de pesquisa e $6$ microscópios diferentes**, compondo **$22$ classes** (1L, 2–6L e $>6\text{L}$ para grafeno, $\text{MoS}_2$, $\text{WS}_2$ e $\text{TaS}_2$, mais $9$ materiais com classe única e fundo).
- **Rotulagem e recorte:** Rotulagem semiautomática via *graph-cut* no MATLAB. Após divisão **$90:10$ em nível de imagem**, os autores extraem recortes de $224 \times 224$ pixels: **$3.825$ recortes de treino ($4.275$ com fundo)** e **$2.550$ recortes de teste**.
- **Estratégia de aumento de dados (Tabela S3):** Comparou-se aumento básico $6\times$, aumento cromático $13\times$ e **rotação aleatória por época durante $250$ épocas**. A rotação aleatória por época superou as alternativas; o aumento artificial de cor **prejudicou** a acurácia de espessura.
- **Treinamento e fluxo automatizado:** Treinado em GPU NVIDIA GTX 1080 Ti ($30\ \text{h}\ 56\ \text{min}\ 23\ \text{s}$; inferência a $2{,}5\ \text{fps}$ em CPU e $22\ \text{fps}$ em GPU). Em validação de varredura real, um estágio motorizado Nikon $XYZ$ escaneou $1{,}5 \times 1{,}5\ \text{cm}^2$ em $50\ \text{min}$ ($>1.000$ imagens de $1636 \times 1088$, gerando $22.344$ patches de grafeno e $16.872$ de $\text{MoS}_2$), processados em $<15\ \text{min}$ em GPU, retendo $9{,}45\%$ e $8{,}25\%$ dos quadros ($>100\ \text{px}$ de 1L/poucas camadas) para triagem humana de $5\ \text{min}$.
- **Transferência e ensemble:** Ensemble de $16$ redes projetando similaridades para inferir *bandgap* e estrutura cristalina de $17$ materiais 2D não vistos (Fig. 4); *transfer learning* avaliado em grafeno CVD (1L–5L) e $\text{Td-WTe}_2$ (Fig. 5).

### Obra B — Leger et al. (2024) `[Extraído do artigo]`
- **Conjunto de dados:** $1.400$ imagens pré-rotuladas de $100 \times 100$ provenientes do repositório GitHub de Han/Yang + $408$ imagens extraídas de $18$ imagens brutas de MO recortadas em $100 \times 100$.
- **Pré-processamentos testados:** (1) Normalização mediana em $\text{L}^*\text{a}^*\text{b}^*$ (`None` / base normalizada, com mediana sobre subamostra $1/10$); (2) Escala de cinza (para 1D/2D U-Net); (3) Contraste; (4) TCD ($\Delta E$) mapeada em paletas *Plasma*, *HSV* e *Spectral*.
- **Aumento de dados e artefato geométrico:** Rotações e cisalhamento afim (*affine shear* com `affine2d` no MATLAB). O cisalhamento introduziu **cantos pretos de preenchimento zero**, forçando o teste comparativo entre $3$ classes (substrato, monocamada, multicamada) e $4$ classes (incluindo classe explícita para os cantos pretos de *shear*).
- **Pré-rotulagem:** Superpixels SLIC + DBSCAN com dois limiares + correção visual manual (sem nova confirmação por AFM ou Raman nas novas imagens).
- **Arquiteturas comparadas:** **2D SegNet** (implementação MATLAB com transferência de pesos sobre $1.400$ imagens), **2D U-Net** e **1D U-Net** (por linhas).

### `[Análise crítica — Agente E]`
- **Ponto forte metodológico em Han et al. (2020):** A divisão $90:10$ é realizada **antes** do recorte em *patches* $224 \times 224$ ($3.825$/$4.275$ treino vs. $2.550$ teste), evitando o erro clássico de dividir *patches* sobrepostos da mesma imagem entre treino e teste. Contudo, como múltiplos recortes são gerados por imagem, imagens distintas obtidas no mesmo dia/substrato por um mesmo usuário podem ainda correlacionar-se sem agrupamento explícito por sessão/amostra.
- **Falhas metodológicas críticas identificadas em Leger et al. (2024):**
  1. **Ausência de *ground truth* físico:** Os rótulos das $408$ novas imagens dependem exclusivamente de SLIC + DBSCAN + julgamento visual humano, **sem validação por AFM ou espectroscopia Raman** — criando risco de circularidade visual na definição de monocamada vs. bicamada/multicamada.
  2. **Artefato de pré-processamento autoinduzido:** A aplicação de `affine2d` com preenchimento zero criou regiões pretas artificiais que exigiram uma 4.ª classe sintética no modelo de segmentação.
  3. **Origem única de dados:** Todas as imagens derivam de uma única fonte/repositório, limitando a generalização interlaboratorial.

---

## 5. Resultados

### Obra A — Han et al. (2020) `[Extraído do artigo]`
- **Melhor modelo (Network #5, Depth = 5, Tabelas 1 e S4):**
  - Acurácia global de pixel: **$0{,}9689$** ($96{,}89\%$);
  - Acurácia média por classe: **$0{,}7978$** ($79{,}78\%$);
  - *Mean IoU*: **$0{,}5878$**.
- **Robustez a foco e aumento de dados:** Manteve detecção robusta mesmo sob desfocagem controlada (Fig. S9); a rotação aleatória por época ($250$ épocas) superou claramente aumentos estáticos $6\times$ e aumento cromático $13\times$ (Tabela S3).
- **Interpretabilidade (Tabela S6, Figs. S51–S52):** Os $21$ mapas de características de Depth = 5 organizam-se em quatro grupos físicos/geométricos: **contraste/cor**, **borda**, **forma** e **tamanho** — reproduzindo-se consistentemente ao longo de $16$ inicializações independentes (Fig. S51). Identificaram-se ainda canais de contorno que compensam artefatos circulares gerados pelo *padding* de rotação (Fig. S52).
- **Predição indireta de propriedades físicas e *transfer learning*:** O *ensemble* de $16$ redes correlacionou confusões ópticas a propriedades (*bandgap* e estrutura cristalina) de $17$ materiais 2D inéditos (Fig. 4). Por *transfer learning* (Fig. 5), grafeno CVD (1L–5L) atingiu **$67\%$** com apenas $60$ imagens (contra $\ge 240$ imagens para treino aleatório do zero), e $\text{Td-WTe}_2$ alcançou **$91\%$** de acurácia média por classe.

### Obra B — Leger et al. (2024) `[Extraído do artigo]`
- **Melhor desempenho por arquitetura (Tabelas I–V):**
  - **2D U-Net (`None` / normalização simples de fundo):** Acurácia global **$0{,}960$**, substrato $0{,}970$, monocamada **$0{,}737$**, multicamada **$0{,}758$**, Precisão $0{,}721$, Revocação $0{,}654$, F1 **$0{,}665$**.
  - **2D SegNet ($1.400$ imagens + *transfer learning*, `None`):** Acurácia global **$0{,}915$**, substrato $0{,}915$, monocamada **$0{,}908$**, multicamada **$0{,}917$**, *Mean IoU* $0{,}631$, *Mean BF* $0{,}503$.
  - **1D U-Net (melhor caso: Contraste):** Acurácia global $0{,}932$, mas **acurácia em monocamada $= 0{,}000$ / `NaN`**, produzindo predições com listras horizontais (*streaky predictions*, Fig. 6) e sendo **mais lenta na inferência** que a 2D U-Net por sobrecarga de movimentação de memória por linha e perda de contexto vertical.
- **Impacto da Diferença Total de Cor (TCD / $\Delta E$):** A conversão em paletas TCD (*Plasma*, *HSV*, *Spectral*) **degradou** o desempenho tanto da 2D SegNet quanto da 2D U-Net em comparação direta com a normalização simples de fundo $\text{L}^*\text{a}^*\text{b}^*$.

### `[Análise crítica — Agente E]`
Os números de Leger et al. (2024) revelam um contraste metodológico fundamental entre **acurácia global** e **métricas sensíveis à classe minoritária**:
- A 1D U-Net reporta acurácia global aparentemente alta (**$0{,}932$**), mas tem **acurácia $0{,}000$ / `NaN` em monocamada**! Isso ocorre porque o fundo (substrato) compõe a esmagadora maioria dos pixels. Em qualquer problema de caracterização (DRX com picos minoritários, MEV com defeitos/poros/flocos raros, AFM com degraus nanométricos), **acurácia global de pixel é uma métrica enganosa** que mascara falha total na classe de interesse científico.
- Da mesma forma, enquanto a 2D SegNet obteve acurácia por classe equilibrada ($0{,}908$–$0{,}917$) via *transfer learning*, o seu *Mean IoU* foi de $0{,}631$ e *Mean BF* (alinhamento de borda) apenas $0{,}503$ — confirmando o mesmo padrão visto em Han et al. (2020: global $0{,}9689$ vs. *mean IoU* $0{,}5878$) e Masubuchi et al. (2020: *mAP@IoU50%* $\sim 0{,}50$): **bordas nanométricas/submicrométricas são o calcanhar de Aquiles da segmentação por DL óptico**.

---

## 6. Limitações

### `[Extraído dos artigos]`
- **Han et al. (2020):**
  - *Mean IoU* moderado ($0{,}5878$) apesar de acurácia global de $96{,}89\%$, devido a erros nas bordas e confusão entre faixas adjacentes de espessura de materiais distintos entre os $22$ rótulos.
  - Custo de treinamento elevado ($\sim 31\ \text{h}$ em GTX 1080 Ti) e necessidade de normalização de substrato de $\text{SiO}_2/\text{Si}$ ($285/90\ \text{nm}$).
  - *Padding* circular da rotação induz artefatos de borda que a própria rede precisa aprender a cancelar em canais internos (Fig. S52).
- **Leger et al. (2024):**
  - Rótulos das $408$ imagens extras obtidos apenas por SLIC + DBSCAN + inspeção visual, **sem verificação experimental por AFM ou Raman**.
  - Base única de dados de origem; conjunto pequeno de $18$ imagens brutas para os testes extras.
  - Necessidade de 4.ª classe artificial devido ao preenchimento preto do cisalhamento afim (`affine2d`).
  - Colapso completo da 1D U-Net na classe monocamada ($0{,}000$ / `NaN`) e desempenho inferior de todos os esquemas com TCD frente à normalização simples.

### `[Análise crítica — Agente E]`
- **Limitação do *ensemble* de propriedades físicas em Han et al. (2020):** Embora elegante, associar matriz de confusão óptica a *bandgap* e estrutura cristalina (Fig. 4) é uma inferência indireta mediada pela função dielétrica visível $\varepsilon(\omega)$ sobre $\text{SiO}_2$; materiais com índice de refração complexo coincidente podem colidir no espaço de cor sem possuírem mesma simetria cristalina nem mesmo *bandgap*. Para determinação estrutural e de fases, **DRX e análise física direta são insubstituíveis**.

---

## 7. Contribuição para a dissertação

### `[Análise crítica — Agente E]`
1. **Regra de ouro contra *feature engineering* prejudicial em DL vs. PDI clássico:** Leger et al. (2024) fornecem prova empírica de que projetar a imagem em um índice escalar TCD ($\Delta E$) com *colormaps* artificiais pode *ajudar* um operador humano ou um algoritmo de limiar clássico univariado, mas **piora** redes convolucionais 2D ao descartar canais $\text{L}^*\text{a}^*\text{b}^*$ ortogonais. Da mesma forma, Han et al. (2020) provam que *color augmentation* distorce a física do contraste de camadas.
2. **Alerta contra redução dimensional ingênua (1D vs. 2D) e contra métrica de acurácia global:** A falha catastrófica da 1D U-Net (`NaN`/`0.000` em monocamadas com `0.932` global) serve como estudo de caso perfeito na dissertação para justificar por que métricas como **IoU por classe, Dice, Precisão/Revocação por classe e *Boundary F1*** são obrigatórias na avaliação de MEV e AFM, e por que contexto 2D (ou 3D/espectral adequado) não deve ser sacrificado por ganhos teóricos de FLOPs que sequer se traduzem em velocidade real por gargalos de memória.
3. **Referência de interpretabilidade em camadas profundas:** A análise dos $21$ canais de Depth = 5 em Han et al. (2020) — mostrando separação emergente em contraste/cor, borda, forma e tamanho além de canais de correção de *padding* — oferece um roteiro concreto para auditar modelos treinados na dissertação e evitar que a rede aprenda artefatos de recorte ou borda da imagem (*shortcut learning*).

---

## 8. Possíveis aplicações

### `[Análise crítica — Agente E]`
- **Normalização de fundo baseada em mediana do substrato em MEV/AFM:** Adaptar a ideia de normalização ancorada no substrato de $\text{L}^*\text{a}^*\text{b}^*$ para **nivelamento e normalização do plano de referência do substrato** (em AFM via `Gwyddion`/polinomial e em MEV via estimativa robusta de moda/mediana do suporte de carbono/silício) antes de qualquer segmentação clássica ou neural.
- **Auditoria de artefatos de *data augmentation*:** Evitar *affine shear* com *zero-padding* preto (erro exposto em Leger et al., 2024) usando preenchimento por reflexão (*mirror/reflect padding*) ou recortes internos inscritos ao rotacionar imagens de MEV/AFM, e banir *color/brightness jitter* agressivo quando a intensidade física codifica espessura ou número atômico $Z$.
- **Seleção de métricas em MEV/AFM:** Empregar obrigatoriamente Dice/IoU por classe minoritária (flocos finos/defeitos) e *Boundary F1* (*Mean BF*), rejeitando avaliações baseadas apenas em acurácia global de pixel.

---

## 9. Evidências

### `[Extraído dos artigos]`
| Trabalho | Modelo / Pré-processamento | Conjunto de Dados | Métricas Quantitativas Verificadas | Evidências Adicionais |
| :--- | :--- | :--- | :--- | :--- |
| **Han et al. (2020)** (*Adv. Mater.*) | SegNet (VGG16, Depth=5) + norm. mediana $\text{L}^*\text{a}^*\text{b}^*$ + rot. aleatória/época | $917$ imgs ($817$ flocos + $100$ BG), $13$ mat., $22$ classes; $3.825$/$4.275$ treino e $2.550$ teste ($224\times 224$) | **Global:** $0{,}9689$; **Mean Class Acc:** $0{,}7978$; **Mean IoU:** $0{,}5878$ | Varredura $1{,}5\times 1{,}5\ \text{cm}^2$ ($>1.000$ imgs) em $50\ \text{min}$ + $<15\ \text{min}$ GPU; *transfer* $\text{Td-WTe}_2$ $= 91\%$; *color aug* degrada acurácia (Tab. S3) |
| **Leger et al. (2024)** (*Sci. Rep.*) | 2D U-Net (`None` norm. simples) | $1.400$ pré-rotuladas + $408$ de $18$ brutas ($100\times 100$) | **Global:** $0{,}960$; Sub $0{,}970$; **Mono $0{,}737$**; Multi $0{,}758$; F1 $0{,}665$ | TCD ($\Delta E$) degrada 2D U-Net e 2D SegNet |
| **Leger et al. (2024)** (*Sci. Rep.*) | 2D SegNet ($1.400$ + *transfer*, `None`) | Idem | **Global:** $0{,}915$; **Mono $0{,}908$**; Multi $0{,}917$; **Mean IoU $0{,}631$**; Mean BF $0{,}503$ | Alto recall em mono/multi, porém *IoU* e *BF* moderados |
| **Leger et al. (2024)** (*Sci. Rep.*) | 1D U-Net (Contraste) | Idem | **Global:** $0{,}932$; **Mono $0{,}000$ / `NaN`** | Predições listradas; **mais lenta** que 2D U-Net |

---

## 10. Prioridade de estudo

- **Classificação:** **ALTA (Prioridade 1 — Referência obrigatória de desenho experimental, normalização e armadilhas métricas)** `[Análise crítica — Agente E]`.
- **Justificativa:** Han et al. (2020) fornecem o maior estudo multiusuário/multimicroscópio de segmentação de materiais 2D com análise inédita de interpretabilidade interna e prova contra *color augmentation* físico; Leger et al. (2024) complementam-no criticamente ao demonstrar, com evidências numéricas claras, os perigos de métricas globais em classes desbalanceadas (1D U-Net com $93{,}2\%$ global e $0\%$ em monocamada), o fracasso de *colormaps* TCD frente à normalização simples de fundo e os riscos de *ground truth* não validado fisicamente por AFM/Raman.
