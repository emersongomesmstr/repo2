# Fichamento 03 — Shearer et al. (2016): Medição Precisa de Espessura de Grafeno por PeakForce Tapping e Sondas CNT

> **Nível de leitura declarado (Seção 7 do `PROMPT_MESTRE.md`):** **Resumo completo e metadados bibliográficos verificados** (IOPscience, Research@Flinders, PubMed e OpenAlex `verified_catalog.json`), complementados por **trechos indexados do manuscrito e literatura citante verificada** (*DigitalCommons@Linfield* e `arXiv`/AIP RSI 2019). O texto integral em PDF da versão publicada na IOPscience encontra-se sob barreira de acesso por assinatura e não pôde ser extraído integralmente; portanto, todos os números e conclusões aqui atribuídos ao artigo limitam-se estritamente ao que foi verificado nas fontes acessadas, sem preenchimento especulativo de parâmetros experimentais ausentes.

---

## 1. Identificação bibliográfica

- **Título:** Accurate thickness measurement of graphene
- **Autores:** Cameron J. Shearer, Ashley D. Slattery, Andrew J. Stapleton, Joseph G. Shapter, Christopher T. Gibson
- **Ano:** 2016 (publicado em 18 de fevereiro de 2016)
- **Periódico:** *Nanotechnology*, Vol. 27, Nº 12, artigo `125704` (10 páginas; ISSN `0957-4484`)
- **DOI:** `10.1088/0957-4484/27/12/125704`
- **Links oficiais verificados:** [IOPscience (`10.1088/0957-4484/27/12/125704`)](https://iopscience.iop.org/article/10.1088/0957-4484/27/12/125704) | [Repositório Flinders University](https://researchnow.flinders.edu.au/en/publications/accurate-thickness-measurement-of-graphene) | [PubMed (`PMID: 26894444`)](https://pubmed.ncbi.nlm.nih.gov/26894444/)

---

## 2. Problema investigado

**[Extraído do resumo oficial e metadados verificados]**  
Apesar de o AFM ser extensivamente empregado para medir simultaneamente as dimensões laterais e a espessura (e, por extensão, o número de camadas) de filmes de grafeno, a literatura acumulada apresenta grande imprecisão e dispersão para a espessura aparente da **monocamada de grafeno (SLG, *single-layer graphene*)**, com valores reportados entre **$0{,}4\text{ nm}$ e $1{,}7\text{ nm}$** — muito acima da distância interplanar cristalográfica teórica do grafite ($0{,}335\text{ nm}$). Essa discrepância tem sido atribuída a interações ponta–superfície, ajustes de *feedback* da imagem e química superficial. O trabalho busca estabelecer um **protocolo confiável** para medir a espessura real do grafeno e elucidar o papel físico da **camada interfacial de adsorvatos** e da **força/pressão de imageamento**.

---

## 3. Fundamentação

**[Extraído do resumo oficial + contextualização técnica verificada em literatura sobre PeakForce Tapping e nanotubos de carbono]**  

1. **Limitações do *Tapping Mode* (AM-AFM) convencional:** No *tapping mode* clássico, o controle de realimentação é indireto (baseado na amplitude média de oscilação em torno da frequência de ressonância), tornando a força normal instantânea dependente de efeitos dinâmicos não lineares, histerese capilar e transições atrativo–repulsivo (como mostrado por Nemes-Incze *et al.*, 2008).
2. **Princípio do *PeakForce Tapping* (PFT):** No modo *PeakForce Tapping* (documentado em notas técnicas e literatura verificada citada na pesquisa), a sonda oscila muito abaixo da frequência de ressonância do cantilever (tipicamente na faixa de $\text{kHz}$, ex.: $125\text{ Hz}$ a $8\text{ kHz}$), executando uma curva força–distância em cada pixel e utilizando diretamente a **força de pico repulsiva instantânea (*PeakForce setpoint*)** como sinal de realimentação linear, eliminando a bistabilidade de fase/amplitude do *tapping* ressonante.
3. **Camada interfacial de adsorvatos e pressão aplicada pela ponta:** Entre o floco de grafeno depositado ao ar e o substrato (como $\text{SiO}_2$ ou mica) frequentemente se aprisiona uma camada interfacial de adsorvatos/hidratação (água, contaminantes atmosféricos ou resíduos de processo). A espessura aparente medida depende não apenas da força total aplicada ($F$), mas da **pressão efetiva ($P \approx F / A_{\text{contato}}$)** exercida pela ponta, que determina quanto a camada adsorvida (e/ou a própria folha) é comprimida ou penetrada durante a aquisição.
4. **Sondas modificadas com nanotubos de carbono (CNT):** Sondas funcionalizadas com nanotubos de carbono na extremidade apresentam raio de ápice muito menor e razão de aspecto elevada em comparação com pontas piramidais convencionais de silício, reduzindo a área de contato e elevando drasticamente a pressão local mesmo sob forças normais moderadas, além de mitigar artefatos de convolução geométrica lateral.

---

## 4. Metodologia

**[Extraído exclusivamente do resumo oficial e dos trechos verificados indexados]**  

- **Modos e sondas comparados:** Uso comparativo de **sondas padrão de AFM** e **sondas modificadas com nanotubo de carbono (CNT)** operando no modo **PeakForce Tapping (PFT)**.
- **Variável experimental central investigada:** Variação sistemática do ***PeakForce setpoint*** (força máxima aplicada em cada ciclo de toque, calculada previamente pelo software antes da captura da imagem) para avaliar a dependência da altura aparente da monocamada de grafeno com a força/pressão exercida pela ponta e com a presença da camada de adsorvatos entre grafeno e substrato.
- **Referência alvo:** Comparação das alturas medidas sob diferentes pressões/forças com o valor teórico cristalográfico da monocamada ($0{,}335\text{ nm}$), buscando formular um protocolo reprodutível aplicável ao grafeno e extensível a outros materiais bidimensionais.
- *Observação de verificação:* Parâmetros numéricos internos de constantes elásticas específicas das sondas CNT utilizadas e valores exatos de *setpoint* em $\text{nN}$ ou pressão em $\text{GPa}$ não constam do resumo nem dos trechos indexados acessíveis e, portanto, não são especificados aqui (registrados como pendentes de consulta ao PDF integral).

---

## 5. Resultados

**[Extraído exclusivamente do resumo oficial e dos trechos indexados verificados]**  

1. **Redução drástica do erro de espessura na primeira camada:** Por meio do protocolo desenvolvido em *PeakForce Tapping* com controle da força/pressão de imageamento e uso de sondas padrão e modificadas com CNT, **o erro na medição da primeira camada de grafeno foi reduzido de $0{,}1\text{--}1{,}3\text{ nm}$** (correspondente aos $0{,}4\text{--}1{,}7\text{ nm}$ reportados na literatura em relação a $0{,}335\text{ nm}$) **para $0{,}1\text{--}0{,}3\text{ nm}$** (aproximando a leitura do valor verdadeiro de $0{,}335\text{ nm}$).
2. **Identificação dos dois mecanismos físicos dominantes:** O estudo estabelece que:
   - a **camada de adsorvatos na interface grafeno–substrato** é um fator físico determinante na superestimação da altura da monocamada (especialmente em baixas forças aplicadas); e
   - a **força de imageamento — especificamente a *pressão* exercida pela ponta sobre a superfície** (e não apenas a força nominal isolada, pois pontas mais agudas como CNT concentram a tensão em menor área) — governa a convergência da altura aparente em direção ao valor cristalográfico real, permitindo estabelecer um protocolo sistemático para determinar com acurácia a espessura de filmes de grafeno e outros materiais 2D.

---

## 6. Limitações

**[Análise crítica do Agente D — separando limitações físicas do método e lacunas de leitura]**  

- **Limitações físicas e instrumentais do protocolo:**
  1. A necessidade de exercer pressões elevadas (ou usar pontas CNT de raio nanoscópico) para comprimir/minimizar a influência da camada de adsorvatos e evitar a superestimação a baixas forças impõe um **compromisso delicado**: pressões excessivas podem causar desgaste prematuro ou flambagem lateral da ponta CNT (fenômeno posteriormente estudado pelo mesmo grupo em Slattery *et al.*, 2018, *Nanomaterials* 8(10):807), além de potencial dano ou indentação em amostras mais frágeis ou substratos poliméricos.
  2. Sondas modificadas com CNT são significativamente mais caras, menos padronizadas em produção comercial em massa e mais sensíveis a aderência/contaminação do que pontas convencionais de silício, o que restringe sua adoção rotineira em laboratórios multiusuários ou em controle industrial de alta vazão.
  3. O modo *PeakForce Tapping* é uma tecnologia proprietária da Bruker (embora análogos de força pulsada existam em outros fabricantes), de modo que parte dos conjuntos de dados de AFM encontrados na literatura ou gerados em outros equipamentos (como Park Systems ou Veeco antigos) continuará em *tapping* clássico ou contato.
- **Lacuna de verificação documental:** Sem acesso ao texto completo publicado na IOPscience, não foi possível auditar aqui as curvas exatas de altura aparente *versus* *PeakForce setpoint*, os valores numéricos de raio de ponta CNT e a distinção quantitativa entre os substratos testados (como $\text{SiO}_2$ vs. mica).

---

## 7. Contribuição para a dissertação

**[Análise do Agente D para o projeto PPGCEM/UFCA]**  

Este artigo — explicitamente citado inclusive no Slide 14 do piloto `IVEFAC333.pptx` (*"Shearer et al. (2016) · Medição de espessura de grafeno por AFM"*) — é o elo direto entre a física de interação ponta–amostra e o desenho experimental/computacional da dissertação:
1. **Complementaridade com Nemes-Incze *et al.* (2008):** Enquanto Nemes-Incze (2008) explicou o erro de até $\sim 1\text{ nm}$ pela **bistabilidade dinâmica (regime atrativo vs. repulsivo)** no *tapping mode* ressonante, Shearer *et al.* (2016) demonstram que, mesmo controlando diretamente a força normal em *PeakForce Tapping*, a **pressão da ponta e a camada interfacial de adsorvatos entre o grafeno e o substrato** ainda produzem um viés de $0{,}1\text{--}0{,}3\text{ nm}$ na primeira camada (e de $0{,}1\text{--}1{,}3\text{ nm}$ se não controlados).
2. **Implicação direta para o grafeno esfoliado eletroquimicamente da UFCA:** Flocos produzidos por esfoliação eletroquímica em meio aquoso/salino carregam maior probabilidade de retenção de água interfacial, resíduos iônicos/surfactantes e defeitos/grupos oxigenados do que grafeno clivado mecanicamente. Portanto, uma ferramenta computacional que estime o número de camadas $N$ **não deve assumir espessura nula de adsorvato interfacial ($h_0 = 0$)**; em vez disso, deve modelar $h(N) = h_0 + (N - 1)\,d_{002}$ (ou equivalente com *offset* interfacial $h_{\text{interface}}$ específico da 1ª camada sobre o substrato, distinguindo o degrau 1L–substrato dos degraus intercamadas $d_{002} \approx 0{,}335\text{--}0{,}34\text{ nm}$).

---

## 8. Possíveis aplicações

**[Análise do Agente D — abordagens futuras para a pesquisa]**  

- Adotar um **modelo paramétrico em duas etapas** no algoritmo de contagem de camadas a partir de mapas AFM: estimar separadamente (i) o *offset* interfacial $h_{\text{1L}\text{--}\text{sub}}$ (esperado entre $0{,}4$ e $0{,}7\text{ nm}$ em protocolos otimizados, ou até $1{,}7\text{ nm}$ em condições não otimizadas) e (ii) o passo intercamadas $\Delta h$ entre terraços adjacentes dentro de um mesmo floco multicamada, comparando $\Delta h$ com $0{,}335\text{ nm}$.
- Quando disponíveis os canais auxiliares de *PeakForce QNM* (adesão e dissipação), utilizá-los como **canais de entrada multimodais** para distinguir fronteiras de grafeno sobre $\text{SiO}_2$ ou regiões contaminadas por resíduos poliméricos/eletrolíticos mesmo quando o degrau topográfico estiver mascarado pela camada de adsorvato.

---

## 9. Evidências

- **Resumo oficial e metadados verificados:** *Nanotechnology* **27**(12), `125704` (2016), DOI `10.1088/0957-4484/27/12/125704` — faixa reportada na literatura ($0{,}4\text{--}1{,}7\text{ nm}$), redução do erro na 1ª camada de $0{,}1\text{--}1{,}3\text{ nm}$ para $0{,}1\text{--}0{,}3\text{ nm}$, emprego de sondas padrão e CNT em *PeakForce Tapping*, identificação da camada de adsorvato grafeno–substrato e da pressão da ponta como variáveis críticas.
- **Trechos indexados do manuscrito e literatura citante:** `DigitalCommons@Linfield` (`Shearer_2016_Nanotechnology_27_125704.pdf`, p. 6: referência ao valor verdadeiro de $0{,}335\text{ nm}$, estudo da superestimação da altura de SLG a baixa força aplicada em função do *PeakForce setpoint* e papel da camada de adsorvato); citação verificada em *Rev. Sci. Instrum.* **90**, 103702 (2019) confirmando o uso de PFT com sonda baseada em nanotubo de carbono e dependência da força normal.

---

## 10. Prioridade de estudo

**Alta (Indispensável — leitura integral recomendada assim que obtido acesso institucional via CAPES/IOPscience).** Juntamente com Nemes-Incze *et al.* (2008), constitui a principal referência experimental para justificar limites físicos de acurácia na determinação do número de camadas de grafeno por AFM e já integra o escopo bibliográfico citado pelo mestrando no piloto `IVEFAC333.pptx`.
