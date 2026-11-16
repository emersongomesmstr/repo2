# Levantamento Técnico de Skills, Plugins, Servidores MCP, APIs e Ferramentas — Missão 01 (PPGCEM/UFCA)

**Data da auditoria:** 16/11/2026  
**Contexto:** Preparação de infraestrutura para pesquisa investigativa (fase de fundamentação e viabilidade — software **não** desenvolvido nem validado) sobre caracterização de grafeno e materiais relacionados via DRX, MEV, AFM, PDI e ML/VC, com apresentação de Seminários I amanhã (**17/11/2026**).  
**Autoria:** `@agente-ferramentas` (propriedade exclusiva deste documento).

---

## Sumário Executivo e Declaração de Evidência

### 1. Ambiente Real Diagnosticado (Empiricamente Verificado em 16/11/2026)

| Componente | Estado Verificado | Caminho / Versão Observada |
| :--- | :--- | :--- |
| Sistema Operacional / Shell | Ativo | Windows 10 + PowerShell 5.1 |
| Antigravity CLI (`agy`) | Ativo | `agy 1.5.9` |
| Python Gerenciado (`uv`) | Ativo | `uv 0.13.7` / `uvx 0.13.7` (`316c827e0 2026-11-03 x86_64-pc-windows-msvc`) |
| Python Local (`python3.11`) | Ativo | `C:\Users\emer\.local\bin\python3.11.exe` (`Python 3.11.18`, `sqlite3` `3.53.1` com `ENABLE_FTS5`) |
| Stubs `python` / `python3` no `PATH` | **Risco Crítico** | `where python` e `where python3` resolvem para stubs WindowsApps (`C:\Users\emer\AppData\Local\Microsoft\WindowsApps\python*.exe`) |
| Node.js / npx | Ativo | `node v26.13.0` / `npx 11.20.0` |
| Navegador Chromium | Ativo fora do `PATH` | `C:\Program Files\Google\Chrome\Application\chrome.exe` (`True`); `msedge.exe` nos caminhos padrão (`False`) |
| Arquivo `~/.env` | **Sem chaves (0 bytes)** | Inexistente no início da sessão (`False`); ao final, presente apenas como arquivo vazio (`0` bytes) com `OPENALEX_API_KEY` = `False` e `USER_EMAIL` = `False` |
| Customizações `.agents/skills` | **Ausente** | Nem no workspace nem em `~/.agents/skills` (`False`) |
| `C:\Users\emer\.gemini\config\mcp_config.json` | **Vazio** | Nenhum MCP global configurado pelo usuário |
| Binários ausentes no `PATH` | **Ausentes** | `git`, `pandoc`, `quarto`, `marp`, `typst`, `pdflatex`, `xelatex`, `lualatex`, `tesseract`, `soffice`, `zotero`, `gh`, `docker`, `java`, `pip`, `pipx`, `conda` (`NOT_FOUND`); `POWERPNT.EXE`, `LibreOffice`, `JabRef`, `Zotero`, `VS Code` ausentes nos caminhos padrão checados |

### 2. Separação Rigorosa: Testado Localmente vs. Consultado em Documentação/GitHub

| Categoria de Evidência | O que foi **Verificado Empiricamente Nesta Sessão** | O que foi **Apenas Consultado (Documentação / GitHub / Marketplace)** |
| :--- | :--- | :--- |
| **Configuração Antigravity** | Leitura direta de `config.json`, `mcp_config.json`, `skills.json`, `plugins/science/` (48 skills + 1 MCP nativo), `plugins/google-antigravity-sdk/`, `~/.gemini/config/skills/` (2 skills) e `builtin/skills/` (14 skills). | Comportamento em runtime dos plugins não instalados do Marketplace (`tavily`, `parallel`, `keenable`, `context7`, `notion`, `gslides`, `gdocs`, `gdrive`, `chrome-devtools-plugin`). |
| **Execução Efêmera (Camada 1)** | `uv run --with pymupdf4llm` (`pymupdf 2.1`, `pymupdf4llm 2.1`, 12 pacotes em cache efêmero em 829 ms); `uv run --with python-pptx` (`python-pptx 1.0.2`, 5 pacotes em 233 ms); `sqlite3` `FTS5`; `--help` de `openalex_cli.py`, `search_arxiv.py`, `europepmc_api.py` e `pubmed_api.py`. | Execução real de `Docling`, `Marker`, `Pix2Tex`, `pdfplumber`, `MarkItDown`, `rank_bm25`, `LanceDB`, `ChromaDB`, `@marp-team/marp-cli`, `Reveal.js`, `PptxGenJS`, `Typst`/`Touying`, `Quarto`, `Pandoc`, `GROBID`, `Zotero 7`, `JabRef`. |
| **Servidores MCP (GitHub)** | Inspeção local de `plugins/science/mcp_config.json` (`biomolecular_structure_viewer_mcp`). | Todos os 11 repositórios GitHub de terceiros (Zotero, arXiv, multi-base, Semantic Scholar, Docling) foram auditados via `search_web`; **nenhum** foi instalado, clonado ou conectado em runtime no `mcp_config.json`. Contagens de estrelas são aproximadas conforme captura web em 16/11/2026. |
| **APIs e Bases Científicas** | Presença dos arquivos `.licenses/` em `c:\Users\emer\dissertacao\Missao1\.licenses\` e leitura dos `SKILL.md` e cabeçalhos PEP 723 dos wrappers oficiais. | Cotas, rate limits e políticas de Semantic Scholar, Crossref, Unpaywall, Google Scholar, SciELO, CAPES/CAFe e Dimensions consultados na documentação oficial via `search_web`. |

### 3. Os 12 Critérios Obrigatórios Aplicados a Cada Ferramenta

Todas as ferramentas analisadas nas Seções 1 a 8 documentam explicitamente os **12 critérios**:
**(1)** Nome e finalidade; **(2)** Repositório e documentação oficial; **(3)** Tipo; **(4)** Compatibilidade com Antigravity; **(5)** Requisitos de instalação; **(6)** Comandos de instalação/configuração; **(7)** Dependência de APIs ou contas; **(8)** Custos e limites; **(9)** Maturidade e manutenção; **(10)** Possíveis riscos de segurança; **(11)** Vantagens sobre alternativas; **(12)** Teste simples de verificação.

---

## 1. Skills Antigravity Instaladas e Customizáveis (`.agents/skills/`)

Inventário local verificado em `C:\Users\emer\.gemini\`:
- **Plugin `science` v1.4.0** (`C:\Users\emer\.gemini\config\plugins\science\skills\`): **48 skills** no total. Releva-se que **39 delas** são voltadas à bioinformática/quimioinformática (`alphafold_*`, `alphagenome_*`, `chembl_database`, `cheminformatics_*`, `clinical_trials_database`, `clinvar_database`, `dbsnp_database`, `embl_ebi_ols`, `encode_ccres_database`, `ensembl_database`, `foldseek_structural_search`, `gnomad_database`, `gtex_database`, `human_protein_atlas_database`, `interpro_database`, `jaspar_database`, `ncbi_sequence_fetch`, `openfda_database`, `opentargets_database`, `pdb_database`, `predictingthepast`, `protein_sequence_*`, `pubchem_database`, `pymol`, `quickgo_database`, `rdkit_general`, `reactome_database`, `string_database`, `ucsc_conservation_and_tfbs`, `unibind_database`, `uniprot_database`), enquanto **9 skills** têm impacto direto na pesquisa bibliográfica, química/estrutural de apoio ou infraestrutura da Missão 01/02 (`literature_search_openalex`, `literature_search_arxiv`, `literature_search_europepmc`, `literature_search_biorxiv`, `pubmed_database`, `credentials`, `uv`, `workflow_skill_creator`, `biomolecular_structure_viewer`).
- **Plugin `google-antigravity-sdk` v0.0.9**: 1 skill (`google-antigravity-sdk`).
- **Skills globais do usuário** (`C:\Users\emer\.gemini\config\skills\`): `optimize-tokens`, `plan-token-optimization`.
- **Skills built-in** (`C:\Users\emer\.gemini\antigravity\builtin\skills\`): 14 diretórios (`agy-customizations`, `antigravity_guide`, `automation`, `generative_ui`, `mcp-app-development`, `migrate-agent-settings`, `migrate-workflows`, `native_swarm`, `permissioned-github`, `plugin`, `run-workflow`, `swarm_monitor`, `swarm_narrator`, `ui-plugin-navigation`).
- **Skills customizáveis de workspace** (`.agents/skills/<nome>/SKILL.md`): prioridade máxima na hierarquia de descoberta do Antigravity (ainda inexistentes em `Missao1`).

### 1.1 `literature-search-openalex` (`literature_search_openalex`)
1. **Nome e finalidade:** `literature-search-openalex` — consulta bibliográfica completa à base OpenAlex (artigos, autores, instituições, tópicos, citações, resolução de DOIs e download de PDFs em acesso aberto).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\SKILL.md`; código-fonte referenciado em `openalex_cli.py`: `https://github.com/google-deepmind/science-skills/tree/main/literature-search-openalex`; API docs: `https://help.openalex.org/llms.txt`.
3. **Tipo:** Skill Antigravity CLI-backed (PEP 723 + `uv`).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0). Usa `uv run <script>` com dependências declaradas (`polite-http`, `python-dotenv`), evitando conflito com o stub `python.exe` do WindowsApps.
5. **Requisitos de instalação:** Já instalada no plugin `science`; exige apenas `uv` no `PATH` (presente: `0.13.7`) e rede HTTPS.
6. **Comandos de instalação/configuração:** Já configurada. Uso obrigatório sem prefixar `python`:
   ```powershell
   uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works --search "graphene Raman XRD" --per-page 5
   ```
7. **Dependência de APIs ou contas:** Funciona sem conta/chave; `OPENALEX_API_KEY` gratuita em `~/.env` é recomendada e obrigatória para `download-pdf` via `content.openalex.org`.
8. **Custos e limites:** Sem chave: `10 req/s` e **$0.10/dia por IP compartilhado**. Com chave gratuita: `30 req/s` e **$1.00/dia**. Custos internos da API OpenAlex: `get` = grátis; `filter` = `$0.0001`; `--search`/`resolve` = `$0.001`; `download-pdf` = `$0.01`. Filtros `from_created_date`, `from_updated_date` e `to_updated_date` retornam HTTP 429 (`Plan upgrade required`) fora de plano pago. Nota: `mailto` não eleva mais limites.
9. **Maturidade e manutenção:** Alta; mantida oficialmente pelo time Google DeepMind (`science-skills` / plugin `science v1.4.0`).
10. **Possíveis riscos de segurança:** Baixo; exige criação de `.licenses/literature_search_openalex_LICENSE.txt` (já presente em `Missao1\.licenses\`) e adoção do protocolo `credentials` para não vazar `OPENALEX_API_KEY`.
11. **Vantagens sobre alternativas:** Cobertura multidisciplinar superior (~250M+ obras, forte em Ciência dos Materiais/Engenharia), resolução de IDs antes de filtrar e backoff automático contra HTTP 429.
12. **Teste simples de verificação:** **Executado localmente com sucesso** (`uv run "...\openalex_cli.py" --help`, saída exibindo subcomandos `resolve, get, download-pdf, filter, rate-limit`).

### 1.2 `literature-search-arxiv` (`literature_search_arxiv`)
1. **Nome e finalidade:** `literature-search-arxiv` — busca preprints no arXiv (`cond-mat.mtrl-sci`, `physics`, `cs.CV`), extrai metadados e baixa PDF, HTML ou fonte LaTeX (`.tar.gz`).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_arxiv\SKILL.md`; API oficial: `https://info.arxiv.org/help/api/index.html`.
3. **Tipo:** Skill Antigravity CLI-backed (`search_arxiv.py`, `download_paper.py`, `download_paper_source.py`).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0).
5. **Requisitos de instalação:** Já instalada no plugin `science`; exige `uv` (`0.13.7`).
6. **Comandos de instalação/configuração:** Já configurada:
   ```powershell
   uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_arxiv\scripts\search_arxiv.py" --query "ti:graphene AND abs:SEM" --max_results 5
   ```
7. **Dependência de APIs ou contas:** Nenhuma chave nem conta exigida (arXiv Export API pública).
8. **Custos e limites:** Gratuita; Termos de Uso exigem no máximo **1 requisição a cada 3 segundos** (aplicado automaticamente pelo `polite-http` no script: `qps=1.0/3.0`).
9. **Maturidade e manutenção:** Alta; mantida pelo Google (`science` v1.4.0).
10. **Possíveis riscos de segurança:** A extração de arquivos fonte LaTeX (`download_paper_source.py`, `.tar.gz`) exige descompactação em pasta isolada para evitar path traversal / poluição do workspace; licença `.licenses/literature_search_arxiv_LICENSE.txt` já registrada.
11. **Vantagens sobre alternativas:** Permite baixar o **código-fonte LaTeX** original (equações exatas sem erros de OCR de PDF) e não requer qualquer API key.
12. **Teste simples de verificação:** **Executado localmente com sucesso** (`uv run "...\search_arxiv.py" --help`, código de saída `0`).

### 1.3 `literature-search-europepmc` (`literature_search_europepmc`)
1. **Nome e finalidade:** `literature-search-europepmc` — busca e download de textos completos (XML JATS / texto puro / PDF por PMCID) e grafo de citações/referências em acesso aberto no Europe PMC.
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_europepmc\SKILL.md`; portal: `https://europepmc.org/` e `https://europepmc.org/searchsyntax`.
3. **Tipo:** Skill Antigravity CLI-backed (`europepmc_api.py`).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0).
5. **Requisitos de instalação:** Já instalada no plugin `science`; exige `uv`.
6. **Comandos de instalação/configuração:** Já configurada (`search`, `download_pdf`, `get_fulltext`, `get_citations`, `get_references`).
7. **Dependência de APIs ou contas:** Nenhuma conta nem chave obrigatória.
8. **Custos e limites:** Gratuita; wrapper força `OPEN_ACCESS:y` e limita a `1 req/s`.
9. **Maturidade e manutenção:** Alta (`science` v1.4.0).
10. **Possíveis riscos de segurança:** Baixo; arquivos `.licenses/literature_search_europepmc_LICENSE.txt` já presentes; saída obrigatória com `--output` reduz risco de estouro de contexto.
11. **Vantagens sobre alternativas:** Entrega XML JATS estruturado sem OCR, útil para artigos biomédicos/nanotoxicidade/biossensores de grafeno, embora tenha menor cobertura em metalurgia/DRX pura que OpenAlex.
12. **Teste simples de verificação:** **Executado localmente com sucesso** (`uv run "...\europepmc_api.py" --help`, código de saída `0`).

### 1.4 `literature-search-biorxiv` (`literature_search_biorxiv`)
1. **Nome e finalidade:** `literature-search-biorxiv` — busca por intervalo de datas ou DOI em preprints do bioRxiv e medRxiv.
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_biorxiv\SKILL.md`; API: `https://api.biorxiv.org/`.
3. **Tipo:** Skill Antigravity CLI-backed (`search_by_dates.py`, `search_by_doi.py`).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0).
5. **Requisitos de instalação:** Já instalada (`science` v1.4.0); exige `uv`.
6. **Comandos de instalação/configuração:** Já configurada. Regra crítica: jamais passar janelas longas com `--keywords` (a API não busca por palavra-chave no servidor; filtragem é local).
7. **Dependência de APIs ou contas:** Nenhuma chave exigida.
8. **Custos e limites:** Gratuita; rate limit cruzado gerenciado pelos scripts; não suporta download direto de PDF (deve encadear com `europepmc`).
9. **Maturidade e manutenção:** Alta (`science` v1.4.0).
10. **Possíveis riscos de segurança:** Baixo; risco operacional de timeout/bloqueio de IP se violar a regra de janelas curtas (1–4 semanas + `--category`).
11. **Vantagens sobre alternativas:** Útil apenas para resolução rápida de DOIs `10.1101/...`; baixa relevância para DRX/MEV/AFM de grafeno (foco em ciências da vida).
12. **Teste simples de verificação:** **Consultado localmente** via leitura integral do `SKILL.md` (não executado por baixa relevância temática ao PPGCEM).

### 1.5 `pubmed-database` (`pubmed_database`)
1. **Nome e finalidade:** `pubmed-database` — interface com NCBI E-utilities e PMC BioC APIs (busca de PMIDs, resumos, texto completo PMC, verificação ortográfica médica e *citation matching*).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\pubmed_database\SKILL.md`; políticas: `https://www.ncbi.nlm.nih.gov/home/about/policies/`.
3. **Tipo:** Skill Antigravity CLI-backed (`pubmed_api.py`).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0).
5. **Requisitos de instalação:** Já instalada (`science` v1.4.0); exige `uv` e leitura prévia das referências em `references/*.md` antes de chamar funções posicionais.
6. **Comandos de instalação/configuração:** Já configurada:
   ```powershell
   uv run "C:\Users\emer\.gemini\config\plugins\science\skills\pubmed_database\scripts\pubmed_api.py" out.json search_pubmed "graphene AFM" --max_results 5
   ```
7. **Dependência de APIs ou contas:** Funciona sem chave; recomenda `USER_EMAIL` e `NCBI_API_KEY` gratuita (`https://www.ncbi.nlm.nih.gov/account/settings/`) em `~/.env`.
8. **Custos e limites:** Gratuita; **3 req/s sem chave** e **10 req/s com `NCBI_API_KEY`**.
9. **Maturidade e manutenção:** Alta (`science` v1.4.0).
10. **Possíveis riscos de segurança:** Baixo; seguir protocolo `credentials` ao configurar `NCBI_API_KEY`/`USER_EMAIL`; criar `.licenses/pubmed_database_LICENSE.txt` no primeiro uso.
11. **Vantagens sobre alternativas:** Ótima para *raw citation matching* e intersecção grafeno–biossensores/microscopia, mas escopo primário biomédico.
12. **Teste simples de verificação:** **Testado localmente** (`uv run "...\pubmed_api.py" --help` instalou 2 pacotes em 34 ms e imprimiu a lista de 10 funções disponíveis, retornando código `1` porque o script exige `<output_file> <func>` em vez de `--help`).

