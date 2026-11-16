# Fichamento 01 — Fundamentos do Processamento Digital de Imagens Clássico: Limiarização de Otsu (1979), `scikit-image` (van der Walt et al., 2014) e `Fiji/ImageJ` (Schindelin et al., 2012)

---

## 1. Identificação bibliográfica

Este fichamento integra três referências basilares do processamento digital de imagens (PDI) clássico e de suas plataformas científicas abertas de execução:

1. **Otsu (1979) — Método clássico de limiarização global não paramétrica**
   - **Título:** *A Threshold Selection Method from Gray-Level Histograms*
   - **Autor:** Nobuyuki Otsu
   - **Ano:** 1979 (janeiro de 1979)
   - **Periódico:** *IEEE Transactions on Systems, Man, and Cybernetics*, v. 9, n. 1, p. 62–66
   - **DOI:** `10.1109/TSMC.1979.4310076`
   - **Link oficial:** <https://doi.org/10.1109/TSMC.1979.4310076> (cópia de leitura utilizada: <https://engineering.purdue.edu/kak/computervision/ECE661.08/OTSU_paper.pdf>)
   - **Nível de leitura:** **Texto completo lido** (páginas 62–66 extraídas integralmente do PDF).

2. **van der Walt et al. (2014) — Ecossistema programático em Python (`scikit-image`)**
   - **Título:** *scikit-image: image processing in Python*
   - **Autores:** Stéfan van der Walt, Johannes L. Schönberger, Juan Nunez-Iglesias, François Boulogne, Joshua D. Warner, Neil Yager, Emmanuelle Gouillart, Tony Yu e colaboradores do *scikit-image*
   - **Ano:** 2014
   - **Periódico:** *PeerJ*, v. 2, e453
   - **DOI:** `10.7717/peerj.453`
   - **Link oficial:** <https://doi.org/10.7717/peerj.453> (acesso aberto também em `arXiv:1407.6245`; arquivo local: `ARTIGOS_PDF/VanDerWalt_2014_scikit-image_Image_Processing_Python.pdf` e `VanDerWalt_2014_scikit-image_Image_Processing_Python.md`)
   - **Nível de leitura:** **Texto completo lido** (19 páginas integrais do PDF e texto extraído).

3. **Schindelin et al. (2012) — Plataforma interativa e extensível em Java (`Fiji/ImageJ`)**
   - **Título:** *Fiji: an open-source platform for biological-image analysis*
   - **Autores:** Johannes Schindelin, Ignacio Arganda-Carreras, Erwin Frise, Verena Kaynig, Mark Longair, Tobias Pietzsch, Stephan Preibisch, Curtis Rueden, Stephan Saalfeld, Benjamin Schmid, Jean-Yves Tinévez, Daniel James White, Volker Hartenstein, Kevin W. Eliceiri, Pavel Tomančák e Albert Cardona
   - **Ano:** 2012 (publicado online em 28/06/2012; edição de julho de 2012)
   - **Periódico:** *Nature Methods*, v. 9, n. 7, p. 676–682
   - **DOI:** `10.1038/nmeth.2019` (`PMID: 22743772`, `PMCID: PMC3855844`)
   - **Link oficial:** <https://doi.org/10.1038/nmeth.2019> (acesso aberto integral via PubMed Central: <https://pmc.ncbi.nlm.nih.gov/articles/PMC3855844/>)
   - **Nível de leitura:** **Texto completo lido** (texto integral extraído de PMC3855844).

---

## 2. Problema investigado

