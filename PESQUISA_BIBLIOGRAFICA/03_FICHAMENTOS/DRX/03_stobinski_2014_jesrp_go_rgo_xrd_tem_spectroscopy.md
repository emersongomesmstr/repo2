# Fichamento 03 — Caracterização Multimodal de GO e rGO por DRX, TEM e Espectroscopias Eletrônicas, e Auditoria de Armadilhas Interpretativas (Stobiński et al., 2014; Manoj & Kunjomana, 2012; Siburian et al., 2018)

> **Status de Leitura e Verificação:**
> - **Stobiński et al. (2014):** **Metadados verificados, Highlights, Resumo completo, Introdução completa e trechos públicos das seções *Samples*, *Structural characterization by TEM and XRD* e *Conclusions* (ScienceDirect preview + repositório ASEP `hdl:11104/0239279`)** — artigo de acesso fechado (`oa_status: closed`).
> - **Manoj & Kunjomana (2012):** **Metadados verificados e Resumo completo (OpenAlex / ScienceDirect OA)**, além de trechos públicos indexados.
> - **Siburian et al. (2018):** **Texto completo lido integralmente** a partir da versão oficial *Diamond Open Access* (`Oriental Journal of Chemistry`, HTML e PDF integral `OJC_Vol34_No1_p_182-187.pdf`), submetido a auditoria crítica rigorosa de coerência física.

---

## 1. Identificação bibliográfica

### Referência Principal
- **Título:** Graphene oxide and reduced graphene oxide studied by the XRD, TEM and electron spectroscopy methods
- **Autores:** Leszek Stobiński, B. Lesiak, Artur Małolepszy, Marta Mazurkiewicz-Pawlicka, Bogusław Mierzwa, Josef Zemek, Petr Jiricek, Igor Bieloshapka
- **Ano:** 2014 (publicado online em 10 de julho de 2014; edição de agosto de 2014)
- **Periódico:** *Journal of Electron Spectroscopy and Related Phenomena* (Elsevier), Volume 195, Páginas 145–154
- **DOI:** `10.1016/j.elspec.2014.07.003`
- **URL oficial:** <https://doi.org/10.1016/j.elspec.2014.07.003> (ScienceDirect: <https://www.sciencedirect.com/science/article/abs/pii/S0368204814001510>; Repositório ASEP: <http://hdl.handle.net/11104/0239279>)
- **Citações verificadas (OpenAlex):** 1.946 (`W1976073956`)

### Referências Complementares Verificadas (via `openalex_cli.py` e texto OA)
1. **Manoj & Kunjomana (2012):**
   - **Título:** Study of Stacking Structure of Amorphous Carbon by X-Ray Diffraction Technique
   - **Autores:** B. Manoj, A. G. Kunjomana
   - **Ano:** 2012 (abril de 2012)
   - **Periódico:** *International Journal of Electrochemical Science*, Volume 7, Número 4, Páginas 3127–3134
   - **DOI:** `10.1016/s1452-3981(23)13940-x`
   - **URL oficial:** <https://doi.org/10.1016/s1452-3981(23)13940-x> (ScienceDirect Gold OA: <https://www.sciencedirect.com/science/article/pii/S145239812313940X>; índice oficial: <https://www.electrochemsci.org/list12.htm>)
   - **OpenAlex ID:** `W2398254313`
2. **Siburian et al. (2018):**
   - **Título:** New Route to Synthesize of Graphene Nano Sheets
   - **Autores:** Rikson Asman Fertiles Siburian (`R. Siburian`), Hengki Tamando Sihotang (`H. Sihotang`), Saur Lumban Raja (`S. Lumban Raja`), Minto Supeno (`M. Supeno`), Crystina Simanjuntak (`C. Simanjuntak`)
   - **Ano:** 2018
   - **Periódico:** *Oriental Journal of Chemistry*, Volume 34, Número 1, Páginas 182–187
   - **DOI:** `10.13005/ojc/340120`
   - **URL oficial:** <https://doi.org/10.13005/ojc/340120> (PDF *Diamond Open Access* integral lido: <http://www.orientjchem.org/pdf/vol34no1/OJC_Vol34_No1_p_182-187.pdf>)
   - **Citações verificadas (OpenAlex):** 514 (`W2787748576`)

---

## 2. Problema investigado

