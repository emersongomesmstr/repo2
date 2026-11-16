---
name: auditoria-grafeno-materiais
description: >
  Checklist de rigor físico, metodológico e normativo para a dissertação e
  apresentação de Seminários I (PPGCEM/UFCA) sobre caracterização de grafeno
  por DRX, MEV, AFM, PDI e ML/VC.
---

# Skill Local: Auditoria de Rigor em Grafeno e Seminários I (PPGCEM/UFCA)

## Travas de Rigor Físico (Obrigatórias)
1. **Status do software:** a ferramenta computacional **não está desenvolvida nem validada**; o projeto está em fase investigativa de viabilidade.
2. **Não-intercambiabilidade de DRX, MEV e AFM:**
   - **DRX:** média volumétrica cristalográfica ($d_{002}$, $L_c$); monocamada isolada não gera pico `(002)` 3D.
   - **MEV:** morfologia lateral e contraste dependente de tensão (kV), substrato e carregamento; não quantifica espessura atômica absoluta sozinha.
   - **AFM:** perfil topográfico local sujeito a convolução geométrica de ponta e superestimação de altura aparente por camada de hidratação/adsorvato (ex.: Shearer et al., 2016, `10.1088/0957-4484/27/12/125704`).
   - **Técnicas complementares:** citar explicitamente o papel de **Raman** ($I_D/I_G$, banda $2D$), **MET (TEM)** e **XPS** como referência/validação.
3. **Blindagem de ML/VC:**
   - Nunca apresentar os `100%` do piloto `IVEFAC333.pptx` (`QUAM-AFM Lite`, $\text{C}_6\text{H}_4\text{BrClO}$) como validação em grafeno real (houve *data leakage* na divisão 80/20 por arquivo e *domain shift* extremo).
   - Exigir particionamento agrupado por amostra/lote físico (*GroupKFold*) e priorizar PDI transparente antes de ML.

## Normas Oficiais de Seminários I (PPGCEM/UFCA)
- **Duração oficial:** **40 a 45 minutos** (nunca 60 min).
- **6 componentes do roteiro:** (1) Definição e aplicação; (2) Fundamentação e estado da arte; (3) Justificativa; (4) Planejamento metodológico; (5) Estimativas de resultados/impactos; (6) Referências bibliográficas.
- **4 critérios de avaliação (2,5 pts cada):** Entendimento do projeto; Clareza dos objetivos; Comunicação/argumentação; Relação com o PPGCEM/UFCA.
