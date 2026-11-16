# 06 — Prioridades Imediatas para Hoje (16/11/2026) e Plano do Seminário de Amanhã (17/11/2026)

**Disciplina:** Seminários I — PPGCEM / Universidade Federal do Cariri (UFCA)  
**Docentes da disciplina:** Profas. Laédna Neiva e Isabel Brasileiro Rodrigues (`Seminarios-I-Programa.pdf`)  
**Orientador:** Prof. Dr. Job Saraiva Furtado Neto | **Discente:** Emerson de Sousa Gomes  
**Data atual:** 16/11/2026 | **Data do seminário:** **17/11/2026**  
**Posição científica:** Pesquisa em **fase investigativa** (viabilidade de ferramenta computacional para caracterização de grafeno e derivados via DRX, MEV, AFM, PDI e ML/VC quando justificáveis) — **software NÃO desenvolvido e NÃO validado**.

---

> [!CAUTION]
> ### DIVERGÊNCIA CRÍTICA NO TEMPO DE APRESENTAÇÃO (`Seminarios-I-Programa.pdf`, p. 5)
> - **Regra oficial do programa:** *"A disciplina será conduzida na forma de apresentações individuais com **tempo de duração entre 40 e 45 minutos**."*
> - **Mencionado inicialmente pelo pesquisador:** 60 minutos.
> - **Ação obrigatória para amanhã (17/11):** estruturar e ensaiar a fala para **40 a 42 minutos** (nunca planejar 60 min de slides!). Os **~15 a 18 minutos complementares** fecham a janela típica de 1 hora justamente para a **arguição e perguntas** das professoras e da banca. Estourar 45 minutos compromete a arguição e penaliza o critério *"Capacidade de comunicação e/ou argumentativa"* (2,5 pts).

---

## 1. Infraestrutura Mínima Imediata para Hoje (16/11/2026)

Com menos de 24 horas para o seminário e o arquivo `Pré projeto\projeto-atual.md` atualmente vazio (`0` bytes), o foco absoluto é **executar a Missão 02 (base bibliográfica verificada)** e **montar/ensaiar a apresentação de 40–45 min** com zero tempo perdido em manutenção de infraestrutura.

### 1.1 O que USAR AGORA (Camada 0 Zero-Install + Camada 1 Efêmera)

| Camada | Recurso verificado | Uso imediato entre 16/11 e 17/11 | Por que funciona hoje sem risco |
| :--- | :--- | :--- | :--- |
| **Camada 0 (Ativa)** | Antigravity + `/swarm` + Plugin `science v1.4.0` (`literature_search_openalex`, `literature_search_arxiv`, `literature_search_europepmc`, `pubmed_database`) | Paralelizar a Missão 02 (busca, verificação de DOIs, fichamento, matriz de evidências e revisão crítica). | Já está habilitado em `config.json` e operacional nesta máquina. |
| **Camada 0 (Ativa)** | `C:\Users\emer\.local\bin\uv.exe` (`0.13.7`) + `C:\Users\emer\.local\bin\python3.11.exe` (`3.11.18`) | Rodar scripts das skills (`openalex_cli.py`, `search_arxiv.py`), consultar Crossref/DataCite/Unpaywall via GET read-only, gerar/validar `.bib` e extrair conteúdo XML de `.pptx`. | Independe do stub `python.exe`/`python3.exe` de 0 bytes do WindowsApps. |
| **Camada 0 (Ativa)** | Tool nativa `read_file` | Leitura direta (inclusive visual/OCR em PDFs curtos) de programas e artigos prioritários. | Sem instalação nem dependências externas. |
| **Camada 1 (Efêmera)** | `uv run --with pymupdf4llm` (ou `pymupdf`) | Converter os 5–8 artigos essenciais baixados em PDF para Markdown estruturado preservando seções, páginas e tabelas. | Ambiente isolado temporário em cache do `uv`, sem instalar pacotes globais. |
| **Camada 1 (Efêmera)** | `uv run --with python-pptx` + `matplotlib` *(ou alternativa `npx @marp-team/marp-cli`)* | Gerar/atualizar deck **editável em `.pptx`** (reaproveitando template visual UFCA de `Apresentação de Projeto PPGCEM.pptx` ou `IVEFAC333.pptx`) e gráficos/diagramas técnicos em alta resolução. | `python-pptx` entrega arquivo editável diretamente pelo pesquisador no PowerPoint/Google Slides e evita depender de browser headless ou LaTeX para compilação final. |
| **Camada 1 (Opcional se validada)** | `npx --yes @marp-team/marp-cli` (`node v26.13.0` / `npx 11.20.0`) | Útil se desejar rascunho rápido em Markdown com equações LaTeX (KaTeX/MathJax) em HTML. | **Atenção:** exportação para PDF pelo Marp CLI depende de navegador Chromium/Edge/Chrome instalado localmente (não testado nesta sessão). Se escolher Marp, testar exportação PDF nos primeiros 5 min ou usar `.pptx` como via principal. |

