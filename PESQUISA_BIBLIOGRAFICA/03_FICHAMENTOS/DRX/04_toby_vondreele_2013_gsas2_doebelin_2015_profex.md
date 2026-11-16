# Fichamento 04 — Softwares Abertos Consolidados de Refinamento Rietveld e Modelagem de Perfil em DRX: GSAS-II e Profex/BGMN (Toby & Von Dreele, 2013; Doebelin & Kleeberg, 2015)

> **Status de Leitura e Verificação:**
> - **Toby & Von Dreele (2013) — GSAS-II:** **Metadados verificados, Resumo oficial completo (OpenAlex / IUCr) e documentação/relatórios técnicos oficiais dos autores (ANL / OSTI `1465500` e `1542591`, repositório oficial `AdvancedPhotonSource/GSAS-II`)**; o texto integral do artigo de 2013 encontra-se em acesso fechado (`oa_status: closed`).
> - **Doebelin & Kleeberg (2015) — Profex/BGMN:** **Texto completo lido integralmente** (`Doebelin_2015_Profex_PMC4603273.txt`, obtido via Europe PMC Open Access, `PMC4603273`).

---

## 1. Identificação bibliográfica

### Software / Artigo 1 — GSAS-II
- **Título:** GSAS-II : the genesis of a modern open-source all purpose crystallography software package
- **Autores:** Brian H. Toby, Robert B. Von Dreele
- **Ano:** 2013 (publicado online em 13 de março de 2013)
- **Periódico:** *Journal of Applied Crystallography*, Volume 46, Número 2, Páginas 544–549
- **DOI:** `10.1107/S0021889813003531`
- **URL oficial:** <https://doi.org/10.1107/S0021889813003531> (Repositório oficial do código: <https://github.com/AdvancedPhotonSource/GSAS-II>; Documentação: <https://advancedphotonsource.github.io/GSAS-II-tutorials>)
- **Citações verificadas (OpenAlex):** 6.459 (`W1967485833`)

### Software / Artigo 2 — Profex / BGMN
- **Título:** Profex : a graphical user interface for the Rietveld refinement program BGMN
- **Autores:** Nicola Doebelin, Reinhard Kleeberg
- **Ano:** 2015 (outubro de 2015)
- **Periódico:** *Journal of Applied Crystallography*, Volume 48, Número 5, Páginas 1573–1580
- **DOI:** `10.1107/S1600576715014685`
- **URL oficial:** <https://doi.org/10.1107/S1600576715014685> (Acesso Aberto Europe PMC: <https://pmc.ncbi.nlm.nih.gov/articles/PMC4603273/>; PubMed `PMID 26500466`; Site oficial: <http://profex.doebelin.org>)
- **Citações verificadas (OpenAlex):** 2.015 (`W1955431138`)

---

## 2. Problema investigado

### Fatos extraídos dos artigos
- **Toby & Von Dreele (2013):** Os pacotes clássicos GSAS (em Fortran/VAX) e EXPGUI (interface Tcl/Tk) atingiram limites arquiteturais (expansibilidade restrita, interface datada, ausência de indexação de pó, solução de estrutura e redução de dados de detectores bidimensionais modernos, além de dependência de compiladores legados). O objetivo foi projetar do zero um pacote cristalográfico **aberto, moderno, extensível e de propósito geral** em Python para cobrir todas as etapas da análise de difração (pó e monocristal, raios X e nêutrons).
- **Doebelin & Kleeberg (2015):** Programas acadêmicos poderosos de refinamento Rietveld baseados em arquivos de texto — como **BGMN** (Bergmann et al., 1998), FullProf.2k (Rodríguez-Carvajal, 2001) e GSAS — exigem edição manual complexa de arquivos de controle e estrutura, conversão de formatos proprietários de fabricantes e repetição tediosa para séries de amostras. Interfaces que escondem totalmente os arquivos de texto (como o software comercial **AUTOQUAN**) sacrificam a programabilidade necessária para modelos avançados (ex.: falhas de empilhamento, amostras orientadas 1D e refinamento paramétrico) e criam risco de sobre-parametrização por usuários inexperientes. **Profex** foi desenvolvido para conciliar **fluxo de trabalho eficiente, processamento em lote e independência de fabricante** com um **baixo nível de abstração**, preservando acesso integral ao *scripting* estrutural do BGMN.

### Análise crítica — Agente B
- Para evitar alegações falsas de originalidade na dissertação (conforme Seção 3-F e 3-B do `PROMPT_MESTRE.md`), é indispensável mapear que **já existem pacotes open-source maduros e altamente citados** (GSAS-II em Python e Profex/BGMN em C++/Qt + C) para análise quantitativa de DRX, separação instrumental rigorosa e processamento em lote — de modo que qualquer ferramenta nova não deve "reinventar o Rietveld", mas sim resolver lacunas específicas (ex.: modelagem de materiais lamelares desordenados/grafeno, automação de pré-análise para usuários não cristalógrafos ou integração multimodal com MEV/AFM).