### 1.6 `credentials` e `uv` (Skills de Infraestrutura do Plugin `science`)
1. **Nome e finalidade:** `credentials` (protocolo seguro de verificação e solicitação de segredos em `~/.env` sem expor valores no histórico do agente) e `uv` (verificação/configuração do gerenciador `uv` no `PATH`).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\credentials\SKILL.md` e `...\uv\SKILL.md`.
3. **Tipo:** Skills Antigravity de protocolo/instrução (instruction-only).
4. **Compatibilidade com Antigravity:** Nativas e ativas hoje (Camada 0). **Nota Windows 10:** os exemplos de `credentials` usam comandos POSIX (`grep -sq`, `read -s`), devendo ser adaptados em PowerShell 5.1 (`Select-String -Quiet` e `Read-Host -AsSecureString`).
5. **Requisitos de instalação:** Já instaladas no plugin `science`.
6. **Comandos de instalação/configuração:** Já configuradas. Verificação segura em PowerShell sem exibir segredos:
   ```powershell
   if (Test-Path "$env:USERPROFILE\.env") { Select-String -Path "$env:USERPROFILE\.env" -Pattern "^OPENALEX_API_KEY=" -Quiet } else { $false }
   ```
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuitas e sem limites.
9. **Maturidade e manutenção:** Alta (`publisher: google`).
10. **Possíveis riscos de segurança:** Mitigam exatamente o maior risco em agentes de IA: vazamento de chaves de API no contexto/transcript (`cat ~/.env`, `echo $VAR`). O snippet de instalação do `uv` na doc usa `irm ... | iex` (desnecessário aqui pois `uv 0.13.7` já está instalado).
11. **Vantagens sobre alternativas:** Padrão auditável de manuseio de credenciais que todos os scripts `science` carregam via `python-dotenv`.
12. **Teste simples de verificação:** **Verificado localmente** (`~/.env` com `0` bytes, `Select-String -Quiet` para `OPENALEX_API_KEY` e `USER_EMAIL` retornando `False`; `uv --version` = `0.13.7`).

### 1.7 `biomolecular-structure-viewer` e `rdkit-general`
1. **Nome e finalidade:** `biomolecular-structure-viewer` (visualização 3D Mol* no painel lateral de arquivos `.cif`/`.mmcif`/`.pdb`) e `rdkit-general` (depicção química 2D via RDKit, validação IUPAC e grids HTML interativos).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\skills\biomolecular_structure_viewer\SKILL.md` e `...\rdkit_general\SKILL.md`.
3. **Tipo:** Skills Antigravity (uma acoplada a MCP sidecar e outra CLI-backed via `uv run`).
4. **Compatibilidade com Antigravity:** Nativas e ativas hoje (Camada 0).
5. **Requisitos de instalação:** Já instaladas; `rdkit-general` usa PEP 723 (`uv run <script.py>`).
6. **Comandos de instalação/configuração:** Já configuradas. Regra crítica documentada em `rdkit_general`: **nunca** rodar `uv run python3 <script.py>` (pois ignora o bloco `# /// script`).
7. **Dependência de APIs ou contas:** `biomolecular-structure-viewer` opera em arquivos locais no diretório de artefatos; `rdkit_general` usa OPSIN/PubChem para verificação nomenclatural.
8. **Custos e limites:** Gratuitas. Limitação temática importante: Mol* é otimizado para biomoléculas (`.cif`/`.pdb`), **não** substitui ferramentas de cristalografia periódica de grafeno/DRX (como VESTA/pymatgen) nem análise de topografia AFM.
9. **Maturidade e manutenção:** Alta (`science` v1.4.0).
10. **Possíveis riscos de segurança:** Baixo; `biomolecular-structure-viewer` restringe carga apenas a arquivos locais na pasta de artefatos da conversa.
11. **Vantagens sobre alternativas:** Úteis em intersecções de grafeno funcionalizado/moléculas orgânicas adsorvidas (ex.: contexto QUAM-AFM com moléculas orgânicas C₆H₄BrClO), sem custo de instalação.
12. **Teste simples de verificação:** **Consultado localmente** via leitura dos `SKILL.md` e verificação de existência em `skills/`.

### 1.8 `workflow-skill-creator`, `optimize-for-tokens` e `plan-token-optimization`
1. **Nome e finalidade:** `workflow-skill-creator` (destila workflows repetíveis em novas skills com CLI + rate limiting + file-lock); `optimize-for-tokens` e `plan-token-optimization` (auditoria de arquivos >300 linhas e redução de consumo de contexto).
2. **Repositório e documentação oficial:** `...\plugins\science\skills\workflow_skill_creator\SKILL.md` e `C:\Users\emer\.gemini\config\skills\*\SKILL.md`.
3. **Tipo:** Skills de meta-autoria e otimização de contexto.
4. **Compatibilidade com Antigravity:** Ativas hoje (Camada 0); `skills.json` declara explicitamente `~/.gemini/config/skills`.
5. **Requisitos de instalação:** Já instaladas.
6. **Comandos de instalação/configuração:** Ativação automática por descrição ou menção `/nome`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuitas. Nota prática: `optimize-for-tokens` menciona `find_by_name`/`list_dir` (nomes herdáveis de outros ambientes/IDE — no conjunto atual usa-se `run_command` ou `read_file`).
9. **Maturidade e manutenção:** `workflow-skill-creator` tem especificação rigorosa (`google`); as duas skills em `~/.gemini/config/skills/` são customizações locais.
10. **Possíveis riscos de segurança:** Baixo; `workflow-skill-creator` exige confirmação de design antes de gerar código.
11. **Vantagens sobre alternativas:** Permite empacotar futuramente na Missão 02 uma skill específica do projeto (ex.: busca Crossref + geração/validação `.bib` ou auditoria de citações).
12. **Teste simples de verificação:** **Verificado localmente** via `read_file` dos três `SKILL.md` e de `C:\Users\emer\.gemini\config\skills.json`.

### 1.9 Skills Customizáveis de Workspace (`.agents/skills/`) e Built-in Relevantes
1. **Nome e finalidade:** Mecanismo nativo de skills por projeto (`.agents/skills/<nome>/SKILL.md`, além de `.agent/`, `_agents/`, `_agent/`) com descoberta progressiva e suporte a `/<nome>`; complementado pelas 14 skills built-in (destaque para `agy-customizations`, `generative_ui`, `native_swarm`, `run-workflow`, `plugin`, `automation`, `mcp-app-development`).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\antigravity\builtin\skills\agy-customizations\SKILL.md` e `docs\skills.md`.
3. **Tipo:** Arquitetura extensível nativa do Antigravity.
4. **Compatibilidade com Antigravity:** Prioridade **#1** na ordem de carregamento (acima de `skills.json`, `~/.gemini/config/` e `builtin/`). Ativável hoje criando `.agents/skills/` na raiz do projeto (não criado nesta missão por restrição de propriedade de arquivos).
5. **Requisitos de instalação:** Nenhum binário extra; apenas arquivo Markdown com frontmatter YAML (`name`, `description`) e scripts opcionais executados via `uv run`.
6. **Comandos de instalação/configuração:** Criar `.agents/skills/<skill-name>/SKILL.md` (e subpastas `scripts/`, `references/`, `resources/`).
7. **Dependência de APIs ou contas:** Nenhuma intrínseca.
8. **Custos e limites:** Gratuitas. Frontmatter exige `name` ≤ 64 caracteres (minúsculas + hifens) e `description` ≤ 1024 caracteres; *progressive disclosure* mantém o prompt enxuto até ativação.
9. **Maturidade e manutenção:** Padrão central do Antigravity `1.5.9`.
10. **Possíveis riscos de segurança:** Scripts em `.agents/skills/` rodam com as permissões do agente (`globalPermissionGrants` em `config.json` atualmente está em modo `TURBO` com `allow: ["command(*)","mcp(*)","read_file(*)","write_file(*)"]`, exigindo cuidado redobrado ao importar skills externas!).
11. **Vantagens sobre alternativas:** Permite versionar fluxos do PPGCEM (ex.: skill de verificação Crossref+OpenAlex, template de fichamento ou exportação PPTX) separados da configuração global.
12. **Teste simples de verificação:** **Verificado localmente** (`Test-Path "c:\Users\emer\dissertacao\Missao1\.agents\skills"` = `False`; leitura completa de `agy-customizations/SKILL.md` e `docs/skills.md`).

### Tabela Comparativa e Ranking Técnico — Categoria 1 (Skills)

| Posição | Skill | Escopo Principal | Pronta Hoje? | Dependência Externa | Verificação Local |
| :---: | :--- | :--- | :---: | :--- | :--- |
| **1º** | `literature_search_openalex` | Busca multidisciplinar/materiais, citações, DOIs | **Sim (Camada 0)** | Chave gratuita opcional (`OPENALEX_API_KEY`) | `--help` OK |
| **2º** | `literature_search_arxiv` | Preprints física/materiais/CV + fonte LaTeX | **Sim (Camada 0)** | Nenhuma (1 req/3s) | `--help` OK |
| **3º** | `.agents/skills/` (custom) | Fluxos específicos Missão 02 (Crossref/BibTeX/slides) | **Sim (Camada 0/1)** | Nenhuma | Hierarquia lida |
| **4º** | `credentials` + `uv` | Segurança de `~/.env` e execução Python isolada | **Sim (Camada 0)** | Nenhuma | `SKILL.md` + `uv` OK |
| **5º** | `generative_ui` | Widgets HTML interativos / visualização inline | **Sim (Camada 0)** | Nenhuma (Tailwind CDN allowlist) | `SKILL.md` lido |
| **6º** | `literature_search_europepmc` | Texto completo JATS XML OA (nanobio/biossensores) | **Sim (Camada 0)** | Nenhuma (1 req/s) | `--help` OK |
| **7º** | `pubmed_database` | E-utilities biomédico + citation matching | **Sim (Camada 0)** | `NCBI_API_KEY` opcional | `pubmed_api.py` OK |
| **8º** | `workflow_skill_creator` | Empacotamento de workflows validados em skills | **Sim (Camada 0)** | Nenhuma | `SKILL.md` lido |
| **9º** | `literature_search_biorxiv` | Preprints biologia/medicina por data/DOI | **Sim (Camada 0)** | Nenhuma | `SKILL.md` lido |

---

## 2. Plugins do Antigravity Marketplace

Verificados via `C:\Users\emer\.gemini\config\config.json` (instalados) e ferramenta `search_marketplace` (catálogo oficial/parceiros). Regra do Antigravity (`builtin/skills/plugin/SKILL.md`): plugins do Marketplace devem ser instalados/habilitados pela UI (`Customizations` ou `<plugin-card>`), **nunca** editando `config.json` manualmente.

### 2.1 `Science` (`antigravity-plugins-official/plugin/science`) — **INSTALADO (v1.4.0)**
1. **Nome e finalidade:** `Science` — pacote oficial curado com 48 skills científicas (busca bibliográfica, química, biologia) e o servidor MCP `biomolecular_structure_viewer_mcp`.
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\config\plugins\science\plugin.json`; catálogo ID `antigravity-plugins-official/plugin/science`.
3. **Tipo:** Plugin Oficial Antigravity (skills + MCP sidecar).
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0).
5. **Requisitos de instalação:** Já instalado; requer `uv` para scripts Python e `agy-node` (embutido no Antigravity) para o sidecar 3D.
6. **Comandos de instalação/configuração:** Já instalado em `C:\Users\emer\.gemini\config\plugins\science\`.
7. **Dependência de APIs ou contas:** Opcional (`OPENALEX_API_KEY`, `NCBI_API_KEY`, `USER_EMAIL` em `~/.env`).
8. **Custos e limites:** Plugin gratuito; respeita limites individuais das APIs (OpenAlex $0.10/dia sem chave, arXiv 1 req/3s, Europe PMC 1 req/s).
9. **Maturidade e manutenção:** Alta; mantido oficialmente (v1.4.0).
10. **Possíveis riscos de segurança:** Baixo; scripts inspecionáveis localmente e com controle de rate-limit/licenças.
11. **Vantagens sobre alternativas:** Zero configuração imediata e substitui vários MCPs externos de busca acadêmica com maior controle de contexto (saída em JSON para arquivo).
12. **Teste simples de verificação:** **Verificado localmente** via leitura de `config.json`, `plugin.json`, `mcp_config.json` e execução `--help` das skills de literatura.

### 2.2 `Google Antigravity SDK` (`antigravity-plugins-official/plugin/google-antigravity-sdk`) — **INSTALADO (v0.0.9)**
1. **Nome e finalidade:** `Google Antigravity SDK` — guia e exemplos para programar agentes em Python via biblioteca `google-antigravity`.
2. **Repositório e documentação oficial:** `https://github.com/google-antigravity/antigravity-sdk-python`; local: `C:\Users\emer\.gemini\config\plugins\google-antigravity-sdk\`.
3. **Tipo:** Plugin Oficial Antigravity (skill + exemplos/referências).
4. **Compatibilidade com Antigravity:** Nativo e ativo hoje (Camada 0).
5. **Requisitos de instalação:** O plugin de documentação já está ativo; usar o SDK em código próprio exigiria `pip install google-antigravity` / `uv` + chave `GEMINI_API_KEY` ou modelo local `LiteRT`.
6. **Comandos de instalação/configuração:** Plugin já ativo; pacote Python opcional: `uv run --with google-antigravity ...`.
7. **Dependência de APIs ou contas:** `GEMINI_API_KEY` (Google AI Studio) ou Vertex AI ADC para modelos hospedados; nenhum para modelos locais LiteRT.
8. **Custos e limites:** Plugin gratuito; uso externo via SDK consome cota da Gemini API.
9. **Maturidade e manutenção:** Oficial Google (`0.0.9`, licença `Apache-2.0`).
10. **Possíveis riscos de segurança:** Baixo; na Missão 01/02 é supérfluo porque a orquestração nativa (`/swarm`, `invoke_subagent`) já atende sem escrever código SDK externo.
11. **Vantagens sobre alternativas:** Útil apenas se no futuro o projeto criar um pipeline Python autônomo fora da IDE/CLI Antigravity.
12. **Teste simples de verificação:** **Verificado localmente** via leitura de `plugin.json` e `SKILL.md`.

### 2.3 `Parallel` (`antigravity-plugins-partners/plugin/parallel`)
1. **Nome e finalidade:** `Parallel` — servidor MCP hospedado para busca web ao vivo e leitura limpa de páginas web.
2. **Repositório e documentação oficial:** Marketplace ID `antigravity-plugins-partners/plugin/parallel`; docs/endpoint citados na busca web: `https://mcp.parallel.ai/v1`.
3. **Tipo:** Plugin Parceiro Antigravity (MCP remoto Streamable HTTP).
4. **Compatibilidade com Antigravity:** Compatível (Camada 2 via Marketplace ou Streamable HTTP). Não instalado hoje.
5. **Requisitos de instalação:** Instalação via Marketplace do Antigravity (UI ou CLI).
6. **Comandos de instalação/configuração:** Via UI (`<plugin-card catalog-id="antigravity-plugins-partners/plugin/parallel">`) ou CLI `agy plugin install antigravity-plugins-partners/plugin/parallel` (após aprovação do usuário).
7. **Dependência de APIs ou contas:** Segundo descrição oficial no Marketplace: **acesso gratuito sem conta Parallel, sem API key e sem CLI** (*"Free access with no Parallel account, API key, or Parallel CLI required"*).
8. **Custos e limites:** Gratuito sem chave; sujeito a limites do serviço hospedado remoto.
9. **Maturidade e manutenção:** Oficialmente listado no catálogo de parceiros do Antigravity.
10. **Possíveis riscos de segurança:** Médio (envia consultas de busca a servidor remoto de terceiros; não enviar dados confidenciais não publicados).
11. **Vantagens sobre alternativas:** Zero cadastro/API key, útil quando `search_web` nativa precisar extrair páginas de documentações ou repositórios específicos.
12. **Teste simples de verificação:** **Apenas consultado** via `search_marketplace` (não instalado).

### 2.4 `Tavily` (`antigravity-plugins-partners/plugin/tavily`)
1. **Nome e finalidade:** `Tavily` — busca web para agentes, extração limpa em Markdown, rastreamento (*crawling*), descoberta de URLs e *deep research* via MCP hospedado e skills.
2. **Repositório e documentação oficial:** Marketplace ID `antigravity-plugins-partners/plugin/tavily`; `https://tavily.com/`.
3. **Tipo:** Plugin Parceiro Antigravity (MCP remoto + skills).
4. **Compatibilidade com Antigravity:** Compatível (Camada 2 via Marketplace). Não instalado hoje.
5. **Requisitos de instalação:** Instalação pelo Marketplace + configuração de API key `tvly-...` (embora possua modo keyless limitado segundo docs Tavily).
6. **Comandos de instalação/configuração:** Instalar pelo Marketplace do Antigravity e fornecer `TAVILY_API_KEY` quando solicitado na interface de Customizations.
7. **Dependência de APIs ou contas:** Conta gratuita Tavily (*Researcher plan*) recomendada para API key estável.
8. **Custos e limites:** Plano gratuito oferece **1.000 créditos/mês** sem cartão de crédito (1 crédito busca básica; 2 créditos busca avançada).
9. **Maturidade e manutenção:** Alta; um dos provedores de busca para agentes mais consolidados.
10. **Possíveis riscos de segurança:** Médio (serviço externo hospedado + armazenamento de API key).
11. **Vantagens sobre alternativas:** Filtros por domínio (`include_domains`) permitem buscar seletivamente em portais acadêmicos (`.edu`, `sciencedirect`, `pubs.acs.org`, `arxiv.org`) sem violar ToS do Google Scholar via scraping.
12. **Teste simples de verificação:** **Apenas consultado** via `search_marketplace` e `search_web`.

### 2.5 `Keenable` (`antigravity-plugins-partners/plugin/keenable`) e `Keenable SELECT`
1. **Nome e finalidade:** `Keenable` — motor de busca focado em agentes e leitura de páginas em Markdown limpo sem cadastro; `Keenable SELECT` extrai tabelas estruturadas de múltiplas buscas (exige conta).
2. **Repositório e documentação oficial:** Marketplace IDs `antigravity-plugins-partners/plugin/keenable` e `antigravity-plugins-partners/plugin/keenable-select`.
3. **Tipo:** Plugins Parceiros Antigravity.
4. **Compatibilidade com Antigravity:** Compatível (Camada 2 via Marketplace). Não instalados hoje.
5. **Requisitos de instalação:** Instalação pelo Marketplace.
6. **Comandos de instalação/configuração:** Via UI Customizations / Marketplace (`keenable`).
7. **Dependência de APIs ou contas:** `Keenable`: **keyless** (sem signup nem API key); `Keenable SELECT`: exige login Keenable.
8. **Custos e limites:** `Keenable` gratuito keyless (limites de serviço remoto); `SELECT` depende de conta.
9. **Maturidade e manutenção:** Parceiro oficial no Marketplace.
10. **Possíveis riscos de segurança:** Médio (tráfego de consultas para infraestrutura de terceiros).
11. **Vantagens sobre alternativas:** Alternativa gratuita sem chave ao Tavily para leitura limpa de páginas web/manuais em Markdown.
12. **Teste simples de verificação:** **Apenas consultado** via `search_marketplace`.

