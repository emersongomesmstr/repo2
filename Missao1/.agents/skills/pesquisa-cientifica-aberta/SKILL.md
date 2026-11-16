---
name: pesquisa-cientifica-aberta
description: >
  Fluxo padronizado para busca, verificação de DOIs, extração de texto e geração
  de BibTeX verificado usando OpenAlex, Crossref, DataCite, arXiv, Europe PMC e
  Unpaywall neste ambiente Windows 10 (via uv run e python3.11.exe).
---

# Skill Local: Pesquisa Científica Aberta e Verificada

## Regras de Ambiente (Windows 10)
1. **Nunca** invocar `python` ou `python3` diretamente no `PATH` (resolvem para stubs `0 B` em `WindowsApps`). Use sempre `C:\Users\emer\.local\bin\python3.11.exe` ou `uv run`.
2. Ao chamar scripts das skills do plugin `science`, **nunca** coloque `python` após `uv run` (para preservar as dependências PEP 723):
   - OpenAlex: `uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_openalex\scripts\openalex_cli.py"`
   - arXiv: `uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_arxiv\scripts\search_arxiv.py"`
   - Europe PMC: `uv run "C:\Users\emer\.gemini\config\plugins\science\skills\literature_search_europepmc\scripts\europepmc_api.py"`
3. **NUNCA** exiba ou leia `C:\Users\emer\.env` no terminal ou no chat; verifique apenas a existência das chaves de forma booleana/silenciosa.

## Protocolo Anti-Alucinação Bibliográfica
1. **Toda referência citada precisa de verificação em fonte primária** (Crossref `/works/{doi}`, DataCite `/dois/{doi}` para `arXiv`/`Zenodo`/`BFAU11`, ou OpenAlex `/works/`).
2. **Atenção conhecida (Holm et al., 2020):** o DOI real de *Overview: Computer Vision and Machine Learning for Microstructural Characterization and Analysis* é `10.1007/s11661-020-06008-4` (nunca `10.1007/s11837-020-04347-6`).
3. **Extração de PDFs:** use execução efêmera sem alterar o sistema global:
   `uv run --with pymupdf4llm python -c "import pymupdf4llm, pathlib; pathlib.Path('out.md').write_text(pymupdf4llm.to_markdown('in.pdf'), encoding='utf-8')"`
4. **BibTeX determinístico:** obtenha via Crossref Content Negotiation (`Accept: application/x-bibtex`) e valide cada entrada antes de incorporar em `.bib`.