> [!TIP]
> **Decisão opcional de 2 minutos (com aprovação do pesquisador):** criar `C:\Users\emer\.env` pelo protocolo seguro `credentials` apenas com `OPENALEX_API_KEY` gratuita. Isso eleva a cota do OpenAlex de `$0,10/dia` compartilhado por IP (sem chave) para `$1/dia` dedicado e libera `download-pdf` via `content.openalex.org`. Caso não deseje configurar agora, a Passagem 1 já roda com orçamento keyless econômico (`--select`, `--per-page 5-10`) + Crossref + arXiv + Europe PMC + Unpaywall.

### 1.2 O que NÃO Instalar nem Perder Tempo Configurando Hoje

| Ferramenta / Setup | Por que **NÃO** mexer hoje (16/11) | Quando reavaliar |
| :--- | :--- | :--- |
| **Docker + GROBID** | `docker` e `java` estão ausentes no sistema; baixar imagens de gigabytes e configurar serviço consome horas e não agrega valor para ler 5–8 artigos até amanhã. | Pós-seminário (se houver corpus > 50 PDFs na dissertação). |
| **Distribuição LaTeX completa (`TeX Live` / `MiKTeX`)** | Download e instalação de vários GBs com alto risco de falta de pacotes na véspera da banca. | Pós-seminário (para escrita da dissertação/artigos). |
| **Docling pesado** | Puxa dependências pesadas de modelos de layout/PyTorch locais apenas para converter PDFs; `uv run --with pymupdf4llm` + `read_file` resolvem hoje em segundos. | Pós-seminário, se precisar de OCR/tabelas complexas em massa. |
| **Zotero Desktop + Better BibTeX + Zotero MCP** | `zotero` **não está instalado** localmente. Instalar app, criar conta, importar referências, configurar Better BibTeX e depurar um servidor MCP do GitHub (não testado no Windows 10) é armadilha de tempo hoje. Substituir por `.bib` gerado e validado via script `python3.11.exe` + Crossref/OpenAlex. | Pós-seminário (Camada 2 com aprovação). |
| **Quarto / Pandoc / Typst / LibreOffice / Tesseract / Git** | Todos ausentes no `PATH`; nenhum deles é bloqueador para a Missão 02 nem para produzir o seminário de amanhã via `python-pptx` / PowerPoint / HTML. | Pós-seminário (Camada 2 com aprovação). |
| **Correção do stub `python3` no `PATH` para habilitar `run_workflow`** | `/swarm` já funciona nativamente hoje sem precisar alterar Aliases do Windows 10 nem retestar `run_workflow`. | Pós-seminário, para pipelines em lote da dissertação. |

---

## 2. Plano da Apresentação de Amanhã (17/11/2026) vs. Programa Oficial

O roteiro deve responder estritamente aos **6 componentes obrigatórios** (`Seminarios-I-Programa.pdf`, p. 4) e maximizar a pontuação nos **4 critérios de avaliação de 2,5 pts cada** (`Seminarios-I-Programa.pdf`, p. 6).

### 2.1 Estrutura de Slides e Orçamento de Tempo (Alvo: 40–42 min | ~26–28 slides)

