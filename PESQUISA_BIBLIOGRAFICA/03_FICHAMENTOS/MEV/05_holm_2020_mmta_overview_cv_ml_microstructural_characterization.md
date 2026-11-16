# Fichamento 05 — Holm et al. (2020): Visão Computacional e Aprendizado de Máquina para Caracterização e Análise Microestrutural

> **Status de Leitura e Verificação:** **Texto completo lido integralmente** em `_scratch/textos_extraidos/Holm_2020_Overview_CV_ML_Microstructural_Characterization.md` (15 páginas, 9 figuras, 128 referências). A tabela suplementar `Table SI` com detalhamento dos códigos citados na Seção II encontra-se apenas no suplemento online da editora e não compõe o texto extraído. **Conferência crítica de DOI:** o DOI verdadeiro e verificado deste artigo é **`10.1007/s11661-020-06008-4`** (OpenAlex W3031142281 e cabeçalho do PDF).

---

## 1. Identificação bibliográfica

- **Título:** Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis
- **Autores:** Elizabeth A. Holm, Ryan Cohn, Nan Gao, Andrew R. Kitahara, Thomas P. Matson, Bo Lei, Srujana Rao Yarasi
- **Ano:** 2020 (submetido em 3 de maio de 2020; publicado online em 29 de setembro de 2020; fascículo de dezembro de 2020)
- **Periódico:** *Metallurgical and Materials Transactions A* (TMS / ASM International / Springer), Vol. 51A, No. 12, pp. 5985–5999
- **DOI:** `10.1007/s11661-020-06008-4`
- **Link oficial:** [https://doi.org/10.1007/s11661-020-06008-4](https://doi.org/10.1007/s11661-020-06008-4) (`https://link.springer.com/content/pdf/10.1007/s11661-020-06008-4.pdf`)
- **Métricas catalogadas:** 290 citações registradas em `_scratch/verified_catalog.json` (OpenAlex). *(Artigo-chave também citado no pré-projeto original de seleção de Emerson Gomes no PPGCEM/UFCA.)*

---

## 2. Problema investigado

- **[Extraído do artigo]:** A caracterização microestrutural quantitativa esbarra historicamente em dois problemas fundamentais (Seção I):
  1. **O que medir (*What to measure*):** microestruturas reais ocupam um espaço visual imenso (Fig. 1) e frequentemente apresentam múltiplas escalas ou morfologias complexas para as quais não existe uma métrica universal evidente que conecte processamento, estrutura e propriedade (PSP).
  2. **Como medir (*How to measure it*):** mesmo métricas conceitualmente simples exigem localizar fronteiras ambíguas ou descontínuas via segmentação — como zonas descarbonetadas difusas ao redor de carbonetos em MEV (Fig. 1d) ou contornos de grão mal revelados (*"missing boundaries"*, Fig. 1a) — onde algoritmos convencionais falham e a avaliação humana é lenta, subjetiva e pouco reprodutível.
  Os autores investigam como métodos modernos de **Visão Computacional (CV)** e **Aprendizado de Máquina (ML)** codificam o conteúdo visual de micrografias em vetores de características e resolvem, de maneira objetiva e autônoma, a taxonomia completa de análise de imagens microestruturais.

---

## 3. Fundamentação

- **[Extraído do artigo — Seção II]:**
  - **Codificação visual (CV):** contrasta representações baseadas em características projetadas por especialistas (*feature-based*, como SIFT/gradientes em DeCost & Holm, 2015) com representações baseadas em **Redes Neurais Convolucionais (CNNs)**, que superaram os métodos manuais desde o AlexNet (2012). Destacam-se duas extrações:
    1. **Vetor de camada de CNN por imagem (`C(i)`, Fig. 2):** usa *transfer learning* de redes pré-treinadas em imagens naturais (ex.: `VGG16` na base `ImageNet`) truncadas antes da camada classificadora, aplicando redução de dimensionalidade como `PCA` ou `VLAD`. Propriedade crítica: convoluções conferem invariância à **translação**, mas **não à rotação nem à escala**. Além disso, camadas rasas codificam vizinhanças locais (ideais para microestruturas simples), enquanto camadas profundas codificam estruturas multiescala, exigindo seleção empírica por tentativa e erro.
    2. **Vetor de hipercoluna por pixel (`H(p)`, PixelNet, Fig. 2):** empilha as ativações de **todas** as camadas convolucionais correspondentes à posição espacial real de um pixel (ou subconjunto esparso de pixels por economia de memória), preservando contexto multiescala para **segmentação semântica**.
  - **Modelos de ML (Seção II.B):** compara algoritmos **supervisionados** — *Support Vector Machines* (SVM, baseados em hiperplanos separadores), *Random Forests* (RF, árvores de decisão interpretáveis, porém mais difíceis de aplicar a representações visuais complexas) e *Redes Neurais Artificiais / CNNs* (flexíveis e escaláveis, porém *"caixas-pretas"*) — e **não supervisionados** — *k-means* (agrupamento por centróides no espaço *N*-D, problema NP-difícil sensível a inicialização) e *t-SNE* (projeção não linear em 2D/3D que preserva vizinhança local, mas exige recálculo integral para novos dados, não servindo diretamente para classificar amostras inéditas).
  - **Riqueza informacional de micrografias (Seção II.C):** explica por que sistemas CV/ML funcionam em ciência dos materiais com **pouquíssimas imagens originais (às vezes `< 10` micrografias)**: diferente de fotos naturais ("um gato"), uma única micrografia contém centenas de partículas/precipitados e praticamente nenhum fundo irrelevante. Redundância de campos não sobrepostos, padronização de aquisição (instrumento, magnificação, configurações) e *data augmentation* (rotações, subamostragem, transformações afins — lembrando que *augmentation* facilita o treino, mas **não cria informação física nova**) elevam a robustez.
  - **Taxonomia de tarefas de análise (Seção III, Fig. 3 em MEV de pó metálico):**
    1. **Classificação de imagem:** atribui classe à micrografia inteira (ex.: `"powder"`).
    2. **Segmentação semântica:** rotula cada pixel (ex.: `"partícula"` vs. `"fundo"`), mas **não separa objetos individuais quando há contato ou sobreposição**.
    3. **Detecção de objetos:** localiza caixas delimitadoras (*bounding boxes*) ao redor de instâncias individuais.
    4. **Segmentação de instâncias:** atribui máscaras de pixels individuais a cada objeto distinto, mesmo sob sobreposição densa.

---

## 4. Metodologia

- **[Extraído do artigo]:** Revisão aplicada e demonstrativa articulada por estudos de caso experimentais e sintéticos conduzidos pelo grupo da Carnegie Mellon University e colaboradores sobre micrografias ópticas, tomográficas e **MEV**:
  - **Classificação e busca visual (UHCSDB):** `961` micrografias de aços de ultra-alto carbono (incluindo MEV) codificadas com camada CNN + redução de dimensão + distância Euclidiana (`L²`), `t-SNE` e `SVM linear`.
  - **Quantificação direta sem segmentação:** `15.213` micrografias sintéticas de crescimento de grão isotrópico simuladas no código Monte Carlo cinético `SPPARKS`, avaliadas por CNN com camada de regressão totalmente conectada sob remoção arbitrária de contornos (fração de *missing boundaries* até `0,4`).
  - **Inferência composicional em MEV por informação latente:** base de `2.543` imagens MEV de inclusões em aço balanceadas em `5` tipos (rotuladas originalmente com EDS) usadas para retreinar CNN pré-treinada e testar em `509` imagens inéditas.
  - **Segmentação semântica via `PixelNet` (`hypercolumn`):** `20` imagens UHCS MEV anotadas manualmente para treino + `4` de teste; e `30` fatias tomográficas `Al-Zn` para treino + `10` de teste.
  - **Segmentação composta em MEV de fluência (ECCI-SEM, superliga de Ni):** `17` imagens MEV (`15` treino / `2` teste) comparando `ImageJ` vs. `U-Net` direta vs. arquitetura em **duas etapas** (CNN de traços lineares combinada à máscara CNN de textura de região deformada/não deformada).
  - **Detecção de objetos e segmentação de instâncias em pós metálicos MEV (`Faster R-CNN` / `Mask R-CNN`):** transferência de pesos `COCO` com apenas **`5` imagens MEV anotadas** (centenas de partículas por imagem; validação cruzada `3` treino / `2` teste) para partículas principais e partículas-satélite aderidas.
  - **Métricas não supervisionadas para partículas (`Inconel-718` MEV):** segmentação por *connected-component labeling* de `~1.100` partículas -> vetor de camada CNN -> `PCA` -> *k-means* (`8` clusters) -> mapa de densidade visual `t-SNE`.

---

## 5. Resultados

- **[Extraído do artigo]:**
  - **Classificação/Busca (UHCSDB, Fig. 4):** a distância Euclidiana entre vetores CNN recuperou microconstituintes semelhantes até em magnificações diferentes; `t-SNE` agrupou naturalmente esferoidita, carboneto em rede e perlita; e a `SVM linear` atingiu **`99 ± 1%` de acurácia**.
  - **Regressão de tamanho de grão sem segmentação (Fig. 5a):** erro padrão de **`2,3%`** em policristais perfeitos, subindo linearmente para apenas **`3,9%`** com `40%` de contornos ausentes (superando/atendendo à precisão ASTM E112-13 de `±0,5` unidades).
  - **Composição de inclusões apenas por MEV (Fig. 5b):** **`76%`** de acurácia global nas `509` imagens de teste (contra `20%` ao acaso), concentrando erros em inclusões de sulfeto com sobreposição composicional — tarefas quase impossíveis a olho nu.
  - **Segmentação semântica por `PixelNet` (Fig. 6):** acurácia de **`93%`** no aço UHCS em MEV (capturando inclusive "furos" omitidos pelo anotador humano!) e **`99,6%`** nas fatias `Al-Zn` (ignorando automaticamente artefatos de preparação como borda da amostra, poros e marca do feixe).
  - **Limite instrutivo da `U-Net` pura vs. máscara de textura (Fig. 7):** ao tentar separar linhas de discordâncias e contornos `gamma-gamma'` (ambos representados por linhas de 1 pixel de largura em apenas 17 imagens), a `U-Net` treinada diretamente falhou em ignorar os contornos ou subestimou discordâncias horizontais/verticais. A combinação lógica **bordas CNN ∩ máscara de textura deformada CNN** isolou corretamente as discordâncias.
  - **Detecção e segmentação de instâncias em MEV de pós sobrepostos (Fig. 8):** em apenas 5 imagens anotadas, `Faster R-CNN` alcançou recall de **`80%`** e precisão de **`94%`** na detecção (perdendo apenas partículas pequenas/oclusas de baixo peso volumétrico), enquanto `Mask R-CNN` atingiu precisão média de **`97,5%`** e recall de **`95,4%`** na segmentação das partículas. Para **partículas-satélite** (maior subjetividade humana), atingiu precisão de **`69,2%`** e recall de **`54,5%`**, ainda suficientes para tendências estatísticas em alta vazão.
  - **Assinatura não supervisionada de pós (`Inconel-718`, Fig. 9):** *k-means* (`8` clusters) e `t-SNE` organizaram `~1.100` partículas por rugosidade, forma, alongamento e aglomeração, criando "impressões digitais" quantitativas mais ricas que simples distribuições de tamanho.

---

## 6. Limitações

- **[Reconhecidas pelos autores]:**
  - **Não invariância rotacional e de escala em CNNs:** exige atenção no protocolo de coleta e uso consciente de *data augmentation*.
  - **Empirismo na escolha de camadas e arquitetura:** não existe método *a priori* para definir qual camada de uma CNN pré-treinada representa melhor determinada microestrutura (exige tentativa e erro).
  - **Falha quando classes distintas compartilham geometria de contorno local idêntica em datasets pequenos:** exemplificado pelo fracasso da segmentação em estágio único na superliga (Fig. 7).
  - **Dependência de metadados e escassez para PSP:** estabelecer conexões processamento–estrutura–propriedade (Seção IV.B) sofre com falta de grandes bancos com histórico/propriedades e com a limitação fundamental de inferir características **3D** controladoras de propriedade a partir de seções **2D** (estereologia quantitativa em micrografias ≠ projeção óptica de fotos naturais).
  - **Problema aberto da interpretabilidade (*Black Box*, Seção IV.C):** ainda não há solução geral para mapear assinaturas visuais internas do vetor de características às leis físicas subjacentes, o que gera cautela científica em análises explicativas.
- **[Críticas adicionais — Agente C]:**
  - **Ausência de estudos de caso em materiais bidimensionais (grafeno/2D):** toda a casuística concentra-se em ligas metálicas (aços, `Al-Zn`, superligas de `Ni`) e pós metálicos para manufatura aditiva (`Inconel-718`); embora a **taxonomia e a `Mask R-CNN` para partículas sobrepostas** sejam diretamente transferíveis para flocos de grafeno no MEV, os contrastes atômicos sutis, efeitos de carregamento e substratos de 2D exigem validação específica.
  - **Métricas de acurácia global em segmentação:** o relato de `"93%"` e `"99,6%"` sem detalhar IoU/Dice por classe minoritária na revisão principal pode mascarar desequilíbrios em estruturas raras (como discutido mais tarde em `Azimi et al., 2018` e `Gerçek et al., 2025`).

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Este artigo é a **principal bússola arquitetural** para evoluir o pré-projeto original de Emerson Gomes (que já citava `Holm et al., 2020`) rumo ao tema atual de caracterização de grafeno por MEV:
  1. **Diagnóstico exato do algoritmo por tarefa morfológica:** a Seção III (Fig. 3) resolve uma decisão técnica crucial do software da dissertação — se houver **flocos de grafeno isolados** (como no protocolo VAMAS), *segmentação semântica* clássica ou U-Net + componentes conectados bastam; mas se houver **flocos sobrepostos/aglomerados** (caso real em dispersões drop-cast ou CVD policristalino), é obrigatório usar **segmentação de instâncias** (`Mask R-CNN`, `YOLOv8-seg`) para não fundir dois flocos adjacentes em uma única partícula falsa gigante!
  2. **Prova de viabilidade em pequena escala laboratorial:** mostra que com boa padronização de aquisição e *transfer learning* (`VGG16` / `PixelNet` / `Mask R-CNN`), **`3` a `20` micrografias MEV bem anotadas** (contendo dezenas/centenas de objetos cada) já viabilizam resultados quantitativos altamente úteis — algo totalmente compatível com a realidade experimental de um mestrado no PPGCEM/UFCA.
  3. **Alerta metodológico contra o uso ingênuo de IA:** reforça a regra da Missão 02 de que técnicas tradicionais (componentes conectados, regressão, *ImageJ*) têm domínio claro quando objetos são bem separados e de alto contraste, devendo-se reservar ML/DL para bordas difusas, artefatos de preparação, texturas multiescala e sobreposição de flocos.

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Adotar explicitamente a **taxonomia de 4 níveis de Holm et al. (2020)** como arquitetura modular do software proposto: (Módulo 1) triagem/agrupamento visual não supervisionado de micrografias MEV de grafeno (vetores CNN + `PCA` + `t-SNE` / *k-means* para catalogar morfologias de flocos vs. aglomerados vs. resíduos); (Módulo 2) segmentação semântica (`U-Net`/`PixelNet` ou `Otsu` adaptativo) para fração de recobrimento global; (Módulo 3) segmentação de instâncias para extrair `ECD`, `Feret`, razão de aspecto e circularidade de flocos individuais mesmo sob toque parcial.
  - Investigar o **paradigma híbrido em dois estágios (Fig. 7)** para grafeno: combinar detector de região/máscara de floco com detector de defeitos lineares (dobras/rugas), evitando que rugas internas sejam confundidas com bordas externas do floco.

---

## 9. Evidências

- **Seção I & Fig. 1 (pp. 5985–5986):** definição dos dois problemas fundamentais (*what to measure* e *how to measure*), incluindo exemplo MEV de aço com zona descarbonetada difusa (Fig. 1d).
- **Seção II & Fig. 2 (pp. 5986–5989):** formalismo de CNN layers vs. `hypercolumn` (`PixelNet`), invariância de translação vs. escala/rotação, comparação SVM/RF/ANN/*k-means*/*t-SNE*, e discussão sobre pequenas bases (`<10` micrografias ricas em objetos).
- **Seção III & Fig. 3 (pp. 5989–5990):** taxonomia das 4 tarefas visuais aplicada a micrografia MEV de pó metálico denso.
- **Seções III.A–D & Figs. 4–8 (pp. 5990–5995):** métricas numéricas completas (`99±1%` UHCSDB; `2,3–3,9%` SPPARKS; `76%` inclusões MEV; `93%` e `99,6%` PixelNet; falha/sucesso em `17` imagens ECCI-SEM com U-Net; `80%/94%` Faster R-CNN e `97,5%/95,4%` Mask R-CNN em `5` imagens MEV).
- **Seção IV & Fig. 9 (pp. 5995–5997):** fingerprinting de `~1.100` partículas MEV de `Inconel-718` via *k-means*/`t-SNE`, desafios de inferência 3D, conexões PSP e interpretabilidade.

---

## 10. Prioridade de estudo

- **Prioridade:** **ALTA (Artigo indispensável para 17/11/2026).**
- **Justificativa:** Já é citado no pré-projeto original do candidato, está integralmente verificado (com DOI exato `10.1007/s11661-020-06008-4`), e oferece o vocabulário taxonômico, os benchmarks quantitativos de viabilidade com poucos dados MEV (`3–20` imagens) e a justificativa cristalina que a banca cobrará para distinguir segmentação clássica, segmentação semântica, detecção de objetos e segmentação de instâncias em micrografias eletrônicas.
