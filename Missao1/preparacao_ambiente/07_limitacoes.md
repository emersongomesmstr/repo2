# 07 — Limitações, Riscos Metodológicos e Escopo Verificado (Missão 01)

**Projeto:** Viabilidade de ferramenta computacional para caracterização de grafeno e materiais relacionados (DRX, MEV, AFM, PDI e ML/VC)  
**Contexto:** PPGCEM/UFCA — Disciplina *Seminários I* (Apresentação: 17/11/2026 | Data da auditoria: 16/11/2026)  
**Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
**Status do software:** **NÃO desenvolvido e NÃO validado** (pesquisa em fase investigativa)

---

## 1. Limitações Técnicas Reais do Ambiente

As limitações abaixo foram constatadas diretamente no sistema local em 16/11/2026 e condicionam tanto a execução da Missão 02 quanto a preparação imediata para o seminário de amanhã:

### 1.1 Sistema Operacional, Shell e Armadilha do `python.exe` (WindowsApps)
- **Sistema:** Microsoft Windows 10 Pro (`10.0.19045`, 64 bits) com Windows PowerShell `5.1.19041.6456`.
- **Conflito crítico no `PATH` (`python` / `python3`):** os comandos `python` e `python3` resolvem para `C:\Users\emer\AppData\Local\Microsoft\WindowsApps\python.exe` e `python3.exe`, que são **stubs de 0 bytes** do *App Execution Alias* da Microsoft Store. A execução de `python --version` falha com **código de saída `9009`** (*"Python não foi encontrado"*).
- **Python funcional isolado:** o interpretador operacional é `C:\Users\emer\.local\bin\python3.11.exe` (**Python 3.11.18**), acompanhado por `C:\Users\emer\.local\bin\uv.exe` (**uv 0.13.7**).
- **Impacto prático:**
  1. Servidores MCP, extensões ou workflows (incluindo scripts que dependam de `python` ou `python3` no `PATH`) falharão caso invoquem `python`/`python3` diretamente sem apontar para `uv run` ou para `C:\Users\emer\.local\bin\python3.11.exe`.
  2. No PowerShell 5.1, scripts Python inline devem usar *here-string* literal (`@' ... '@ | & "C:\Users\emer\.local\bin\python3.11.exe" -`) para evitar criação de arquivos temporários soltos e erros de escape de aspas.

### 1.2 Ausência de Binários Externos e Ferramentas de Publicação/OCR
Verificação direta no `PATH` confirmou **ausência** de:
- **Versionamento e automação:** `git`, `gh`, `docker`.
- **Compilação de apresentações e documentos:** `pandoc`, `quarto`, `marp` (ausente globalmente, requer execução efêmera via `npx`), `pdflatex`, `xelatex`, `lualatex`, `typst`, `soffice` / `libreoffice`.
- **Gestão bibliográfica e extração pesada:** `zotero`, `java` (inviabilizando GROBID local sem JVM/Docker), `tesseract` (inviabilizando OCR local de figuras/slides rasterizados).
- **Empacotadores Python tradicionais:** `pip`, `pipx`, `conda`, `py`, `choco` (todo fluxo Python efêmero deve usar `uv`).

> **Nota sobre conteúdo visual nos arquivos antigos:** `Apresentação sem título (1).pptx` possui 32 slides e **38 arquivos de mídia** (com vários slides — como 1–4, 13, 17 e 22 — contendo apenas imagens e zero texto XML), enquanto `Apresentação de Projeto PPGCEM.pptx` possui 10 slides e **69 arquivos de mídia**. Sem OCR (`tesseract`) ou inspeção visual dedicada das imagens extraídas, a leitura automática por XML/ZIP captura apenas o texto editável e as notas do apresentador.