### Fatos extraídos dos artigos
- **Stobiński et al. (2014):** Óxido de grafeno (GO) e óxido de grafeno reduzido (rGO) contêm diversos grupos funcionais oxigenados (hidroxila, epóxi, carbonila, carboxila) e água adsorvida/intercalada que governam o empilhamento das camadas e suas propriedades eletrônicas (que se aproximam do grafite a partir de ~10 camadas). O problema investigado é como caracterizar de maneira consistente a morfologia, o **diâmetro lateral, a altura de empilhamento, o espaçamento interplanar e o número de camadas** dessas nanoestruturas combinando técnicas de volume (**DRX/XRD** e **TEM**) com espectroscopias eletrônicas sensíveis à superfície (**XPS** e **REELS** — profundidade de informação de poucos nanômetros).
- **Manoj & Kunjomana (2012):** Como quantificar a estrutura de empilhamento aleatório de lamelas grafênicas/aromáticas (aromaticidade $f_a$, átomos por lamela $n$, $L_a$, $L_c$, $d_{002}$ e número de camadas) em carbonos amorfos/desordenados (carvões) a partir de perfis de DRX.
- **Siburian et al. (2018):** Avaliar se a redução química de GO com amônia ($\text{NH}_3$) em vez de hidrazina tóxica permite obter "folhas de nanografeno" (*graphene nano sheets*) em escala de grama e verificar sua estrutura por DRX, FTIR e SEM-EDX.

### Análise crítica — Agente B
- Esse conjunto de três artigos permite confrontar diretamente: (i) uma caracterização **multimodal robusta e convergente** (Stobiński et al., 2014, cruzando XRD + TEM + XPS + REELS), (ii) um procedimento clássico de **deconvolução de empilhamento por DRX** em carbonos desordenados (Manoj & Kunjomana, 2012) e (iii) um caso real e amplamente citado (>500 citações) de **interpretação fisicamente contraditória de DRX** na literatura (Siburian et al., 2018), reforçando por que a validação cruzada entre técnicas é indispensável.

---

## 3. Fundamentação

### Fatos extraídos dos artigos
- **Stobiński et al. (2014):**
  - A oxidação úmida do grafite (Brodie, Staudenmaier, Hofmann, Hummers & Offeman) introduz grupos oxigenados (`-OH`, `C-O-C`, `C=O`, `-COOH`) no plano basal e nas bordas, além de moléculas de $\text{H}_2\text{O}$ ligadas fortemente por pontes de hidrogênio aos grupos oxigenados, expandindo o espaçamento interplanar.
  - A redução química (ex.: hidrazina) degrada grupos oxigenados, produz água adicional que pode levar à delaminação de camadas e reduz a distância interplanar à medida que oxigênio e água são removidos, restaurando parcialmente ligações $\text{C } sp^2$.
  - O DRX sonda dimensões médias em volume (altura/diâmetro de empilhamento e distância interplanar), enquanto XPS (`C 1s`, `O 1s`) e REELS (espectroscopia de perda de energia de elétrons por reflexão) sondam química superficial ($sp^2$ vs. $sp^3$) e número de camadas nos primeiros nanômetros.
- **Manoj & Kunjomana (2012):**
  - Baseia-se no modelo turboestrático de empilhamento aleatório de lamelas aromáticas (bandas $(002)$ e $(100)/(10)$ e banda $\gamma$ associada a estruturas saturadas alifáticas) e no cálculo de altura de empilhamento $L_c$, tamanho lateral $L_a$, espaçamento $d_{002}$ e número de camadas por lamela.
- **Siburian et al. (2018):**
  - Fundamenta a oxidação do grafite pelo aumento da distância interplanar devido à intercalação de grupos oxigenados e água, e a redução química pela remoção desses grupos (especialmente abertura do anel epóxi por $\text{NH}_3$) e restauração do sistema $\pi$ conjugado $sp^2$.

