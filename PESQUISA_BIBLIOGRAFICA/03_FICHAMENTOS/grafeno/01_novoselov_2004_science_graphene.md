# Fichamento 01 — Novoselov et al. (2004), *Science*

> **Distinção metodológica:** As informações das Seções 1 a 5 e os dados citados na Seção 9 provêm diretamente do artigo analisado (**fatos extraídos**). A avaliação crítica das limitações, da relevância para a dissertação e das extrapolações aplicáveis corresponde à **análise crítica do Agente A**.

---

## 1. Identificação Bibliográfica

- **Título:** Electric Field Effect in Atomically Thin Carbon Films
- **Autores:** K. S. Novoselov, A. K. Geim, S. V. Morozov, D. Jiang, Y. Zhang, S. V. Dubonos, I. V. Grigorieva, A. A. Firsov
- **Ano:** 2004 (22 de outubro de 2004)
- **Periódico:** *Science*, v. 306, n. 5696, p. 666–669
- **DOI:** `10.1126/science.1102896`
- **URL oficial:** https://doi.org/10.1126/science.1102896 (versão Open Access Green verificada: https://arxiv.org/pdf/cond-mat/0410550; OpenAlex: https://openalex.org/W2058122340)
- **Status de leitura:** Texto completo extraído em [`Novoselov_2004_Electric_Field_Effect_Atomically_Thin_Carbon_Films.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Novoselov_2004_Electric_Field_Effect_Atomically_Thin_Carbon_Films.md).

---

## 2. Problema Investigado

*(Fatos extraídos do artigo)*  
Os autores investigaram se seria possível isolar filmes cristalinos de carbono com espessura de apenas uma a poucas camadas atômicas (denominados no artigo *few-layer graphene*, FLG, incluindo grafeno monocamada), estáveis em condições ambiente, e demonstrar neles um **efeito de campo elétrico pronunciado** (*all-metallic field-effect transistor*). Até então, presumia-se que o grafeno planar livre fosse termodinamicamente instável em relação a estruturas curvas (fulerenos, nanotubos, fuligem) e que filmes metálicos ultrafinos (< 1 nm, necessários para evitar blindagem eletrostática) fossem descontínuos e incapazes de exibir modulação de condutividade > 1% por tensão de porta (*gate*).

---

## 3. Fundamentação

*(Fatos extraídos do artigo)*  
- **Estrutura e conceito de grafeno:** camada única de átomos de carbono densamente empacotados em anéis benzênicos (rede hexagonal bidimensional), bloco fundamental do grafite 3D, fulerenos e nanotubos.
- **Blindagem elétrica e dopagem por campo:** em metais convencionais, o campo elétrico é blindado em distâncias < 1 nm e a concentração volumétrica de portadores supera a carga induzível por capacitor. Em filmes bidimensionais acoplados a um substrato $\text{SiO}_2/\text{Si}$ (dielétrico de espessura $t = 300\ \text{nm}$), a tensão de porta $V_g$ induz densidade superficial de carga $n = \varepsilon_0 \varepsilon V_g / (te)$ (para $V_g = 100\ \text{V}$, $n \approx 7{,}2 \times 10^{12}\ \text{cm}^{-2}$), deslocando o nível de Fermi $\varepsilon_F$.
- **Modelo de semimetal 2D (formulação inicial de 2004):** os autores modelaram os filmes FLG como um semimetal 2D com pequena superposição de bandas $\delta\varepsilon$ entre condução e valência, utilizando oscilações de Shubnikov-de Haas (ShdH) em campo magnético inclinado ($B\cos\theta$) para comprovar a dimensionalidade 2D e extrair densidade de estados ($D = 2m_e/\pi\hbar^2$) e massas efetivas.

*(Análise crítica — Agente A)*  
Do ponto de vista histórico-físico, este trabalho inaugural ainda interpreta os dados com um modelo parabólico de massa efetiva finita e pequeno *overlap* ($\delta\varepsilon \approx 4\text{–}20\ \text{meV}$), registrando explicitamente a aparente contradição com a dispersão linear teórica sem massa do grafeno monocamada — paradoxo que seria resolvido apenas em 2005 (férmions de Dirac sem massa) e consolidado em Geim & Novoselov (2007).

---

## 4. Metodologia

*(Fatos extraídos do artigo)*  
- **Preparação das amostras:** esfoliação mecânica (descascamento repetido / *repeated peeling*) de pequenas mesas de grafite pirolítico altamente orientado (HOPG), transferindo flocos para substrato de silício oxidado ($n^+\text{-Si}$ com $300\ \text{nm}$ de $\text{SiO}_2$).
- **Localização e caracterização física/morfológica:**
  - **Microscopia óptica** em luz branca para identificar flocos finos sobre $\text{SiO}_2$ ($300\ \text{nm}$); filmes com $d \ge 3\ \text{nm}$ atingiram até $\sim 100\ \mu\text{m}$ sendo visíveis a olho nu, enquanto os filmes FLG mais finos atingiram até $10\ \mu\text{m}$.
  - **Microscopia de Força Atômica (AFM)** para medir altura topográfica dos flocos e degraus dobrados em relação ao $\text{SiO}_2$.
  - **Microscopia Eletrônica de Varredura (MEV/SEM)** para inspeção da geometria dos dispositivos fabricados em barra de Hall multiterminal.
- **Caracterização de transporte elétrico:** mais de 60 dispositivos com $d < 10\ \text{nm}$ foram processados em barras de Hall, medindo resistividade longitudinal $\rho_{xx}$, coeficiente Hall $R_H$ e resistividade Hall $\rho_{xy}$ em função de $V_g$, temperatura ($T = 5\text{–}300\ \text{K}$, inclusive $3\text{–}4\ \text{K}$) e campo magnético ($B$ até $10\ \text{T}$). Também foram testados recozimento em vácuo e exposição a vapor d'água ($p$-dopagem) e $\text{NH}_3$ ($n$-dopagem).

---

## 5. Resultados

*(Fatos extraídos do artigo)*  
1. **Estabilidade e morfologia observada (Fig. 1):** filmes monocristalinos de 1, 2 ou 3 camadas atômicas mostraram-se contínuos e estáveis ao ambiente. Na **Fig. 1C** (AFM de monocamada sobre $\text{SiO}_2$), a área central sobre o substrato registrou altura aparente de **$0{,}8\ \text{nm}$** (além de regiões de $1{,}2\ \text{nm}$ e $2{,}5\ \text{nm}$), enquanto uma dobra interna da própria folha apresentou **altura diferencial de $\approx 0{,}4\ \text{nm}$**.
2. **Efeito de campo ambipolar (Fig. 2):** $\rho(V_g)$ apresenta pico agudo de vários $\text{k}\Omega$ caindo para $\approx 100\ \Omega$ em altos $|V_g|$, sem região de condutância nula (*zero-gap*); $\sigma = 1/\rho$ cresce linearmente com $V_g$ para elétrons e lacunas, enquanto $R_H$ inverte de sinal no pico de $\rho$. Foram induzidas concentrações de até $\sim 10^{13}\ \text{cm}^{-2}$ (máximo experimental $\approx 3 \times 10^{13}\ \text{cm}^{-2}$).
3. **Mobilidade e transporte balístico:** mobilidades $\mu$ entre **$3.000$ e $10.000\ \text{cm}^2/\text{V}\cdot\text{s}$** nos filmes FLG (quase independentes de $T$, limitadas por defeitos), implicando livre caminho médio $\approx 0{,}4\ \mu\text{m}$ (e até $\approx 15.000\ \text{cm}^2/\text{V}\cdot\text{s}$ a $300\ \text{K}$ / $60.000\ \text{cm}^2/\text{V}\cdot\text{s}$ a $4\ \text{K}$ em grafeno multicamada). Densidade de corrente sustentável $> 10^8\ \text{A/cm}^2$ e razão liga/desliga $< 30$ a $300\ \text{K}$.
4. **Provas de bidimensionalidade (Fig. 3):** oscilações de ShdH dependeram apenas de $B\cos\theta$, com frequência $B_F \propto V_g$ (comprovando densidade de estados 2D constante $\varepsilon_F \propto n$, distinta do comportamento 3D $\varepsilon_F \propto n^{2/3}$). A superposição de bandas $\delta\varepsilon$ nos FLGs variou de $4$ a $20\ \text{meV}$, bem abaixo dos $\approx 40\ \text{meV}$ do grafite 3D, decrescendo com a redução do número de camadas.

---

## 6. Limitações

*(Fatos extraídos do artigo)*  
- Os autores reconhecem baixa razão liga/desliga ($< 30$ a $300\ \text{K}$) para transistores lógicos devido à ausência de *band gap* e aos portadores termicamente excitados.
- Reconhecem que o modelo simples de elétrons livres com massa efetiva finita ($m_e \approx 0{,}06\,m_0$; lacunas $0{,}03\,m_0$ e $0{,}1\,m_0$) não explicava plenamente a dispersão linear com portadores de massa zero teoricamente esperada para monocamada (e atribuem $\delta\varepsilon$ finito em parte à dopagem inomogênea ou à mistura de dispositivos de 1 a 3 camadas).
- Adsorção de gases ambientais (como vapor de água) desloca o ponto de neutralidade de $V_g = 0$ para tensões positivas ($p$-dopagem não intencional), exigindo recozimento em vácuo.

*(Análise crítica — Agente A)*  
- **Lacuna metrológica crucial para o nosso projeto:** a **Fig. 1C** já expõe empiricamente o problema central da caracterização por AFM: a altura medida da monocamada diretamente sobre $\text{SiO}_2$ foi **$0{,}8\ \text{nm}$**, mais que o dobro da altura diferencial de dobra grafeno-sobre-grafeno (**$\approx 0{,}4\ \text{nm}$**), antecipando o viés químico/adsorvato que mais tarde seria sistematizado por Nemes-Incze et al. (2008) e Shearer et al. (2016).
- **Ausência de métricas de dispersão em massa:** o método de esfoliação mecânica por fita gera pouquíssimos flocos isolados ($\le 10\ \mu\text{m}$), muito distante da polidispersidade de flocos obtida por esfoliação eletroquímica em solução na UFCA.
- **MEV apenas ilustrativo:** o MEV (Fig. 1D) foi usado exclusivamente para visualizar o dispositivo litografado, sem qualquer tentativa de inferir espessura ou número de camadas a partir da micrografia eletrônica.

---

## 7. Contribuição para a Dissertação

*(Análise crítica — Agente A)*  
1. Estabelece o marco físico e experimental da estabilidade do grafeno 2D em condições ambiente e da dependência crítica das propriedades eletrônicas em função de $N = 1, 2, 3$ camadas vs. multicamadas/grafite 3D ($\delta\varepsilon$, mobilidade, comportamento 2D vs. 2D+3D).
2. Fornece a primeira evidência experimental publicada na literatura (Fig. 1C) de que **altura AFM substrato–floco ($\sim 0{,}8\ \text{nm}$) difere da espessura interplanar intrínseca ($\sim 0{,}4\ \text{nm}$)**, justificando por que qualquer ferramenta computacional para AFM não pode converter altura bruta por divisão simples por $0{,}335\ \text{nm}$.
3. Fundamenta a distinção física entre **grafeno poucas camadas (FLG)** e **grafite multicamada** ($d \ge 3\ \text{nm}$ / $\ge 10$ camadas), orientando a taxonomia de classes aceitáveis no projeto PPGCEM/UFCA.

---

## 8. Possíveis Aplicações

*(Análise crítica — Agente A — distinção rigorosa de extrapolações)*  
- **Não confundir com resultado do artigo:** Novoselov et al. (2004) não propuseram automação por visão computacional nem analisaram DRX.
- **Extrapolação metodológica para a dissertação:** o uso de **degraus diferenciais internos** (floco dobrado sobre floco ou terraços em flocos parcialmente esfoliados, como na Fig. 1C) em algoritmos automáticos de análise de perfis/histogramas de AFM é uma estratégia fisicamente defensável para contornar o erro sistemático da interface grafeno–substrato (desde que validada com amostras reais e técnica complementar).

---

## 9. Evidências

- **Declaração de leitura:** **Análise realizada a partir do texto completo** ([`Novoselov_2004_Electric_Field_Effect_Atomically_Thin_Carbon_Films.md`](file:///C:/Users/emer/dissertacao/Artigos/PESQUISA_BIBLIOGRAFICA/_scratch/textos_extraidos/Novoselov_2004_Electric_Field_Effect_Atomically_Thin_Carbon_Films.md), 109 linhas / páginas internas 1–3 do manuscrito correspondente à publicação *Science* v. 306, p. 666–669).
- **Evidências localizadas:**
  - **Texto principal, p. 1 (linhas 17–21):** preparação por esfoliação mecânica de HOPG em $\text{SiO}_2/\text{Si}$ ($300\ \text{nm}$), flocos FLG até $10\ \mu\text{m}$, mais de 60 dispositivos com $d < 10\ \text{nm}$, foco em dispositivos de 1, 2 ou 3 camadas.
  - **Texto principal, p. 2 (linhas 25–35):** cálculo de $n(V_g)$, efeito de adsorção de $\text{H}_2\text{O}/\text{NH}_3$, mobilidades de $3.000\text{–}10.000\ \text{cm}^2/\text{V}\cdot\text{s}$ e oscilações ShdH.
  - **Texto principal, p. 3 (linhas 37–39):** estimativa de $\delta\varepsilon = 4\text{–}20\ \text{meV}$ em FLG vs. $\approx 40\ \text{meV}$ em grafite 3D.
  - **Figura 1 (linha 94):** imagens óptica (1A, $\approx 3\ \text{nm}$), AFM (1B, 1C com monocamada a $0{,}8\ \text{nm}$ e dobra a $\approx 0{,}4\ \text{nm}$) e MEV (1D, dispositivo FLG).
  - **Figuras 2 e 3 (linhas 101, 108):** curvas $\rho(V_g)$, $\sigma(V_g)$, $R_H(V_g)$ e $B_F \propto V_g$.

---

## 10. Prioridade de Estudo

- **Prioridade:** **Alta**
- **Justificativa:** Referência seminal fundacional do campo (67.486 citações no OpenAlex); essencial para contextualizar a definição física de grafeno monocamada e poucas camadas no Seminário I e demonstrar, já desde o artigo original de 2004, a discrepância entre altura aparente de AFM sobre $\text{SiO}_2$ ($0{,}8\ \text{nm}$) e espessura de dobra ($\approx 0{,}4\ \text{nm}$).