### 1.3 Ausência de Chaves em `~/.env`, Quotas de APIs Científicas e Bloqueios Anti-Bot
- **`C:\Users\emer\.env` sem credenciais:** inexistente no início da sessão (`Test-Path` = `False`); durante a execução de scripts do ambiente passou a constar apenas como arquivo vazio de **`0` bytes**, mantendo ausentes `OPENALEX_API_KEY`, `USER_EMAIL`, `SEMANTIC_SCHOLAR_API_KEY` e `NCBI_API_KEY`.
- **OpenAlex (modo sem chave):** a consulta `uv run openalex_cli.py rate-limit` confirmou `authenticated: false`, orçamento compartilhado por endereço IP de **`$0,10/dia`** (`1.000` requisições/dia; `$0,0985` / `985` restantes no momento da verificação). Além disso, `download-pdf` autenticado via `content.openalex.org` exige `OPENALEX_API_KEY`.
- **Semantic Scholar (sem chave):** chamada GET direta a `https://api.semanticscholar.org/graph/v1/paper/search?query=graphene+AFM&limit=1` retornou **HTTP 429 (`Too Many Requests`)** imediatamente, demonstrando que o pool anônimo compartilhado é altamente restritivo para buscas em lote na Missão 02 sem `x-api-key`.
- **Google Scholar:** protegido por mecanismos anti-bot/CAPTCHA e restrições nos Termos de Serviço; **não é viável nem permitido** automatizar raspagem ou contornar desafios anti-bot.
- **MCPs externos ausentes:** `C:\Users\emer\.gemini\config\mcp_config.json` está vazio (`0` bytes). Apenas o servidor nativo do plugin `science` (`biomolecular_structure_viewer_mcp`, voltado a visualização biomolecular) está declarado em `C:\Users\emer\.gemini\config\plugins\science\mcp_config.json`.

---

## 2. Riscos Científicos e Metodológicos Graves para a Arguição (17/11/2026)

A auditoria dos documentos históricos (`pre-projeto-da-selecao.md`, `Apresentação de Projeto PPGCEM.pptx`, `Apresentação sem título (1).pptx`, `IVEFAC333.pptx`) e dos programas oficiais (`Seminarios-I-Programa.pdf` e `Ciencias dos Materiais - Programa.pdf`) identificou **cinco vulnerabilidades críticas** que a banca ou as professoras podem atacar amanhã caso não sejam blindadas antecipadamente:

### Risco 1 — *Data Leakage* (Vazamento de Dados) no Piloto QUAM-AFM Lite
- **Evidência nos arquivos:** em `IVEFAC333.pptx` (slides 11 e 13), o piloto classificou 3 moléculas orgânicas (CIDs `16268`, `19859`, `69670`) usando 720 imagens (`576` treino / `144` validação) com **"Divisão 80/20 por arquivo"**, reportando **"100% PyTorch na validação interna (144 imagens)"**.
- **Falha metodológica:** o próprio conjunto QUAM-AFM gera múltiplas imagens altamente correlacionadas da mesma molécula variando levemente a distância ponta–amostra e a amplitude de oscilação. Uma divisão aleatória *por arquivo* distribui quadros vizinhos da mesma simulação entre treino e validação (como o próprio slide 13 reconhece em *"A divisão por arquivo pode misturar imagens da mesma pilha"*). O resultado de `100%` é inflado por vazamento de dados e **não mede capacidade de generalização**.
- **Estratégia de blindagem na arguição:**
  - Apresentar o piloto do IV EFAC 2026 apenas como **prova de conceito didática/computacional de pipeline** (comparação do laço de treino explícito do PyTorch vs. `fit()` do TensorFlow/Keras), nunca como validação científica de caracterização.
  - Declarar explicitamente que, na dissertação com dados reais, o protocolo exigirá **particionamento agrupado por amostra física / síntese / sessão de varredura** (*GroupKFold* ou *Leave-One-Batch-Out*), garantindo independência estatística entre treino, validação e teste cego.

