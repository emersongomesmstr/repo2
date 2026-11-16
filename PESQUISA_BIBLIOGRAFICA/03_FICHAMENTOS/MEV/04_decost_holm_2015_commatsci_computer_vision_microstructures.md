# Fichamento 04 — DeCost & Holm (2015): Visão Computacional Baseada em *Bag of Visual Features* para Classificação e Busca de Microestruturas

> **Status de Leitura e Verificação:** **Resumo e metadados verificados** em `_scratch/verified_catalog.json` (OpenAlex W1141054642), **trecho da legenda da figura na página da editora** (ScienceDirect), **material técnico complementar das próprias autoras** sobre o trabalho ([`ElizabethHolm_Presentation.pdf`, CHiMaD 2016](https://chimad.northwestern.edu/docs/2016DATA_documents/ElizabethHolm_Presentation.pdf)) e **contextualização direta em `Holm et al. (2020)`** (texto completo lido). O PDF integral publicado em *Computational Materials Science* 110 (2015) 126–133 não esteve acessível neste ambiente (`oa_status: hybrid`, sem repositório verde indexado e falha de extração direta na ScienceDirect). Todas as distinções entre o que foi confirmado nos registros do artigo de 2015 e o que provém dos slides/revisão das autoras estão explicitadas abaixo.

---

## 1. Identificação bibliográfica

- **Título:** A computer vision approach for automated analysis and classification of microstructural image data
- **Autores:** Brian L. DeCost, Elizabeth A. Holm
- **Ano:** 2015 (1 de dezembro de 2015)
- **Periódico:** *Computational Materials Science*, Volume 110, pp. 126–133
- **DOI:** `10.1016/j.commatsci.2015.08.011`
- **Link oficial:** [https://doi.org/10.1016/j.commatsci.2015.08.011](https://doi.org/10.1016/j.commatsci.2015.08.011)
- **Métricas catalogadas:** 375 citações registradas em `_scratch/verified_catalog.json` (OpenAlex); 432 citações segundo snippet recente de busca; financiado por NSF `DMR-1307138`. *(O artigo também é citado no pré-projeto original de seleção de Emerson Gomes no PPGCEM/UFCA.)*

---

## 2. Problema investigado

- **[Extraído do resumo e material das autoras]:** Grandes acervos de imagens microestruturais (ópticas e eletrônicas de varredura) contêm informações ricas sobre composição, histórico de processamento e propriedades, mas os métodos tradicionais de caracterização exigem desenvolver métricas e algoritmos específicos caso a caso (*ad hoc*), geralmente dependentes de segmentação manual subjetiva e pouco transferíveis entre sistemas materiais distintos. A questão motivadora foi investigar se **representações genéricas de visão computacional** — tratando micrografias como imagens puras de textura e gradientes locais, sem definição manual prévia de descritores metalográficos — podem gerar assinaturas numéricas universais para **classificação automática** e **busca visual** em bases heterogêneas de microestruturas.

---

## 3. Fundamentação

- **[Extraído do resumo, ScienceDirect snippet e apresentação complementar CHiMaD 2016 de E. Holm & B. DeCost]:**
  - ***Bag of Visual Features* (BoVF / *Bag of Visual Words*):** trata uma micrografia não como objeto geométrico único, mas como uma coleção não ordenada (histograma de frequências) de padrões locais de gradiente de intensidade em múltiplas escalas.
  - **Detectores de pontos-chave (*keypoints*) e descritor SIFT:** emprega detectores de gradiente de contraste — especificamente *Difference of Gaussians* (DoG, sensível a *blobs*/manchas) e *Harris-Laplace* (sensível a cantos/*corners*) — e codifica cada vizinhança local com **SIFT** (*Scale Invariant Feature Transform*), um vetor de **128 elementos** baseado em histogramas espaciais de gradientes orientados, invariante à rotação e à escala local.
  - **Dicionário visual (*visual codebook*) por *k-means* / Voronoi:** agrupa os vetores SIFT de todo o conjunto por análise de *clusters* *k-means* (particionamento de Voronoi no espaço 128-D), definindo `N` centróides como "palavras visuais" (metafeatures como partículas, cantos, contornos planos, bordas, texturas granuladas).
  - **Classificação por *Support Vector Machine* (SVM):** projeta o vetor de frequência de palavras visuais ("impressão digital microestrutural") em hiperplanos separadores aprendidos de forma supervisionada.
  - **Evolução histórica documentada por `Holm et al. (2020)` (Seção II.A):** esse paradigma baseado em filtros/descritores projetados manualmente (*feature-based representations*, incluindo citações `[34, 35, 37, 38]` de DeCost & Holm) foi o alicerce da visão computacional em ciência dos materiais pré-deep learning, antes de ser superado em desempenho por representações aprendidas em camadas de Redes Neurais Convolucionais (CNNs pré-treinadas).

---

## 4. Metodologia

- **[Extraído do resumo verificável e fontes complementares das autoras]:**
  - **Base de imagens:** micrografias heterogêneas (acervo da biblioteca *DoITPoMS Micrograph Library*, Universidade de Cambridge, segundo o material das autoras e citação em `Holm et al., 2020`), organizadas em **7 grupos/classes microestruturais** no experimento principal de classificação (trecho verificado na legenda da figura em ScienceDirect cita entre os sete grupos: *brass/bronze*, *ductile cast iron*, *gray cast iron*; os quatro restantes e o número exato total de imagens utilizadas no teste de 2015 não constam nos resumos/trechos públicos).
  - **Extração de assinatura visual:** detecção de *keypoints* -> extração de descritores locais SIFT -> quantização vetorial contra dicionário visual aprendido por *k-means* -> construção do histograma de palavras visuais normalizado por imagem.
  - **Avaliação supervisionada e busca:** treinamento e avaliação de classificador **SVM** em esquema de **validação cruzada *5-fold*** sobre as 7 classes, além da implementação de um **motor de busca visual** baseado em similaridade entre histogramas de palavras visuais.

---

## 5. Resultados

- **[Extraído exclusivamente do resumo verificado em `verified_catalog.json`]:**
  - A representação por *bag of visual features* gerou assinaturas microestruturais genéricas capazes de capturar similaridades visuais entre classes distintas de materiais sem engenharia prévia de métricas metalográficas específicas.
  - O classificador **SVM** treinado sobre essas assinaturas alcançou **acurácia superior a 80% na classificação entre os 7 grupos microestruturais em validação cruzada *5-fold***.
  - A implementação do **motor de busca visual** demonstrou a capacidade de recuperar as imagens mais similares em uma base microestrutural dada uma imagem de consulta.
- *(Nota: resultados adicionais mostrados nos slides CHiMaD 2016 de Holm — como ~95% em pós metálicos SEM e mapa t-SNE de 894 aços — pertencem a apresentações/extensões posteriores do grupo, 2016–2017, não sendo atribuídos como resultados publicados no artigo de 2015 sem o texto completo.)*

---

## 6. Limitações

- **[Reconhecidas no resumo / fontes das autoras]:**
  - O resumo assinala explicitamente que os experimentos demonstram tanto o potencial quanto **as limitações dos conceitos clássicos de visão computacional** na ciência microestrutural.
  - Em `Holm et al. (2020)` (Seção II.A), as próprias autoras reconhecem que abordagens baseadas em filtros fixos selecionados por humanos (como SIFT + BoVF) apresentam desempenho inferior às representações hierárquicas aprendidas por CNNs.
- **[Críticas adicionais — Agente C]:**
  - **Perda de informação espacial global e métrica absoluta:** por definição, *bag of visual features* descarta a geometria global dos objetos (conectividade, contorno completo de um floco, área real em `µm²`, diâmetro de Feret ou razão de aspecto). Consequentemente, serve para classificar/recuperar *texturas de micrografias inteiras*, mas **não resolve segmentação nem medição dimensional** exigidas por normas de grafeno como `ISO/TS 21356-1` e `VAMAS TWA 41`.
  - **Invariância de escala pode ser armadilha em MEV:** descritores locais SIFT buscam invariância de escala em termos de pixels; se duas micrografias MEV de grafeno tiverem magnificações diferentes (`5.000×` vs. `25.000×`), o algoritmo sem calibração física em nanômetros por pixel confunde flocos micrométricos com subestruturas nanométricas.
  - **Restrição documental:** por ausência do PDF completo nesta execução, não foi possível auditar o tamanho exato do dicionário `N`, o kernel da SVM, a matriz de confusão entre as 7 classes nem eventuais pré-processamentos das imagens originais.

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Como já aparecia citado nas referências do **pré-projeto da seleção de Emerson Gomes (2026)**, `DeCost & Holm (2015)` é o elo histórico que explica a transição da proposta original para o escopo investigativo atual:
  1. Demonstra a viabilidade de representar microestruturas sem criar heurísticas manuais frágeis para cada material — base conceitual útil caso a ferramenta do PPGCEM precise organizar um **catálogo visual / banco de imagens** de micrografias MEV heterogêneas (grafeno, compósitos, ligas, cerâmicas) por similaridade ou tipo de morfologia (ex.: flocos isolados vs. aglomerados vs. filmes contínuos).
  2. Ao mesmo tempo, evidencia os **limites das técnicas clássicas pré-CNN** e da análise puramente por textura global: para medir dimensões laterais de flocos de grafeno no MEV, métodos que preservam máscara e fronteira espacial (segmentação clássica supervisionada ou arquiteturas encoder-decoder / detecção de instâncias) são indispensáveis.

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Usar representação por assinatura visual (ou *embeddings* de CNN/t-SNE, conforme evolução em `Holm et al., 2020`) como **camada inicial de triagem/indexação** no banco de imagens do PPGCEM/UFCA para agrupar automaticamente micrografias MEV por classe de amostra ou identificar *outliers*/artefatos visuais, antes de enviá-las ao módulo geométrico de medição de flocos.
  - Usar `DeCost & Holm (2015)` vs. `Holm et al. (2020)` na revisão da dissertação para justificar comparativamente **quando algoritmos clássicos leves bastam** e **quando modelos profundos trazem ganho comprovado**.

---

## 9. Evidências

- **Abstract e metadados em `_scratch/verified_catalog.json` (linhas 869–893):** descrição do modelo *bag of visual features*, classificador SVM em 7 grupos microestruturais com acurácia `> 80%` em *5-fold CV* e motor de busca visual.
- **ScienceDirect figure caption snippet:** enumeração parcial de classes de teste (*brass/bronze, ductile cast iron, gray cast iron*) dentre as 7 classes.
- **Apresentação complementar de E. Holm & B. DeCost (`ElizabethHolm_Presentation.pdf`, slides 3–10, CHiMaD 2016) e `Holm et al. (2020)` (`10.1007/s11661-020-06008-4`, Seção II.A e Ref. `[37]`):** detalhamento do fluxo DoG + Harris-Laplace + SIFT (128-D) + k-means/Voronoi + histograma de palavras visuais (100 palavras mais frequentes no Cambridge DoITPoMS Micrograph Library).
- *(Texto integral do artigo de 2015 pendente de verificação em acesso institucional.)*

---

## 10. Prioridade de estudo

- **Prioridade:** **MÉDIA (complementar à leitura principal de `Holm et al., 2020`).**
- **Justificativa:** É um trabalho fundacional e diretamente citado no pré-projeto do candidato, excelente para situar o início da aplicação de Visão Computacional em microestruturas. Porém, para estudo imediato visando a apresentação de 17/11/2026 e o desenvolvimento metodológico de segmentação MEV, `Holm et al. (2020)` (cujo texto integral foi lido e sintetiza inclusive a superação desse paradigma clássico pelos métodos modernos) deve ser priorizado em relação a este artigo de 2015.