### 2.6 `Context7` (`antigravity-plugins-partners/plugin/context7`)
1. **Nome e finalidade:** `Context7` (Upstash) — injeta documentação atualizada e exemplos por versão exata diretamente de repositórios-fonte para bibliotecas de código.
2. **Repositório e documentação oficial:** Marketplace ID `antigravity-plugins-partners/plugin/context7`; `https://context7.com/`.
3. **Tipo:** Plugin Parceiro Antigravity (MCP).
4. **Compatibilidade com Antigravity:** Compatível (Camada 2 via Marketplace). Não instalado hoje.
5. **Requisitos de instalação:** Instalação pelo Marketplace; API key gratuita recomendada ao atingir limite anônimo.
6. **Comandos de instalação/configuração:** Via Marketplace UI; chave configurável caso apareça erro `429` / cota excedida.
7. **Dependência de APIs ou contas:** Opcional (conta gratuita em `context7.com` para chave dedicada).
8. **Custos e limites:** Tier gratuito limitado a **1.000 chamadas/mês** (conforme histórico de limites consultado).
9. **Maturidade e manutenção:** Alta no ecossistema de desenvolvimento AI.
10. **Possíveis riscos de segurança:** Baixo (consulta apenas documentação pública de bibliotecas open-source).
11. **Vantagens sobre alternativas:** Muito útil na Missão 02+ caso sejam escritos scripts com `python-pptx`, `pymupdf4llm`, `scikit-image`, `PyTorch` ou `pymatgen`, evitando APIs obsoletas.
12. **Teste simples de verificação:** **Apenas consultado** via `search_marketplace` e `search_web`.

### 2.7 `Notion` (`antigravity-plugins-partners/plugin/notion`)
1. **Nome e finalidade:** `Notion` — conecta ao workspace Notion via MCP oficial + skills de pesquisa, documentação, acompanhamento e notas de reunião.
2. **Repositório e documentação oficial:** Marketplace ID `antigravity-plugins-partners/plugin/notion`.
3. **Tipo:** Plugin Parceiro Antigravity (MCP OAuth + skills).
4. **Compatibilidade com Antigravity:** Compatível (Camada 2). Não instalado hoje.
5. **Requisitos de instalação:** Instalação via Marketplace + autenticação OAuth 2.0 no navegador com conta Notion.
6. **Comandos de instalação/configuração:** Via Marketplace UI + fluxo OAuth PKCE no navegador.
7. **Dependência de APIs ou contas:** Obrigatória (conta Notion e permissões explícitas por página/database).
8. **Custos e limites:** Depende do plano Notion do usuário (Free/Plus/Education).
9. **Maturidade e manutenção:** Alta.
10. **Possíveis riscos de segurança:** Médio (concede ao agente leitura/escrita em bases pessoais do Notion se autorizado).
11. **Vantagens sobre alternativas:** Útil apenas se o pesquisador já centralizar fichamentos e cronograma da dissertação no Notion; na Missão 01, arquivos Markdown locais no repositório são mais versionáveis e auditáveis.
12. **Teste simples de verificação:** **Apenas consultado** via `search_marketplace` e `search_web`.

### 2.8 `Google Slides` / `Google Docs` / `Google Drive` (`gslides`, `gdocs`, `gdrive`)
1. **Nome e finalidade:** Plugins oficiais Google Workspace para ler, criar, editar e exportar apresentações (`gslides`), documentos (`gdocs`) e gerenciar arquivos (`gdrive`).
2. **Repositório e documentação oficial:** Marketplace IDs `antigravity-plugins-official/plugin/gslides`, `.../gdocs`, `.../gdrive`.
3. **Tipo:** Plugins Oficiais Antigravity (MCP + OAuth Google).
4. **Compatibilidade com Antigravity:** Compatíveis (Camada 2). Verificado em `list_plugin_accounts` que nenhuma conta Google de plugin está conectada hoje.
5. **Requisitos de instalação:** Instalação via Marketplace + sign-in OAuth com conta Google (ou credenciais Google Cloud ADC).
6. **Comandos de instalação/configuração:** Instalar via Marketplace UI e conectar conta na aba de contas do plugin.
7. **Dependência de APIs ou contas:** Obrigatória (conta Google / Google Workspace).
8. **Custos e limites:** Gratuitos para uso pessoal Google; sujeitos às cotas da Google Workspace API.
9. **Maturidade e manutenção:** Alta (oficiais Antigravity).
10. **Possíveis riscos de segurança:** Médio/Alto (acesso OAuth ao Google Drive do usuário exige escopo mínimo e atenção em pastas compartilhadas da UFCA/orientador).
11. **Vantagens sobre alternativas:** Notamos que `Apresentação sem título (1).pptx` no histórico parece exportação do Google Slides; `gslides` permitiria editar/exportar direto na nuvem caso o pesquisador prefira Google Slides em vez de `python-pptx`/Marp local.
12. **Teste simples de verificação:** **Consultado via `search_marketplace` e `list_plugin_accounts`** (nenhuma conta conectada localmente).

### 2.9 `Chrome DevTools` (`antigravity-plugins-official/plugin/chrome-devtools-plugin`)
1. **Nome e finalidade:** Automação confiável, depuração e inspeção de páginas no Chrome usando Chrome DevTools e Puppeteer.
2. **Repositório e documentação oficial:** Marketplace ID `antigravity-plugins-official/plugin/chrome-devtools-plugin`.
3. **Tipo:** Plugin Oficial Antigravity.
4. **Compatibilidade com Antigravity:** Compatível (Camada 2). Google Chrome está presente em `C:\Program Files\Google\Chrome\Application\chrome.exe`.
5. **Requisitos de instalação:** Instalação via Marketplace.
6. **Comandos de instalação/configuração:** Via Marketplace UI.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito.
9. **Maturidade e manutenção:** Oficial Antigravity.
10. **Possíveis riscos de segurança:** Médio (automação de navegador local e acesso a sessões/DOM; não usar para contornar anti-bot/CAPTCHA).
11. **Vantagens sobre alternativas:** Útil na Missão 02 para validar visualmente slides em **Reveal.js** / HTML ou inspecionar exportação PDF/layout no Chrome real instalado.
12. **Teste simples de verificação:** **Consultado** via `search_marketplace`; presença do `chrome.exe` **verificada localmente**.

### Tabela Comparativa e Ranking Técnico — Categoria 2 (Plugins Marketplace)

| Posição | Plugin (ID) | Status Atual | Chave / Conta? | Relevância Missão 01/02 |
| :---: | :--- | :--- | :--- | :--- |
| **1º** | `antigravity-plugins-official/plugin/science` | **Instalado (v1.4.0)** | Opcional (`~/.env`) | **Crítica** (OpenAlex, arXiv, Europe PMC, credentials, uv) |
| **2º** | `antigravity-plugins-partners/plugin/context7` | Não instalado | Opcional (1k/mês grátis) | **Alta (Missão 02+)** para código PDI/ML/slides |
| **3º** | `antigravity-plugins-partners/plugin/parallel` | Não instalado | **Não (grátis/keyless)** | **Média-Alta** para busca/leitura web limpa |
| **4º** | `antigravity-plugins-partners/plugin/tavily` | Não instalado | Opcional/Grátis (1k/mês) | **Média-Alta** (busca por domínio acadêmico) |
| **5º** | `antigravity-plugins-partners/plugin/keenable` | Não instalado | **Não (keyless)** | **Média** (alternativa web limpa ao Parallel) |
| **6º** | `antigravity-plugins-official/plugin/gslides` | Não instalado | Sim (OAuth Google) | **Média** (se optar por Google Slides na Missão 02) |
| **7º** | `antigravity-plugins-official/plugin/chrome-devtools-plugin` | Não instalado | Não | **Média** (inspeção visual de slides HTML/Reveal.js) |
| **8º** | `antigravity-plugins-official/plugin/google-antigravity-sdk` | **Instalado (v0.0.9)** | Gemini API se usado | **Baixa** (desnecessário frente ao `/swarm` nativo) |
| **9º** | `antigravity-plugins-partners/plugin/notion` | Não instalado | Sim (OAuth Notion) | **Baixa** (opcional apenas se usar Notion) |

---

## 3. Servidores MCP e Compatibilidade com Antigravity

**Regra de Compatibilidade Antigravity (`agy-customizations/docs/mcp_servers.md`):**
- Arquivo global: `C:\Users\emer\.gemini\config\mcp_config.json` (atualmente vazio nesta máquina).
- Transportes aceitos: **Stdio** (`"command"`, `"args"`, `"env"`) e **Streamable HTTP** (`"url"`, ex.: `.../mcp`). O transporte legado HTTP+SSE (`/sse`, spec 2024-11-05) **não** é suportado diretamente (exige bridge como `mcp-remote`).
- **Armadilha Windows 10 deste ambiente:** Nunca configurar `"command": "python"` ou `"command": "python3"` no `mcp_config.json`, pois ambos apontam para os stubs do WindowsApps! Deve-se usar `"uvx"`, `"npx"` ou o caminho explícito `"C:\\Users\\emer\\.local\\bin\\python3.11.exe"`.

### 3.1 `science_biomolecular_structure_viewer_mcp` (Nativo Instalado)
1. **Nome e finalidade:** `biomolecular_structure_viewer_mcp` (exposto como `science_biomolecular_structure_viewer_mcp`) — renderizador 3D Mol* em painel lateral para estruturas `.cif`, `.mmcif` e `.pdb`, com anotações e seleções de resíduos.
2. **Repositório e documentação oficial:** Local em `C:\Users\emer\.gemini\config\plugins\science\mcp_config.json` e `skills\biomolecular_structure_viewer\SKILL.md`.
3. **Tipo:** MCP Server Stdio embutido em plugin + UI Sidecar.
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0), executada via `agy-node sidecars/biomolecular_structure_viewer/dist/mcp_entry.cjs`.
5. **Requisitos de instalação:** Já instalado com o plugin `science`.
6. **Comandos de instalação/configuração:** Pré-configurado no plugin.
7. **Dependência de APIs ou contas:** Nenhuma; aceita apenas arquivos locais na pasta de artefatos da conversa.
8. **Custos e limites:** Gratuito; restrito a formatos biomoleculares/cristalográficos suportados por Mol* (`.cif`/`.pdb`), sem suporte a imagens MEV/AFM ou difratogramas DRX.
9. **Maturidade e manutenção:** Alta (oficial Antigravity/Google).
10. **Possíveis riscos de segurança:** Muito baixo (lê apenas arquivos copiados para o diretório de artefatos da conversa).
11. **Vantagens sobre alternativas:** Já instalado, sem dependência de Python/Node externos.
12. **Teste simples de verificação:** **Verificado localmente** via leitura de `plugins/science/mcp_config.json` e `SKILL.md`.

### 3.2 `oscardvs/zoteus` (Zotero MCP — Local-First)
1. **Nome e finalidade:** `zoteus` (`@oscardvs/zoteus`) — servidor MCP TypeScript local-first para Zotero 7 (leitura de PDFs completos, buscas salvas, citações CSL via `citeproc-js`, busca semântica e anotações/highlights com reconstrução de coordenadas PDF).
2. **Repositório e documentação oficial:** `https://github.com/oscardvs/zoteus` (pacote npm `@oscardvs/zoteus`).
3. **Tipo:** MCP Server Stdio (Node.js/TypeScript).
4. **Compatibilidade com Antigravity:** Compatível via Stdio (`"command": "npx"`, `"args": ["-y", "@oscardvs/zoteus"]`), porém **bloqueado hoje** porque `zotero.exe` não está instalado.
5. **Requisitos de instalação:** Node.js `>= 20.19` (presente: `v26.13.0`), `npx` (presente: `11.20.0`), **Zotero 7 Desktop instalado e em execução** com API local habilitada (e opcionalmente Web API para grupos/escritas).
6. **Comandos de instalação/configuração:** `npx -y @oscardvs/zoteus` (efêmero via Node quando Zotero 7 estiver instalado).
7. **Dependência de APIs ou contas:** Local API do Zotero 7 para leituras; Web API key opcional para sincronização/grupos.
8. **Custos e limites:** Gratuito (MIT); acoplado ao Zotero 7 aberto na máquina.
9. **Maturidade e manutenção:** ~61+ estrelas (consulta web); projeto ativo de 2025–2026 com escopo avançado, sujeito a complexidade de manutenção por ser projeto independente.
10. **Possíveis riscos de segurança:** Médio: realiza **escritas** na biblioteca Zotero (tags, coleções, anotações, adição de itens) e executa código remoto via `npx -y` se não fixar versão.
11. **Vantagens sobre alternativas:** Arquitetura local-first que evita dependência constante da nuvem Zotero e inclui formatação CSL nativa (`citeproc-js`) e mapeamento preciso de trechos em PDF.
12. **Teste simples de verificação:** **Apenas consultado** na web/GitHub (não testado porque Zotero Desktop está ausente).

### 3.3 `cookjohn/zotero-mcp` (Plugin Zotero 7 + MCP)
1. **Nome e finalidade:** `cookjohn/zotero-mcp` — servidor MCP embutido diretamente como plugin `.xpi` dentro do próprio Zotero 7, expondo busca, metadados, texto completo e anotações via API interna JS do Zotero.
2. **Repositório e documentação oficial:** `https://github.com/cookjohn/zotero-mcp`.
3. **Tipo:** Plugin Zotero (`.xpi`) + Servidor MCP (Streamable HTTP na porta `23120` ou bridge Node `stdio`).
4. **Compatibilidade com Antigravity:** Compatível via Streamable HTTP (`"url": "http://127.0.0.1:23120/mcp"`) ou Stdio Node, mas **indisponível hoje** pela ausência do Zotero 7.
5. **Requisitos de instalação:** Zotero `7.0+` Desktop instalado; Node `18+` e `git`/`npm` apenas se compilar do código-fonte (usuário final usa o `.xpi` das Releases).
6. **Comandos de instalação/configuração:** Instalar `.xpi` em `Zotero > Tools > Plugins`, habilitar servidor nas preferências e apontar `mcp_config.json` para `http://127.0.0.1:23120/mcp`.
7. **Dependência de APIs ou contas:** Nenhuma API key externa exigida para uso local.
8. **Custos e limites:** Gratuito (open-source, ~2.7k estrelas — consulta web); funciona apenas enquanto Zotero 7 Desktop estiver aberto.
9. **Maturidade e manutenção:** Alta popularidade (~2.7k estrelas), porém frágil a atualizações internas do Zotero 7/8 por depender do contexto JS interno de extensões.
10. **Possíveis riscos de segurança:** Médio: abre servidor HTTP local na porta `23120` (`127.0.0.1`) com acesso de leitura/escrita ao banco Zotero local; baixar `.xpi` apenas de releases oficiais verificadas.
11. **Vantagens sobre alternativas:** Mais popular da categoria e dispensa gerenciar Web API key ou runtime Python externo para uso básico.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (Zotero 7 ausente).

### 3.4 `kaliaboi/mcp-zotero`
1. **Nome e finalidade:** `mcp-zotero` (`kaliaboi`) — conector minimalista em TypeScript para consultar a biblioteca Zotero na nuvem (`get_collections`, `get_collection_items`, `get_item_details`, `search_library`, `get_recent`).
2. **Repositório e documentação oficial:** `https://github.com/kaliaboi/mcp-zotero` (npm: `mcp-zotero`).
3. **Tipo:** MCP Server Stdio (Node.js).
4. **Compatibilidade com Antigravity:** Compatível via Stdio (`"command": "npx"`, `"args": ["mcp-zotero"]`).
5. **Requisitos de instalação:** Node.js (presente `v26.13.0`), conta Zotero sincronizada na nuvem (`zotero.org`).
6. **Comandos de instalação/configuração:** Bloco `mcp_config.json` com `ZOTERO_API_KEY` e `ZOTERO_USER_ID` em `"env"`.
7. **Dependência de APIs ou contas:** Obrigatória: conta Zotero Cloud + Web API Key + User ID numérico.
8. **Custos e limites:** Gratuito (MIT, ~164 estrelas — consulta web); sujeito ao limite de armazenamento gratuito da nuvem Zotero (300 MB para anexos) e rate limits da Web API.
9. **Maturidade e manutenção:** Moderada; wrapper simples e enxuto, mas sem recursos avançados de PDF local/anotações profundas.
10. **Possíveis riscos de segurança:** Baixo/Médio (requer armazenar `ZOTERO_API_KEY` na configuração; preferir chave read-only se não precisar escrever).
11. **Vantagens sobre alternativas:** Único que **não** exige o Zotero Desktop rodando localmente (opera 100% via nuvem Zotero).
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 3.5 `Xevos117/mcp-zotero`
1. **Nome e finalidade:** `@xevos117/mcp-zotero` — servidor MCP em Node focado em automação via Zotero Web API, adição de itens por DOI, descoberta automática de PDF via Unpaywall e injeção de citações com códigos de campo nativos do Zotero em documentos Word (`.docx`).
2. **Repositório e documentação oficial:** `https://github.com/Xevos117/mcp-zotero` (npm: `@xevos117/mcp-zotero`).
3. **Tipo:** MCP Server Stdio (Node.js / pacote `.mcpb`).
4. **Compatibilidade com Antigravity:** Compatível via Stdio (`npx @xevos117/mcp-zotero`).
5. **Requisitos de instalação:** Node.js + conta Zotero Web API + User ID.
6. **Comandos de instalação/configuração:** Invocação via `npx @xevos117/mcp-zotero` com variáveis `ZOTERO_API_KEY` e `ZOTERO_USER_ID`.
7. **Dependência de APIs ou contas:** Zotero Web API Key + User ID (e consultas Unpaywall para PDFs OA).
8. **Custos e limites:** Gratuito (MIT, ~37 estrelas — consulta web); limitado pelas cotas da nuvem Zotero.
9. **Maturidade e manutenção:** Nicho/experimental (~37 estrelas); alta superfície de complexidade por manipular códigos XML `.docx`.
10. **Possíveis riscos de segurança:** Médio (escrita na biblioteca Zotero + geração/injeção em `.docx` + escopo amplo de Web API key).
11. **Vantagens sobre alternativas:** Diferencial exclusivo de gerar `.docx` já com field codes Zotero atualizáveis no Microsoft Word (útil somente se redigir dissertação no Word com Zotero).
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 3.6 `danielostrow/zotero-mcp-server`
1. **Nome e finalidade:** `danielostrow/zotero-mcp-server` — servidor MCP Node.js enxuto para pesquisar, citar e gerenciar referências via Zotero Web API.
2. **Repositório e documentação oficial:** `https://github.com/danielostrow/zotero-mcp-server`.
3. **Tipo:** MCP Server Stdio (Node.js).
4. **Compatibilidade com Antigravity:** Compatível via Stdio, porém exige build manual do repositório (`git` e `npm`), e `git` está ausente hoje.
5. **Requisitos de instalação:** Node.js `>= 20.16.0` (presente `v26.13.0`), `git` (ausente), `npm`, conta Zotero Web API.
6. **Comandos de instalação/configuração:** `git clone ... && npm install && npm run build` + `.env` com `ZOTERO_API_KEY` e `ZOTERO_USER_ID` (ou `ZOTERO_GROUP_ID`).
7. **Dependência de APIs ou contas:** Obrigatória: Zotero Web API Key + User/Group ID.
8. **Custos e limites:** Gratuito (open-source, projeto recente de início de 2026 com baixa adoção frente a `cookjohn`/`oscardvs`/`kaliaboi`).
9. **Maturidade e manutenção:** Inicial/comunitária; histórico documenta alto volume de dúvidas de configuração manual.
10. **Possíveis riscos de segurança:** Baixo/Médio (mesmos riscos de chave Web API do Zotero + dependência de build local).
11. **Vantagens sobre alternativas:** Suporte explícito a `ZOTERO_GROUP_ID` para bibliotecas compartilhadas em grupo de pesquisa, porém sem diferencial frente a `kaliaboi` (que roda direto via `npx`) ou `oscardvs/zoteus`.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

