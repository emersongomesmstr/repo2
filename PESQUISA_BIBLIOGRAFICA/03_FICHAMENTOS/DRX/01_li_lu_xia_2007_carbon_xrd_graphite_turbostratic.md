# Fichamento 01 — Padrões de Difração de Raios X de Grafite e Carbono Turboestrático e Padronização Metrológica (Li et al., 2007; Iwashita et al., 2004)

> **Status de Leitura e Verificação:** **Metadados verificados, resumos oficiais completos, trechos públicos da Introdução e índice de seções (ScienceDirect / OpenAlex)** para ambos os artigos (publicações em acesso fechado / assinatura, `oa_status: closed`, sem recuperação de PDF integral neste ambiente). Todas as informações específicas extraídas dos textos acessíveis estão explicitamente separadas da fundamentação física estabelecida e da análise crítica do Agente B.

---

## 1. Identificação bibliográfica

### Referência Principal
- **Título:** X-ray diffraction patterns of graphite and turbostratic carbon
- **Autores:** Zongquan Li (`Z.Q. Li`), C. J. Lu, Z. P. Xia, Yanchun Zhou (`Y. Zhou`), Zhihong Luo (`Z. Luo`)
- **Ano:** 2007 (publicado online em 2 de abril de 2007; fascículo de julho de 2007)
- **Periódico:** *Carbon* (Elsevier), Volume 45, Número 8, Páginas 1686–1695
- **DOI:** `10.1016/j.carbon.2007.03.038`
- **URL oficial:** <https://doi.org/10.1016/j.carbon.2007.03.038> (ScienceDirect: <https://www.sciencedirect.com/science/article/abs/pii/S0008622307001467>)
- **Identificador OpenAlex:** `W2024817672` (1.735 citações verificadas em OpenAlex; acesso fechado)

### Referência Complementar de Padronização Experimental
- **Título:** Specification for a standard procedure of X-ray diffraction measurements on carbon materials
- **Autores:** Norio Iwashita, Chong Rae Park, Hiroyuki Fujimoto, Minoru Shiraishi, Michio Inagaki
- **Ano:** 2004
- **Periódico:** *Carbon* (Elsevier), Volume 42, Número 4, Páginas 701–714 *(Tipo OpenAlex: `standard`)*
- **DOI:** `10.1016/j.carbon.2004.02.008`
- **URL oficial:** <https://doi.org/10.1016/j.carbon.2004.02.008> (ScienceDirect: <https://www.sciencedirect.com/science/article/abs/pii/S0008622304001046>)
- **Corrigendum verificado:** Iwashita, N. et al., *Corrigendum to "Specification for a standard procedure of X-ray diffraction measurements on carbon materials" [Carbon 42 (2004) 701–714]*, *Carbon*, v. 42, n. 10, p. 2131, 2004, DOI: `10.1016/j.carbon.2004.05.027` (`W2024685917`).
- **Identificador OpenAlex:** `W1988932847` (526 citações verificadas em OpenAlex; acesso fechado)

---

## 2. Problema investigado

### Fatos extraídos dos textos acessíveis
- **Li et al. (2007):** Embora a difratometria de raios X (DRX/XRD) seja rotineiramente empregada para caracterizar grafite hexagonal (`h-graphite`) e carbono turboestrático (`t-carbon`, frequentemente denominado "grafite desordenado" ou produzido durante moagem em moinho de bolas após a fase nanocristalina inicial de $2\text{–}10\ \text{nm}$), havia necessidade de identificar quantitativamente **como variações microestruturais específicas alteram as intensidades, posições angulares ($2\theta$) e larguras à meia altura (FWHM) das linhas de difração**. O problema central é testar se ângulos de difração e FWHMs medidos diretamente no DRX podem ser convertidos de forma simples e ingênua em parâmetros de rede e tamanhos de cristalito no carbono turboestrático.
- **Iwashita et al. (2004):** O 117º Comitê da *Japan Society for the Promotion of Sciences* (JSPS) havia estabelecido originalmente em **1963** o procedimento-padrão denominado **método "Gakushin"** para determinar constantes de rede e tamanhos de cristalito em materiais carbonosos (especialmente grafitizados). Em **2002**, o comitê iniciou a revisão dessa especificação para incorporar procedimentos computacionais modernos (varredura automática passo-a-passo — *step-scanning* — e ajuste de perfil das linhas de difração) e disponibilizá-la em inglês à comunidade internacional.