---

## 3. Fundamentação

### Fatos extraídos dos artigos
- **GSAS-II (Toby & Von Dreele, 2013 — Resumo e documentação oficial APS/OSTI):**
  - Integra redução de dados (calibração e integração de detectores 2D e 1D), busca de picos, indexação, solução de estrutura (*charge flipping*, Monte Carlo) e **refinamento de Rietveld**, além de ajustes alternativos de intensidade sem modelo estrutural completo (*Pawley* e *Le Bail*), refinamento sequencial/paramétrico e exportação `pdCIF`.
  - Escrito majoritariamente em **Python orientado a objetos**, apoiado em **NumPy** e **SciPy** (com extensões pontuais em Fortran para velocidade), atingindo desempenho comparável a código compilado.
- **Profex / BGMN (Doebelin & Kleeberg, 2015 — texto completo):**
  - **Convolução rigorosa de parâmetros fundamentais (BGMN):** Todos os ajustes de perfil aplicam a convolução estrita entre contribuições de **comprimento de onda, geometria do difratômetro e efeitos da amostra**. A geometria instrumental (aberrações complexas de difratômetros laboratoriais) é pré-calculada por simulação **Monte Carlo** (`GEOMET`), deconvoluída (`VERZERR`) e interpolada (`MAKEGEQ` $\to$ arquivos binários `*.geq`). **Durante o refinamento Rietveld, os parâmetros instrumentais permanecem fixos e apenas os parâmetros de alargamento da amostra (tamanho de cristalito isotrópico/anisotrópico e microdeformação) são refinados.**
  - **Convergência estabilizada automaticamente:** O BGMN implementa estratégia embutida de liberação sequencial de parâmetros refináveis, ativando modelos anisotrópicos complexos (como correção de orientação preferencial) apenas em estágios posteriores e **desativando-os automaticamente quando não há informação suficiente** (intensidade, número ou separação de picos) no difratograma — evitando divergência numérica.
  - **Linguagem programável de descrição estrutural:** Permite formular modelos para **descrição estatística de falhas de empilhamento (*stacking faults*, Ufer et al., 2008)** e **padrões de difração unidimensionais de amostras orientadas (Ufer et al., 2012)**, além de refinamentos paramétricos.

### Análise crítica — Agente B
- Do ponto de vista físico da caracterização de carbonos lamelares (grafite, GO, rGO), dois mecanismos do BGMN/Profex são particularmente relevantes:
  1. A separação estrita $B_{\text{inst}}$ (pré-calculada por parâmetros fundamentais em `*.geq`) vs. $B_{\text{amostra}}$ implementa exatamente a exigência física de **Holzwarth & Gibson (2011)** e **Iwashita et al. (2004)** para que tamanho de cristalito ($L_c$, $L_a$) e microdeformação não sejam contaminados pelo alargamento do equipamento.
  2. A capacidade de modelar **falhas de empilhamento estatísticas** (Ufer et al., 2008) e difração 1D orientada (Ufer et al., 2012) via linguagem estrutural `*.str` supera o Rietveld isotrópico convencional para argilominerais e potencialmente materiais lamelares com desordem turboestrática — embora exija forte especialização em cristalografia para escrever tais modelos `*.str`.

---

## 4. Metodologia

### Fatos extraídos dos artigos
- **Toby & Von Dreele (2013):**
  - Desenvolvimento de arquitetura modular open-source em Python/NumPy/SciPy (Windows, macOS, Linux), com interface gráfica unificada e visualização integrada de parâmetros e ajustes (com posterior adição documentada via OSTI `1465500` de API para *scripting* em Python).
- **Doebelin & Kleeberg (2015) *(texto completo)*:**
  - **Arquitetura de software:** GUI escrita integralmente em **C++ com toolkit Qt**, usando **QuaZIP** e **zlib** para leitura de arquivos comprimidos; licença open-source **GNU GPL v2 ou posterior**; multiplataforma (Windows, macOS OS X, Linux); suporte principal ao núcleo **BGMN** e suporte legado mantido ao **FullProf.2k**.
  - **Manipulação de dados brutos (Tabela 1 e 2 do artigo):** Conversores nativos independentes de fabricante (incluindo formatos proprietários Bruker `RAW`/`BRML`, PANalytical `XRDML` etc. classificados nos níveis A, B e C de suporte, além de ASCII genérico $2\theta\text{–}I$); escalonamento linear, $\log_{10}$ ou $\sqrt{I}$; cursores interativos para inspeção de raias $K\alpha_1$, $K\alpha_2$, $K\beta$ (e linhas de tungstênio $W\ L\alpha_1$, $W\ L\beta_1$) e ruído estatístico.
  - **Fluxo de trabalho automatizado no Profex:** Seleção de arquivo de configuração instrumental (`*.geq`) e arquivos de estrutura (`*.str`) em repositório local ou de rede $\to$ criação automática de arquivo de controle e variáveis `GOAL` $\to$ importação semi-automática de arquivos **CIF** ou **ICDD PDF-4+ XML** para gerar `*.str` $\to$ execução em *background* com alocação controlada de núcleos de CPU $\to$ **processamento em lote (*batch processing*)** aplicando um arquivo de controle a centenas de varreduras $\to$ exportação consolidada de `GOAL`s globais/locais e composição química calculada para **CSV**, além de gráficos vetoriais **SVG**, **PNG** e scripts **Gnuplot**.
  - **Reprodutibilidade:** Recurso de *Refinement Presets* com verificação de integridade por **checksum** para garantir que séries de controle de qualidade usem exatamente a mesma estratégia de refinamento.