### Risco 2 — Salto de Domínio (*Domain Shift*) Entre UHV Simulado Orgânico e Grafeno Real da UFCA
- **Evidência nos arquivos:** `IVEFAC333.pptx` utiliza simulações em **altura constante** de moléculas orgânicas de bromoclorofenol ($\text{C}_6\text{H}_4\text{BrClO}$) do dataset QUAM-AFM Lite (Carracedo-Cosme et al., 2021/2022), enquanto os slides 4 e 14 vinculam a motivação à caracterização de **"amostras de grafeno obtidos por esfoliação eletroquímica"** na UFCA.
- **Falha metodológica:** há um salto de domínio extremo entre:
  1. Imagens sintéticas idealizadas de moléculas pequenas isoladas em ultra-alto vácuo (UHV) com simulação de ponta funcionalizada; e
  2. Folhas e multicamadas reais de grafeno produzidas por esfoliação eletroquímica em condições ambientes, sujeitas a polidispersidade de tamanho lateral, empilhamento heterogêneo, rugas/dobras, resíduos de eletrólito/intercalantes, defeitos oxidativos, ruído instrumental, deriva térmica e convolução de ponta de AFM.
- **Estratégia de blindagem na arguição:** explicitar que modelos treinados em simulações orgânicas UHV **não são transferíveis diretamente** para grafeno eletroquímico; a transição exige dados experimentais reais (ou simulação fisicamente calibrada para o domínio de grafeno/grafite) acompanhados de validação experimental pareada.

### Risco 3 — Não-Intercambiabilidade Física de DRX, MEV e AFM e Dependência de Técnicas Complementares
- **Evidência nos arquivos:** o escopo atual investiga o uso de DRX, MEV e AFM, e rascunhos passados (`Apresentação sem título (1).pptx`, slides 29–31) chegaram a sugerir perguntas como *"Quantas camadas?"* e *"Temos como estimar a pureza?"* com classificadores e regressões diretamente sobre difratogramas ou micrografias.
- **Limites físicos irredutíveis que não podem ser violados na arguição:**

| Técnica | O que mede fisicamente de modo direto | O que **NÃO** pode provar sozinha (armadilhas para a banca) |
| :--- | :--- | :--- |
| **DRX (XRD)** | Média estatística volumétrica de espaçamento interplanar $d_{002}$ (pico `(002)` do grafite em $2\theta \approx 26{,}5^\circ$ para Cu $K\alpha$, lei de Bragg) e alargamento de picos (estimativa de tamanho médio de cristalito/domínio coerente via Scherrer). | **Não mede flocos individuais** nem garante monocamada isolada pela simples ausência ou baixa intensidade do pico `(002)` (que pode advir de massa insuficiente, desordem turbostrática, esfoliação parcial desorientada ou amorfização). |
| **MEV (SEM)** | Morfologia superficial e dimensões laterais aparentes (área, perímetro, distribuição de tamanho de flocos, aglomeração, dobras) por contraste de elétrons secundários/retroespalhados. | **Não quantifica espessura absoluta nem número exato de camadas** em escala atômica: o contraste de camadas finas varia fortemente com tensão de aceleração, distância de trabalho, função trabalho do substrato, carregamento elétrico e contaminação superficial. |
| **AFM** | Perfil topográfico local em escala subnanométrica/nanométrica (degraus, rugosidade superficial, altura aparente de flocos sobre substrato). | **Sofre convolução geométrica da ponta** (superestimando dimensões laterais) e **erro sistemático de espessura aparente** por camada de hidratação interfacial e interação distinta ponta–grafeno vs. ponta–substrato (Shearer et al., 2016: monocamadas exibem altura aparente tipicamente $> 0{,}34\text{ nm}$, dependendo de modo e ambiente). |