### Análise crítica — Agente B
- Esses dois trabalhos formam o alicerce experimental e teórico da difração em carbonos $sp^2$ lamelares: enquanto Iwashita et al. (2004) padronizam *como medir e calibrar* experimentalmente um difratograma de carbono (corrigindo desvios angulares e instrumentais com padrão interno de silício), Li et al. (2007) demonstram os *limites físicos da interpretação convencional* (Bragg + Scherrer) quando o empilhamento ordenado `ABAB` dá lugar à desordem turboestrática, curvatura de folhas e flutuações de espaçamento interplanar — exatamente o regime estrutural encontrado em pós de grafeno esfoliado, GO e rGO.

---

## 3. Fundamentação

### Fatos extraídos dos textos acessíveis
- **Li et al. (2007):**
  - **Grafite hexagonal (`h-graphite`) vs. carbono turboestrático (`t-carbon`):** Ambos são formados pelo empilhamento de camadas de grafeno com espaçamento regular, mas com graus distintos de ordenamento de empilhamento. O `h-graphite` possui empilhamento `AB` ordenado tridimensionalmente, enquanto no `t-carbon` as camadas de grafeno podem **transladar-se aleatoriamente** entre si e **rotacionar em torno da normal às camadas**, além de exibir espaçamento interplanar aumentado (particularmente nas bordas de flocos), **curvatura** de folhas e outros defeitos estruturais observados em grafite moído mecanicamente.
  - **Equação geral de Debye (*general Debye equation*):** Em vez de assumir periodicidade cristalina infinita tridimensional (como na cristalografia clássica de Bragg para monocristais/pós ideais), Li et al. (2007) simulam o padrão de difração diretamente a partir da distribuição discreta de distâncias interatômicas no cristalito.
  - **Densidade numérica de distâncias interatômicas (NDID):** Definida pelos autores como métrica sensível simultaneamente ao tamanho e às distorções microestruturais do cristalito, mediando a relação entre geometria realística em espaço real e intensidade espalhada no espaço recíproco.
- **Iwashita et al. (2004):**
  - Fundamenta-se na determinação padronizada dos parâmetros de rede ($a_0$, $c_0$, $d_{002}$) e dos tamanhos médios de cristalito ($L_a$, $L_c$) de materiais carbonosos, utilizando padrão interno de referência (silício) para calibração angular de $2\theta$ e correção da função instrumental sob aquisição digital por *step-scanning* e *profile fitting*.

### Fundamentação física estabelecida (contexto obrigatório de DRX — Agente B)
- **Lei de Bragg e fator de estrutura ($F_{hkl}$):** Para radiação monocromática de comprimento de onda $\lambda$ (tipicamente Cu $K\alpha$, $\lambda = 0{,}15406\ \text{nm}$ para $K\alpha_1$ ou média ponderada $0{,}15418\ \text{nm}$), a interferência construtiva entre planos cristalinos $(hkl)$ com distância interplanar $d_{hkl}$ ocorre nos ângulos definidos pela Lei de Bragg:
  $$n\lambda = 2\,d_{hkl}\sin\theta_{hkl}$$
  A intensidade integrada depende do quadrado do **fator de estrutura** $|F_{hkl}|^2 = \left|\sum_j f_j \exp\left[2\pi i (hx_j + ky_j + lz_j)\right]\right|^2$, multiplicidade, fator de Lorentz-polarização e absorção.