---

## 5. Resultados

### Fatos extraídos dos artigos
- **Toby & Von Dreele (2013):**
  - Demonstrou-se que uma implementação orientada a objetos em Python/NumPy/SciPy alcança velocidade compatível com código compilado e viabiliza uma plataforma integrada da redução de dados 2D/1D até o refinamento estrutural completo (confirmada pela adoção massiva da comunidade com >6.400 citações e uso em simulações de padrões sintéticos em trabalhos recentes de ML, como Greasley & Hosein, 2023).
- **Doebelin & Kleeberg (2015) *(texto completo)*:**
  - Demonstrou-se na prática a robustez do fluxo em lote ao processar **mais de 600 conjuntos de dados (*datasets*)** em batelada mantendo a interface responsiva por meio de execução multithread.
  - Exportação unificada de parâmetros globais (frações de fases normalizadas, deslocamento de altura da amostra, *zero offset*) e locais (parâmetros de rede, **tamanhos médios de cristalito, microdeformação**, coordenadas atômicas, ocupação de sítios) e tabela de composição química em porcentagem de óxidos para comparação direta com XRF.
  - Validação por adoção independente citada no texto (Pujari-Palmer et al., 2015; Bobrovs et al., 2015).

### Análise crítica — Agente B
- Tanto o **GSAS-II** quanto o **Profex/BGMN** provam que a comunidade cristalográfica já resolveu com excelência de código aberto: (i) leitura de formatos proprietários, (ii) modelagem rigorosa do perfil instrumental, (iii) refinamento multifásico e extração de tamanho/microdeformação quando há modelos cristalinos 3D ou modelos estatísticos `*.str` bem formulados.
- **Onde reside a lacuna para grafeno/GO/rGO?** Esses softwares são centrados em **refinamento Rietveld baseado em estrutura cristalina periódica**. Em amostras de **grafeno de poucas camadas, GO hidratado variável ou rGO altamente turboestrático**, muitas vezes não há uma célula unitária periódica única capaz de descrever simultaneamente flocos curvados, distribuição contínua de espaçamento $d_{002}$ e bandas bidimensionais assimétricas `(hk)` sem construir modelos estatísticos altamente especializados (e não padronizados para grafeno) ou recorrer à equação de Debye.

---

## 6. Limitações

### Fatos extraídos dos artigos
- **Doebelin & Kleeberg (2015) *(explicitadas no texto completo)*:**
  - A estratégia de **baixo nível de abstração** (edição de arquivos de texto de controle e `*.str`) impõe uma **curva de aprendizado mais íngreme** ao usuário novato.
  - A programação de modelos avançados no BGMN (ex.: falhas de empilhamento ou estruturas orientadas 1D) **não é trivial** e exige domínio profundo de palavras-chave, variáveis e funções predefinidas do BGMN.
  - Na importação de CIFs, muitos arquivos CIF não trazem todas as informações exigidas pelo formato `*.str` (ex.: número de grupo espacial, símbolo Hermann-Mauguin, ajuste de célula ou símbolos de Wyckoff), demandando intervenção guiada do usuário.
  - A estimativa de composição química assume amostra livre de **fases amorfas** e refinamento preciso de ocupações de sítio.
  - A identificação de fases integrada no Profex (visualização de linhas $hkl$ dos `*.str` locais) é explicitamente descrita pelos autores como um meio **rudimentar** (*rudimentary means of phase identification*), não substituindo um sistema dedicado de *search-match*.
- **Toby & Von Dreele (2013):**
  - *Lacuna documental:* Sem acesso ao texto integral de 2013, detalhes internos de implementação numérica específica daquela versão inicial não foram inspecionados (observando-se na documentação OSTI que a biblioteca de *scripting* para Python foi expandida posteriormente em 2018).

