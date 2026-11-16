# Registro Completo de Consultas Utilizadas — Missão 02 (PPGCEM/UFCA)

**Data de execução e consolidação das consultas:** 16/11/2026 (`2026-11-16`)  
**Habilidades (*skills*) utilizadas:** `literature-search-openalex` (`openalex_cli.py`), `literature-search-arxiv` (`search_arxiv.py`), `literature-search-europepmc` (`europepmc_api.py`), além de consultas de resolução pontual em `api.crossref.org`, `api.datacite.org` e `api.semanticscholar.org`.  
**Conformidade de licença:** Termos registrados em [`literature_search_openalex_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_openalex_LICENSE.txt), [`literature_search_arxiv_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_arxiv_LICENSE.txt) e [`literature_search_europepmc_LICENSE.txt`](file:///C:/Users/emer/dissertacao/Artigos/.licenses/literature_search_europepmc_LICENSE.txt).

> [!NOTE]
> Todos os valores de `meta.count` (OpenAlex), `hitCount` (Europe PMC) e `results_count` (arXiv) listados abaixo foram obtidos empiricamente pela execução direta das ferramentas em **16/11/2026**, cujos arquivos JSON brutos encontram-se preservados em [`_scratch/agente-a/queries/`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/queries).

---

## 1. Consultas Estruturadas no OpenAlex (`openalex_cli.py filter works`)

Todas as 22 consultas abaixo utilizaram o comando `filter works` (`$0,0001`/requisição) com `--sort "cited_by_count:desc"`, `--select "id,doi,display_name,publication_year,cited_by_count"` e `--per-page 5` (economizando cota sem chave de `$0,10/dia` e evitando `--search` que custa `10×` mais). O saldo da cota compartilhada após a execução de todas as consultas do Agente A foi verificado via `rate-limit`: `$0,0366` restantes (`366/1000` requisições no dia).

### 1.1 Consultas em Inglês (Eixos A, B, C, D e Seção 5 do `PROMPT_MESTRE.md`)

| ID | Eixo / Origem | Filtro Exato (`--filter`) | `meta.count` | Principais Registros Observados no Topo (`ano \| cit. \| DOI \| título`) |
| :--- | :--- | :--- | :---: | :--- |
| **Q-OA-01** | Eixo A — Clássicos de grafeno e GO | `title.search:("Electric Field Effect in Atomically Thin Carbon Films" OR "The rise of graphene" OR "The electronic properties of graphene" OR "The chemistry of graphene oxide")` | **131** | `2004 \| 67.486 \| 10.1126/science.1102896` (*Electric Field Effect...*); `2007 \| 40.337 \| 10.1038/nmat1849` (*The rise of graphene*); `2009 \| 25.204 \| 10.1103/revmodphys.81.109` (*The electronic properties...*); `2009/2010 \| 11.840 \| 10.1039/b917103g` (*The chemistry of graphene oxide*) |
| **Q-OA-02** | Eixo A — Esfoliação eletroquímica | `title_and_abstract.search:graphene AND "electrochemical exfoliation"` | **1.130** | `2014 \| 1.478 \| 10.1021/ja5017156` (Parvez et al., *Exfoliation of Graphite into Graphene in Aqueous Solutions of Inorganic Salts*); `2009 \| 1.218 \| 10.1021/nn900546b`; `2011 \| 1.043 \| 10.1021/nn200025p` |
| **Q-OA-03** | Eixo B (DRX) — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:graphene AND ("X-ray diffraction" OR XRD) AND characterization` | **7.300** | `2008 \| 2.122 \| 10.1021/jp710931h`; `2009 \| 1.190 \| 10.1002/adfm.200900377`; `2010 \| 1.080 \| 10.1039/b917240h` (alta proporção de artigos de síntese/compósitos usando DRX apenas como checagem rotineira) |
| **Q-OA-04** | Eixo B (DRX) — Refinamento por título | `title.search:(graphene OR "graphene oxide" OR graphite) AND ("X-ray diffraction" OR XRD)` | **418** | `2014 \| 1.946 \| 10.1016/j.elspec.2014.07.003` (Stobiński et al.); `2007 \| 1.735 \| 10.1016/j.carbon.2007.03.038` (Li, Lu & Xia); `2020 \| 439 \| 10.1088/1742-6596/1495/1/012012` |
| **Q-OA-05** | Eixo B (AFM) — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:graphene AND "atomic force microscopy" AND thickness` | **786** | `2008 \| 3.290 \| 10.1016/j.carbon.2008.09.045`; `2014 \| 1.691 \| 10.1021/ar4002312`; `2010 \| 1.211 \| 10.1021/nn101781v` |
| **Q-OA-06** | Eixo B (AFM) — Convolução de ponta | `title_and_abstract.search:("tip convolution" OR "tip-sample convolution" OR "tip dilation") AND ("atomic force microscopy" OR AFM)` | **87** | `1999 \| 779 \| 10.1021/jp9904771`; `1997 \| 680 \| 10.6028/jres.102.030` (Villarrubia, *Algorithms for scanned probe microscope image simulation, surface reconstruction, and tip estimation*); `1995 \| 470 \| 10.1063/1.113809` |
| **Q-OA-07** | Eixo B (MEV) — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:graphene AND "scanning electron microscopy" AND "image analysis"` | **38** | `2016 \| 126 \| 10.1016/j.conbuildmat.2016.11.083` (GO-cement); `2024 \| 122 \| 10.1002/adfm.202316379`; `2016 \| 115 \| 10.1016/j.cemconcomp.2016.03.005` (evidencia ruído semântico em busca ampla sem filtro de contraste/camadas/morfometria) |
| **Q-OA-08** | Eixo B (MEV) — Contraste e camadas | `title.search:graphene AND ("scanning electron" OR "secondary electron" OR SEM) AND (contrast OR layer OR layers OR thickness)` | **34** | `2010 \| 100 \| 10.1143/apex.3.095101` (Hiura et al.); `2011 \| 63 \| 10.1063/1.3601467`; `2011 \| 62 \| 10.1063/1.3608062`; `2024 \| 51 \| 10.1016/j.micron.2024.103716` (Huang & Gan) |
| **Q-OA-09** | Eixos C/D — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:graphene AND "machine learning" AND microscopy` | **124** | `2023 \| 146 \| 10.1016/j.solmat.2023.112207`; `2018 \| 92 \| 10.1007/s12274-018-2155-0`; `2019 \| 88 \| 10.1038/s41699-018-0084-0` |
| **Q-OA-10** | Eixos C/D — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:"2D materials" AND "computer vision"` | **23** | `2020 \| 144 \| 10.1021/acs.nanolett.0c00269`; `2019 \| 51 \| 10.1002/inf2.12026`; `2023 \| 23 \| 10.1038/s41598-023-28664-3` (*Automatic detection of multilayer h-BN...*) |
| **Q-OA-11** | Eixo D (DRX+ML) — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:("X-ray diffraction" OR XRD) AND ("deep learning" OR "convolutional neural network" OR "machine learning") AND (phase OR crystal OR identification),publication_year:>2018` | **868** | `2022 \| 901 \| 10.3390/min12020205`; `2019 \| 347 \| 10.1038/s41524-019-0196-x` (Oviedo et al.); `2020 \| 230 \| 10.1038/s41467-019-13749-3` (Lee et al.) |
| **Q-OA-12** | Multimodalidade — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:"multimodal characterization" AND graphene` | **13** | `2021 \| 24 \| 10.1002/smtd.202001193`; `2008 \| 8 \| 10.1088/0953-8984/20/47/470301`; `2026 \| 0 \| 10.1063/5.0326941` |
| **Q-OA-16** | Automação — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:"graphene" AND "automated characterization"` | **1** | `2026 \| 4 \| 10.1103/hc53-g1p3` (*Elastic Constants and Bending Rigidities from Long-Wavelength Perturbation Expansions*) |
| **Q-OA-17** | Detecção de flocos — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:"graphene flakes" AND ("automated detection" OR "image segmentation")` | **1** | `2021 \| 3 \| 10.48550/arxiv.2103.13495` (*Machine Learning-based Automatic Graphene Detection with Color Correction for Optical Microscope Images*) |
| **Q-OA-18** | AFM + Segmentação — §5 `PROMPT_MESTRE.md` | `title_and_abstract.search:"AFM" AND "graphene" AND "image segmentation"` | **1** | `2025 \| 1 \| 10.21577/0100-4042.20250243` (Martins et al., *Química Nova* — protocolo híbrido SEM+AFM e segmentação por entropia de GO em parceria LNCC/UFBA/ABNT) |
| **Q-OA-19** | Eixo B (AFM) — Refinamento por título | `title.search:(graphene OR "2D") AND ("atomic force microscopy" OR AFM) AND (thickness OR height OR tip OR layer)` | **77** | `2008 \| 604 \| 10.1016/j.carbon.2008.06.022` (Nemes-Incze et al.); `2016 \| 96 \| 10.1016/j.jmst.2016.07.020` (Yao et al.); `2015 \| 125 \| 10.1039/c5nr02480c` |
| **Q-OA-20** | Eixo B (Raman) — Referências-chave | `title.search:("Raman spectrum of graphene and graphene layers" OR "Raman spectroscopy as a versatile tool for studying the properties of graphene")` | **2** | `2006 \| 15.244 \| 10.1103/physrevlett.97.187401` (Ferrari et al.); `2013 \| 7.522 \| 10.1038/nnano.2013.46` (Ferrari & Basko) |
| **Q-OA-21** | Eixos C/D — ML/DL em 2D por título | `title.search:(graphene OR "2D materials" OR "two-dimensional") AND ("machine learning" OR "deep learning" OR "computer vision") AND (characterization OR identification OR classification OR thickness OR microscopy)` | **133** | `2020 \| 177 \| 10.1038/s41699-020-0137-z` (Masubuchi et al.); `2020 \| 124 \| 10.1002/adma.202000953` (Han et al.); `2018 \| 92 \| 10.1007/s12274-018-2155-0` |
| **Q-OA-22** | Eixo B (MEV) — Tamanho lateral de flocos | `title_and_abstract.search:("graphene" OR "graphene oxide") AND ("scanning electron microscopy" OR SEM) AND ("lateral size" OR "flake size" OR segmentation)` | **173** | `2016 \| 367 \| 10.1021/acsami.5b12723`; `2015 \| 171 \| 10.1088/2053-1583/2/1/014006`; `2015 \| 150 \| 10.1016/j.msea.2015.01.018` |

### 1.2 Consultas em Português no OpenAlex (Requisito da Seção 5 do `PROMPT_MESTRE.md`)

| ID | Tema da Consulta em Português | Filtro Exato (`--filter`) | `meta.count` | Diagnóstico Empírico dos Resultados Obtidos |
| :--- | :--- | :--- | :---: | :--- |
| **Q-OA-13** | Grafeno + caracterização por DRX/MEV/AFM | `title_and_abstract.search:grafeno AND ("difração de raios X" OR "microscopia eletrônica de varredura" OR "microscopia de força atômica" OR caracterização)` | **570** | Retorna majoritariamente artigos nacionais de síntese/aplicação (*Matéria*, *JCECVL*, *REASE*) onde DRX, MEV e AFM são usadas apenas como técnicas de suporte descritivo, sem foco em metrologia automatizada ou visão computacional. |
| **Q-OA-14** | Visão computacional / ML / PDI + microscopia ou grafeno | `title_and_abstract.search:("visão computacional" OR "aprendizado de máquina" OR "processamento de imagens") AND (microscopia OR microestrutura OR grafeno)` | **85** | Retorna teses e dissertações brasileiras (UNICAMP, USP, UFU) sobre segmentação de imagens biológicas, microtomografia de rochas e clínquer por CNN, revelando **escassez de literatura em português** dedicada à automação de MEV/AFM/DRX em grafeno. |
| **Q-OA-15** | Grafeno/GO + esfoliação eletroquímica / análise de imagens | `title_and_abstract.search:(grafeno OR "óxido de grafeno") AND ("esfoliação eletroquímica" OR "análise de imagens" OR espessura)` | **106** | Predominância de estudos experimentais de filmes finos, nanocompósitos poliméricos e membranas em português (`10.1590/s1517-707620170005.0244`, `10.54751/revistafoco.v17n11-116`), reforçando que o estado da arte computacional em materiais 2D concentra-se em inglês (exceto publicações brasileiras em inglês como `10.21577/0100-4042.20250243` capturada por `Q-OA-18`). |

---

## 2. Consultas no arXiv (`search_arxiv.py`)

Executadas em 16/11/2026 com `--max_results 10 --sort_by relevance` via Python `subprocess.run`. Nota metodológica: a interface CLI `search_arxiv.py` reporta `results_count` limitado ao parâmetro `--max_results` (10), não expondo o total global do índice `opensearch:totalResults`.

| ID | Expressão Booleana (`--query`) | Retornados (`results_count`) | Principais Preprints Retornados e Observações |
| :--- | :--- | :---: | :--- |
| **Q-ARX-01** | `(ti:graphene OR ti:"2D material" OR ti:"2D materials") AND (ti:"machine learning" OR ti:"deep learning" OR ti:"computer vision" OR abs:"AFM" OR abs:"SEM" OR abs:"XRD")` | **10** | `2506.20467v1` (*Visualizing intercalation effects in 2D materials using AFM...*, já publicado `10.1021/acs.jpclett.5c00322`); `2201.08091v2`; `2201.12630v1`; `2410.17206v1` (*4D-STEM in SEM*) |
| **Q-ARX-02** | `(ti:graphene OR ti:"2D material" OR ti:"2D materials" OR abs:"graphene flakes") AND (abs:"deep learning" OR abs:"machine learning" OR abs:"computer vision" OR abs:"segmentation")` | **10** | `2412.09333v1` (*MaskTerial*, publicado `10.1039/D5DD00156K`); `2203.15252v1` (*Identification and classification of exfoliated graphene flakes...*); `2103.09449v1` (`10.1038/s41598-021-85159-9`); `2509.01826v1`; `2103.13495v1` |
| **Q-ARX-03** | `(abs:"scanning electron microscopy" OR abs:"atomic force microscopy") AND (abs:"deep learning" OR abs:"machine learning") AND (abs:graphene OR abs:"2D" OR abs:microstructure)` | **10** | `2511.11485v1` (Gerçek et al., *Data-efficient U-Net for Segmentation of Carbide Microstructures in SEM Images...* — NeurIPS 2025 ML4PS); `2512.24220v1`; `1901.09071v2` |
| **Q-ARX-04** | `(ti:"X-ray diffraction" OR abs:"X-ray diffraction") AND (abs:"deep learning" OR abs:"machine learning") AND (abs:phase OR abs:crystal OR abs:carbon)` | **10** | `2305.15410v1`; `2510.17936v1`; `2406.15469v2` (*SimXRD-4M*); `1812.05625v1` (`10.1103/PhysRevB.99.245120`); `2607.17162v1` (Cao, *XMatcher*) |

Consultas diretas por `--id_list` realizadas para auditoria de preprints em 16/11/2026:
- `2211.08591v1,2508.04035v1,2511.11485v1,2509.26548v1,2312.01389v1,2507.13527v1,2609.19191v1,2609.37827v1,2607.17162v1,2406.16211v1` ([`arxiv_preprint_audit.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_preprint_audit.json))
- `2608.22400v2` ([`arxiv_2608_22400v2.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-a/arxiv_2608_22400v2.json))

---

## 3. Consultas no Europe PMC (`europepmc_api.py`)

Executadas em 16/11/2026 com o filtro automático obrigatório `OPEN_ACCESS:y` e ordenação `--sort "CITED desc"`:

| ID | Consulta (`query`) | `hitCount` | Retornados | Observações sobre Cobertura |
| :--- | :--- | :---: | :---: | :--- |
| **Q-EPMC-01** | `graphene AND ("atomic force microscopy" OR "scanning electron microscopy" OR "X-ray diffraction") AND ("layer" OR "thickness" OR "characterization")` | **47.257** | 5 | Forte viés biomédico/nanomedicina no topo por citações (ex.: `PMC10200802` macrófagos; `PMC6223899` nanopartículas de ZnO), inadequado como filtro primário para física do grafeno sem refinamento disciplinar. |
| **Q-EPMC-02** | `"graphene" AND ("machine learning" OR "deep learning") AND ("microscopy" OR "segmentation")` | **4.204** | 5 | Topo dominado por revisões de catálise e barreira hematoencefálica/oncologia (`PMC6061779`, `PMC10212980`, `PMC11252281`). |
| **Q-EPMC-03** | `DOI:10.1021/acs.jcim.1c01323` | **1** | 1 | Confirmou indexação e disponibilidade OA de `Carracedo-Cosme et al. (2022)` (*QUAM-AFM*, `PMID 35234034`, `PMCID PMC9942089`). |

---

## 4. Consultas Complementares por Encadeamento e Verificação de DOIs

Além das buscas temáticas acima, foram executadas consultas direcionadas (`openalex_cli.py filter works` e `get works`, `crossref`, `datacite` e `semanticscholar`):
- **Checagem específica de artigos seminais de DRX, MEV, AFM e PDI/CV:** registradas em [`_scratch/agente-b/`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-b) e [`_scratch/agente-e/`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/agente-e) (ex.: Iwashita 2004, Holzwarth & Gibson 2011, Li et al. 2007, Stobiński et al. 2014, Toby & Von Dreele 2013, Doebelin & Kleeberg 2015, van der Walt et al. 2014).
- **Verificação em Crossref e DataCite:** resolução dos 59 registros em [`verified_catalog.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_catalog.json) e [`verified_dois.json`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/verified_dois.json), além de confirmação de datas *online/print* e números de artigo em `api.crossref.org` para os trabalhos-chave do Eixo A e preprints promovidos, bem como validação HTTP 200 na `api.datacite.org` para `10.21950/BFAU11`, `10.48550/arXiv.2508.04035`, `10.48550/arXiv.2608.22400`, `10.5281/zenodo.10119370` e `10.14278/rodare.4123`.

---

## 5. Lista de URLs e Identificadores Consultados nas Skills (Conformidade OpenAlex / arXiv / Europe PMC)

Para cumprimento estrito das regras das skills `literature-search-openalex`, `literature-search-arxiv` e `literature-search-europepmc`, registram-se os principais identificadores/URLs retornados e inspecionados nesta etapa:
- OpenAlex & Crossref (Eixo A e Metrologia): `https://doi.org/10.1126/science.1102896`, `https://doi.org/10.1038/nmat1849`, `https://doi.org/10.1103/revmodphys.81.109`, `https://doi.org/10.1103/physrevlett.97.187401`, `https://doi.org/10.1038/nnano.2013.46`, `https://doi.org/10.1002/adma.201803784`, `https://doi.org/10.1088/2053-1583/ab1e0a`, `https://doi.org/10.1021/ja5017156`, `https://doi.org/10.1039/b917103g`, `https://doi.org/10.1039/c4nr06942k`, `https://doi.org/10.21577/0100-4042.20250243`.
- OpenAlex & Crossref (Eixos B, C, D e Auditoria): `https://doi.org/10.1016/j.carbon.2007.03.038`, `https://doi.org/10.1016/j.elspec.2014.07.003`, `https://doi.org/10.6028/jres.102.030`, `https://doi.org/10.1143/apex.3.095101`, `https://doi.org/10.1016/j.micron.2024.103716`, `https://doi.org/10.1016/j.carbon.2008.06.022`, `https://doi.org/10.1088/0957-4484/27/12/125704`, `https://doi.org/10.1016/j.jmst.2016.07.020`, `https://doi.org/10.1007/s11661-020-06008-4`, `https://doi.org/10.1038/s41524-019-0196-x`, `https://doi.org/10.1038/s41467-019-13749-3`, `https://doi.org/10.1038/s41699-020-0137-z`, `https://doi.org/10.1002/adma.202000953`, `https://doi.org/10.1038/s41598-024-79386-z`, `https://doi.org/10.1016/j.apmt.2024.102499`, `https://doi.org/10.1038/s41524-026-02211-w`, `https://doi.org/10.1007/s10853-023-08343-4`, `https://doi.org/10.1117/12.3067427`.
- arXiv & DataCite: `https://arxiv.org/abs/2211.08591`, `https://arxiv.org/abs/2312.01389`, `https://arxiv.org/abs/2406.16211`, `https://arxiv.org/abs/2507.13527`, `https://arxiv.org/abs/2508.04035`, `https://arxiv.org/abs/2509.26548`, `https://arxiv.org/abs/2511.11485`, `https://arxiv.org/abs/2607.17162`, `https://arxiv.org/abs/2608.22400`, `https://arxiv.org/abs/2609.19191`, `https://arxiv.org/abs/2609.37827`, `https://doi.org/10.21950/BFAU11`, `https://doi.org/10.5281/zenodo.10119370`, `https://doi.org/10.14278/rodare.4123`.
- Europe PMC: `https://europepmc.org/article/MED/35234034` (`PMCID: PMC9942089`).
