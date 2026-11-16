# Fichamento 03 — Castro Neto et al. (2009), *Reviews of Modern Physics*

> **Distinção metodológica:** Equações, parâmetros cristalográficos, modelos teóricos e classificações de empilhamento e defeitos descritos nas Seções 1 a 5 e 9 são **fatos extraídos** do artigo. A seleção dos tópicos pertinentes ao problema de caracterização e o diagnóstico crítico de limites integram a **análise crítica do Agente A**.

---

## 1. Identificação Bibliográfica

- **Título:** The electronic properties of graphene
- **Autores:** A. H. Castro Neto, F. Guinea, N. M. R. Peres, K. S. Novoselov, A. K. Geim
- **Ano:** 2009 (14 de janeiro de 2009)
- **Periódico:** *Reviews of Modern Physics*, v. 81, n. 1, p. 109–162
- **DOI:** `10.1103/RevModPhys.81.109`
- **URL oficial:** https://doi.org/10.1103/RevModPhys.81.109 (versão Bronze OA APS: http://link.aps.org/pdf/10.1103/RevModPhys.81.109; OpenAlex: https://openalex.org/W2105685140)
- **Status de leitura:** Seções relevantes do texto completo lidas em [`Castro_Neto_2009_Electronic_Properties_of_Graphene.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Castro_Neto_2009_Electronic_Properties_of_Graphene.md) (foco nas Seções I, II.A–C, II.E–H, III, IV e VI, evitando formalismos avançados de muitos corpos irrelevantes para a caracterização experimental).

---

## 2. Problema Investigado

*(Fatos extraídos do artigo)*  
Os autores realizam um tratado teórico abrangente sobre como a geometria cristalina bidimensional em favo de mel do grafeno, o acoplamento entre camadas empilhadas, as terminações de borda, as deformações elásticas (*ripples*) e diferentes classes de desordem estrutural e química determinam sua estrutura de bandas eletrônicas, excitando férmions de Dirac e alterando drasticamente o transporte e as assinaturas espectroscópicas do material.

---

## 3. Fundamentação

*(Fatos extraídos do artigo — foco estrutural e cristalográfico)*  
- **Rede cristalina e rede recíproca (Seção II.A, Eq. 1–4, Fig. 2):** a rede em favo de mel do grafeno **não é uma rede de Bravais**, mas uma rede triangular (hexagonal) com **base de dois átomos inequivalentes ($A$ e $B$) por célula unitária**. A distância carbono–carbono na hibridização $sp^2$ é $a \approx 1{,}42\ \text{\AA}$ (parâmetro de rede no plano $a_0 = \sqrt{3}\,a \approx 2{,}46\ \text{\AA}$). Os vetores da rede direta são $\mathbf{a}_1 = \frac{a}{2}(3,\sqrt{3})$ e $\mathbf{a}_2 = \frac{a}{2}(3,-\sqrt{3})$, gerando a rede recíproca com vetores $\mathbf{b}_1 = \frac{2\pi}{3a}(1,\sqrt{3})$ e $\mathbf{b}_2 = \frac{2\pi}{3a}(1,-\sqrt{3})$ e área de célula unitária $A_c = 3\sqrt{3}a^2/2$.
- **Estrutura eletrônica $\sigma$/$\pi$ e pontos de Dirac (Seção I e II.A–B, Eq. 5–23, Fig. 3–5):** ligações $\sigma$ planares respondem pela robustez mecânica excepcional, enquanto orbitais $p_z$ perpendiculares formam bandas $\pi$ e $\pi^*$ semipreenchidas. No modelo *tight-binding* com *hopping* aos primeiros vizinhos $t \approx 2{,}8\ \text{eV}$ ($\gamma_0 = 3{,}16\ \text{eV}$ na Tabela I do modelo SWM do grafite) e segundos vizinhos $t' \approx 0{,}1\text{–}0{,}2t$, as bandas $\pi$ e $\pi^*$ tocam-se nos cantos $\mathbf{K}$ e $\mathbf{K}'$ da Zona de Brillouin, produzindo dispersão cônica linear $E_{\pm}(\mathbf{q}) \approx \pm v_F |\mathbf{q}|$ com $v_F = 3ta/2 \approx 10^6\ \text{m/s}$, densidade de estados linear $\rho(E) = 2A_c|E|/(\pi v_F^2)$ nula no ponto de Dirac e massa ciclotrônica $m^* \propto \sqrt{n}$.
- **Ordens de empilhamento e grafeno multicamada (Seção II.C e II.E, Fig. 9, 12 e 13, Tabela I):**
  - Distância interplanar mínima entre camadas adjacentes: $c = 3{,}4\ \text{\AA}$ (no texto de II.E e III; acoplamento interplanar $\gamma_1 = t_\perp \approx 0{,}39\text{–}0{,}4\ \text{eV}$, $\gamma_3 \approx 0{,}315\ \text{eV}$).
  - **Empilhamento Bernal (`1212...` / ABAB):** forma mais comum no grafite; gera $N/2$ sub-bandas parabólicas para $N$ par (como na bicamada) e adiciona uma sub-banda linear tipo Dirac para $N$ ímpar (como na tricamada Bernal).
  - **Empilhamento romboédrico (`123123...` / ABC):** observado em certas regiões de grafite; gera dispersão $\propto k^N$ com estados de superfície nas camadas extremas.
  - **Grafite/empilhamento turboestrático (sem ordem de empilhamento discernível)** e **camadas rotacionadas (Moiré):** pequenas rotações relativas desacoplam efetivamente as camadas e **restauram o espectro linear tipo monocamada** (Lopes dos Santos et al., 2007), um resultado crítico para interpretar espectros de amostras crescidas ou reempilhadas.

---

## 4. Metodologia

*(Fatos extraídos do artigo)*  
Revisão teórica analítica e computacional baseada em formalismo *tight-binding* (Hamiltoniano Slonczewski–Weiss–McClure, SWM, estendido a pilhas finitas), aproximação contínua pela equação de Dirac 2D, teoria de elasticidade de membranas acopladas a fônons flexurais, teoria de campos de calibre (*gauge fields*) induzidos por curvatura/deformação e análise de espalhamento por defeitos pontuais, bordas e impurezas carregadas, confrontados com dados experimentais de STM/STS, ARPES, TEM/STEM (Fig. 24), MEV (Fig. 30) e magnetotransporte.

---

## 5. Resultados

*(Fatos extraídos do artigo pertinentes à caracterização estrutural e defeitos)*  
1. **Flexuralidade, ondulações (*ripples*) e acoplamento com substrato (Seção III e IV.A, Eq. 125–155, Fig. 24–25):** fônons flexurais fora do plano possuem dispersão quadrática $\omega_{\text{flex}}(k) \propto k^2$ e rigidez à flexão $\kappa = Yt^3 \approx 1\ \text{eV}$ ($Y \approx 10^{12}\ \text{N/m}$, $\rho \approx 2200\ \text{kg/m}^3$). Em folhas livres a $300\ \text{K}$, o comprimento térmico $L_T \approx 1\ \text{\AA}$ induz instabilidade de enrugamento suprimida por efeitos anarmônicos ou tensão. Sobre substrato de perfil $s(\mathbf{r})$, a folha segue parcialmente o relevo até escalas elásticas características $\ell_t = (\gamma/v)^{1/2}$ e $\ell_c = (\kappa/v)^{1/4}$, explicando por que a **rugosidade do substrato se traduz diretamente em topografia e ondulações medidas por STM/AFM**.
2. **Taxonomia teórica de defeitos estruturais e químicos (Seção IV.B–F, Fig. 26–29, Tabela II):**
   - **Defeitos topológicos:** disclinações (pentágonos/heptágonos que introduzem curvatura intrínseca — como em fulerenos — e misturam os vales $K$ e $K'$), discordâncias (pares pentágono–heptágono) e defeitos de Stone–Wales (dois pares pentágono–heptágono).
   - **Defeitos pontuais e estendidos:** vacâncias e adátomos geram estados localizados/semilocalizados no meio do *gap* ($1/r$ em vacâncias) que elevam localmente a densidade de estados (observáveis por STS/STM, não por DRX ou MEV). Bordas *zigzag* sustentam estados localizados de energia zero em $1/3$ da zona de Brillouin; bordas *armchair* não os sustentam e misturam vales.
   - **Deformação elástica (*strain*) e campos pseudomagnéticos (Tabela II):** ondulações típicas ($h \approx 1\ \text{nm}$, $l \approx 10\text{–}20\ \text{nm}$) geram campos magnéticos efetivos de $\sim 0{,}06\ \text{T}$ (curvatura) até $\sim 6\ \text{T}$ (deformação elástica de ligação C–C).
   - **Desordem no eixo $c$ (Seção IV.H):** impurezas intercaladas ou rotações relativas entre camadas afetam diretamente o transporte interplanar e o acoplamento eletrônico.
3. **Lacunas declaradas pelos autores (Seção VI, p. 48):** destacam que centenas de artigos concentraram-se na monocamada ideal, enquanto a física experimental e teórica de **multicamadas** e de **grafeno quimicamente modificado** permanecia comparativamente pouco explorada, com grande potencial prático.

---

## 6. Limitações

*(Fatos extraídos do artigo)*  
- A revisão concentra-se na física eletrônica e teórica de grafeno de carbono puro, tratando apenas marginalmente derivados fortemente oxidados (GO/rGO) ou compósitos industriais.
- Vários parâmetros SWM ($\gamma_0, \dots, \gamma_5, \Delta$) em pilhas com número pequeno e finito de camadas ainda careciam de determinação experimental precisa à época da revisão.

*(Análise crítica — Agente A)*  
- **Abstração frente à metrologia de bancada:** por ser uma revisão teórica de física da matéria condensada, não oferece protocolos práticos de aquisição nem métricas estatísticas de flocos em dispersão (como polidispersidade de tamanho lateral e espessura em amostras reais de laboratório).
- **Risco de má interpretação em DRX:** o reconhecimento teórico de empilhamentos **Bernal, romboédrico e turboestrático / rotacionado** explica por que técnicas de difração ou espectroscopia podem confundir multicamadas desordenadas com monocamadas se interpretadas ingenuamente, reforçando a necessidade de modelos físicos específicos em DRX (como Li et al., 2007).

---

## 7. Contribuição para a Dissertação

*(Análise crítica — Agente A)*  
1. Fornece toda a **base cristalográfica rigorosa** (rede triangular com base diatômica $A/B$, $a = 1{,}42\ \text{\AA}$, $a_0 = 2{,}46\ \text{\AA}$, distância interplanar $c \approx 3{,}4\ \text{\AA}$, espaço recíproco $\mathbf{b}_1, \mathbf{b}_2$, pontos $K/K'$) necessária para fundamentar tanto a física do grafeno quanto as reflexões $(hk0)$ e $(00l)$ em DRX e difração de elétrons no Seminário I.
2. Explica fisicamente **como defeitos e substratos alteram a topografia e as propriedades medidas**: a Eq. (152) demonstra que o relevo do substrato $s(\mathbf{r})$ acopla-se elasticamente à altura da folha $h(\mathbf{r})$, ajudando a compreender artefatos topográficos em AFM; já a presença de defeitos topológicos, vacâncias, bordas *zigzag*/*armchair* e desordem ao longo do eixo $c$ elucida o vínculo processamento–estrutura–propriedades exigido pelo PPGCEM/UFCA.
3. Fundamenta a distinção crítica entre empilhamento **Bernal ABAB**, **romboédrico ABC** e **turboestrático**, indispensável para evitar conclusões falsas ao analisar picos alargados ou ausentes em difratogramas de amostras esfoliadas.

---

## 8. Possíveis Aplicações

*(Análise crítica — Agente A)*  
- **Base conceitual direta:** incorporar na fundamentação da dissertação um diagrama comparativo conectando a **rede real/recíproca** (Castro Neto et al., 2009) às grandezas acessíveis por **DRX** (periodicidade interplanar $d_{002} \approx 3{,}35\text{–}3{,}4\ \text{\AA}$, domínios coerentes $L_c, L_a$), **MEV** (morfologia de bordas e flocos na escala $\mu\text{m}$) e **AFM** (topografia $h(\mathbf{r})$, rugosidade e degraus).
- **Hipótese de trabalho (a validar, não fato publicado):** ao caracterizar amostras esfoliadas eletroquimicamente por AFM, separar descritores de rugosidade induzida pelo substrato ($\ell_t, \ell_c$) da rugosidade intrínseca ou residual de oxidação/dobras.

---

## 9. Evidências

- **Declaração de leitura:** **Análise realizada a partir do texto completo** (seções estruturais e de desordem lidas diretamente em [`Castro_Neto_2009_Electronic_Properties_of_Graphene.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Castro_Neto_2009_Electronic_Properties_of_Graphene.md), 334 linhas / 55 páginas na edição *Rev. Mod. Phys.* 81, 109–162).
- **Evidências localizadas:**
  - **Seção I e II.A (linhas 4–36, pp. 2–6):** geometria em favo de mel, $a \approx 1{,}42\ \text{\AA}$, vetores $\mathbf{a}_1, \mathbf{a}_2$ (Eq. 1), $\mathbf{b}_1, \mathbf{b}_2$ (Eq. 2), pontos $\mathbf{K}, \mathbf{K}'$ (Eq. 3), dispersão linear (Eq. 7) e Fig. 2–5.
  - **Seção II.C e II.E (linhas 61–95, pp. 10–14):** Hamiltoniano da bicamada (Eq. 37–42), empilhamentos Bernal (`1212`), romboédrico (`123123`) e turboestrático, distância interplanar $c = 3{,}4\ \text{\AA}$, Tabela I (parâmetros SWM) e desacoplamento em camadas rotacionadas (Fig. 12–13).
  - **Seção II.F–H (linhas 95–120, pp. 14–18):** estados de borda *zigzag* vs. *armchair* (Fig. 14–17).
  - **Seção III (linhas 175–186, pp. 24–26):** fônons flexurais $\omega_{\text{flex}} \propto k^2$, $\kappa \approx 1\ \text{eV}$ (Eq. 135), enrugamento térmico ($L_T \approx 1\ \text{\AA}$) e Fig. 24 (TEM/STEM de folha suspensa).
  - **Seção IV.A–H (linhas 186–236, pp. 26–36):** interação folha–substrato $h(k)$ (Eq. 151–155), defeitos topológicos (Fig. 26), vacâncias/impurezas (Fig. 27), campos de calibre por deformação/curvatura (Tabela II) e desordem no eixo $c$.
  - **Seção VI (linhas 296–301, pp. 47–48):** conclusões sobre lacunas abertas em multicamadas e grafeno quimicamente modificado.

---

## 10. Prioridade de Estudo

- **Prioridade:** **Alta** (com leitura seletiva das Seções I, II.A, II.E, III, IV.A–B e VI)
- **Justificativa:** Referência teórica definitiva sobre cristalografia, estrutura eletrônica, empilhamentos e defeitos do grafeno (25.204 citações no OpenAlex); fornece a base física para não confundir propriedades de monocamada com empilhamentos Bernal/turboestráticos em DRX e para interpretar topografia/ondulações em AFM.