### Análise crítica — Agente B
- Para a caracterização de **grafeno e derivados**:
  1. Nem GSAS-II nem Profex oferecem fluxos automatizados prontos (*turnkey*) para caracterização diagnóstica de **grafite $\leftrightarrow$ GO $\leftrightarrow$ rGO $\leftrightarrow$ carbono turboestrático**, cálculo de $L_a$ pela banda bidimensional assimétrica `(10)` de Warren, ou verificação automática de armadilhas interpretativas do pico `(002)`.
  2. Ambos exigem conhecimento cristalográfico substancial para evitar modelos fisicamente absurdos (ex.: tentar refinar uma monocamada ou GO desordenado como grafite $2H$ cristalino ideal ajustando parâmetros de orientação preferencial e microdeformação irreais até obter um bom $R_{wp}$ estatístico, porém sem significado físico).

---

## 7. Contribuição para a dissertação

- **Análise — Agente B:**
  1. **Mapeamento rigoroso do estado da arte em software livre de DRX:** Evita que a dissertação proponha desenvolver "mais um visualizador ou refinador Rietveld genérico". GSAS-II e Profex/BGMN já cumprem esse papel com décadas de desenvolvimento acumulado.
  2. **Arquitetura de integração e referência em Python:** O sucesso do GSAS-II (Python + NumPy/SciPy) confirma a viabilidade computacional do ecossistema Python científico para processamento de DRX; além disso, GSAS-II pode atuar como motor de referência ou gerador de padrões simulados com alargamento realista (como feito por Greasley & Hosein, 2023).
  3. **Identificação da lacuna específica para o projeto UFCA:** Há espaço para uma camada computacional **especializada em materiais carbonosos bidimensionais e desordenados** (ou na ponte interpretativa DRX + MEV + AFM), operando antes ou complementarmente ao Rietveld formal: triagem automatizada de assinaturas `(002)` / `(001)` / `(10)`, diagnóstico de desordem turboestrática e alertas contra falsas inferências de monocamada.

---

## 8. Possíveis aplicações

- **Proposições — Agente B (sem extrapolar resultados não lidos):**
  - Utilizar **Profex/BGMN** (por sua modelagem rigorosa de perfil instrumental `*.geq` e suporte a formatos comerciais) ou **GSAS-II** (via API Python) como linha de base de validação para comparar extrações de $d_{002}$, FWHM, tamanho de cristalito e microdeformação em amostras de grafite e compósitos cristalinos de referência no laboratório.
  - Desenvolver um protótipo em Python capaz de exportar relatórios estruturados e metadados compatíveis com importação posterior em **GSAS-II**, **Profex** ou **XMatcher**, funcionando como módulo de triagem inicial para grafeno/GO/rGO antes de análises cristalográficas avançadas.

---

## 9. Evidências

- **Toby & Von Dreele (2013) (`10.1107/S0021889813003531`):**
  - *Abstract* oficial completo (OpenAlex `W1967485833`): arquitetura Python orientada a objetos usando NumPy/SciPy; substituição de GSAS e EXPGUI; suporte a dados de pó e monocristal, raios X e nêutrons (fontes laboratoriais e síncrotron, detectores 1D e 2D), redução, solução de estrutura e refinamento.
  - Documentação técnica pública dos autores (OSTI `1465500` e `1542591`, GitHub `AdvancedPhotonSource/GSAS-II`): detalhamento de *sequential fitting*, Pawley/Le Bail e interface de *scripting*.
- **Doebelin & Kleeberg (2015) (`10.1107/S1600576715014685` / `PMC4603273`):**
  - **Texto completo** lido integralmente (`Doebelin_2015_Profex_PMC4603273.txt`): seções *Introduction*, *BGMN* (convolução Monte Carlo `GEOMET`/`VERZERR`/`MAKEGEQ`, fixação de parâmetros instrumentais vs. amostra, convergência estabilizada, modelos de *stacking faults* Ufer et al. 2008 e amostras orientadas 1D Ufer et al. 2012), *BGMNwin interface*, *AUTOQUAN*, *Profex* (C++/Qt, GPLv2+), *Data file handling*, *Internal structure and device file databases*, *Control, structure and results file management*, *Batch processing* (>600 datasets), *Exporting results*, *Creating structure and device files* (CIF/ICDD XML), *Chemical composition*, *Refinement presets* (checksums) e *Summary*.

---

## 10. Prioridade de estudo

- **Prioridade:** **Média-Alta (leitura já concluída para Profex; consulta prática ao tutorial/API Python do GSAS-II conforme necessidade de implementação).**
- **Justificativa:** Indispensável para a seção de *Softwares Existentes* e *Análise de Originalidade* da dissertação, garantindo que o pesquisador conheça as capacidades, licenças e limites dos dois principais pacotes open-source de cristalografia de pós antes de definir o escopo computacional de DRX da ferramenta proposta.