- **Assinaturas do grafite hexagonal $2H$ (grupo espacial $P6_3/mmc$):** O empilhamento ordenado `ABAB` produz a reflexão basal intensa **`(002)` em $2\theta \approx 26{,}5^\circ$ (Cu $K\alpha$), correspondente a $d_{002} \approx 0{,}335\ \text{nm}$** ($c_0 \approx 0{,}6708\ \text{nm}$), além de harmônicos `(004)` ($2\theta \approx 54{,}6^\circ$) e reflexões mistas tridimensionais `(100)`, `(101)`, `(102)`, `(103)`, `(110)` e `(112)` que atestam coerência de fase entre camadas adjacentes.
- **Transição para carbono turboestrático (`t-carbon`):** Quando as folhas paralelas sofrem rotações e translações aleatórias no plano basal (perda de registro `ABAB`), os termos de interferência cruzada entre camadas para $h, k \neq 0$ e $l \neq 0$ se anulam em média:
  1. As reflexões 3D `(101)`, `(102)`, `(103)` desaparecem;
  2. Os picos `(00l)` subsistem apenas como reflexões basais alargadas e frequentemente deslocadas para ângulos menores ($d_{002} \ge 0{,}344\ \text{nm}$);
  3. Surgem **bandas bidimensionais assimétricas `(hk)`** — especialmente a banda **`(10)` em torno de $2\theta \approx 42^\circ\text{–}45^\circ$ (Cu $K\alpha$)** e a banda `(11)` em torno de $77^\circ\text{–}80^\circ$ — com subida abrupta no lado de baixo ângulo e cauda prolongada para ângulos maiores (perfil de Warren), decorrente do corte do bastão recíproco contínuo $(hk)$ pela esfera de Ewald em amostras orientadas aleatoriamente.

---

## 4. Metodologia

### Fatos extraídos dos textos acessíveis
- **Li et al. (2007):**
  - Simulação computacional de padrões de DRX de grafite hexagonal (`h-graphite`) e carbono turboestrático (`t-carbon`) pela **equação geral de Debye**.
  - Análise paramétrica da sensibilidade das curvas de NDID, posições angulares ($2\theta$) e larguras à meia altura (FWHM) em função do tamanho de cristalito e de **cinco fatores de distorção** no `t-carbon`:
    1. Rotação aleatória em torno da normal às camadas de grafeno;
    2. Translação lateral aleatória entre camadas;
    3. Curvatura das camadas de grafeno;
    4. Flutuação positiva local do espaçamento interplanar;
    5. Flutuação das posições atômicas intracamada.
  - Comparação com padrões experimentais de grafite submetido a moagem em moinho de bolas (*ball-milled graphite*, seção *Sample preparation* e *Experimental XRD patterns and simulation*).
- **Iwashita et al. (2004):**
  - Especificação normativa revisada pelo 117º Comitê da JSPS descrevendo preparo de amostra misturada a **padrão de silício** (*silicon standard*), parâmetros de varredura automática por passos (*step-scanning*), correção angular com base nas reflexões conhecidas do Si, ajuste computacional de perfil (*profile fitting*) e extração padronizada de $a_0$, $c_0$, $L_a$ e $L_c$.

### Análise crítica — Agente B
- A abordagem pela equação de Debye (Li et al., 2007) evita a hipótese irrealista de rede periódica 3D infinita embutida na formulação padrão de Rietveld baseada em células unitárias convencionais, tornando-se computacionalmente compatível com modelos atomísticos finitos, curvos e turboestráticos de grafeno de poucas camadas. Contudo, o custo computacional da equação de Debye escala quadraticamente $O(N_{\text{átomos}}^2)$ (ou via histograma de pares/NDID), o que exige otimização algorítmica para inversão/ajuste direto contra difratogramas experimentais.

---

## 5. Resultados

