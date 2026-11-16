# Plano de Instalação e Ativação em 3 Camadas — Missão 01 (PPGCEM/UFCA)

**Data:** 16/11/2026 (véspera da apresentação de Seminários I em 17/11/2026)  
**Princípio operacional:** Proteger o prazo de amanhã mantendo o sistema Windows 10 limpo e estável. Nenhuma ferramenta global foi instalada, `C:\Users\emer\.gemini\config\mcp_config.json` não foi alterado (permanece com `0` bytes) e nenhuma credencial foi gravada em `~/.env` durante a Missão 01.  
**Autoria:** `@agente-ferramentas` (propriedade exclusiva deste documento; ver análise detalhada das ferramentas em [02_skills_plugins_mcp.md](file:///c:/Users/emer/dissertacao/Missao1/preparacao_ambiente/02_skills_plugins_mcp.md)).

---

## Visão Geral da Estratégia em 3 Camadas

| Camada | Natureza | Altera o Sistema? | Quando Usar |
| :--- | :--- | :---: | :--- |
| **Camada 0 — Zero-Install** | Recursos já ativos no Antigravity, `python3.11.exe`, `uv`, `node/npx`, Chrome e APIs abertas | **Não** | **Hoje (16/11) e imediatamente na Missão 02** |
| **Camada 1 — Efêmera** | Pacotes executados sob demanda em cache isolado via `uv run --with ...` e `npx ...` | **Não** (cache temporário local) | **Hoje (16/11) e Missão 02** (leitura de PDFs, geração de slides `.pptx`/PDF) |
| **Camada 2 — Permanente** | `~/.env`, servidores MCP, plugins Marketplace e apps desktop (`Zotero 7`, `Git`, `Quarto`/`Typst`, etc.) | **Sim** (requer aprovação explícita) | **Somente após aprovação do pesquisador** (maioria recomendada pós-17/11) |

---

## Camada 0 — Zero-Install (Já Ativa e Pronta Hoje)

Todos os componentes abaixo foram **verificados empiricamente nesta sessão** e funcionam imediatamente sem instalar absolutamente nada:

### 1. Plataforma Antigravity e Customizações Ativas
- **Antigravity CLI / Runtime:** `agy 1.5.9`.
- **Plugins instalados e ativos** (`C:\Users\emer\.gemini\config\config.json`):
  - `science` (`v1.4.0`) — 48 skills (destaque para `literature_search_openalex`, `literature_search_arxiv`, `literature_search_europepmc`, `literature_search_biorxiv`, `pubmed_database`, `credentials`, `uv`, `workflow_skill_creator`, `biomolecular_structure_viewer`) + MCP sidecar `biomolecular_structure_viewer_mcp`.
  - `google-antigravity-sdk` (`v0.0.9`).
  - `swarm` (`enabled: true`).
- **Skills globais em `C:\Users\emer\.gemini\config\skills\`:** `optimize-tokens` e `plan-token-optimization`.
- **Skills built-in:** `/swarm` (`native_swarm`), `invoke_subagent`, `generative_ui`, `agy-customizations`, `plugin`, `automation`, entre outras.
- **Arquivos de licença pré-registrados no workspace:** `c:\Users\emer\dissertacao\Missao1\.licenses\` já contém `literature_search_openalex_LICENSE.txt`, `literature_search_arxiv_LICENSE.txt` e `literature_search_europepmc_LICENSE.txt`.

### 2. Runtimes e Ferramentas Locais Prontos
- **Python 3.11.18 real:** `C:\Users\emer\.local\bin\python3.11.exe`
  - **SQLite FTS5 nativo:** verificado `sqlite_version: 3.53.1` com `ENABLE_FTS5` ativo — pronto para busca lexical BM25 persistente em disco com zero dependências.
  - **Biblioteca padrão:** `zipfile`, `xml.etree.ElementTree`, `urllib.request`, `json` (suficientes para auditar `.pptx`, consultar Crossref/Unpaywall/SciELO e gerar `.bib` verificável).
- **Gerenciador Python `uv` / `uvx`:** `0.13.7` (`316c827e0 2026-11-03 x86_64-pc-windows-msvc`).
- **Node.js / npx:** `node v26.13.0` / `npx 11.20.0`.
- **Google Chrome:** `C:\Program Files\Google\Chrome\Application\chrome.exe` (útil para renderizar HTML/Reveal.js e exportar PDF).

### 3. Regras de Ouro de Execução no PowerShell 5.1 Atual
1. **Evite os stubs do WindowsApps:** `where python` e `where python3` retornam apenas `C:\Users\emer\AppData\Local\Microsoft\WindowsApps\python*.exe`. Sempre invoque explicitamente:
   ```powershell
   & "C:\Users\emer\.local\bin\python3.11.exe" --version
   ```
2. **Nunca coloque `python` após `uv run` ao executar scripts das Science Skills:** colocar `python` antes do arquivo ignora o bloco PEP 723 (`# /// script`) de dependências!
   ```powershell
   # CORRETO: uv resolve polite-http e python-dotenv automaticamente
   uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" --help

   # INCORRETO: ignora o cabeçalho PEP 723
   # uv run python "C:\Users\emer\...\openalex_cli.py" --help
   ```
3. **Economize o orçamento keyless do OpenAlex:** enquanto `OPENALEX_API_KEY` não estiver definida em `~/.env`, todas as requisições sem chave compartilham `$0.10/dia` por IP. Sempre usar `--select` e `--per-page 5` ou `10`, redirecionando saídas longas para arquivo antes de ler.

---

## Camada 1 — Execução Efêmera (Sem Instalações Permanentes)

Usa `uv run --with ...` e `npx ...` para carregar bibliotecas apenas em cache temporário isolado, **sem** executar `pip install`, `npm install -g`, `uv tool install` ou `winget`.

### 1. Checagens Leves Já Comprovadas Empiricamente Nesta Sessão (16/11/2026)

1. **Extração rápida de PDF para Markdown (`PyMuPDF` / `pymupdf4llm`):**
   ```powershell
   uv run --with pymupdf4llm python -c "import pymupdf4llm; print(pymupdf4llm.__file__)"
   ```
   - **Resultado verificado hoje:** `Installed 12 packages in 829ms` no cache efêmero `C:\Users\emer\AppData\Local\uv\cache\archive-v0\...`; importação validada com `pymupdf: 2.1` e `pymupdf4llm: 2.1`.

2. **Leitura e geração nativa de slides editáveis (`.pptx`) (`python-pptx`):**
   ```powershell
   uv run --with python-pptx python -c "import pptx; print(pptx.__version__)"
   ```
   - **Resultado verificado hoje:** `Installed 5 packages in 233ms` no cache efêmero; imprimiu `python-pptx: 1.0.2`.

3. **CLIs locais do plugin `science` (`--help`):**
   - `openalex_cli.py --help` (código `0`), `search_arxiv.py --help` (código `0`), `europepmc_api.py --help` (código `0`), `pubmed_api.py --help` (imprimiu as 10 funções disponíveis; retorno `1` esperado por exigir argumento posicional `<output_file> <func>`).

### 2. Comandos Efêmeros Prontos para a Missão 02 (Documentados / Não Executados Ainda)

- **Converter PDFs científicos baixados (ex.: via arXiv/Unpaywall/CAPES) para Markdown:**
  ```powershell
  uv run --with pymupdf4llm python -c "import pymupdf4llm, pathlib; pathlib.Path('artigo.md').write_text(pymupdf4llm.to_markdown('artigo.pdf'), encoding='utf-8')"
  ```
- **Extrair tabelas experimentais precisas de DRX/MEV/AFM em PDF (licença MIT):**
  ```powershell
  uv run --with pdfplumber python script_tabelas.py
  ```
- **Converter `.pptx` ou `.pdf` simples para Markdown (licença MIT):**
  ```powershell
  uv run --with "markitdown[pdf,pptx]" markitdown entrada.pptx -o saida.md
  ```
- **Gerar apresentação `.pptx` editável com figuras científicas e notas do apresentador:**
  ```powershell
  uv run --with python-pptx --with matplotlib python gerar_seminario.py
  ```
- **Gerar apresentação em PDF/HTML via Markdown + KaTeX com `Marp` (usando o Chrome já instalado):**
  ```powershell
  npx -y @marp-team/marp-cli slides.md --pdf --allow-local-files -o slides.pdf
  ```
  *(Aviso: **não** passar `--pptx-editable` hoje, pois depende do LibreOffice ausente nesta máquina; sem ele, `--pptx` gera slides como imagem estática).*
- **Busca lexical/híbrida efêmera adicional (caso o `SQLite FTS5` da Camada 0 precise de complemento vetorial):**
  ```powershell
  uv run --with lancedb --with fastembed python indexar_corpus.py
  ```

---

## Camada 2 — Instalações Permanentes, Credenciais e MCPs (Sujeita à Aprovação Explícita)

Nenhuma das ações desta camada deve ser executada sem autorização explícita do usuário.

### 2A. Configuração Segura de `~/.env` (Protocolo `credentials`)

Atualmente `C:\Users\emer\.env` (`$env:USERPROFILE\.env`) encontra-se vazio (`0` bytes) — **nenhuma chave está configurada** (`OPENALEX_API_KEY` = `False`, `USER_EMAIL` = `False`).

**Regras de segurança obrigatórias (`credentials/SKILL.md`):**
- **NUNCA** colar chaves de API no chat da conversa nem rodar `cat ~/.env`, `Get-Content ~/.env`, `echo $env:VAR` ou `printenv`.
- Verificar presença **apenas** em modo silencioso/booleano antes de rodar scripts:
  ```powershell
  # PowerShell 5.1 (retorna apenas True ou False, sem exibir valores)
  if (Test-Path "$env:USERPROFILE\.env") { Select-String -Path "$env:USERPROFILE\.env" -Pattern "^OPENALEX_API_KEY=" -Quiet } else { $false }
  ```
  *(Em Bash/WSL equivalente da skill: `grep -sq "^OPENALEX_API_KEY=" ~/.env`.)*

**Como o pesquisador deve gravar as chaves localmente (sem expor ao agente):**
Execute no seu próprio terminal PowerShell (a digitação ficará oculta por `-AsSecureString`):

```powershell
# Template seguro em PowerShell 5.1 para gravar variável em ~/.env sem exibir na tela
function Add-EnvSecret {
    param([Parameter(Mandatory=$true)][string]$Name)
    $sec = Read-Host "Digite o valor de $Name (digitacao oculta)" -AsSecureString
    $ptr = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sec)
    try {
        $plain = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($ptr)
        $envPath = Join-Path $env:USERPROFILE ".env"
        Add-Content -Path $envPath -Value "$Name=$plain" -Encoding UTF8
        Write-Host "$Name salvo com seguranca em $envPath."
    } finally {
        [System.Runtime.InteropServices.Marshal]::ZeroFreeBSTR($ptr)
    }
}

# Exemplo de uso (execute apenas para as chaves que desejar cadastrar):
Add-EnvSecret -Name "USER_EMAIL"
Add-EnvSecret -Name "OPENALEX_API_KEY"
```

*(Equivalente POSIX/Git Bash previsto originalmente em `credentials/SKILL.md` caso use Bash:)*
```bash
printf "Enter OPENALEX_API_KEY (typing hidden): " && read -s val && echo && echo "OPENALEX_API_KEY=$val" >> "$HOME/.env" && echo "Saved."
```

**Onde obter gratuitamente as variáveis recomendadas:**

| Variável em `~/.env` | Obrigatória? | Onde Obter (Gratuito) | Benefício Prático |
| :--- | :---: | :--- | :--- |
| `USER_EMAIL` | Recomendada | Seu e-mail institucional UFCA ou pessoal | Ativa Polite Pool no Crossref (`10 req/s`), libera Unpaywall (obrigatório) e identifica chamadas NCBI |
| `OPENALEX_API_KEY` | Recomendada | Conta gratuita em `https://openalex.org/` → *Account Settings* | Eleva cota de `$0.10/dia` (IP compartilhado) para **`$1.00/dia`** (`30 req/s`) e habilita `download-pdf` em `content.openalex.org` |
| `SEMANTIC_SCHOLAR_API_KEY` | Opcional | Solicitação gratuita em `https://www.semanticscholar.org/product/api` | Garante **`1 req/s` dedicado** sem sofrer HTTP 429 do pool anônimo compartilhado |
| `NCBI_API_KEY` | Opcional | `https://www.ncbi.nlm.nih.gov/account/settings/` | Eleva PubMed de `3 req/s` para `10 req/s` |

---

### 2B. Snippet Ilustrativo de `C:\Users\emer\.gemini\config\mcp_config.json`

> [!IMPORTANT]
> **Este bloco é apenas ilustrativo para referência futura.** Não edite nem sobrescreva `C:\Users\emer\.gemini\config\mcp_config.json` sem aprovação explícita, e substitua os placeholders antes de usar.

Observações críticas para Windows 10 neste ambiente:
1. O Antigravity suporta transportes **Stdio** (`command`/`args`/`env`) e **Streamable HTTP** (`url`), **não** HTTP+SSE legado (`/sse`).
2. Usar sempre `"command": "uvx"` ou `"npx"` (jamais `"python"` ou `"python3"`, devido aos stubs WindowsApps!).
3. **Atenção:** só ative servidores Zotero (`zoteus` ou `zotero-mcp`) **depois** de instalar o Zotero 7 Desktop (ou use `kaliaboi/mcp-zotero` somente se mantiver biblioteca sincronizada na nuvem Zotero).
4. **Evite** ativar `openags/paper-search-mcp` com fallback de Sci-Hub/Google Scholar habilitado e **evite** `docling-mcp[local]` antes de confirmar ~10–20 GB livres em disco e RAM suficiente.

```json
{
  "mcpServers": {
    "arxiv": {
      "command": "uvx",
      "args": [
        "arxiv-mcp-server",
        "--storage-path",
        "C:\\Users\\emer\\dissertacao\\corpus_arxiv"
      ]
    },
    "semantic-scholar": {
      "command": "uvx",
      "args": [
        "semantic-scholar-fastmcp-mcp-server"
      ],
      "env": {
        "SEMANTIC_SCHOLAR_API_KEY": "<PREENCHER_CHAVE_SEMANTIC_SCHOLAR>"
      }
    },
    "zoteus-opcional-pos-zotero7": {
      "command": "npx",
      "args": [
        "-y",
        "@oscardvs/zoteus"
      ]
    },
    "zotero-plugin-http-alternativo": {
      "url": "http://127.0.0.1:23120/mcp"
    }
  }
}
```
*(Nota: escolha **apenas um** conector Zotero caso instale o Zotero 7 — `zoteus` via `npx` OU `cookjohn/zotero-mcp` via Streamable HTTP na porta `23120` — e note que o plugin `science` já atende buscas arXiv sem precisar do MCP `arxiv-mcp-server`.)*

---

### 2C. Plugins do Antigravity Marketplace (Via UI / Aprovação do Usuário)

Regra da plataforma: nunca editar `C:\Users\emer\.gemini\config\config.json` manualmente; instalar pela aba **Customizations > Marketplace** na interface (ou `<plugin-card>` quando solicitado):
1. `antigravity-plugins-partners/plugin/context7` — útil na Missão 02+ para documentação atualizada de código (`python-pptx`, `scikit-image`, `PyTorch`).
2. `antigravity-plugins-partners/plugin/parallel` (gratuito sem chave) ou `antigravity-plugins-partners/plugin/tavily` (1.000 créditos/mês gratuitos) — busca e leitura web limpa quando precisar ir além das APIs científicas.
3. `antigravity-plugins-official/plugin/gslides` / `gdocs` — opcional apenas se optar por fluxo Google Slides (exige login OAuth Google).
4. `antigravity-plugins-official/plugin/chrome-devtools-plugin` — opcional para inspecionar slides HTML/`Reveal.js` no Chrome local.

---

### 2D. Aplicativos e Ferramentas de Sistema (Pós-Seminário I — Dissertação PPGCEM)

Comandos recomendados **apenas para execução pós-17/11/2026 após aprovação do usuário** (todos ausentes hoje no `PATH`):

| Ferramenta | Prioridade | Método Sugerido (Windows 10) | Finalidade na Dissertação |
| :--- | :---: | :--- | :--- |
| **Zotero 7 + Better BibTeX** | **Alta (Pós-17/11)** | `winget install --id DigitalScholar.Zotero` + `.xpi` BBT | Gestão de PDFs, anotações e `.bib` auto-atualizável |
| **Git** | **Alta (Pós-17/11)** | `winget install --id Git.Git` | Versionamento seguro do código, `.bib` e textos da dissertação (e habilita `workspace:"branch"` em swarms) |
| **Correção de `python3` no `PATH` (opcional)** | **Média** | Desativar *App Execution Aliases* (`python.exe`/`python3.exe`) nas Configurações do Windows e manter `C:\Users\emer\.local\bin` no `PATH` | Desbloqueia `run_workflow` (que exige `python3 >= 3.8` no `PATH`) |
| **Quarto** | **Média** | `winget install --id Posit.Quarto` | Slides reproduzíveis e relatórios científicos Python + Markdown |
| **Typst** | **Média** | `winget install --id Typst.Typst` | Tipografia matemática leve (`Touying` para slides PDF / textos sem TeX Live completo) |
| **JabRef (alternativa ao Zotero)** | **Baixa** | `winget install --id JabRef.JabRef` (já inclui JRE próprio) | Edição direta de `.bib` em texto plano |
| **Pandoc / LibreOffice** | **Baixa** | `winget install --id JohnMacFarlane.Pandoc` / `TheDocumentFoundation.LibreOffice` | Conversões `.md ↔ .docx` ou `--pptx-editable` no Marp |
| **Docker Desktop (para GROBID)** | **Opcional/Pesada** | `winget install --id Docker.DockerDesktop` | Apenas se construir pipeline massivo de mineração bibliográfica TEI XML em centenas de PDFs |

### O que **NÃO** Instalar Hoje (16/11/2026 — Véspera do Seminário)
1. **Docker Desktop / GROBID / Java JDK:** consumo alto de tempo, RAM e risco de reinicialização do Windows às vésperas da apresentação.
2. **TeX Live / MiKTeX completo:** gigabytes de download desnecessários hoje quando `python-pptx` (Camada 1) e `Marp`/Chrome funcionam imediatamente.
3. **Docling local (`docling-mcp[local]`) / Marker:** download de vários GBs de modelos ML e lentidão em CPU sem GPU antes da entrega imediata.
4. **Zotero MCPs (`zoteus`, `cookjohn`, `kaliaboi`, etc.):** inúteis hoje sem Zotero 7 instalado ou conta sincronizada.

---

### 2E. Checklist de Aprovação Explícita para o Pesquisador

| Item Proposto | Camada | Altera Sistema / Disco? | Recomendação de Momento | Decisão do Usuário |
| :--- | :---: | :---: | :--- | :---: |
| Usar `science` + `python3.11` + `SQLite FTS5` | **0** | Não | **Ativo agora** | `[x] Pronto` |
| Usar `uv run --with pymupdf4llm` e `python-pptx` | **1** | Cache efêmero `uv` | **Ativo agora / Missão 02** | `[ ] Confirmar uso na Missão 02` |
| Preencher `~/.env` com `USER_EMAIL` e `OPENALEX_API_KEY` | **2A** | Escreve credenciais em `~/.env` | **Antes da busca sistemática (Missão 02)** | `[ ] Aprovar` |
| Solicitar `SEMANTIC_SCHOLAR_API_KEY` | **2A** | Adiciona chave ao `~/.env` | **Opcional Missão 02** | `[ ] Aprovar` |
| Instalar plugins Marketplace (`context7`, `parallel`/`tavily`) | **2C** | Config Antigravity via UI | **Missão 02+** | `[ ] Aprovar via UI` |
| Instalar Zotero 7 + Better BibTeX + Git | **2D** | Instalação Windows | **Pós-Seminário I (após 17/11)** | `[ ] Aprovar pós-17/11` |
| Configurar `mcp_config.json` (Zotero/S2/arXiv) | **2B** | Edita `mcp_config.json` | **Pós-Zotero 7 / pós-17/11** | `[ ] Aprovar pós-17/11` |
| Corrigir aliases `python.exe`/`python3.exe` no Windows | **2D** | Config Windows | **Pós-17/11 (se usar `run_workflow`)** | `[ ] Aprovar pós-17/11` |
