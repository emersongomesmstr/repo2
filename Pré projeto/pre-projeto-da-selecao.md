**![][image1]**  
**MINISTÉRIO DA EDUCAÇÃO**  
**UNIVERSIDADE FEDERAL DO CARIRI**  
**CENTRO DE CIÊNCIA E TECNOLOGIA**  
**PROGRAMA DE PÓS-GRADUAÇÃO EM CIÊNCIA E ENGENHARIA DE MATERIAIS**

**DESENVOLVIMENTO DE UMA FERRAMENTA COMPUTACIONAL BASEADA EM VISÃO COMPUTACIONAL PARA CARACTERIZAÇÃO AUTOMATIZADA DE MICROESTRUTURAS EM MATERIAIS**

Projeto de Pesquisa apresentado ao Programa de Pós-Graduação em Ciência e Engenharia de Materiais da Universidade Federal do Cariri, como requisito para participação no processo seletivo do curso de Mestrado Acadêmico.

**Candidato**: Emerson de Sousa Gomes  
**Linha de Pesquisa**: Tecnologia dos Materiais

**Brejo Santo**  
**2026**  
**1 INTRODUÇÃO**

O desenvolvimento de novos materiais impulsiona diversos setores tecnológicos, como saúde, energia, eletrônica, construção civil e sustentabilidade. O desempenho de uma macroestrutura vincula-se diretamente às suas características microestruturais, tornando a caracterização uma etapa fundamental na ciência dos materiais, pois as propriedades mecânicas, elétricas e químicas dependem dessa organização interna (CALLISTER; RETHWISCH, 2018).  
Técnicas como microscopia óptica e eletrônica de varredura (MEV) geram grandes volumes de imagens com informações sobre tamanho de grão, porosidade, defeitos e distribuição de fases (PADILHA, 2007). Fazer a análise desses dados manualmente é um processo muito demorado, e ainda sujeito à variabilidade do operador, além de serem de difícil reprodutibilidade.   
Recentemente, técnicas de Processamento Digital de Imagens (GONZALEZ; WOODS, 2018\) e Visão Computacional (SZELISKI, 2022\) possibilitaram automatizar a caracterização microestrutural por meio de algoritmos de segmentação, detecção de bordas e extração de características geométricas, garantindo resultados quantitativos velozes e reprodutíveis, além de auxiliar na classificação de microestruturas e identificação de padrões, produzindo resultados precisos e objetivos (HOLM et al., 2020).  
Além disso, aborda0gens baseadas em aprendizado de máquina têm ampliado a capacidade desses sistemas em reconhecer padrões complexos e auxiliar a classificação automática de microestruturas, reduzindo a influência da subjetividade presente nas análises convencionais (HOLM et al., 2020).  
Embora a visão computacional seja uma abordagem consolidada (DE COST; HOLM), muitas ferramentas disponíveis restringem-se a aplicações específicas, exigem intervenção intensa do usuário ou carecem de flexibilidade. Assim, torna-se necessária a construção de ferramentas que automatizem a caracterização com técnicas modernas, aumentando a eficiência das análises, reduzindo a subjetividade e eleva a reprodutibilidade dos resultados.  
Este trabalho propõe o desenvolvimento de uma ferramenta computacional em código aberto para caracterização automatizada de microestruturas via MEV, utilizando Processamento Digital de Imagens e Visão Computacional para extrair parâmetros de interesse e otimizar o tempo de análise, fornecendo resultados quantitativos confiáveis que possam auxiliar pesquisadores na caracterização de diferentes classes de materiais.

**2 OBJETIVOS**  
**Geral:** Desenvolver uma ferramenta computacional para caracterização automatizada de imagens obtidas por microscopia eletrônica de varredura (MEV) de materiais estudados nos Laboratórios do PPGCEM.   
**Específicos:** 

* Realizar levantamento bibliográfico sobre técnicas de caracterização microestrutural e métodos computacionais empregados na análise automatizada de imagens de materiais.  
* Construir um banco de imagens de microestruturas obtidas por MEV para desenvolvimento e validação da plataforma.  
* Desenvolver algoritmos para pré-processamento, segmentação e detecção automática de regiões de interesse nas micrografias.  
* Implementar rotinas para extração automática de parâmetros microestruturais, como tamanho de grão, área, perímetro, circularidade, porosidade e outras características de interesse.  
* Validar os resultados obtidos pela plataforma por meio da comparação com métodos convencionais de análise utilizados pelo laboratório.  
* Desenvolver uma interface computacional que possibilite a utilização da plataforma por pesquisadores e estudantes.  
* Disponibilizar a plataforma em ambiente de código aberto, favorecendo sua utilização e expansão em pesquisas futuras.

