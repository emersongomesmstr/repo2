# Fichamento 05 — Yao et al. (2017), Nečas & Klapetek (2012 / Gwyddion) e Protocolo VAMAS NPL AS 103 (2022/2023): Nivelamento, Histograma de Altura, Rugosidade e Padronização Metrológica de Grafeno em AFM

> **Nível de leitura declarado (Seção 7 do `PROMPT_MESTRE.md`):**
> - **Despotelis *et al.* — Protocolo VAMAS / NPL Report AS 103 (2022/2023):** **TEXTO COMPLETO LIDO E AUDITADO** diretamente do PDF local (`NPL_VAMAS_2023_Graphene_Flakes_Lateral_Size_Thickness_SEM_AFM.pdf`, 24 páginas numeradas / 30 páginas no arquivo, Figs. 1–17, foco detalhado na Seção 5 "AFM Analysis", pp. 13–23).
> - **Yao *et al.* (2017):** **Resumo completo, todas as 3 tabelas quantitativas (Tabelas 1–3), legendas das 5 figuras (Figs. 1–5) e 26 referências verificados diretamente na página oficial da JMST** (`jmst.org/EN/abstract/abstract26022.shtml`); o corpo textual integral (Introdução/Métodos/Discussão) encontra-se sob assinatura e não foi lido diretamente.
> - **Nečas & Klapetek (2012):** **Resumo e metadados verificados** (Crossref, OpenAlex, MUNI, Springer) complementados por **documentação técnica oficial dos autores** (apresentação de D. Nečas, CEITEC/2017, e *Gwyddion User Guide* em `gwyddion.net`); o PDF de acesso aberto do artigo de 2012 em `is.muni.cz` falhou na extração automática, de modo que todas as funcionalidades atribuídas ao artigo restringem-se ao resumo e documentação oficial verificada.

---

## 1. Identificação bibliográfica

