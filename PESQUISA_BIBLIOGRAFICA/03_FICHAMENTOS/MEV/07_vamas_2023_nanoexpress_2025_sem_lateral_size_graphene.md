# Fichamento 07 — Protocolos Metrológicos para Dimensões Laterais de Flocos de Grafeno e Óxido de Grafeno por MEV: VAMAS TWA 41 / NPL AS 103 (2022/2023) & Chemello et al. (*Nano Express*, 2025)

> **Status de Leitura e Verificação (Documento Integrado de 2 Fontes Complementares):**
> 1. **Despotelis, Pollard, Clifford & Paton (2022/2023) — NPL Report AS 103 (VAMAS TWA 41 Project 12):** **Texto completo lido integralmente** em `_scratch/textos_extraidos/NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.md` (24 páginas, 17 figuras).
> 2. **Chemello, Despotelis, Paton, Clifford, Pollard, Radnik & Hodoroaba (2025) — *Nano Express*:** **Texto completo lido via versão *Gold Open Access* (CC BY 4.0) em IOPscience** (`https://iopscience.iop.org/article/10.1088/2632-959X/adae28`, Seções 1, 2, 3, Tabelas 1–5 e parágrafo inicial da Seção 4 *Conclusions*). *Nota de transparência:* a lista pontual final logo após *"The main conclusions of this study are:"* na Seção 4 não veio renderizada na extração HTML da página, mas todos os resultados numéricos e conclusões encontram-se integralmente presentes no corpo das Seções 3 e 4.

---

## 1. Identificação bibliográfica