### Fatos extraídos dos textos acessíveis
- **Li et al. (2007):**
  - Os cinco fatores de distorção no `t-carbon` (rotação, translação, curvatura, flutuação positiva local de $d_{002}$ e flutuação de posições atômicas) exercem **influências distintas sobre a densidade numérica de distâncias interatômicas (NDID)** e, consequentemente, sobre os perfis de difração simulados.
  - **Resultado central declarado no resumo:** os ângulos de difração e as FWHMs das linhas de difração **não podem ser utilizados de forma simplificada** para determinar parâmetros de rede e tamanhos de cristalito de carbono turboestrático (`t-carbon`).
- **Iwashita et al. (2004):**
  - Entrega a versão em inglês da especificação revisada do **método Gakushin** (originalmente de 1963, revisado em 2002), padronizando a transição de leituras analógicas/manuais para coleta digital por *step-scanning* e ajuste computacional de perfil para $a_0$, $c_0$, $L_a$ e $L_c$ em materiais carbonosos (posteriormente objeto de testes interlaboratoriais *round-robin* e de um *Corrigendum* em *Carbon* 42(10):2131, 2004).

### Análise crítica — Agente B
- O resultado de Li et al. (2007) explica por que valores nominais de $L_c$ e $L_a$ obtidos por aplicação direta da fórmula de Scherrer a grafenos reduzidos (rGO) ou esfoliados em fase líquida frequentemente divergem de medidas por TEM ou Raman: em sistemas com curvatura de folha e flutuação local de $d_{002}$, o alargamento e a assimetria dos picos combinam tamanho finito *e* distorção estrutural, deslocando inclusive o máximo aparente de `(002)` e das bandas `(hk)`. Sem o protocolo de calibração instrumental tipo Iwashita et al. (2004) e sem modelagem de perfil/desordem, o usuário confunde artefato de equipamento ou desordem turboestrática com espessura nanométrica.

---

## 6. Limitações

### Fatos extraídos dos textos acessíveis
- **Lacuna de leitura integral:** Ambos os artigos são de **acesso fechado** na editora Elsevier; portanto, equações explícitas de cada modelo de distorção, parâmetros geométricos exatos dos cristalitos simulados, valores numéricos de desvios de $2\theta$/FWHM em Li et al. (2007) e tabelas de coeficientes de calibração do padrão Si em Iwashita et al. (2004) **não puderam ser inspecionados diretamente neste ambiente**.

### Análise crítica — Agente B
- **Limitações metodológicas e físicas relevantes para o tema da dissertação:**
  1. **Escopo do método Gakushin (Iwashita et al., 2004):** O protocolo Gakushin foi concebido originalmente para **materiais carbonosos grafitizados e pós volumosos** com reflexões `(002)` e `(004)` bem definidas; quando aplicado a flocos ultrafinos de grafeno, GO ou rGO com pouquíssimas camadas, a baixa razão sinal-ruído, sobreposição com bandas amorfas ($\gamma$) e assimetria severa comprometem o ajuste simétrico convencional.
  2. **Limitação da equação de Debye pura (Li et al., 2007):** Modelos atomísticos isolados via Debye não modelam diretamente efeitos macroscópicos de amostra em porta-amostra plano (deslocamento de altura da amostra, absorção, orientação preferencial em filmes depositados por *drop-casting* ou filtração a vácuo) a menos que acoplados a correções geométricas do difratômetro.
  3. **Armadilha de interpretação de ausência do pico `(002)`:** Nem a atenuação nem o desaparecimento do pico `(002)` em um difratograma provam que a amostra é grafeno monocamada; como discutido nas seções de fundamentação física, massa insuficiente do filme, desordem turboestrática extrema ou textura paralela/inadequada ao espalhamento fora do plano também suprimem ou achatam a reflexão `(002)`.

---

## 7. Contribuição para a dissertação