| Bloco | Componente Oficial (`Seminarios-I-Programa.pdf`, p. 4) | Slides sugeridos | Tempo alvo | Conteúdo técnico indispensável (com rigor científico) |
| :--- | :--- | :---: | :---: | :--- |
| **Abertura** | Identificação e enquadramento no PPGCEM/UFCA | S1–S2 | 2 min | Título realista (investigação de viabilidade, **não** software pronto); linha de pesquisa; orientador Prof. Dr. Job Saraiva Furtado Neto; síntese da evolução do pré-projeto até o recorte atual em grafeno. |
| **Comp. 1** | **1) Definir o que será desenvolvido e a aplicação principal** | S3–S5 | 5 min | O que é a pesquisa: estudo de **viabilidade científica e computacional** para apoiar a caracterização de grafeno e derivados (grafite, GO, rGO) produzidos por rotas como esfoliação eletroquímica na UFCA. Entrada esperada: dados experimentais de **DRX, MEV e AFM**; saída investigada: métricas morfométricas/espectro-estruturais rastreáveis (PDI clássico primeiro; ML/VC apenas se justificáveis). |
| **Comp. 2** | **2) Apresentar a fundamentação científica e o estado da arte** | S6–S13 | 11 min | **Física do grafeno:** rede hexagonal $sp^2$, monocamada/bicamada/poucas camadas/grafite, defeitos e oxidação (GO/rGO). **Física e limites NÃO intercambiáveis das 3 técnicas:** (i) **DRX** (pico `(002)` em $2\theta \approx 26{,}5^\circ$ Cu $K\alpha$, Bragg/Scherrer, média volumétrica — ausência do pico não prova sozinha monocamada); (ii) **MEV** (morfologia lateral, elétrons secundários, não mede espessura atômica absoluta); (iii) **AFM** (topografia nanométrica, convolução de ponta, hidratação interfacial — Shearer et al., 2016). **Técnicas complementares necessárias:** Raman ($I_D/I_G$, banda $2D$) e TEM/XPS. **Estado da arte:** PDI/CV em materiais 2D e microestruturas (Holm et al., 2020 — DOI verificado `10.1007/s11661-020-06008-4`; DeCost & Holm, 2015; softwares como ImageJ/Fiji, Gwyddion, ferramentas de DRX). |
| **Comp. 3** | **3) Apresentar a justificativa desta oportunidade de pesquisa** | S14–S16 | 5 min | Gargalos reais da análise manual (subjetividade entre operadores, tempo elevado, baixa reprodutibilidade estatística); por que aplicar ML "caixa-preta" sem critério físico falha; **conexão direta com o PPGCEM/UFCA** (`Ciencias dos Materiais - Programa.pdf`, p. 2: relação *processamento–estrutura–propriedades*). Premissa orientadora: *"o software é consequência; o objetivo é melhorar a pesquisa em Materiais"*. |
| **Comp. 4** | **4) Apresentar o planejamento metodológico da pesquisa** | S17–S23 | 11 min | **Desenho em 4 fases investigativas:** Fase 1 (Revisão sistemática/narrativa + matriz grandeza física × técnica); Fase 2 (Aquisição e curadoria de amostras reais de grafeno da UFCA + *datasets* de referência); Fase 3 (Comparação controlada **PDI clássico** — pré-processamento, limiarização, morfologia, ajuste de perfis — **vs. ML/VC** sob particionamento agrupado por amostra/lote para zerar *data leakage*); Fase 4 (Validação contra medições manuais de especialistas e técnicas complementares como Raman/TEM). **Análise crítica transparente do piloto IV EFAC 2026 (`IVEFAC333.pptx`):** explicar o que ensinou (arquitetura de treino PyTorch vs. TensorFlow em `QUAM-AFM Lite`) e assumir seus dois limites metodológicos críticos (**data leakage** na divisão 80/20 por arquivo e **domain shift** entre $\text{C}_6\text{H}_4\text{BrClO}$ simulado em UHV e grafeno eletroquímico real). Cronograma 2026.2–2028.1. |
| **Comp. 5** | **5) Apresentar estimativas de resultados ou impactos esperados** | S24–S26 | 5 min | **Entregas realistas e verificáveis:** (1) Critérios científicos explícitos sobre quais grandezas cada técnica permite estimar com segurança; (2) Fluxos reprodutíveis e interpretáveis (benchmark PDI vs. ML com intervalos de erro e análise de incerteza); (3) Base de dados curada de grafeno/derivados no PPGCEM/UFCA; (4) Código/protótipo aberto **se e somente se** a viabilidade for comprovada na validação experimental. Impactos: redução de viés, reprodutibilidade laboratorial e suporte à síntese eletroquímica na UFCA. |
| **Comp. 6** | **6) Apresentar as principais referências bibliográficas** | S27–S28 | 1–2 min | Referências essenciais verificadas na Missão 02 (com autor, ano, periódico e DOI conferido — corrigindo Holm et al. 2020 e removendo fontes não científicas como apostilas/blogs). |
| **Total** | **Apresentação oral controlada** | **26–28 slides** | **40–42 min** | **Margem de 3–5 min abaixo do limite máximo oficial de 45 min + 15–18 min livres para arguição.** |