1. **Relatório Metrológico VAMAS TWA 41 / NPL:**
   - **Título:** VAMAS TWA 41 - Graphene and related 2D materials project 12 - Distribution of lateral size and thickness of few-layer graphene flakes using SEM and AFM. SEM and AFM measurement protocol
   - **Autores:** Konstantinos Despotelis, Andrew J. Pollard, Charles A. Clifford, Keith R. Paton (National Physical Laboratory — NPL, Reino Unido)
   - **Ano:** Documento NPL Report `AS 103` datado de novembro de 2022 (indexado OpenAlex 2023; projeto EMPIR `19NORM04 / 19NRM04 ISO-G-SCoPe`)
   - **DOI:** `10.47120/npl.as103` | Dataset associado no Zenodo: `10.5281/zenodo.10119370`
   - **Link oficial:** [https://doi.org/10.47120/npl.as103](https://doi.org/10.47120/npl.as103) (`http://eprintspublications.npl.co.uk/9631/1/AS103.pdf`)
2. **Validação Experimental e Comparação de Abordagens (*Nano Express*):**
   - **Título:** Approaches for the measurement of lateral dimensions of graphene oxide flakes using scanning electron microscopy
   - **Autores:** Giovanni Chemello, Konstantinos Despotelis, Keith R. Paton, Charles A. Clifford, Andrew J. Pollard, Jörg Radnik, Vasile-Dan Hodoroaba (BAM — Alemanha & NPL — Reino Unido)
   - **Ano:** 2025 (publicado em 5 de fevereiro de 2025)
   - **Periódico:** *Nano Express* (IOP Publishing), Vol. 6, No. 1, `015006`
   - **DOI:** `10.1088/2632-959x/adae28` | **Link oficial:** [https://doi.org/10.1088/2632-959X/adae28](https://doi.org/10.1088/2632-959X/adae28) (28 citações em `verified_catalog.json`)

---

## 2. Problema investigado

- **[Extraído dos dois documentos]:**
  - **NPL Report AS 103 (VAMAS TWA 41):** Mais de 100 fornecedores comerciais ofertam "grafeno", mas caracterizações deficientes frequentemente mascaram grafite em micropartículas ou elevada variabilidade lote a lote ("fake graphene"). A especificação técnica **`ISO/TS 21356-1:2021`** definiu procedimentos para caracterizar tamanho lateral (via MEV) e espessura (via AFM) de flocos em pós/dispersões, porém suas seções permaneceram informativas por ausência de comparação interlaboratorial (ILC) que quantificasse as fontes de incerteza e a variabilidade intra- e interlaboratorial em diferentes microscópios e operadores.
  - **Chemello et al. (2025):** Há necessidade industrial urgente de medir dimensões laterais e fatores de forma de **óxido de grafeno (GO)** comercial de forma simples, rápida e não ambígua para subsidiar a futura norma **`ISO/DTS 23879`**. Como existem duas famílias distintas de descritores normativos — a de nanopartículas por contorno (`ISO 19749` / `ISO 21363`) e a específica de grafeno por eixos ortogonais (`ISO/TS 21356-1` / NPL GPG 145) — o trabalho avalia sistematicamente: (i) preparação de amostras por *drop-casting*, (ii) discrepância entre ambas as abordagens de análise de imagem e (iii) reprodutibilidade entre laboratórios e analistas.

---

## 3. Fundamentação

- **[Extraído dos documentos]:**
  - **Física e precauções operacionais no MEV para grafeno/GO:**
    1. **Escolha do substrato vs. carregamento (*charging*):** para MEV, ambos os trabalhos adotam `wafer` de **silício com película fina de óxido nativo (`SiO2 nativo / Si`)**, porque o óxido fino mantém condutividade elétrica suficiente para dissipar carga e **minimizar carregamento sob o feixe**. Em contraste, para AFM/OM, o protocolo VAMAS usa `SiO2 (300 ± 5 nm)/Si` (grade `ISO-G-SCoPe`) para maximizar o contraste óptico interferencial.
    2. **Contaminação por carbono amorfo induzida pelo feixe:** VAMAS Sec. 4.1 e 4.2.1 explicitam que **a varredura no MEV deposita material carbonáceo na superfície**; por isso, **as medições de MEV e AFM devem ser feitas em substratos separados** (nunca medir espessura em AFM sobre floco já varrido em MEV, para não superestimar a altura!), e o ajuste de foco, abertura, `WD` e estigmador no MEV **nunca deve ser feito sobre um floco de interesse** (o alto *dwell time* modifica/contamina a região), mas sim em estrutura vizinha similar.
    3. **Baixa tensão de aceleração e detector *InLens*:** VAMAS exige `V_acc <= 5 kV` para reduzir carregamento; Chemello et al. empregam `3 kV` e `5 kV` com detector de elétrons secundários **InLens**, destacando que somente o detector *in-lens* ofereceu contraste e definição de bordas suficientes para distinguir até limites de **flocos moderadamente sobrepostos** (até 2 camadas sobrepostas; com `>= 3` sobrepostos as bordas tornam-se ambíguas).
  - **Duas formulações normativas de descritores morfológicos (Chemello et al., Fig. 1):**
    - **Abordagem A1 (Contorno completo — `ISO 19749` / `ISO 21363`):** delimita o contorno real do floco -> calcula Área (`A`), `minFeret` e `maxFeret` -> Diâmetro Circular Equivalente **`ECD_A1 = 2 * sqrt(A / pi)`** e razão de forma **`Feret ratio = minFeret / maxFeret`**.
    - **Abordagem A2 ("Cruz" comprimento × largura — `ISO/TS 21356-1` / VAMAS AS 103 / NPL GPG 145):** ajusta visualmente o menor retângulo/elipse envolvente, mede o comprimento (`L`, maior dimensão borda-a-borda dentro do floco) e a largura (`W`, segmento contido no floco **perpendicular e bissetor de `L`**; em casos ambíguos usa-se `minFeret` como `W` e sua bissetriz como `L`). VAMAS usa `(L + W)/2` com desvio padrão como incerteza; Chemello (A2) calcula a área da elipse de eixos `L, W`, derivando **`ECD_A2`** e **`Aspect Ratio (AR) = W / L`**.
  - **Distribuição estatística lognormal vs. gaussiana:** tamanhos laterais de flocos esfoliados/GO ajustam-se a uma **distribuição lognormal** (`>= 20` *bins* no VAMAS), enquanto fatores de forma (`Feret ratio` e `AR`) seguem **distribuição gaussiana**.

---

## 4. Metodologia

- **[Extraído de NPL Report AS 103 (VAMAS TWA 41)]:**
  - **Triagem óptica prévia (Sec. 3):** uso de OM (`20×–50×`) para mapear zonas com flocos bem separados e abundantes, evitando resíduos de solvente que alteram contraste (Fig. 4).
  - **Protocolo MEV rigoroso (Sec. 4.2–4.4):**
    - Montagem reversível sem risco de riscar/quebrar o *wafer*;
    - `V_acc <= 5 kV`, detector SE;
    - Passo 1–2: imagem de baixa magnificação (`~10.000×`) em área rica em flocos isolados;
    - Passo 3: imagens de maior resolução (tipicamente **`> 20.000×`**) enquadrando o floco inteiro com **tamanho de pixel `< 10 nm`**, analisando **pelo menos `200` flocos isolados** aleatórios e **todos** os flocos elegíveis em cada imagem (proibido selecionar apenas flocos grandes ou fáceis; excluem-se flocos tocando outros, sobrepostos sem circunferência visível ou não identificados como flocos); garantir que flocos fotografados em múltiplas magnificações sejam contados uma única vez;
    - Passo 5 & Sec. 4.3.1: **calibração dimensional pós-ensaio obrigatória** com grade certificada `Pelcotec G-1T um` montada junto à amostra e medida nas **mesmas condições (`WD`, `V_acc`, magnificação `20.000×–40.000×`)** em `3` áreas distintas (`>= 5` quadrados em X e `>= 5` em Y, via perfil linear ou FFT no mesmo software).
  - **Acoplamento estatístico com AFM (Sec. 5):** medir **`>= 20` flocos isolados e planos** (sem dobras/resíduos nem artefatos de ponta dupla/deriva) no AFM em modo contato intermitente (*tapping*, closed-loop, `512×512 px` para `(0,5 µm)²` a `(2 µm)²`, *set-point* `40% < sp <= 70%`) cobrindo exatamente a faixa de tamanhos laterais encontrada no MEV; extrair média de 3 perfis de altura e plotar espessura vs. tamanho lateral com `R²`.
- **[Extraído de Chemello et al. (2025)]:**
  - **Material e otimização de preparo:** dispersão aquosa comercial de GO (`0,4 mass-%`, Graphenea, `>95%` monocamada). Limpeza dos wafers `Si/SiO2 nativo` (`1×1 cm`) por ultrassom em etanol (10 min), IPA (10 min), ozônio (30 min) e secagem com `N2`. Diluição de `10 µL` da suspensão em `8 mL H2O DI + 8 mL IPA`, **sonicação breve de apenas `1 min` após diluição** (evitando ultrassonicação longa que fragmenta/esfolia flocos), *drop-cast* de `10 µL` à temperatura ambiente e secagem *overnight* em dessecador -> `3` amostras replicadas (`GO1, GO2, GO3`).
  - **Aquisição em dois laboratórios:**
    - `L1 (M1)`: `Zeiss Supra 40` (emissor Schottky, **InLens**), `3 kV`, `WD = 4–5 mm`, largura de campo `37,6 µm`, pixel `< 50 nm/px`, corrente `< 1 nA`; calibrado com referência certificada `100 nm CD-XC01-0913`.
    - `L2 (M2)`: `Zeiss Supra` (**InLens**), `5 kV`, `WD = 4,2 mm`, pixel `< 15 nm/px`; calibrado com `Pelcotec 687-01 CDMS-0.1C` rastreável ao NIST (`2–20 kV`).
  - **Análise no software aberto `Fiji ImageJ v1.54c`:** medição manual de `>= 200` flocos por amostra em zonas de "densidade média" (entre anéis de café — *coffee rings* — e zonas de baixa densidade), aplicando `A1` e `A2` sobre exatamente os mesmos flocos, além de análise cruzada inter-operadores (`O1` em L1 vs. `O2` em L2) sobre as mesmas imagens de `GO2/M2`.

---

## 5. Resultados

- **[Extraído de Chemello et al. (2025)]:**
  - **Padrões de deposição heterogêneos (Fig. 2):** mesmo sob preparo idêntico, `GO1` exibiu deposição em baía com mais flocos isolados, enquanto `GO2` e `GO3` formaram anéis de café (*coffee rings*) concêntricos onde flocos sobrepostos impedem segmentação. Zonas de densidade média entre os anéis mostraram-se ideais para análise.
  - **Comparação A1 vs. A2 em `>= 200` flocos (`GO1, GO2, GO3`, Tabelas 2–3, Figs. 4–5):**
    - `ECD_A1` médio lognormal: `2,11 ± 1,04 µm` (`GO1`), `2,10 ± 1,13 µm` (`GO2`), `1,76 ± 1,05 µm` (`GO3`); média global **`1,99 ± 0,20 µm`** (**RSD entre amostras = `10,0%`**).
    - `ECD_A2` médio lognormal: `2,21 ± 1,10 µm` (`GO1`), `2,17 ± 1,15 µm` (`GO2`), `1,84 ± 1,10 µm` (`GO3`); média global **`2,07 ± 0,20 µm`** (**RSD entre amostras = `9,8%`**).
    - **Viés sistemático entre abordagens:** `A2` superestima consistentemente o ECD médio em **`3–5%`** (`4,0%` na média geral: `+4,7%`, `+3,3%`, `+4,5%`) em comparação à medida exata por área (`A1`). Medir `100` flocos extras em outras regiões de `GO3` elevou `ECD` para `2,13 ± 1,15 µm`, confirmando que a diferença de `GO3` decorreu de **segregação espacial no substrato / escolha de região**.
    - **Descritores de forma (Tabela 3):** `Feret ratio (A1)` = `0,63–0,65` (média **`0,64`**, **RSD = `1,6%`**); `Aspect ratio (A2)` = `0,58–0,60` (média **`0,59`**, **RSD = `2,0%`**). `A2` subestima o fator de forma em **`~7,8–9,4%`** (porque `W <= minFeret` em contornos irregulares). A forma mostrou-se quase invariante mesmo quando o tamanho variou entre áreas!
  - **Variabilidade inter-operadores nas *mesmas* imagens vs. troca de região/equipamento (`GO2`, Tabelas 4–5, Figs. 6–7):**
    - Quando dois analistas (`O1` e `O2`) mediram **exatamente os mesmos flocos** nas imagens `GO2/M2`: `ECD_A1` deu `1,39 µm` vs. `1,43 µm` (**RSD = `2,0%`**), `ECD_A2` deu `1,44 µm` vs. `1,35 µm` (**RSD = `4,6%`**), e tanto `Feret ratio` (`0,60`) quanto `AR` (`0,56`) apresentaram **RSD = `0,0%` (desvio nulo!)**.
    - Em contraste, comparando `GO2/M1` (`~2,10–2,17 µm`) contra `GO2/M2` (`~1,35–1,44 µm`, outra região do *mesmo* wafer medida em L2), surgiu uma discrepância de **quase `30%`** no ECD médio — provando que **a escolha da área amostral e a heterogeneidade da deposição superam em quase uma ordem de grandeza a variabilidade entre analistas ou entre A1/A2**!
  - **Tempo e horizonte de IA:** análise manual de 200 flocos requer **várias horas**, e os autores concluem indicando que **análise automatizada assistida por IA** (com pré-treinamento manual apropriado) é o caminho para acelerar o processo e lidar com flocos sobrepostos/aglomerados.
- **[Extraído de NPL Report AS 103]:** o documento define integralmente o protocolo de coleta e reporte padronizado (planilhas Excel e formatos brutos) sem publicar ainda os resultados interlaboratoriais finais dos laboratórios participantes (o protocolo de 2022/2023 prepara a rodada ILC e o dataset Zenodo).

---

## 6. Limitações

- **[Reconhecidas nos dois documentos]:**
  - **Incerteza dominante de preparo e amostragem espacial (*coffee rings* e segregação):** mesmo sob limpeza com ozônio e diluição padronizada em H2O/IPA, o *drop-casting* gera regiões heterogêneas (anéis de café excluídos da estatística) e desvios de `~10%` entre amostras replicadas ou até `~30%` entre áreas distintas do mesmo substrato (Chemello et al., 2025).
  - **Incapacidade de resolver `>= 3` flocos sobrepostos manualmente:** mesmo usando detector *InLens*, empilhamentos de 3 ou mais flocos inviabilizam delimitar bordas individuais, levando à exclusão desses objetos — o que pode introduzir **viés de seleção populacional** caso flocos maiores ou mais grossos aglomerem preferencialmente nos anéis de café.
  - **Custo de mão de obra manual:** anotar `>= 200` flocos no `Fiji/ImageJ` leva horas por amostra, limitando controle de qualidade rotineiro em escala industrial.
  - **Impossibilidade de correlacionar MEV -> AFM no mesmo floco após feixe eletrônico (VAMAS):** deposição de carbono induzida por MEV impede reutilizar a mesma área para altura atômica no AFM (exigindo correlação estatística em substratos separados, e não floco a floco direto na ordem MEV->AFM).
- **[Críticas adicionais — Agente C]:**
  - **Diferença de protocolo entre os dois documentos quanto à resolução mínima de pixel:** o relatório VAMAS (GNPs) exige `< 10 nm/pixel` (`> 20.000×`), ao passo que Chemello et al. em L1 (`Zeiss Supra 40`) aceitaram `< 50 nm/pixel` (largura de `37,6 µm`) porque os flocos de GO comerciais tinham ECD médio de `~2 µm`; usar `50 nm/px` em nanoplaquetas menores (ex.: `100–300 nm` previstas no VAMAS) causaria erro severo de quantização geométrica (apenas `2–6` pixels por floco!). Logo, ferramentas computacionais devem impor critério mínimo de pixels por diâmetro equivalente (ex.: `>= 15–20 px`), não apenas resolução nominal fixa.
  - **Aproximação elíptica da abordagem A2:** em flocos altamente irregulares, côncavos ou dobrados (comuns em GO e LPE), aproximar área por elipse `pi*L*W/4` introduz erro sistemático (`+3–5%` no ECD e `-8–9%` na razão de forma) frente ao contorno `A1`, que a automação computacional baseada em máscaras de segmentação elimina naturalmente calculando área, `minFeret`, `maxFeret`, circularidade e razão de aspecto diretamente do polígono segmentado!

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Este par de fontes é o **núcleo metrológico** que ancora a dissertação no que o MEV faz **com excelência comprovada e normalizada** (`ISO/TS 21356-1`, `ISO/DTS 23879`, `VAMAS TWA 41`): **distribuição estatística de dimensões laterais e morfologia planar de flocos (`>= 200` flocos)**, em contraponto claro às restrições do MEV para espessura atômica.
  1. **Define exatamente os algoritmos e métricas geométricas que a ferramenta deve implementar em `Python/OpenCV/scikit-image`:** replicar e automatizar integralmente a **Abordagem A1** (`area`, `ECD = 2*sqrt(A/pi)`, `minFeret`, `maxFeret`, `Feret ratio`, circularidade `4*pi*A/P^2`) e também calcular os equivalentes da **Abordagem A2** (`L` e largura bissetriz perpendicular `W`, razão de aspecto `W/L`, área elíptica), ajustando automaticamente histogramas lognormais (`>= 20 bins`) para tamanho e gaussianos para forma, além da fração de recobrimento (`area_flocos / area_campo`).
  2. **Fornece uma justificativa numérica irrefutável para o trabalho:** `Chemello et al. (2025)` demonstraram em `Fiji/ImageJ` que a variabilidade entre analistas na *mesma* imagem é apenas `2–4,6%`, mas que a anotação manual de `200` flocos consome **várias horas** e que a **amostragem espacial limitada** induz vieses de `10–30%`. Uma ferramenta automatizada por visão computacional + ML permite processar dezenas de campos de visão não sobrepostos em minutos (eliminando viés de amostragem local e acelerando o fluxo em ordens de grandeza!).
  3. **Integra MEV e AFM com rigor físico no workflow da dissertação:** estabelece as regras práticas para o laboratório do PPGCEM: (a) usar `Si/SiO2 nativo` para MEV (evitar carregamento) e `SiO2 300 nm` separado para AFM (evitar contaminação carbonácea de MEV sobre as amostras AFM!); (b) calibrar `nm/pixel` antes ou depois com grade padrão; (c) usar MEV para estatística rápida de `>= 200` flocos laterais + morfologia e AFM para espessura em `>= 20` flocos representativos.

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Desenvolver um **módulo de metrologia morfológica compatível com `ISO/TS 21356-1` e `ISO/DTS 23879`** que exporte, para cada micrografia MEV calibrada (ou lote de micrografias), uma tabela por floco (ID, Área `µm²`, Perímetro `µm`, `ECD_A1`, `L` e `W` bissetriz `A2`, `minFeret`, `maxFeret`, `Feret ratio`, `AR`, circularidade, e fração de recobrimento total), acompanhada de ajuste automático de distribuição **lognormal** (com `>= 20` bins) e **gaussiana**, além de verificação de critério de qualidade (`pixel_size` vs. tamanho mínimo de floco em pixels, exclusão automática de flocos tocando as bordas da imagem).
  - Validar o módulo computacional contra medições manuais no `Fiji/ImageJ 1.54c` seguindo exatamente a comparação `A1` vs. `A2` e a tolerância inter-operadores (`2–4,6%`) estabelecida por Chemello et al. (2025).

---

## 9. Evidências

- **NPL Report AS 103 (VAMAS TWA 41 Project 12):**
  - Seção 2 (pp. 1–3): especificação de substratos distintos (`Si` óxido nativo para MEV vs. `300±5 nm SiO2/Si` para AFM).
  - Seção 4.1–4.2 (pp. 6–9) & Fig. 5: contaminação carbonácea induzida por feixe e carregamento; foco em feição vizinha; `V_acc <= 5 kV`; `10.000× -> >20.000×`; pixel `< 10 nm`; `>= 200` flocos isolados; calibração `Pelcotec G-1T um`.
  - Seção 4.3–4.4 (pp. 10–12) & Fig. 7: definição da bissetriz perpendicular `L, W`, exclusão de aglomerados/sobreposições, histograma lognormal (`>= 20` bins) e protocolo de reporte.
  - Seção 5 (pp. 13–22) & Figs. 10–17: protocolo AFM em `>= 20` flocos cobrindo a faixa lateral do MEV e correlação `espessura vs. tamanho lateral`.
- **Chemello et al. (*Nano Express*, 2025):**
  - Seção 2.2–2.4 & Fig. 1: preparação de GO sem sonicação destrutiva (1 min pós-diluição), parâmetros `Zeiss Supra` InLens `3 kV`/`5 kV`, análise no `Fiji ImageJ 1.54c` com definições formais de `A1` vs. `A2`.
  - Seção 3.1 & Fig. 2: zonas de deposição (*coffee rings* vs. baixa vs. média densidade) e visibilidade de até 2 flocos sobrepostos via InLens.
  - Seção 3.2–3.3, Tabelas 2–5 & Figs. 4–7: resultados numéricos completos (`ECD_A1 = 1,99 µm` vs `ECD_A2 = 2,07 µm`, `+3–5%`; `Feret ratio = 0,64` vs `AR = 0,59`, `-8–9%`; RSD inter-amostras `~10%`, inter-regiões `M1/M2 ~30%`, inter-analistas `2,0%`/`4,6%` ECD e `0,0%` forma).
  - Seção 4 (*Conclusions*): tempo manual (várias horas para 200 flocos) e recomendação explícita de automação assistida por IA para produtividade e flocos sobrepostos.

---

## 10. Prioridade de estudo

- **Prioridade:** **ALTA (Artigo e protocolo indispensáveis para 17/11/2026).**
- **Justificativa:** Constituem os documentos normativos e experimentais **mais diretamente aplicáveis** ao objetivo prático de uma ferramenta computacional para MEV no PPGCEM/UFCA. Respondem com rigor metrológico a praticamente todas as perguntas potenciais de banca sobre preparação de amostra, controle de carregamento/contaminação, escolha de detector (`InLens`), amostragem estatística (`>= 200` flocos), métricas geométricas corretas (`ECD`, `Feret`, razão de aspecto), separação entre MEV (lateral) e AFM (espessura) e validação quantitativa contra o software padrão de referência (`Fiji/ImageJ`).