### Fundamentação física rigorosa de DRX em GO, rGO e grafeno — Agente B
- **Evolução canônica do pico `(002)` / `(001)` (para radiação $\text{Cu } K\alpha$, $\lambda = 0{,}15406\ \text{nm}$):**
  1. **Grafite precursor:** Reflexão basal `(002)` intensa e estreita em **$2\theta \approx 26{,}5^\circ$**, correspondendo a $d_{002} \approx 0{,}335\ \text{nm}$ pela Lei de Bragg ($n\lambda = 2d\sin\theta$).
  2. **Óxido de grafeno (GO):** A oxidação e intercalação de grupos funcionais ($-\text{OH}$, epóxi, $-\text{COOH}$) e $\text{H}_2\text{O}$ expandem fortemente os planos basais; a reflexão basal desloca-se para **$2\theta \approx 10^\circ\text{–}11^\circ$** (frequentemente indexada como `(001)` pela perda de empilhamento alternado `ABAB`, com $d \approx 0{,}75\text{–}0{,}90\ \text{nm}$ dependendo da umidade relativa e grau de oxidação).
  3. **Óxido de grafeno reduzido (rGO):** A remoção térmica ou química dos grupos oxigenados colapsa o espaçamento interplanar de volta para próximo do grafite, porém com elevada desordem turboestrática, rugas e poucos planos coerentes — resultando tipicamente em uma banda **muito larga e assimétrica centrada em $2\theta \approx 24^\circ\text{–}25^\circ$** ($d \approx 0{,}355\text{–}0{,}370\ \text{nm}$, podendo chegar a $\sim 0{,}4\ \text{nm}$ ou aproximar-se de $26{,}5^\circ$ quando ocorre reempilhamento intenso).
- **Por que a ausência (ou fraqueza) do pico `(002)` NÃO prova grafeno monocamada:**
  - Como princípio físico inegociável da difração, o pico `(002)` advém da interferência construtiva entre **múltiplos planos basais empilhados periodicamente ao longo do eixo $c$**. Logo, uma monocamada isolada de grafeno ($N=1$) realmente **não produz pico `(002)`**. Contudo, a **recíproca é falsa**: um difratograma sem pico `(002)` (ou com pico muito fraco) pode ocorrer mesmo na presença de flocos multicamadas por pelo menos cinco razões físicas:
    1. **Baixa massa difratante / filme ultrafino** abaixo do limite de detecção do difratômetro em geometria convencional $\theta\text{–}2\theta$;
    2. **Desordem turboestrática severa e flutuação de espaçamento interplanar** (conforme Li et al., 2007), que alargam o pico a ponto de confundi-lo com o ruído/linha de base amorfa;
    3. **Delaminação parcial ou esfoliação heterogênea** sem monocamadas puras (poucos planos coerentes com $d$ variável);
    4. **Orientação preferencial desfavorável** (ex.: folhas enrugadas, dobradas ou inclinadas cujo vetor de espalhamento não satisfaz a geometria Bragg-Brentano);
    5. **Espalhamento difuso** elevado do substrato (ex.: $\text{SiO}_2$/vidro) mascarando sinais fracos de carbono (elemento de baixo número atômico $Z=6$).
  - Portanto, a confirmação inequívoca de monocamada exige técnicas complementares: **espectroscopia Raman** (perfil lorentziano único e intenso da banda `2D` vs. `G`), **TEM de alta resolução / SAED** (contagem direta de franjas `(0002)` em bordas dobradas e razão de intensidade $\{1100\}/\{2110\}$) e **AFM** (perfil topográfico em degraus).
- **Erro físico inverso (exemplificado em Siburian et al., 2018):** Inferir grafeno monocamada a partir da *presença/reemergência* do pico `(002)` em $2\theta = 26{,}5^\circ$ é fisicamente autocontraditório, pois o pico `(002)` exige periodicidade de empilhamento multicamada ao longo de $c$.

---

## 4. Metodologia

### Fatos extraídos dos artigos
- **Stobiński et al. (2014):**
  - Investigação comparativa de amostras comerciais em poucas camadas (`FL-GOc` e `FL-RGOc`, GrapheneXpert, especificação do fabricante de $3\text{–}7$ camadas e $<3\ \text{nm}$ de espessura), grafite comercial (Acros Organics, 99,0%, 325 mesh) e amostras sintetizadas em laboratório de GO (método úmido/Hummers modificado) e rGO (redução com hidrazina).
  - Caracterização combinada em volume (**DRX** para distância interplanar, diâmetro $\times$ altura de empilhamento e número de camadas; **TEM** para morfologia lamelar e transparência eletrônica) e em superfície (**XPS** para razão C/O, fração $sp^3$ e especiação de grupos oxigenados; **REELS** como método complementar independente para estimar o número de camadas).
- **Manoj & Kunjomana (2012):**
  - Análise de perfis de DRX de amostras de carvão (72–77,4% de carbono) com extração dos parâmetros de empilhamento de lamelas aromáticas ($f_a$, $n$, $L_a$, $L_c$, $d_{002}$ e número de camadas).
