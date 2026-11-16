# Fichamento 02 — Hiura, Miyazaki & Tsukagoshi (2010): Distribuição Discreta da Intensidade de Elétrons Secundários para Contagem de Camadas de Grafeno

> **Status de Leitura e Verificação:** **Texto completo lido** via versão *Green Open Access* depositada pelos autores no arXiv ([`arXiv:1008.2039v2`](https://arxiv.org/abs/1008.2039), 15 páginas incluindo 4 figuras), correspondente ao manuscrito do artigo publicado em *Applied Physics Express* 3 (2010) 095101 (3 páginas no formato impresso). *Nota bibliográfica:* o título da versão publicada traz *"Stemming from Individual Graphene Layers"*, enquanto o preprint `arXiv:1008.2039v2` traz *"Derived from Individual Graphene Layers"*.

---

## 1. Identificação bibliográfica

- **Título (versão publicada):** Determination of the Number of Graphene Layers: Discrete Distribution of the Secondary Electron Intensity Stemming from Individual Graphene Layers
- **Título (preprint arXiv v2):** Determination of the Number of Graphene Layers: Discrete Distribution of the Secondary Electron Intensity Derived from Individual Graphene Layers
- **Autores:** Hidefumi Hiura, Hisao Miyazaki, Kazuhito Tsukagoshi
- **Ano:** 2010 (publicado em 27 de agosto de 2010; arXiv v1 em 12 ago 2010, v2 em 28 set 2010)
- **Periódico:** *Applied Physics Express* (The Japan Society of Applied Physics), Vol. 3, No. 9, `095101`
- **DOI:** `10.1143/APEX.3.095101` (DOI arXiv: `10.48550/arXiv.1008.2039`)
- **Links oficiais:** [https://doi.org/10.1143/APEX.3.095101](https://doi.org/10.1143/APEX.3.095101) | [https://arxiv.org/abs/1008.2039](https://arxiv.org/abs/1008.2039) | [https://arxiv.org/pdf/1008.2039](https://arxiv.org/pdf/1008.2039)
- **Métricas catalogadas:** 100 citações em `_scratch/verified_catalog.json`.

---

## 2. Problema investigado

- **[Extraído do artigo]:** A determinação experimental do número de camadas (`L`) de flocos de grafeno é essencial para a fabricação de nanodispositivos eletrônicos, pois a estrutura de bandas e o transporte de portadores variam fortemente entre monocamada (`1L`), bicamada (`2L`), tricamada (`3L`) e multicamadas. Os métodos então usuais — microscopia óptica (OM) e espectroscopia Raman — sofriam limitações severas para nanodispositivos: ambos são restringidos pelo limite de difração da luz (impraticáveis para áreas submicrométricas `< 1 µm²`), a OM de refletância só fornece bom contraste em substratos de `Si` com espessura específica de `SiO2` (`~100 nm` ou `~300 nm`), e o laser Raman pode induzir degradação estrutural. O MEV era utilizado apenas como ferramenta auxiliar porque ainda não havia um método quantitativo estabelecido para relacionar de modo inequívoco o contraste em MEV ao número de camadas sobre múltiplos substratos isolantes espessos.

---

## 3. Fundamentação

- **[Extraído do artigo]:**
  - **Definição de contraste relativo em MEV:** os autores definem o contraste `C` como `C = (I - I_0) / I_0`, em que `I` é a intensidade de elétrons secundários (SE) medida sobre o grafeno e `I_0` é a intensidade SE sobre o substrato nu adjacente (a mesma fórmula é aplicada comparativamente à luz refletida ou transmitida na OM).
  - **Rendimento de SE em função da tensão de aceleração (`V_acc`) e atenuação por camadas:** para `SiO2` com `V_acc > 0,5 kV`, o rendimento de SE do substrato decresce monotonicamente com `V_acc` (citando Yong et al., 1998). A curva de contraste do grafeno sobre `SiO2/Si`, safira e mica exibe um pico positivo em torno de `1,0 kV` e um platô negativo entre `3,0` e `20,0 kV`, o que os autores atribuem a características intrínsecas de emissão SE do grafeno somadas à atenuação proporcional dos elétrons secundários que atravessam `L` camadas de grafeno.
  - **Função trabalho vs. atenuação:** os autores discutem explicitamente o papel da função trabalho (citando Hibino et al., *Phys. Rev. B* 79, 2009: função trabalho cresce linearmente de `~4,3 eV` em `1L` a `~4,6 eV` em `4L`, saturando para `L >= 4`), argumentando que a variação da função trabalho **sozinha não explica** a relação linear observada até `L = 8` — logo, a atenuação de SE ao atravessar cada camada atômica domina para espessuras maiores, enquanto a anomalia observada especificamente em `1L` (desvio da reta) é sugerida como efeito de a monocamada simultaneamente receber excitação do substrato e emitir diretamente para o vácuo sem subcamadas de grafeno.
- **[Análise crítica — Agente C]:** Este é um trabalho pioneiro e histórico (2010), anterior ao modelo analítico completo de Zhou et al. (2016). Nota-se que, em `2010`, os autores usaram um MEV convencional de filamento com detector externo e **não modelaram quantitativamente** o coeficiente de retroespalhamento (`eta_s`), o livre caminho médio inelástico (`lambda`) nem a influência de carregamento elétrico positivo/negativo em `0,5–1,5 kV` sobre isolantes espessos como safira e mica — aspectos posteriormente refinados na literatura.

---

## 4. Metodologia

- **[Extraído do artigo]:**
  - **Preparação de amostras:** esfoliação mecânica (*glue tape method*) de grafite natural depositado sobre três substratos isolantes espessos distintos:
    1. Silício com `300 nm` de `SiO2` térmico (`SiO2/Si`);
    2. Safira (*sapphire*);
    3. Mica.
  - **Referência independente de camadas (ground truth):** contagem prévia de camadas determinada por microscopia óptica via **refletância** (no caso de `SiO2/Si`) e **transmitância** (nos casos de safira e mica), calibrando os passos de contraste óptico (`-5,29%`, `-2,26%` e `-2,29%` por camada, respectivamente).
  - **Aquisição em MEV:** microscópio padrão `KEYENCE VE-9800` em vácuo, equipado com **detector externo** (*outer detector*) operando com tensão de coleta/aceleração dos SE de `10 keV`. Varredura sistemática da tensão de aceleração do feixe primário `V_acc` em `0,5; 0,8; 1,0; 1,4; 2,0; 3,0; 5,0; 10,0` e `20,0 kV` (Figs. 1 e 3).
  - **Processamento de imagem e método prático de contagem:** captura de imagens MEV a `V_acc = 1,0 kV` (condição ótima), conversão da área selecionada em **histograma de contraste** (frequência vs. `C`), identificação do pico de substrato (`C = 0`) e dos picos discretos correspondentes às camadas, e conversão do eixo de contraste em número de camadas dividindo `C` pela diferença de contraste por camada previamente calibrada (coeficiente angular da reta para cada substrato e `V_acc`).

---

## 5. Resultados

- **[Extraído do artigo]:**
  - **Inversão de contraste dependente de `V_acc` (Figs. 1 e 2):**
    - Em `V_acc = 0,5` a `2,0 kV`, poucas camadas de grafeno aparecem **mais claras** (`C > 0`) que o substrato `SiO2/Si`, atingindo pico de contraste próximo a `1,0 kV` (análogo ao comportamento de nanotubos de carbono de parede única em `SiO2`, pico em `1–2 kV`).
    - Para `V_acc >= 3,0 kV`, todas as camadas tornam-se **mais escuras** (`C < 0`) que o `SiO2`, formando um platô entre `3,0` e `20,0 kV`. Em `V_acc = 20,0 kV`, o contraste entre camadas torna-se indistinguível na imagem (Fig. 1h).
  - **Linearidade discreta e desvio em `1L` (Fig. 3):** para qualquer `V_acc` avaliada (`0,5`, `1,0`, `1,5`, `3,0`, `10 kV`), o contraste SE decresce **linearmente** com o aumento de `L` (de `2L` até `8L`) em `SiO2/Si`, bem como em safira e mica a `1,0 kV` — **com exceção consistente de `L = 1`**, cujo ponto se situa acima da reta ajustada em todos os substratos e tensões testadas.
  - **Condição ótima e taxas de contraste por camada a `V_acc = 1,0 kV` (Fig. 4):** a faixa `0,5–1,5 kV` (ótimo em **`1,0 kV`**) maximiza a inclinação da curva de calibração e a facilidade de detecção visual. As diferenças de contraste por camada medidas a `1,0 kV` foram:
    - `SiO2/Si`: **`-5,05%` por camada** (vs. `-5,29%` na OM de reflexão);
    - Mica: **`-2,65%` por camada** (vs. `-2,26%` na OM de transmissão);
    - Safira: **`-6,11%` por camada** (vs. `-2,29%` na OM de transmissão).
  - **Validação comparativa por histogramas discretos (Fig. 4):** os histogramas de contraste MEV a `1,0 kV` produziram picos discretos bem resolvidos correspondentes exatamente às mesmas distribuições de camadas identificadas por OM: `1L, 3L, 5L` (`SiO2/Si`); `1L, 2L, 4L, 8L` (mica); e `2L, 4L, 9L` (safira), demonstrando capacidade de caracterizar regiões `< 1 µm²` em múltiplos substratos isolantes de forma não destrutiva a `~1 kV`.

---

## 6. Limitações

- **[Reconhecidas pelos autores]:**
  - **Desvio sistemático da monocamada (`L = 1`):** `1L` desvia consistentemente da linha reta em todos os substratos e tensões; sua origem física exata não foi fechada no artigo ("The origin of this peculiarity is unclear").
  - **Necessidade de calibração específica:** a inclinação da reta de contraste depende fortemente de `V_acc`, do tipo de substrato e das condições instrumentais, exigindo sempre o levantamento prévio de uma curva de calibração em amostra-padrão nas mesmas condições antes de determinar camadas de amostras desconhecidas.
- **[Críticas adicionais — Agente C]:**
  - **Inversão de dependência de sinal em detectores modernos e alta tensão:** enquanto Hiura et al. (detector externo Keyence `VE-9800` a `10 keV` de aceleração no coletor) observaram inversão de claro (`<= 2 kV`) para escuro (`>= 3 kV`) e contraste nulo a `20 kV`, estudos posteriores com detectores *InLens* (como `Zhou et al., 2016`) obtiveram contraste negativo máximo em `5 kV` e contraste positivo/nulo em `0,5 / 1,5 kV` — provando que as curvas de calibração de Hiura **não são transferíveis diretamente** entre diferentes geometrias de detector e colunas MEV.
  - **Ausência de controle/relato sobre carregamento dinâmico e contaminação carbonácea:** em substratos isolantes espessos (safira, mica, `SiO2 300 nm`), a baixa `V_acc = 1,0 kV` situa-se próxima ao ponto de cruzamento E2 de carregamento (como depois apontado por `Zhou et al., 2016` para `< 1 keV`). Além disso, não há relato da corrente de feixe, dose eletrônica (`e-/cm²`), tempo de exposição nem da degradação do contraste por deposição de carbono amorfo durante varreduras repetidas.
  - **Omissão da propagação da anomalia `1L` no algoritmo de histograma:** o método prático descrito no texto divide o contraste diretamente pelo passo constante da inclinação (`contrast difference per layer`), o que introduziria erro na atribuição de `1L` caso o desvio não linear de `1L` (visível como *offset* na Fig. 3/4) não seja tratado explicitamente.

---

## 7. Contribuição para a dissertação

- **[Análise — Agente C]:** Este artigo fundamenta dois argumentos centrais da dissertação:
  1. **Origem da técnica de histograma de intensidades em MEV:** mostra exatamente como um pipeline computacional simples (extração de histograma de tons de cinza normalizados pelo substrato `I_0`) pode separar domínios discretos em flocos esfoliados quando a aquisição é estritamente controlada em baixa tensão (`~1 kV`), além de explicar por que o MEV supera a OM para domínios `< 1 µm²`.
  2. **Prova experimental de não universalidade:** fornece evidência quantitativa primária de que (a) um mesmo floco muda drasticamente de intensidade (e até inverte polaridade claro/escuro) com `V_acc`, (b) substratos diferentes mudam o passo por camada em mais de 2× (`-2,65%` em mica vs. `-6,11%` em safira) e (c) `1L` viola a linearidade. Isso impede que a ferramenta proposta tente "adivinhar número de camadas" a partir de uma única micrografia MEV sem curva de calibração ou confirmação por AFM/Raman.

---

## 8. Possíveis aplicações

- **[Proposições — Agente C]:**
  - Implementar na ferramenta computacional um módulo de **análise de histograma normalizado ao substrato** (`C = (I - I_0)/I_0`) com detecção automática de picos multimodais para mapear **regiões de contraste discreto relativo** (útil para segmentar dobras, degraus e sobreposições dentro de um mesmo campo de visão de `1–5 kV`), rotulando os domínios como *"níveis relativos de contraste"* e exigindo calibração do usuário ou entrada correlativa de AFM/Raman antes de convertê-los em "número absoluto de camadas".

---

## 9. Evidências

- **Fig. 1 (arXiv pp. 11, 13):** série de imagens MEV no mesmo floco em `SiO2/Si` (`L = 1, 3, 4, 5, 6, 7, 8` e grafite `>> 10L`) de `V_acc = 0,5` a `20,0 kV` comparada à imagem óptica (1i).
- **Fig. 2 (arXiv pp. 11, 14):** curvas de contraste MEV vs. `V_acc` (`0,5–20 kV`) para `1L, 2L, 4L, 6L, 8L` e grafite.
- **Fig. 3 e Inset (arXiv pp. 5–6, 11, 15):** linearidade negativa do contraste vs. número de camadas (`0,5–10 kV`) e comparação entre `SiO2/Si`, mica e safira a `1,0 kV`, destacando o desvio sistemático de `1L`.
- **Fig. 4 (arXiv pp. 6–7, 11, 16):** comparação quantitativa OM vs. MEV a `1,0 kV` e respectivos histogramas de contraste com inclinações `-5,05%`, `-2,65%` e `-6,11%` por camada.

---

## 10. Prioridade de estudo

- **Prioridade:** **ALTA.**
- **Justificativa:** Artigo clássico seminal (apenas ~8 páginas de texto limpo e 4 figuras diretas no preprint arXiv), leitura rápida (~30–40 minutos) e indispensável para dominar na arguição da apresentação (17/11/2026) por que a tensão de aceleração (`0,5–5 kV`) controla o contraste e a inversão claro/escuro do grafeno no MEV, e quais os limites metodológicos para inferência de número de camadas.