- **[Extraído — Otsu, 1979]:** Como selecionar automaticamente, sem supervisão e sem ajuste paramétrico complexo (como ajuste de misturas gaussianas por mínimos quadrados), um limiar ótimo de intensidade em histogramas de níveis de cinza para separar objetos do fundo — inclusive quando o vale entre picos no histograma é largo e raso, ruidoso ou fortemente desbalanceado em altura (Seção I, p. 62)?
- **[Extraído — van der Walt et al., 2014]:** Como prover uma biblioteca de código aberto em Python, interoperável com o ecossistema científico (`NumPy`, `SciPy`, `matplotlib`, `scikit-learn`), com API funcional consistente, cobertura rigorosa de testes e licença permissiva (Modified BSD), superando restrições de licenciamento comercial (MATLAB), complexidade de estudo/modificação em C/C++ (OpenCV) e acoplamento à interface gráfica (ImageJ/Fiji) (Seções *Introduction* e *Discussion — Related work*, p. 1–2, 15–16)?
- **[Extraído — Schindelin et al., 2012]:** Como modernizar a engenharia de software do ecossistema ImageJ (criado para biólogos, mas carente de controle de versão, gerenciamento de dependências, atualização automática e abstrações genéricas de dados) para transformar rapidamente algoritmos de visão computacional em plugins práticos, reprodutíveis e utilizáveis em conjuntos massivos de microscopia multidimensional (Seções *Introduction* e *How Fiji enhances ImageJ*, PMC3855844)?

---

## 3. Fundamentação

- **[Extraído — Otsu, 1979]:** A formulação baseia-se em análise discriminante clássica aplicada ao histograma normalizado de níveis de cinza $p_i = n_i / N$ ($i \in \{1, \dots, L\}$, $\sum p_i = 1$). Para uma dicotomia no limiar $k$ em classes $C_0 = [1, \dots, k]$ e $C_1 = [k+1, \dots, L]$, definem-se os momentos cumulativos de ordem zero e primeira ordem $\omega(k) = \sum_{i=1}^k p_i$ e $\mu(k) = \sum_{i=1}^k i p_i$, além da média global $\mu_T = \mu(L)$ (Eqs. 1–8). A variância total $\sigma_T^2$ decompõe-se exatamente na soma da variância intraclasse $\sigma_W^2$ com a variância entre classes $\sigma_B^2$: $\sigma_W^2 + \sigma_B^2 = \sigma_T^2$ (Eq. 16). Maximizar a separabilidade $\eta(k) = \sigma_B^2(k)/\sigma_T^2$ equivale a maximizar $\sigma_B^2(k)$ (baseada apenas em estatísticas de primeira ordem), obtida via busca sequencial na faixa efetiva $0 < \omega(k) < 1$ (Eqs. 12–19).
- **[Extraído — van der Walt et al., 2014]:** O fundamento estrutural é representar toda imagem como um *array* $n$-dimensional `NumPy` (2D escala de cinza, 3D multicanal ou volume, 4D volume multicanal) com faixas numéricas padronizadas (`float` em $[0,1]$ ou $[-1,1]$; `uint8` em $\{0,\dots,255\}$) e semântica *"Anything In, Anything Out"* nas funções. Os algoritmos clássicos de PDI cobrem conversão de cores (`color`), equalização de histograma (`exposure`), detecção de bordas/filtros lineares e de ordem (`filter`, incluindo Canny, Sobel, mediana por `rank.median`, filtro gaussiano / Diferença de Gaussianos), morfologia matemática (`morphology`, abertura, esqueletização, rotulagem conectada `label`), medidas geométricas (`measure.regionprops`, `profile_line`, RANSAC), detecção de feições (`feature.peak_local_max`, ORB), restauração/denoising (`restoration`), transformadas geométricas e de Hough (`transform`) e segmentação (`segmentation`).
- **[Extraído — Schindelin et al., 2012]:** Fiji ancora-se em dois pilares arquiteturais: (i) compatibilidade retroativa com ImageJ acrescida de infraestrutura moderna (Git, Fiji Updater, *update sites* comunitários, integração com múltiplas linguagens de *script* como Jython, Clojure, Javascript, JRuby e Beanshell); e (ii) a biblioteca **`ImgLib`**, que separa a formulação matemática de um algoritmo da dimensionalidade (1D, 2D, 3D, $n$D+t), tipo de dado (8-bit, 16-bit etc.) e estratégia de armazenamento (memória, paginação em disco, rede), permitindo implementar detectores como Diferença de Gaussianos (DoG) e *Maximally Stable Extremal Regions* (MSER) uma única vez para dados arbitrários. Inclui ainda ponte com aprendizado de máquina clássico via plugin *Trainable Segmentation* (biblioteca WEKA).
- **[Análise crítica — Agente E]:** Em conjunto, essas três referências formam o núcleo metodológico do PDI clássico: métodos determinísticos e explicitamente parametrizáveis (limiarização por momentos de histograma, filtragem espacial/morfológica, extração de descritores geométricos e registro por transformações explícitas) onde cada operação tem interpretação matemática direta e baixo custo computacional, sem exigir grandes volumes de dados anotados.

