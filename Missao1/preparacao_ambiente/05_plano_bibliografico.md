# 05 — Plano Bibliográfico Científico (Missão 01 — PPGCEM/UFCA)

**Projeto:** Viabilidade científica e metodológica de ferramenta computacional para caracterização de grafeno e materiais relacionados (DRX/XRD, MEV/SEM, AFM, PDI e ML/VC quando cientificamente justificáveis)  
**Instituição / Disciplina:** PPGCEM/UFCA — Seminários I  
**Orientador:** Prof. Dr. Job Saraiva Furtado Neto  
**Data da elaboração:** 16/11/2026 (Seminários I em 17/11/2026)  
**Responsável:** Agente 1 (Bibliografia Científica)

> [!IMPORTANT]
> **Natureza investigativa e trava anti-alucinação:** O software objeto desta dissertação **ainda não foi desenvolvido nem validado**. Este plano bibliográfico documenta exclusivamente artigos, datasets, DOIs, identificadores arXiv, metadados e *abstracts* **empiricamente verificados nesta sessão** via `literature-search-openalex` (`openalex_cli.py`), `literature-search-arxiv` (`search_arxiv.py`), `literature-search-europepmc` (`europepmc_api.py`) e consultas HTTP GET somente leitura às APIs públicas da Crossref, DataCite e Semantic Scholar. Nenhum DOI, citação ou resultado foi fabricado ou inferido de memória.

---

## 1. Fontes, APIs Verificadas e Limitações Reais do Ambiente