*(Nota comparativa: na comunidade Python também existe `54yyyu/zotero-mcp`, instalável via `uv`/`pip`, com suporte híbrido Web API + Local API e busca semântica; igualmente dependente de usuário Zotero ativo.)*

### 3.7 `blazickjp/arxiv-mcp-server`
1. **Nome e finalidade:** `arxiv-mcp-server` (`blazickjp`) — servidor MCP Python para revisão bibliográfica no arXiv: busca, armazenamento local de artigos em disco, leitura das seções LaTeX originais e geração de BibTeX.
2. **Repositório e documentação oficial:** `https://github.com/blazickjp/arxiv-mcp-server`.
3. **Tipo:** MCP Server Stdio (Python via `uvx`).
4. **Compatibilidade com Antigravity:** Totalmente compatível via Stdio (`"command": "uvx"`, `"args": ["arxiv-mcp-server", "--storage-path", "C:\\..."]`), sem conflito com stub WindowsApps.
5. **Requisitos de instalação:** `uv`/`uvx` (`0.13.7` presente hoje) e Python `>= 3.10` (`3.11.18` presente).
6. **Comandos de instalação/configuração:** Execução efêmera via `uvx arxiv-mcp-server` ou declaração em `mcp_config.json` usando `ARXIV_STORAGE_PATH` / `--storage-path` com barras escapadas no Windows.
7. **Dependência de APIs ou contas:** Nenhuma conta nem API key (usa API pública do arXiv).
8. **Custos e limites:** Gratuito (`Apache-2.0`, ~1.2k+ estrelas); sujeito ao limite do arXiv (`1 req/3s`).
9. **Maturidade e manutenção:** **Alta** — atualização recente verificada (`v0.8.2` em 08/10/2026).
10. **Possíveis riscos de segurança:** Baixo; baixa arquivos locais em `--storage-path` e executa pacote PyPI de terceiros via `uvx` (recomendável fixar versão em produção).
11. **Vantagens sobre alternativas:** Muito mais maduro que `AnnaSuSu/arxiv-mcp` e extrai seções LaTeX originais + BibTeX. Entretanto, para este ambiente, a skill nativa `literature_search_arxiv` já cobre arXiv sem abrir servidor MCP extra.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (não executado via `uvx`).

### 3.8 `AnnaSuSu/arxiv-mcp`
1. **Nome e finalidade:** `AnnaSuSu/arxiv-mcp` — servidor MCP simples em Python para buscar e baixar artigos do arXiv.
2. **Repositório e documentação oficial:** `https://github.com/AnnaSuSu/arxiv-mcp` (também referenciado como `arxiv-paper-mcp-server` no PyPI).
3. **Tipo:** MCP Server Stdio (Python).
4. **Compatibilidade com Antigravity:** Compatível em tese via Stdio (`uv run`), mas exige `git clone` na instrução oficial de dev (`git` ausente hoje).
5. **Requisitos de instalação:** Python `3.10+`, pacote `mcp`, `uv` ou `git`.
6. **Comandos de instalação/configuração:** `git clone https://github.com/AnnaSuSu/arxiv-mcp.git && uv sync && uv run arxiv-mcp-server`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (`MIT`, ~1 estrela — consulta web).
9. **Maturidade e manutenção:** **Baixa/estagnada** — último desenvolvimento relevante por volta de meados de 2025, apenas ~1 estrela.
10. **Possíveis riscos de segurança:** Baixo impacto direto, porém código pouco auditado pela comunidade devido à baixíssima adoção.
11. **Vantagens sobre alternativas:** Nenhuma vantagem prática frente a `blazickjp/arxiv-mcp-server` ou à skill nativa `literature_search_arxiv`.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 3.9 `openags/paper-search-mcp`
1. **Nome e finalidade:** `paper-search-mcp` (`openags`) — servidor MCP e CLI multi-base que busca, deduplica, baixa e extrai texto de PDFs em **20+ fontes** (arXiv, PubMed, PMC, OpenAlex, Crossref, Semantic Scholar, bioRxiv, medRxiv, Unpaywall, CORE, Europe PMC, DOAJ, dblp, OpenAIRE, Zenodo, SSRN, além de conectores opcionais para Google Scholar e Sci-Hub).
2. **Repositório e documentação oficial:** `https://github.com/openags/paper-search-mcp` (PyPI: `paper-search-mcp` / `paper-search-cli`).
3. **Tipo:** MCP Server (Stdio, SSE ou Streamable HTTP) + CLI.
4. **Compatibilidade com Antigravity:** Compatível via Stdio (`"command": "uvx"`, `"args": ["paper-search-mcp"]`) ou Streamable HTTP local (`127.0.0.1`). Não usar transporte `sse`.
5. **Requisitos de instalação:** `uv`/`uvx` (`0.13.7` presente) e Python `>= 3.10`.
6. **Comandos de instalação/configuração:** `uvx paper-search-mcp` (MCP) ou `uv run --with paper-search-cli ...`. Variáveis opcionais: `PAPER_SEARCH_UNPAYWALL_EMAIL`, `PAPER_SEARCH_SEMANTIC_SCHOLAR_API_KEY`, `PAPER_SEARCH_CORE_API_KEY`.
7. **Dependência de APIs ou contas:** Todas as chaves são opcionais, mas recomendadas para estabilidade (Unpaywall exige e-mail válido).
8. **Custos e limites:** Gratuito (`MIT`, ~2.7k–3.1k estrelas); sujeito aos rate limits de cada fonte consultada.
9. **Maturidade e manutenção:** Alta e ativa em 2026 (publicação automatizada no PyPI).
10. **Possíveis riscos de segurança e conformidade (ATENÇÃO):** **Alto risco regulatório/ToS se usado sem restrição** — inclui cadeia de fallback opcional envolvendo **Sci-Hub** (direitos autorais / risco legal-institucional em dissertação pública) e **Google Scholar** (risco de CAPTCHA/bloqueio de IP da rede UFCA/residencial). Além disso, injetar texto completo extraído direto no contexto do MCP consome tokens rapidamente.
11. **Vantagens sobre alternativas:** Centraliza mais de 20 bases (inclusive Crossref, Semantic Scholar e Unpaywall) em um único servidor MCP, cobrindo lacunas que o plugin `science` nativo ainda não traz (Crossref/Semantic Scholar/Unpaywall).
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (não executado para evitar baixar pacotes de terceiros não auditados nesta missão).

### 3.10 `zongmin-yu/semantic-scholar-fastmcp-mcp-server`
1. **Nome e finalidade:** Servidor MCP Python baseado em **FastMCP** para a API do Semantic Scholar: busca avançada com filtros (ano, citações), recuperação em lote (até 1.000 IDs), grafos de citações/referências, perfis de autores e recomendações baseadas em múltiplos artigos (exemplos positivos e negativos).
2. **Repositório e documentação oficial:** `https://github.com/zongmin-yu/semantic-scholar-fastmcp-mcp-server`.
3. **Tipo:** MCP Server Stdio (Python / FastMCP).
4. **Compatibilidade com Antigravity:** Compatível via `uvx` ou `C:\Users\emer\.local\bin\python3.11.exe` em `mcp_config.json` (Stdio).
5. **Requisitos de instalação:** `uv`/`uvx` (ou `pip` + `fastmcp`, `httpx`/`requests`, `semanticscholar`); sem necessidade de Node/Docker.
6. **Comandos de instalação/configuração:**
   ```json
   { "command": "uvx", "args": ["semantic-scholar-fastmcp-mcp-server"], "env": { "SEMANTIC_SCHOLAR_API_KEY": "..." } }
   ```
7. **Dependência de APIs ou contas:** Funciona sem chave (pool público instável), mas recomenda fortemente `SEMANTIC_SCHOLAR_API_KEY` gratuita.
8. **Custos e limites:** Gratuito (`MIT`, ~100–166 estrelas); respeita `1 req/s` dedicado com chave ou pool anônimo compartilhado de 1.000 req/s (sujeito a HTTP 429).
9. **Maturidade e manutenção:** Moderada/Boa; arquitetura modular em FastMCP superior à versão básica de `JackKuo666`.
10. **Possíveis riscos de segurança:** Baixo/Médio (execução de pacote comunitário via `uvx` e guarda da chave `SEMANTIC_SCHOLAR_API_KEY`).
11. **Vantagens sobre alternativas:** Operações em lote (até 1.000 papers) e recomendações por exemplos positivos/negativos são excelentes para descoberta de estado da arte em grafeno + ML/VC.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 3.11 `JackKuo666/semanticscholar-MCP-Server`
1. **Nome e finalidade:** Servidor MCP Python minimalista com 4 ferramentas para Semantic Scholar (`search_semantic_scholar`, `get_semantic_scholar_paper_details`, `get_semantic_scholar_author_details`, `get_semantic_scholar_citations_and_references`).
2. **Repositório e documentação oficial:** `https://github.com/JackKuo666/semanticscholar-MCP-Server`.
3. **Tipo:** MCP Server Stdio (Python).
4. **Compatibilidade com Antigravity:** Compatível via Stdio usando `C:\Users\emer\.local\bin\python3.11.exe` (ou `uv run --with semanticscholar --with mcp ...`).
5. **Requisitos de instalação:** Python + bibliotecas `semanticscholar` e `mcp` (ou `git` para clonar).
6. **Comandos de instalação/configuração:** Instalação via `pip`/Smithery ou execução do script Python em `mcp_config.json`.
7. **Dependência de APIs ou contas:** Semantic Scholar API (chave opcional).
8. **Custos e limites:** Gratuito (`MIT`, ~87 estrelas).
9. **Maturidade e manutenção:** Básica/simples (menos recursos que `zongmin-yu`).
10. **Possíveis riscos de segurança:** Baixo/Médio (código comunitário; evitar instaladores automáticos Smithery que alteram configs sem revisão).
11. **Vantagens sobre alternativas:** Código pequeno e fácil de auditar antes de usar, embora inferior em recursos ao `zongmin-yu/semantic-scholar-fastmcp-mcp-server`.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 3.12 `docling-project/docling-mcp`
1. **Nome e finalidade:** Servidor MCP oficial do projeto **Docling** (IBM Research / LF AI & Data) que expõe conversão agêntica de PDF, DOCX, PPTX e imagens para Markdown/JSON estruturado (layout + tabelas) com cache em disco.
2. **Repositório e documentação oficial:** `https://github.com/docling-project/docling-mcp` e `https://docling-project.github.io/docling-mcp/`.
3. **Tipo:** MCP Server Stdio ou remoto via `docling-serve` (Python).
4. **Compatibilidade com Antigravity:** Compatível com Windows 10 via `uvx --from=docling-mcp docling-mcp-server`, porém **inviável/desaconselhado hoje (16/11)** no modo local por peso computacional.
5. **Requisitos de instalação:** `uv`/`uvx` (`0.13.7` presente). Modo `docling-mcp[local]` baixa modelos de layout/OCR (`RT-DETR`/DocLayNet, `TableFormer`, `RapidOCR`/`EasyOCR`) que exigem **~10–20 GB de disco** e idealmente 16 GB+ de RAM ou GPU CUDA; modo remoto exige instância `docling-serve`.
6. **Comandos de instalação/configuração:**
   ```json
   { "command": "uvx", "args": ["--from=docling-mcp", "docling-mcp-server"] }
   ```
7. **Dependência de APIs ou contas:** Nenhuma no modo local; requer URL de servidor próprio no modo remoto.
8. **Custos e limites:** Gratuito (`MIT`, ~790–800+ estrelas no `docling-mcp`, >70k no `docling`). Limite prático é tempo de download/RAM/CPU no Windows.
9. **Maturidade e manutenção:** **Muito Alta** (projeto oficial IBM / LF AI & Data).
10. **Possíveis riscos de segurança:** Baixo (processamento 100% local de PDFs sem enviar artigos para nuvem de terceiros).
11. **Vantagens sobre alternativas:** Melhor precisão estrutural aberta para tabelas complexas e PDFs multi-coluna, mas excessivo para uso emergencial antes da apresentação de amanhã quando `pymupdf4llm` já resolve em <1 segundo.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (não baixado para não consumir GBs de cache hoje).

### Tabela Comparativa e Ranking Técnico — Categoria 3 (Servidores MCP)

| Posição | Servidor MCP | Runtime / Transporte | Zotero/Conta Exigida? | Risco / Peso | Recomendação |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1º** | `science_biomolecular_structure_viewer_mcp` | `agy-node` / Stdio (Plugin) | Não | Baixíssimo | **Já ativo** (uso limitado a `.cif`/`.pdb`) |
| **2º** | `zongmin-yu/semantic-scholar-fastmcp-mcp-server` | `uvx` / Stdio | Chave gratuita recomendada | Baixo/Médio | **Top Camada 2** se precisar grafos/recomendações S2 |
| **3º** | `blazickjp/arxiv-mcp-server` | `uvx` / Stdio | Não | Baixo | Bom na Camada 2, mas **redundante** com skill `science` |
| **4º** | `docling-project/docling-mcp` | `uvx` / Stdio | Não | Pesado (10–20 GB local) | **Top Camada 2 (Pós-Seminário)** para parsing pesado |
| **5º** | `oscardvs/zoteus` | `npx` / Stdio | Sim (Zotero 7 local) | Médio (escritas locais) | **Melhor MCP Zotero** quando Zotero 7 for instalado |
| **6º** | `cookjohn/zotero-mcp` | `.xpi` + Streamable HTTP | Sim (Zotero 7 local) | Médio (porta local) | Excelente alternativa Zotero 7 na Camada 2 |
| **7º** | `openags/paper-search-mcp` | `uvx` / Stdio | Opcional | **Alto (Sci-Hub/Scholar)** | Usar só se desabilitar Sci-Hub/Google Scholar |
| **8º** | `kaliaboi/mcp-zotero` | `npx` / Stdio | Sim (Zotero Cloud API) | Baixo/Médio | Melhor opção caso use Zotero apenas na nuvem |
| **9º** | `JackKuo666/semanticscholar-MCP-Server` | Python / Stdio | Chave opcional | Baixo/Médio | Básico; superado por `zongmin-yu` |
| **10º** | `Xevos117/mcp-zotero` | `npx` / Stdio | Sim (Zotero Cloud API) | Médio | Relevante só para fluxo Word `.docx` |
| **11º** | `danielostrow/zotero-mcp-server` | Node / Stdio | Sim (Zotero Cloud API) | Médio (`git` ausente) | Sem diferencial prático |
| **12º** | `AnnaSuSu/arxiv-mcp` | Python / Stdio | Não | Baixo (estagnado 2025) | **Descartado** frente a `blazickjp` e skill nativa |

---

## 4. Bases e APIs de Pesquisa Acadêmica

### 4.1 OpenAlex API
1. **Nome e finalidade:** OpenAlex — grafo bibliográfico aberto com ~250M+ trabalhos, autores, instituições, conceitos, citações e links de acesso aberto.
2. **Repositório e documentação oficial:** `https://openalex.org/` e `https://docs.openalex.org/` (`https://help.openalex.org/llms.txt`).
3. **Tipo:** API REST JSON aberta (consumida nativamente pela skill `literature_search_openalex`).
4. **Compatibilidade com Antigravity:** Nativa hoje via `openalex_cli.py` (Camada 0).
5. **Requisitos de instalação:** Zero instalação adicional (`uv run` no plugin `science`).
6. **Comandos de instalação/configuração:** Já pronta em `openalex_cli.py`; adicionar `OPENALEX_API_KEY` em `~/.env` na Camada 2.
7. **Dependência de APIs ou contas:** Funciona sem chave; conta gratuita gera `OPENALEX_API_KEY`.
8. **Custos e limites:** Sem chave: `10 req/s` e **$0.10/dia por IP**; com chave gratuita: `30 req/s` e **$1.00/dia**. `get` é grátis; `filter` custa `$0.0001`; `--search`/`resolve` custa `$0.001`; `download-pdf` custa `$0.01` e exige chave.
9. **Maturidade e manutenção:** Altíssima (mantida pela OurResearch).
10. **Possíveis riscos de segurança:** Baixo; risco apenas de esgotar o orçamento diário de `$0.10/IP` sem chave ou tentar filtros pagos (`from_*_date`) gerando HTTP 429.
11. **Vantagens sobre alternativas:** Melhor cobertura multidisciplinar aberta em Física, Ciência dos Materiais, Química, Engenharia e Visão Computacional com suporte a DOIs, filtros booleanos e contagem de citações.
12. **Teste simples de verificação:** CLI verificada localmente (`openalex_cli.py --help` OK; modelo de limites confirmado no `SKILL.md`).

