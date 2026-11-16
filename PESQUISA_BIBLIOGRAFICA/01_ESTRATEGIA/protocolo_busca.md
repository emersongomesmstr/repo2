# Protocolo de Busca Bibliográfica — Missão 02 (PPGCEM/UFCA)

**Projeto de dissertação:** Viabilidade de ferramenta computacional para apoiar a caracterização de grafeno e materiais relacionados utilizando dados experimentais de Difração de Raios X (DRX/XRD), Microscopia Eletrônica de Varredura (MEV/SEM) e Microscopia de Força Atômica (AFM)  
**Pesquisador:** Emerson de Sousa Gomes | **Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
**Instituição / Disciplina:** PPGCEM/UFCA — Seminários I  
**Data da execução e auditoria:** 16/11/2026 (`2026-11-16`, véspera da apresentação em 17/11/2026)  
**Responsável pelo protocolo:** Agente A (Física do Grafeno + Estratégia de Busca)

---

## 1. Natureza Metodológica da Revisão

> [!IMPORTANT]
> **Revisão Crítica Narrativa Estruturada (não PRISMA formal):** Em conformidade estrita com a Seção 5 do [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md), esta pesquisa bibliográfica caracteriza-se como uma **revisão crítica narrativa estruturada e rastreável**, e **não** como uma revisão sistemática formal sob protocolo PRISMA completo. Embora adote consultas booleanas reprodutíveis, registro de contagens por consulta, critérios explícitos de elegibilidade, auditoria de preprints e verificação cruzada de metadados/DOIs, não houve triagem duplicada cega em escala populacional de milhares de resumos nem avaliação psicométrica formal de viés com diagrama PRISMA exaustivo.

Os objetivos do protocolo são:
1. Mapear fundamentos físicos estabelecidos do grafeno, óxido de grafeno (GO), óxido de grafeno reduzido (rGO) e grafite (Eixo A);
2. Delimitar o alcance físico e as restrições não intercambiáveis de DRX, MEV e AFM, bem como a dependência de técnicas complementares como espectroscopia Raman, TEM e XPS (Eixo B);
3. Identificar métodos computacionais (PDI clássico, visão computacional, aprendizado de máquina/profundo) e softwares abertos validados para difratogramas e micrografias (Eixos C e D);
4. Diagnosticar lacunas científicas, riscos de *data leakage* e *domain shift*, e orientar decisões metodológicas realistas para a dissertação (Eixo E).

---

## 2. Bases Bibliográficas, APIs Consultadas e Políticas de Uso

As consultas foram conduzidas combinando habilidades (*skills*) oficiais do ambiente (`science v1.4.0`) e consultas HTTP GET somente leitura às APIs abertas de registro de DOIs, respeitando integralmente os termos de uso registrados na pasta `.licenses/`:

- Termos OpenAlex: [`literature_search_openalex_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_openalex_LICENSE.txt) (`https://help.openalex.org/`)
- Termos arXiv: [`literature_search_arxiv_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_arxiv_LICENSE.txt) (`https://info.arxiv.org/help/api/index.html`)
- Termos Europe PMC: [`literature_search_europepmc_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_europepmc_LICENSE.txt) (`https://europepmc.org/`)

| Base / Serviço | Interface / Método de Acesso | Função no Protocolo | Limites Observados e Controles Aplicados em 16/11/2026 |
| :--- | :--- | :--- | :--- |
| **OpenAlex** | Skill `literature-search-openalex` (`uv run .../openalex_cli.py`) | Busca booleana estruturada (`filter works`), contagem exata (`meta.count`), metadados completos, localização de OA (`open_access.oa_url`) e resolução gratuita por DOI (`get works`). | Modo sem chave (`authenticated: false`) com pool diário compartilhado por IP de `$0,10/dia` (`1.000 req/dia`). Na Missão 01 consumiu `$0,0288` (`$0,0987 -> $0,0699`); nesta execução da Missão 02 iniciou com `$0,0617` (`617 req` restantes) e encerrou as consultas do Agente A com `$0,0366` (`366 req` restantes). Priorizou-se `filter works` (`$0,0001/consulta`) com `--select` enxuto e `--per-page 5–10`, evitando `--search` (`$0,001`). **Restrição de sintaxe observada:** OpenAlex retorna HTTP 400 ao tentar `\|` entre campos distintos (ex.: `title.search:A\|title.search:B`); operadores booleanos `OR`/`AND` funcionam dentro de um mesmo campo (`title_and_abstract.search:` ou `title.search:`). |
| **arXiv** | Skill `literature-search-arxiv` (`uv run .../search_arxiv.py` e `download_paper.py`) | Localização de preprints recentes em física da matéria condensada (`cond-mat.mtrl-sci`) e visão computacional/ML (`cs.CV`, `cs.LG`), auditoria de versão/comentários de retirada e download legal de PDFs CC/arXiv. | Gratuito, sem chave, limite rígido de **1 requisição a cada 3 segundos** garantido pelos scripts oficiais. Executado via `subprocess.run` em Python 3.11 para evitar corrupção de aspas pelo PowerShell 5.1 e geração de arquivos em UTF-16LE com `>`. |
| **Europe PMC** | Skill `literature-search-europepmc` (`uv run .../europepmc_api.py`) | Busca em literatura Open Access (`OPEN_ACCESS:y` obrigatório) e confirmação de disponibilidade/PMCID para artigos interdisciplinares (ex.: `QUAM-AFM`, `PMC9942089`). | Gratuito, limite de `1 req/s`. Base focada em ciências da vida e biomedicina: consultas amplas com `"graphene"` retornam maioria de trabalhos biomédicos/toxicológicos, tendo papel secundário/complementar frente a OpenAlex e arXiv. |
| **Crossref REST API** | HTTP GET `https://api.crossref.org/works/<doi>` | Verificação primária de existência de DOIs de periódicos/anais, confirmação de título, periódico, volume, número, páginas/artigo e datas `published-print`/`published-online`. | Gratuito, sem chave, com cabeçalho `User-Agent: PPGCEM-UFCA-BibAudit/1.0`. Retorna HTTP 404 para DOIs com prefixo DataCite (`10.21950/*`, `10.48550/arXiv.*`, `10.5281/*`, `10.14278/*`). |
| **DataCite REST API** | HTTP GET `https://api.datacite.org/dois/<doi>` | *Fallback* obrigatório para validação de DOIs de datasets e preprints arXiv (`10.21950/BFAU11`, `10.48550/arXiv.*`, `10.5281/zenodo.10119370`, `10.14278/rodare.4123`). | Gratuito, sem chave; confirmou HTTP 200 e metadados de publicador/ano para todos os DOIs de repositórios e datasets citados. |
| **Semantic Scholar Graph API** | HTTP GET `https://api.semanticscholar.org/graph/v1/paper/DOI:<doi>` | Consulta pontual por DOI para recuperação complementar de *abstracts* ausentes no OpenAlex. | Endpoint de busca livre (`/paper/search`) retornou **HTTP 429 (`Too Many Requests`)** sem `x-api-key`, inviabilizando buscas em lote; mantido apenas como consulta auxiliar por DOI. |
| **Unpaywall / Google Scholar** | Não automatizados nesta sessão | — | **Unpaywall** retornou `HTTP 422` por ausência de `USER_EMAIL` configurado. **Google Scholar** não possui API oficial e é protegido por CAPTCHA/anti-bot; respeitando as regras de integridade e termos de serviço, **nenhuma raspagem automatizada ou contorno de proteção foi realizado**. |

---

## 3. Fluxo Operacional em Duas Passagens e Estratégia de Encadeamento

Seguindo as Seções 4, 7, 13 e 14 do [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md), o protocolo foi estruturado em etapas sequenciais e auditáveis:

1. **Auditoria prévia de legado (Missão 01 → Missão 02):** inspeção empírica de todas as referências e DOIs herdados de [`pre-projeto-da-selecao.md`](file:///C:/Users/emer/dissertacao/Artigos/Pr%C3%A9%20projeto/pre-projeto-da-selecao.md) e das apresentações anteriores (`Apresentação de Projeto PPGCEM.pptx`, `Apresentação sem título (1).pptx`, `IVEFAC333.pptx`), conforme documentado em [`05_plano_bibliografico.md`](file:///C:/Users/emer/dissertacao/Missao1/preparacao_ambiente/05_plano_bibliografico.md).
2. **Passagem 1 — Pesquisa essencial e recuperação por eixos:** execução das consultas booleanas estruturadas em inglês e português no OpenAlex (`Q-OA-01` a `Q-OA-22`), arXiv (`Q-ARX-01` a `Q-ARX-04`) e Europe PMC (`Q-EPMC-01` a `Q-EPMC-03`), privilegiando tanto artigos seminais quanto publicações até novembro de 2026.
3. **Encadeamento de citações (*citation chaining*) e desdobramento por especialistas:** uso de trabalhos estruturantes (Novoselov 2004; Geim & Novoselov 2007; Castro Neto 2009; Ferrari 2006 / Ferrari & Basko 2013; Backes 2020; Shearer 2016; Holm 2020; Botifoll 2022; Choudhary 2022; Meng 2024; Huang & Gan 2024) para localizar normas, metodologias de histogramas/convolução (Iwashita 2004; Villarrubia 1997; Yao 2016/2017; Chemello 2025; NPL VAMAS 2023) e estudos recentes de ML/CV.
4. **Protocolo de verificação canônica (zero alucinação):** conferência em 5 etapas (normalização de DOI/arXiv ID → Crossref → DataCite/arXiv → OpenAlex `get` → registro de status de leitura). Todos os metadados consolidados constam em [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json) e [`verified_dois.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_dois.json).
5. **Auditoria obrigatória de preprints e retratações/retiradas:** verificação sistemática via OpenAlex (`preprint_to_journal_check.json`), Crossref (`crossref_preprint_check.json`) e API arXiv (`arxiv_preprint_audit.json`, `arxiv_2608_22400v2.json`) para identificar (i) preprints posteriormente publicados em periódicos revisados por pares e (ii) preprints com aviso oficial de retirada (*withdrawn*).
6. **Obtenção legal de textos integrais e rastreabilidade de leitura:** download exclusivo de PDFs Open Access legítimos (`ARTIGOS_PDF/`) com extração de texto para `_scratch/textos_extraidos/`. Nos fichamentos, distingue-se explicitamente quando a análise provém do **texto completo** versus quando se restringe a **resumo e metadados verificados** (casos de periódicos fechados sem acesso institucional CAPES/UFCA na estação local).

---

## 4. Limitações Operacionais Registradas no Ambiente

- **Ausência de `C:\Users\emer\.env` com chaves de API:** manteve OpenAlex no pool sem chave (`$0,10/dia`), impediu acesso autenticado a `content.openalex.org`, bloqueou buscas em lote no Semantic Scholar (`HTTP 429`) e impediu chamadas ao Unpaywall (`HTTP 422`).
- **Acesso restrito a periódicos por assinatura:** artigos sem versão Open Access acessível (como Kauling et al. 2018, Dreyer et al. 2010, Abdelkader et al. 2015, Li et al. 2007, Stobiński et al. 2014, Holzwarth & Gibson 2011, Huang & Gan 2024) foram analisados apenas via metadados e resumos verificados, mantendo pendência de leitura integral via Portal de Periódicos CAPES/UFCA.
- **Armadilha de ambiente Windows 10 / PowerShell 5.1:** `python`/`python3` no `PATH` resolvem para stubs de 0 bytes da Microsoft Store; todas as execuções e scripts foram rodados com `C:\Users\emer\.local\bin\python3.11.exe` e `uv run`, garantindo saída em UTF-8 sem BOM UTF-16LE.

---

## 5. Fontes e URLs de Referência do Protocolo

- [`PROMPT_MESTRE.md`](file:///C:/Users/emer/dissertacao/Artigos/PROMPT_MESTRE.md)
- [`05_plano_bibliografico.md`](file:///C:/Users/emer/dissertacao/Missao1/preparacao_ambiente/05_plano_bibliografico.md)
- [`07_limitacoes.md`](file:///C:/Users/emer/dissertacao/Missao1/preparacao_ambiente/07_limitacoes.md)
- [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json)
- [`preprint_to_journal_check.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/preprint_to_journal_check.json)
- [`crossref_preprint_check.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/crossref_preprint_check.json)
- [`arxiv_preprint_audit.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_preprint_audit.json)
- [`arxiv_2608_22400v2.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_2608_22400v2.json)
- OpenAlex Help & Terms: https://help.openalex.org/
- arXiv API Terms of Use: https://info.arxiv.org/help/api/index.html
- Europe PMC Terms & Search Syntax: https://europepmc.org/
- Crossref REST API: https://api.crossref.org/
- DataCite REST API: https://api.datacite.org/