### Artigo 1 — Método do Histograma e Efeito do Nivelamento (Yao *et al.*, 2017)
- **Título:** Histogram method for reliable thickness measurements of graphene films using atomic force microscopy (AFM)
- **Autores:** Yaxuan Yao, Lingling Ren, Sitian Gao, Shi Li
- **Ano:** 2017 (aceito em julho de 2016 — registrado como 2016 no OpenAlex pelo DOI; publicado online em 20/08/2017 e na edição impressa em 31/10/2017)
- **Periódico:** *Journal of Materials Science & Technology* (*J. Mater. Sci. Technol.*), Vol. 33, Nº 8, pp. 815–820
- **DOI:** `10.1016/j.jmst.2016.07.020`
- **Links oficiais verificados:** [Página oficial JMST](https://www.jmst.org/EN/abstract/abstract26022.shtml) | [DOI](https://doi.org/10.1016/j.jmst.2016.07.020)

### Artigo 2 — Software Open-Source Gwyddion (Nečas & Klapetek, 2012)
- **Título:** Gwyddion: an open-source software for SPM data analysis
- **Autores:** David Nečas, Petr Klapetek
- **Ano:** 2012 (publicação online em 16/11/2011 — registrada como 2011 no OpenAlex; fascículo impresso de fevereiro de 2012)
- **Periódico:** *Central European Journal of Physics* (posteriormente renomeada para *Open Physics*), Vol. 10, Nº 1, pp. 181–188
- **DOI:** `10.2478/s11534-011-0096-2`
- **Links oficiais verificados:** [DOI / De Gruyter](https://doi.org/10.2478/s11534-011-0096-2) | [Repositório MUNI](https://www.muni.cz/en/research/publications/966983) | [Portal oficial Gwyddion](https://gwyddion.net/)

### Protocolo Metrológico 3 — VAMAS TWA 41 / NPL Report AS 103 (Despotelis *et al.*, 2022/2023)
- **Título:** VAMAS TWA 41 - Graphene and related 2D materials project 12 - Distribution of lateral size and thickness of few-layer graphene flakes using SEM and AFM. SEM and AFM measurement protocol
- **Autores:** Konstantinos Despotelis, Andrew J. Pollard, Charles A. Clifford, Keith R. Paton
- **Ano:** 2022 (relatório datado de novembro de 2022; indexado no OpenAlex/DOI em 2023)
- **Publicação:** *NPL Report AS 103*, National Physical Laboratory (Teddington, UK), 24 páginas numeradas (EMPIR 19NRM04 ISO-G-SCoPe; ISSN `1754-2928`)
- **DOI:** `10.47120/npl.AS103`
- **Link oficial verificado:** [DOI / NPL](https://doi.org/10.47120/npl.AS103)

---

## 2. Problema investigado

- **Yao *et al.* (2017) [extraído do resumo oficial JMST]:** A medição de espessura de grafeno por perfis lineares simples em AFM sofre elevada variabilidade devido à rugosidade intrínseca da amostra/substrato, às escolhas subjetivas do operador na posição da linha de corte, à ordem de nivelamento (*flatten*) aplicada no pós-processamento e a parâmetros de aquisição (*amplitude setpoint* e *drive amplitude*). Como obter medidas estatisticamente confiáveis e reprodutíveis de espessura de grafeno por AFM?
- **Nečas & Klapetek (2012) [extraído do resumo oficial + apresentação oficial]:** Suprir a falta de um software transparente, gratuito, multiplataforma, modular e auditável em código aberto para processamento, nivelamento, análise de grãos/máscaras e metrologia com rastreabilidade de incertezas em dados de Microscopia de Varredura por Sonda (SPM/AFM), superando limitações de pacotes proprietários fechados.
- **Protocolo VAMAS / NPL AS 103 (2022/2023) [extraído integralmente, Seções 1 e 5]:** Padronizar um procedimento interlaboratorial internacional (dando suporte à revisão futura da norma **ISO/TS 21356-1**) para correlacionar distribuições de tamanho lateral (via MEV em $\ge 200$ flocos) com medições de tamanho lateral e espessura de nanoplaquetas de grafeno (GNPs) individuais por AFM ($\ge 20$ flocos), controlando calibração, seleção amostral, artefatos, nivelamento, rugosidade do substrato e estimativa de incerteza entre laboratórios.

---

## 3. Fundamentação

1. **Método do Histograma vs. Perfil Linear Único (Yao *et al.*, 2017):** Enquanto uma linha de perfil 1D amostra apenas dezenas/centenas de pixels (sensíveis a ruído de varredura, picos locais e inclinação residual), o **histograma de alturas** sobre regiões amplas do grafeno ($A_A$) e do substrato adjacente ($A_B$) estima os centros estatísticos de duas distribuições aproximadamente gaussianas (ou modas bem definidas), reduzindo a variância aleatória e fornecendo desvio padrão associado à rugosidade combinada.
2. **Distorção por Ordem de Nivelamento (*Flatten / Plane Level*, Yao *et al.*, 2017 & NPL AS 103):**
   - Imagens brutas de AFM contêm **inclinação de plano (*tilt*)** decorrente da montagem mecânica da amostra e **curvatura (*bow*)** do tubo/estágio piezoelétrico, além de deslocamentos entre linhas de varredura (*scan-line offsets / scars*).
   - Um ajuste polinomial de ordem excessiva (ex.: 3ª ordem) ou aplicado **sem mascarar os flocos de grafeno** tenta ajustar o polinômio atravessando tanto o substrato quanto o degrau elevado do floco, "dobrando" o fundo ao redor da borda e colapsando ou até **invertendo o sinal** da altura aparente!
3. **Arquitetura Metrológica e Processamento sob Máscaras (Nečas & Klapetek, 2012 + doc. oficial):** No Gwyddion, campos de altura (`GwyDataField`) suportam **máscaras arbitrárias** (`GwyMask`) que restringem nivelamentos (plano médio, plano por facetas dominantes, ajuste polinomial, alinhamento de linhas), cálculo de rugosidade ($R_a$, $R_q$), funções estatísticas (ACF, HHCF, PSDF) e análise de partículas/grãos (limiarização de Otsu, *watershed*) exclusivamente às regiões válidas, além de propagação de incertezas locais de calibração.
4. **Protocolo Correlativo MEV–AFM e Controle de Contaminação (NPL AS 103):** O relatório demonstra uma restrição experimental crítica: **não se deve medir no AFM o mesmo substrato previamente imageado no MEV**, pois o feixe de elétrons deposita contaminação carbonácea sobre os flocos e o substrato, alterando a espessura aparente; por isso, o protocolo separa substratos idênticos em lote ($\text{Si}$ com óxido nativo fino para MEV vs. $\text{SiO}_2/\text{Si}$ de $300 \pm 5\text{ nm}$ para contraste óptico e AFM) e correlaciona distribuições estatísticas.

---

## 4. Metodologia

### A. Yao *et al.* (2017) [extraído do resumo, Tabelas 1–3 e legendas das Figs. 1–5]
- **Amostras:** Filmes de grafeno de 1L, 2L e 4L previamente confirmados por espectroscopia Raman (razões de área G/2D iguais a $0{,}20$, $0{,}44$ e $0{,}63$, respectivamente, Fig. 1).
- **Aquisição multimodal e parâmetros variados:** Registro simultâneo de mapas topográficos, erro de amplitude e fase (Figs. 2, 4 e 5). Estudo sistemático variando: (i) ordem de *flatten* ($0\text{ª}, 1\text{ª}, 2\text{ª}, 3\text{ª}$, Tabela 1); (ii) *amplitude setpoint* ($60, 80, 100, 120\text{ mV}$, Tabela 2); e (iii) *drive amplitude* ($60, 80, 100, 120, 140, 160\text{ mV}$, Tabela 3).
- **Extração de espessura:** Histograma de alturas comparando a área sobre o grafeno ($A_A$) e a área sobre o substrato ($A_B$), com obtenção de espessura incremental intercamadas pela diferença entre 1L, 2L e 4L.

### B. Nečas & Klapetek (2012) [extraído do resumo + documentação oficial Gwyddion]
- **Arquitetura em 3 camadas:** (1) Bibliotecas centrais em C sobre GLib/GObject/GTK+ (`libgwyddion`, `libgwyprocess`, `libgwydgets`, `libgwyfile` etc.); (2) aplicativo leve unificador; (3) módulos carregáveis em tempo de execução (>120–140 módulos de leitura de formatos proprietários de fabricantes de AFM, processamento, ferramentas interativas e `pygwy` para automação via *scripts* Python).
- **Fluxo algorítmico padrão para materiais 2D/partículas:** Abertura de dados brutos $\rightarrow$ correção de inclinação/arco (*Plane Level*, *Facet Level*, *Polynomial Background*, *Flatten Base*) e correção de linhas (*Align Rows*, remoção de *scars*) usando máscaras de exclusão $\rightarrow$ marcação de grãos/flocos (limiarização de altura/Otsu) $\rightarrow$ leitura de distribuições estatísticas 1D/2D, rugosidade ($R_q$/RMS, $R_a$), erosão/dilatação e reconstrução cega de ponta (algoritmos de Villarrubia).

### C. Protocolo VAMAS / NPL AS 103 (2022/2023) [extraído integralmente, Seção 5, pp. 13–23]
- **Preparação e calibração:** Substrato de $\text{SiO}_2/\text{Si}$ ($300 \pm 5\text{ nm}$ de óxido) com grade central de calibração ISO-G-SCoPe e quadrículas numeradas; inspeção óptica prévia ($50\times$/$20\times$) evitando regiões com resíduos de solvente (Figs. 3–4); calibração do eixo Z piezoelétrico *in-house* e aquisição de 3 varreduras ($10 \times 10\text{ }\mu\text{m}$) na grade central ao final para medir *pitch* em X/Y (média de 10 feições ou FFT) e degrau Z por **histograma bimodal de alturas** (Fig. 12).
- **Parâmetros de aquisição AFM (Seção 5.2):** Modo de contato intermitente (*tapping* ou *PeakForce Tapping*) ao ar em **malha fechada (*closed loop*)**; cantilever típico $k \sim 40\text{ N/m}$, $f_0 \sim 240\text{ kHz}$, raio de ponta $5\text{--}15\text{ nm}$, frequência deslocada em $5\%$ da FWHM do pico de ressonância; ângulo de varredura rápida perpendicular ($90^\circ$) ao eixo do cantilever; velocidade de linha $< 10\text{ }\mu\text{m/s}$; engajamento inicial a $\sim 80\%$ da amplitude livre mínima estável e varredura com *setpoint* $\le 70\%$ (reduzível sobre o floco para testar convergência de altura menor e mais acurada, mas **evitando $< 40\%$** para não danificar o ápice da ponta).
- **Estratégia amostral hierárquica (Seção 5.2.2):** Varredura ampla ($20 \times 20\text{ }\mu\text{m}$, $256 \times 256$ px) $\rightarrow$ seleção de $\ge 20$ flocos primários isolados e planos cobrindo toda a faixa de tamanhos laterais vista no MEV (ex.: $100\text{ nm}$ a $10\text{ }\mu\text{m}$, evitando viés para flocos grandes) $\rightarrow$ varreduras de alta resolução em $(0{,}5\text{ }\mu\text{m})^2$ a $(2\text{ }\mu\text{m})^2$ com **$\ge 512 \times 512$ pixels**, salvando **exclusivamente arquivos brutos sem processamento**.
- **Critérios de exclusão e análise de dados (Seção 5.3.2):**
  - Rejeitar categoricamente imagens com artefatos de **ponta dupla** (*double-tip*, Fig. 13a), **deriva / "flying tip"** gerando linhas de varredura defeituosas (Fig. 13b), aglomerados, sobreposições, dobras ou resíduos (Fig. 15).
  - Usar preferencialmente o canal do **sensor Z** (*Z-axis sensor*) ou, na falta deste, o canal *Height*.
  - Aplicar apenas correção de plano global de **1ª ordem** (ou no máximo **2ª ordem se houver *bow* significativo, preferencialmente mascarando/excluindo os flocos do ajuste**).
  - **Medição de espessura:** Traçar **3 perfis igualmente espaçados na direção de varredura rápida (*fast scan*)** evitando picos locais (Fig. 16); ajustar segmentos retos médios no substrato adjacente e no platô plano do floco (reportando o menor valor se houver duas alturas distintas nas bordas); incerteza = desvio padrão das 3 leituras. Calcular e reportar também a **rugosidade RMS ($R_q$) do substrato** para cada imagem.
  - **Medição de tamanho lateral:** Medir comprimento (maior eixo do retângulo/elipse mínima) e largura (bissetriz perpendicular dentro do floco; ou diâmetro mínimo de Feret se forma ambígua), tomando a **média entre o valor máximo (base do degrau) e o mínimo (topo do platô)** no perfil (Fig. 14c) para compensar a inclinação/convolução das paredes laterais; reportar tamanho lateral médio e construir gráfico Espessura $\times$ Tamanho Lateral ($N \ge 20$, ajuste linear com banda de confiança de $95\%$ e $R^2$, Fig. 17).

---

## 5. Resultados

1. **Yao *et al.* (2017) [extraído literalmente do resumo e das Tabelas 1–3]:**
   - **Impacto crítico da ordem de *flatten* (Tabela 1, grafeno 1L):** ordem $0\text{ª} \rightarrow 4{,}01\text{ nm}$; $1\text{ª} \rightarrow 1{,}63\text{ nm}$; $2\text{ª} \rightarrow 1{,}52\text{ nm}$; $3\text{ª} \rightarrow \mathbf{-0{,}32\text{ nm}}$ (inversão espúria completa do degrau!).
   - **Impacto do *amplitude setpoint* (Tabela 2, 1L):** $60\text{ mV} \rightarrow 1{,}23\text{ nm}$; $80\text{ mV} \rightarrow 1{,}37\text{ nm}$; $100\text{ mV} \rightarrow 1{,}52\text{ nm}$; $120\text{ mV} \rightarrow 1{,}51\text{ nm}$ (mostrando redução sistemática de espessura aparente ao comprimir mais com menor *setpoint*).
   - **Impacto da *drive amplitude* (Tabela 3, 1L):** $60\text{ mV} \rightarrow 3{,}89\text{ nm}$ (anomalia severa em baixa excitação!); $80\text{ mV} \rightarrow 1{,}37\text{ nm}$; $100\text{ mV} \rightarrow 1{,}52\text{ nm}$; $120\text{ mV} \rightarrow 1{,}59\text{ nm}$; $140\text{ mV} \rightarrow 1{,}48\text{ nm}$; $160\text{ mV} \rightarrow 3{,}07\text{ nm}$ (nova instabilidade em excitação muito elevada!).
   - **Medição confiável por histograma em condição otimizada ($100\text{ mV}$ / $100\text{ mV}$):** $h_{\text{1L}} = \mathbf{1{,}51 \pm 0{,}16\text{ nm}}$, $h_{\text{2L}} = \mathbf{1{,}92 \pm 0{,}13\text{ nm}}$, $h_{\text{4L}} = \mathbf{2{,}73 \pm 0{,}10\text{ nm}}$. Por regressão/diferença entre esses valores ($h_{\text{2L}}-h_{\text{1L}} = 0{,}41\text{ nm}$; $(h_{\text{4L}}-h_{\text{1L}})/3 \approx 0{,}407\text{ nm}$), **a espessura da monocamada é determinada com precisão em $0{,}41 \pm 0{,}09\text{ nm}$**.
2. **Nečas & Klapetek (2012) [resumo + doc. oficial]:** Consolidou o Gwyddion como padrão aberto mundial em SPM (mais de $4.600$ citações no OpenAlex / $>3.000$ no Crossref), demonstrando que bibliotecas modulares abertas permitem algoritmos auditáveis de nivelamento mascarado, análise estatística, erosão de ponta e cálculo de incertezas metrológicas.
3. **Protocolo VAMAS / NPL AS 103 (2022/2023) [texto completo]:** Entregou protocolo harmonizado completo (com planilhas padronizadas de reporte ambiental, calibração, rugosidade RMS do substrato, incertezas por partícula e correlação tamanho–espessura) adotado para avaliação interlaboratorial global visando validar as seções informativas da norma ISO/TS 21356-1.

---

## 6. Limitações

**[Análise crítica do Agente D combinando os três documentos]**  

1. **Yao *et al.* (2017):** Mesmo com o método do histograma em parâmetros estáveis ($100\text{ mV}/100\text{ mV}$), a altura absoluta 1L–substrato permaneceu em $1{,}51 \pm 0{,}16\text{ nm}$ (quase $4{,}5\times$ o valor de $0{,}335\text{ nm}$), demonstrando que o histograma reduz a variância aleatória da rugosidade e da escolha de linhas, mas **não elimina o *offset* físico da interface grafeno–substrato**; é necessário medir múltiplos degraus/camadas (1L, 2L, 4L) para extrair o passo diferencial de $0{,}41 \pm 0{,}09\text{ nm}$. Ademais, os parâmetros na tabela foram expressos em $\text{mV}$ instrumentais sem conversão calibrada para $\text{nm}$ de amplitude livre ou $\text{nN}$, dificultando comparação quantitativa direta com outros microscópios. *(Nota de leitura: como não acessamos o corpo integral Elsevier, detalhes do modelo do microscópio, substrato e algoritmo exato de ajuste de pico do histograma ficam pendentes).*
2. **Nečas & Klapetek (2012):** O *script* nativo `pygwy` historicamente baseia-se em Python 2 (fato explicitamente documentado nos slides de D. Nečas, 2017, slide 28, embora o projeto mantenha atualizações contínuas), criando atrito de integração direta com ecossistemas modernos de *deep learning* em Python 3 (PyTorch/TensorFlow) — exigindo exportação de matrizes brutas ou conversão via bibliotecas externas (ou uso de ferramentas como `gwyfile` em Python 3).
3. **Protocolo VAMAS / NPL AS 103 (2022/2023):**
   - O protocolo ainda depende fortemente de **inspeção e seleção manual** (triagem visual de artefatos *double-tip*/linhas, desenho manual de 3 perfis retos e marcação de base/platô para comprimento e largura em $\ge 20$ flocos), tornando o fluxo lento e sujeito a variação residual entre operadores.
   - Curiosamente, embora o NPL AS 103 utilize o **histograma de alturas** na calibração do degrau da grade de referência (Fig. 12c), ele ainda prescreve **3 perfis de linha manuais** ao longo da direção rápida (*fast scan*) para os flocos individuais (Fig. 16), abrindo espaço científico direto para automatizar o cálculo por máscaras segmentadas + histograma local mascarado como em Yao *et al.* (2017)!
   - Exclui explicitamente flocos dobrados, empilhados ou com resíduos (Fig. 15) — o que funciona para controle metrológico de referência, mas pode subestimar a fração aglomerada em pós comerciais ou dispersões de grafeno esfoliado eletroquimicamente.

---

## 7. Contribuição para a dissertação

**[Análise do Agente D para o projeto PPGCEM/UFCA]**  

Este conjunto forma a **espinha dorsal algorítmica e metrológica** do módulo de AFM da dissertação:
- **Regras obrigatórias de pré-processamento computacional:**
  1. Trabalhar sobre **dados brutos de altura (preferencialmente canal *Z-sensor*)**, nunca sobre capturas de tela em PNG/RGB com escala de cor já nivelada arbitrariamente.
  2. Executar **nivelamento de 1ª ordem (ou 2ª ordem estritamente com máscara de exclusão dos flocos)** e **alinhamento de linhas (*row alignment*) mascarado**, bloqueando *flatten* polinomial de 3ª ordem sem máscara (que Yao *et al.* provaram poder inverter o degrau para $-0{,}32\text{ nm}$!).
  3. Usar **direção de varredura rápida (*fast scan*)** para perfis de degrau (reduzindo efeito de *drift* térmico lento entre linhas, conforme NPL AS 103) ou, preferencialmente, **método do histograma bimodal mascarado** (região do platô vs. anel de substrato adjacente) com ajuste de duas gaussianas para extrair $\Delta h \pm \sigma_{\Delta h}$ e a rugosidade $R_q$ do substrato local.
  4. Medir dimensões laterais descontando a rampa de convolução da ponta por **interpolação meia-altura / média base–platô** (Fig. 14c do NPL AS 103).

---

## 8. Possíveis aplicações

**[Análise do Agente D — arquitetura concreta de software científico]**  

- **Pipeline determinístico auditável (sem caixa-preta) como *baseline* e gerador de rótulos físicos:** Antes de treinar qualquer rede neural, pode-se construir em Python um módulo reprodutível inspirado em Gwyddion + Yao (2017) + NPL AS 103 que execute: (1) detecção automática de *outliers*/linhas defeituosas (*scars*) e teste de assimetria de bordas; (2) nivelamento iterativo em dois estágios (segmentação grosseira $\rightarrow$ máscara de exclusão $\rightarrow$ ajuste de plano 1ª/2ª ordem no substrato); (3) cálculo da rugosidade $R_q$ e $R_a$ do substrato; (4) extração de altura e incerteza de cada floco via **histograma local bimodal** comparado aos **3 perfis *fast-scan*** do protocolo VAMAS; e (5) reporte padronizado em tabela compatível com ISO/TS 21356-1 (tamanho lateral, espessura, incerteza e correlação $R^2$).

---

## 9. Evidências

- **Yao *et al.* (2017):** Resumo, Tabelas 1–3 e legendas das Figs. 1–5 verificadas em `jmst.org/EN/abstract/abstract26022.shtml` (DOI `10.1016/j.jmst.2016.07.020`) — dados de *flatten* (4,01; 1,63; 1,52; −0,32 nm), *setpoint* (1,23–1,52 nm), *drive amplitude* (3,89; 1,37; 1,52; 1,59; 1,48; 3,07 nm) e espessuras por histograma ($1{,}51 \pm 0{,}16$; $1{,}92 \pm 0{,}13$; $2{,}73 \pm 0{,}10$; passo 1L $= 0{,}41 \pm 0{,}09\text{ nm}$).
- **Nečas & Klapetek (2012):** Resumo e metadados verificados (Crossref `10.2478/s11534-011-0096-2`; MUNI `966983`) + apresentação oficial *Open source software Gwyddion for SPM data analysis* (D. Nečas, 2017, slides 1–33) e *Gwyddion User Guide* (Cap. 1 e Cap. 4, p. 161 sobre incertezas locais).
- **NPL Report AS 103 (2022/2023):** PDF completo lido (`10.47120/npl.AS103`): Seção 2 (pp. 1–2, separação substrato SEM vs. AFM), Seção 4.1 (p. 6, contaminação carbonácea pelo feixe MEV), Seção 5.1–5.4 (pp. 13–23), Figs. 8–17 (grade de calibração e histograma bimodal na Fig. 12; *double-tip* e linhas na Fig. 13; tamanho lateral mínimo/máximo na Fig. 14; critérios de aceitação de flocos na Fig. 15; 3 perfis *fast-scan* na Fig. 16; gráfico correlação espessura $\times$ tamanho lateral na Fig. 17).

---

## 10. Prioridade de estudo

**Alta (Indispensável para implementação).** Enquanto Nemes-Incze (2008) e Shearer (2016) ensinam **como adquirir** dados confiáveis no microscópio, o trio **Yao (2017) + Gwyddion (2012) + Protocolo VAMAS NPL AS 103 (2022/2023)** define exatamente **como processar, nivelar, filtrar artefatos e quantificar** mapas reais de AFM com rigor metrológico.