### 2.2 Alinhamento Explícito aos 4 Critérios de Avaliação (2,5 pts cada = 10,0 pts)

| Critério Oficial (`Seminarios-I-Programa.pdf`, p. 6) | Peso | Como garantir nota máxima amanhã (17/11/2026) | Armadilha fatal a evitar |
| :--- | :---: | :--- | :--- |
| **1. Grau de entendimento do discente sobre o seu projeto de dissertação** | **2,5 pts** | Explicar com clareza física por que DRX, MEV e AFM não medem a mesma coisa; justificar por que a pesquisa está na etapa investigativa; diagnosticar criticamente os limites do próprio piloto anterior (`IVEFAC333.pptx`). | Tratar DRX/MEV/AFM como sinônimos ou defender o `100%` do piloto `QUAM-AFM Lite` como prova de que o método funciona em grafeno. |
| **2. Clareza dos objetivos** | **2,5 pts** | Enunciar um Objetivo Geral inequívoco (*investigar viabilidade, fundamentos físicos e abordagem computacional para apoio à caracterização de grafeno*) seguido de 4–5 Objetivos Específicos mensuráveis ligados diretamente às fases metodológicas. | Apresentar objetivos de pré-projeto genérico de 2026 ("construir plataforma web para qualquer microestrutura") sem foco em grafeno nem critérios de validação. |
| **3. Capacidade de comunicação e/ou argumentativa** | **2,5 pts** | Respeitar rigorosamente o intervalo **40–45 min** (ensaio cronometrado hoje à noite); usar diagramas limpos, pouco texto por slide e notas orais estruturadas; responder perguntas difíceis na arguição reconhecendo limites e propondo controles experimentais. | Preparar conteúdo para 60 min (ser interrompido antes do método/resultados esperados) ou ler slides densos sem domínio conceitual. |
| **4. Relação da temática da dissertação com o objetivo do programa PPGCEM/UFCA** | **2,5 pts** | Ancorar o discurso na ementa do programa (`Ciencias dos Materiais - Programa.pdf`, p. 2: compreender a relação **processamento → estrutura → propriedades → desempenho** em escala microscópica e macroscópica) e na rota real estudada no laboratório (esfoliação eletroquímica de grafeno na UFCA). | Focar 80% da fala em códigos PyTorch/CNNs fazendo a banca perguntar *"Onde está a Ciência e Engenharia de Materiais nesta dissertação?"*. |

### 2.3 Triagem do Material Histórico: O que Aproveitar vs. O que Descartar/Corrigir