- **Siburian et al. (2018) *(texto completo lido)*:**
  - Oxidação de $0{,}2\ \text{g}$ de pó de grafite com $0{,}2\ \text{g}\ \text{NaNO}_3$, $15\ \text{mL}\ \text{H}_2\text{SO}_4\ 96\%$ (2 h), $1\ \text{g}\ \text{KMnO}_4$ (24 h), seguidos de $\text{H}_2\text{SO}_4\ 5\%$ + $\text{H}_2\text{O}_2\ 30\%$, centrifugação a 3000 rpm por 20 min, redução do filtrado com $10\ \text{mL}$ de $\text{NH}_3\ 10\ \text{M}$ por 48 h e secagem a $80\ ^\circ\text{C}$ por 24 h.
  - Caracterização realizada apenas por **DRX**, **FTIR** (mencionado no resumo) e **SEM-EDX** ($15\ \text{kV}$), **sem TEM, AFM ou espectroscopia Raman**.

---

## 5. Resultados

### Fatos extraídos dos artigos
- **Stobiński et al. (2014) *(Highlights, Resumo e Conclusões na pré-visualização ScienceDirect)*:**
  - **`FL-GOc` comercial:** O DRX indica nanoestrutura empilhada de aproximadamente **$22 \times 6\ \text{nm}$** (diâmetro médio $\times$ altura), com separação interplanar de **$0{,}9\ \text{nm}$** entre **6–7 camadas** — em boa concordância com **8 camadas** estimadas por REELS.
  - **`FL-RGOc` comercial:** O DRX indica nanoestrutura empilhada reduzida para aproximadamente **$8 \times 1\ \text{nm}$** (diâmetro médio $\times$ altura), com separação interplanar de **$0{,}4\ \text{nm}$** entre **2–3 camadas** — consistente com **4 camadas** por REELS.
  - **GO e rGO sintetizados do grafite:** O método REELS indica **8–11 camadas** para o GO e **7–10 camadas** para o rGO.
  - **Química por XPS:** Todas as amostras de GO exibiram razão C/O de **$2{,}1\text{–}2{,}3$** e **$26{,}5\text{–}32{,}1\ \text{at\%}$ de ligações $\text{C } sp^3$**; após redução, a razão C/O elevou-se para **$2{,}8\text{–}10{,}3$**, o teor de $\text{C } sp^3$ caiu para **$11{,}4\text{–}20{,}3\ \text{at\%}$**, com diminuição de epóxi/carbonila e aumento relativo de hidroxila/carboxila.
  - **Morfologia TEM:** Folhas com áreas escuras (empilhamentos espessos) coexistindo com regiões de maior transparência (filmes mais finos).
- **Manoj & Kunjomana (2012) *(Resumo)*:**
  - Com o aumento do teor de carbono ($72\text{–}77{,}4\%$), aromaticidade e *rank*, $f_a$ e $L_c$ aumentam enquanto $d_{002}$ diminui.
  - O número de camadas variou de **7 a 8** e o número médio de átomos de carbono por lamela aromática foi de **16 a 21**, observando-se relação linear entre número de camadas e altura de empilhamento $L_c$.
- **Siburian et al. (2018) *(texto completo)*:**
  - **DRX:** Grafite com pico agudo em $2\theta = 26{,}5^\circ$ ($d = 3{,}36\ \text{Å}$) e pico em $23{,}88^\circ$ ($d = 3{,}72\ \text{Å}$); GO com pico largo em **$2\theta = 11{,}6^\circ$ ($d = 7{,}5\ \text{Å}$)** além de picos residuais em $20{,}1^\circ, 23{,}9^\circ$ e $26{,}4^\circ$; produto reduzido com $\text{NH}_3$ apresentando desaparecimento/achatamento do pico em $\sim 11^\circ$ e **reemergência do pico `(002)` mais largo e menos intenso em $2\theta = 26{,}5^\circ$ ($d = 3{,}35\ \text{Å}$)**.
  - **EDX:** Teor elementar de carbono passou de $88{,}374\%$ (grafite) e $88{,}114\%$ (GO) para $97{,}723\%$ (após $\text{NH}_3$), com oxigênio caindo de $11{,}886\%$ para $2{,}277\%$.

