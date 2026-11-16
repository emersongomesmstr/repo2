# 01 — Inventário do Ambiente, Capacidades Nativas do Antigravity e Auditoria Documental

**Missão 01 — Preparação de Ambiente e Auditoria Inicial (PPGCEM/UFCA)**  
**Data da auditoria:** 16/11/2026 | **Seminários I:** 17/11/2026 | **Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
**Autor:** Agente 4 (`@agente-documentos`)  
**Status do projeto:** **Fase investigativa de viabilidade científica** — o software computacional **NÃO está desenvolvido nem validado**.

> [!IMPORTANT]
> **Divergência Crítica de Duração (Seminários I):** O programa oficial da disciplina ([Seminarios-I-Programa.pdf](file:///C:/Users/emer/dissertacao/Disciplinas-Mestrado/Seminarios-I-Programa.pdf), p. 5) estabelece apresentações individuais com duração entre **40 e 45 minutos**, **e não 60 minutos** como mencionado inicialmente. O planejamento da apresentação deve seguir estritamente a faixa oficial de **40–45 minutos**.

---

## 1. Diagnóstico Técnico do Ambiente Real (Verificado Empiricamente)

### 1.1 Sistema Operacional e Hardware

| Componente | Especificação Verificada | Observação Operacional |
|---|---|---|
| **Sistema Operacional** | Microsoft Windows 10 Pro (`10.0.19045.0`, Build `19045`, 64 bits) | Verificado via `[System.Environment]::OSVersion` e `Win32_OperatingSystem` |
| **Shell padrão** | Windows PowerShell `5.1.19041.6456` | Sintaxe Bash (`&&`, heredocs Unix, `/tmp`) falha; usar PowerShell (`;` / here-strings `@' ... '@`) |
| **Processador (CPU)** | AMD Ryzen 3 7320U with Radeon Graphics (4 núcleos físicos / 8 threads) | Suficiente para análise documental, consultas API e PDI clássico leve |
| **Memória RAM visível** | `3.396.860 KB` (~3,24 GiB total visível); `248.784 KB` (~243 MiB livres na leitura) | **Restrição severa** para containers pesados (Docker/GROBID), modelos locais de LLM/VLM ou treino de CNNs localmente |
| **GPU** | AMD Radeon(TM) 610M integrada (`AdapterRAM = 536.870.912 B` / 512 MiB; driver `32.0.21030.11004`) | **Sem GPU NVIDIA/CUDA** — inviável para aceleração CUDA local |
| **Disco (`C:`)** | `120.932.253.696 B` (~112,6 GiB usados) / `134.421.159.936 B` (~125,2 GiB livres) | Espaço livre adequado para PDFs, caches efêmeros do `uv` e dados |
| **WSL2** | `wsl --status` retorna distribuição padrão `Ubuntu`, versão `2` | Presença verificada; conteúdo/pacotes internos no Ubuntu não foram inspecionados |
| **Navegador (fora do PATH)** | `C:\Program Files\Google\Chrome\Application\chrome.exe` presente | Microsoft Office, LibreOffice e Zotero não encontrados em `Program Files` padrão |

### 1.2 Binários e Runtimes Presentes no Sistema

| Binário / Ferramenta | Versão Verificada | Caminho Real | Observações |
|---|---|---|---|
| **`uv`** | `uv 0.13.7` (`316c827e0 2026-11-03 x86_64-pc-windows-msvc`) | `C:\Users\emer\.local\bin\uv.exe` | `uv tool list` retornou `No tools installed` |
| **`python3.11.exe`** | `Python 3.11.18` (CPython 64-bit gerenciado pelo `uv`) | `C:\Users\emer\.local\bin\python3.11.exe` (aponta para `AppData\Roaming\uv\python\cpython-3.11.18-windows-x86_64-none\python.exe`) | Único Python funcional. Via `-m pip list`: apenas `pip 26.2.2` e `setuptools 84.2.0` |
| **`python.exe` / `python3.exe`** | Stub `0.0.0.0` (0 bytes) — **NÃO funcional** | `C:\Users\emer\AppData\Local\Microsoft\WindowsApps\python.exe` e `python3.exe` | Atalho da Microsoft Store; bloqueia scripts que chamam `python3` diretamente (afeta ex. `run_workflow`) |
| **`node`** | `v26.13.0` (`26.13.0.0`) | `C:\Program Files\nodejs\node.exe` | Funcional |
| **`npm` / `npx`** | `11.20.0` | `C:\Program Files\nodejs\npm.ps1` / `npm.cmd` / `npx.ps1` / `npx.cmd` | `npm list -g --depth=0` falha com `ENOENT` (`AppData\Roaming\npm` inexistente — 0 pacotes globais) |
| **`agy.exe`** | Metadado `0.0.0.0` (binário CLI do Antigravity) | `C:\Users\emer\AppData\Local\agy\bin\agy.exe` | Também presentes em `.gemini\antigravity\bin`: `agy-node.cmd`, `agentapi.bat`, `webm_encoder.exe` |

### 1.3 Binários Ausentes no `PATH` (Verificado via `Get-Command`)

Todos os seguintes binários foram testados e estão **AUSENTES** no `PATH` atual do Windows:

- **Controle de versão e GitHub:** `git`, `gh`
- **Publicação, slides e LaTeX:** `pandoc`, `quarto`, `marp`, `typst`, `pdflatex`, `xelatex`, `lualatex`
- **OCR, suíte Office e referência bibliográfica:** `tesseract`, `soffice`, `libreoffice`, `zotero`
- **Containers e runtimes adicionais:** `docker`, `java`, `conda`, `pipx`
- **Python CLI direto:** `pip` (ausente como binário autônomo no `PATH`; acessível apenas via `C:\Users\emer\.local\bin\python3.11.exe -m pip`)
- **Utilitários Unix ausentes no `PATH` PowerShell:** `rg`, `grep`

### 1.4 Credenciais e Arquivo `~/.env`

- **`~/.env` (`C:\Users\emer\.env`):** **NÃO EXISTE** (`Test-Path "$env:USERPROFILE\.env"` = `False`).
- **Variáveis de ambiente ausentes:** `OPENALEX_API_KEY`, `USER_EMAIL`, `GEMINI_API_KEY`, `SEMANTIC_SCHOLAR_API_KEY` e `NCBI_API_KEY` não estão definidas nem em arquivo `.env` nem no ambiente do processo.
- **Impacto prático imediato:** conforme a skill `literature_search_openalex`, a ausência de `OPENALEX_API_KEY` restringe o uso do OpenAlex ao orçamento compartilhado por IP de **$0,10/dia** (10 req/s) e impede downloads diretos via `content.openalex.org` (`download-pdf` usa apenas fallback de URLs abertas quando disponíveis).

---

## 2. Inventário de Capacidades Nativas do Antigravity

### 2.1 Configurações Globais e Plugins Ativos

Arquivos auditados em `C:\Users\emer\.gemini\config\`:

1. **[config.json](file:///C:/Users/emer/.gemini/config/config.json)**:
   - **Plugins declarados:**
     - `google-antigravity-sdk` (`antigravity-plugins-official/plugin/google-antigravity-sdk`, versão `0.0.9`)
     - `science` (`antigravity-plugins-official/plugin/science`, versão `1.4.0`)
     - `swarm` (`enabled: true`)
   - **Sidecars ativos:**
     - `science/biomolecular_structure_viewer` (`projectId: e0b4f9c5-3e81-4f2e-9bdd-16538aef5af3`)
     - `swarm/swarm_board` (`projectId: e971dec7-6d98-44b7-82e3-1a1b6d2c52e7`)
   - **Configurações de execução (`userSettings`):** `artifactReviewMode: ARTIFACT_REVIEW_MODE_TURBO`, `autoExecutionPolicy: CASCADE_COMMANDS_AUTO_EXECUTION_EAGER`, `browserJsExecutionPolicy: BROWSER_JS_EXECUTION_POLICY_TURBO`, `enableTerminalSandbox: false`, `nonWorkspaceFileAccessPolicy: AGENT_SETTING_POLICY_ALLOW`, `permissionPreset: AGENT_PERMISSION_PRESET_TURBO`, `globalPermissionGrants.allow: ["command(*)", "mcp(*)", "read_file(*)", "write_file(*)"]`.
   - **Host remoto:** `desktop-im1gb5c-plasma-ember`.
2. **[mcp_config.json](file:///C:/Users/emer/.gemini/config/mcp_config.json)**: arquivo vazio (0 bytes) — nenhum servidor MCP global configurado manualmente fora de plugins.
3. **[skills.json](file:///C:/Users/emer/.gemini/config/skills.json)**: registra os diretórios `~/.gemini/config/skills` e `C:/Users/emer/.gemini/antigravity/builtin/skills`.
4. **Contas de plugins (`list_plugin_accounts`):** *"No installed plugins declare account sign-ins."*

### 2.2 Plugin `science` (`v1.4.0`)

- **Manifesto ([plugin.json](file:///C:/Users/emer/.gemini/config/plugins/science/plugin.json)):** `name: "science"`, `displayName: "Science"`, `version: "1.4.0"`, descrição: *"Curated collection of agent skills for science tasks."*
- **MCP Config ([mcp_config.json](file:///C:/Users/emer/.gemini/config/plugins/science/mcp_config.json)):** declara **1 único servidor MCP**:
  - `biomolecular_structure_viewer_mcp` (`command: "agy-node"`, `args: ["sidecars/biomolecular_structure_viewer/dist/mcp_entry.cjs"]`) — visualizador 3D Mol* para arquivos `.cif`, `.mmcif`, `.pdb`. Não atende grafeno/DRX/MEV/AFM nem busca bibliográfica.
- **Regra do plugin ([rules/AGENTS.md](file:///C:/Users/emer/.gemini/config/plugins/science/rules/AGENTS.md)):** prioriza o uso dos sidecars interativos de visualização científica sobre imagens estáticas ou Generative UI quando aplicável.
- **Registros de licença ativos no workspace:** `C:\Users\emer\dissertacao\Missao1\.licenses\` já contém arquivos de notificação gerados em `2026-11-16T11:58:35-03:00` para `literature_search_arxiv`, `literature_search_europepmc` e `literature_search_openalex`.

**Lista completa das 48 skills instaladas em `C:\Users\emer\.gemini\config\plugins\science\skills\`:**

| Categoria | Quantidade | Skills (`nome do diretório`) | Aderência à Missão (Grafeno / DRX / MEV / AFM / ML) |
|---|---|---|---|
| **Busca de Literatura (Relevantes)** | 2 | `literature_search_openalex`, `literature_search_arxiv` | **Alta** — bases multidisciplinares/física/materiais/IA |
| **Busca de Literatura (Biomédicas)** | 3 | `literature_search_europepmc`, `literature_search_biorxiv`, `pubmed_database` | **Baixa** (foco biomédico/ciências da vida; úteis apenas para bioaplicações ou metadados pontuais) |
| **Infraestrutura e Fluxo do Plugin** | 3 | `uv`, `credentials`, `workflow_skill_creator` | **Alta** (`uv` já instalado; `credentials` define protocolo seguro para `~/.env`) |
| **Química, Quimioinformática e Estruturas** | 12 | `pubchem_database`, `chembl_database`, `rdkit_general`, `cheminformatics_core`, `cheminformatics_cofolding`, `cheminformatics_doc2mol`, `cheminformatics_ml`, `cheminformatics_physics`, `cheminformatics_reactions`, `biomolecular_structure_viewer`, `pymol`, `pdb_database` | **Baixa a pontual** (ex.: `pubchem_database` pode consultar CIDs moleculares como os do piloto $C_6H_4BrClO$; não cobrem estado sólido/DRX de grafeno) |
| **Proteômica / Genômica / Biologia / Clínica** | 27 | `alphafold_database_fetch_and_analyze`, `alphagenome_atlas_website_links`, `alphagenome_single_variant_analysis`, `alphagenome_variant_impact_score`, `clinical_trials_database`, `clinvar_database`, `dbsnp_database`, `embl_ebi_ols`, `encode_ccres_database`, `ensembl_database`, `foldseek_structural_search`, `gnomad_database`, `gtex_database`, `human_protein_atlas_database`, `interpro_database`, `jaspar_database`, `ncbi_sequence_fetch`, `openfda_database`, `opentargets_database`, `protein_sequence_msa`, `protein_sequence_similarity_search`, `quickgo_database`, `reactome_database`, `string_database`, `ucsc_conservation_and_tfbs`, `unibind_database`, `uniprot_database` | **Nula** para o escopo PPGCEM/grafeno |
| **Humanidades Clássicas** | 1 | `predictingthepast` | **Nula** (restauração de latim/grego antigo) |
| **Total** | **48** | — | **5 úteis diretamente** (`openalex`, `arxiv`, `uv`, `credentials`, `pubchem` pontual) |

### 2.3 Plugin `google-antigravity-sdk` (`v0.0.9`)

- **Localização:** `C:\Users\emer\.gemini\config\plugins\google-antigravity-sdk\`
- **Estrutura verificada:** `plugin.json` (Apache-2.0, `Using the Google Antigravity Python SDK to build AI agents`), `skills/google-antigravity-sdk/SKILL.md`, `examples/getting_started/`, e 8 documentos em `references/` (`agent_configuration.md`, `architecture.md`, `built_in_tools.md`, `error_handling.md`, `local_models.md`, `mcp_integration.md`, `observability.md`, `safety_policies.md`).
- **Requisitos:** requer pacote Python `google-antigravity` (não instalado) e `GEMINI_API_KEY` (ou runtime local LiteRT / servidor OpenAI-compatible). Serve para construir agentes customizados em código Python via `Agent` / `Conversation` / `Connection`, não sendo necessário para operar o swarm nativo do IDE.

### 2.4 Skills Pessoais (`C:\Users\emer\.gemini\config\skills\`)

- `optimize-tokens` (`name: optimize-for-tokens`) — auditoria de estrutura de projeto para redução de consumo de tokens.
- `plan-token-optimization` (`name: plan-token-optimization`) — planejamento de redução de contexto sem editar arquivos.

### 2.5 Plugins e Skills Built-in (`C:\Users\emer\.gemini\antigravity\builtin\`)

- **Plugin `swarm`** (`builtin/plugins/swarm/plugin.json` + `sidecars/swarm_board/`): habilitado e ativo nesta sessão.
- **14 skills built-in:** `agy-customizations`, `antigravity_guide`, `automation`, `generative_ui`, `mcp-app-development`, `migrate-agent-settings`, `migrate-workflows`, `native_swarm`, `permissioned-github`, `plugin`, `run-workflow`, `swarm_monitor`, `swarm_narrator`, `ui-plugin-navigation`.
- **Detalhamento das 5 capacidades built-in centrais para a orquestração:**
  1. **`swarm` (`native_swarm/SKILL.md`):** coordenação nativa multiagente via quadro compartilhado (`swarm`, `post_message`, `read_board`, `swarm_wait`). Suporta `workspace: "inherit" | "share" | "branch"`, fork de histórico e sidecar visual (`swarm_board`). É o mecanismo ativo e funcional no Windows atual.
  2. **`run_workflow` (`run-workflow/SKILL.md`):** orquestração programática em Python (`agent`, `parallel`, `pipeline`, `phase`, `trajectory`). **Alerta de compatibilidade:** a documentação exige *"The script runs in its own `python3` process, which needs Python 3.8 or later on `PATH`"*, porém `python3.exe` no `PATH` atual aponta para o stub `0.0.0.0` da WindowsApps — risco de falha se invocado sem ajuste de `PATH`.
  3. **`agy-customizations` (`agy-customizations/SKILL.md`):** governa descoberta e precedência de customizações (`Workspace .agents/` > `skills.json`/`plugins.json` > Global `~/.gemini/config/` > Built-in) e carregamento progressivo de `SKILL.md` e `GEMINI.md`/`AGENTS.md`.
  4. **`plugin` (`plugin/SKILL.md`):** gerenciamento do ciclo de vida de plugins (inventário via Language Server RPC, habilitação/desabilitação por link `customization://` e sugestão de Marketplace via `<plugin-card>`).
  5. **`generative_ui` (`generative_ui/SKILL.md`):** renderização de HTML/JS interativo inline (`<= 450 px`, `<agent-embed>`) ou artefatos standalone usando Tailwind allowlisted (`gstatic.com`) e variáveis semânticas de tema.

---

## 3. Auditoria Completa dos Documentos em `C:\Users\emer\dissertacao\`

### 3.1 Inventário Geral de Arquivos e Duplicidade Verificada

A verificação por hash **SHA-256** confirmou que a subpasta `C:\Users\emer\dissertacao\Artigos\` contém `PROMPT_MESTRE.md` (Missão 02) e **cópias bit-a-bit idênticas** de todas as pastas de apresentações, disciplinas e pré-projeto da raiz:

| Caminho na Raiz | Cópia em `Artigos\` | Tamanho | Hash SHA-256 (prefixo 12) | Idênticos? |
|---|---|---|---|---|
| `PROMPT.txt` | *(somente raiz)* | 10.775 B | — | — |
| *(somente `Artigos\`)* | `Artigos\PROMPT_MESTRE.md` | 15.865 B | — | — |
| `Apresentacoes_passadas\Apresentação de Projeto PPGCEM.pptx` | `Artigos\Apresentacoes_passadas\...` | 1.115.676 B | `445642a9a60f` | Sim |
| `Apresentacoes_passadas\Apresentação sem título (1).pptx` | `Artigos\Apresentacoes_passadas\...` | 12.254.154 B | `ee68d1931242` | Sim |
| `Apresentacoes_passadas\IVEFAC333.pptx` | `Artigos\Apresentacoes_passadas\...` | 1.371.980 B | `3ba9f50f3422` | Sim |
| `Disciplinas-Mestrado\Ciencias dos Materiais - Programa.pdf` | `Artigos\Disciplinas-Mestrado\...` | 666.934 B | `77930e661ed5` | Sim |
| `Disciplinas-Mestrado\Seminarios-I-Programa.pdf` | `Artigos\Disciplinas-Mestrado\...` | 427.571 B | `862e4ff1786c` | Sim |
| `Pré projeto\pre-projeto-da-selecao.md` | `Artigos\Pré projeto\...` | 11.030 B | `1e5355420885` | Sim |
| `Pré projeto\projeto-atual.md` | `Artigos\Pré projeto\...` | **0 B (vazio)** | `e3b0c44298fc` | Sim |

> [!WARNING]
> **Lacuna Documental Crítica:** O arquivo [projeto-atual.md](file:///C:/Users/emer/dissertacao/Pré%20projeto/projeto-atual.md) possui **0 bytes (vazio)**. Não há hoje um texto-base formal atualizado da dissertação descrevendo o recorte atual (grafeno + DRX/MEV/AFM); a definição do escopo atual existe apenas nos prompts operacionais ([PROMPT.txt](file:///C:/Users/emer/dissertacao/PROMPT.txt) e [PROMPT_MESTRE.md](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md)).

### 3.2 Disciplina: Seminários I ([Seminarios-I-Programa.pdf](file:///C:/Users/emer/dissertacao/Disciplinas-Mestrado/Seminarios-I-Programa.pdf))

- **Metadados:** 6 páginas PDF (numeradas internamente até `5/5`, pois a página 5 repete o marcador `4/5`), Agosto de 2026, PPGCEM/UFCA, **Professoras: Laédna Neiva e Isabel Brasileiro Rodrigues**. Carga horária: **32 horas**. Atendimento: segundas e quartas-feiras, 10h–12h. Início das apresentações: `15/setembro/2026`.
- **Objetivo (p. 2):** Desenvolver a capacidade do pós-graduando de conceber, estruturar e comunicar de forma clara, crítica e fundamentada a proposta de pesquisa de dissertação, articulando problema, fundamentação científica, objetivos, metodologia e contribuições esperadas.
- **6 Componentes Obrigatórios do Roteiro (p. 4 — "Sugestão de roteiro para construção das apresentações"):**
  1. Definir o que será desenvolvido e a aplicação principal.
  2. Apresentar a fundamentação científica e o estado da arte de cada projeto de dissertação.
  3. Apresentar a justificativa desta oportunidade de pesquisa.
  4. Apresentar o planejamento metodológico da pesquisa.
  5. Apresentar estimativas de resultados ou impactos esperados.
  6. Apresentar as principais referências bibliográficas.
- **Duração Oficial (p. 5 — "Metodologia da Disciplina"):** *"A disciplina será conduzida na forma de apresentações individuais com tempo de duração entre **40 e 45 minutos**."* (**DIVERGÊNCIA CRÍTICA** em relação aos 60 minutos citados inicialmente.)
- **4 Critérios de Avaliação (p. 6, total = 10,0 pontos):**
  1. O grau de entendimento do discente sobre o seu projeto de dissertação (**2,5 pontos**).
  2. Clareza dos objetivos (**2,5 pontos**).
  3. Capacidade de comunicação e/ou argumentativa (**2,5 pontos**).
  4. Relação da temática da dissertação com o objetivo do programa PPGCEM/UFCA (**2,5 pontos**).

### 3.3 Disciplina: Ciência dos Materiais ([Ciencias dos Materiais - Programa.pdf](file:///C:/Users/emer/dissertacao/Disciplinas-Mestrado/Ciencias%20dos%20Materiais%20-%20Programa.pdf))

- **Metadados:** 10 páginas PDF (numeradas até `8/9`), Agosto de 2026, **Professoras: Laédna Neiva e Isabel Brasileiro Rodrigues**, **64 horas**. Avaliações: 1ª escrita (`14/10/2026`), 2ª a definir (Profa. Isabel), **3ª seminário individual com início em `16/11/2026`** (coincidindo com a véspera/semana de Seminários I!) e previsão de Avaliação Final em `09/12/2026`.
- **Aderência direta ao tema do projeto (Critério 4 de Seminários I):**
  - Os objetivos da disciplina (p. 2) enfatizam o estudo das propriedades em níveis **microscópico e macroscópico** e a relação **processamento / estrutura / propriedades / desempenho**.
  - O conteúdo programático (pp. 4–5) cobre diretamente os fundamentos exigidos na caracterização de grafeno e derivados: **2) Teorias de ligações químicas em sólidos** (ligações $sp^2$ / empilhamento van der Waals), **3) Estrutura cristalina / Sólidos amorfos** (rede hexagonal, base física de DRX), **4) Defeitos cristalinos** (vacâncias, bordas, desordem estrutural), **7) Propriedades e aplicações**, **9–13) Propriedades mecânicas, elétricas, magnéticas, térmicas e ópticas**.
  - O tema nº 8 de seminário (p. 10) é explicitamente **"Relação Estrutura – Propriedade dos Materiais"**.
  - **Bibliografia da disciplina (p. 8):** Básica — Callister (10ª ed., LTC, 2024) e Shackelford (6ª ed., Pearson, 2018); Complementar — Askeland & Phulé (Cengage, 2019), Fahlman (*Materials Chemistry*, 4th ed., Springer, 2023) e White (*Physical Properties of Materials*, 3rd ed., CRC Press, 2019).

### 3.4 Pré-projeto da Seleção ([pre-projeto-da-selecao.md](file:///C:/Users/emer/dissertacao/Pré%20projeto/pre-projeto-da-selecao.md))

- **Título:** *Desenvolvimento de uma ferramenta computacional baseada em visão computacional para caracterização automatizada de microestruturas em materiais* (Brejo Santo, 2026, Linha: Tecnologia dos Materiais).
- **Escopo original:** focado **exclusivamente em micrografias MEV** dos laboratórios do PPGCEM/UFCA, empregando Python + OpenCV (Bradski, 2000) + Scikit-image (van der Walt et al., 2014) para pré-processamento, segmentação e extração geométrica (tamanho de grão, área, perímetro, circularidade, porosidade), com ML colocado apenas como opção condicional futura (*"Caso o volume e diversidade das imagens seja suficiente"*). Cronograma original: `2026.2` a `2028.1`.
- **Referências citadas (9):** Callister & Rethwisch (2018), Holm et al. (2020), Gerhardt & Silveira (2009), Padilha (2007), Gonzalez & Woods (2018), Szeliski (2022), Bradski (2000), van der Walt et al. (2014), De Cost & Holm (sem ano/volume no texto).

### 3.5 Auditoria das 3 Apresentações em `Apresentacoes_passadas\`

#### A. [Apresentação de Projeto PPGCEM.pptx](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/Apresentação%20de%20Projeto%20PPGCEM.pptx)
- **Estrutura:** 10 slides, `1.115.676 B`, 69 PNGs internos, **notas do apresentador presentes** em 6 slides (`notesSlide1`, `2`, `3`, `4`, `7`, `8`). Fontes embutidas (`Poppins`, `Lato`).
- **Observação técnica de extração:** Grande parte do conteúdo textual nos slides 2–9 foi inserida como **imagens PNG rasterizadas (`Google Shape;...`)** em vez de caixas de texto editáveis XML — o que impede leitores apenas de `<a:t>` de recuperar o conteúdo completo sem inspeção visual/OCR.
- **Conteúdo verificado (XML + notas + inspeção visual dos cartões PNG):**
  - **Slide 1:** Título (mesma proposta do pré-projeto da seleção — caracterização quantitativa automatizada de microestruturas via MEV) + nota introdutória.
  - **Slide 2 (*Motivação*):** Cartões PNG (`Micrografias`, `Análise manual`, `Tempo elevado`, `Subjetividade`, `Baixa reprodutibilidade`), imagem composta com 4 micrografias MEV (`15kV X1,000 10µm COPPE/UFRJ`, `image14.png`), e **placeholder cinza `600 × 400` não substituído** (`image8.png`).
  - **Slide 3 (*Estado da Arte*):** Ref. `Holm et al. (2020) | De Cost & Holm`; cartões PNG (`Caracterização`, `ImageJ`, `Análise manual`, `Ferramenta proposta`).
  - **Slide 4 (*O Problema de Pesquisa*):** Pergunta sobre automatização de microestruturas em MEV; cartões PNG (`MEV`, `Processamento`, `Segmentação`, `Extração`, `Resultados`); nota: *"O foco do projeto não é substituir o pesquisador..."*.
  - **Slide 5 (*Objetivos*):** Objetivo geral (ferramenta robusta e código aberto para MEV) e 6 específicos (banco de imagens, desenvolvimento, segmentação, extração de parâmetros, validação, código aberto) + bloco azul sólido (`image24.png`).
  - **Slide 6 (*Metodologia*):** Fluxo em cartões PNG (`Revisão Bibliográfica`, `Banco de Imagens`, `Desenvolvimento`, `Segmentação`, `Extração de parâmetros`, `Validação`, `Ferramenta Final`).
  - **Slide 7 (*Arquitetura da Ferramenta*):** Pipeline `Micrografia MEV → Pré-processamento → Segmentação → Extração de Características → Relatórios` + nota detalhando área, perímetro, circularidade, tamanho de grão e porosidade.
  - **Slide 8 (*Resultados Esperados*):** Comparativo Cenário Atual vs. Com o Projeto + nota crítica reaproveitável: *"Mostre que o software é consequência. O objetivo é melhorar a pesquisa."*
  - **Slide 9 (*Contribuições do Projeto*):** Cartões PNG (`Ferramenta científica`, `Código aberto`, `Apoio ao PPGCEM`, `Possibilidade de expansão`) e palavra residual `Obrigado.` (também repetida no Slide 10).
  - **Slide 10 (*Limitações do Projeto*):** Delimitação para uma classe específica de materiais inicialmente, com adaptação futura mediante validação.

#### B. [Apresentação sem título (1).pptx](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/Apresentação%20sem%20título%20(1).pptx)
- **Estrutura:** 32 slides, `12.254.154 B`, 38 mídias (PNG/JPG e 4 GIFs pesados até 4,7 MB), sem notas do apresentador. Vários slides introdutórios têm conteúdo apenas em imagem rasterizada (sem `<a:t>`).
- **Título real da capa (verificado na imagem `image5.jpg` do Slide 1):** *"SEMINÁRIO / APLICAÇÕES DE IA — Introdução à IA e Diferenças de Métodos e Modelos para ML/DL na Caracterização de Materiais via MeV ou DRX"* (Emerson Gomes, PPGCEM / UFCA).
- **Mapeamento por blocos:**
  - **Slides 1–15 (Fundamentos de IA/ML/DL):** Capa (S1); Venn IA > ML > DL (S2); Neurônios naturais e artificiais, Johan Jarnestad (S3–S4); Rede Neural, MLP, CNN, RNN, LSTM, GAN (S5–S12); Meme "Transformers Prime" (S13) seguido de Transformers (S14–S15).
  - **Slides 16–28 (Frameworks e Paradigmas):** Bibliotecas e Frameworks (S16); Diagrama Scikit-learn vs TensorFlow vs PyTorch de Sumit Srivastava (S17); Gráficos de comparação PyTorch vs TensorFlow citando `https://arxiv.org/html/2508.04035v1` (S18–S21: adoção indústria/pesquisa, tempo de treino 16,98h vs 21,95h citando Novac et al. 2022, GPU/TPU images/sec, deployment browser/mobile e frase informal *"Se fossemos criar uma plataforma web, o PyTorch seria uma péssima ideia…"*); Diagrama Supervisionado/Não Supervisionado/Reforço (S22); Exemplo didático Cachorros vs Gatos com `PyTorch+ResNet (Torchvision)` (S23–S27); Aprendizado por Reforço com Gymnasium (S28).
  - **Slides 29–32 (Primeira inflexão para Grafeno + DRX + MEV — com excessos):**
    - **S29 (*Objetivos e Questões-Chave*):** *"Temos grafeno? Ou Grafite?"*, *"Quantas camadas?"*, *"Temos como estimar a pureza?"*, *"Como melhorar a qualidade de vida do técnico/pesquisador?"*
    - **S30 (*DRX*):** Dados brutos com `Scikit-learn + KNN + Regressão Linear + pymatgen` + ilustração IA 3D.
    - **S31 (*MEV*):** `CNN + Visão Computacional` e *"Múltiplas CNNs Especializadas"* em paralelo.
    - **S32 (*Diferenciais & Agilidade*):** Afirma *"Validação Prévia — Já começamos a testar antes das aulas começarem"* e *"Ativos Encontrados por Agentes — Temos imagens e datasets encontrados por AI Agents"*. **Alerta:** essas afirmações do rascunho **NÃO devem ser repetidas** no seminário atual de viabilidade sem evidência empírica e validação.

#### C. [IVEFAC333.pptx](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/IVEFAC333.pptx)
- **Estrutura:** 15 slides, `1.371.980 B`, 14 mídias, sem notas do apresentador.
- **Evento e autoria (Slide 1):** *IV Encontro de Física e Astronomia do Cariri (IV EFAC 2026)*, 11–12 de novembro de 2026, Campus Brejo Santo (apoio FUNCAP), Eixo 3 — Física Computacional e Ciência de Dados, Apresentação Oral. Título: *"Redes Neurais na caracterização de imagens microscópicas: Recorte comparativo com imagens simuladas de AFM"*, por **Emerson de Sousa Gomes¹** (PPGCEM/UFCA e IFE/UFCA) e **Job Saraiva Furtado Neto²** (CCT/UFCA, doutor em Física da Matéria Condensada pela UFAL).
- **Conteúdo por slide:**
  - **S2–S3:** 3 isômeros moleculares de $C_6H_4BrClO$ do conjunto **QUAM-AFM Lite**: `CID 16268` (2-bromo-6-clorofenol), `CID 19859` (4-bromo-2-clorofenol) e `CID 69670` (2-bromo-4-clorofenol).
  - **S4 (*Objetivos*):** Discutir ML em imagens AFM comparando PyTorch vs TensorFlow; **Motivação explícita:** *"Caracterização de amostras de grafeno obtidos por esfoliação eletroquímica."*
  - **S5–S9 (*Fundamentação*):** Princípio do AFM (Binnig, Quate e Gerber, 1986) em imagens simuladas a altura constante; Perceptron de Rosenblatt (1958) com exemplo didático ("Eu vou ao casamento?"); matriz de pixels 5×5; MLP vs CNN (**ResNet-18**, He et al., 2016).
  - **S10–S12 (*Metodologia*):** Overfitting vs Underfitting; piloto no **QUAM-AFM Lite** (Carracedo-Cosme et al., 2021) com variação de distância ponta–amostra e amplitude: **576 imagens de treino e 144 de validação** (**divisão 80/20 por arquivo**); comparação de loop de treino PyTorch vs TensorFlow+Keras (Ba Alawi, 2025, seções III e IV-D).
  - **S13 (*Resultados e discussão*):** Escores da classe prevista nos 3 exemplos: CID `16268` (`89,12%` PyTorch vs `40,72%` TF), CID `19859` (`82,34%` vs `41,31%`), CID `69670` (`88,37%` vs `37,31%`); `3/3` acertos nos exemplos exibidos; **`100%` PyTorch na validação interna (144 imagens)**. **Limitação reconhecida no próprio slide:** *"Limite do teste: A divisão por arquivo pode misturar imagens da mesma pilha."* (risco clássico de *data leakage* entre imagens da mesma molécula/condição).
  - **S14 (*Considerações finais*):** *"Do piloto às amostras de grafeno"*; propõe reservar condições inteiras de simulação, treinar com dados correlatos ao **grafeno sintetizado por esfoliação eletroquímica na UFCA** e validar contra perfis manuais reservando amostras inteiras para teste; cita Shearer et al. (2016) para medição de espessura de grafeno por AFM.
  - **S15 (*Referências*):** Rosenblatt (1958, `10.1037/h0042519`), He et al. (2016, `10.1109/CVPR.2016.90`), Carracedo-Cosme et al. (2021, `10.21950/BFAU11`), Carracedo-Cosme et al. (2022, `10.1021/acs.jcim.1c01323`), Ba Alawi (2025, `10.48550/arXiv.2508.04035`), Shearer et al. (2016 — **sem DOI impresso no slide**, pendente de verificação na Missão 02), Data Science Academy (2022).

---

## 4. Linha do Tempo Evolutiva do Projeto e Matriz de Aproveitamento

```
[Fase 1: Seleção 2026]          [Fase 2: Seminário IA]          [Fase 3: IV EFAC 11-12/11/2026]        [Fase 4: Atual 16/11/2026]
pre-projeto-da-selecao.md   --> Apresentação sem título (1) --> IVEFAC333.pptx                     --> Seminários I (17/11/2026)
PPGCEM.pptx (10 slides)         (32 slides)                     (15 slides)                            PROMPT.txt / PROMPT_MESTRE.md
MEV genérico + OpenCV/          DL + PyTorch vs TF +            Piloto ResNet-18 em QUAM-AFM Lite      Estudo de VIABILIDADE científica:
Scikit-image (PDI clássico)     Grafeno/Grafite + DRX/MEV       (C6H4BrClO simulado) c/ motivação      Grafeno e relacionados via
                                                                em esfoliação eletroquímica UFCA       DRX + MEV + AFM + PDI + ML/VC
```

| Fase | Escopo Central | O que é Aproveitável para 17/11/2026 | O que NÃO Deve Ser Confundido com a Versão Atual |
|---|---|---|---|
| **1. Proposta Inicial (Seleção)** | Ferramenta open-source para microestruturas genéricas apenas em **MEV** (OpenCV/Scikit-image) | Motivação de reprodutibilidade vs análise manual; pipeline modular (pré-processamento → segmentação → extração → validação); insight *"o software é consequência"* (nota do slide 8) | Escopo genérico de metais/cerâmicas somente em MEV; cronograma e promessa de software pronto de engenharia sem estudo prévio de viabilidade em grafeno |
| **2. Rascunhos Intermediários** | Seminário comparando IA/ML/DL, PyTorch vs TensorFlow, primeiros esboços de grafeno/grafite + DRX/MEV | Transição conceitual para grafeno/grafite e motivação prática do pesquisador/técnico; escolha de PyTorch para prototipagem | Promessas de "plataforma web", "múltiplas CNNs especializadas", estimativa automática de pureza sem técnica física adequada (ex. Raman/XPS), e alegações de "validação prévia" / "datasets prontos por agentes" (slide 32) |
| **3. Estudo Piloto (IV EFAC 2026)** | Classificação de 3 isômeros $C_6H_4BrClO$ simulados (**QUAM-AFM Lite**, 576/144) com **ResNet-18** (PyTorch vs TF) | Experiência concreta do mestrando com AFM, ResNet-18 e PyTorch; vínculo real com a rota de **esfoliação eletroquímica de grafeno na UFCA**; consciência metodológica sobre **divisão por grupo/amostra** e **validação contra perfis manuais** | **100% em QUAM-AFM Lite NÃO valida caracterização de grafeno**: houve divisão 80/20 por arquivo (*data leakage* potencial) e há *domain shift* extremo entre moléculas orgânicas UHV simuladas e grafeno esfoliado real |
| **4. Proposta Atual (16/11/2026)** | Investigação científica de **viabilidade** para caracterização de grafeno e relacionados via **DRX, MEV, AFM, PDI e ML/VC** | Alinha-se exatamente aos 6 componentes e 4 critérios de Seminários I e à relação estrutura–propriedade do PPGCEM, mantendo rigor físico (técnicas não intercambiáveis) | Não apresentar como ferramenta implementada/validada; `projeto-atual.md` ainda está vazio (0 B) e precisa ser redigido após a revisão bibliográfica |

---

## 5. Separação Explícita: Verificado Empiricamente vs. Incerto / Não Testado

| Verificado Empiricamente Nesta Sessão | Incerto / Não Testado Nesta Sessão |
|---|---|
| SO Windows 10 Pro (`10.0.19045.0`), PowerShell 5.1, CPU Ryzen 3 7320U, RAM ~3,24 GiB visível (~243 MiB livres), GPU integrada AMD Radeon 610M (sem CUDA) | Conteúdo interno e pacotes instalados dentro da distribuição Ubuntu do WSL2 |
| Presença e versões exatas de `uv 0.13.7`, `python3.11.exe` (`3.11.18`, apenas `pip` + `setuptools`), `node v26.13.0`, `npm/npx 11.20.0`, `agy.exe`, stub `0.0.0.0` de `python.exe`/`python3.exe` em WindowsApps | Existência de suítes de escritório ou leitores instalados fora dos diretórios padrão verificados ou fora do `PATH` (exceto `chrome.exe`, confirmado em `Program Files\Google\Chrome`) |
| Ausência no `PATH` de `git`, `pandoc`, `quarto`, `marp`, `typst`, `pdflatex`, `xelatex`, `lualatex`, `tesseract`, `soffice`, `libreoffice`, `zotero`, `gh`, `docker`, `java`, `pip`, `pipx`, `conda`, `rg`, `grep` | Conectividade de rede em tempo real e latência atual das APIs OpenAlex, arXiv, Crossref e Semantic Scholar (não consultadas por este agente) |
| Ausência de `~/.env` e das variáveis `OPENALEX_API_KEY` e `USER_EMAIL` | Acesso institucional da UFCA (Periódicos CAPES / VPN) a textos completos pagos |
| Conteúdo completo de `config.json`, `science/plugin.json`, `science/mcp_config.json`, `google-antigravity-sdk`, 48 skills de `science`, 2 skills em `config/skills`, 14 skills built-in | Execução prática de `run_workflow` no Windows atual (prevê-se conflito com o stub `python3.exe` da WindowsApps, mas não foi disparado em teste) |
| Conteúdo integral de `Seminarios-I-Programa.pdf` (40–45 min, 6 componentes, 4 critérios de 2,5 pts), `Ciencias dos Materiais - Programa.pdf`, `pre-projeto-da-selecao.md`, `projeto-atual.md` (0 B), `PROMPT.txt`, `PROMPT_MESTRE.md` e todos os slides/notas/imagens-chave das 3 apresentações PPTX | Verificação do DOI ausente de Shearer et al. (2016) no slide 15 de `IVEFAC333.pptx` e validade bibliográfica de `arXiv:2508.04035v1` / Novac et al. (2022) (escopo do `@agente-bibliografia` / `@revisor-critico`) |