**3 METODOLOGIA**   
	Esta pesquisa se caracteriza como uma pesquisa aplicada, de natureza quantitativa (GERHARDT; SILVEIRA, 2009), uma vez que busca desenvolver uma ferramenta computacional para solucionar um problema prático relacionado à caracterização microestrutural de materiais, sendo the desenvolvimento da mesma, dividido em cinco etapas, conforme descrito a seguir.  
**3.1  Levantamento bibliográfico**  
Inicialmente será realizada uma busca na literatura sobre caracterização microestrutural de materiais, processamento digital de imagens, visão computacional e as aplicações de tais técnicas na Ciência e Engenharia de Materiais. Além disso, também serão estudados trabalhos relacionados ao desenvolvimento de ferramentas computacionais de análise automatizada de imagens obtidas por MEV, com o objetivo de buscar métodos consolidados e também de verificar possíveis limitações existentes.  
**3.2 Obtenção de banco de imagens:**  
	Nessa etapa será construído um banco de imagens que conterá micrografias obtidas por MEV, proveniente dos materiais estudados pelo PPGCEM/UFCA. Essas imagens serão organizadas e catalogadas de acordo com o tipo de material e suas características, o que possibilitará o uso durante o desenvolvimento e também da validação da ferramenta. Quando necessário, serão aplicadas etapas de pre-processamento para padronização das imagens, incluindo remoção de ruídos, ajuste de contraste e também normalização. Caso o volume e diversidade das imagens seja suficiente, poderão ser avaliadas abordagens que têm base em aprendizado de máquina para auxiliar a classificação automática das microestruturas.  
**3.3 \- Desenvolvimento da ferramenta computacional**  
A ferramenta será desenvolvida em Python, utilizando bibliotecas como OpenCV (BRADSKI, 2000\) e Scikit-image (VAN DER WALT et al., 2014). Serão avaliadas diferentes técnicas de segmentação e processamento de imagens, incluindo métodos baseados em limiarização, detecção de bordas, operações morfológicas e segmentação por regiões, sendo selecionadas aquelas que apresentarem melhor desempenho para os materiais estudados. Após a segmentação, rotinas automatizadas extrairão parâmetros geométricos, como área, perímetro e circularidade, organizando os resultados em tabelas e gráficos. A arquitetura modular permitirá futuras adaptações para outros parâmetros compatíveis com o tipo de material analisado, sendo disponibilizada em código aberto.

**3.4 Validação dos resultados**  
A validação será realizada por meio da comparação entre os resultados obtidos pela ferramenta desenvolvida e aqueles obtidos pelos métodos convencionais utilizados pelo laboratório. E nessa etapa serão avaliados critérios como precisão, confiabilidade e reprodutibilidade das análises. Sempre que possível, serão empregadas métricas estatísticas, como erro relativo, coeficiente de correlação e estatísticas descritivas, permitindo quantificar a concordância entre os métodos de análise.

**Cronograma**

| Etapa | 2026.2 | 2027.1 | 2027.2 | 2028.1 |
| :---- | :---- | :---- | :---- | :---- |
| Levantamento bibliografico | **X** | **X** |  |  |
| Revisão da literatura | **X** | **X** |  |  |
| Obtenção e organização do banco de imagens |  | **X** | **X** |  |
| Desenvolvimento da ferramenta computacional |  | **X** | **X** | **X** |
| Implementação de algoritmos de processamento de imagens |  | **X** | **X** |  |
| Testes e validação da ferramenta |  |  | **X** | **X** |
| Análise e discussão dos resultados |  |  | **X** | **X** |
| Redação de artigo científico |  |  | **X** | **X** |
| Redação da dissertação |  |  |  | **X** |
| Defesa da dissertação |  |  |  | **X** |

**Referencias**

CALLISTER, William D.; RETHWISCH, David G. Materials Science and Engineering: An Introduction. 10\. ed. Hoboken: Wiley, 2018\.

HOLM, Elizabeth A. et al. Overview: Computer vision and machine learning for microstructural characterization and analysis. Metallurgical and Materials Transactions A, v. 51, n. 12, p. 5985-5999, 2020\.

GERHARDT. T. E.; SILVEIRA, D. T. (org). Métodos de Pesquisa. Porto Alegre: Editora da UFRGS, 2009\.