### 4.2 Crossref REST API
1. **Nome e finalidade:** Crossref — registro oficial de DOIs para periódicos e conferências (IEEE, Elsevier, Springer, ACS, IOP, etc.), metadados autorais e geração direta de BibTeX.
2. **Repositório e documentação oficial:** `https://api.crossref.org/` e `https://www.crossref.org/documentation/retrieve-metadata/rest-api/`.
3. **Tipo:** API REST JSON + negociação de conteúdo (`application/x-bibtex`).
4. **Compatibilidade com Antigravity:** Alta via Python stdlib (`C:\Users\emer\.local\bin\python3.11.exe` com `urllib.request`) sem instalar nada (Camada 0).
5. **Requisitos de instalação:** Nenhum.
6. **Comandos de instalação/configuração:** Consultar `https://api.crossref.org/works/{doi}?mailto=seu@email` ou `https://api.crossref.org/works/{doi}/transform/application/x-bibtex`.
7. **Dependência de APIs ou contas:** Nenhuma chave obrigatória; identificar `mailto` coloca no **Polite Pool**.
8. **Custos e limites:** Pública e gratuita. **Public Pool (anônimo):** `5 req/s` registro único, `1 req/s` listas, concorrência 1. **Polite Pool (`mailto`):** `10 req/s` registro único, `3 req/s` listas, concorrência 3–5. Tier pago *Metadata Plus* >150 req/s.
9. **Maturidade e manutenção:** Altíssima (infraestrutura central de DOIs científicos).
10. **Possíveis riscos de segurança:** Baixo; não traz resumos completos para todas as editoras (algumas omitem `abstract`), exigindo cruzamento com OpenAlex/Semantic Scholar.
11. **Vantagens sobre alternativas:** **Fonte da verdade** para validar se um DOI existe e gerar `.bib` exato sem alucinação de páginas/volume/ano.
12. **Teste simples de verificação:** **Apenas consultado** na documentação nesta sessão (verificação real de DOIs conduzida em paralelo pelo `@agente-bibliografia`).

### 4.3 arXiv API
1. **Nome e finalidade:** arXiv Export API — acesso a preprints de física de materiais (`cond-mat.mtrl-sci`), física aplicada, visão computacional (`cs.CV`) e ML, incluindo PDFs e fontes LaTeX.
2. **Repositório e documentação oficial:** `https://info.arxiv.org/help/api/index.html`.
3. **Tipo:** API HTTP/Atom XML (consumida nativamente pela skill `literature_search_arxiv`).
4. **Compatibilidade com Antigravity:** Nativa hoje via `search_arxiv.py` (Camada 0).
5. **Requisitos de instalação:** Nenhum adicional.
6. **Comandos de instalação/configuração:** Usar `uv run "...\search_arxiv.py"`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuita; máximo **1 requisição a cada 3 segundos**.
9. **Maturidade e manutenção:** Altíssima (Cornell University).
10. **Possíveis riscos de segurança:** Preprints não passaram por *peer review* formal — requerem distinção explícita na revisão bibliográfica frente a periódicos revisados por pares.
11. **Vantagens sobre alternativas:** Acesso imediato ao estado da arte em ML/VC e código-fonte LaTeX integral.
12. **Teste simples de verificação:** Wrapper verificado localmente (`search_arxiv.py --help` OK).

### 4.4 Semantic Scholar Academic Graph API
1. **Nome e finalidade:** Semantic Scholar API — grafo semântico de literatura com resumos, *TL;DRs*, contexto de citações (*influential citations*), embeddings e API de recomendações.
2. **Repositório e documentação oficial:** `https://api.semanticscholar.org/` e `https://www.semanticscholar.org/product/api`.
3. **Tipo:** API REST JSON.
4. **Compatibilidade com Antigravity:** Alta via Python stdlib (Camada 0) ou via MCP `zongmin-yu` (Camada 2).
5. **Requisitos de instalação:** Nenhum via HTTP Python; opcional MCP via `uvx`.
6. **Comandos de instalação/configuração:** Passar cabeçalho `x-api-key: $SEMANTIC_SCHOLAR_API_KEY` quando houver chave.
7. **Dependência de APIs ou contas:** Sem chave usa pool global compartilhado; solicitação de API key gratuita via portal Semantic Scholar.
8. **Custos e limites:** Gratuita. **Sem chave:** pool compartilhado global de `1.000 req/s` entre todos os usuários anônimos no mundo (altamente sujeito a HTTP `429` em horários de pico). **Com chave introdutória gratuita:** **`1 req/s` dedicado** em todos os endpoints.
9. **Maturidade e manutenção:** Alta (Allen Institute for AI — Ai2).
10. **Possíveis riscos de segurança:** Baixo; em consultas anônimas, falha intermitente por HTTP `429` exige backoff exponencial.
11. **Vantagens sobre alternativas:** Excelente para identificar *influential citations* e descoberta por similaridade semântica entre artigos de PDI/grafeno.
12. **Teste simples de verificação:** **Apenas consultado** na documentação oficial via `search_web`.

### 4.5 Unpaywall REST API (v2)
1. **Nome e finalidade:** Unpaywall — resolve um DOI para URLs legais e gratuitas de acesso aberto (repositórios institucionais, versões *Green/Gold/Bronze OA*).
2. **Repositório e documentação oficial:** `https://unpaywall.org/products/api`.
3. **Tipo:** API REST JSON.
4. **Compatibilidade com Antigravity:** Alta via Python stdlib `urllib.request` (Camada 0).
5. **Requisitos de instalação:** Nenhum.
6. **Comandos de instalação/configuração:** `GET https://api.unpaywall.org/v2/{doi}?email={USER_EMAIL}`.
7. **Dependência de APIs ou contas:** Sem API key, mas **parâmetro `email` real é obrigatório** (e-mails genéricos como `test@example.com` são rejeitados com HTTP `422 Unprocessable Entity`).
8. **Custos e limites:** Gratuita; diretriz de **100.000 chamadas/dia** (para volumes maiores exige download do snapshot completo).
9. **Maturidade e manutenção:** Alta (OurResearch, mesma mantenedora do OpenAlex).
10. **Possíveis riscos de segurança:** Baixo; usa apenas links legais indexados, evitando riscos de direitos autorais do Sci-Hub.
11. **Vantagens sobre alternativas:** Complementa perfeitamente o Crossref/OpenAlex para localizar PDFs legais sem paywall.
12. **Teste simples de verificação:** **Apenas consultado** na documentação via `search_web`.

### 4.6 Europe PMC e PubMed / NCBI E-utilities
1. **Nome e finalidade:** Europe PMC (`https://europepmc.org/webservices/rest`) e PubMed/NCBI E-utilities (`https://eutils.ncbi.nlm.nih.gov/`) — bases biomédicas e interdisciplinares com acesso a texto completo OA (PMC JATS XML).
2. **Repositório e documentação oficial:** `https://europepmc.org/` e `https://www.ncbi.nlm.nih.gov/books/NBK25501/`.
3. **Tipo:** APIs REST (já encapsuladas nas skills `literature_search_europepmc` e `pubmed_database`).
4. **Compatibilidade com Antigravity:** Nativas hoje (Camada 0).
5. **Requisitos de instalação:** Já integradas ao plugin `science`.
6. **Comandos de instalação/configuração:** Via `uv run` dos scripts em `plugins/science/skills/`.
7. **Dependência de APIs ou contas:** Europe PMC não exige chave; PubMed aceita `NCBI_API_KEY` gratuita + `USER_EMAIL`.
8. **Custos e limites:** Gratuitas; Europe PMC `1 req/s` no wrapper (`OPEN_ACCESS:y`); NCBI `3 req/s` sem chave e `10 req/s` com `NCBI_API_KEY`.
9. **Maturidade e manutenção:** Altíssima (EMBL-EBI e NIH/NCBI).
10. **Possíveis riscos de segurança:** Muito baixo.
11. **Vantagens sobre alternativas:** Entrega texto completo XML limpo para artigos de caracterização AFM/MEV aplicada a biomateriais e nanocompósitos de grafeno.
12. **Teste simples de verificação:** Wrappers `--help` **testados localmente** nesta sessão.

### 4.7 SciELO (OAI-PMH & ArticleMeta), Periódicos CAPES (CAFe) e Dimensions
1. **Nome e finalidade:**
   - **SciELO:** base aberta latino-americana/ibero-americana com endpoints OAI-PMH (`http://www.scielo.br/oai/scielo-oai.php`), ArticleMeta REST API e CitedBy API.
   - **Portal de Periódicos da CAPES:** biblioteca virtual nacional com acesso pago pelo governo brasileiro a Elsevier/ScienceDirect, Springer, ACS, IEEE, Scopus e Web of Science via federação **CAFe** (UFCA).
   - **Dimensions (Digital Science):** base integrada de publicações, citações, patentes e financiamentos com interface web gratuita e API baseada em **DSL**.
2. **Repositório e documentação oficial:** `https://scielo.org/` / `https://articlemeta.scielo.org/`; `https://www.periodicos.capes.gov.br/`; `https://www.dimensions.ai/`.
3. **Tipo:** APIs abertas (SciELO), Portal Web autenticado via Shibboleth/CAFe (CAPES) e Plataforma/API comercial com camada web gratuita (Dimensions).
4. **Compatibilidade com Antigravity:** SciELO API é compatível hoje via Python (Camada 0); CAPES/CAFe **exige login humano no navegador** (incompatível com automação autônoma segura por exigir credencial institucional UFCA/Shibboleth); Dimensions API completa exige licença institucional/paga.
5. **Requisitos de instalação:** Nenhum para SciELO/CAPES web; Dimensions API exige conta/licença autorizada.
6. **Comandos de instalação/configuração:** Para CAPES: acessar pelo navegador via CAFe -> UFCA e baixar PDFs manualmente para a pasta local, processando depois com `pymupdf4llm`.
7. **Dependência de APIs ou contas:** SciELO: livre; CAPES: vínculo ativo UFCA via CAFe; Dimensions API: credencial institucional ou plano acadêmico aprovado.
8. **Custos e limites:** SciELO gratuita; CAPES gratuito para discentes/docentes UFCA; Dimensions web gratuita com limites de exportação e API comercial/restrita.
9. **Maturidade e manutenção:** Institucionais (FAPESP/BIREME, MEC/CAPES, Digital Science).
10. **Possíveis riscos de segurança:** **Jamais** automatizar login CAFe/UFCA inserindo senha institucional em scripts ou `.env`! Fazer download manual no navegador quando o artigo estiver atrás de paywall (Elsevier/ACS/IOP) e coberto pela CAPES.
11. **Vantagens sobre alternativas:** SciELO captura literatura nacional em português/espanhol; CAPES/CAFe é a **única via legal gratuita** para ler o texto integral de periódicos fechados essenciais em Ciência dos Materiais (*Carbon*, *ACS Nano*, *Nanotechnology*, *Computational Materials Science*).
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (presença de acesso CAPES/UFCA do pesquisador não testada nesta sessão).

### 4.8 Google Scholar (Limitações Críticas de Anti-Bot, CAPTCHA e ToS)
1. **Nome e finalidade:** Google Scholar (`https://scholar.google.com/`) — motor de busca acadêmica amplo em texto completo.
2. **Repositório e documentação oficial:** `https://scholar.google.com/` (não possui API pública oficial).
3. **Tipo:** Aplicação web fechada (sem API REST oficial).
4. **Compatibilidade com Antigravity:** **Incompatível para automação agêntica direta.** Bibliotecas de scraping (ex.: `scholarly`, ou módulos de scraping em `openags/paper-search-mcp`) disparam proteção anti-bot.
5. **Requisitos de instalação:** Não aplicável (uso apenas interativo humano no navegador).
6. **Comandos de instalação/configuração:** Não configurar scrapers nem proxies de contorno.
7. **Dependência de APIs ou contas:** Sem API oficial.
8. **Custos e limites:** Gratuito apenas no navegador humano; requisições automatizadas sofrem HTTP `403 Forbidden`, bloqueio temporário de IP e desafios **CAPTCHA** agressivos.
9. **Maturidade e manutenção:** Serviço consolidado para busca manual, mas **impróprio para pipelines automáticos**.
10. **Possíveis riscos de segurança e compliance:** Violação explícita dos **Termos de Serviço (ToS)** do Google ao automatizar scraping; risco de banir o IP da rede universitária/residencial para buscas legítimas; e **regra estrita** de nunca tentar burlar CAPTCHAs.
11. **Vantagens sobre alternativas:** Alta indexação de teses/dissertações brasileiras em PDF que às vezes escapam do Crossref — deve ser usado **manualmente pelo pesquisador** no Chrome quando necessário, enquanto agentes usam **OpenAlex + Crossref + arXiv + Semantic Scholar + Unpaywall**.
12. **Teste simples de verificação:** **Documentado pela política oficial/busca web** (nenhum scraping executado em conformidade com as regras de segurança).

### Tabela Comparativa e Ranking Técnico — Categoria 4 (Bases e APIs)

| Posição | Base / API | Cobertura Materiais & CV/ML | Limite Gratuito | Pronta Hoje? | Uso Principal |
| :---: | :--- | :--- | :--- | :---: | :--- |
| **1º** | **OpenAlex** | **Excelente** | `$0.10/dia` IP (`$1/dia` chave grátis) | **Sim (Skill)** | Descoberta sistemática, citações, DOIs |
| **2º** | **Crossref** | **Excelente** (periódicos DOI) | `10 req/s` (`mailto`) | **Sim (Python)** | Validação de metadados e `.bib` oficial |
| **3º** | **arXiv** | **Excelente** (`cond-mat`, `cs.CV`) | `1 req/3s` | **Sim (Skill)** | Preprints recentes + código LaTeX |
| **4º** | **Semantic Scholar** | **Muito Boa** | `1 req/s` c/ chave grátis (pool sem chave instável) | **Sim (Python)** | Grafos de citação e recomendações |
| **5º** | **Unpaywall** | Boa (resolutor OA legal) | `100k/dia` (`email` real) | **Sim (Python)** | Localizar PDF aberto legal por DOI |
| **6º** | **Periódicos CAPES (CAFe)** | **Excelente** (Elsevier/ACS/IOP) | Ilimitado via UFCA (humano) | **Navegador** | Baixar PDFs fechados de periódicos |
| **7º** | **Europe PMC** | Limitada (nanobio/sensor) | `1 req/s` | **Sim (Skill)** | Full text JATS XML OA |
| **8º** | **SciELO** | Regional (América Latina) | Aberta (OAI-PMH/REST) | **Sim (Python)** | Teses/artigos em português/região |
| **9º** | **PubMed / NCBI** | Limitada (biomédico) | `3 req/s` (`10/s` c/ chave) | **Sim (Skill)** | Intersecção bio-materiais |
| **10º** | **Dimensions** | Boa | Web grátis limitada / API paga | **Web manual** | Conferência pontual de métricas |
| **11º** | **Google Scholar** | Excelente (manual) | **Bloqueio CAPTCHA/ToS** | **Só manual** | **Proibido automatizar scraping** |

---

## 5. Análise de PDFs, PPTX e Recuperação Local

### 5.1 `PyMuPDF` / `pymupdf4llm`
1. **Nome e finalidade:** `PyMuPDF` (`pymupdf`) + `pymupdf4llm` — extração ultrarrápida de PDF para Markdown estruturado para LLMs, com leitura de colunas, tabelas e metadados.
2. **Repositório e documentação oficial:** `https://github.com/pymupdf/PyMuPDF` e `https://pymupdf.readthedocs.io/`.
3. **Tipo:** Biblioteca Python (Camada 1 efêmera via `uv run --with pymupdf4llm`).
4. **Compatibilidade com Antigravity:** **100% compatível hoje** no Windows 10 via `uv run --with pymupdf4llm`.
5. **Requisitos de instalação:** Apenas `uv` (`0.13.7` presente). Baixa ~12 pacotes no cache efêmero (`pymupdf` 60.1 MiB, `onnxruntime` 15.9 MiB, `networkx` 2.0 MiB).
6. **Comandos de instalação/configuração:**
   ```powershell
   uv run --with pymupdf4llm python -c "import pymupdf4llm; print(pymupdf4llm.to_markdown('artigo.pdf')[:500])"
   ```
7. **Dependência de APIs ou contas:** Nenhuma (100% offline/local).
8. **Custos e limites:** **Atenção à licença:** código aberto sob **GNU AGPL v3.0** (gratuita para uso acadêmico/pesquisa local; uso comercial/SaaS fechado exige licença comercial Artifex).
9. **Maturidade e manutenção:** Altíssima; padrão de mercado em velocidade.
10. **Possíveis riscos de segurança:** Baixo (processamento local; risco apenas de licença AGPL se um software proprietário futuro incorporar o código sem abrir fontes).
11. **Vantagens sobre alternativas:** Sub-segundo em CPU comum (sem exigir GPU nem baixar 10–20 GB de modelos como Docling/Marker).
12. **Teste simples de verificação:** **TESTADO LOCALMENTE NESTA SESSÃO (16/11/2026)** — `uv run --with pymupdf4llm python -c "import pymupdf, importlib.metadata as m; print('pymupdf:', m.version('pymupdf'), 'pymupdf4llm:', m.version('pymupdf4llm'))"` executou com sucesso, retornando `pymupdf: 2.1 pymupdf4llm: 2.1` (12 pacotes resolvidos em 829 ms).

### 5.2 `python-pptx`
1. **Nome e finalidade:** `python-pptx` — leitura e criação programática de arquivos PowerPoint `.pptx` (slides, caixas de texto, tabelas, imagens, gráficos e notas do apresentador).
2. **Repositório e documentação oficial:** `https://github.com/scanny/python-pptx` e `https://python-pptx.readthedocs.io/`.
3. **Tipo:** Biblioteca Python (Camada 1 efêmera via `uv run --with python-pptx`).
4. **Compatibilidade com Antigravity:** **100% compatível hoje** no Windows 10 via `uv run --with python-pptx`.
5. **Requisitos de instalação:** Apenas `uv` (baixa 5 pacotes leves, incluindo `lxml` 3.8 MiB).
6. **Comandos de instalação/configuração:**
   ```powershell
   uv run --with python-pptx python -c "import pptx; print(pptx.__version__)"
   ```
