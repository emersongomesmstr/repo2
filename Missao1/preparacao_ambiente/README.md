# Consolidação Estratégica — Missão 01 (`preparacao_ambiente/`)

**Projeto:** Viabilidade científica e computacional de ferramenta para caracterização de grafeno e materiais relacionados (DRX, MEV, AFM, PDI e ML/VC)  
**Programa / Disciplina:** PPGCEM/UFCA — *Seminários I* (`17/11/2026`)  
**Orientador:** Prof. Dr. Job Saraiva Furtado Neto | **Discente:** Emerson de Sousa Gomes  
**Data da consolidação:** `16/11/2026`  
**Status real da pesquisa:** **Fase investigativa de fundamentação e viabilidade** — **software NÃO desenvolvido e NÃO validado**.

> [!IMPORTANT]
> **Alerta oficial de Seminários I ([Seminarios-I-Programa.pdf](file:///C:/Users/emer/dissertacao/Disciplinas-Mestrado/Seminarios-I-Programa.pdf)):** a duração oficial da apresentação é de **40 a 45 minutos** (p. 5), e **não 60 minutos** como citado inicialmente. A exposição deve cobrir os **6 componentes obrigatórios** (p. 4) para atender aos **4 critérios de avaliação de 2,5 pontos cada = 10,0 pontos** (p. 6), reservando ~15–18 minutos para a arguição.

---

## 1. Índice Navegável dos Entregáveis Auditados (`01` a `07`)

Todos os sete relatórios abaixo passaram por auditoria cruzada independente do Revisor Crítico (`@revisor-critico`), incluindo conferência empírica de ambiente, contagem de arquivos e validação de DOIs/arXiv IDs nas APIs oficiais Crossref, DataCite e arXiv:

| Arquivo | Escopo Principal | Autor | Status de Auditoria |
| :--- | :--- | :--- | :---: |
| [`01_inventario.md`](./01_inventario.md) | Diagnóstico de hardware/SO/PATH, inventário Antigravity, auditoria completa dos PDFs/MDs/3 PPTXs e linha do tempo do projeto | `@agente-documentos` | **APROVADO** |
| [`02_skills_plugins_mcp.md`](./02_skills_plugins_mcp.md) | Levantamento de 8 categorias (skills, Marketplace, 11 MCPs GitHub + nativo, bases/APIs, PDF/PPTX/RAG, BibTeX, slides, orquestração) com 12 critérios e rankings | `@agente-ferramentas` | **APROVADO** |
| [`03_instalacao.md`](./03_instalacao.md) | Plano em 3 camadas (Camada 0 ativa, Camada 1 efêmera, Camada 2 sujeita à aprovação), protocolo `~/.env` e snippet ilustrativo `mcp_config.json` | `@agente-ferramentas` | **APROVADO** |
| [`04_arquitetura_agentes.md`](./04_arquitetura_agentes.md) | Mapeamento dos 6 papéis em `/swarm`, análise de `run_workflow` vs. `invoke_subagent`, diagrama Mermaid, contratos I/O e trava anti-alucinação | `@agente-arquitetura` | **APROVADO** |
| [`05_plano_bibliografico.md`](./05_plano_bibliografico.md) | Auditoria de referências históricas, busca verificada nos Eixos A–E (43 DOIs + 9 arXiv IDs checados), matriz de não-intercambiabilidade DRX/MEV/AFM e fluxo BibTeX | `@agente-bibliografia` | **APROVADO** |
| [`06_prioridades_hoje.md`](./06_prioridades_hoje.md) | Infraestrutura mínima imediata para 16–17/11, roteiro 40–42 min contra os 6 componentes e 4 critérios, triagem do histórico e cronograma hora a hora | `@agente-arquitetura` | **APROVADO** |
| [`07_limitacoes.md`](./07_limitacoes.md) | Limitações reais do Windows 10/APIs, 5 riscos metodológicos graves para blindagem na arguição e tabela verificado vs. incerto | `@revisor-critico` | **APROVADO** |

---

## 2. Resumo do Diagnóstico Técnico e Documental

### 2.1 Ambiente Real Verificado (Windows 10)
- **Sistema e Hardware:** Windows 10 Pro (`10.0.19045.0`), PowerShell `5.1.19041.6456`, CPU AMD Ryzen 3 7320U (4 núcleos / 8 threads), RAM visível de **`3.396.860 KB` (~3,24 GiB)** e GPU integrada AMD Radeon 610M (**sem CUDA**).
- **Runtimes funcionais:** `uv 0.13.7` (`C:\Users\emer\.local\bin\uv.exe`), `python3.11.exe` (**Python 3.11.18** com `sqlite3 3.53.1` + `ENABLE_FTS5`), `node v26.13.0`, `npm/npx 11.20.0`, `agy.exe` e Google Chrome (`C:\Program Files\Google\Chrome\Application\chrome.exe`).
- **Armadilha crítica de `PATH`:** `python.exe` e `python3.exe` no `PATH` apontam para **stubs de 0 bytes** em `C:\Users\emer\AppData\Local\Microsoft\WindowsApps\` (falham com código `9009`). Isso bloqueia ferramentas que chamam `python3` diretamente (como `run_workflow` sem ajuste prévio) e exige o uso de `uv run` ou do caminho absoluto de `python3.11.exe`.
- **Binários ausentes no `PATH`:** `git`, `gh`, `pandoc`, `quarto`, `marp`, `typst`, `pdflatex`, `xelatex`, `lualatex`, `tesseract`, `soffice`, `libreoffice`, `zotero`, `docker`, `java`, `pip`, `pipx`, `conda`, `choco`, `py`, `rg`, `grep`.
- **Antigravity e Credenciais:** `config.json` ativa os plugins `science v1.4.0` (**48 skills** + MCP `biomolecular_structure_viewer_mcp`), `google-antigravity-sdk v0.0.9` e `swarm`; `~/.gemini/config/skills/` possui 2 skills (`optimize-tokens`, `plan-token-optimization`); há 14 skills built-in. `mcp_config.json` global está vazio (`0` B) e `~/.env` está sem chaves (`0` B), restringindo OpenAlex a `$0,10/dia` por IP compartilhado e causando HTTP `429` imediato nas buscas anônimas do Semantic Scholar e HTTP `422` no Unpaywall sem `email`.

### 2.2 Diagnóstico Científico e Histórico do Projeto
- **Lacuna de documentação atual:** `Pré projeto\projeto-atual.md` está **vazio (`0` bytes)**, e `Artigos\` contém uma cópia espelhada idêntica (SHA-256) de `Apresentacoes_passadas\`, `Disciplinas-Mestrado\` e `Pré projeto\`.
- **5 Riscos Científicos Críticos Identificados para a Arguição de Amanhã (`17/11/2026`):**
  1. ***Data leakage* no piloto `IVEFAC333.pptx`:** o piloto em `QUAM-AFM Lite` (576 treino / 144 validação, ResNet-18) usou divisão aleatória `80/20` *por arquivo*, obtendo `100%` no PyTorch ao misturar quadros da mesma molécula/pilha simulada. Na dissertação, é obrigatório usar divisão agrupada por amostra física/lote (*GroupKFold*).
  2. ***Domain shift* extremo:** simulações em altura constante em UHV de isômeros orgânicos $\text{C}_6\text{H}_4\text{BrClO}$ não se transferem para grafeno real esfoliado eletroquimicamente na UFCA. O piloto é apenas estudo exploratório de pipeline PyTorch vs. TensorFlow.
  3. **Não-intercambiabilidade física de DRX, MEV e AFM:** DRX mede média volumétrica cristalográfica ($d_{002}, L_c$ — monocamada isolada não gera pico `(002)`); MEV mede morfologia lateral e contraste SE dependente de kV/substrato/função trabalho; AFM mede topografia local sujeita a convolução de ponta e superestimação da altura aparente da monocamada (`0,4–1,7 nm` vs. `0,335 nm` teórico por camada de adsorvato/hidratação, Shearer et al., 2016). A quantificação confiável de camadas e defeitos depende de técnicas complementares como **Espectroscopia Raman** (banda $2D$, razão $I_D/I_G$), **TEM** e **XPS**.
  4. **Sobrepromessa de engenharia:** rascunhos passados (`Apresentação sem título (1).pptx`) prometiam "plataforma web", "múltiplas CNNs especializadas", estimativa de "pureza" por imagem e alegavam "validação prévia". O discurso oficial deve defender **pesquisa investigativa de viabilidade** (PDI clássico transparente primeiro; ML/VC somente onde fisicamente justificável e validado).
  5. **Correção de duração e DOIs:** alinhar tempo a **40–45 min** (alvo de fala **40–42 min**) e corrigir referências — especialmente **Holm et al. (2020)** cujo DOI real é **`10.1007/s11661-020-06008-4`** (*Metall. Mater. Trans. A*), **nunca** `10.1007/s11837-020-04347-6` (artigo distinto sobre $\text{TiO}_2$ no *JOM*), além de incluir o DOI de Shearer et al. (2016) (`10.1088/0957-4484/27/12/125704`), corrigir o typo do DOI de Ba Alawi (2025) e remover fontes não científicas (`Data Science Academy`).

---

## 3. Ranking Top das Ferramentas (Consolidado da Seção 9 de `02_skills_plugins_mcp.md`)

| Posição | Ferramenta / Recurso | Camada | Verificação Local | Papel Estratégico |
| :---: | :--- | :---: | :---: | :--- |
| **1º** | **Plugin `science` (`literature_search_openalex` + `literature_search_arxiv`)** | **0** | `--help` + consultas reais OK | Busca bibliográfica verificada em Materiais, Física e CV/ML |
| **2º** | **OpenAlex + Crossref + DataCite + Unpaywall (APIs)** | **0** | Crossref/DataCite/OpenAlex testados | Validação real de DOIs e geração determinística de `.bib` |
| **3º** | **`python3.11.exe` (`3.11.18`) + `SQLite FTS5` (`3.53.1`)** | **0** | Testado localmente | Scripts XML/PPTX, requisições API e busca lexical BM25 em disco |
| **4º** | **`uv` / `uvx` (`0.13.7`) + `PyMuPDF`/`pymupdf4llm` (`2.1`)** | **1** | Testado efêmero (829 ms) | Extração rápida de PDFs científicos para Markdown sem GPU |
| **5º** | **`python-pptx` (`1.0.2`) + `matplotlib`** | **1** | Testado efêmero (233 ms) | Geração de `.pptx` 100% editável com figuras DPI e notas orais |
| **6º** | **`/swarm` (`native_swarm`) + `.agents/skills/`** | **0** | Em produção nesta missão | Orquestração paralela com revisão crítica independente |
| **7º** | **`Marp` (`@marp-team/marp-cli` via `npx` + Chrome) / `Reveal.js`** | **1** | `npx` e `chrome.exe` confirmados | Opção para slides HTML/PDF com KaTeX nativo (`--pptx-editable` bloqueado sem LibreOffice) |
| **8º** | **Periódicos CAPES (CAFe/UFCA no navegador)** | **Manual** | Consultado | Acesso legal gratuito a periódicos fechados (*Carbon*, *ACS*, *IOP*) |
| **9º** | **`pdfplumber` & `MarkItDown`** | **1** | Consultados | Extração de tabelas PDF e conversão multi-formato (MIT) |
| **10º** | **Semantic Scholar API + `zongmin-yu/semantic-scholar-fastmcp-mcp-server`** | **0 / 2** | API testada (`429` sem chave) | Grafos de citação e recomendações (após obter chave gratuita) |
| **11º–14º** | **`Zotero 7 + Better BibTeX`**, **`Docling`/`Marker`/`LanceDB`**, **`Quarto`/`Typst`**, **`Context7`/`Parallel`/`Tavily`** | **2** | Consultados | Infraestrutura pós-Seminário I (sujeita à aprovação explícita) |

---

## 4. Infraestrutura Mínima Recomendada (Hoje vs. Pós-Aprovação)

### 4.1 Hoje e Amanhã (`16–17/11/2026` — Camadas 0 e 1, Zero Mudanças Globais)
- **Usar imediatamente:** `/swarm` + `science` (`openalex_cli.py`, `search_arxiv.py`, `europepmc_api.py`) + `python3.11.exe` (Crossref/DataCite/`SQLite FTS5`) + `uv run --with pymupdf4llm` (leitura dos PDFs essenciais) + `uv run --with python-pptx` (ou `Marp`/Chrome para PDF se validado).
- **NÃO instalar hoje:** Docker Desktop, GROBID, Java JDK, TeX Live / MiKTeX completo, `docling-mcp[local]` / `Marker` (inviáveis hoje com ~3,24 GiB RAM sem GPU e pouco tempo), Zotero Desktop + Zotero MCPs (sem Zotero instalado), Quarto/Pandoc/Typst/LibreOffice/Tesseract.
- **NÃO usar:** scraping do Google Scholar (CAPTCHA/ToS), fallback do Sci-Hub no `openags/paper-search-mcp`, ou `run_workflow` antes de resolver o stub `WindowsApps\python3.exe`.

### 4.2 Ações de Camada 2 Sujeitas à Aprovação do Pesquisador
1. **Imediata recomendada (2 min, antes da Missão 02):** preencher `C:\Users\emer\.env` via protocolo seguro `credentials` (sem exibir chaves no chat) com `USER_EMAIL` e `OPENALEX_API_KEY` gratuita (eleva OpenAlex de `$0,10/dia` para `$1,00/dia`, libera `download-pdf` em `content.openalex.org` e habilita Unpaywall/Crossref Polite Pool) + opcional `SEMANTIC_SCHOLAR_API_KEY` gratuita.
2. **Pós-Seminário I (após `17/11/2026`):** instalar `Zotero 7 + Better BibTeX` (`DigitalScholar.Zotero`), `Git` (`Git.Git`), avaliar `Quarto` ou `Typst (Touying)`, plugins Marketplace (`Context7`, `Parallel`/`Tavily`) e, se desejar usar `run_workflow` em lote, desativar o *App Execution Alias* de `python.exe`/`python3.exe` no Windows 10.

---

## 5. Plano Imediato para a Missão 02 e Seminário (`16–17/11/2026`)

Conforme [`Artigos/PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md), [`04_arquitetura_agentes.md`](./04_arquitetura_agentes.md), [`05_plano_bibliografico.md`](./05_plano_bibliografico.md) e [`06_prioridades_hoje.md`](./06_prioridades_hoje.md):

1. **Missão 02 — Passagem 1 (Pesquisa Essencial em `/swarm`):**
   - `@agente-bibliografia` executa consultas e baixa PDFs legais em acesso aberto (`ARTIGOS_PDF/`) para os **15–25 trabalhos prioritários** dos 5 Eixos (e sinaliza artigos fechados para download manual via CAPES/CAFe), gerando `01_ESTRATEGIA/`, `02_REFERENCIAS/` (`referencias.bib` validado no Crossref/DataCite e `matriz_comparativa.csv`).
   - `@agente-documentos` extrai texto integral dos PDFs via `uv run --with pymupdf4llm` (mantendo propriedade exclusiva de extratos).
   - `@agente-fisica` e `@agente-metodologia` produzem os fichamentos críticos (`03_FICHAMENTOS/`) e o pacote de estudo imediato com **5 a 8 artigos indispensáveis** (`05_ESTUDO_IMEDIATO/`: destaque para Shearer 2016, Nemes-Incze 2008, Holm 2020, Backes 2020, Parvez 2014, Zhou 2016, Ferrari 2006/2013, Wang 2026 `arXiv:2608.22400v2`).
   - `@revisor-critico` audita todos os DOIs, leitura integral vs. resumo e rigor físico antes de liberar para estudo.
2. **Missão 02 — Passagem 2 (Aprofundamento em Paralelo):** enquanto o pesquisador estuda os 5–8 artigos essenciais, o `/swarm` consolida `04_ESTADO_DA_ARTE/` (softwares existentes, limitações científicas e oportunidades reais) e `PESQUISA_BIBLIOGRAFICA/README.md`.
3. **Missão 03 (Pós-Missão 02 — Produção do Seminário e Ensaio de Arguição):** com a base bibliográfica aprovada, `@agente-comunicacao` gera deck editável em `.pptx` (26–28 slides, ritmo calibrado para **40–42 min** cobrindo os 6 componentes e 4 critérios de 2,5 pts) + notas orais + banco de perguntas difíceis para arguição, seguido de gate final do `@revisor-critico` e ensaio cronometrado na noite de `16/11`.