PADILHA, Angelo Fernando.Materiais de Engenharia: Microestrutura e Propriedades.  
GONZALEZ, Rafael C.; WOODS, Richard E. Digital Image Processing. 4\. ed. Pearson, 2018\.

SZELISKI, Richard. Computer Vision: Algorithms and Applications. 2\. ed. Springer, 2022\. 

BRADSKI, Gary. The OpenCV Library. Dr. Dobb's Journal of Software Tools, 2000\.

VAN DER WALT, Stefan et al. scikit-image: image processing in Python. PeerJ, 2014\.

DE COST, Brian L.; HOLM, Elizabeth A. A computer vision approach for automated analysis and classification of microstructural image data. Computational Materials Science.  


[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAF0AAABCCAYAAAA18dqNAAAEnElEQVR4Xu2bTWgVVxTHB2nGuHBjwMaXWoQuWkIXGixGKPU9sbbVVGpFFy6iqfGrG9uCSFEwWChFEQJJhdpEN37Q0kJFoSXQYo240KogzcK6EV0J0YUx9GFMpu+M74zn/u+dea9pXlp6zw/+zMyde88df3Nz855oECiKoiiK4h8T19dF2KbUGJU+jURDrUvuXlo6a+TIpkjFTxMkmkLSVfw0wLKldBVfY6RomScXN6j0WhH93txIx2VNzxUKubpEdPHMRpVeC0hyfkFQT0cjTTNX8zmOUf4hLNWSrsJri5D8CK5V+lRBvyTl9cMjmw/jL1HsQ7jalBRGvtzchTJRMGVHy/NWW9Y4cxYlpndwVVvPhVWRDLWjzL8TGu+qqQS2GJQkRW4avOnMg6+2jst+WEdm/7frQ3wG70ApGBRcTbAGBp/BK1wysA2FVkr74M21WAODz+EVKMMVlFpNsAbOhc/hFSin/+Ka2dUIvxs2xMF2DtZ2XXsNi8g31i9gYQSK5Ow4dS6S4H2Uz7XoC5RKL0MS+FulFJa12plKK16Gv7Wq9KCydJd4F9gHo39VUEb+uKN0Ft8xOGS1U4jSsEzp8mVK6V6v9izpcpXTvY5fbhj37xcfx9Ipo6OjhmTXT47cXlR6Kctz4Wm6RuEsnY8ffHHQEEkJyuKxnUWLfsacfO0lJIBXIUrHFyAl8vnGvQdStxfZT873bHZPYZml9KIwlI4iOUHKSpf95fYCj+AfQroli8PC23d/4uwXqPTqkduGSyYmrU+pVLT77AWrHcfKOeFR/CGR3lTXniYUxWGbzM+/HbXa5Fg5Jz6Ll1QSyuLkNf0jo2qvWbpSJt9U11rIhT+hZJm0LUiKTTun4Jzew6sQhcpkSWfB8qjSK0Aym5uDEIWmSUehLFnGNR7n9RoWKj+Tc1D69oHLmbJdUekOsqTLVNvPFZUOVJJ5pmuxsXJ7Tubj9m35RqN939oXrbEqPQOXdGrDrYJzes9Cq43Te/4dZy2c03tc0r/5dJEltJowhvR54Tmc02t4FaJ0lOkKjSV2tS1NZBP4EnFO73FJP/hZS7Tm5YZEoJTJ+XzLe+L+RLIdoXDKWy8Ec3Ber2GJLAjh+3KFH//oVWvVy3QsbjCk84tVyrik3/ruTUukzMcr51ltGJWegZS+Yv7M+Hz82vuWRBle+fcGVlv3KB8um6vSLbb2/8Gny3Nhl1zpKJDT0/FKfGx7qT6WOHbl6Yv5tft1qy/l6K5mlW7Q2ReVcjs+CuTqnKpQ3UR6PO/XV3He/zdPZVvhLYa6oLTJpvv8269xzfjomNcf+eIPTKD4qZBvyC7POVoci+4MP/JQeBleeTO2HYsO/ThkSJis/KSuqBFPVqr78M/HhuyWwrvx/9DzE8eKT5OfSBTkc3UD0Od6IRceiG+K2kZ9JbD2+Rnbj6UKeiM3a758Gc9khz/EHTr7T2C9vd9fc9ZSCJA1PFI0rkXGSp9Aio72JK3dA2abkkFn3zgKxNTvPB4f5ZZBXL49bPXF8kolQCDu+9ZezdnSN4GllMmCcjlK7TE+DirTg0r/l1DpiqIoyn+BvwCYYa892OCPAQAAAABJRU5ErkJggg==>