| Origem verificada | O que pode ser aproveitado amanhã | O que **NÃO** pode ir para o seminário sem correção |
| :--- | :--- | :--- |
| `Apresentação de Projeto PPGCEM.pptx` (10 slides + notas) | Identidade visual UFCA/PPGCEM; argumento de motivação (reduzir subjetividade/tempo manual); nota do slide 8 (*"o software é consequência, o objetivo é melhorar a pesquisa"*). | Escopo antigo genérico ("qualquer microestrutura") sem delimitação de grafeno/DRX/MEV/AFM e sem estado investigativo explícito. |
| `Apresentação sem título (1).pptx` (32 slides, 38 mídias) | Apenas eventualmente ilustrações didáticas revisadas (se verificadas visualmente uma a uma). | Slides 21 e 29–32: promessas de *"plataforma web"*, *"pureza automática"*, *"múltiplas CNNs especializadas"*, *"validação prévia"* e *"ativos encontrados por agentes"*. |
| `IVEFAC333.pptx` (15 slides) | Contexto de esfoliação eletroquímica de grafeno na UFCA (S14); explicação didática de AFM e comparação introdutória PyTorch vs. TensorFlow (como **antecedente exploratório**). | Apresentar a acurácia de `100%` (S13) como resultado generalizável (há *data leakage* por arquivo e *domain shift* de $\text{C}_6\text{H}_4\text{BrClO}$ UHV); citar `Data Science Academy` como referência científica; quebra de linha no DOI de Ba Alawi (2025). |
| `Pré projeto\pre-projeto-da-selecao.md` e `projeto-atual.md` | Estrutura clássica de pré-projeto para adaptar tópicos de seleção ao recorte atual; registro de que `projeto-atual.md` está vazio (`0` bytes) exige consolidar o texto atual a partir da Missão 02. | Referências sem DOI/incompletas (ex.: Padilha sem ano na lista final) e foco exclusivo em MEV genérico. |

---

## 3. Cronograma Prático Hora a Hora (16/11 Tarde/Noite → 17/11 Seminário)

| Horário | Bloco de Trabalho | Atores | Entregáveis Concretos e Critério de Parada |
| :--- | :--- | :--- | :--- |
| **16/11 — 12:30–13:00** | **Fechamento Missão 01 & Decisão de Credenciais** | Pesquisador + Coordenador | Ler `README.md` de `preparacao_ambiente/`, decidir se cadastra `OPENALEX_API_KEY` gratuita em `~/.env` (2 min), e autorizar início imediato da **Missão 02** em Camada 0/1 (sem instalar ferramentas pesadas). |
| **16/11 — 13:00–15:30** | **Missão 02 — Passagem 1 (Pesquisa Bibliográfica Essencial)** | `/swarm` (Agentes 1, 4, 2, 3 + `@revisor-critico`) | Verificar 15–25 artigos dos Eixos A–E; gerar `referencias.bib` e `matriz_comparativa.csv` auditados; baixar PDFs Open Access legítimos e extrair texto via `uv run --with pymupdf4llm`; selecionar **5–8 artigos indispensáveis** em `05_ESTUDO_IMEDIATO/`. |
| **16/11 — 15:30–17:30** | **Estudo Dirigido dos 5–8 Artigos + Missão 02 Passagem 2** | Pesquisador (leitura) + `/swarm` em paralelo | **Pesquisador:** estuda os fichamentos prioritários e `conceitos_fundamentais.md` (dominar Bragg/Scherrer em DRX, contraste em MEV, artefatos de ponta/hidratação em AFM, papel do Raman, e lições de Holm 2020 / Shearer 2016). **Agentes:** fecham `04_ESTADO_DA_ARTE/` (softwares existentes, lacunas e oportunidades) com revisão final do `@revisor-critico`. |
| **16/11 — 17:30–19:30** | **Missão 03 — Construção do Deck (26–28 slides) + Notas + Arguição** | Agente 5 (`@agente-comunicacao`) + `@revisor-critico` | Produzir apresentação editável (`python-pptx` + gráficos `matplotlib`, ou Marp HTML/PDF se browser testado), notas detalhadas por slide calibradas para **40–42 min**, e lista de **10–12 perguntas difíceis de arguição** com respostas fundamentadas. `@revisor-critico` audita 100% dos slides contra o protocolo anti-alucinação e contra os 6 componentes / 4 critérios. |
| **16/11 — 19:30–20:30** | **Pausa / Jantar + Inspeção Visual dos Slides** | Pesquisador | Abrir o arquivo gerado no PowerPoint/visualizador local, conferir fórmulas, figuras, contraste e alinhamento visual, e ajustar eventuais quebras de layout. |
| **16/11 — 20:30–22:00** | **Ensaio Geral Cronometrado #1 + Simulação de Arguição** | Pesquisador (com apoio do Agente 5 se necessário) | **Simular apresentação completa em voz alta com cronômetro:** verificar se fecha entre **40 e 42 min** (marcas de passagem: `S5 @ 7 min`, `S13 @ 18 min`, `S16 @ 23 min`, `S23 @ 34 min`, `S28 @ 41 min`). Em seguida, responder em voz alta 15 min de perguntas duras sobre: *não-intercambiabilidade DRX/MEV/AFM, necessidade de Raman, data leakage no piloto IV EFAC, domain shift QUAM-AFM vs. UFCA, por que não há software pronto ainda, e conexão com Ciência dos Materiais*. |
| **16/11 — 22:00–22:45** | **Cortes de Ritmo + Folha de Cola Conceitual + Backup** | Pesquisador | Cortar slides/exemplos que atrasaram o ensaio; imprimir ou salvar folha resumo de 1 página (números-chave, equações de Bragg/Scherrer, DOIs centrais); exportar cópia em **`.pdf` de segurança** ao lado do `.pptx` editável. **Encerrar às 22:45 para descansar.** |
| **17/11 — 07:30–09:00** | **Revisão Matinal Leve + Ensaio de Transições** | Pesquisador | Reler apenas abertura (2 min), bloco de metodologia (11 min), fechamento (5 min) e respostas das 5 perguntas mais prováveis da banca; conferir arquivos em pendrive e nuvem. |
| **17/11 — T-60 min até Seminário** | **Setup na Sala + Apresentação (40–45 min) + Arguição** | Pesquisador | Testar projetor com `.pptx` (ou `.pdf` fallback), ativar modo apresentador com cronômetro visível: manter ritmo entre **40 e 42 min** e abrir espaço firme e seguro para a arguição de ~15 min. |