Em conformidade com as políticas de uso registradas em [`.licenses/literature_search_openalex_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Missao1/.licenses/literature_search_openalex_LICENSE.txt), [`.licenses/literature_search_arxiv_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Missao1/.licenses/literature_search_arxiv_LICENSE.txt) e [`.licenses/literature_search_europepmc_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Missao1/.licenses/literature_search_europepmc_LICENSE.txt), foram utilizadas as skills instaladas do plugin `science`, complementadas por APIs abertas de metadados.

| Fonte / API | Método Utilizado nesta Sessão | Status Verificado em 16/11/2026 | Custos / Limites Reais Observados | Observações Operacionais Críticas |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAlex** | `uv run .../openalex_cli.py` | **Funcional (sem chave)** | Pool compartilhado por IP: `$0,10/dia` e `1000 req` sem chave (`$0,0987` antes $\rightarrow$ `$0,0699` após consultas; gasto total de `$0,0288`). Com `OPENALEX_API_KEY` gratuita: `$1,00/dia`. | `get` unitário é **gratuito (`$0`)**; `filter` custa `$0,0001` (inclusive lote `doi:a\|b\|...`); `--search` custa `$0,001`. Usar `--select` e `--per-page 5–10`. Não suporta operador `\|` entre campos distintos no mesmo `--filter` (ex.: `title.search:A\|title.search:B` retornou HTTP 400). |
| **Crossref REST API** | HTTP GET `https://api.crossref.org/works/<doi>` e `/transform/application/x-bibtex` | **Funcional (sem chave)** | Gratuito e sem chave; cabeçalho `User-Agent` cortês recomendado. | Resolve DOIs de periódicos/anais e exporta BibTeX direto. **Retorna HTTP 404 para DOIs DataCite** (ex.: `10.21950/BFAU11`, `10.48550/arXiv.2508.04035`), exigindo fallback para DataCite. |
| **DataCite REST API** | HTTP GET `https://api.datacite.org/dois/<doi>` | **Funcional (sem chave)** | Gratuito e sem chave. | Essencial para verificar DOIs de datasets e preprints (`10.21950/*` e-cienciaDatos; `10.48550/arXiv.*`). |
| **arXiv API** | `uv run .../search_arxiv.py` | **Funcional (sem chave)** | Gratuito; limite rígido de **1 requisição a cada 3 s**. | Em PowerShell 5.1, aspas internas escapadas (`\"`) são corrompidas ao invocar `uv.exe`; executar via `subprocess.run` em Python garante preservação exata de frases booleanas. Retorna metadados, `summary` completo e `pdf_url`. |
| **Semantic Scholar Graph API** | HTTP GET `https://api.semanticscholar.org/graph/v1/paper/...` | **Parcial (sem chave)** | `/paper/DOI:...` retornou HTTP 200 com *abstracts*; `/paper/search` retornou **HTTP 429** rapidamente sem `x-api-key`. | Útil como segunda fonte para recuperar *abstracts* ausentes no OpenAlex, mas sujeita a estrangulamento imediato no endpoint de busca sem chave dedicada. |
| **Europe PMC** | `uv run .../europepmc_api.py` | **Funcional (OA obrigatório)** | Gratuito; limite automático de `1 req/s` no script. | Restrito a conteúdo Open Access (`OPEN_ACCESS:y`). Confirmou disponibilidade OA de Carracedo-Cosme et al. (2022) (`PMID 35234034`, `PMCID PMC9942089`). Cobertura focada em ciências biomédicas/computacionais, menor para física/materiais puros. |
| **Unpaywall API** | HTTP GET `https://api.unpaywall.org/v2/<doi>` | **Bloqueado sem e-mail (`HTTP 422`)** | Gratuito, porém exige `?email=USER_EMAIL`. | Teste sem e-mail retornou `HTTP 422: Email address required in API call`. Como `~/.env` não existe e `USER_EMAIL` não está configurado, o roteamento legal de PDFs OA usou `open_access.oa_url` (OpenAlex), `openAccessPdf` (Semantic Scholar) e `pdf_url` (arXiv) nesta missão. |
| **Google Scholar** | Não automatizado | **Não integrável por API** | Sem API oficial; proteções anti-bot/CAPTCHA e restrições nos Termos de Serviço. | **Proibido** contornar CAPTCHAs ou realizar *scraping* automatizado. Uso restrito à conferência manual pontual pelo pesquisador em navegador, nunca como etapa programática de pipeline. |

> [!NOTE]
> **Armadilha de encoding no Windows PowerShell 5.1:** O redirecionamento `>` no PowerShell 5.1 grava arquivos em **UTF-16LE com BOM**, causando `UnicodeDecodeError` em leitores UTF-8 estritos. Na Missão 02, preferir captura via Python (`encoding="utf-8"`) ou `Out-File -Encoding utf8`.

---

## 2. Auditoria Empírica das Referências Citadas no Histórico do Projeto

Foram auditadas todas as referências e DOIs presentes nas apresentações anteriores ([`Apresentação de Projeto PPGCEM.pptx`](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/Apresentação%20de%20Projeto%20PPGCEM.pptx), [`Apresentação sem título (1).pptx`](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/Apresentação%20sem%20título%20(1).pptx), [`IVEFAC333.pptx`](file:///C:/Users/emer/dissertacao/Apresentacoes_passadas/IVEFAC333.pptx)) e no pré-projeto ([`pre-projeto-da-selecao.md`](file:///C:/Users/emer/dissertacao/Pré%20projeto/pre-projeto-da-selecao.md)).

| Citação no Histórico | Onde Aparece | DOI / ID Auditado | Resultado da Verificação Empírica (OpenAlex / Crossref / DataCite / arXiv / S2) | Diagnóstico e Ação Corretiva |
| :--- | :--- | :--- | :--- | :--- |
| **Rosenblatt (1958)** | `IVEFAC333.pptx` (slides 6, 7, 15) | `10.1037/h0042519` | **VERIFICADO** (OA `W2040870580`; CR 200): *The perceptron: A probabilistic model for information storage and organization in the brain.*, *Psychological Review*, v. 65, p. 386–408, 1958 (13.389 citações). | Referência válida (contexto histórico de MLP/CNN; uso opcional/secundário no seminário de materiais). |
| **Binnig, Quate & Gerber (1986)** | `IVEFAC333.pptx` (slide 5; ausente no slide 15) | `10.1103/PhysRevLett.56.930` | **VERIFICADO** (OA `W3150248096`; CR 200): *Atomic Force Microscope*, G. Binnig, C. F. Quate, Ch. Gerber, *Physical Review Letters*, v. 56, p. 930–933, 1986 (15.391 citações; Bronze OA). | Incluir na lista formal de referências (omitida no slide 15 do `IVEFAC333.pptx`). |
| **DeCost & Holm (2015)** | `pre-projeto-da-selecao.md`; `Apresentação de Projeto PPGCEM.pptx` (slide 3) | `10.1016/j.commatsci.2015.08.011` | **VERIFICADO** (OA `W1141054642`; CR 200; S2 200): *A computer vision approach for automated analysis and classification of microstructural image data*, Brian L. DeCost, Elizabeth A. Holm, *Computational Materials Science*, v. 110, p. 126–133, 2015 (345 citações OA; Hybrid OA). | No pré-projeto estava sem ano no texto e sem ano/volume/páginas na lista bibliográfica. Completar metadados. |
| **He et al. (2016)** | `IVEFAC333.pptx` (slides 9, 15) | `10.1109/CVPR.2016.90` | **VERIFICADO** (OA `W2194775991`; CR 200): *Deep Residual Learning for Image Recognition*, Kaiming He et al., *2016 IEEE CVPR*, p. 770–778, 2016 (243.677 citações). | Válido para fundamentação de arquiteturas CNN (ResNet) no Eixo C. |
| **Shearer et al. (2016)** | `IVEFAC333.pptx` (slides 14, 15 — sem DOI no slide 15) | `10.1088/0957-4484/27/12/125704` | **VERIFICADO** (OA `W2275457611`; CR 200; S2 200): *Accurate thickness measurement of graphene*, Cameron J. Shearer et al., *Nanotechnology*, v. 27, n. 12, p. 125704, 2016 (515 citações; Bronze OA). | **Referência central do Eixo B (AFM):** prova variação aparente de 0,4–1,7 nm na monocamada por camada de adsorvato/hidratação e força da ponta. Adicionar DOI explícito. |
| **Holm et al. (2020)** | `pre-projeto-da-selecao.md`; `Apresentação de Projeto PPGCEM.pptx` (slide 3) | **CORRETO:** `10.1007/s11661-020-06008-4` <br> **ERRADO:** `10.1007/s11837-020-04347-6` | **CORRETO VERIFICADO** (OA `W3031142281`; CR 200; S2 200): *Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis*, Elizabeth A. Holm et al., *Metallurgical and Materials Transactions A*, v. 51, n. 12, p. 5985–5999, 2020 (290 citações; Hybrid OA). <br> **ERRADO VERIFICADO** (OA `W3086739661`; CR 200): resolve para *Investigation of the Nanomechanical Properties of Crystalline Anatase Titanium Dioxide Films Synthesized Using Atomic Layer Deposition*, Y. S. Mohammed et al., *JOM*, v. 73, p. 534–540, 2021 (online 2020). | **CORREÇÃO OBRIGATÓRIA:** Nunca utilizar `10.1007/s11837-020-04347-6` (pertence a outro artigo no *JOM*). Usar exclusivamente `10.1007/s11661-020-06008-4`. |
| **Carracedo-Cosme et al. (2021) [Dataset]** | `IVEFAC333.pptx` (slides 10, 11, 15) | `10.21950/BFAU11` | **VERIFICADO** (CR 404 $\rightarrow$ **DataCite 200**): *QUAM-AFM Lite*, Jaime Carracedo-Cosme, Carlos Romero-Muñíz, Pablo Pou, Rubén Pérez, *e-cienciaDatos*, 2021. | Válido exclusivamente para contextualizar o **estudo piloto anterior** em moléculas orgânicas simuladas ($\text{C}_6\text{H}_4\text{BrClO}$), não como dado de grafeno. |
| **Carracedo-Cosme et al. (2022) [Artigo]** | `IVEFAC333.pptx` (slide 15) | `10.1021/acs.jcim.1c01323` | **VERIFICADO** (OA `W4214840389`; CR 200; S2 200; Europe PMC `PMC9942089`): *QUAM-AFM: A Free Database for Molecular Identification by Atomic Force Microscopy*, *Journal of Chemical Information and Modeling*, v. 62, p. 1214–1223, 2022 (19 citações). | Documenta 685.513 moléculas orgânicas em pilhas 3D de AFM simuladas; evidencia o *domain shift* caso comparado diretamente a grafeno esfoliado real. |
| **Ba Alawi (2025)** | `Apresentação sem título (1).pptx` (slides 18–21); `IVEFAC333.pptx` (slides 12, 15) | `10.48550/arXiv.2508.04035` (`arXiv:2508.04035v1`) | **VERIFICADO** (CR 404 $\rightarrow$ **DataCite 200** + `search_arxiv.py`): *A Comparative Survey of PyTorch vs TensorFlow for Deep Learning: Usability, Performance, and Deployment Trade-offs*, Zakariya Ba Alawi, arXiv `cs.LG`, 2025-08-06 (14 pp., 15 figs., 43 refs.). | No slide 15 de `IVEFAC333.pptx` há erro de digitação (`·1 0.48550/arXiv.2508.04035`). Corrigir DOI; lembrar que é preprint de engenharia de *frameworks* (PyTorch vs. TensorFlow), sem relação física com materiais. |
| **van der Walt et al. (2014)** | `pre-projeto-da-selecao.md` (Seção 3.3 e Referências) | `10.7717/peerj.453` | **VERIFICADO** (OA `W2015159529`): *scikit-image: image processing in Python*, Stéfan van der Walt et al., *PeerJ*, v. 2, p. e453, 2014 (7.411 citações; Gold OA). | Válido para referenciar PDI reprodutível em Python no Eixo C. |

*(Nota sobre o pré-projeto: referências a livros-texto e notas técnicas como Callister & Rethwisch 2018, Padilha 2007, Gonzalez & Woods 2018, Szeliski 2022, Gerhardt & Silveira 2009 e Bradski 2000 não foram consultadas via ISBN/catálogo de editora nesta sessão e permanecem pendentes de conferência formal caso sejam citadas na dissertação.)*

---

## 3. Queries Booleanas Reproduzíveis (OpenAlex e arXiv)

Todas as consultas abaixo foram executadas nesta sessão. Para economizar a cota keyless do OpenAlex, priorizou-se `filter works` com `title_and_abstract.search:` / `title.search:` (`$0,0001`/consulta) e `--select` enxuto em vez de `--search` genérico (`$0,001`).

### 3.1 OpenAlex (`openalex_cli.py`)

```powershell
# Eixo A — Clássicos de grafeno e química do óxido de grafeno ($0.0001)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:("Electric Field Effect in Atomically Thin Carbon Films" OR "The rise of graphene" OR "The electronic properties of graphene" OR "The chemistry of graphene oxide")' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8

# Eixo A — Esfoliação eletroquímica de grafite em grafeno ($0.0001)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title_and_abstract.search:graphene AND "electrochemical exfoliation"' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8

# Eixo B (DRX) — Grafeno, GO e grafite por difração de raios X ($0.0001)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:(graphene OR "graphene oxide" OR graphite) AND ("X-ray diffraction" OR XRD)' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8

# Eixo B (MEV) — Contraste e número de camadas de grafeno em MEV ($0.0001)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:graphene AND ("scanning electron" OR "secondary electron" OR SEM) AND (contrast OR layer OR layers OR thickness)' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8

# Eixo B (AFM) — Anomalias de altura e convolução de ponta ($0.0001 cada)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:(graphene OR "2D") AND ("atomic force microscopy" OR AFM) AND (thickness OR height OR tip OR layer)' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8

uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title_and_abstract.search:("tip convolution" OR "tip-sample convolution" OR "tip dilation") AND ("atomic force microscopy" OR AFM)' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 5

# Eixo B (Raman complementar) ($0.0001)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:("Raman spectrum of graphene and graphene layers" OR "Raman spectroscopy as a versatile tool for studying the properties of graphene")' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 5

# Eixo C & D — PDI/ML/CV em microscopia, 2D e DRX ($0.0001 cada)
uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title.search:(graphene OR "2D materials" OR "two-dimensional") AND ("machine learning" OR "deep learning" OR "computer vision") AND (characterization OR identification OR classification OR thickness OR microscopy)' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 10

uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py" filter works `
  --filter 'title_and_abstract.search:("X-ray diffraction" OR XRD) AND ("deep learning" OR "convolutional neural network" OR "machine learning") AND (phase OR crystal OR identification),publication_year:>2018' `
  --sort "cited_by_count:desc" --select "id,doi,display_name,publication_year,cited_by_count,primary_location,open_access,authorships" --per-page 8
```

### 3.2 arXiv (`search_arxiv.py`, executado via Python `subprocess.run`)

1. **Grafeno/2D + ML/CV/Microscopia (relevância):**  
   `(ti:graphene OR ti:"2D material" OR ti:"2D materials") AND (ti:"machine learning" OR ti:"deep learning" OR ti:"computer vision" OR abs:"AFM" OR abs:"SEM" OR abs:"XRD")`
2. **Grafeno/2D + defeitos/interfaces (mais recentes):**  
   `(ti:graphene OR ti:"2D material" OR ti:"2D materials" OR abs:"graphene flakes") AND (abs:"deep learning" OR abs:"machine learning" OR abs:"computer vision" OR abs:"segmentation")`
3. **MEV/AFM + Deep Learning em 2D/microestruturas:**  
   `(abs:"scanning electron microscopy" OR abs:"atomic force microscopy") AND (abs:"deep learning" OR abs:"machine learning") AND (abs:graphene OR abs:"2D" OR abs:microstructure)`
4. **DRX + Deep Learning / Sim-to-Real / Identificação de fases:**  
   `(ti:"X-ray diffraction" OR abs:"X-ray diffraction") AND (abs:"deep learning" OR abs:"machine learning") AND (abs:phase OR abs:crystal OR abs:carbon)`

---

## 4. Literatura Verificada por Eixo Temático (5 Eixos)

### Eixo A — Física e Propriedades do Grafeno, Grafite, GO e rGO

| Referência Verificada | Ano | Periódico / Fonte | DOI / ID | Cit. | Papel no Projeto |
| :--- | :---: | :--- | :--- | :---: | :--- |
| Novoselov et al., *Electric Field Effect in Atomically Thin Carbon Films* | 2004 | *Science*, v. 306(5696), p. 666–669 | `10.1126/science.1102896` | 67.486 | Marco experimental de monocamada de grafeno $sp^2$ estável em condições ambiente. |
| Geim & Novoselov, *The rise of graphene* | 2007 | *Nature Materials*, v. 6(3), p. 183–191 | `10.1038/nmat1849` | 40.337 | Síntese física: dependência eletrônica e estrutural com o número de camadas (monocamada vs. bicamada vs. grafite). |
| Castro Neto et al., *The electronic properties of graphene* | 2009 | *Rev. Mod. Phys.*, v. 81, p. 109 | `10.1103/revmodphys.81.109` | 25.204 | Rede hexagonal em favo de mel ($sp^2$), férmions de Dirac, defeitos e acoplamento entre camadas. |
| Dreyer et al., *The chemistry of graphene oxide* | 2010 | *Chem. Soc. Rev.*, v. 39(1), p. 228–240 | `10.1039/b917103g` | 11.840 | Estrutura química e defeitos oxigenados ($sp^3$) no GO vs. redução parcial para rGO. |
| Parvez et al., *Exfoliation of Graphite into Graphene in Aqueous Solutions of Inorganic Salts* | 2014 | *J. Am. Chem. Soc.*, v. 136(16), p. 6083–6091 | `10.1021/ja5017156` | 1.478 | Rota direta de **esfoliação eletroquímica** ($>85\%$ $\le 3$ camadas, tamanho lateral até $44\ \mu\text{m}$, C/O = 17,2) em eletrólitos inorgânicos. |
| Abdelkader, Cooper & Dryfe, *How to get between the sheets: a review of recent works on the electrochemical exfoliation of graphene materials from bulk graphite* | 2015 | *Nanoscale*, v. 7(16), p. 6944–6956 | `10.1039/c4nr06942k` | 428 | Revisão dos mecanismos de intercalação anódica/catódica, defeitos oxidativos e heterogeneidade de flocos na esfoliação eletroquímica. |
| Backes et al., *Production and processing of graphene and related materials* | 2020 | *2D Materials*, v. 7(2), p. 022001 | `10.1088/2053-1583/ab1e0a` | 517 | Guia padronizado de síntese e caracterização de GRMs; enfatiza que dispersões esfoliadas geram distribuições heterogêneas de tamanho lateral e espessura. |
| Dautov et al., *Green synthesis of graphene oxide via electrochemical exfoliation and its characterization* | 2026 | *Results in Chemistry* | `10.1016/j.rechem.2026.103746` | 1 | Exemplo recente (2026) de esfoliação eletroquímica em $(\text{NH}_4)_2\text{SO}_4\ 0{,}1\ \text{M}$ comparada ao método de Hummers. |
| Costa et al., *Machine-Learning Exploration of Defect Topologies and Thermodynamic Stability in Graphene with Atomic Vacancies* | 2026 | *arXiv* (`cond-mat.mtrl-sci`) | `arXiv:2609.19191v1` | — | Topologias de vacâncias atômicas e estabilidade termodinâmica em grafeno defeituoso. |

### Eixo B — Caracterização Experimental (DRX, MEV, AFM e Complementares)

| Técnica | Referência Verificada | Ano | DOI / ID | Contribuição Física & Evidência Verificada |
| :--- | :--- | :---: | :--- | :--- |
| **DRX/XRD** | Holzwarth & Gibson, *The Scherrer equation versus the 'Debye-Scherrer equation'* (*Nature Nanotechnol.*, v. 6(9), p. 534) | 2011 | `10.1038/nnano.2011.145` | Distingue rigorosamente tamanho de domínio de difração coerente (Scherrer) de tamanho físico de partícula/floco; exige separação de alargamento instrumental e microdeformação. |
| **DRX/XRD** | Li, Lu & Xia, *X-ray diffraction patterns of graphite and turbostratic carbon* (*Carbon*, v. 45(8), p. 1686–1695) | 2007 | `10.1016/j.carbon.2007.03.038` | Modelagem de perfis $(002)$ e bandas assimétricas $(hk)$ em grafite vs. carbono turboestrático desordenado. |
| **DRX/XRD** | Stobiński et al., *Graphene oxide and reduced graphene oxide studied by the XRD, TEM and electron spectroscopy methods* (*J. Electron Spectrosc.*, v. 195, p. 145–154) | 2014 | `10.1016/j.elspec.2014.07.003` | Contraste estrutural entre grafite, GO e rGO integrando DRX, TEM e espectroscopia eletrônica. |
| **DRX/XRD** | Manoj & Kunjomana (*Int. J. Electrochem. Sci.*) & Siburian et al. (*Orient. J. Chem.*) | 2012 / 2018 | `10.1016/s1452-3981(23)13940-x` / `10.13005/ojc/340120` | Extração de $d_{002} \approx 3{,}35\ \text{\AA}$ ($2\theta \approx 26{,}5^\circ$), $L_c$, $L_a$ e número médio de planos empilhados em materiais grafíticos agregados/pós. |
| **MEV/SEM** | Huang & Gan, *A review on SEM imaging of graphene layers* (*Micron*, v. 187, p. 103716) | 2024 | `10.1016/j.micron.2024.103716` | Revisão dedicada ao mecanismo de contraste de elétrons secundários (SE) em camadas de grafeno e sua forte dependência dos parâmetros instrumentais. |
| **MEV/SEM** | Hiura, Miyazaki & Tsukagoshi, *Determination of the Number of Graphene Layers...* (*Appl. Phys. Express*) | 2010 | `10.1143/apex.3.095101` | Relação linear entre intensidade relativa de SE e número de camadas ocorre **somente sob baixa tensão de aceleração** e controle estrito do substrato isolante. |
| **MEV/SEM** | Zhou et al., *Quantitative secondary electron imaging for work function extraction at atomic level and layer identification of graphene* (*Sci. Rep.*, v. 6, 21045) | 2016 | `10.1038/srep21045` | Contraste SE em grafeno ligado à variação da função trabalho entre poucas camadas, exigindo calibração quantitativa específica. |
| **AFM** | Binnig, Quate & Gerber, *Atomic Force Microscope* (*Phys. Rev. Lett.*, v. 56, p. 930–933) | 1986 | `10.1103/PhysRevLett.56.930` | Princípio físico de deflexão da haste por forças de interação ponta–amostra. |
| **AFM** | Nemes-Incze et al., *Anomalies in thickness measurements of graphene and few layer graphite crystals by tapping mode AFM* (*Carbon*, v. 46(11), p. 1435–1442) | 2008 | `10.1016/j.carbon.2008.06.022` | Demonstra variações anômalas na altura aparente de monocamadas no modo *tapping* em função dos parâmetros de varredura e interação com o substrato. |
| **AFM** | Shearer et al., *Accurate thickness measurement of graphene* (*Nanotechnology*, v. 27(12), 125704) | 2016 | `10.1088/0957-4484/27/12/125704` | Mostra valores reportados de **0,4 a 1,7 nm** para monocamada (teórico 0,335 nm) por **camada de adsorvato/hidratação interfacial**, pressão da ponta e parâmetros de *feedback*; PeakForce tapping reduz erro de 0,1–1,3 nm para 0,1–0,3 nm. |
| **AFM** | Villarrubia, *Algorithms for scanned probe microscope image simulation, surface reconstruction, and tip estimation* (*J. Res. NIST*, v. 102(4), p. 425) | 1997 | `10.6028/jres.102.030` | Formaliza matematicamente a **convolução/dilatação geométrica da ponta** (*tip dilation*) distorcendo dimensões laterais na escala nanométrica. |
| **AFM** | Yao et al., *Histogram method for reliable thickness measurements of graphene films using atomic force microscopy (AFM)* (*J. Mater. Sci. Technol.*, v. 33(8), p. 815–820) | 2017 | `10.1016/j.jmst.2016.07.020` | Método estatístico baseado em histogramas de altura em AFM para reduzir viés de leitura pontual na estimativa de espessura de filmes de grafeno. |
| **AFM + Raman** | Obraztsova et al. (*phys. stat. sol. (b)*, v. 245(10), p. 2055–2059) | 2008 | `10.1002/pssb.200879657` | Demonstra que a correlação estatística entre AFM e Raman é necessária para reduzir ambiguidade na contagem de camadas. |
| **Raman (Compl.)** | Ferrari et al. (*PRL*, 2006) & Ferrari & Basko (*Nature Nanotechnol.*, 2013) | 2006 / 2013 | `10.1103/physrevlett.97.187401` / `10.1038/nnano.2013.46` | Padrão-ouro não destrutivo para número de camadas (forma da banda $2D$), densidade de defeitos ($I_D/I_G$), dopagem e tensão mecânica, superando os artefatos de hidratação do AFM. |
| **STEM/STM (Compl.)** | Ziatdinov et al. (*Science Advances*, v. 5(9), eaaw8989) | 2019 | `10.1126/sciadv.aaw8989` | Mapeamento direto de vacâncias atômicas e defeitos pontuais em grafeno monocamada impossíveis de resolver por DRX ou MEV convencional. |

#### Por que DRX, MEV e AFM **NÃO são intercambiáveis** (Rigor Físico Obrigatório)

| Dimensão Analítica | DRX / XRD (Difração de Raios X) | MEV / SEM (Microscopia Eletrônica de Varredura) | AFM (Microscopia de Força Atômica) | Técnicas Complementares Obrigatórias (Raman / TEM) |
| :--- | :--- | :--- | :--- | :--- |
| **Princípio físico** | Interferência construtiva de raios X espalhados por planos cristalinos periódicos (Lei de Bragg: $n\lambda = 2d\sin\theta$). | Interação de feixe de elétrons focalizado com a superfície, coletando elétrons secundários (SE) ou retroespalhados (BSE). | Forças atômicas/intermoleculares (van der Waals, repulsão, capilaridade) entre nanoponta e superfície. | **Raman:** espalhamento inelástico de fótons por fônons ($D, G, 2D$). **TEM:** transmissão e difração eletrônica em escala atômica. |
| **Volume / Escala amostrada** | Média volumétrica de conjunto (*bulk/ensemble* em $\text{mm}^2\text{–cm}^2$); não vê flocos individuais dispersos. | Superficial local ($\text{nm}$ a dezenas de $\mu\text{m}$); campo de visão amplo e rápido. | Topografia local de altíssima resolução vertical ($\text{sub-nm}$ em $Z$) em campos pequenos (tipicamente $\mu\text{m}$); varredura lenta. | **Raman:** ponto confocal ($\sim 0{,}5\text{–}1\ \mu\text{m}$). **TEM:** sub-angstrom local. |
| **Medição de número de camadas ($N$)** | **NÃO mede $N$ em monocamada isolada:** uma única folha 2D não tem periodicidade ao longo do eixo $c$, logo **não produz pico de Bragg $(002)$**. Em pós/agregados, $L_c/d_{002}$ mede apenas espessura média de domínios empilhados coerentes. | **Indireta e frágil:** contraste SE entre 1–4 camadas depende criticamente de baixa kV ($< 5\ \text{kV}$), função trabalho, substrato isolante, detector e contaminação (Hiura 2010; Huang & Gan 2024). | **Direta, porém enviesada:** mede degrau topográfico floco–substrato, mas superestima monocamada ($0{,}4\text{–}1{,}7\ \text{nm}$ vs. $0{,}335\ \text{nm}$) por hidratação/adsorbatos e pressão da ponta (Shearer 2016; Nemes-Incze 2008). | **Raman (padrão-ouro)** distingue $1, 2, 3\ldots$ camadas pelo perfil da banda $2D$ sem viés de adsorvato. |
| **Morfologia lateral e área de flocos** | **Não aplicável** (fornece apenas $L_a$ coerente médio via Scherrer, sem imagem de forma/dobras). | **Técnica primária:** alta profundidade de campo para tamanho lateral, razão de aspecto, bordas, dobras e aglomeração. | Mede dimensões laterais com alta precisão, mas sofre **dilatação/convolução de ponta** em degraus/bordas abruptas (Villarrubia 1997) e baixa vazão amostral. | TEM confirma bordas dobradas e contagem direta de franjas na borda. |
| **Defeitos e oxidação (Grafeno vs. GO vs. rGO)** | Detecta expansão/colapso do espaçamento interplanar $d_{002}$ (grafite $2\theta \approx 26{,}5^\circ \leftrightarrow$ GO deslocado para menor $2\theta$), mas **não distingue vacâncias pontuais nem química superficial direta**. | Sensível a carregamento elétrico (GO isolante carrega sob feixe vs. grafeno condutor), mas não quantifica razão $sp^2/sp^3$ ou C/O sem EDS/XPS. | Detecta rugosidade, furos mesoscópicos e contraste de fase/adesão (ou condutividade local via C-AFM), sem assinatura química elementar. | **Raman ($I_D/I_G$)** quantifica desordem estrutural; **XPS/FTIR** quantifica grupos funcionais C/O. |
| **Papel no sistema computacional viável** | Classificação de fases residuais grafite/GO/rGO, ajuste de picos e estimativa de $d_{002}$ e $L_c$ com incerteza instrumental. | Segmentação automática de flocos e morfometria 2D (área, perímetro, diâmetro equivalente, circularidade) + triagem qualitativa. | Extração automatizada de histogramas de altura (Yao et al., 2017), nivelamento de plano, perfis de degrau e correção geométrica de borda. | Referência de calibração / *ground truth* necessário para treinar ou validar qualquer modelo de ML sobre $N$ camadas ou defeitos. |

### Eixo C — Caracterização Computacional (PDI, Segmentação, Morfometria, ML/CV)

| Referência Verificada | Ano | DOI / ID | Contribuição para PDI / ML / VC |
| :--- | :---: | :--- | :--- |
| Otsu, *A Threshold Selection Method from Gray-Level Histograms* (*IEEE Trans. SMC*, v. 9(1), p. 62–66) | 1979 | `10.1109/tsmc.1979.4310076` | Base clássica de limiarização não supervisionada (útil como *baseline*, mas falha em micrografias com sobreposição de níveis de cinza ou iluminação irregular). |
| van der Walt et al., *scikit-image: image processing in Python* (*PeerJ*, v. 2, e453) | 2014 | `10.7717/peerj.453` | Biblioteca aberta para filtragem, segmentação clássica, morfologia matemática e extração de descritores geométricos. |
| Ronneberger, Fischer & Brox, *U-Net: Convolutional Networks for Biomedical Image Segmentation* (*LNCS*, p. 234–241) | 2015 | `10.1007/978-3-319-24574-4_28` | Arquitetura referência para segmentação semântica em regimes de **poucas imagens anotadas**. |
| DeCost & Holm, *A computer vision approach for automated analysis and classification of microstructural image data* (*Comput. Mater. Sci.*, v. 110, p. 126–133) | 2015 | `10.1016/j.commatsci.2015.08.011` | Descritores visuais (*Bag of Visual Features*) + SVM atingindo $>80\%$ em classificação microestrutural sem exigir redes profundas pesadas. |
| He et al., *Deep Residual Learning for Image Recognition* (*IEEE CVPR*, p. 770–778) | 2016 | `10.1109/CVPR.2016.90` | Blocos residuais (ResNet) para evitar degradação em redes convolucionais (usada no piloto IV EFAC). |
| Azimi et al., *Advanced Steel Microstructural Classification by Deep Learning Methods* (*Sci. Rep.*) | 2018 | `10.1038/s41598-018-20037-5` | Referência de segmentação pixel a pixel por FCN em micrografias SEM metalográficas. |
| Holm et al., *Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis* (*Metall. Mater. Trans. A*, v. 51(12), p. 5985–5999) | 2020 | `10.1007/s11661-020-06008-4` | **Referência estruturante:** formaliza a taxonomia de tarefas (classificação, segmentação semântica, detecção de objetos, segmentação de instâncias) e alerta para riscos em dados microestruturais. |
| Botifoll, Pinto-Huguet & Arbiol, *Machine learning in electron microscopy for advanced nanocharacterization...* (*Nanoscale Horizons*, v. 7(12), p. 1427–1477) | 2022 | `10.1039/d2nh00377e` | Revisão específica de ML em microscopia eletrônica (denoising, segmentação, detecção de defeitos e ferramentas abertas disponíveis). |
| Choudhary et al., *Recent advances and applications of deep learning methods in materials science* (*npj Comput. Mater.*, v. 8(1)) | 2022 | `10.1038/s41524-022-00734-6` | Revisão abrangendo imagens, espectros/difração, dados sintéticos vs. experimentais e **quantificação de incerteza**. |
| Gerçek et al., *Data-efficient U-Net for Segmentation of Carbide Microstructures in SEM Images of Steel Alloys* | 2025 | `arXiv:2511.11485v1` | Prova que uma U-Net enxuta treinada em **apenas 10 imagens SEM anotadas** supera métodos clássicos onde há sobreposição de cinza (Dice 0,98 vs. 0,85). |
| Pan, Wang & Cai, *Automated and Scalable SEM Image Analysis of Perovskite Solar Cell Materials via a Deep Segmentation Framework* | 2025 | `arXiv:2509.26548v1` | Exemplo recente de segmentação profunda em SEM (PerovSegNet/YOLOv8x) extraindo contagem e distribuição de área por fase/grão. |

### Eixo D — Estado da Arte em Automação/IA/CV Aplicada a Grafeno, Materiais 2D e DRX/AFM/MEV

| Referência Verificada | Ano | Fonte / DOI ou arXiv | Foco Principal e Métrica/Achado Verificado |
| :--- | :---: | :--- | :--- |
| Saito et al., *Deep-learning-based quality filtering of mechanically exfoliated 2D crystals* | 2019 | *npj Comput. Mater.* (`10.1038/s41524-019-0262-4`) | U-Net treinada com conjunto pequeno de imagens ópticas distingue monocamada e bicamada de $\text{MoS}_2$ e grafeno com **70–80% de sucesso** como etapa de **triagem inicial**. |
| Masubuchi et al., *Deep-learning-based image segmentation integrated with optical microscopy for automatically searching for 2D materials* | 2020 | *npj 2D Mater. Appl.* (`10.1038/s41699-020-0137-z`) | Mask-RCNN integrada a microscópio motorizado para grafeno, hBN, $\text{MoS}_2$ e $\text{WTe}_2$ (200 ms por imagem $1024\times1024$), com código e pesos públicos. |
| Han et al., *Deep-Learning-Enabled Fast Optical Identification and Characterization of 2D Materials* | 2020 | *Adv. Mater.* (`10.1002/adma.202000953`) | Rede neural com *transfer learning* que extrai contraste, cor, bordas, forma e distribuição de tamanho de flocos 2D. |
| Meng et al., *Deep learning in two-dimensional materials: Characterization, prediction, and design* | 2024 | *Frontiers of Physics* (`10.1007/s11467-024-1394-7`) | Revisão atualizada cobrindo identificação de defeitos, classificação de materiais e determinação automática de espessura por CNN/GAN/U-Net em 2D. |
| Leger et al., *Machine-Learning-Enabled Fast Optical Identification and Characterization of 2D Materials* | 2024 | `arXiv:2406.16211v1` | Compara SegNet, 1D U-Net e 2D U-Net para identificação de monocamadas e discute estratégias de rotulagem/pré-processamento de espessura. |
| Harris et al., *SparseC-AFM: a deep learning method for fast and accurate characterization of $\text{MoS}_2$ with C-AFM* | 2025 | `arXiv:2507.13527v1` / `10.1117/12.3067427` | Reconstrução por DL a partir de varreduras esparsas de C-AFM (redução $>11\times$ no tempo de aquisição) com extração de cobertura, densidade de defeitos, bordas e trincas. |
| Dabrowski et al., *Electronic Coupling and Charge-Transfer Landscape of Graphene on Ge(001)/Si(001): Multiscale Analysis Assisted by Machine Learning* | 2026 | `arXiv:2609.37827v1` | Integra KPFM (derivado de AFM), UPS, ARPES, STS e classificação por ML de regimes locais em grafeno. |
| Oviedo et al., *Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks* | 2019 | *npj Comput. Mater.* (`10.1038/s41524-019-0196-x`) | Combina dados simulados (ICSD) + *data augmentation* físico e CAMs interpretáveis (93% dimensionalidade, 89% grupo espacial) em conjuntos pequenos de DRX. |
| Lee et al., *A deep-learning technique for phase identification in multiphase inorganic compounds using synthetic XRD powder patterns* | 2020 | *Nature Commun.* (`10.1038/s41467-019-13749-3`) | CNN treinada em 1,78 milhão de difratogramas simulados identifica fases em misturas reais (~100% identificação; 86% fração aproximada). |
| Wang et al., *Rapid Identification of X-ray Diffraction Patterns Based on Very Limited Data by Interpretable Convolutional Neural Networks* | 2020 | *J. Chem. Inf. Model.* (`10.1021/acs.jcim.0c00020`) | Extrai ruído experimental real e funde com picos teóricos para classificar DRX com poucos dados e mapas de ativação explicáveis. |
| Szymanski et al., *An autonomous laboratory for the accelerated synthesis of inorganic materials* | 2023 | *Nature* (`10.1038/s41586-023-06734-w`) | Demonstra laboratório autônomo com interpretação automatizada de DRX de pó (A-Lab). |
| Cao, *XMatcher: An Open-Source Framework for X-Ray Diffraction Phase Identification* | 2026 | `arXiv:2607.17162v1` | Framework aberto e interpretável que combina bibliotecas cristalográficas, correção global de deslocamento angular e métricas por pico em vez de caixa-preta. |
| Wang et al., *Diagnosing and narrowing the simulation-to-real gap in powder X-ray diffraction with a wet-dry agentic loop* | 2026 | `arXiv:2608.22400v2` | **Achado crucial para viabilidade:** modelos de DL em DRX degradam em medidas reais (*sim-to-real gap* estrutural); corrigir pequenos desvios de posição de pico mais que dobra a correlação de recuperação, enquanto *denoising* sintético isolado não gera ganho real. |
| Qi et al., *Deep Learning Assisted Raman Spectroscopy for Rapid Identification of 2D Materials* | 2023 | `arXiv:2312.01389v1` | Exemplo complementar de DDPM + CNN para contornar escassez e desbalanceamento de dados espectrais Raman em materiais 2D. |

### Eixo E — Matriz de Viabilidade Científica (O que Pode vs. O que Exige Validação)

| Grandeza Física de Interesse | Técnica Primária (+ Complementar) | O que Algoritmos (PDI / ML / VC) Podem Estimar de Modo Defensável | O que EXIGE Calibração, Modelo Físico ou Experimento Complementar | Risco Científico se Automatizado Ingenuamente |
| :--- | :--- | :--- | :--- | :--- |
| **Tamanho lateral e distribuição morfológica de flocos** ($\mu\text{m}$, circularidade, razão de aspecto, área projetada) | **MEV** (e **AFM** para flocos sub-micrométricos) | Segmentação de contornos (PDI clássico / U-Net), remoção de escala, medição de área, perímetro, diâmetro de Feret e estatística de população. | Calibração de escala em $\text{nm/pixel}$ (metadados do microscópio); correção de **dilatação de ponta** no AFM (Villarrubia 1997); separação de flocos sobrepostos/dobrados. | Confundir contraste de fundo/carregamento no MEV ou artefato de ponta no AFM com tamanho real do floco. |
| **Espessura de floco isolado e número de camadas ($N$)** | **AFM** + **Raman** (triagem rápida via óptica/MEV baixa kV) | Nivelamento automático de substrato (*plane fitting*), extração de histograma de altura ($\Delta z$) em AFM (Yao et al., 2017) e triagem probabilística de candidatos ($N \le 3$ vs. multicamadas). | Modelo físico da **camada de hidratação/adsorvato** e força da ponta no AFM (Shearer 2016; Nemes-Incze 2008); no MEV, calibração estrita de kV/substrato (Hiura 2010); **confirmação obrigatória por Raman (banda 2D)** (Ferrari 2006). | Prometer "contagem exata de camadas por imagem MEV/AFM genérica" ignorando erro de $0{,}4\text{–}1{,}7\ \text{nm}$ na monocamada por AFM ou inversão de contraste no MEV. |
| **Espaçamento interplanar ($d_{002}$), grau de empilhamento ($L_c$) e presença de GO / grafite residual** | **DRX** (pós/filmes empilhados) | Remoção de *background*, ajuste de picos (pseudo-Voigt/Lorentziana), cálculo automatizado de $2\theta_{(002)}$, $d_{002}$ (Bragg), FWHM e estimativa de $L_c$ (Scherrer), além de *peak-shift alignment*. | Calibração do **alargamento instrumental** ($B_{\text{inst}}$) com padrão ($\text{LaB}_6/\text{Si}$) e separação de microdeformação (Holzwarth & Gibson 2011); ajuste experimental para deslocamento angular (*zero-shift*, `arXiv:2608.22400v2`). | Tentar detectar **monocamada isolada** por pico $(002)$ em DRX (fisicamente inexistente sem empilhamento $c$) ou reportar $L_c$ de Scherrer como "tamanho lateral do floco". |
| **Grau de defeitos ($sp^3$, vacâncias, oxidação) e "pureza" da amostra** | **Raman** + **XPS/FTIR** (MEV/AFM/DRX são apenas indiretos) | Análise quantitativa de razão $I_D/I_G$ caso espectros Raman sejam integrados; detecção de regiões anômalas/poros/dobras em MEV/AFM como **indicadores morfológicos indiretos**. | **Não é estimável apenas por imagens MEV/AFM ou difração DRX isolada:** exige espectroscopia Raman, XPS ou análise elementar para quantificar defeitos estruturais e razão C/O (Parvez 2014; Ferrari & Basko 2013). | **Sobrepromessa grave** (identificada em `Apresentação sem título (1).pptx` slide 29): prometer estimativa automática de "pureza química" apenas por visão computacional sobre micrografias. |
| **Generalização de modelos de DL/CNN em dados laboratoriais reais** | **PDI + ML/VC** sobre dados UFCA | *Baselines* interpretáveis (PDI + descritores morfológicos + modelos clássicos/U-Net com poucas amostras como em Gerçek 2025), com **intervalos de confiança e validação cruzada agrupada**. | **Protocolo anti-leakage** (divisão por amostra/síntese/dia, nunca por recorte/arquivo da mesma varredura como no piloto `IVEFAC333.pptx`) e mitigação do **salto simulação-real** (*domain shift* entre QUAM-AFM/sintético e amostras reais da UFCA). | Treinar CNN em base simulada ou dividida aleatoriamente por arquivo e reportar "100% de acurácia" sem validade física nem generalização externa. |

---

## 5. Protocolo de Verificação de Existência de Referências e Fluxo BibTeX

### 5.1 Protocolo Obrigatório em 5 Etapas (Zero Alucinação)

1. **Extração canônica de identificadores:** Capturar DOI normalizado (sem prefixo `https://doi.org/` e sem quebras/typos como `1 0.48550`) ou ID `arXiv:YYMM.NNNNN`.
2. **Consulta primária em Crossref (`api.crossref.org/works/<doi>`):**
   - Se HTTP 200: extrair `title`, `author`, `container-title`, `volume`, `issue`, `page`, `published-print`/`published-online`.
3. **Fallback obrigatório para DataCite (`api.datacite.org/dois/<doi>`) e arXiv (`search_arxiv.py --id_list`):**
   - Se Crossref retornar HTTP 404 (padrão para datasets `10.21950/*`, Zenodo `10.5281/*` e arXiv `10.48550/arXiv.*`), consultar DataCite / arXiv antes de declarar DOI inexistente.
4. **Conferência cruzada em OpenAlex (`openalex_cli.py get works` — custo `$0`) e Semantic Scholar:**
   - Comparar **título completo, primeiro autor, periódico e ano** contra a afirmação do texto. Rejeitar imediatamente se o DOI resolver para obra distinta (ex.: caso **Holm et al. 2020** `10.1007/s11661-020-06008-4` vs. **Mohammed et al. 2021** `10.1007/s11837-020-04347-6`).
5. **Registro de status de leitura:** Marcar toda referência como `[VERIFICADA-METADADOS]`, `[VERIFICADA-ABSTRACT]` ou `[LIDA-INTEGRALMENTE]` antes de incluí-la na apresentação ou dissertação.

### 5.2 Fluxo Reproduzível para Gerar e Validar BibTeX (Sem Escrita Manual)

Na Missão 02, o arquivo `referencias.bib` deverá ser gerado programaticamente a partir das APIs verificadas e auditado antes da compilação de slides ou texto:

```powershell
# Exemplo verificado nesta sessão via Crossref Content Negotiation:
@'
import urllib.request

dois = ["10.1007/s11661-020-06008-4", "10.1088/0957-4484/27/12/125704"]
for doi in dois:
    req = urllib.request.Request(
        f"https://api.crossref.org/works/{doi}/transform/application/x-bibtex",
        headers={"User-Agent": "PPGCEM-UFCA-BibAudit/1.0"}
    )
    with urllib.request.urlopen(req, timeout=15) as r:
        print(r.read().decode("utf-8").strip())
'@ | & "C:\Users\emer\.local\bin\python3.11.exe" -
```

**Saída empírica real observada nesta sessão:**
```bibtex
@article{Holm_2020, title={Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis}, volume={51}, ISSN={1543-1940}, url={http://dx.doi.org/10.1007/s11661-020-06008-4}, DOI={10.1007/s11661-020-06008-4}, number={12}, journal={Metallurgical and Materials Transactions A}, publisher={Springer Science and Business Media LLC}, author={Holm, Elizabeth A. and Cohn, Ryan and Gao, Nan and Kitahara, Andrew R. and Matson, Thomas P. and Lei, Bo and Yarasi, Srujana Rao}, year={2020}, month=Sept, pages={5985–5999} }
@article{Shearer_2016, title={Accurate thickness measurement of graphene}, volume={27}, ISSN={1361-6528}, url={http://dx.doi.org/10.1088/0957-4484/27/12/125704}, DOI={10.1088/0957-4484/27/12/125704}, number={12}, journal={Nanotechnology}, publisher={IOP Publishing}, author={Shearer, Cameron J and Slattery, Ashley D and Stapleton, Andrew J and Shapter, Joseph G and Gibson, Christopher T}, year={2016}, month=Feb, pages={125704} }
```

**Checklist automático de validação de `.bib` (via `uv run --with bibtexparser` na Missão 02):**
- Unicidade das chaves de citação (ex.: `Holm_2020`, `Shearer_2016`).
- Presença obrigatória de `author`, `title`, `year` e `journal`/`booktitle` (ou `eprint`/`archivePrefix={arXiv}` para preprints).
- Normalização de `month` não padronizado (ex.: `Sept` $\rightarrow$ `{sep}` ou `9` para evitar avisos no BibTeX/BibLaTeX) e remoção de chaves vazias.
- Revalidação de que todo `doi` no `.bib` retorna HTTP 200 em Crossref/DataCite e corresponde ao `title` armazenado.

---

## 6. Modelo de Fichamento Crítico (Para Execução na Missão 02)

Todo artigo lido na íntegra na Missão 02 deverá receber um fichamento em Markdown seguindo exatamente esta estrutura:

```markdown
### Fichamento: [Sobrenome et al., Ano] — [Título]
- **Identificadores verificados:** DOI / arXiv ID | URL oficial | Status de leitura (`[LIDA-INTEGRALMENTE]`)
- **Eixo(s) do projeto:** [A / B / C / D / E]
- **Material e rota de síntese analisados:** (ex.: grafeno CVD, esfoliação mecânica, esfoliação eletroquímica, GO/rGO, simulação)
- **Técnica(s) experimental(is) e condições:** (ex.: DRX Cu Kα, MEV kV/detector, AFM modo PeakForce/tapping, Raman λ)
- **Abordagem computacional / algoritmo:** (ex.: pré-processamento, segmentação, U-Net, Mask-RCNN, descritores, métricas)
- **Protocolo de divisão de dados e validação:** (há risco de *data leakage*? O teste foi *out-of-distribution* / amostra independente?)
- **Principais achados quantitativos:** (citar apenas números e intervalos com página/seção de origem)
- **Limitações e ameaças à validade para o PPGCEM/UFCA:** (*domain shift*, dependência de substrato, necessidade de técnica complementar)
- **Uso defensável no Seminário I / Dissertação:** (como sustenta o argumento sem sobreprometer)
```

---

## 7. Matriz de Evidências (Exemplos Empiricamente Preenchidos nesta Sessão)

> [!NOTE]
> Os registros abaixo baseiam-se exclusivamente nos metadados e *abstracts* inspecionados nesta sessão. Afirmações que dependam de parâmetros experimentais internos (tabelas, gráficos, equações completas do corpo do artigo) só poderão ser incorporadas após leitura integral do PDF na Missão 02.

| Afirmação Científica / Metodológica a Defender | Eixo | Artigo Verificado (DOI / arXiv) | Trecho / Evidência Direta do Abstract Verificado | Limitação / Ressalva Obrigatória |
| :--- | :---: | :--- | :--- | :--- |
| A espessura aparente de monocamada de grafeno medida por AFM varia amplamente e superestima o valor teórico devido a forças de ponta e camada interfacial de adsorbatos. | B / E | Shearer et al. (2016) — `10.1088/0957-4484/27/12/125704` | Relata valores publicados de **0,4 a 1,7 nm** para monocamada; demonstra que a camada de adsorvato grafeno–substrato e a pressão da ponta são determinantes, reduzindo o erro de 0,1–1,3 nm para 0,1–0,3 nm em modo PeakForce tapping. | O software **não pode** usar limiar fixo de $0{,}34\ \text{nm}$ no AFM para rotular monocamadas automaticamente sem calibração do substrato/modo. |
| A contagem de camadas de grafeno por MEV via elétrons secundários não é universal; depende da tensão de aceleração, função trabalho e substrato. | B / E | Hiura et al. (2010) `10.1143/apex.3.095101`; Zhou et al. (2016) `10.1038/srep21045`; Huang & Gan (2024) `10.1016/j.micron.2024.103716` | Hiura et al. observam relação linear discreta de intensidade SE vs. número de camadas *desde que* usada **baixa tensão de aceleração** sobre substrato isolante espesso; Zhou et al. associam o sinal à função trabalho por camada. | Não substitui Raman ou AFM calibrado em amostras espessas, condutoras ou com resíduos superficiais. |
| A esfoliação eletroquímica produz dispersões de grafeno com distribuição heterogênea de camadas, tamanho lateral e oxidação residual, exigindo caracterização multimodal. | A / B | Parvez et al. (2014) `10.1021/ja5017156`; Backes et al. (2020) `10.1088/2053-1583/ab1e0a` | Parvez et al. reportam rendimento $>85\%$ de flocos $\le 3$ camadas, até $44\ \mu\text{m}$ e razão C/O = 17,2; Backes et al. destacam a heterogeneidade de tamanho lateral e espessura como gargalo crítico das rotas em fase líquida. | Parvez (2014) representa um protocolo específico em sais de sulfato; amostras locais da UFCA exigem medição empírica própria. |
| A espectroscopia Raman é necessária como técnica complementar não destrutiva para confirmar número de camadas e densidade de defeitos. | B / E | Ferrari et al. (2006) `10.1103/physrevlett.97.187401`; Ferrari & Basko (2013) `10.1038/nnano.2013.46` | O espectro Raman (especialmente a evolução do pico $2D$ por dupla ressonância e banda $G$/$D$) captura de forma não destrutiva o número de camadas, desordem, dopagem e tensão. | Exige acesso a espectrômetro Raman (ou calibração prévia do conjunto de amostras de referência). |
| Modelos de *Deep Learning* em DRX sofrem degradação estrutural entre dados simulados e experimentais (*simulation-to-real gap*). | D / E | Wang et al. (2026) — `arXiv:2608.22400v2` | Analisadores de DL em PXRD têm excelente desempenho em padrões simulados e degradam nos medidos; *denoising* sintético isolado não melhora espectros reais, enquanto corrigir pequenos desvios de posição de pico mais que dobra a correlação mediana de recuperação. | Validação ocorreu em fases inorgânicas/ligas; reforça a necessidade de alinhamento físico e dados experimentais reais antes de confiar em CNNs sobre DRX de carbono. |
| Segmentação por DL pode superar sobreposição de níveis de cinza em micrografias SEM mesmo com conjuntos pequenos de treino, sendo viável como *baseline* investigativo se validada com rigor. | C / D | Gerçek et al. (2025) `arXiv:2511.11485v1`; Saito et al. (2019) `10.1038/s41524-019-0262-4` | Gerçek et al. atingem Dice de 0,98 (vs. 0,85 clássico) com apenas 10 imagens SEM anotadas; Saito et al. alcançam 70–80% com U-Net pequena para triagem inicial de monocamadas/bicamadas ópticas. | O desempenho em aços (Gerçek) ou microscopia óptica (Saito) não garante transferência direta para MEV de grafeno eletroquímico sem validação cruzada por amostra. |
| O estudo piloto anterior em QUAM-AFM Lite não prova viabilidade sobre grafeno real por *domain shift* e risco de *data leakage*. | E | Carracedo-Cosme et al. (2022) `10.1021/acs.jcim.1c01323`; análise de `IVEFAC333.pptx` (slides 11–13) | QUAM-AFM contém 685.513 moléculas orgânicas pequenas em pilhas 3D simuladas em UHV; no piloto (`IVEFAC333.pptx`), a divisão 80/20 por arquivo pode misturar imagens da mesma pilha/molécula. | O piloto deve ser apresentado honestamente como exercício exploratório de pipeline (PyTorch vs. TensorFlow), nunca como validação em grafeno. |

---

## 8. Status de Leitura (Missão 01 vs. Fila Prioritária da Missão 02)

### 8.1 Escopo Efetivamente Lido nesta Missão 01
- **Status atual de todos os artigos listados na Seção 4:** **`[VERIFICADA-METADADOS]` ou `[VERIFICADA-ABSTRACT]`**. Nenhum PDF completo foi baixado nem lido na íntegra durante a Missão 01 (foco exclusivo em preparação do ambiente, auditoria de histórico e planejamento bibliográfico).
- **Documentos locais inspecionados integralmente:** pré-projeto (`pre-projeto-da-selecao.md`) e textos/notas das 3 apresentações passadas (`Apresentação de Projeto PPGCEM.pptx`, `Apresentação sem título (1).pptx`, `IVEFAC333.pptx`).

### 8.2 Fila Prioritária de Download Legal e Leitura Integral para a Missão 02

Ordem recomendada de leitura (priorizando acesso aberto legítimo já confirmado pelas APIs e utilidade direta para o Seminário I de 17/11/2026):

1. **Prioridade Máxima — Núcleo do Seminário I (Acesso Aberto Confirmado):**
   - **Shearer et al. (2016)** (`10.1088/0957-4484/27/12/125704`) — Bronze OA IOP (`https://iopscience.iop.org/article/10.1088/0957-4484/27/12/125704/pdf`) — *essencial para defender limites do AFM*.
   - **Nemes-Incze et al. (2008)** (`10.1016/j.carbon.2008.06.022`) — Green OA arXiv (`https://arxiv.org/pdf/0812.0690`) — *anomalias de tapping AFM em grafeno*.
   - **Holm et al. (2020)** (`10.1007/s11661-020-06008-4`) — Hybrid OA Springer (`https://link.springer.com/content/pdf/10.1007/s11661-020-06008-4.pdf`) — *taxonomia CV/ML em materiais*.
   - **Backes et al. (2020)** (`10.1088/2053-1583/ab1e0a`) — Hybrid OA IOP (`https://iopscience.iop.org/article/10.1088/2053-1583/ab1e0a/pdf`) — *protocolos de síntese/caracterização de grafeno*.
   - **Parvez et al. (2014)** (`10.1021/ja5017156`) — Green OA Max Planck (`http://hdl.handle.net/11858/00-001M-0000-0019-B711-7`) — *esfoliação eletroquímica*.
   - **Zhou et al. (2016)** (`10.1038/srep21045`) — Gold OA Nature (`https://doi.org/10.1038/srep21045`) — *contraste quantitativo SE em MEV de grafeno*.
   - **Ferrari et al. (2006)** (`10.1103/physrevlett.97.187401`, `https://arxiv.org/pdf/cond-mat/0606284`) e **Ferrari & Basko (2013)** (`10.1038/nnano.2013.46`, `https://arxiv.org/pdf/1306.5856`) — *justificativa de complementaridade por Raman*.
   - **Wang et al. (2026)** (`arXiv:2608.22400v2`, `https://arxiv.org/pdf/2608.22400v2`) — *evidência de sim-to-real gap em DRX*.
2. **Prioridade Alta — Estado da Arte CV/ML e Padrões:**
   - **Masubuchi et al. (2020)** (`10.1038/s41699-020-0137-z`, `https://www.nature.com/articles/s41699-020-0137-z.pdf`), **Han et al. (2020)** (`10.1002/adma.202000953`, `https://arxiv.org/pdf/1906.11220`), **Meng et al. (2024)** (`10.1007/s11467-024-1394-7`, `https://link.springer.com/content/pdf/10.1007/s11467-024-1394-7.pdf`), **Botifoll et al. (2022)** (`10.1039/d2nh00377e`), **Choudhary et al. (2022)** (`10.1038/s41524-022-00734-6`), **Oviedo et al. (2019)** (`10.1038/s41524-019-0196-x`), **Harris et al. (2025)** (`arXiv:2507.13527v1`), **Gerçek et al. (2025)** (`arXiv:2511.11485v1`), **Villarrubia (1997)** (`10.6028/jres.102.030`).
3. **Artigos Fechados (Acesso via Portal de Periódicos CAPES/UFCA na Missão 02):**
   - **Huang & Gan (2024)** (`10.1016/j.micron.2024.103716`), **Li et al. (2007)** (`10.1016/j.carbon.2007.03.038`), **Stobiński et al. (2014)** (`10.1016/j.elspec.2014.07.003`), **Abdelkader et al. (2015)** (`10.1039/c4nr06942k`), **Dreyer et al. (2010)** (`10.1039/b917103g`), **Holzwarth & Gibson (2011)** (`10.1038/nnano.2011.145`), **Hiura et al. (2010)** (`10.1143/apex.3.095101`).

---

## 9. Registro Completo de Fontes e URLs Utilizadas (Requisito OpenAlex / arXiv / Europe PMC)

Este plano utilizou as skills `literature-search-openalex`, `literature-search-arxiv` e `literature-search-europepmc`, além das APIs Crossref, DataCite e Semantic Scholar. Todas as URLs abaixo correspondem a registros efetivamente consultados/retornados pelas ferramentas nesta sessão (incluindo o DOI incorreto auditado na Seção 2 para rastreabilidade):

- https://doi.org/10.1037/h0042519 (OpenAlex: https://openalex.org/W2040870580)
- https://doi.org/10.1103/PhysRevLett.56.930 (OpenAlex: https://openalex.org/W3150248096 | OA PDF: http://link.aps.org/pdf/10.1103/PhysRevLett.56.930)
- https://doi.org/10.1016/j.commatsci.2015.08.011 (OpenAlex: https://openalex.org/W1141054642)
- https://doi.org/10.1109/CVPR.2016.90 (OpenAlex: https://openalex.org/W2194775991)
- https://doi.org/10.1088/0957-4484/27/12/125704 (OpenAlex: https://openalex.org/W2275457611 | OA PDF: https://iopscience.iop.org/article/10.1088/0957-4484/27/12/125704/pdf)
- https://doi.org/10.1007/s11661-020-06008-4 (OpenAlex: https://openalex.org/W3031142281 | OA PDF: https://link.springer.com/content/pdf/10.1007/s11661-020-06008-4.pdf)
- https://doi.org/10.1007/s11837-020-04347-6 (OpenAlex: https://openalex.org/W3086739661 — *DOI errado auditado: Mohammed et al., JOM*)
- https://doi.org/10.21950/BFAU11 (DataCite: https://edatos.consorciomadrono.es/citation?persistentId=doi:10.21950/BFAU11)
- https://doi.org/10.1021/acs.jcim.1c01323 (OpenAlex: https://openalex.org/W4214840389 | Europe PMC: https://europepmc.org/article/MED/35234034 / PMC9942089)
- https://doi.org/10.48550/arXiv.2508.04035 (arXiv: https://arxiv.org/abs/2508.04035 | PDF: https://arxiv.org/pdf/2508.04035v1)
- https://doi.org/10.7717/peerj.453 (OpenAlex: https://openalex.org/W2015159529)
- https://doi.org/10.1126/science.1102896 (OpenAlex: https://openalex.org/W2058122340 | OA PDF: https://arxiv.org/pdf/cond-mat/0410550)
- https://doi.org/10.1038/nmat1849 (OpenAlex: https://openalex.org/W2014935324 | OA PDF: https://arxiv.org/pdf/cond-mat/0702595)
- https://doi.org/10.1103/revmodphys.81.109 (OA PDF: http://link.aps.org/pdf/10.1103/RevModPhys.81.109)
- https://doi.org/10.1039/b917103g (OpenAlex: https://openalex.org/W2135479172)
- https://doi.org/10.1021/ja5017156 (OpenAlex: https://openalex.org/W2071955897 | OA: http://hdl.handle.net/11858/00-001M-0000-0019-B711-7)
- https://doi.org/10.1039/c4nr06942k (OpenAlex: https://openalex.org/W2025235443)
- https://doi.org/10.1088/2053-1583/ab1e0a (OpenAlex: https://openalex.org/W2998241881 | OA PDF: https://iopscience.iop.org/article/10.1088/2053-1583/ab1e0a/pdf)
- https://doi.org/10.1016/j.rechem.2026.103746
- https://arxiv.org/pdf/2609.19191v1
- https://doi.org/10.1038/nnano.2011.145
- https://doi.org/10.1016/j.carbon.2007.03.038 (OpenAlex: https://openalex.org/W2024817672)
- https://doi.org/10.1016/j.elspec.2014.07.003 (OpenAlex: https://openalex.org/W1976073956)
- https://doi.org/10.1016/s1452-3981(23)13940-x
- https://doi.org/10.1016/j.electacta.2013.11.040
- https://doi.org/10.3103/s1068364x17090058
- https://doi.org/10.13005/ojc/340120
- https://doi.org/10.1088/1742-6596/1495/1/012012
- https://doi.org/10.1016/j.micron.2024.103716 (OpenAlex: https://openalex.org/W4402436866)
- https://doi.org/10.1143/apex.3.095101
- https://doi.org/10.1063/1.3608062
- https://doi.org/10.1038/srep21045 (OpenAlex: https://openalex.org/W2409692358)
- https://doi.org/10.1002/smll.201704190
- https://doi.org/10.1016/j.carbon.2008.06.022 (OpenAlex: https://openalex.org/W2164856334 | OA PDF: https://arxiv.org/pdf/0812.0690)
- https://doi.org/10.6028/jres.102.030
- https://doi.org/10.1002/pssb.200879657
- https://doi.org/10.1016/j.jmst.2016.07.020
- https://doi.org/10.1103/physrevlett.97.187401 (OpenAlex: https://openalex.org/W2136334331 | OA PDF: https://arxiv.org/pdf/cond-mat/0606284)
- https://doi.org/10.1038/nnano.2013.46 (OpenAlex: https://openalex.org/W2074880343 | OA PDF: https://arxiv.org/pdf/1306.5856)
- https://doi.org/10.1109/tsmc.1979.4310076 (OpenAlex: https://openalex.org/W2133059825)
- https://doi.org/10.1007/978-3-319-24574-4_28 (OpenAlex: https://openalex.org/W1901129140 | OA PDF: https://link.springer.com/content/pdf/10.1007/978-3-319-24574-4_28.pdf)
- https://doi.org/10.1038/s41598-018-20037-5
- https://doi.org/10.1039/d2nh00377e (OpenAlex: https://openalex.org/W4306248068)
- https://doi.org/10.1038/s41524-022-00734-6 (OpenAlex: https://openalex.org/W3208687975 | OA PDF: https://www.nature.com/articles/s41524-022-00734-6.pdf)
- https://doi.org/10.1038/s41524-019-0262-4 (OA PDF: https://www.nature.com/articles/s41524-019-0262-4.pdf)
- https://doi.org/10.1038/s41699-020-0137-z (OpenAlex: https://openalex.org/W2982049401 | OA PDF: https://www.nature.com/articles/s41699-020-0137-z.pdf)
- https://doi.org/10.1002/adma.202000953 (OpenAlex: https://openalex.org/W3034093793 | OA PDF: https://arxiv.org/pdf/1906.11220)
- https://doi.org/10.1007/s11467-024-1394-7 (OpenAlex: https://openalex.org/W4394845933 | OA PDF: https://link.springer.com/content/pdf/10.1007/s11467-024-1394-7.pdf)
- https://doi.org/10.1126/sciadv.aaw8989 (OpenAlex: https://openalex.org/W2890058181)
- https://doi.org/10.1038/s41524-019-0196-x (OpenAlex: https://openalex.org/W2940802411 | OA PDF: https://www.nature.com/articles/s41524-019-0196-x.pdf)
- https://doi.org/10.1038/s41467-019-13749-3 (OpenAlex: https://openalex.org/W2997208716 | OA PDF: https://www.nature.com/articles/s41467-019-13749-3.pdf)
- https://doi.org/10.1021/acs.jcim.0c00020 (OpenAlex: https://openalex.org/W3013216111 | OA PDF: https://arxiv.org/pdf/1912.07750)
- https://doi.org/10.1038/s41586-023-06734-w
- https://arxiv.org/pdf/2312.01389v1
- https://arxiv.org/pdf/2406.16211v1
- https://arxiv.org/pdf/2507.13527v1 (DOI: https://doi.org/10.1117/12.3067427)
- https://arxiv.org/pdf/2509.26548v1
- https://arxiv.org/pdf/2511.11485v1
- https://arxiv.org/pdf/2607.17162v1
- https://arxiv.org/pdf/2608.22400v2
- https://arxiv.org/pdf/2609.37827v1
