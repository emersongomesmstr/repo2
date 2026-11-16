# Missão 01 — Preparação de Ambiente e Auditoria Inicial (PPGCEM/UFCA)

Workspace de trabalho para a preparação da infraestrutura científica da dissertação de mestrado de **Emerson de Sousa Gomes** (PPGCEM/UFCA, orientação do **Prof. Dr. Job Saraiva Furtado Neto**) e organização da apresentação de **Seminários I** (`17/11/2026`).

**Tema atual:** Investigação da viabilidade científica e computacional de ferramenta para caracterização de grafeno e materiais relacionados usando **DRX/XRD**, **MEV/SEM**, **AFM**, **PDI** e **ML/VC** quando cientificamente justificáveis.  
**Estado real do projeto:** **Fase investigativa** — **software NÃO desenvolvido e NÃO validado**.

---

## 1. Guia Rápido dos Arquivos de `preparacao_ambiente/`

- **[Consolidação Estratégica da Missão 01 (`preparacao_ambiente/README.md`)](./preparacao_ambiente/README.md)** — síntese executiva, top ranking de ferramentas, infraestrutura mínima hoje/amanhã, resumo da auditoria e plano para a Missão 02.
- **[`01_inventario.md`](./preparacao_ambiente/01_inventario.md)** — diagnóstico real do Windows 10/hardware/PATH, inventário nativo do Antigravity, auditoria dos documentos originais e linha do tempo do projeto.
- **[`02_skills_plugins_mcp.md`](./preparacao_ambiente/02_skills_plugins_mcp.md)** — avaliação em 12 critérios, tabelas comparativas e ranking técnico de 8 categorias (skills, plugins Marketplace, 12 servidores MCP, APIs acadêmicas, parsers PDF/PPTX/RAG, bibliografia, slides e orquestração).
- **[`03_instalacao.md`](./preparacao_ambiente/03_instalacao.md)** — plano em 3 camadas (Camada 0 Zero-Install, Camada 1 efêmera via `uv run --with` / `npx`, Camada 2 permanente sujeita à aprovação) + protocolo seguro de `~/.env` e snippet ilustrativo de `mcp_config.json`.
- **[`04_arquitetura_agentes.md`](./preparacao_ambiente/04_arquitetura_agentes.md)** — desenho da orquestração dos 6 agentes sobre `/swarm` (com alerta sobre `run_workflow`), diagrama Mermaid, contratos I/O e protocolo anti-alucinação.
- **[`05_plano_bibliografico.md`](./preparacao_ambiente/05_plano_bibliografico.md)** — auditoria de DOIs históricos (incluindo correção de Holm et al., 2020), literatura verificada nos Eixos A–E, prova física de não-intercambiabilidade DRX/MEV/AFM, queries reproduzíveis e fluxo BibTeX.
- **[`06_prioridades_hoje.md`](./preparacao_ambiente/06_prioridades_hoje.md)** — plano tático para `16–17/11/2026`, roteiro de **40–42 min** alinhado aos 6 componentes e 4 critérios de avaliação (`2,5 pts` cada) e cronograma hora a hora.
- **[`07_limitacoes.md`](./preparacao_ambiente/07_limitacoes.md)** — limitações reais do ambiente local/APIs, 5 riscos metodológicos críticos para blindagem na arguição e tabela de rastreabilidade (*verificado empiricamente vs. incerto*).

Diretório auxiliar já registrado no workspace:
- [`.licenses/`](./.licenses/) — avisos de termos de uso gerados para `literature_search_openalex`, `literature_search_arxiv` e `literature_search_europepmc`.

---

## 2. Regras Operacionais e de Rigor Científico

1. **Preservar os originais intactos:** não modificar nem sobrescrever nenhum arquivo em `C:\Users\emer\dissertacao\` (`Apresentacoes_passadas/`, `Disciplinas-Mestrado/`, `Pré projeto/`, `PROMPT.txt`, `Artigos/`).
2. **Nenhuma instalação global ou alteração permanente sem aprovação:** não rodar `pip install`, `npm install -g`, `uv tool install`, `winget`, nem editar `C:\Users\emer\.gemini\config\mcp_config.json` ou gravar chaves em `C:\Users\emer\.env` sem autorização explícita do pesquisador.
3. **Sem slides nesta missão:** a Missão 01 entrega diagnóstico, ranking e plano; os slides de Seminários I serão produzidos somente após a base bibliográfica verificada da Missão 02.
4. **Proibição de sobrepromessa e alucinação:** nunca afirmar que o software está pronto/validado; nunca fabricar DOIs, citações ou resultados experimentais; nunca usar os resultados do piloto `IVEFAC333.pptx` (moléculas orgânicas $\text{C}_6\text{H}_4\text{BrClO}$ em `QUAM-AFM Lite` com divisão 80/20 por arquivo) como validação em grafeno real.
5. **Rigor físico obrigatório:** nunca tratar DRX, MEV e AFM como técnicas intercambiáveis nem alegar que ausência de pico `(002)` no DRX ou espessura aparente no AFM/MEV prova isoladamente monocamada sem calibração e técnicas complementares (como Raman/TEM).
6. **Duração oficial do seminário:** seguir rigorosamente **40 a 45 minutos** conforme [`Seminarios-I-Programa.pdf`](file:///C:/Users/emer/dissertacao/Disciplinas-Mestrado/Seminarios-I-Programa.pdf) (e **não** 60 minutos), cobrindo os 6 componentes do roteiro e os 4 critérios de 2,5 pts.
7. **Regras técnicas deste Windows 10:** usar sempre `uv run` ou `C:\Users\emer\.local\bin\python3.11.exe` (evitar `python`/`python3` do stub WindowsApps); nunca exibir conteúdo de `~/.env` no chat; nunca contornar CAPTCHAs ou fazer scraping no Google Scholar.