7. **Dependência de APIs ou contas:** Nenhuma (100% offline).
8. **Custos e limites:** Gratuita (**MIT License**). Limitação conhecida: **não** renderiza equações LaTeX nativamente para OMML sem gerar XML customizado ou imagem PNG/SVG via `matplotlib`.
9. **Maturidade e manutenção:** Muito alta (estável `1.0.2`).
10. **Possíveis riscos de segurança:** Muito baixo; cuidado apenas ao inspecionar `.pptx` externos por XML malformado (`lxml` já protege por padrão contra entidades externas em versões modernas).
11. **Vantagens sobre alternativas:** Funciona **hoje** sem PowerPoint nem LibreOffice instalados e produz `.pptx` 100% editável pelo pesquisador/orientador.
12. **Teste simples de verificação:** **TESTADO LOCALMENTE NESTA SESSÃO (16/11/2026)** — `uv run --with python-pptx python -c "import pptx; print('python-pptx:', pptx.__version__)"` instalou 5 pacotes em 233 ms e imprimiu `python-pptx: 1.0.2`.

### 5.3 `pdfplumber`
1. **Nome e finalidade:** `pdfplumber` — extração precisa de coordenadas de caracteres, linhas, retângulos e **tabelas estruturadas** em PDFs científicos (built on `pdfminer.six`).
2. **Repositório e documentação oficial:** `https://github.com/jsvine/pdfplumber`.
3. **Tipo:** Biblioteca Python (Camada 1 efêmera via `uv run --with pdfplumber`).
4. **Compatibilidade com Antigravity:** Compatível hoje via `uv run --with pdfplumber`.
5. **Requisitos de instalação:** Apenas `uv` (pure Python + `Pillow`/`pypdfium2`).
6. **Comandos de instalação/configuração:** `uv run --with pdfplumber python script.py`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuita (**MIT License**); mais lenta que PyMuPDF em PDFs extensos e **não** faz OCR de PDFs escaneados.
9. **Maturidade e manutenção:** Alta.
10. **Possíveis riscos de segurança:** Muito baixo.
11. **Vantagens sobre alternativas:** Licença MIT (sem restrição AGPL do PyMuPDF) e depuração visual/geométrica exata para tabelas de parâmetros DRX/MEV/AFM em artigos.
12. **Teste simples de verificação:** **Apenas consultado** na documentação (`uv run --with pdfplumber` não executado nesta sessão).

### 5.4 `MarkItDown` (`microsoft/markitdown`)
1. **Nome e finalidade:** `MarkItDown` — utilitário e biblioteca leve da Microsoft para converter PDF, PPTX, DOCX, XLSX e HTML em Markdown limpo para LLMs.
2. **Repositório e documentação oficial:** `https://github.com/microsoft/markitdown`.
3. **Tipo:** Biblioteca Python / CLI / MCP opcional (`markitdown-mcp`).
4. **Compatibilidade com Antigravity:** Compatível via `uv run --with "markitdown[pdf,pptx]"`.
5. **Requisitos de instalação:** `uv` / Python `3.10+`.
6. **Comandos de instalação/configuração:** `uv run --with "markitdown[pdf,pptx]" markitdown arquivo.pdf`.
7. **Dependência de APIs ou contas:** Nenhuma para conversão padrão (opcional Azure Document Intelligence / LLM para descrição de imagens).
8. **Custos e limites:** Gratuito (**MIT License**). Limite: em PDFs científicos com duas colunas e equações complexas, entrega texto mais simples que `pymupdf4llm` ou `Docling`.
9. **Maturidade e manutenção:** Alta (Microsoft open-source, amplamente adotado em 2025–2026).
10. **Possíveis riscos de segurança:** Muito baixo em uso offline.
11. **Vantagens sobre alternativas:** Única ferramenta ultraleve com interface única para ler tanto `.pdf` quanto `.pptx` e `.docx` direto para Markdown.
12. **Teste simples de verificação:** **Apenas consultado** no GitHub via `search_web`.

### 5.5 `Docling` (Biblioteca Python)
1. **Nome e finalidade:** `Docling` — parser documental avançado (IBM Research) com detecção de layout (DocLayNet/RT-DETR), estruturação de tabelas (`TableFormer`) e exportação para Markdown/JSON/DocTags.
2. **Repositório e documentação oficial:** `https://github.com/docling-project/docling` e `https://ds4sd.github.io/docling/`.
3. **Tipo:** Biblioteca Python / CLI (Camada 2 se local com cache de modelos).
4. **Compatibilidade com Antigravity:** Compatível no Windows 10 via `uv`, mas pesado para hoje.
5. **Requisitos de instalação:** Python `3.10+`, ~2–16 GB RAM (recomendado 8+ cores ou GPU NVIDIA), vários GBs de espaço em disco para pesos de modelos baixados na primeira execução.
6. **Comandos de instalação/configuração:** `uv run --with docling docling artigo.pdf`.
7. **Dependência de APIs ou contas:** Nenhuma (modelos abertos executam localmente).
8. **Custos e limites:** Gratuito (**MIT License**); lento em CPU pura sem GPU para dezenas de artigos.
9. **Maturidade e manutenção:** Altíssima (>70k estrelas — LF AI & Data / IBM).
10. **Possíveis riscos de segurança:** Baixo (100% local após download dos pesos).
11. **Vantagens sobre alternativas:** Fidelidade muito superior em tabelas científicas densas e leitura de ordem multi-coluna sem exigir Java/Docker como o GROBID.
12. **Teste simples de verificação:** **Apenas consultado** na documentação/GitHub.

### 5.6 `GROBID`
1. **Nome e finalidade:** `GROBID` (*GeneRation Of BIbliographic Data*) — servidor ML especializado em converter PDFs acadêmicos para XML TEI estruturado (metadados, seções, citações inline e referências).
2. **Repositório e documentação oficial:** `https://github.com/kermitt2/grobid` e `https://grobid.readthedocs.io/`.
3. **Tipo:** Serviço REST local (Java / Docker).
4. **Compatibilidade com Antigravity:** **Incompatível hoje (16/11)** — exige **Java 11+** ou **Docker**, ambos **ausentes** neste Windows 10.
5. **Requisitos de instalação:** Docker Desktop ou JDK 11+ + 4–8 GB RAM.
6. **Comandos de instalação/configuração:** `docker run --rm --init -p 8070:8070 lfoppiano/grobid:latest`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (**Apache-2.0**).
9. **Maturidade e manutenção:** Altíssima (padrão ouro em mineração bibliográfica TEI há mais de uma década).
10. **Possíveis riscos de segurança:** Baixo localmente; exige Docker/WSL2 no Windows.
11. **Vantagens sobre alternativas:** Extração incomparável de *referências bibliográficas citadas dentro de PDFs* para montar grafos, porém completamente inviável para o prazo de amanhã.
12. **Teste simples de verificação:** **Verificado impedimento local** (`docker -> NOT_FOUND`, `java -> NOT_FOUND`).

### 5.7 `Pandoc` (Análise de Entrada Documental)
1. **Nome e finalidade:** `Pandoc` — conversor universal entre formatos de marcação (`Markdown`, `LaTeX`, `DOCX`, `HTML`, `BibTeX`, `EPUB`).
2. **Repositório e documentação oficial:** `https://github.com/jgm/pandoc` e `https://pandoc.org/`.
3. **Tipo:** Binário CLI Haskell (ausente no `PATH` atual).
4. **Compatibilidade com Antigravity:** **Indisponível hoje** (`pandoc -> NOT_FOUND`); pode ser baixado como `.zip` portátil ou via `winget` na Camada 2.
5. **Requisitos de instalação:** Binário `pandoc.exe` (Windows x64).
6. **Comandos de instalação/configuração:** `winget install --id JohnMacFarlane.Pandoc` (sujeito à aprovação).
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (**GPL-2.0**). Limitação crítica na Categoria 5: **Pandoc não lê PDF como formato de entrada** (exige outro parser antes).
9. **Maturidade e manutenção:** Altíssima.
10. **Possíveis riscos de segurança:** Muito baixo.
11. **Vantagens sobre alternativas:** Excelente para converter Markdown/LaTeX em `.docx`/`.tex`/HTML na escrita da dissertação, mas inútil para extrair dados de PDFs.
12. **Teste simples de verificação:** **Verificado localmente ausente** (`pandoc -> NOT_FOUND`).

### 5.8 Extratores de Equações, Tabelas e Figuras (`Marker`, `Pix2Tex`, `pdfplumber` [ver 5.3])
- **`Marker` (`datalab-to/marker`):**
  1. **Nome e finalidade:** `Marker` — converte PDFs científicos para Markdown/JSON reconstruindo **equações em LaTeX**, tabelas e layout via modelos Surya OCR/DL.
  2. **Repositório e documentação oficial:** `https://github.com/datalab-to/marker`.
  3. **Tipo:** Biblioteca Python / CLI (Camada 2 pesada).
  4. **Compatibilidade com Antigravity:** Compatível via Python `3.10+` / `uv`, mas pesado para CPU sem GPU.
  5. **Requisitos de instalação:** PyTorch, modelos Surya (~vários GBs baixados na primeira execução), alta RAM/VRAM recomendada.
  6. **Comandos de instalação/configuração:** `uv run --with marker-pdf marker_single artigo.pdf`.
  7. **Dependência de APIs ou contas:** Nenhuma no modo local; API hospedada Datalab opcional paga.
  8. **Custos e limites:** **Licença dupla:** código `Apache-2.0`, mas **pesos dos modelos** sob *Modified AI Pubs Open RAIL-M* (grátis para pesquisa pessoal/acadêmica e pequenas startups; uso comercial amplo exige licença Datalab).
  9. **Maturidade e manutenção:** Alta e em rápida evolução em 2025–2026.
  10. **Possíveis riscos de segurança:** Baixo localmente; atenção à licença restritiva dos pesos para uso comercial futuro.
  11. **Vantagens sobre alternativas:** Melhor preservação automática de fórmulas matemáticas (Bragg, Scherrer, razão $I_D/I_G$ Raman, funções de perda ML) em PDFs.
  12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

- **`Pix2Tex` (`lukas-blecher/LaTeX-OCR`):**
  1. **Nome e finalidade:** `Pix2Tex` — converte **recortes de imagem** (PNG) de equações matemáticas diretamente em código LaTeX via Vision Transformer (ViT).
  2. **Repositório e documentação oficial:** `https://github.com/lukas-blecher/LaTeX-OCR`.
  3. **Tipo:** Biblioteca Python / CLI (`pix2tex`).
  4. **Compatibilidade com Antigravity:** Compatível via `uv run --with pix2tex` (Camada 2 pela dependência pesada de PyTorch).
  5. **Requisitos de instalação:** PyTorch, `timm`, `transformers`, `albumentations` + download de pesos ViT.
  6. **Comandos de instalação/configuração:** `uv run --with pix2tex pix2tex equacao.png`.
  7. **Dependência de APIs ou contas:** Nenhuma.
  8. **Custos e limites:** Gratuito (**MIT License**); sujeito a erros em equações multi-linha densas ou baixa resolução.
  9. **Maturidade e manutenção:** Moderada/estável (superado em página inteira pelo ecossistema Surya/`Marker`, útil para recortes pontuais).
  10. **Possíveis riscos de segurança:** Baixo.
  11. **Vantagens sobre alternativas:** Leve em escopo (foca apenas no recorte da equação sem precisar processar o PDF inteiro); alternativa gratuita/MIT ao Mathpix pago.
  12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### 5.9 Busca e Indexação Local (`SQLite FTS5`, `rank_bm25`, `LanceDB`, `ChromaDB`)
- **`SQLite FTS5` (Python `sqlite3` stdlib):**
  1. **Nome e finalidade:** Motor de busca *full-text* relacional com algoritmo **BM25 nativo** embutido diretamente na biblioteca padrão do Python `3.11.18`.
  2. **Repositório e documentação oficial:** `https://www.sqlite.org/fts5.html` e `https://docs.python.org/3/library/sqlite3.html`.
  3. **Tipo:** Motor embarcado nativo (Camada 0 Zero-Install!).
  4. **Compatibilidade com Antigravity:** **100% ativo hoje** em `C:\Users\emer\.local\bin\python3.11.exe`.
  5. **Requisitos de instalação:** **Zero** (já compilado na stdlib local).
  6. **Comandos de instalação/configuração:** `CREATE VIRTUAL TABLE docs_fts USING fts5(doi, title, section, body);`.
  7. **Dependência de APIs ou contas:** Nenhuma (100% offline).
  8. **Custos e limites:** Gratuito (Domínio Público / Python PSF); busca estritamente lexical (não captura sinônimos semânticos sem expansão).
  9. **Maturidade e manutenção:** Máxima (`sqlite 3.53.1`).
  10. **Possíveis riscos de segurança:** Muito baixo (arquivo único `.db` local; usar queries parametrizadas contra SQL injection).
  11. **Vantagens sobre alternativas:** **Zero dependências, zero downloads, persistência imediata em disco** e ranking BM25 nativo — ideal para indexar os PDFs/fichamentos da Missão 02 hoje!
  12. **Teste simples de verificação:** **TESTADO LOCALMENTE NESTA SESSÃO** (`sqlite_version: 3.53.1`, `FTS5: ['ENABLE_FTS3', 'ENABLE_FTS3_PARENTHESIS', 'ENABLE_FTS4', 'ENABLE_FTS5']`).

- **`rank_bm25`:**
  1. **Nome e finalidade:** `rank_bm25` — biblioteca Python pura com implementações de Okapi BM25, BM25L e BM25+ em memória.
  2. **Repositório e documentação oficial:** `https://github.com/dorianbrown/rank_bm25` (`https://pypi.org/project/rank-bm25/`).
  3. **Tipo:** Biblioteca Python pura (Camada 1 efêmera).
  4. **Compatibilidade com Antigravity:** Compatível hoje via `uv run --with rank-bm25`.
  5. **Requisitos de instalação:** `uv` (apenas `numpy` leve).
  6. **Comandos de instalação/configuração:** `uv run --with rank-bm25 python script.py`.
  7. **Dependência de APIs ou contas:** Nenhuma.
  8. **Custos e limites:** Gratuita (**Apache-2.0**); índice não é persistido em disco automaticamente (reconstruído em memória).
  9. **Maturidade e manutenção:** Estável, porém minimalista.
  10. **Possíveis riscos de segurança:** Muito baixo.
  11. **Vantagens sobre alternativas:** Mais flexível para tokenização científica customizada em memória (ex.: siglas `DRX`/`XRD`, `MEV`/`SEM`), porém redundante frente ao `SQLite FTS5` para persistência em disco.
  12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

- **`LanceDB`:**
  1. **Nome e finalidade:** `LanceDB` — banco vetorial embarcado *serverless* baseado no formato colunar **Lance** (Rust + Apache Arrow) com busca híbrida nativa (vetorial + lexical via *Reciprocal Rank Fusion* — RRF).
  2. **Repositório e documentação oficial:** `https://github.com/lancedb/lancedb` e `https://lancedb.com/`.
  3. **Tipo:** Banco vetorial embarcado Python (Camada 1/2).
  4. **Compatibilidade com Antigravity:** Excelente suporte no Windows + Python 3.11 via wheels Rust pré-compilados (`uv run --with lancedb`).
  5. **Requisitos de instalação:** `uv` + modelo de embeddings local (ex.: `fastembed`/`sentence-transformers`) ou API de embeddings.
  6. **Comandos de instalação/configuração:** `uv run --with lancedb python rag.py`.
  7. **Dependência de APIs ou contas:** Nenhuma em modo embarcado local com embeddings locais.
  8. **Custos e limites:** Gratuito (**Apache-2.0**).
  9. **Maturidade e manutenção:** Alta e muito ativa em 2025–2026.
  10. **Possíveis riscos de segurança:** Baixo localmente.
  11. **Vantagens sobre alternativas:** Armazenamento nativo em disco sem esgotar RAM, instalação limpa no Windows sem precisar de compilador C++ e busca híbrida pronta.
  12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

- **`ChromaDB`:**
  1. **Nome e finalidade:** `ChromaDB` — banco vetorial local/cliente-servidor usando SQLite + índices HNSW, amplamente integrado a LangChain/LlamaIndex.
  2. **Repositório e documentação oficial:** `https://github.com/chroma-core/chroma`.
  3. **Tipo:** Banco vetorial embarcado Python (Camada 1/2).
  4. **Compatibilidade com Antigravity:** Compatível via Python 3.11, porém com ressalva no Windows se alguma versão exigir compilação nativa de `hnswlib` sem wheel compatível.
  5. **Requisitos de instalação:** `uv` + espaço para modelo padrão ONNX (`all-MiniLM-L6-v2`) se usado sem embeddings externos.
  6. **Comandos de instalação/configuração:** `uv run --with chromadb python rag.py`.
  7. **Dependência de APIs ou contas:** Nenhuma em modo persistente local.
  8. **Custos e limites:** Gratuito (**Apache-2.0**); índices HNSW tendem a consumir mais RAM conforme a coleção cresce.
  9. **Maturidade e manutenção:** Alta.
  10. **Possíveis riscos de segurança:** Baixo localmente.
  11. **Vantagens sobre alternativas:** Grande quantidade de tutoriais e integração nativa de embeddings padrão, embora `LanceDB` seja tecnicamente mais suave no Windows e já faça busca híbrida.
  12. **Teste simples de verificação:** **Apenas consultado** via `search_web`.

### Tabela Comparativa e Ranking Técnico — Categoria 5 (PDF, PPTX & Busca Local)