---

## 4. Metodologia

- **[Extraído — Otsu, 1979]:**
  - Formulação analítica de $\sigma_B^2(k) = \frac{[\mu_T \omega(k) - \mu(k)]^2}{\omega(k)[1 - \omega(k)]}$ (Eq. 18) e busca exaustiva discreta $k^* = \arg\max_{1 \le k < L} \sigma_B^2(k)$ (Eq. 19).
  - Extensão direta para multilimiarização ($M$ classes via $M-1$ limiares discretos $1 \le k_1 < k_2 < \dots < k_{M-1} < L$, reduzindo de $3M-1$ parâmetros contínuos do modelo gaussiano para $M-1$ limiares discretos; Seção III-B).
  - Avaliação qualitativa/quantitativa em imagens 64×64 pixels (caracteres tipográficos com 16 níveis, texturas com 64 níveis incluindo vale plano e pico unimodal, e células com 32 e 256 níveis em 3 classes: fundo, citoplasma e núcleo; Figs. 1–3).
- **[Extraído — van der Walt et al., 2014]:**
  - Engenharia de software: API majoritariamente funcional em Python puro com núcleos críticos de desempenho em **Cython**; licença *Modified BSD*; cobertura de testes unitários superior a 87% (versão 0.10), integração contínua (Travis CI), verificação de estilo PEP8/`flake8` e documentação automática em Sphinx.
  - Fluxos exemplificados no artigo: (a) segmentação de moedas (`data.coins`: histograma `np.histogram`, limiarização adaptativa local `filter.threshold_adaptive`, máximos locais `feature.peak_local_max`, bordas de Canny `filter.canny`, rotulagem `morphology.label` e propriedades `measure.regionprops`: caixa envolvente, posição, área, excentricidade, perímetro e momentos; Figs. 1a–f); (b) monitoramento de propagação de trincas em gotas coloidais via transformada circular de Hough (`transform.hough_circle`) e perfis radiais (Fig. 2); (c) perfil de fluorescência ao longo de linha (`measure.profile_line`, Fig. 3); (d) detecção de defeitos cristalinos (discordâncias) e impurezas em *wafers* de silício por fotoluminescência usando `transform.hough_line` e filtro passa-banda por Diferença de Gaussianos via `filter.gaussian_filter` (Fig. 4); e (e) registro/costura panorâmica com descritores binários ORB, rejeição de *outliers* por RANSAC (`measure.ransac`) e deformação inversa (`transform.warp`, Fig. 5).
- **[Extraído — Schindelin et al., 2012]:**
  - Empacotamento autocontido em Java com controle de menus curado, *Script Editor* multilíngue e sistema de atualização distribuído (Fiji Updater).
  - Três fluxos completos de microscopia descritos no artigo: (1) costura (*stitching*) de pilhas confocais 2D/3D por correlação de fase e otimização global de deslocamentos (Fig. 3a–e); (2) reconstrução de mosaicos massivos de microscopia eletrônica de transmissão por seções seriadas (ssTEM) via **TrakEM2**, incluindo correção de distorção de lente, alinhamento global por SIFT, contornos ativos, *level sets* e *Trainable Segmentation* baseado na biblioteca **WEKA** (Fig. 3f–j); e (3) processamento multivisão de SPIM com integração ao *Micro-Manager* e registro baseado em marcadores fiduciais (Fig. 3k–o).