- **Fatos verificados + Análise — Agente B:**
  1. **Base teórica para o módulo de DRX da ferramenta computacional:** Fundamenta a necessidade de o software proposto na dissertação **não** se limitar a um calculador ingênuo de Bragg + Scherrer sobre um único pico `(002)`. Para materiais grafíticos/turboestráticos, é imprescindível suportar: (i) calibração de deslocamento zero / padrão interno (inspirada em Iwashita et al., 2004), (ii) ajuste assimétrico de bandas bidimensionais `(10)`/`(11)` e decomposição de perfis `(002)`, e (iii) alertas explícitos sobre distorções de curvatura e flutuação de $d_{002}$ (Li et al., 2007).
  2. **Critério rigoroso de falsificação física:** Impede que a ferramenta ou o texto da dissertação rotule um espectro sem pico `(002)` como "grafeno monocamada confirmado por DRX", estabelecendo a exigência de técnicas complementares (Raman, TEM, AFM).

---

## 8. Possíveis aplicações

- **Proposições — Agente B (sem extrapolar resultados não lidos):**
  - Implementar no protótipo computacional de DRX um módulo de **verificação de qualidade metrológica** inspirado no protocolo Gakushin (entrada opcional de padrão de Si ou $\text{LaB}_6$ para correção de $2\theta$ e $B_{\text{inst}}$) antes de reportar $d_{002}$, $L_c$ ou $L_a$.
  - Avaliar o uso da **equação de Debye** (ou bibliotecas pré-computadas baseadas em modelos de camadas turboestráticas com rotação/translação aleatória) para gerar padrões sintéticos realistas de grafeno multicamada desordenado, reduzindo o viés de simulações estritamente cristalinas baseadas apenas em célula unitária `ABAB`.

---

## 9. Evidências

- **Nível de leitura declarado:** **Leitura baseada em metadados verificados, resumos oficiais completos e trechos introdutórios/índices públicos (ScienceDirect e OpenAlex)**, sem acesso ao texto integral completo (*closed access*).
- **Evidências verificadas em Li et al. (2007) (`10.1016/j.carbon.2007.03.038`):**
  - *Abstract* completo (verificado): simulação de `h-graphite` e `t-carbon` via equação geral de Debye; métrica NDID; dependência de $2\theta$ e FWHMs frente ao tamanho de cristalito e cinco fatores de distorção (rotação, translação, curvatura, flutuação positiva local de $d$ e flutuação atômica); conclusão de que ângulos de difração e FWHMs não podem ser usados simplesmente para obter parâmetros de rede e tamanhos de cristalito de `t-carbon`.
  - *Introduction* (trecho público ScienceDirect): referência ao regime de grafite nanocristalino ($2\text{–}10\ \text{nm}$) $\to$ `t-carbon` $\to$ amorfo em moagem em moinho de bolas; definição estrutural de `h-graphite` (`AB` ordenado) vs. `t-carbon` (translações/rotações aleatórias em torno da normal); lista de seções (`Structure of turbostratic carbon`, `Results and discussion`, `Sample preparation`, `Experimental XRD patterns and simulation`, `Conclusions`).
- **Evidências verificadas em Iwashita et al. (2004) (`10.1016/j.carbon.2004.02.008` e Corrigendum `10.1016/j.carbon.2004.05.027`):**
  - *Abstract* completo (verificado): norma original de 1963 do 117º Comitê da JSPS ("Gakushin"); revisão iniciada em 2002 para incluir *step-scanning* automático e *profile fitting*; determinação de parâmetros de rede ($a_0, c_0$) e tamanhos de cristalito ($L_a, L_c$).
  - Trecho público do *Corrigendum* (2004): uso do padrão de silício (*silicon standard*) para correção dos ângulos de difração $2\theta$.

---

## 10. Prioridade de estudo

- **Prioridade:** **Alta (com obtenção recomendada dos PDFs integrais via Portal de Periódicos CAPES / UFCA).**
- **Justificativa:** Li et al. (2007) e Iwashita et al. (2004) são as duas referências clássicas mais citadas para fundamentar a física e a metrologia experimental da difração em carbonos grafíticos e turboestráticos. A obtenção do texto completo via acesso institucional da UFCA permitirá extrair as equações exatas de NDID, os gráficos quantitativos de erro na estimativa de $L_c$/$L_a$ e os coeficientes da Tabela 2 do protocolo Gakushin para calibração com silício.