### Análise crítica — Agente B (sobre os resultados e sobre Siburian et al., 2018)
- Em **Stobiński et al. (2014)**, a convergência entre DRX ($6\text{–}7$ e $2\text{–}3$ camadas) e REELS ($8$ e $4$ camadas) ilustra a consistência possível quando se combinam sondas volumétricas e superficiais — embora haja pequena diferença sistemática (1 camada) esperada pelas diferentes profundidades de sondagem e hipóteses de cálculo.
- Em **Siburian et al. (2018)**, a leitura integral revelou **graves inconsistências científicas**:
  1. Na Seção *Results and Discussion* (pp. 183–184) e no *Abstract*, os autores escrevem acertadamente que o pico `C(002)` em $26{,}5^\circ$ ($d = 3{,}35\ \text{Å}$) representa *"typical structure of graphite and multiple layer of graphene"* e que *"NH3 has not been able to create a single layered graphene nano sheets structure"*. Contudo, na *Conclusion* (p. 186), afirmam de forma oposta: *"The graphene XRD pattern shows single-layered graphene due to the emergence of the diffraction peak at C (002)"* — uma contradição física frontal com a Lei de Bragg e com os próprios resultados do artigo.
  2. Além disso, o artigo não reporta comprimentos de onda/equipamento do DRX, não aplica Scherrer nem corrige $B_{\text{inst}}$, atribui picos EDX em $0{,}15\ \text{keV}$ e $0{,}25\ \text{keV}$ a C e O (enquanto a linha característica $K\alpha$ do carbono é $\sim 0{,}277\ \text{keV}$ e a do oxigênio é $\sim 0{,}525\ \text{keV}$), e não utiliza Raman, AFM ou TEM. Isso torna o artigo um **contraexemplo didático obrigatório** na revisão bibliográfica sobre os riscos de alegações infundadas em caracterização de grafeno por DRX.

---

## 6. Limitações

### Fatos extraídos dos textos e auditoria crítica — Agente B
- **Stobiński et al. (2014):**
  - *Lacuna documental desta revisão:* Por estar sob acesso fechado na Elsevier, não foi possível auditar as equações exatas utilizadas pelos autores para extrair $22 \times 6\ \text{nm}$ e $8 \times 1\ \text{nm}$ (presumivelmente Scherrer aplicado a `(10)`/`(100)` e `(002)`/`(001)`, mas sem verificação direta dos parâmetros $K$ e correção instrumental no corpo do texto), nem os difratogramas completos.
  - *Limitação física inerente:* O DRX relata médias de empilhamento ($6\text{–}7$ e $2\text{–}3$ camadas) em pó/aglomerados secos, onde ocorre reempilhamento parcial durante a secagem, não medindo a fração de monocamadas em dispersão.
- **Manoj & Kunjomana (2012):**
  - *Lacuna documental:* Apenas metadados e resumo inspecionados nesta passagem; ausência de detalhes de correção instrumental e separação de deformação sem leitura do PDF completo. Ademais, carvões minerais possuem fração amorfa alifática elevada (banda $\gamma$), distinta de grafeno esfoliado de alta cristalinidade.
- **Siburian et al. (2018):**
  - *Limitações metodológicas severas identificadas no texto completo:* Contradição interna entre Discussão e Conclusão sobre grafeno monocamada vs. multicamada; ausência total de Raman, AFM e TEM; ausência de análise quantitativa de largura de pico ou controle instrumental; inconsistências instrumentais na interpretação de EDX.

---

## 7. Contribuição para a dissertação

- **Análise — Agente B:**
  1. **Benchmark quantitativo de evolução DRX (Grafite $\to$ GO $\to$ rGO):** Fornece faixas experimentais concretas para validação de módulos de análise de difratogramas (`FL-GOc`: $d \approx 0{,}9\ \text{nm}$, $6\text{–}7$ camadas; `FL-RGOc`: $d \approx 0{,}4\ \text{nm}$, $2\text{–}3$ camadas; Siburian 2018: $2\theta_{\text{GO}} = 11{,}6^\circ$ / $7{,}5\ \text{Å}$ vs. $2\theta_{\text{grafite/rGO}} = 26{,}5^\circ$ / $3{,}35\text{–}3{,}36\ \text{Å}$), reforçando a necessidade de associar DRX a **TEM, XPS/Raman ou AFM**.
  2. **Evidência documental contra afirmações falaciosas em DRX:** A auditoria direta de Siburian et al. (2018) demonstra com um artigo de >500 citações que erros primários de interpretação do pico `(002)` existem na literatura publicada — justificando que uma ferramenta computacional bem projetada deve incorporar **regras de consistência física (*guardrails*)** que impeçam o usuário de concluir "monocamada" apenas pela presença ou ausência isolada do pico `(002)`.