- **Dependência de técnicas complementares:** nenhuma das três técnicas fornece isoladamente a assinatura vibracional de defeitos $sp^3$ / vacâncias ($I_D/I_G$) nem a impressão digital inequívoca do número de poucas camadas via forma da banda $2D$ e razão $I_{2D}/I_G$. Na ausência de **Espectroscopia Raman**, **MET (TEM)** ou **XPS** (especialmente em rotas eletroquímicas com possível oxidação parcial GO/rGO), inferências computacionais sobre "pureza" ou "número de camadas" carecem de *ground truth* físico robusto.

### Risco 4 — Sobrepromessa de Engenharia vs. Fase Investigativa Real
- **Evidência nos arquivos:**
  - `pre-projeto-da-selecao.md` e `Apresentação de Projeto PPGCEM.pptx` propunham uma ferramenta aberta pronta para automação de MEV no PPGCEM.
  - `Apresentação sem título (1).pptx` mencionava *"plataforma web"* (slide 21), estimativa automática de *"pureza"* e *"número de camadas"* (slide 29), pipeline `Scikit-learn + KNN + Regressão Linear + pymatgen` para DRX (slide 30), *"Múltiplas CNNs Especializadas"* para MEV (slide 31), e alegava *"Validação Prévia"* e *"Ativos Encontrados por Agentes"* (slide 32).
  - Paralelamente, `Pré projeto\projeto-atual.md` encontra-se **vazio (`0` bytes)**, e **nenhum software ou modelo está desenvolvido ou validado para grafeno**.
- **Risco acadêmico:** defender soluções de engenharia pesada (plataforma web, múltiplas CNNs) antes de demonstrar que existe viabilidade física, volume amostral suficiente e superioridade sobre PDI clássico (limiarização adaptativa, morfologia matemática, ajuste de perfis/picos) expõe o projeto a críticas severas de falta de foco científico e desconexão com Ciência e Engenharia de Materiais.
- **Estratégia de blindagem na arguição:** adotar a linha do **realismo científico**: o objetivo do mestrado é **investigar a viabilidade técnica e física** de apoiar a caracterização de grafeno — começando por métodos transparentes, interpretáveis e fisicamente calibrados (PDI e análise quantitativa de perfis/picos), recorrendo a ML/VC apenas onde houver ganho mensurável e dados experimentais com referência confiável.