| Posição | Ferramenta | Papel Principal | Licença | Pronta Hoje? | Verificação Local |
| :---: | :--- | :--- | :--- | :---: | :--- |
| **1º** | **`SQLite FTS5`** (`sqlite3`) | Indexação & busca BM25 persistente local | Domínio Público | **Sim (Camada 0)** | **Testado (`3.53.1` + FTS5)** |
| **2º** | **`PyMuPDF` / `pymupdf4llm`** | Extração rápida PDF → Markdown para LLMs | AGPL-3.0 | **Sim (Camada 1)** | **Testado (`2.1`)** |
| **3º** | **`python-pptx`** | Leitura e geração nativa de `.pptx` | MIT | **Sim (Camada 1)** | **Testado (`1.0.2`)** |
| **4º** | **`pdfplumber`** | Extração exata de tabelas em PDF | MIT | **Sim (Camada 1)** | Consultado |
| **5º** | **`MarkItDown`** | Conversor leve multi-formato (`pdf`/`pptx`/`docx`) | MIT | **Sim (Camada 1)** | Consultado |
| **6º** | **`LanceDB`** | RAG vetorial + busca híbrida em disco (Missão 02+) | Apache-2.0 | **Sim (Camada 1/2)** | Consultado |
| **7º** | **`Docling`** | Layout + `TableFormer` de alta fidelidade | MIT | **Camada 2 (Pesado)** | Consultado |
| **8º** | **`Marker`** | PDF → Markdown + equações LaTeX (Surya OCR) | Apache-2.0 / RAIL-M | **Camada 2 (Pesado)** | Consultado |
| **9º** | **`ChromaDB`** | Banco vetorial SQLite + HNSW | Apache-2.0 | **Camada 1/2** | Consultado |
| **10º** | **`rank_bm25`** | Ranking lexical em memória | Apache-2.0 | **Sim (Camada 1)** | Consultado |
| **11º** | **`Pix2Tex`** | Recorte PNG de equação → LaTeX | MIT | **Camada 2 (PyTorch)** | Consultado |
| **12º** | **`Pandoc`** | Conversão Markdown/LaTeX/DOCX (não lê PDF) | GPL-2.0 | **Ausente hoje** | `NOT_FOUND` |
| **13º** | **`GROBID`** | XML TEI bibliográfico (exige Java/Docker) | Apache-2.0 | **Bloqueado hoje** | `java/docker NOT_FOUND` |

---

## 6. Gerenciamento Bibliográfico

### 6.1 Geração Direta e Verificável de `.bib` via Crossref + OpenAlex (API/Python)
1. **Nome e finalidade:** Pipeline reprodutível em Python (`C:\Users\emer\.local\bin\python3.11.exe`) que resolve cada DOI na API oficial do **Crossref** (`Accept: application/x-bibtex` ou `/transform/application/x-bibtex`) e cruza metadados com **OpenAlex** para validar existência, autores, periódico, ano e gerar arquivos `.bib` limpos e auditáveis.
2. **Repositório e documentação oficial:** APIs `https://api.crossref.org/` e `https://docs.openalex.org/` (implementação local por script próprio ou `uv`).
3. **Tipo:** Fluxo CLI / Script Python stdlib (Camada 0 Zero-Install!).
4. **Compatibilidade com Antigravity:** **100% compatível hoje** sem instalar apps desktop nem Java.
5. **Requisitos de instalação:** Nenhum (usa `urllib.request` e `json` da stdlib de `python3.11.exe`).
6. **Comandos de instalação/configuração:** Invocar `python3.11.exe` para consultar `/works/{doi}/transform/application/x-bibtex`, normalizar citekeys (`AutorAnoPalavra`) e checar duplicatas/erros de DOI (ex.: detectar DOIs trocados como o caso Holm et al. 2020).
7. **Dependência de APIs ou contas:** Crossref pública (`mailto` opcional recomendado); OpenAlex sem chave (`$0.10/dia`) ou com `OPENALEX_API_KEY`.
8. **Custos e limites:** Totalmente gratuito dentro dos limites das APIs (`10 req/s` Crossref polite pool).
9. **Maturidade e manutenção:** Padrão determinístico e 100% auditável no controle de versão.
10. **Possíveis riscos de segurança:** Baixo; validar sintaxe `.bib` (chaves balanceadas, caracteres `&`/`%` escapados e verificação se o título retornado pelo Crossref bate com o artigo citado!).
11. **Vantagens sobre alternativas:** **Única solução pronta hoje (16/11/2026)** sem instalar Zotero ou JabRef, eliminando fabricação de DOIs/BibTeX por LLMs.
12. **Teste simples de verificação:** **Verificada capacidade local** de `python3.11.exe` + `openalex_cli.py`; validação efetiva dos DOIs executada em paralelo por `@agente-bibliografia`.

### 6.2 `Zotero 7` + `Better BibTeX (BBT)`
1. **Nome e finalidade:** `Zotero 7` (gerenciador completo de PDFs, anotações e coleções) combinado ao plugin `Better BibTeX` (`retorquere/zotero-better-bibtex`) para gerar citekeys determinísticas e auto-sincronizar um arquivo `.bib`/`.json` para LaTeX, Quarto, Typst e Pandoc.
2. **Repositório e documentação oficial:** `https://www.zotero.org/` e `https://retorque.re/zotero-better-bibtex/` (`https://github.com/retorquere/zotero-better-bibtex`).
3. **Tipo:** Aplicativo Desktop + Extensão `.xpi` (Camada 2).
4. **Compatibilidade com Antigravity:** Não instalado hoje (`zotero.exe` ausente); quando instalado na Camada 2, integra-se via exportação automática de `.bib` (leitura direta pelos agentes) e opcionalmente via MCP (`oscardvs/zoteus` ou `cookjohn/zotero-mcp`).
5. **Requisitos de instalação:** Instalador Windows Zotero 7 + download do `.xpi` do Better BibTeX.
6. **Comandos de instalação/configuração:** `winget install --id DigitalScholar.Zotero` (após aprovação) + instalação manual do `.xpi` em `Tools > Plugins`.
7. **Dependência de APIs ou contas:** Nenhuma obrigatória para uso local; conta Zotero gratuita para nuvem (limite 300 MB grátis de anexos).
8. **Custos e limites:** Gratuito e open-source (`AGPL` Zotero / `MIT` BBT); armazenamento em nuvem >300 MB é pago (contornável com WebDAV ou armazenamento 100% local).
9. **Maturidade e manutenção:** Altíssima (padrão ouro acadêmico).
10. **Possíveis riscos de segurança:** Baixo; manter backup da pasta `Zotero/` e evitar que MCPs façam escritas em massa sem revisão.
11. **Vantagens sobre alternativas:** Melhor organização visual de centenas de PDFs da dissertação, leitor nativo de PDF com anotações e exportação contínua de `.bib` limpo.
12. **Teste simples de verificação:** **Verificado localmente ausente** (`zotero -> NOT_FOUND` e `C:\Users\emer\AppData\Local\Programs\Zotero\zotero.exe -> False`).

### 6.3 `JabRef`
1. **Nome e finalidade:** `JabRef` — gerenciador bibliográfico open-source cujo formato nativo de banco de dados já é `.bib` (BibTeX / BibLaTeX), com busca em Crossref/arXiv/OpenAlex, limpeza de campos e detecção de duplicatas.
2. **Repositório e documentação oficial:** `https://github.com/JabRef/jabref` e `https://www.jabref.org/`.
3. **Tipo:** Aplicativo Desktop (Java empacotado, Camada 2).
4. **Compatibilidade com Antigravity:** Excelente via arquivo `.bib` direto no repositório (nenhum plugin/MCP extra necessário para agentes lerem `.bib`), porém **ausente hoje** (`JabRef.exe` não encontrado).
5. **Requisitos de instalação:** Apesar de ser escrito em Java, desde a v5.0 os instaladores e pacotes portáteis oficiais para Windows **já vêm com JRE embutido**, dispensando `java` global no sistema.
6. **Comandos de instalação/configuração:** Instalador oficial/portátil em `jabref.org` ou `winget install --id JabRef.JabRef` (sujeito à aprovação).
7. **Dependência de APIs ou contas:** Nenhuma conta obrigatória.
8. **Custos e limites:** Totalmente gratuito (**MIT License**).
9. **Maturidade e manutenção:** Altíssima (mais de 20 anos de desenvolvimento ativo).
10. **Possíveis riscos de segurança:** Baixo.
11. **Vantagens sobre alternativas:** Edita diretamente o `.bib` em texto plano (ideal para Git e revisão por agentes sem camada de exportação), embora tenha leitor/anotador de PDF menos fluido que o Zotero 7.
12. **Teste simples de verificação:** **Verificado localmente ausente** (`java -> NOT_FOUND`, `C:\Program Files\JabRef\JabRef.exe -> False`).

### Tabela Comparativa e Ranking Técnico — Categoria 6 (Gerenciamento Bibliográfico)

| Posição | Solução | Pronta Hoje? | Vantagem Decisiva | Indicação |
| :---: | :--- | :---: | :--- | :--- |
| **1º** | **Geração direta `.bib` via Crossref/OpenAlex (`python3.11`)** | **Sim (Camada 0)** | Zero instalação, DOIs verificados na fonte | **Hoje / Missão 01 e início Missão 02** |
| **2º** | **Zotero 7 + Better BibTeX** | Não (Camada 2) | Gestão visual de PDFs, anotações, `.bib` automático, MCP | **Padrão recomendado pós-Seminário I** |
| **3º** | **JabRef (instalador c/ JRE embutido)** | Não (Camada 2) | `.bib` nativo amigo do Git/LaTeX/Typst | Alternativa leve se preferir fluxo 100% `.bib` |

---

## 7. Construção de Apresentações Científicas

Comparação rigorosa das **7 ferramentas solicitadas**, considerando o ambiente real de **16/11/2026** (sem `quarto`, `pandoc`, `marp`, `typst`, `pdflatex`, `libreoffice`, `POWERPNT.EXE`; com `uv 0.13.7`, `python3.11`, `node v26.13.0`/`npx 11.20.0` e Google Chrome instalado).

### 7.1 `python-pptx`
1. **Nome e finalidade:** `python-pptx` — geração programática de apresentações PowerPoint `.pptx` nativas e 100% editáveis.
2. **Repositório e documentação oficial:** `https://github.com/scanny/python-pptx` e `https://python-pptx.readthedocs.io/`.
3. **Tipo:** Biblioteca Python (Camada 1 efêmera).
4. **Compatibilidade com Antigravity:** **Máxima hoje (16/11)** via `uv run --with python-pptx`.
5. **Requisitos de instalação:** Apenas `uv` (`0.13.7` presente).
6. **Comandos de instalação/configuração:** `uv run --with python-pptx --with matplotlib python gerar_slides.py`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuita (**MIT**). Não compila LaTeX nativamente para OMML (contornável renderizando equações com `matplotlib` mathtext em PNG/SVG de alta DPI ou inserindo texto/Unicode + revisão no PowerPoint/Google Slides).
9. **Maturidade e manutenção:** Alta (`1.0.2`).
10. **Possíveis riscos de segurança:** Muito baixo (execução local offline).
11. **Vantagens sobre alternativas:** Gera **`.pptx` nativo com objetos editáveis** (títulos, listas, tabelas, imagens MEV/AFM/DRX, fluxogramas PNG/SVG e **notas do apresentador** em `slide.notes_slide`) **hoje**, sem LibreOffice, Pandoc ou LaTeX.
12. **Teste simples de verificação:** **TESTADO LOCALMENTE NESTA SESSÃO** (`python-pptx: 1.0.2`).

### 7.2 `Marp` (`@marp-team/marp-cli`)
1. **Nome e finalidade:** `Marp` — gera slides elegantes em PDF, HTML ou PPTX a partir de Markdown puro com tema CSS, KaTeX/MathJax e notas de apresentador.
2. **Repositório e documentação oficial:** `https://github.com/marp-team/marp-cli` e `https://marp.app/`.
3. **Tipo:** CLI Node.js (Camada 1 efêmera via `npx`).
4. **Compatibilidade com Antigravity:** **Compatível hoje para HTML/PDF/PPTX-imagem** usando `npx -y @marp-team/marp-cli` + Google Chrome detectado em `C:\Program Files\Google\Chrome\Application\chrome.exe`. **Limitação crítica:** a flag `--pptx-editable` requer **LibreOffice Impress** (ausente hoje!), e sem ela o `.pptx` gerado é apenas um conjunto de imagens estáticas; além disso, mesmo com `--pptx-editable`, texto sai fragmentado caixa-por-caixa.
5. **Requisitos de instalação:** `node`/`npx` (presentes: `v26.13.0` / `11.20.0`) + Chrome/Edge (Chrome presente); LibreOffice (ausente) apenas para `--pptx-editable`.
6. **Comandos de instalação/configuração:** `npx -y @marp-team/marp-cli slides.md --pdf --allow-local-files` (ou `--html`).
7. **Dependência de APIs ou contas:** Nenhuma para HTML/PDF local (Mermaid via CDN ou pré-renderizado se offline).
8. **Custos e limites:** Gratuito (**MIT**).
9. **Maturidade e manutenção:** Alta.
10. **Possíveis riscos de segurança:** Baixo (atenção apenas a `--allow-local-files` com Markdown confiável).
11. **Vantagens sobre alternativas:** Velocidade extrema de autoria em Markdown, suporte nativo excelente a **equações LaTeX (KaTeX)** e **notas do apresentador (`<!-- note -->`)** no HTML/PDF.
12. **Teste simples de verificação:** **Parcialmente verificado localmente** (`npx 11.20.0` e `chrome.exe` confirmados; `marp-cli` em si não executado para evitar download npm remoto nesta missão).

### 7.3 `Reveal.js`
1. **Nome e finalidade:** `Reveal.js` — framework web HTML/CSS/JS padrão para apresentações interativas científicas, com MathJax/KaTeX nativo, visão do apresentador (`S`) e impressão para PDF (`?print-pdf`).
2. **Repositório e documentação oficial:** `https://github.com/hakimel/reveal.js` e `https://revealjs.com/`.
3. **Tipo:** Framework Web HTML/JS (Camada 0/1).
4. **Compatibilidade com Antigravity:** **Compatível hoje** (pode ser aberto no Chrome local ou servido via `python3.11.exe -m http.server`).
5. **Requisitos de instalação:** Zero instalação via CDN ou pacote npm `reveal.js` (`v6.0.2`).
6. **Comandos de instalação/configuração:** Servir diretório HTML local ou `npx` / HTML autocontido; exportar PDF abrindo `?print-pdf` no Chrome local.
7. **Dependência de APIs ou contas:** Nenhuma se assets locais; se usar CDN online, exige internet na apresentação.
8. **Custos e limites:** Gratuito (**MIT**, ~72.5k estrelas). **Não gera `.pptx` editável.**
9. **Maturidade e manutenção:** Altíssima.
10. **Possíveis riscos de segurança:** Muito baixo.
11. **Vantagens sobre alternativas:** Melhor suporte a fluxogramas **Mermaid**, gráficos interativos e equações LaTeX impecáveis, com timer + notas de apresentador em tela dupla (`S`), sendo ideal quando **PDF/Navegador** é aceito em vez de `.pptx`.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (`chrome.exe` local confirmado).

### 7.4 `PptxGenJS`
1. **Nome e finalidade:** `PptxGenJS` (`pptxgenjs`) — biblioteca JavaScript/Node para criação programática de arquivos `.pptx` editáveis com formas, tabelas, gráficos e notas.
2. **Repositório e documentação oficial:** `https://github.com/gitbrent/PptxGenJS` (`https://gitbrent.github.io/PptxGenJS/`).
3. **Tipo:** Biblioteca Node.js/JS (Camada 1 efêmera via `npx`/npm, `v4.0.1`).
4. **Compatibilidade com Antigravity:** Compatível hoje com `node v26.13.0` + `npm/npx`.
5. **Requisitos de instalação:** Node.js (presente).
6. **Comandos de instalação/configuração:** Script Node em projeto temporário com `pptxgenjs`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuita (**MIT**, ~5.9k estrelas). **Limitação crítica:** não renderiza LaTeX/MathJax nem Mermaid nativamente (exige pré-renderização externa para SVG/PNG).
9. **Maturidade e manutenção:** Alta (`v4.0.1`).
10. **Possíveis riscos de segurança:** Baixo (risco padrão de supply chain npm ao instalar pacotes).
11. **Vantagens sobre alternativas:** Excelente API para `.pptx` editável, porém em ecossistema científico Python (`matplotlib`, `numpy`, `scipy`, imagens AFM/DRX) **`python-pptx` integra-se muito melhor** sem trocar de linguagem.
12. **Teste simples de verificação:** **Apenas consultado** via `search_web` (`node v26.13.0` confirmado localmente).

### 7.5 `Typst` (`Touying` / `Polylux`)
1. **Nome e finalidade:** `Typst` — sistema moderno de tipografia científica (compilação em milissegundos, matemática nativa inspirada em LaTeX) com pacotes de slides **`Touying`** (atual líder em recursos, animações `#pause` e notas) e **`Polylux`** (pioneiro inspirado no Beamer, notas `pdfpc`).
2. **Repositório e documentação oficial:** `https://github.com/typst/typst`, `https://touying-typ.github.io/` (`@preview/touying`), `https://polylux.dev/` e PyPI `touying` / `typst`.
3. **Tipo:** Compilador CLI / Binding Python PyPI (`typst`, `touying`, `typ2pptx`).
4. **Compatibilidade com Antigravity:** O binário `typst` não está no `PATH` hoje (`NOT_FOUND`), mas existem wrappers PyPI (`uv run --with typst` / `uv run --with touying`) na Camada 1/2 (não testados localmente).
5. **Requisitos de instalação:** Binário `typst` ou pacote PyPI `typst`/`touying`; acesso à rede no primeiro download de pacotes `@preview/...`.
6. **Comandos de instalação/configuração:** `winget install --id Typst.Typst` (Camada 2) ou teste efêmero `uv run --with touying ...`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (`Apache-2.0` Typst / `MIT` Touying). Exportação nativa é **PDF**; exportação para PPTX via utilitários como `touying` PyPI ou `typ2pptx` produz conversão indireta/limitada comparada a `python-pptx`.
9. **Maturidade e manutenção:** Alta e em forte crescimento acadêmico (especialmente `Touying` frente ao `Polylux` mais antigo).
10. **Possíveis riscos de segurança:** Baixo.
11. **Vantagens sobre alternativas:** Melhor tipografia matemática e velocidade de compilação para apresentações em PDF e futura escrita técnica sem o peso de gigabytes do TeX Live/Beamer.
12. **Teste simples de verificação:** **Verificado binário ausente** (`typst -> NOT_FOUND`); pacotes `Touying`/`Polylux` e PyPI **consultados via `search_web`**.

