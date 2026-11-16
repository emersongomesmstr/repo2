# Base Bibliográfica e Guia de Estudo — Missão 02 (PPGCEM/UFCA)

Portal central da revisão bibliográfica crítica e do guia de preparação científica para a disciplina **Seminários I** (apresentação em **17/11/2026**; preparação em **16/11/2026**), no Programa de Pós-Graduação em Ciência e Engenharia de Materiais (**PPGCEM/UFCA**).

- **Mestrando:** Emerson de Sousa Gomes  
- **Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
- **Estágio do projeto:** fase investigativa inicial (estruturação do referencial teórico, diagnóstico crítico de viabilidade experimental/computacional e desenho metodológico)  
- **Escopo deste diretório:** base bibliográfica auditada, fichamentos técnicos e plano de estudo imediato dos artigos científicos (este repositório **não** contém slides nem roteiro de apresentação oral).

---

## 1. Pergunta Central e Objetivo da Revisão

> **Pergunta central:** Em que medida técnicas de caracterização frequentemente associadas à pesquisa em grafeno e derivados (**DRX**, **MEV** e **AFM**), combinadas com métodos de **Visão Computacional (VC)** e **Aprendizagem de Máquina (AM/DL)** e ancoradas por técnicas de referência (**Raman**, **TEM/SAED** e **XPS**), permitem inferir de forma confiável estrutura cristalina, defeitos, morfologia, tamanho lateral, espessura e número de camadas — e onde cada abordagem falha ou induz interpretações fisicamente equivocadas?

---

## 2. Sumário Executivo dos Achados Científicos

### 2.1 Não-intercambialidade física entre DRX, MEV e AFM
Uma conclusão central da literatura revisada é que **DRX, MEV e AFM medem grandezas físicas distintas em escalas diferentes** e **não são intercambiáveis** para determinar número de camadas ou confirmar grafeno monocamada isolado:

1. **DRX (Difração de Raios X):** sonda o **volume médio do pó/amostra** por coerência estrutural de longo alcance (lei de Bragg para espaçamento interplanar $d_{002}$ e equação de Scherrer com correção instrumental para tamanhos médios de cristalito $L_c$ e $L_a$, conforme `Holzwarth & Gibson, 2011`). Permite distinguir grafite cristalino ($d_{002} \approx 0{,}335\text{ nm}$), óxido de grafite/grafeno expandido e rGO com desordem turboestrática (`Li, Lu & Xia, 2007`; `Stobinski et al., 2014`). **Limite crítico:** a redução ou ausência do pico `(002)` indica perda de empilhamento ordenado ao longo de $c$, sendo condição *necessária, mas insuficiente* para provar monocamada pura — não conta camadas de flocos individuais.
2. **MEV (Microscopia Eletrônica de Varredura):** sonda a **morfologia superficial 2D**, dobras, rugas, contornos e contraste de elétrons secundários (SE) em baixa tensão de aceleração (kV). O contraste por número de camadas depende da interação entre emissão SE, variação da função trabalho ($\Phi$), substrato, detector (*InLens* vs. *Everhart-Thornley*) e carregamento superficial (`Zhou et al., 2016`; `Huang & Gan, 2024`; `Hiura et al., 2010`). O protocolo internacional `NPL/VAMAS (2023)` padroniza a medição de **tamanho lateral** por diâmetros de Feret e área projetada em MEV, mas reforça que MEV isolado não fornece espessura absoluta sem calibração local rigorosa.
3. **AFM (Microscopia de Força Atômica):** mede o **perfil topográfico nanométrico** sobre o substrato, sendo a técnica direta mais utilizada para espessura de degrau, porém sujeita a forte **anomalia de espessura aparente** (`Nemes-Incze et al., 2008`; `Shearer et al., 2016`). Interações tip-amostra (amplitude livre e *setpoint* em modo intermitente/*tapping*, forças capilares, rigidez elástica e filmes de adsorvato/água interfacial) deslocam a espessura medida de uma monocamada de $\sim 0{,}34\text{ nm}$ teórico para faixas típicas de $\sim 0{,}7\text{–}1{,}7\text{ nm}$ (ou mais). Além disso, o raio finito da ponta introduz **convolução lateral**, superestimando dimensões estreitas (`NPL/VAMAS, 2023`).
4. **Técnicas de referência (*ground truth*) e heterogeneidade comercial:** para validar rótulos físicos de número de camadas, defeitos e composição química, a literatura estabelece **Espectroscopia Raman** (razão $I_D/I_G$, posição/largura/forma da banda $2D$; `Ferrari, 2006`; `Ferrari & Basko, 2013`), **TEM/SAED** (contagem em bordas dobradas e padrão de difração) e **XPS** (razão C/O e grupos oxigenados em GO/rGO; `Stobinski et al., 2014`). Paralelamente, estudos de padronização mostram enorme heterogeneidade e baixa fração de monocamadas verdadeiras em amostras produzidas comercialmente e por esfoliação (`Kauling et al., 2018`; `Backes et al., 2020`).

### 2.2 Visão Computacional e Aprendizagem de Máquina na Caracterização
- **Pipeline clássico vs. Deep Learning em microscopia:** segmentação clássica (limiarização de Otsu, transformações morfológicas, *watershed* e descritores de textura/forma em `scikit-image`/Fiji) contrasta com redes profundas como U-Net (segmentação semântica) e Mask R-CNN (instâncias), sendo o maior gargalo atual a **escassez de anotações confiáveis e a padronização dos metadados microscópicos** (`Holm et al., 2020`; `DeCost & Holm, 2015`; `Ronneberger et al., 2015`; `Gercek et al., 2025`).
- **Automação específica em materiais 2D:** pipelines eficazes no estado da arte acoplam visão computacional com **controle de qualidade físico** e calibração controlada em substratos padronizados (ex. $\text{SiO}_2/\text{Si}$), como demonstrado em segmentação automatizada (`Masubuchi et al., 2020`) e filtragem automática de qualidade (`Saito et al., 2019`).
- **ML/DL em DRX e lacuna *sim-to-real*:** redes treinadas majoritariamente em difratogramas sintéticos sofrem degradação severa em amostras experimentais reais devido ao *domain shift* causado por orientação preferencial/textura, alargamento por tamanho/microdeformação, ruído de fundo e coexistência multifásica (`Oviedo et al., 2019`; `Greasley & Hosein, 2023`).

### 2.3 Diagnóstico Crítico e Enquadramento Honesto do Piloto `IVEFAC333.pptx`
- O experimento piloto registrado em [IVEFAC333.pptx](file:///C:/Users/emer/dissertacao/Artigos/Apresentacoes_passadas/IVEFAC333.pptx) comparou classificadores **ResNet-18** (PyTorch vs. TensorFlow) sobre um recorte da base pública **QUAM-AFM Lite** contendo 3 isômeros moleculares de fórmula $\text{C}_6\text{H}_4\text{BrClO}$ (CIDs `16268`, `19859` e `69670`), obtidos de simulações teóricas de AFM de alta resolução — **não** de amostras de grafeno.
- Como os próprios slides reconhecem, a acurácia de **100%** obtida na validação em PyTorch com divisão aleatória **por arquivo** (`576` treino / `144` validação, proporção `80/20`) decorre de **vazamento de dados (*data leakage*)** ao misturar diferentes alturas/imagens da mesma pilha simulada entre treino e validação.
- **Implicação metodológica:** esse piloto serve estritamente como *teste de infraestrutura computacional (pipeline PyTorch/TensorFlow)* e evidencia duas exigências obrigatórias para a dissertação: (i) substituir o *split* aleatório por divisão agrupada por amostra/floco/pilha (`GroupKFold`) e (ii) treinar/validar o sistema em **amostras reais de grafeno/GO/rGO** (como as produzidas por **esfoliação eletroquímica** na UFCA), com rótulos verificados por técnicas de referência (Raman/AFM/TEM).

---

## 3. Resumo da Auditoria Bibliográfica, Preprints e Integridade de DOIs

Os levantamentos registrados em [01_ESTRATEGIA](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/01_ESTRATEGIA/protocolo_busca.md) e consolidados em [biblioteca_completa.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/biblioteca_completa.md) e [referencias.bib](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/referencias.bib) seguem critérios estritos de rastreabilidade:

- **Total ativo no catálogo bibliográfico:** **61 obras ativas** (`59` do catálogo primário verificado + `2` incorporações da Passagem 2: `Martins_2025`, DOI `10.21577/0100-4042.20250243`, e `Uslu_2025`, DOI `10.1039/d5dd00156k`).
- **Composição por status editorial:** **52 trabalhos revisados por pares** (incluindo **6 preprints promovidos** à versão final publicada), **2 normas/relatórios técnicos** (`Despotelis_2023` — NPL/VAMAS; `Iwashita_2004`), **3 conjuntos de dados abertos** e **3 preprints ativos sinalizados explicitamente como não revisados por pares** (`Ba_Alawi_2025_arXiv`, `Gercek_2025_arXiv` e `Cao_2026_arXiv`).
- **Textos completos locais verificados:** **30 arquivos PDF** armazenados em [ARTIGOS_PDF](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/ARTIGOS_PDF) + **2 textos completos abertos auxiliares** (`Carracedo-Cosme 2022` via Europe PMC `PMC9942089` e `Doebelin & Kleeberg 2015` via Europe PMC `PMC4603273`, lidos pelos agentes durante a pesquisa), somando **32 textos integrais consultados**.
- **Descartes e correções críticas de integridade:**
  1. **Preprint oficialmente retirado (*withdrawn*) — excluído da bibliografia ativa:** `Wang et al. (2026)` (`arXiv:2608.22400v2`) apresentou pedido formal de retirada pelos autores no registro do arXiv e foi **descartado**; sua função no tema de ML em DRX é coberta pelos artigos revisados por pares `Oviedo et al. (2019)` (`10.1038/s41524-019-0196-x`) e `Greasley & Hosein (2023)` (`10.1007/s10853-023-08343-4`).
  2. **Fonte não científica descartada:** `Data Science Academy (2022)`, citada em apresentação preliminar antiga, foi descartada como referência bibliográfica principal da dissertação.
  3. **Correção de DOI corrompido:** para `Holm et al. (2020)` (*Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis*), um identificador incorreto (`10.1007/s11837-020-04347-6`) detectado em registros preliminares foi substituído exclusivamente pelo DOI real verificado **`10.1007/s11661-020-06008-4`** (*Metallurgical and Materials Transactions A*).
- **Rigor entre texto completo e resumo/metadados:** nos guias e fichamentos da pasta `05_ESTUDO_IMEDIATO/`, artigos abertos lidos na íntegra são identificados como `Texto completo lido` (com citação de seções e figuras reais), enquanto artigos de acesso fechado de editora (`Shearer et al., 2016`; `Li, Lu & Xia, 2007`; `Holzwarth & Gibson, 2011`; `Huang & Gan, 2024`; `Kauling et al., 2018`) são explicitamente marcados como `Resumo e metadados verificados`, sem extrapolação de páginas ou figuras não lidas.

---

## 4. Estrutura de Pastas e Mapa de Arquivos

### `01_ESTRATEGIA/` — Protocolo e critérios de busca
- [protocolo_busca.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/01_ESTRATEGIA/protocolo_busca.md) — Desenho da revisão narrativa crítica estruturada, fontes consultadas (OpenAlex, arXiv, Europe PMC, Crossref/DataCite) e governança de verificação.
- [consultas_utilizadas.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/01_ESTRATEGIA/consultas_utilizadas.md) — Registro exato das strings de busca (`Q-OA-01` a `Q-OA-22`, `Q-ARX-01` a `Q-ARX-04`, `Q-EPMC-01` a `Q-EPMC-03`) e triagem.
- [criterios_selecao.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/01_ESTRATEGIA/criterios_selecao.md) — Critérios de inclusão/exclusão, política para preprints, promoções e justificativa dos descartes.

### `02_REFERENCIAS/` — Base bibliográfica consolidada
- [biblioteca_completa.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/biblioteca_completa.md) — Catálogo anotado completo das 61 referências ativas, status editorial, DOIs verificados e registro de auditoria.
- [referencias.bib](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/referencias.bib) — Arquivo BibTeX padronizado pronto para uso em LaTeX/gerenciadores de referência.
- [matriz_comparativa.csv](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/02_REFERENCIAS/matriz_comparativa.csv) — 45 obras × 10 colunas da Seção 9 (validado).

### `03_FICHAMENTOS/` — Fichamentos temáticos por domínio
- **Grafeno e derivados (`grafeno/`):**
  - [01_novoselov_2004_science_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/01_novoselov_2004_science_graphene.md)
  - [02_geim_novoselov_2007_nature_materials_rise_of_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/02_geim_novoselov_2007_nature_materials_rise_of_graphene.md)
  - [03_castro_neto_2009_rmp_electronic_properties_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/03_castro_neto_2009_rmp_electronic_properties_graphene.md)
  - [04_ferrari_2006_prl_raman_spectrum_graphene_layers.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/04_ferrari_2006_prl_raman_spectrum_graphene_layers.md)
  - [05_kauling_2018_adma_worldwide_graphene_flake_production.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/05_kauling_2018_adma_worldwide_graphene_flake_production.md)
  - [06_parvez_2014_jacs_electrochemical_exfoliation_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/grafeno/06_parvez_2014_jacs_electrochemical_exfoliation_graphene.md)
- **Difração de Raios X (`DRX/`):**
  - [01_li_lu_xia_2007_carbon_xrd_graphite_turbostratic.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/DRX/01_li_lu_xia_2007_carbon_xrd_graphite_turbostratic.md)
  - [02_holzwarth_gibson_2011_nat_nanotechnol_scherrer_equation.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/DRX/02_holzwarth_gibson_2011_nat_nanotechnol_scherrer_equation.md)
  - [03_stobinski_2014_jesrp_go_rgo_xrd_tem_spectroscopy.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/DRX/03_stobinski_2014_jesrp_go_rgo_xrd_tem_spectroscopy.md)
  - [04_toby_vondreele_2013_gsas2_doebelin_2015_profex.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/DRX/04_toby_vondreele_2013_gsas2_doebelin_2015_profex.md)
  - [05_oviedo_2019_npj_lee_2020_nat_commun_deep_learning_xrd.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/DRX/05_oviedo_2019_npj_lee_2020_nat_commun_deep_learning_xrd.md)
- **Microscopia Eletrônica de Varredura (`MEV/`):**
  - [01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/01_huang_gan_2024_micron_review_sem_imaging_graphene_layers.md)
  - [02_hiura_2010_apex_sem_number_of_graphene_layers.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/02_hiura_2010_apex_sem_number_of_graphene_layers.md)
  - [03_zhou_2016_scirep_quantitative_se_imaging_work_function_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/03_zhou_2016_scirep_quantitative_se_imaging_work_function_graphene.md)
  - [04_decost_holm_2015_commatsci_computer_vision_microstructures.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/04_decost_holm_2015_commatsci_computer_vision_microstructures.md)
  - [05_holm_2020_mmta_overview_cv_ml_microstructural_characterization.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/05_holm_2020_mmta_overview_cv_ml_microstructural_characterization.md)
  - [06_gercek_2025_data_efficient_unet_sem_botifoll_2022.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/06_gercek_2025_data_efficient_unet_sem_botifoll_2022.md)
  - [07_vamas_2023_nanoexpress_2025_sem_lateral_size_graphene.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/MEV/07_vamas_2023_nanoexpress_2025_sem_lateral_size_graphene.md)
- **Computação científica, segmentação e classificação (`computacao/`):**
  - [01_otsu_1979_vanderwalt_2014_skimage_schindelin_2012_fiji.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/computacao/01_otsu_1979_vanderwalt_2014_skimage_schindelin_2012_fiji.md)
  - [02_ronneberger_2015_unet_he_2016_resnet.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/computacao/02_ronneberger_2015_unet_he_2016_resnet.md)
- **Microscopia de Força Atômica ([AFM/](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/03_FICHAMENTOS/AFM)):** 6 fichamentos — Binnig 1986, Nemes-Incze 2008, Shearer 2016, Villarrubia 1997 (+ Obraztsova 2008), Yao 2017 (+ Gwyddion, VAMAS), Carracedo-Cosme 2022 / Harris 2025 (crítica ao piloto `IVEFAC333`).

### `04_ESTADO_DA_ARTE/` — Síntese crítica comparativa
- [revisao_critica.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/04_ESTADO_DA_ARTE/revisao_critica.md) (10 perguntas da Seção 10) · [softwares_existentes.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/04_ESTADO_DA_ARTE/softwares_existentes.md) · [oportunidades_pesquisa.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/04_ESTADO_DA_ARTE/oportunidades_pesquisa.md) · [limitacoes_cientificas.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/04_ESTADO_DA_ARTE/limitacoes_cientificas.md)

### `05_ESTUDO_IMEDIATO/` — Preparação focada para hoje (16/11/2026)
- [artigos_essenciais.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/artigos_essenciais.md) — Plano de leitura em **7 blocos indispensáveis** com os 6 tópicos obrigatórios por bloco (por que estudar, seções/foco conceitual, conceitos físicos, resultado relevante, perguntas de banca e tempo aproximado).
- [fichamentos_prioritarios.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/fichamentos_prioritarios.md) — Síntese científica detalhada dos 7 conjuntos essenciais, distinguindo explicitamente fontes com `Texto completo lido` daquelas analisadas por `Resumo e metadados verificados`.
- [conceitos_fundamentais.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/conceitos_fundamentais.md) — Glossário técnico rigoroso cobrindo Física do Grafeno/GO/rGO, DRX, MEV, AFM, técnicas complementares (Raman/TEM/XPS/OM) e Computação Científica/ML.
- [questoes_para_estudar.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/questoes_para_estudar.md) — Banco de perguntas difíceis esperadas da banca PPGCEM/UFCA com respostas diretas, fundamentadas e honestas.

### `ARTIGOS_PDF/` — Acervo local de textos integrais em PDF
- Diretório [ARTIGOS_PDF](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/ARTIGOS_PDF) contendo **30 PDFs científicos** (inclui `Szymanski 2021`) baixados e verificados localmente para leitura direta offline (`Nemes-Incze 2008`, `Holm 2020`, `Backes 2020`, `NPL/VAMAS 2023`, `Zhou 2016`, `Masubuchi 2020`, `Saito 2019`, `Oviedo 2019`, `Greasley & Hosein 2023`, `Ferrari & Basko 2013`, `Novoselov 2004`, `Geim & Novoselov 2007`, `Castro Neto 2009`, `Ferrari 2006`, `Ronneberger 2015`, `Van der Walt 2014`, entre outros).

---

## 5. Roteiro Sugerido para Estudar Hoje (16/11/2026 → 17/11/2026)

Para maximizar o domínio conceitual antes da apresentação de amanhã, recomenda-se seguir esta ordem dentro de `05_ESTUDO_IMEDIATO/`:

1. **Etapa 1 — Visão de conjunto e priorização (~20 min):** leia [artigos_essenciais.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/artigos_essenciais.md) para enxergar o mapa dos **7 blocos prioritários**, entender o que cada um resolve na sua pesquisa e anotar as perguntas da banca associadas a cada estudo.
2. **Etapa 2 — Fixação dos resultados e limites reais (~90–120 min):** estude [fichamentos_prioritarios.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/fichamentos_prioritarios.md) lado a lado com os PDFs de [ARTIGOS_PDF](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/ARTIGOS_PDF) quando quiser inspecionar gráficos/figuras originais (priorize os blocos 1, 3, 4 e 5 caso o tempo aperte).
3. **Etapa 3 — Nivelamento conceitual e rigor físico-computacional (~45 min):** revise [conceitos_fundamentais.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/conceitos_fundamentais.md), garantindo fluência imediata em equação de Bragg/Scherrer, desordem turboestrática, contraste SE em kV e função trabalho, anomalia de espessura em AFM, razão $I_D/I_G$ e banda $2D$ em Raman, métricas IoU/Dice, *data leakage*, `GroupKFold` e *sim-to-real gap*.
4. **Etapa 4 — Treino de arguição com a banca (~30–45 min):** percorra todas as perguntas e respostas em [questoes_para_estudar.md](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/05_ESTUDO_IMEDIATO/questoes_para_estudar.md), praticando respostas concisas e transparentes — especialmente sobre por que DRX/MEV/AFM não são intercambiáveis, por que o piloto `IVEFAC333.pptx` em `QUAM-AFM Lite` foi apenas teste computacional e por que o projeto está em fase investigativa exigindo validação com Raman/TEM em amostras locais de esfoliação eletroquímica.


---

## Parecer Final de Controle de Qualidade (Seção 14)

**Auditoria executada em 16/11/2026 (script automatizado + revisão do coordenador):**

| Item verificado | Resultado |
| :--- | :--- |
| Estrutura completa da Seção 12 (UTF-8, sem arquivos vazios) | ✅ Aprovado |
| 31 fichamentos com os 10 blocos da Seção 8 e declaração de nível de leitura | ✅ Aprovado |
| `referencias.bib` — 61 entradas, 0 chaves duplicadas, chaves balanceadas | ✅ Aprovado |
| `matriz_comparativa.csv` — 45 linhas × 10 colunas exatas | ✅ Aprovado |
| DOI errado de Holm et al. 2020 (`10.1007/s11837-020-04347-6`) | ✅ Aparece apenas em notas explícitas de correção |
| `arXiv:2608.22400v2` (retirado pelos autores) | ✅ Ausente de `.bib` e `.csv`; citado só como descarte |
| Preprints → versão publicada (Leger, Qi, Pan/Wang, Harris, Greasley, MaskTerial) | ✅ Versão publicada priorizada |
| Preprints sem publicação confirmada (Ba Alawi 2025, Gerçek 2025, Cao 2026) | ✅ Sinalizados explicitamente |
| 30 PDFs idênticos em `ARTIGOS_PDF/` e `SALVE_AQUI_OS_ARTIGOS_QUE_ACHAR/` (> 10 KB, `%PDF`) | ✅ Aprovado |
| Links `file:///` do README | ✅ 100% válidos |
| Nenhum slide, roteiro oral ou código do software; arquivos originais intactos | ✅ Aprovado |

**Afirmações que permanecem pendentes:**
- Artigos de acesso fechado (Shearer 2016, Li 2007, Iwashita 2004, Holzwarth & Gibson 2011, Stobiński 2014, Huang & Gan 2024, Kauling 2018, Parvez 2014, Dreyer 2010, Abdelkader 2015, Yao 2017, Otsu 1979) foram analisados **apenas por resumo/metadados** — devem ser lidos na íntegra via Portal CAPES/UFCA antes de citar detalhes internos na dissertação.
- Toda viabilidade de ferramenta sobre grafeno da UFCA é **hipótese de pesquisa**: o software não foi desenvolvido nem validado, e qualquer modelo exigirá dados experimentais próprios com referência Raman/TEM e validação agrupada por amostra.

**Veredito:** base bibliográfica **APROVADA** para estudo imediato e construção posterior do seminário.