---

## 4. Separação Explícita: Verificado Empiricamente vs. Incerto

| Item | Status nesta sessão | Base / Motivo |
| :--- | :--- | :--- |
| Duração oficial (`40–45 min`), 6 componentes do roteiro e 4 critérios (`2,5 pts` cada) | **Verificado empiricamente** | Leitura direta de `C:\Users\emer\dissertacao\Disciplinas-Mestrado\Seminarios-I-Programa.pdf` (págs. 4–6). |
| Ementa e relação processamento–estrutura–propriedades no PPGCEM | **Verificado empiricamente** | Leitura direta de `C:\Users\emer\dissertacao\Disciplinas-Mestrado\Ciencias dos Materiais - Programa.pdf` (pág. 2). |
| Estado de `Pré projeto\projeto-atual.md` (`0` bytes) e conteúdo dos 3 `.pptx` antigos e `pre-projeto-da-selecao.md` | **Verificado empiricamente** | Inspecionados via `read_file` e extração Python `zipfile`/`ElementTree`. |
| Disponibilidade imediata de Camada 0 (`uv 0.13.7`, `python3.11.exe`, `node v26.13.0`, `npx 11.20.0`, `/swarm`, plugin `science`) e ausência de `git`, `docker`, `java`, `zotero`, `pandoc`, `quarto`, `marp`, `latex`, `libreoffice`, `tesseract` | **Verificado empiricamente** | Comandos de diagnóstico executados no PowerShell local em 16/11/2026. |
| Presença de PowerPoint / Word / Chrome / Edge instalados fora do `PATH` para abertura visual e exportação PDF via Marp CLI | **Incerto / Não testado** | Não houve varredura de `Program Files` nem teste de exportação PDF via navegador; mitigado priorizando `.pptx` via `python-pptx` e checagem visual direta pelo pesquisador. |
| Horário exato da chamada de amanhã (17/11) dentro da disciplina *Seminários I* | **Incerto / Externo aos arquivos** | `Seminarios-I-Programa.pdf` informa início das apresentações em `15/09/2026` e atendimento segundas/quartas 10h–12h, mas não registra a escala individual nominal de `17/11/2026`. |
| Acesso completo (full-text) a artigos fechados sem Open Access via proxy/CAPES UFCA | **Incerto / Não testado** | A Missão 02 testará na prática quais artigos prioritários possuem PDF OA legítimo (arXiv/Europe PMC/Unpaywall) e quais exigirão download institucional manual pelo pesquisador. |
