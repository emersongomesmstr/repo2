# Fichamento 03 — Zhou et al. (2016): Imageamento Quantitativo por Elétrons Secundários para Extração de Função Trabalho e Identificação de Camadas de Grafeno

> **Status de Leitura e Verificação:** **Texto completo lido integralmente** em `_scratch/textos_extraidos/Zhou_2016_Quantitative_SE_Imaging_Work_Function_Graphene.md` (artigo *Open Access* CC BY 4.0 em *Scientific Reports*, 8 páginas). As Seções S1–S10 da *Supplementary Information* citadas no artigo não compõem o arquivo extraído e ficam registradas como complementos não inspecionados diretamente.

---

## 1. Identificação bibliográfica

- **Título:** Quantitative secondary electron imaging for work function extraction at atomic level and layer identification of graphene
- **Autores:** Yangbo Zhou, Daniel S. Fox, Pierce Maguire, Robert O’Connell, Robert Masters, Cornelia Rodenburg, Han-Chun Wu, Maurizio Dapor, Ying Chen, Hongzhou Zhang
- **Ano:** 2016 (recebido em 29 out 2015; aceito em 25 nov 2015; publicado em 16 fev 2016)
- **Periódico:** *Scientific Reports* (Nature Portfolio), Vol. 6, `21045`
- **DOI:** `10.1038/srep21045`
- **Link oficial:** [https://doi.org/10.1038/srep21045](https://doi.org/10.1038/srep21045) (`https://www.nature.com/articles/srep21045`)
- **Métricas catalogadas:** 46 citações registradas em `_scratch/verified_catalog.json`.

---

## 2. Problema investigado

- **[Extraído do artigo]:** A função trabalho (`Phi`) de materiais 2D como o grafeno depende fortemente do número de camadas (variando dezenas de meV por camada atômica até ~4 camadas), além de dopagem química, deformação (*strain*), substrato e contaminantes, sendo decisiva para o desempenho de transistores, sensores, células solares e emissores de campo. Técnicas convencionais para medir função trabalho (como microscopia de força por sonda Kelvin / KPFM ou microscopia de fotoemissão eletrônica / PEEM) apresentam severas limitações de interferência ambiental/interação ponta-amostra ou baixa vazão e resolução espacial. Embora o contraste de elétrons secundários (SE) em MEV e microscopia iônica de hélio (HIM) seja fisicamente limitado pela barreira de potencial superficial (`Phi`), estudos anteriores de contagem de camadas por SE apresentavam inconsistências e **nenhum método quantitativo reproduzível e independente de instrumento** havia sido estabelecido para identificar camadas e extrair diretamente a função trabalho nanométrica a partir de imagens SE.

---

## 3. Fundamentação

- **[Extraído do artigo]:**
  - **Visibilidade óptica vs. contraste SE em múltiplos substratos:** a microscopia óptica (OM) depende da interferência de reflexão na interface ar/grafeno/dielétrico, restringindo a visibilidade a substratos dielétricos específicos (como `SiO2 285 nm/Si`) e tornando o grafeno praticamente invisível sobre metais monoatômicos (`Au`, `Cu`, `Ni`). Já o contraste SE (definido no texto como razão normalizada entre intensidade do grafeno `I_g` e do substrato `I_s` — nota: há erro tipográfico na p. 2 escrevendo `I_g/I_g - 1` onde fisicamente e dimensionalmente aplica-se `(I_g/I_s - 1)*100%`) exige apenas `|C_g| > ~2%` para detecção e funciona com feixes de elétrons (MEV) ou íons `He+` (HIM) sobre substratos isolantes e metálicos.
  - **Modelo analítico de contraste SE de monocamada — Eq. (1):** o grafeno suportado é excitado simultaneamente pelo feixe primário (`I_p`) e pelos elétrons retroespalhados (BSE) vindos do substrato (`eta_s * I_p`):
    $$C_g(E_p) = \frac{\delta_g(E_p)}{\delta_s(E_p)} \cdot \left[1 + \beta \cdot \eta_s(E_p)\right] + \text{const}$$
    onde `delta_g, delta_s` são os rendimentos SE de grafeno e substrato, `eta_s` é o rendimento BSE do substrato e `beta` corrige a energia menor dos BSEs em relação ao feixe primário. Em metais (`Au`, `Cu`, `Ni`), a variação de `eta_s` com `E_p` é pequena, mantendo `C_g` quase constante (`~10%`); já em `SiO2/Si`, `eta_s(E_p)` e `delta_s(E_p)` geram forte dependência energética (com desvios abaixo de `1 keV` devido ao **carregamento** do substrato isolante, que suprime o rendimento SE).
  - **Modelo de `N` camadas com atenuação exponencial — Eq. (2):** para `N` camadas (espessura por camada `d = 0,335 nm`), soma-se a transmissão atenuada dos SEs gerados no substrato através do grafeno:
    $$C_g(N) = \frac{\delta_g(N)}{\delta_s} \cdot (1 + \beta \cdot \eta_s) + \alpha \cdot e^{-N \cdot d / \lambda} - 1$$
    onde `alpha` descreve a reflexão na interface grafeno-vácuo e `lambda` é o **livre caminho médio inelástico (IMFP)** dos SEs no grafeno. Para `N >= 4`, `Phi(N)` e portanto `delta_g(N)` tornam-se constantes e, enquanto `N*d / lambda << 1`, o contraste decai linearmente com `N`; para espessuras muito grandes (`N > 100`, grafite), `e^(-N*d/lambda) -> 0` e o contraste satura.
  - **Extração da função trabalho via distribuição de Chung & Everhart — Eqs. (3) e (4):** o espectro de energia cinética `E_K` dos SEs segue `d(delta)/dE_K ∝ E_K / (E_K + Phi)^n`, permitindo converter o desvio não linear de `C_g(N)` em `1 <= N <= 3` relativamente à reta extrapolada de atenuação (`C_gi(N)` para `N >= 4`) na função trabalho absoluta por camada:
    $$\varphi(N) = \varphi(4) \left[ 1 + \frac{C_g(N) - C_{gi}(N)}{C_g(\infty) + 1} \right]^{1/(2-n)}$$
  - **Origem eletrônica:** conforme a estrutura de bandas passa da dispersão linear (monocamada) para parabólica (bicamada) e tipo grafite (`4L`), a diferença entre o nível de Fermi `E_F` e o nível de vácuo `E_0` aumenta, elevando `Phi` e reduzindo o escape de SEs de baixa energia.

---

## 4. Metodologia

- **[Extraído do artigo — Seção Methods]:**
  - **Amostras e controle independente (ground truth):** flocos de grafeno preparados por **esfoliação micromecânica** sobre `SiO2 (285 nm) / Si fortemente p-dopado`, com posição e número de camadas previamente confirmados por **contraste de reflexão óptica** (`Olympus BX51`, objetiva `50×`) e **espectroscopia Raman** (referenciando Ni et al., 2007 e Ferrari et al., 2006). Amostras em metais (`50 nm` de `Au`, `Cu`, `Ni` sobre Si) foram transferidas via filme de PMMA (removido em acetona quente `~50 °C` e IPA quente `~50 °C`). Grafeno suspenso foi transferido sobre matriz de furos circulares de `2 µm` de diâmetro e `> 10 µm` de profundidade em `Si`.
  - **Aquisição em MEV:** realizada em **dois equipamentos distintos** (`Carl Zeiss Supra` e `FEI Strata DB235`) para testar reprodutibilidade inter-instrumento. Energia primária variada de `0,5` a `20 keV`. Para minimizar dano de irradiação, contaminação e influência de BSE/SE da câmara, fixaram-se estritamente:
    - Detector: **through-the-lens (*in-lens*)**;
    - Abertura: `10 µm`; corrente de feixe: `5` a `20 pA` (dose por varredura de `~3×10^13` a `~1,2×10^14 e-/cm²`);
    - Distância de trabalho (`WD`): `4 mm`; magnificação: `2.500×`; resolução: `1024 × 768 px`; tempo de varredura: `26 s`; vácuo de base `~2×10^-5 mbar`.
  - **Aquisição em HIM:** `Carl Zeiss Orion Plus` a `30 keV He+`, `WD = 10 mm`, FoV `80 µm`, detector Everhart-Thornley, corrente `1 pA` (dose `~5×10^11 ions/cm²`), com canhão de inundação de elétrons (*electron flood gun*, `500 eV`, tempo de inundação otimizado em `10 µs`) para neutralizar o carregamento positivo de substratos isolantes `SiO2/Si`.
  - **Espectroscopia de energia de SE (validação independente):** filtro passa-alta construído com grade de TEM (`400 µm` de diâmetro de furo) posicionada a `0,7 mm` acima do grafeno aterrado, varrendo tensão retardadora de `0 V` a `-10 V` e diferenciando a curva `corrente vs. tensão` para obter `d(delta)/dE_K`.

---

## 5. Resultados

- **[Extraído do artigo]:**
  - **Dependência energética e inversão de contraste em MEV (`SiO2/Si`, Fig. 1b–c):** a `0,5 keV`, a monocamada é mais clara (`C_g = +9%`); a `1,5 keV`, fica quase invisível no interior (`+1%`), permanecendo apenas contraste de borda (`7%`); acima de `2 keV` torna-se mais escura (`~ -10%` a `-20%`), atingindo máximo absoluto de contraste em **`5 keV` (`|C_g| ≈ 20%`)**. No HIM com neutralização otimizada (`10 µs`), o contraste de `1L` em `SiO2/Si` atinge **`~54%`**.
  - **Resolução espacial lateral (Fig. 2d):** o perfil transversal na borda `1L–2L` apresentou largura de transição de **`~10 nm`** tanto em MEV quanto em HIM, drasticamente superior à largura limitada por difração de **`~680 nm`** na microscopia óptica.
  - **Reprodutibilidade estatística inter-flocos e inter-instrumentos (`5 keV`, InLens, > 100 flocos, Fig. 2e):** as distribuições gaussianas de contraste absoluto em `SiO2/Si` ficaram em **`(18 ± 1)%` para monocamada (`1L`)** e **`(26 ± 2)%` para bicamada (`2L`)**, **sem sobreposição**. Pontos medidos em um **segundo MEV diferente** (`FEI Strata DB235` vs. `Carl Zeiss Supra`) caíram exatamente na mesma faixa.
  - **Regime de camadas, IMFP e saturação (Fig. 3a):** até **10 camadas** puderam ser identificadas distintamente; entre `4` e `12` camadas o contraste varia **linearmente** por efeito de atenuação, fornecendo **`lambda ≈ 5,7 ± 0,1 nm`** (próximo ao modelo de Seah & Dench); a redução desacelera acima de 12 camadas e satura próximo a `14` camadas, convergindo para **`~ -0,60 ± 0,01`** em grafite espesso (`N > 100`).
  - **Extração de função trabalho (`1L` a `4L`, Figs. 3–4):** utilizando `Phi(4) = 4,60 ± 0,07 eV` e índice espectral experimental `n = 4,6` (SEM) / `n = 5,3` (HIM), a monocamada apresentou **`Phi(1) = 4,26 ± 0,05 eV`** (em MEV) e **`4,35 ± 0,02 eV`** a `4,56 ± 0,03 eV` (`1L` a `4L` em HIM), concordando com os **`4,33 eV`** ajustados diretamente no espectro SE de `1L` suspenso (pico em `1,5 eV`) e com a síntese espectral do grafeno suportado (`Fig. 4b`). A precisão relativa declarada entre camadas sucessivas é **`< 10 meV`** (resumo) e o erro absoluto `< 0,05 eV`.

---

## 6. Limitações

- **[Reconhecidas pelos autores]:**
  - **Teto de sensibilidade à função trabalho (`N <= 4`):** como a função trabalho satura a partir de quatro camadas (`N >= 4`), o método de extração de `Phi` aplica-se apenas a `1L–4L`; para `N >= 4`, a variação de contraste decorre essencialmente da atenuação de SEs (e acima de `~10–14` camadas o contraste também satura).
  - **Sensibilidade ao carregamento elétrico:** em `SiO2/Si` abaixo de `1 keV` no MEV, e em qualquer energia no HIM sem ajuste fino do *flood gun* (tempo de inundação), o carregamento suprime o sinal SE e quebra o ajuste teórico da Eq. (1).
  - **Sensibilidade multifatorial:** os autores explicitam no texto introdutório que o contraste SE é afetado por parâmetros de feixe, **contaminação induzida pelo feixe**, potencial elétrico da amostra e eficiência de coleta do detector — exigindo manutenção rigorosa de baixa corrente (`5–20 pA`), abertura pequena (`10 µm`) e geometria fixa (`WD = 4 mm`, InLens).
- **[Críticas adicionais — Agente C]:**
  - **Dependência de calibração externa de `Phi(4)` e detector InLens específico:** a Eq. (4) não fornece `Phi(1)` absolutamente sem ancoragem em `Phi(4)` e na inclinação `C_gi(N)` de `4–8` camadas; ademais, todo o protocolo foi validado com detectores *InLens* a `WD = 4 mm` (que filtram BSEs e SE3 de câmara), não valendo diretamente para detectores E-T convencionais ou `WD` diferentes.
  - **Amostras ideais:** o estudo testou flocos esfoliados limpos em laboratório sobre `SiO2 (285 nm)/p-Si` (e `Au/Cu/Ni` para `1L`), não avaliando dispersões industriais de nanoplaquetas (GNPs) com resíduos de solvente/surfactante ou óxido de grafeno (GO) isolante e funcionalizado, onde contaminação e carregamento alteram `Phi` e `delta`.
  - **Nota de rigor editorial:** a definição impressa na p. 2 (`C_g = (I_g/I_g - 1)*100%`) contém erro tipográfico óbvio (`I_g/I_s - 1`), e as derivações completas constam no Material Suplementar (S1–S10) não disponível no arquivo principal extraído.

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Este trabalho é a **pedra angular física** para o módulo de caracterização por MEV na dissertação:
  1. Explica rigorosamente os dois mecanismos físicos acoplados que governam a intensidade de pixels em micrografias MEV de grafeno: **emissão/função trabalho superficial** (`N <= 4`) + **atenuação exponencial dos SEs do substrato** (`lambda ≈ 5,7 nm`, visível até `~10–14L`).
  2. Prova quantitativamente por que um software de análise de imagens MEV **não pode assumir contraste universal fixo**: a `1,5 keV` no InLens uma monocamada quase desaparece (`+1%`), a `0,5 keV` fica mais brilhante (`+9%`) e a `5 keV` fica mais escura (`-18 ± 1%`) — exatamente o oposto do comportamento a `1,0 kV` em detector externo descrito por Hiura et al. (2010).
  3. Ao mesmo tempo, demonstra que **quando o protocolo instrumental é padronizado** (`5 keV`, InLens, `WD 4 mm`, baixa dose), a separação entre `1L` (`-18±1%`) e `2L` (`-26±2%`) é robusta o bastante para permitir segmentação automatizada com resolução de borda `~10 nm` (68× mais fina que OM).

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Caso o laboratório do PPGCEM disponha de MEV FEG com detector InLens e amostras controladas em `SiO2/Si`, o pipeline computacional pode incorporar um modo **calibrado por usuário** (inserção da intensidade média do substrato `I_s` e de curvas de referência locais para `5 keV` / `WD = 4 mm`) para mapear estatisticamente fração de recobrimento relativa por nível de contraste em `1L`, `2L` e poucas camadas.
  - Em pipelines de segmentação por visão computacional, usar a diferença física entre **contraste de borda** (que persiste em `~7%` mesmo a `1,5 keV` quando o interior da folha zera!) e **contraste de área** ajuda a selecionar detectores de borda/segmentação resistentes à perda local de contraste interno.

---

## 9. Evidências

- **Fig. 1 (p. 2):** comparação OM vs. SEM vs. HIM sobre `Au` (1a); variação do contraste em `SiO2/Si` a `0,5; 1,5; 5; 20 keV` (1b); ajuste teórico da Eq. (1) sobre `SiO2/Si` e `Au` (1c); efeito do *flood time* em HIM atingindo `~54%` (1d).
- **Fig. 2 (p. 4):** imagens `5 keV` SEM e `30 keV` HIM com `1L–10L` (2a–b); perfis de linha `1–4L` (2c); resolução de borda `~10 nm` vs. `~680 nm` OM (2d); distribuição gaussiana inter-flocos (`18±1%` vs. `26±2%`) e validação em segundo MEV (2e).
- **Fig. 3 (p. 5):** curva `C_g(N)` de `1` a `14` camadas + saturação em grafite (`~-0,60`) + ajuste linear `4–8L` (`lambda ≈ 5,7 nm`) e mapa de função trabalho `Phi(1)=4,26 eV` a `Phi(4)=4,60 eV`.
- **Fig. 4 (p. 6):** espectros SE experimentais (grafeno suspenso e suportado em `SiO2/Si`), ajuste Chung & Everhart (`n = 4,6`) e diagrama de bandas.
- **Methods (p. 7):** especificações exatas de preparação, vácuo, dose, abertura, corrente, `WD`, pixelagem e filtro energético.

---

## 10. Prioridade de estudo

- **Prioridade:** **ALTA (Leitura obrigatória para 17/11/2026).**
- **Justificativa:** Fornece a formulação físico-matemática completa e validada experimentalmente em dois MEVs distintos para explicar contraste SE, dependência de energia primária, carregamento em `SiO2/Si`, papel da função trabalho, atenuação exponencial com IMFP e superioridade de resolução lateral (`~10 nm`) sobre OM — respondendo diretamente a possíveis arguições de banca de física/materiais sobre o que o MEV realmente mede.