---

## 8. Possíveis aplicações

- **Proposições — Agente B:**
  - Implementar na futura ferramenta um **módulo de diagnóstico multimodal assistido para carbonos lamelares**: ao detectar pico entre $2\theta \approx 9^\circ\text{–}13^\circ$ (Cu $K\alpha$), sinalizar possível fase GO expandida; entre $23^\circ\text{–}25{,}5^\circ$ (pico largo), sinalizar possível rGO ou carbono turboestrático; em $\sim 26{,}5^\circ$, sinalizar empilhamento grafítico/multicamada; e, **caso nenhum pico basal seja detectado**, emitir alerta obrigatório exigindo confirmação por **Raman (`2D`/`G`), AFM ou TEM** antes de qualquer atribuição de monocamada.
  - Utilizar modelos de deconvolução multi-pico (banda $\gamma \sim 19^\circ\text{–}20^\circ$ + banda `(002)` em $\sim 24^\circ\text{–}26{,}5^\circ$, inspirados em Manoj & Kunjomana, 2012) para separar frações amorfas e empilhamentos ordenados em amostras compósitas ou rGO parcialmente reduzido.

---

## 9. Evidências

- **Stobiński et al. (2014) (`10.1016/j.elspec.2014.07.003`):**
  - *Highlights*, *Abstract*, *Introduction* e *Conclusions* (ScienceDirect preview) + registro ASEP `hdl:11104/0239279`: valores verificados de `FL-GOc` ($22 \times 6\ \text{nm}$, $d = 0{,}9\ \text{nm}$, $6\text{–}7$ camadas XRD / $8$ camadas REELS), `FL-RGOc` ($8 \times 1\ \text{nm}$, $d = 0{,}4\ \text{nm}$, $2\text{–}3$ camadas XRD / $4$ camadas REELS), GO/rGO sintetizados ($8\text{–}11$ e $7\text{–}10$ camadas REELS) e teores XPS ($\text{C/O} = 2{,}1\text{–}2{,}3 \to 2{,}8\text{–}10{,}3$; $\text{C } sp^3 = 26{,}5\text{–}32{,}1\ \text{at\%} \to 11{,}4\text{–}20{,}3\ \text{at\%}$).
- **Manoj & Kunjomana (2012) (`10.1016/s1452-3981(23)13940-x`):**
  - *Abstract* e metadados verificados (OpenAlex `W2398254313` / ScienceDirect): $7\text{–}8$ camadas e $16\text{–}21$ átomos de C por lamela aromática para carvões com $72\text{–}77{,}4\%$ de carbono; tendência de redução de $d_{002}$ com aumento de $f_a$ e $L_c$.
- **Siburian et al. (2018) (`10.13005/ojc/340120`):**
  - **Texto completo** (`OJC_Vol34_No1_p_182-187.pdf`): Seção *Materials and Methods* (p. 183, síntese Hummers + $\text{NH}_3\ 10\ \text{M}$), Seção *Analysis of XRD* (pp. 183–184: $26{,}5^\circ$/$3{,}36\ \text{Å}$ e $23{,}88^\circ$/$3{,}72\ \text{Å}$ no grafite; $11{,}6^\circ$/$7{,}5\ \text{Å}$ no GO; $26{,}5^\circ$/$3{,}35\ \text{Å}$ no rGO-$\text{NH}_3$), Tabela 1 EDX (p. 186) e contradição literal na Seção *Conclusion* (p. 186).

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta para Stobiński et al. (2014) (recomenda-se recuperar o PDF completo via Portal CAPES/UFCA); Baixa/Didática para Siburian et al. (2018) e Média para Manoj & Kunjomana (2012).**
- **Justificativa:** Stobiński et al. (2014) constituem referência experimental rigorosa de caracterização combinada DRX + TEM + XPS/REELS de GO e rGO. Já Siburian et al. (2018) já foi lido integralmente e cumprirá melhor o papel de exemplo crítico de inconsistência física na análise de DRX, não devendo ser usado como modelo metodológico.
