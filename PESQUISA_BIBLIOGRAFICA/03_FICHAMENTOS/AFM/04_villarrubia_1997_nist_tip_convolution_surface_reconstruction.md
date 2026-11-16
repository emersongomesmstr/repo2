# Fichamento 04 — Villarrubia (1997) & Obraztsova et al. (2008): Convolução Geométrica da Ponta, Reconstrução de Superfície e Estatística de Camadas de Grafeno por AFM

> **Nível de leitura declarado (Seção 7 do `PROMPT_MESTRE.md`):**
> - **Villarrubia (1997):** **TEXTO COMPLETO LIDO E AUDITADO** (pp. 425–454 do *J. Res. Natl. Inst. Stand. Technol.*, extraído integralmente via PDF acadêmico indexado, incluindo Seções 1–14, Eqs. 1–21, Figuras 1–16 e códigos C completos nos Apêndices A–E).
> - **Obraztsova *et al.* (2008):** **Resumo completo e metadados bibliográficos verificados** (Crossref e OpenAlex `verified_catalog.json`); o texto completo na editora Wiley está sob assinatura fechada e não foi lido diretamente.

---

## 1. Identificação bibliográfica

### Referência principal (texto completo)
- **Título:** Algorithms for Scanned Probe Microscope Image Simulation, Surface Reconstruction, and Tip Estimation
- **Autor:** John S. Villarrubia
- **Ano:** 1997 (julho–agosto de 1997; aceito em 16 de fevereiro de 1997)
- **Periódico:** *Journal of Research of the National Institute of Standards and Technology* (*J. Res. Natl. Inst. Stand. Technol.*), Vol. 102, Nº 4, pp. 425–454
- **DOI:** `10.6028/jres.102.030`
- **Links oficiais verificados:** [DOI / NIST](https://doi.org/10.6028/jres.102.030) | [PDF indexado (Semantic Scholar)](https://pdfs.semanticscholar.org/53e1/a59af3a688fe65c4df7bfeb18d02604e71ac.pdf)

### Referência complementar (resumo e metadados verificados)
- **Título:** Statistical analysis of atomic force microscopy and Raman spectroscopy data for estimation of graphene layer numbers
- **Autores:** Ekaterina A. Obraztsova, Alexander V. Osadchy, Elena D. Obraztsova, Serge Lefrant, Igor V. Yaminsky
- **Ano:** 2008 (publicado online em 24 de setembro de 2008; edição impressa de outubro de 2008)
- **Periódico:** *physica status solidi (b)*, Vol. 245, Nº 10, pp. 2055–2059
- **DOI:** `10.1002/pssb.200879657`
- **Link oficial verificado:** [DOI / Wiley](https://doi.org/10.1002/pssb.200879657)

---

## 2. Problema investigado

- **Em Villarrubia (1997) [extraído do texto completo, Seção 1, pp. 425–426]:** Como modelar matematicamente, corrigir e estimar as distorções geométricas causadas pela finitude do raio e da forma da ponta em Microscopia de Varredura por Sonda (SPM/AFM) — especialmente na presença de ruído experimental — quando a amostra possui degraus íngremes, partículas ou rugosidades com razão de aspecto comparável à da ponteira? Em particular, como estimar a geometria da ponta **sem depender de um padrão caracterizador previamente conhecido por técnica independente** (*blind tip reconstruction*) e evitar que o ruído desestabilize essa reconstrução?
- **Em Obraztsova *et al.* (2008) [extraído do resumo oficial]:** Como transformar o AFM — frequentemente usado apenas de modo ilustrativo em grafeno — em um método quantitativo simples e confiável para estimar o número de camadas de flocos de grafeno preparados por clivagem mecânica de HOPG, confrontando a distribuição estatística de alturas em AFM com a espectroscopia Raman de dois fônons?

---

## 3. Fundamentação

**[Extraído integralmente de Villarrubia (1997), Seções 2–6, pp. 426–441]**  

1. **Modelo geométrico de contato rígido e *Umbra*:** A amostra $S$, a imagem $I$ e a ponta $T$ (cujo ápice está na origem) são descritas em morfologia matemática em escala de cinza por suas *umbras* ($S = \{(x,y,z) \mid z \le s(x,y)\}$) e por suas superfícies superiores (*tops*, $T[S] = s(x,y)$). Assume-se contato sem compressão elástica nem *undercuts* — aproximação válida em escalas grandes frente a variações sub-nanométricas de compressibilidade ou função trabalho ($\lesssim 1\text{ nm}$).
2. **Formação da imagem como Dilatação Morfológica ($I = S \oplus P$):** Ao baixar a ponta até o primeiro ponto de contato com a amostra (Eq. 1), a altura registrada pelo ápice em $(x,y)$ equivale à dilatação de $S$ pela reflexão da ponta pela origem, $p(x,y) = -t(-x,-y)$ (Eqs. 3–5):
   $$i(x,y) = \max_{(u,v)} [s(x-u, y-v) + p(u,v)]$$
   Como resultado, saliências e bordas de degraus ou flocos na imagem aparecem **lateralmente alargadas** (*tip dilation*), enquanto sulcos estreitos ou bases de degraus íngremes são preenchidos pelo perfil lateral da ponta.
3. **Reconstrução de superfície por Erosão Morfológica ($S_r = I \ominus P$):** Usando propriedades da morfologia matemática ($(A \oplus B) \ominus B \ge A$ e $[(A \oplus B) \ominus B] \oplus B = A \oplus B$), prova-se que a erosão (Eqs. 8–12):
   $$s_r(x,y) = \min_{(u,v)} [i(x+u, y+v) - p(u,v)]$$
   produz o **menor limitante superior** (*least upper bound*) consistente com a imagem medida, correspondente à superfície de penetração mais profunda da ponta (equivalente à reconstrução por envelope de Keller & Franke sem exigir derivadas numéricas instáveis).
4. **Mapas de Certeza (*Certainty Maps*, Pingali & Jain):** Nos pontos onde a ponta toca $S_r$ em um **único ponto** (Eq. 13: $i(x,y) + t(u,v) = s_r(x+u,y+v)$ com contagem $= 1$), garante-se que $s_r = s$; onde há múltiplos contatos simultâneos (ex.: fundo de vales em V ou cantos de degraus íngremes), a região verdadeira não foi tocada e $c(x,y) = 0$.
5. **Reconstrução Cega da Ponta (*Blind Tip Estimation*):** Por simetria entre ponta e amostra, qualquer pico isolado na imagem não pode ter curvatura mais aguda que o próprio ápice da ponta (caso contrário, a amostra teria largura negativa não física). Iterando um limitante superior inicial $P_0$ pela relação (Eqs. 14–15):
   $$P_{i+1} = \bigcap_{x \in I} [(I - x) \oplus P'_i(x)] \cap P_i, \quad P'_i(x) = P_i \cap (x - I)$$
   converge-se para $P_R$, a ponta mais romba possível ainda fisicamente compatível com todas as feições da imagem.
6. **Não linearidade frente ao ruído:** Como dilatação e erosão usam operadores `max`/`min` (não lineares), **ruído de média zero introduz viés sistemático**: na erosão de superfície (Fig. 9), picos positivos de ruído são ignorados, mas picos negativos amplificam-se formando depressões em formato da ponta, rebaixando a reconstrução em $\sim 2\sigma$ a $3\sigma$ quando a ponta cobre $\sim 10\times 10$ pixels. Na reconstrução cega com limiar `thresh = 0`, qualquer pico agudo de ruído colapsa iterativamente a ponta estimada em direção a $I \ominus I$ (ponta artificialmente pontiaguda com descontinuidade de inclinação no ápice, Fig. 11a).
7. **Fundamentação complementar em Obraztsova *et al.* (2008) [resumo oficial]:** Ao invés de depender de um único perfil transversal arbitrário em um floco de grafeno, a análise estatística das distribuições de espessura ao longo do floco e entre múltiplos flocos revela modas discretas correspondentes a $1, 2, 3, \dots$ camadas, corroboráveis por espectroscopia Raman de dupla ressonância (pico 2D) e estrutura eletrônica via DFT.

---

## 4. Metodologia

- **Villarrubia (1997) [extraído integralmente, Seções 3.4, 4.2, 4.4, 5.2–5.3, 6–7 e Apêndices A–E]:**
  - Implementação completa em linguagem C com aritmética inteira (`long **`, evitando erros de arredondamento em testes de igualdade e compatível com conversores A/D de 12–16 bits) de todas as rotinas: `ireflect()`, `idilation()`, `ierosion()`, `iopen()`, `icmap()`, `itip_estimate_point()`, `itip_estimate_iter()`, `itip_estimate()` e a versão acelerada `itip_estimate0()` (que seleciona primeiro máximos locais via `useit()` com vizinhança $\delta = \max(\text{tip\_xsiz}, \text{tip\_ysiz})/10$).
  - Tratamento rigoroso de **bordas de imagem** via suposição de pior caso (*worst-case assumptions*) para não violar os limitantes superiores/inferiores.
  - Introdução do parâmetro de estabilização **`thresh`** ($T \approx 3\sigma\text{--}5\sigma$ do ruído RMS da imagem) na atualização do perfil da ponta (`dil < tip0 - thresh ? dil + thresh`), avaliado em simulações com ruído gaussiano ($\sigma = 1\text{ nm}$ sobre escala de $160\text{ nm}$, Figs. 10–11) e reconstrução cega parcial combinada com esferas conhecidas (Fig. 16).
  - Protocolo prático de pré-processamento (Seção 7.1): **nivelamento por linha (*linewise flattening*) e ajuste de fundo com máscara** (excluindo partículas/moléculas do ajuste) **seguido de filtro mediano** (evitando médias de vizinhança que arredondam bordas agudas) **antes** das operações morfológicas.
- **Obraztsova *et al.* (2008) [extraído do resumo oficial]:**
  - Clivagem micromecânica de HOPG em múltiplos flocos de grafeno; medição de distribuição estatística de espessura por AFM sobre flocos individuais e média entre todos os flocos; caracterização subsequente dos mesmos flocos por espectroscopia Raman de dois fônons e cálculos DFT da estrutura eletrônica em função do número de camadas.

---

## 5. Resultados

1. **Villarrubia (1997) [extraído do texto completo, Seções 5–7, Figs. 6–16]:**
   - Demonstrou reconstrução fiel de uma ponta parabólica ($r = 40\text{ nm}$) a partir de superfície granular simulada ($r_{\min} = 25\text{ nm}$, Fig. 6), provando também que a largura reconstruída próxima ao ápice permanece **insensível em ampla faixa ao tamanho da pegada inicial $s_x$** desde que $s_x$ seja maior que a ponta real (Fig. 7).
   - Quantificou a degradação do mapa de certeza sob ruído $\sigma = 1\text{ nm}$ (correlação cai para $0{,}2$, subindo para $0{,}4$ após fechamento morfológico de lacunas, Fig. 10).
   - Demonstrou que a curva de erro RMS da ponta reconstruída em função do limiar $T$ apresenta um **mínimo claro próximo a $T \approx 3\sigma$** (entre $2{,}3\sigma$ e $4{,}3\sigma$, Fig. 11b), evitando tanto a instabilidade para $T$ muito pequeno quanto o embotamento excessivo para $T$ grande.
   - Formulou protocolos para: (i) usar a própria amostra como caracterizador (aceitável para feições mais rombas/baixas que as mais agudas da imagem, Fig. 13); (ii) usar caracterizador separado com verificação **antes e depois** para detectar desgaste/mudança da ponta (Fig. 14); (iii) combinar múltiplas orientações de bordas ou múltiplas imagens (`itip_estimate` sequencial, Fig. 15); e (iv) reconstrução **parcialmente cega** combinando esferas coloidais conhecidas (ápice) com degraus/rugosidade desconhecidos (flancos, Fig. 16).
2. **Obraztsova *et al.* (2008) [extraído do resumo oficial]:**
   - A distribuição estatística de espessuras dos flocos esfoliados apresentou uma sequência clara de máximos discretos em **$0{,}7\text{ nm}$, $1{,}1\text{ nm}$, $1{,}4\text{ nm}$, $1{,}7\text{ nm}$ e $2{,}1\text{ nm}$**, correspondendo respectivamente a $1, 2, 3, 4$ e $5$ camadas de grafeno (incrementos médios de $\sim 0{,}35\text{ nm}$ por camada após um *offset* inicial de $\sim 0{,}35\text{ nm}$ na primeira camada).
   - Obteve-se **correspondência perfeita** entre o número de camadas estimado pela estatística de AFM e a atribuição por espectroscopia Raman de dois fônons interpretada via DFT.

---

## 6. Limitações

- **Villarrubia (1997) [reconhecidas na Seção 6.4, pp. 441–442, e análise crítica do Agente D]:**
  - *Reconhecidas pelo autor:* O modelo puramente geométrico de contato rígido desconsidera: (1) não linearidades dos *scanners* piezoelétricos (exigindo operação em *closed loop*); (2) flexão lateral do cantilever por atrito; (3) *overshoot* da malha de *feedback* ao varrer degraus íngremes rapidamente; (4) dano/alteração da ponta durante a varredura; e (5) na escala sub-nanométrica, **compressibilidade heterogênea ou variações de função trabalho/forças de interação** — exatamente o regime crítico na caracterização de espessura de grafeno monocamada ($<1\text{ nm}$)! Ademais, é impossível reconstruir regiões profundas que a ponta nunca tocou.
  - *Análise crítica adicional:* A reconstrução cega com imagens muito planas (como substratos de $\text{SiO}_2$ com rugosidade $R_q < 0{,}3\text{ nm}$ e flocos de grafeno de $\sim 0{,}4\text{--}1{,}5\text{ nm}$ com degraus quase planos) contém pouca informação sobre os flancos altos da ponta; nesse cenário, a convolução da ponta afeta principalmente a **medição de largura/área lateral** (alargamento aparente de bordas e *double-tip*, como visto no protocolo VAMAS) e o **arredondamento de perfis de borda**, mas **não corrige** o *offset* vertical físico de adsorvatos/regime atrativo sobre platôs largos.
- **Obraztsova *et al.* (2008) [análise crítica baseada no resumo oficial]:**
  - Sem acesso ao texto completo Wiley, não é possível auditar o modelo do AFM, o modo de operação (*tapping* vs. contato), os parâmetros de *setpoint*, o algoritmo exato de cálculo da distribuição (histograma por pixel vs. média por floco) nem a largura/desvio padrão de cada pico ($0{,}7; 1{,}1; 1{,}4\dots\text{ nm}$). Além disso, um máximo de $0{,}7\text{ nm}$ para monocamada pressupõe condições experimentais relativamente uniformes; se houver mudança de umidade ou de regime atrativo/repulsivo (Nemes-Incze *et al.*, 2008), a escala fixa de $0{,}7\text{ nm}$ para 1L desloca-se.

---

## 7. Contribuição para a dissertação

**[Análise do Agente D para o projeto PPGCEM/UFCA]**  

Este par de referências fundamenta dois pilares matemáticos e algorítmicos da ferramenta computacional proposta:
1. **Separação rigorosa entre distorção lateral (geométrica) e anomalia vertical (física):** Villarrubia (1997) demonstra exatamente como a geometria finita da ponta ($R \sim 5\text{--}30\text{ nm}$) **dilata lateralmente** flocos nanométricos e introduz zonas de incerteza junto às bordas — explicando a diferença entre a largura medida no topo do platô e na base do degrau adotada no protocolo VAMAS (`NPL AS 103`, Fig. 14c). Porém, como Villarrubia adverte na Seção 6.4, seu modelo geométrico *não* corrige efeitos físico-químicos na escala $<1\text{ nm}$, o que complementa perfeitamente Nemes-Incze (2008) e Shearer (2016).
2. **Ordem correta de pré-processamento e perigo de filtros ingênuos:** Como erosão e reconstrução cega não comutam com filtragem, Villarrubia prova que **nivelamento linha-a-linha com máscara (excluindo os flocos) e remoção mediana de *scars*/ruído de varredura devem preceder qualquer extração morfológica**, e que filtros de média borram bordas reais dos degraus.
3. **Quantização estatística de alturas (Obraztsova 2008):** Demonstra que a distribuição estatística de alturas em múltiplos flocos exibe periodicidade de $\sim 0{,}35\text{ nm}$ ($0{,}7 \rightarrow 1{,}1 \rightarrow 1{,}4 \rightarrow 1{,}7 \rightarrow 2{,}1\text{ nm}$), reforçando que o *offset* de interface substrato–1L ($\sim 0{,}35\text{ nm}$ nesse estudo) pode ser calibrado estatisticamente quando há múltiplos terraços/camadas no conjunto amostral.

---

## 8. Possíveis aplicações

**[Análise do Agente D — abordagens futuras para a dissertação]**  

- Integrar rotinas de **reconstrução cega de ponta** (já implementadas no Gwyddion a partir do algoritmo exato de Villarrubia, 1997) para estimar o raio efetivo $R_{\text{tip}}$ diretamente de degraus/partículas na amostra e aplicar correção de largura lateral ou cálculo de incerteza geométrica ($\Delta L \approx 2\sqrt{2 R_{\text{tip}} h}$) na medição automática de flocos submicrométricos de grafeno.
- Implementar **detecção de *double-tip* / assimetria de borda** via estimativa cega da ponta: se a ponta estimada apresentar dois ápices distintos ou forte assimetria anômala, o *pipeline* sinaliza o mapa como contaminado por artefato de ponta dupla (alinhado ao critério de rejeição da Seção 5.3.2 do relatório NPL VAMAS).
- Combinar histogramas de altura individuais com **análise estatística agregada multi-floco** (inspirada em Obraztsova *et al.*, 2008) para identificar os espaçamentos quantizados de camadas em dispersões de grafeno esfoliado eletroquimicamente.

---

## 9. Evidências

- **Villarrubia (1997) [texto completo]:** Seção 2 (pp. 426–428, umbra e dilatação); Seção 3 (pp. 428–430, Eqs. 1–5, `idilation`); Seção 4 (pp. 430–433, Eqs. 8–13, `ierosion` e `icmap`); Seção 5 (pp. 433–438, Eqs. 14–19, reconstrução cega, Figs. 6–8); Seção 6 (pp. 438–442, efeito não linear do ruído, Figs. 9–11 e limitações instrumentais na Seção 6.4); Seção 7 (pp. 442–446, filtragem com máscara e filtro mediano na Seção 7.1, modos práticos nas Figs. 12–16); Apêndices A–E (pp. 447–453, código-fonte completo em C).
- **Obraztsova *et al.* (2008) [resumo oficial]:** *phys. status solidi (b)* **245**(10), 2055–2059 (2008), DOI `10.1002/pssb.200879657` — picos discretos de espessura em $0{,}7\text{ nm}$, $1{,}1\text{ nm}$, $1{,}4\text{ nm}$, $1{,}7\text{ nm}$ e $2{,}1\text{ nm}$ e correspondência com espectroscopia Raman de dois fônons + DFT.

---

## 10. Prioridade de estudo

**Alta.** Villarrubia (1997) é a referência canônica e padrão NIST/Gwyddion para entender e corrigir matematicamente artefatos de ponta e interação não linear com ruído e nivelamento; Obraztsova *et al.* (2008) fornece uma ponte estatística clássica entre distribuição de alturas em AFM e validação por Raman, embora exija leitura integral futura caso seja adotada quantitativamente.