### Risco 5 — Divergência de Duração Oficial, Lacunas Documentais e Erros de DOI
1. **Tempo de apresentação (`40–45 min` vs. `60 min`):** `Seminarios-I-Programa.pdf` (pág. 5) determina expressamente **"tempo de duração entre 40 e 45 minutos"** (e não 60 minutos). Ultrapassar 45 minutos compromete a janela de arguição e pode penalizar o critério *"Capacidade de comunicação e/ou argumentativa"* (2,5 pts).
2. **Alinhamento obrigatório ao programa oficial:** a apresentação deve cobrir os **6 componentes do roteiro** (pág. 4) e atender aos **4 critérios de 2,5 pontos cada** (pág. 6), com ênfase na relação com o **PPGCEM/UFCA** e a relação **processamento–estrutura–propriedades** (`Ciencias dos Materiais - Programa.pdf`, pág. 2).
3. **Erros bibliográficos e de DOIs identificados na auditoria Crossref/DataCite/arXiv:**
   - **Holm et al. (2020) (*Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis*):** o DOI verdadeiro verificado no Crossref é **`10.1007/s11661-020-06008-4`** (*Metallurgical and Materials Transactions A*, 2020). O DOI **`10.1007/s11837-020-04347-6`** (que aparece como erro conhecido a evitar) pertence a outro trabalho completamente distinto no periódico *JOM* (*Investigation of the Nanomechanical Properties of Crystalline Anatase Titanium Dioxide Films Synthesized Using Atomic Layer Deposition*).
   - **`IVEFAC333.pptx` (slide 15):**
     - `Shearer, C. J. et al. (2016)` foi citado sem DOI; DOI real verificado no Crossref: `10.1088/0957-4484/27/12/125704` (*Nanotechnology*, *Accurate thickness measurement of graphene*).
     - `Ba Alawi, Z. (2025)` apresenta quebra de linha no meio do DOI (`·1` / `0.48550/arXiv.2508.04035`), e `Carracedo-Cosme, J. et al. (2021)` usa DOI `10.21950/BFAU11`. Ambos usam prefixos **DataCite** (retornam HTTP 404 na API Crossref e HTTP 200 na API DataCite), detalhe importante para não marcar referências válidas de repositórios como inexistentes por falha de consulta.
     - `Data Science Academy (2022)` é material didático online, não literatura científica revisada por pares; deve ser removido das referências formais do mestrado.
   - **`pre-projeto-da-selecao.md` (linhas 66–81):** lista de referências sem DOIs; `PADILHA` sem ano/editora no bloco final (citado como 2007 no corpo); `DE COST; HOLM` sem ano/volume/páginas (DOI verificado: `10.1016/j.commatsci.2015.08.011`, 2015).
   - **Organização documental:** existência de `Pré projeto\projeto-atual.md` vazio (`0` bytes) e cópia espelhada das pastas originais dentro de `C:\Users\emer\dissertacao\Artigos\`.

---

## 3. Tabela de Rastreabilidade: Verificado Empiricamente vs. Incerto / Não Testado

| Item / Aspecto | Status nesta sessão | Evidência ou Motivo da Incerteza |
| :--- | :--- | :--- |
| SO Windows 10 Pro (`10.0.19045`) e PowerShell `5.1.19041.6456` | **Verificado empiricamente** | `Get-CimInstance Win32_OperatingSystem` e `$PSVersionTable.PSVersion` executados localmente. |
| Stub `WindowsApps\python.exe` (`0` bytes, exit `9009`) vs. `uv 0.13.7` + `python3.11.exe` (`3.11.18`) | **Verificado empiricamente** | `Get-Command python`, `python --version`, `uv --version` e `python3.11.exe --version`. |
| Presença de `node v26.13.0`, `npm/npx 11.20.0`, `agy.exe`, `winget.exe` | **Verificado empiricamente** | Executados e inspecionados via `Get-Command` e `--version`. |
| Ausência no `PATH` de `git`, `pandoc`, `quarto`, `marp`, `pdflatex`, `xelatex`, `lualatex`, `typst`, `soffice`, `libreoffice`, `zotero`, `docker`, `java`, `tesseract`, `gh`, `pip`, `pipx`, `conda`, `choco`, `py` | **Verificado empiricamente** | `Get-Command` retornou `NOT_FOUND` para todos os binários listados. |
| Ausência de credenciais em `C:\Users\emer\.env` e `mcp_config.json` global vazio (`0` bytes) | **Verificado empiricamente** | `Test-Path` retornou `False` no início (e `Length = 0` bytes ao final da sessão, sem chaves); `read_file` confirmou `mcp_config.json` vazio. |
| Hardware restrito (Ryzen 3 7320U, `3.396.860 KB` / ~3,24 GiB RAM visível, sem GPU NVIDIA/CUDA) e presença de `chrome.exe` fora do `PATH` | **Verificado empiricamente** | `Get-CimInstance Win32_Processor` / `Win32_OperatingSystem` e `Test-Path "C:\Program Files\Google\Chrome\Application\chrome.exe"` (`True`). |
| Plugins/skills instalados (`science v1.4.0`, `google-antigravity-sdk v0.0.9`, `swarm`, `biomolecular_structure_viewer_mcp`) | **Verificado empiricamente** | Leitura direta de `config.json`, `plugins\science\mcp_config.json`, `skills.json` e listagem de pastas. |
| Limite OpenAlex sem chave (`$0,10/dia`, `985/1000` restantes) e bloqueio HTTP `429` do Semantic Scholar sem chave | **Verificado empiricamente** | Execução de `openalex_cli.py rate-limit` e GET único na API pública do Semantic Scholar. |
| DOIs históricos (`10.1007/s11661-020-06008-4` vs `10.1007/s11837-020-04347-6`, `10.1088/0957-4484/27/12/125704`, `10.1021/acs.jcim.1c01323`, `10.1037/h0042519`, `10.1109/CVPR.2016.90`, `10.1016/j.commatsci.2015.08.011`, `10.1103/PhysRevLett.56.930`, `10.21950/BFAU11`, `10.48550/arXiv.2508.04035`) | **Verificado empiricamente** | Consultas HTTP GET nas APIs oficiais Crossref, DataCite e arXiv. |
| Conteúdo textual/notas dos PDFs (`Seminarios-I-Programa.pdf`, `Ciencias dos Materiais - Programa.pdf`), Markdowns e 3 `.pptx` | **Verificado empiricamente** | `read_file` nos PDFs/MDs e extração XML via `zipfile`/`ElementTree` nos 3 `.pptx`. |
| Servidores MCP do GitHub (Zotero, arXiv, `paper-search-mcp`, Semantic Scholar, `docling-mcp`) | **Incerto / Não testado** | Não estão instalados nem configurados no ambiente local; compatibilidade e estabilidade em Windows 10 avaliadas apenas via documentação. |
| Aplicativos GUI fora do `PATH` (Word, PowerPoint, Edge, visualizadores PDF locais) e exportação PDF via Chrome | **Incerto / Não testado** | `chrome.exe` foi localizado, mas não houve varredura de pacotes Office nem teste de exportação PDF via navegador. |
| Acesso a textos completos pagos via rede institucional / Portal CAPES | **Incerto / Não testado** | Apenas metadados públicos (Crossref/DataCite/arXiv/OpenAlex) foram consultados; não se testou acesso via proxy/rede da UFCA a periódicos fechados. |
| Conteúdo textual embutido em imagens rasterizadas dos slides antigos (`38` mídias em `Apresentação sem título (1).pptx`, `69` em `Apresentação de Projeto PPGCEM.pptx`) | **Incerto / Não testado** | Extração por XML não lê texto dentro de imagens; sem OCR (`tesseract`) ou inspeção visual individual de cada mídia. |
| Disponibilidade, volume e pareamento experimental (DRX/MEV/AFM + Raman/TEM) das amostras reais de grafeno na UFCA | **Incerto / Não testado** | Não constam conjuntos de dados experimentais reais na pasta inspecionada; depende de levantamento junto ao orientador e laboratório do PPGCEM. |
| Execução de `run_workflow` no Windows 10 com o stub `python.exe` ativo no `PATH` | **Incerto / Não testado** | Não foi testado em execução nesta missão; exige validação prévia caso se opte por `run_workflow` em vez de `/swarm`. |

---

## 4. Alternativas Práticas e Decisão para Hoje (16/11) vs. Pós-Seminário (Missão 02)

1. **Não instalar infraestrutura pesada hoje:** ignorar Docker/GROBID, distribuições LaTeX completas, Zotero MCP (sem Zotero Desktop instalado) e `tesseract` antes do seminário de 17/11.
2. **Usar execução efêmera + nativa hoje:** utilizar exclusivamente ferramentas já ativas (`read_file`, `/swarm`, `literature_search_openalex`, `literature_search_arxiv`, `literature_search_europepmc`, scripts read-only com `python3.11.exe`) e, quando aprovado para a etapa de slides pós-Missão 02, execução efêmera (`uv run --with python-pptx`, `npx @marp-team/marp-cli` ou PowerPoint/PDF).
3. **Desbloquear pesquisa em escala na Missão 02 (com aprovação do usuário):** criar `C:\Users\emer\.env` via protocolo seguro de credenciais contendo `OPENALEX_API_KEY` (gratuita, sobe de `$0,10/dia` compartilhado para `$1/dia` dedicado e libera `download-pdf`) e, opcionalmente, chave gratuita da API do Semantic Scholar para contornar o `HTTP 429`.