---

## 5. Resultados

- **[Extraído — Otsu, 1979]:**
  - Demonstrou seleção estável e automática de limiares usando apenas integração (momentos cumulativos) do histograma, evitando a instabilidade de métodos baseados em diferenciação local de vales.
  - Introduziu a métrica normalizada $\eta^* = \eta(k^*) \in [0, 1]$ como medida da separabilidade das classes (bimodalidade do histograma), **invariante sob transformações afins da escala de cinza** ($g' = ag + b$, Seção III-A, p. 64), além de estimativas das frações de área ($\omega_0, \omega_1$) e médias de nível ($\mu_0, \mu_1$).
  - Obteve separação coerente em cenários adversos: texto impresso com contraste reduzido (Fig. 1: $\eta^*=0{,}894$ vs $\eta^*=0{,}853$), texturas com vale amplo/plano e distribuição unimodal (Fig. 2: $\eta^*=0{,}887$, $0{,}873$, $0{,}767$) e segmentação celular em 3 classes (Fig. 3: $\eta^*=0{,}893$).
- **[Extraído — van der Walt et al., 2014]:**
  - Consolidou uma biblioteca multiplataforma madura (mais de 100 colaboradores e >5.000 downloads mensais no PyPI em março de 2014) organizada em 15 submódulos (v0.10), capaz de sustentar aplicações científicas e industriais reais (ex.: inspeção automática de defeitos em *wafers* na BT Imaging alimentando classificadores de ML).
  - Apresentou comparação explícita entre ferramentas: `scikit-image` supera `Fiji` em automação *headless* (clusters HPC, *backends* web e processamento em lote sem dependências de GUI) e consistência de API; supera `MATLAB Image Processing Toolbox` por ausência de custo de licença (especialmente por núcleo paralelo) e transparência do código-fonte; e complementa `OpenCV` (focado em tempo real 2D em C/C++ com API imperativa) e `Mahotas` (templated C++) via interoperabilidade direta em *arrays* `NumPy`.
- **[Extraído — Schindelin et al., 2012]:**
  - Viabilizou pipelines interativos em escala de terabytes em hardware padrão, com adoção global (~20.000 usuários estimados à época; Fig. 4).
  - Provou que um único algoritmo escrito sobre `ImgLib` (ex.: DoG e MSER, Fig. 2b–j) opera de forma idêntica sobre sinais 1D, fatias 2D e volumes 3D sem duplicação de código, e que o ecossistema de plugins cooperantes (como TrakEM2 + WEKA) conecta diretamente segmentação clássica e aprendizado de máquina raso em microscopia eletrônica.

---

## 6. Limitações

- **[Extraído — Otsu, 1979]:**
  - O critério $\sigma_B^2(k)$ opera exclusivamente sobre o histograma 1D global de intensidades, ignorando completamente informação espacial (vizinhança, bordas, textura) (Seção I e III-B).
  - O próprio autor adverte que, na extensão multilimiarização, os limiares selecionados tornam-se progressivamente **menos confiáveis à medida que o número de classes $M$ aumenta**, pois o critério 1D perde significado discriminativo e a busca combinatória cresce em complexidade (Seção III-B, p. 64).
  - A unimodalidade da função objetivo $\sigma_B^2(k)$ foi observada empiricamente (Figs. 1–2), mas **sem demonstração matemática rigorosa** no artigo (Seção III-D, p. 66).
- **[Extraído — van der Walt et al., 2014]:**
  - A implementação majoritária em linguagem de alto nível (Python) impõe compromisso de velocidade frente a bibliotecas puramente C/C++ em cenários estritos de tempo real, exigindo Cython para gargalos críticos (Seção *Discussion — Related work*, p. 16).
  - Políticas estritas de revisão de código e testes podem tornar a incorporação de novos algoritmos mais lenta do que em repositórios permissivos de plugins; além disso, na versão 0.10 descrita, suporte multidimensional avançado e operações baseadas em grafos ainda constavam como metas de *roadmap* (p. 16–17).
- **[Extraído — Schindelin et al., 2012]:**
  - A dependência de Java levanta discussões de desempenho frente a implementações especializadas em C/C++ em certas cargas intensivas (Seção *Conclusion*).
  - Conforme apontado criticamente por van der Walt et al. (2014, p. 16), muitas funções/macros do Fiji ativam elementos de interface gráfica (GUI), dificultando execução *headless* em servidores ou pipelines em lote automatizados, e a política inclusiva de plugins gera inconsistências de API e variação na qualidade da documentação entre plugins de terceiros.
- **[Análise crítica — Agente E]:** Em caracterização de materiais (MEV, AFM e microscopia óptica de grafeno/materiais 2D), a limiarização global de Otsu falha sistematicamente sob **iluminação não uniforme / gradientes de fundo**, **sobreposição de níveis de cinza entre fases** (como observado na linha de base clássica de Gerçek et al., 2025 para carbonetos em MEV) ou **flocos ultrafinos com baixo contraste sobre o substrato**. Nessas condições, Otsu só permanece válido após correção explícita de fundo (*top-hat*, subtração polinomial, normalização L\*a\*b\*) ou mediante limiarização local/adaptativa (`threshold_adaptive`/Sauvola/Niblack) e pós-processamento morfológico — e não substitui modelos de instância quando há sobreposição física de flocos.

---

## 7. Contribuição para a dissertação

- **[Análise crítica — Agente E]:**
  - **Fundamentação do módulo de PDI clássico e extração de descritores:** Como o pré-projeto da dissertação (*pre-projeto-da-selecao.md*, Seção 3.3) prevê explicitamente o desenvolvimento em Python com `scikit-image` (citando van der Walt et al., 2014) e `OpenCV`, este tripé bibliográfico estabelece a linha de base metodológica obrigatória antes de se recorrer a *deep learning*.
  - **Auditoria e reprodutibilidade laboratorial:** `Fiji/ImageJ` (Schindelin et al., 2012) representa o padrão de referência interativo adotado cotidianamente em laboratórios de microscopia (útil para inspeção visual, calibração de escalas e validação cruzada manual/semiautomática com *Trainable Weka Segmentation*), enquanto `scikit-image` fornece a arquitetura modular, testável e *headless* recomendada para o software da dissertação.
  - **Extração quantitativa de morfologia em MEV/AFM:** O encadeamento clássico `filtro de ruído -> correção de fundo -> Otsu / limiarização adaptativa -> morfologia matemática / watershed -> morphology.label -> measure.regionprops` (van der Walt et al., 2014) permite extrair diretamente área, perímetro, circularidade/excentricidade, diâmetro equivalente e distribuição de tamanho lateral de flocos de grafeno sem necessidade de grandes conjuntos rotulados — desde que haja contraste suficiente entre floco e substrato.

---

## 8. Possíveis aplicações

- **[Análise crítica — Agente E (propostas investigativas a validar experimentalmente, não resultados publicados)]:**
  1. **Linha de base determinística para MEV de grafeno/GO:** Avaliar um pipeline em `scikit-image` combinando filtro preservador de bordas (`median` ou filtro bilateral/NLM), correção de iluminação não uniforme (*rolling-ball* / *top-hat* morfológico), limiarização de Otsu ou adaptativa, separação de flocos tocantes por transformada de distância + *watershed* e extração de área, perímetro e circularidade via `regionprops`, utilizando o índice de separabilidade $\eta^*$ de Otsu (1979) como indicador automático de qualidade de binarização (sinalizando imagens onde o histograma não é bimodal para inspeção ou encaminhamento a modelos aprendidos).
  2. **Validação cruzada inter-ferramentas:** Comparar descritores geométricos obtidos pelo pipeline Python/`scikit-image` com medições de referência realizadas pelos pesquisadores do PPGCEM no `Fiji/ImageJ` sobre as mesmas micrografias MEV (verificando divergências por convenções de conectividade 4 vs. 8 e estimativa de perímetro).
  3. **Pré-rotulagem assistida (*human-in-the-loop*):** Utilizar `Fiji` (*Trainable Weka Segmentation*) ou scripts interativos com `scikit-image` para gerar máscaras iniciais auditáveis de flocos em conjuntos pequenos antes de eventual treinamento supervisionado.

---

## 9. Evidências

- **Otsu (1979):**
  - Seção I (p. 62): motivação contra detecção de vale por diferenciação e misturas gaussianas paramétricas.
  - Seção II, Eqs. (1)–(19) (p. 63): definição formal de $\omega(k)$, $\mu(k)$, $\sigma_W^2$, $\sigma_B^2$, $\sigma_T^2$, equivalência de $\lambda, \kappa, \eta$ e busca de $k^*$.
  - Seção III-A (p. 64): invariância afim de $\eta^*$ como medida de bimodalidade.
  - Seção III-B (p. 64): extensão multilimiarização e perda de confiabilidade para $M$ elevado.
  - Seção III-C, Figs. 1–3 (p. 64–65): resultados numéricos ($\eta^*, \omega_0, \omega_1, \mu_0, \mu_1$) em caracteres, texturas e células em 3 classes.
- **van der Walt et al. (2014):**
  - *Getting Started* e Fig. 1 (p. 2–5): código reproduzível com `threshold_adaptive`, `peak_local_max`, `canny`, `label`, `regionprops`.
  - *Library Overview* e *Data Format and Pipelining* (p. 5–7): lista dos 15 submódulos da v0.10 e contrato de *arrays* `NumPy` / faixas `float` vs `uint8`.
  - *Development Practices* (p. 7–8): licença Modified BSD, Cython, cobertura de testes >87%, CI e PEP8.
  - *Usage Examples* e Figs. 2–5 (p. 8–15): Hough circular/linear, `profile_line`, comparação `median` vs `gaussian_filter` (p. 10), DoG em *wafers* de silício (Fig. 4, p. 11), registro ORB+RANSAC+`warp` (p. 12–15).
  - *Discussion — Related work* (p. 15–16): comparação crítica com Mahotas, Fiji/ImageJ, MATLAB e OpenCV.
- **Schindelin et al. (2012):**
  - *How Fiji enhances ImageJ* e Fig. 1 (PMC3855844): Git, Fiji Updater, *update sites*, organização de plugins e ponte Miji/MATLAB.
  - *Scripting and ImgLib for implementing algorithms* e Fig. 2: Jython/Clojure/Javascript/Beanshell/JRuby e independência dimensional de `ImgLib` com DoG e MSER em 1D/2D/3D.
  - *Synergy as a design principle* e Fig. 3: *Stitching*, `TrakEM2` (SIFT, *Active Contours*, *Level Sets*, *Trainable Segmentation* com **WEKA**), e SPIM + Micro-Manager.

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta**
- **Justificativa:** Os três trabalhos compõem o alicerce técnico direto do sistema proposto na dissertação: Otsu (1979) fornece o critério clássico mais citado de binarização não supervisionada (além da métrica diagnóstica $\eta^*$); `scikit-image` (van der Walt et al., 2014) é a biblioteca central prevista na metodologia do pré-projeto para implementação modular em Python (*headless*, auditável e reprodutível); e `Fiji/ImageJ` (Schindelin et al., 2012) é o padrão laboratorial de comparação e referência em análise microscópica. Dominar suas capacidades e limites evita reinventar rotinas consolidadas ou aplicar modelos profundos onde PDI clássico basta.