### 7.6 `Quarto`
1. **Nome e finalidade:** `Quarto` — sistema científico de publicação que compila Markdown + blocos executáveis Python/R em `revealjs` (HTML), `beamer` (PDF via LaTeX) ou `pptx` (via Pandoc).
2. **Repositório e documentação oficial:** `https://github.com/quarto-dev/quarto-cli` e `https://quarto.org/docs/presentations/`.
3. **Tipo:** CLI Desktop/Sistema (Camada 2).
4. **Compatibilidade com Antigravity:** **Ausente hoje** (`quarto -> NOT_FOUND`); exige instalação permanente (`winget` / `.msi`) + TinyTeX/LaTeX se quiser Beamer PDF.
5. **Requisitos de instalação:** Quarto CLI (embute Pandoc); TinyTeX para PDF Beamer; PowerPoint/LibreOffice recomendado se usar `reference-doc.pptx`.
6. **Comandos de instalação/configuração:** `winget install Posit.Quarto` e `quarto render slides.qmd --to revealjs`.
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (**GPL-2.0**). Limitação conhecida na saída `.pptx`: equações complexas tendem a virar imagens rasterizadas ou exigir ajuste manual, enquanto `revealjs` preserva KaTeX/MathJax e Mermaid nativos.
9. **Maturidade e manutenção:** Altíssima (Posit, padrão ouro em ciência reproduzível).
10. **Possíveis riscos de segurança:** Baixo (cuidado apenas ao renderizar documentos `.qmd` não confiáveis porque executam código).
11. **Vantagens sobre alternativas:** Excelente na **Missão 02+** para gerar slides diretamente ligados a scripts Python de grafeno/DRX/AFM/ML, mas pesado para instalar às pressas para amanhã.
12. **Teste simples de verificação:** **Verificado localmente ausente** (`quarto -> NOT_FOUND`).

### 7.7 `Pandoc` (Construção de Slides)
1. **Nome e finalidade:** `Pandoc` — converte Markdown em slides `beamer` (PDF), `pptx` ou `revealjs`.
2. **Repositório e documentação oficial:** `https://pandoc.org/MANUAL.html#slide-shows`.
3. **Tipo:** Binário CLI (Camada 2).
4. **Compatibilidade com Antigravity:** **Ausente hoje** (`pandoc -> NOT_FOUND`).
5. **Requisitos de instalação:** `pandoc.exe` + distribuição LaTeX (`pdflatex`/`xelatex`) caso o alvo seja Beamer PDF.
6. **Comandos de instalação/configuração:** `pandoc slides.md -t pptx -o slides.pptx` (ou `-t beamer`).
7. **Dependência de APIs ou contas:** Nenhuma.
8. **Custos e limites:** Gratuito (**GPL-2.0**). Controle visual de posicionamento de figuras multi-painel e fluxogramas em `.pptx` é rígido/limitado comparado a `python-pptx` ou `Quarto`/`Marp`.
9. **Maturidade e manutenção:** Altíssima.
10. **Possíveis riscos de segurança:** Muito baixo.
11. **Vantagens sobre alternativas:** Útil como backend (embutido no Quarto), raramente a melhor escolha direta para design visual de seminários científicos.
12. **Teste simples de verificação:** **Verificado localmente ausente** (`pandoc -> NOT_FOUND`).

### Tabela Comparativa Técnica — Categoria 7 (Construção de Apresentações Científicas)

| Critério Técnico | `python-pptx` | `Marp` (`marp-cli`) | `Reveal.js` | `PptxGenJS` | `Typst` (`Touying`) | `Quarto` | `Pandoc` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Equações LaTeX** | Via PNG/SVG `matplotlib` (ou OMML XML manual) | **Nativo** (KaTeX/MathJax em HTML/PDF) | **Nativo** (KaTeX/MathJax) | Não nativo (exige imagem SVG/PNG) | **Nativo** (sintaxe math super-rápida) | **Nativo** (`revealjs`/Beamer); limitado em `.pptx` | Bom em Beamer; limitado em `.pptx` |
| **Figuras Científicas** | **Excelente** (alta DPI direto de Python/artigos) | Muito boa (CSS Grid/Flexbox) | **Excelente** (CSS + zoom/interativo) | Boa (PNG/SVG inseridos) | **Excelente** (vetorial SVG/PDF nativo) | **Excelente** (reproduzível c/ código) | Básica (rígida em `.pptx`) |
| **Fluxogramas** | Formas OOXML nativas ou PNG/SVG de Mermaid/`matplotlib` | Mermaid via plugin/JS ou SVG | **Mermaid / SVG nativo** | Formas PPTX ou PNG/SVG | Pacotes Typst (`fletcher`/`cetz`) ou SVG | **Mermaid / Graphviz nativo** | Requer filtro/imagem externa |
| **Notas do Apresentador** | **Sim** (`notes_slide` nativo no `.pptx`) | **Sim** (`<!-- note -->`, exporta no HTML/PDF notas) | **Sim** (tecla `S`, janela c/ timer) | **Sim** (`slide.addNotes()`) | **Sim** (`Touying` / `pdfpc`) | **Sim** (Reveal.js + `.pptx`) | **Sim** (`::: notes` em Reveal/PPTX) |
| **Editabilidade PPTX vs PDF** | **`.pptx` 100% editável** (PDF requer abrir em PowerPoint/Google Slides) | **PDF excelente**; `.pptx` padrão é **imagem** (`--pptx-editable` exige LibreOffice ausente!) | **HTML/PDF** (`?print-pdf`), sem `.pptx` | **`.pptx` 100% editável** | **PDF vetorial perfeito** (PPTX via `touying` PyPI indireto) | `revealjs` / PDF excelente; `.pptx` restrito | `.pptx` básico / Beamer PDF |
| **Aderência ao Windows 10 Atual (16/11)** | **Máxima (Camada 1 — testado `1.0.2`)** | **Alta p/ PDF/HTML** (`npx` + Chrome local) | **Alta** (`chrome.exe` + Python HTTP) | **Alta** (`node v26.13.0`) | **Baixa/Média** (binário ausente; PyPI não testado) | **Baixa hoje** (`quarto` e LaTeX ausentes) | **Baixa hoje** (`pandoc` ausente) |

**Ranking Técnico — Categoria 7:**
1. **`python-pptx` (Camada 1 — testado)** — Melhor escolha para gerar `.pptx` editável de última hora compatível com PowerPoint/Google Slides na sala de aula da UFCA, combinando figuras matplotlib/artigos e notas do apresentador.
2. **`Marp` (`@marp-team/marp-cli` via `npx` + Chrome local)** — Melhor escolha se o pesquisador aceitar apresentar em **PDF/HTML** (excelente LaTeX + CSS rápido em Markdown; lembre-se de que `--pptx-editable` está bloqueado pela falta do LibreOffice).
3. **`Reveal.js`** — Melhor para apresentações web/PDF altamente interativas com equações e Mermaid, sem dependência de instalação.
4. **`Quarto`** — Melhor arquitetura de **médio prazo (Missão 02/dissertação)** após instalação na Camada 2.
5. **`Typst` (`Touying`)** — Melhor substituto moderno ao LaTeX Beamer para PDFs matemáticos rápidos (Camada 2).
6. **`PptxGenJS`** — Alternativa sólida em Node ao `python-pptx`, mas menos sinérgica com scripts científicos Python.
7. **`Pandoc`** — Útil como peça de conversão textual, inferior como motor isolado de slides visuais.

---

## 8. Orquestração no Antigravity

### 8.1 `/swarm` (`native_swarm`)
1. **Nome e finalidade:** `/swarm` — sistema nativo de múltiplos agentes em conversas paralelas colaborando por um quadro de mensagens compartilhado (*message board*) com papéis de coordenador, workers, revisor crítico, `narrator` e `monitor`.
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\antigravity\builtin\skills\native_swarm\SKILL.md` e `config.json` (`"swarm": {"enabled": true}`).
3. **Tipo:** Orquestrador Nativo Antigravity (Plugin/Skill Built-in).
4. **Compatibilidade com Antigravity:** **Nativa e ativa hoje** (Camada 0 — é o mecanismo executando esta própria Missão 01!).
5. **Requisitos de instalação:** Já habilitado.
6. **Comandos de instalação/configuração:** Acionamento pelo usuário com `/swarm` ou chamadas do coordenador via ferramentas `swarm`, `post_message`, `read_board`, `swarm_wait`.
7. **Dependência de APIs ou contas:** Consome cota de tokens/modelo de cada worker ativo (workers em `swarm_wait` não consomem tokens).
8. **Custos e limites:** Marcado como *(Preview & Quota Heavy)* na própria documentação; cada `@menção` acorda um worker e consome turno. Suporta `workspace:"share"`/`"branch"` para isolamento de edição paralela (sem `git`, o trabalho exige propriedade exclusiva estrita por arquivo!).
9. **Maturidade e manutenção:** Built-in oficial do Antigravity `1.5.9`.
10. **Possíveis riscos de segurança e coordenação:** Conflito de escrita se dois workers editarem o mesmo arquivo (mitigado por **propriedade exclusiva explícita**); risco de consumo rápido de cota se o enxame for grande demais.
11. **Vantagens sobre alternativas:** Permite **revisão crítica entre pares** (`@revisor-critico` auditando e devolvendo correções aos autores) e paralelismo real em tarefas longas com divisão de especialidades (como na Missão 02: Bibliografia + Materiais + Slides + Revisor).
12. **Teste simples de verificação:** **Verificado localmente em produção** (`read_board`, `native_swarm/SKILL.md` e `config.json`).

### 8.2 `run_workflow`
1. **Nome e finalidade:** `run_workflow` — executa um script Python dinâmico de orquestração determinística usando as primitivas `agent()`, `parallel()`, `pipeline()`, `phase()`, `call_tool()` e `trajectory()`, com validação obrigatória de saída por **JSON Schema** (`finish`).
2. **Repositório e documentação oficial:** `C:\Users\emer\.gemini\antigravity\builtin\skills\run-workflow\SKILL.md`.
3. **Tipo:** Ferramenta/Skill Built-in de orquestração programática.
4. **Compatibilidade com Antigravity:** Nativa, **PORÉM COM ALERTA CRÍTICO NESTE WINDOWS 10**: a documentação (`SKILL.md` linha 43–44) declara que *"The script runs in its own `python3` process, which needs Python 3.8 or later on `PATH`"*. Hoje, `where python3` aponta para `C:\Users\emer\AppData\Local\Microsoft\WindowsApps\python3.exe` (stub 0.0.0.0), **não** para `C:\Users\emer\.local\bin\python3.11.exe`! Portanto, `run_workflow` pode falhar enquanto um Python real não estiver como `python3` no `PATH` (ou precisar validação explícita antes de depender dele).
5. **Requisitos de instalação:** Python `>= 3.8` real acessível como `python3` no `PATH`.
6. **Comandos de instalação/configuração:** Chamada da ferramenta `run_workflow(Script=..., Description=...)` ou `ScriptPath=...`.
7. **Dependência de APIs ou contas:** Consome cota dos agentes disparados (permite `model="flash_lite"`/`"flash"` para fan-out leve).
8. **Custos e limites:** Em `parallel()`, a falha de um agente cancela os demais; agentes não têm acesso ao diálogo com o usuário para pedir aprovação interativa.
9. **Maturidade e manutenção:** Built-in oficial do Antigravity.
10. **Possíveis riscos de segurança:** Baixo; chamadas de ferramentas sem permissão pré-concedida são negadas com `ToolError`.
11. **Vantagens sobre alternativas:** Ideal para **pipelines em lote/determinísticos** (ex.: processar e fichar 25 artigos em paralelo retornando JSON validado por schema), superando `/swarm` quando não há necessidade de debate livre no quadro.
12. **Teste simples de verificação:** **Risco diagnosticado localmente** (`SKILL.md` lido + `where python3` apontando apenas para stub WindowsApps).

### 8.3 `invoke_subagent` (e `send_message`)
1. **Nome e finalidade:** `invoke_subagent` — delega uma sub-tarefa isolada e pontual a um subagente dedicado (ou customizado), comunicando-se via `send_message` sem abrir um message board nem criar scripts Python.
2. **Repositório e documentação oficial:** Prompt de sistema `<subagents>` e `agy-customizations` (`agents/*.md`).
3. **Tipo:** Ferramenta nativa de delegação única.
4. **Compatibilidade com Antigravity:** Nativa e ativa hoje (Camada 0), sem depender de `python3` no `PATH` nem abrir infraestrutura de swarm.
5. **Requisitos de instalação:** Nenhum.
6. **Comandos de instalação/configuração:** Invocação direta via ferramenta `invoke_subagent` (ou `define_subagent` temporário na sessão).
7. **Dependência de APIs ou contas:** Cota da sessão Antigravity.
8. **Custos e limites:** Mais econômico que `/swarm` para 1–2 tarefas independentes, porém sem comunicação lateral nativa entre múltiplos subagentes nem painel monitor/narrator.
9. **Maturidade e manutenção:** Built-in oficial Antigravity.
10. **Possíveis riscos de segurança:** Baixo; herda limites de permissão do ambiente.
11. **Vantagens sobre alternativas:** Menor latência e custo de coordenação quando só é preciso isolar contexto de uma leitura pesada (ex.: resumir 1 PDF longo) sem montar enxame completo.
12. **Teste simples de verificação:** **Verificado localmente** pelas especificações nativas do runtime Antigravity nesta sessão.

### Tabela Comparativa e Ranking Técnico — Categoria 8 (Orquestração)

| Posição | Mecanismo | Cenário Ideal | Pronta Hoje? | Cuidado Crítico no Ambiente |
| :---: | :--- | :--- | :---: | :--- |
| **1º** | **`/swarm` (`native_swarm`)** | Trabalho multi-especialidade colaborativo + **Revisor Crítico** | **Sim (Camada 0)** | Definir propriedade exclusiva de arquivo (sem `git` p/ branches) e evitar excesso de `@all` |
| **2º** | **`invoke_subagent`** | Tarefa isolada pontual (ex.: ler documento longo sem sujar contexto) | **Sim (Camada 0)** | Sem interação lateral entre múltiplos subagentes |
| **3º** | **`run_workflow`** | Fan-out determinístico sobre N artigos com JSON Schema | **Com ressalva** | Exige `python3` real no `PATH` (atualmente `where python3` é stub WindowsApps!) |

---

## 9. Ranking Técnico Geral Consolidado (Missão 01 e Missão 02)

Critérios de ordenação: aderência imediata ao Windows 10 atual (16/11/2026), rigor científico (zero alucinação de DOIs/dados), segurança/licenciamento, custo zero e utilidade real para caracterização de grafeno (DRX, MEV, AFM, PDI, ML/VC) + Seminários I amanhã (17/11).

| Ranking | Ferramenta / Tecnologia | Categoria | Camada | Papel Estratégico na Pesquisa |
| :---: | :--- | :---: | :---: | :--- |
| **1º** | **Plugin `science` (`literature_search_openalex` + `literature_search_arxiv`)** | 1 & 2 | **Camada 0** | Descoberta sistemática verificada em Ciência dos Materiais, Física e Visão Computacional |
| **2º** | **OpenAlex + Crossref + Unpaywall (APIs)** | 4 & 6 | **Camada 0** | Validação real de DOIs, citações e geração direta de `.bib` sem alucinação |
| **3º** | **`python3.11.exe` (`3.11.18`) + `SQLite FTS5` (`3.53.1`)** | 5 & 6 | **Camada 0** | Scripting seguro, parsing PPTX/XML, busca lexical BM25 persistente com zero dependências |
| **4º** | **`uv` / `uvx` (`0.13.7`) + `PyMuPDF`/`pymupdf4llm` (`2.1`)** | 5 | **Camada 1** | Conversão ultrarrápida de artigos PDF para Markdown em ambiente efêmero |
| **5º** | **`python-pptx` (`1.0.2`)** | 5 & 7 | **Camada 1** | Inspeção de slides antigos e geração de `.pptx` editável com notas para amanhã |
| **6º** | **`/swarm` (`native_swarm`) + `.agents/skills/`** | 1 & 8 | **Camada 0** | Orquestração auditada (autor + `@revisor-critico`) e skills versionadas do projeto |
| **7º** | **`Marp` (`@marp-team/marp-cli` + Chrome) / `Reveal.js`** | 7 | **Camada 1** | Alternativa superior para equações LaTeX nativas caso a apresentação seja em PDF/HTML |
| **8º** | **Periódicos CAPES (via CAFe/UFCA no navegador)** | 4 | **Manual** | Acesso legal gratuito aos textos integrais pagos (*Carbon*, *ACS Nano*, *Nanotechnology*) |
| **9º** | **`pdfplumber` & `MarkItDown`** | 5 | **Camada 1** | Extração limpa de tabelas PDF e conversão multi-formato sob licença MIT |
| **10º** | **Semantic Scholar API + `zongmin-yu/semantic-scholar-fastmcp-mcp-server`** | 3 & 4 | **Camada 0/2** | Grafos de citação influente e recomendações (após solicitar chave gratuita) |
| **11º** | **`Zotero 7` + `Better BibTeX` (+ `oscardvs/zoteus` ou `cookjohn`)** | 3 & 6 | **Camada 2** | Infraestrutura definitiva de biblioteca e citações da dissertação pós-Seminário I |
| **12º** | **`Docling` / `Marker` / `LanceDB`** | 5 | **Camada 2** | Parsing pesado de tabelas/equações LaTeX e RAG híbrido em disco para corpus amplo |
| **13º** | **`Quarto` / `Typst (Touying)`** | 7 | **Camada 2** | Autoria científica reproduzível e tipografia matemática para futuras qualificações/defesa |
| **14º** | **Plugins `Context7` / `Parallel` / `Tavily`** | 2 | **Camada 2** | Apoio de documentação atualizada de código (Missão 02+) e busca web filtrada |
| **—** | **Não recomendados / Bloqueados hoje:** `Google Scholar` scraping (ToS/CAPTCHA), `openags/paper-search-mcp` c/ Sci-Hub ativo, `GROBID` (sem Java/Docker), `AnnaSuSu/arxiv-mcp` (estagnado), `run_workflow` sem corrigir `python3` no `PATH` | 3, 4, 5, 8 | — | Risco jurídico/anti-bot, bloqueio de binário ausente ou redundância |
