# Fichamento 02 — Nemes-Incze et al. (2008): Anomalias na Medição de Espessura de Grafeno por Tapping Mode AFM

> **Nível de leitura declarado (Seção 7 do `PROMPT_MESTRE.md`):** **TEXTO COMPLETO LIDO E AUDITADO** a partir da extração integral (`Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.md`) e do PDF original com figuras (`Nemes-Incze_2008_Anomalies_Thickness_Measurements_Graphene_AFM.pdf`, pp. 1–16 do manuscrito publicado, Figuras 1–7, 30 referências).

---

## 1. Identificação bibliográfica

- **Título:** Anomalies in thickness measurements of graphene and few layer graphite crystals by tapping mode atomic force microscopy
- **Autores:** Péter Nemes-Incze, Zoltán Osváth, Katalin Kamarás, László Péter Biró
- **Ano:** 2008
- **Periódico:** *Carbon*, Vol. 46, Nº 11, pp. 1435–1442
- **DOI:** `10.1016/j.carbon.2008.06.022`
- **Links oficiais verificados:** [DOI / ScienceDirect](https://doi.org/10.1016/j.carbon.2008.06.022) | [Acesso Aberto Green (`arXiv:0812.0690`)](https://arxiv.org/pdf/0812.0690)

---

## 2. Problema investigado

**[Extraído integralmente do artigo, Seção *Introduction*, pp. 1–2]**  
Na caracterização de grafeno e grafite de poucas camadas (FLG, *few-layer graphene*) esfoliados sobre substratos de $\text{SiO}_2/\text{Si}$, diferentes grupos da literatura reportavam espessuras aparentes altamente discrepantes para uma única monocamada em relação ao óxido — variando de $0{,}35\text{ nm}$ a $1\text{ nm}$, ou até $1{,}0\text{--}1{,}6\text{ nm}$ em Novoselov *et al.* (2004) e $\sim 0{,}7\text{ nm}$ (com *offset* instrumental de $0{,}33\text{ nm}$) em Gupta *et al.* (2006). O trabalho investiga **por que o *Tapping Mode AFM* (TAFM) distorce em até $\sim 1\text{ nm}$ a altura aparente de um mesmo floco de grafeno/FLG sobre $\text{SiO}_2$**, demonstrando o papel decisivo da **amplitude livre de oscilação ($A_0$)**, do ***amplitude setpoint*** e da **transição entre os regimes de interação atrativo e repulsivo**.

---

## 3. Fundamentação

**[Extraído do artigo, Seção *Results and Discussion*, pp. 3–6]**  

1. **TAFM não mede topografia pura:** No modo de contato intermitente (*tapping*, AM-AFM) operando com amplitude constante, o sistema de realimentação traça uma superfície de **amortecimento constante** (*constant damping*) da oscilação do cantilever, a qual depende das propriedades locais do material e das forças ponta–amostra.
2. **Bistabilidade e transição de regime atrativo $\leftrightarrow$ repulsivo:** Conforme as simulações de Anczykowski *et al.* (1996) e o modelo analítico de Garcia & San Paulo (1999) citados pelos autores, ao aproximar a ponta oscilante da superfície, ocorre inicialmente uma redução aproximadamente linear da amplitude devido a forças atrativas de longo alcance (van der Waals, eletrostáticas e **forças capilares** da película de água adsorvida ao ar). A partir de uma separação crítica, ocorre um **salto descontínuo na curva Amplitude–Distância (AD)**, marcando o início do contato mecânico intermitente com domínio de **forças repulsivas líquidas** (*net repulsive regime*).
3. **Assimetria entre materiais heterogêneos ($\text{SiO}_2$ vs. grafeno/FLG):** Como o $\text{SiO}_2$ e o grafeno apresentam propriedades interfaciais e molhabilidade distintas — alterando fortemente a histerese da força capilar de menisco (Zitzler *et al.*, 2002) e o amortecimento no ramo atrativo — o salto de transição atrativo $\rightarrow$ repulsivo ocorre em **amplitudes livres diferentes para o óxido e para o grafeno**. Quando a ponta opera no regime atrativo sobre um ou ambos os materiais, o *offset* de amortecimento introduz um erro sistemático de até $1\text{ nm}$ na altura medida do degrau em relação ao $\text{SiO}_2$.
4. **Modo Contato (CAFM) e forças laterais:** Em modo contato estático, não há salto de bistabilidade oscilatória, mas diferenças de **atrito/forças laterais** entre o grafeno e o $\text{SiO}_2$ fletem/torcem o cantilever em sentidos opostos conforme a direção de varredura (*trace* vs. *retrace*), gerando artefatos de altura.

---

## 4. Metodologia

**[Extraído do artigo, Seção *Experimental* e *Results and Discussion*, pp. 2–6]**  

- **Preparo das amostras:** Esfoliação mecânica de HOPG (grau SPI-1, SPI Supplies) sobre lâminas de silício cobertas por camada de $\text{SiO}_2$ de $300\text{ nm}$. Identificação preliminar por microscopia óptica.
- **Instrumentação e parâmetros de AFM (condições ambiente):**
  - Equipamento: Veeco Multimode Nanoscope SPM, controlador IIIa, operando em TAFM e Contact AFM (CAFM).
  - Pontas de TAFM: silício Nanosensors modelo **PPP-NCHR**, raio de ponta $< 10\text{ nm}$, constante elástica $k \approx 42\text{ N/m}$, frequência de ressonância $f_0 \sim 300\text{ kHz}$; frequência de excitação (*drive frequency*) ajustada $5\%$ abaixo de $f_0$.
  - Experimentos sistemáticos variando a amplitude livre $A_0$ (determinada por curvas AD) de $16\text{ nm}$ a $30\text{ nm}$ (e até $5\text{--}40\text{ nm}$ na Fig. 7) mantendo o *setpoint* constante (ex.: $15\text{ nm}$ nas Figs. 2–3), além de curvas AD adquiridas separadamente sobre o floco FLG e sobre o $\text{SiO}_2$ adjacente (reduzindo a amplitude até $\sim 10\%$ de $A_0$, evitando $0\%$ para preservar reprodutibilidade).
  - Comparação com CAFM em diferentes deflexões (*setpoints* de $-2{,}0$ a $+1{,}0\text{ V}$) e nas duas direções de varredura (*left-to-right* vs. *right-to-left*).
- **Validação independente por Espectroscopia Raman:**
  - Microscópio Raman Renishaw 1000 MB, laser $\text{Ar}^+$ de $488\text{ nm}$, potência na faixa de $\text{mW}$ (evitando aquecimento), *spot* de $2\text{ }\mu\text{m}$.
  - Identificação inequívoca de 1, 2, 3 e $>10$ camadas pela forma e decomposição do pico 2D ($\sim 2700\text{ cm}^{-1}$, segundo Ferrari *et al.*, 2006) e correlação direta com imagens e perfis médios de TAFM nos dois regimes (alta e baixa $A_0$).

---

## 5. Resultados

**[Extraído integralmente do texto e das Figuras 1–7 do artigo]**  

1. **Invariância do degrau grafeno–grafeno vs. salto anômalo grafeno–óxido (Fig. 1):** Em dois flocos sobrepostos (C1 e C2 sobre $\text{SiO}_2$), mantendo o *setpoint* fixo e elevando $A_0$ de $16\text{ nm}$ para $30\text{ nm}$, as alturas aparentes C1–$\text{SiO}_2$ e C2–$\text{SiO}_2$ caíram abruptamente em **$0{,}8\text{--}1\text{ nm}$** próximo a $A_0 \approx 26\text{ nm}$ (por exemplo, C1 caiu de $\sim 1{,}8\text{ nm}$ para $\sim 0{,}7\text{ nm}$ e C2 de $\sim 2{,}2\text{--}2{,}4\text{ nm}$ para $\sim 1{,}3\text{--}1{,}4\text{ nm}$ na Fig. 1c). Em contraste, a altura relativa do degrau **C2 sobreposto a C1** (interface grafite–grafite, triângulos verdes) permaneceu **constante em $\sim 1{,}3\text{ nm}$** em toda a faixa de $A_0$, confirmando que degraus entre materiais idênticos (ou regiões dobradas) cancelam o erro de contraste de interação.
2. **Origem na bistabilidade das curvas AD e chaveamento aleatório (*random switching*, Figs. 2–4):**
   - Na curva AD sobre FLG com $A_0 = 25{,}8\text{ nm}$ (Fig. 2a), observa-se um salto claro na amplitude em $16\text{ nm}$ onde dois valores de deslocamento piezoelétrico separados por $\sim 1\text{ nm}$ correspondem à mesma amplitude.
   - Quando o *setpoint* ($15\text{ nm}$) coincide com o ponto de instabilidade sobre o FLG ($A_0 = 26\text{ nm}$, Fig. 2b), a eletrônica de *feedback* chaveia aleatoriamente entre os dois ramos, gerando linhas ruidosas e degraus falsos dentro do floco; quando coincide com a instabilidade sobre o $\text{SiO}_2$ ($A_0 \approx 21\text{ nm}$, Fig. 2c), a instabilidade aparece sobre o substrato.
   - Na Fig. 4, o mesmo floco apresenta três patamares aparentes conforme $A_0$ cresce: $\sim 3{,}5\text{ nm}$ (regime atrativo em ambos), $\sim 4{,}5\text{ nm}$ (repulsivo no óxido e atrativo no FLG) e **$2{,}25\text{ nm}$** ($\sim 7$ camadas, regime repulsivo em ambos acima de $A_0 \approx 25\text{--}26\text{ nm}$).
3. **Validação Raman $\times$ TAFM para 1, 2 e 3 camadas (Figs. 5 e 6):**
   - **Monocamada (1L, confirmada pelo pico 2D lorentziano único):** medida em **$0{,}406\text{ nm}$** (arredondada para $0{,}4\text{ nm}$ na Fig. 5) no regime repulsivo (Fig. 6a), contra **$1{,}735\text{ nm}$** no regime atrativo (Fig. 6b).
   - **Bicamada (2L, confirmada pelas 4 componentes no pico 2D):** medida em **$0{,}690\text{ nm}$** ($0{,}69\text{ nm}$) no regime repulsivo (Fig. 6c), contra **$1{,}850\text{ nm}$** no regime atrativo (Fig. 6d).
   - **Tricamada (3L):** medida em **$1{,}125\text{ nm}$** ($1{,}12\text{ nm}$) no regime repulsivo (Fig. 6e), contra **$2{,}474\text{ nm}$** no regime atrativo (Fig. 6f).
   - Os autores destacam que, embora o protocolo habitual seja escolher o *setpoint* o mais próximo possível de $A_0$ ("*gentle tapping*") para minimizar forças, essa prática coloca a ponta justamente no **regime atrativo**, produzindo as maiores superestimações ($\sim 1\text{ nm}$ de excesso na monocamada). Operar com alta $A_0$ e menor razão de *setpoint* (no regime repulsivo em ambas as superfícies) não causou dano observável à ponta nem às amostras.
4. **Comparação TAFM $\times$ CAFM (Fig. 7):** Em um floco de 6 camadas ($\sim 2\text{ nm}$ em TAFM repulsivo), o CAFM concordou razoavelmente e não apresentou variação com a força normal de contato (*deflection setpoint* de $-2{,}0$ a $+1{,}0\text{ V}$), porém exibiu uma **discrepância sistemática de $\sim 0{,}2\text{ nm}$ entre varreduras esquerda $\rightarrow$ direita e direita $\rightarrow$ esquerda**, atribuída à variação de forças laterais (atrito) entre grafeno e $\text{SiO}_2$ — efeito ausente em TAFM.

---

## 6. Limitações

**[Reconhecidas pelos autores + análise crítica do Agente D]**  

- **Reconhecidas pelos autores:**
  1. Os próprios autores afirmam (p. 6–7) que a origem exata do deslocamento da amplitude crítica entre o óxido e a grafite e a natureza detalhada das forças atrativas envolvidas ainda não eram totalmente compreendidas, demandando modelagem numérica e experimentos adicionais (especialmente controlando umidade relativa e menisco capilar).
  2. Mesmo no regime repulsivo otimizado, a espessura obtida para a monocamada ($0{,}406\text{ nm}$) ainda excede ligeiramente o espaçamento interplanar do grafite ($0{,}335\text{ nm}$), razão pela qual recomendam sempre corroborar o número de camadas por técnicas complementares (como espectroscopia Raman).
- **Análise crítica do Agente D:**
  1. O estudo foi realizado exclusivamente com um modelo de sonda rígida ($k \approx 42\text{ N/m}$) em um equipamento (Veeco Multimode IIIa) sob umidade ambiente não quantificada numericamente.
  2. Não separa experimentalmente a contribuição da camada de água interfacial aprisionada *entre* o grafeno e o $\text{SiO}_2$ da diferença de amortecimento mecânico ponta–amostra (aspecto que será aprofundado posteriormente por Shearer *et al.*, 2016, em PeakForce Tapping).
  3. O protocolo exige aquisição prévia manual de curvas AD em dois pontos (substrato e floco) para cada experimento, o que dificulta a automação pura sobre imagens já exportadas sem metadados de força/fase.

---

## 7. Contribuição para a dissertação

**[Análise do Agente D para o projeto PPGCEM/UFCA]**  

Este é o **artigo-chave de fundamentação física** sobre medição de espessura de grafeno por AFM na dissertação:
- Explica por que **a literatura reporta valores de $0{,}4$ a $1{,}7\text{ nm}$ para monocamada de grafeno** sem invocar apenas "erro de calibração": mesmo com scanner Z perfeitamente calibrado, uma variação no *setpoint* relativo ou em $A_0$ gera saltos de $\sim 1\text{ nm}$ (maiores que a própria espessura cristalográfica de $0{,}335\text{ nm}$ de uma camada!).
- Mostra que uma **ferramenta computacional que receba apenas imagens topográficas de AFM em RGB/escala de cinza** (ou mesmo mapas de altura em nm sem metadados de aquisição) **não pode inferir o número de camadas $N$ por uma simples divisão $h / 0{,}335\text{ nm}$** — pois $h_{\text{1L}}$ pode ser $0{,}41\text{ nm}$ no regime repulsivo ou $1{,}74\text{ nm}$ no regime atrativo, enquanto o incremento *intercamadas* ($\Delta h = h_{N+1} - h_N$, ou degraus em flocos sobrepostos/dobrados) é muito mais estável ($\sim 0{,}3\text{--}0{,}4\text{ nm}$).
- Fornece critério direto para detectar artefatos em imagens reais de grafeno esfoliado eletroquimicamente: **linhas horizontais de chaveamento abrupto (*bistable scan-line switching*, Fig. 2b–c)** sobre o floco ou sobre o substrato denunciam operação na fronteira de instabilidade da curva AD e devem ser sinalizadas ou rejeitadas pelo software antes da medição estatística.

---

## 8. Possíveis aplicações

**[Análise do Agente D — abordagens derivadas para o projeto]**  

- Implementar no módulo de análise de AFM da dissertação: (a) cálculo separado da altura em relação ao substrato ($h_{\text{1L}\text{--}\text{sub}}$) versus degraus internos floco-sobre-floco ou dobras ($\Delta h_{\text{int}}$); (b) **detector automático de chaveamento bistável por linha** (analisando saltos bimodais abruptos entre linhas de varredura adjacentes na máscara do floco e na máscara do substrato); e (c) registro obrigatório de metadados operacionais ($A_0$, razão de *setpoint*, frequência de operação, modo e canal de fase/erro) para classificar se a imagem foi adquirida em regime atrativo ou repulsivo.

---

## 9. Evidências

- **Seções principais do texto integral:** *Introduction* (pp. 1–2), *Experimental* (pp. 2–3), *Results and Discussion* (pp. 3–6), *Conclusions* (pp. 6–7).
- **Figuras-chave auditadas no PDF:**
  - **Fig. 1 (p. 8):** Flocos sobrepostos C1 e C2; queda de $0{,}8\text{--}1\text{ nm}$ em C1–$\text{SiO}_2$ e C2–$\text{SiO}_2$ em $A_0 \approx 26\text{ nm}$, enquanto C2–C1 permanece constante.
  - **Fig. 2a–c (p. 9):** Curva AD com salto de $\sim 1\text{ nm}$ na amplitude de $16\text{ nm}$ ($A_0 = 25{,}8\text{ nm}$) e imagens com *random switching* no FLG (2b) e no óxido (2c).
  - **Fig. 3a–b (p. 9):** Curvas AD em $A_0 = 24$, $26$ e $28{,}5\text{ nm}$ com *setpoint* a $15\text{ nm}$, evidenciando cruzamentos distintos no FLG ($\sim 26\text{ nm}$) e no óxido ($\sim 21\text{ nm}$).
  - **Fig. 4 (p. 10):** Altura aparente do degrau em função de $A_0$ com dois saltos ($21\text{ nm}$ e $25\text{ nm}$), variando de $3{,}5\text{ nm}$ a $4{,}5\text{ nm}$ e caindo a $2{,}25\text{ nm}$.
  - **Figs. 5 e 6 (pp. 11 e 13):** Correlação Raman 2D $\times$ TAFM para 1L ($0{,}406$ vs. $1{,}735\text{ nm}$), 2L ($0{,}690$ vs. $1{,}850\text{ nm}$) e 3L ($1{,}125$ vs. $2{,}474\text{ nm}$).
  - **Fig. 7 (p. 14):** Comparação TAFM vs. CAFM mostrando discrepância de $\sim 0{,}2\text{ nm}$ entre varreduras ida e volta em modo contato.

---

## 10. Prioridade de estudo

**Alta (Indispensável).** Artigo fundacional para qualquer pesquisador que caracterize espessura de grafeno por AFM. Responde diretamente a perguntas críticas de banca sobre por que o grafeno monocamada raramente mede $0{,}335\text{ nm}$ em AFM convencional e por que um "tapping suave" (*high setpoint*) piora o erro em vez de melhorá-lo.
