# 🚦 Análise de Acidentes — PRF Pará 2024–2025

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Completo-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green)
![Topic](https://img.shields.io/badge/Tema-Segurança%20Viária-red)
![Data](https://img.shields.io/badge/Dados-PRF%2FDATATRAN-orange)

## 📌 Introdução

Estudo completo de segurança viária nas rodovias federais do **Pará (2024–2025)**, baseado em dados abertos da Polícia Rodoviária Federal (PRF/DATATRAN). O Pará ocupa o **2° lugar nacional em taxa de fatalidade** — 18,21%, 2,5× a média nacional de 7,17%.

O projeto combina análise exploratória, modelagem estatística avançada e predição de risco para 2026, organizado em três notebooks encadeados com documentação científica completa.

## 🔑 Resultados principais

| Eixo | Método | Resultado |
|---|---|---|
| Contexto nacional | Ranking por UF | PA: 18,21% fatal — 2° lugar (n=27 UFs) |
| Tendência temporal | GLM Poisson + NB2 | Sobredispersão leve (χ²/df=1,59) |
| Fatores de risco | Regressão Ordinal | Atropelamento (OR=6,2) e Colisão frontal (OR=5,8) |
| Heterogeneidade | GLMM | ICC=14–16% entre rodovias |
| Classificação | XGBoost calibrado | AUC=0,715 · Brier=0,176 (validação temporal) |
| Explicabilidade | SHAP | Pista escorregadia e condutor dormindo = maiores drivers |
| Predição 2026 | Validação temporal | Treino 2024 → Teste 2025 — sem data leakage |
| Score de risco | Histórico + preditivo | 117 trechos ranqueados (0–100) |

## 📊 Visualizações

### NB01 — Análise Espacial

| Densidade de Acidentes Fatais (KDE) |
|---|
| ![](relatorios/nb01_densidade_acidentes_fatais.png) |

### NB02 — Modelagem Estatística

| Forest Plot — OR Cumulativos | SHAP Summary — XGBoost |
|---|---|
| ![](relatorios/nb02_forest_plot_or.png) | ![](relatorios/nb02_shap_summary.png) |

| Curva de Calibração |
|---|
| ![](relatorios/nb02_curva_calibracao.png) |

### NB03 — Validação Temporal e Predição 2026

| Curva ROC + Calibração da Validação Temporal |
|---|
| ![](relatorios/nb03_curva_roc_calibracao.png) |

| Projeção por Rodovia 2026 | Mapa de Risco Preditivo 2026 |
|---|---|
| ![](relatorios/nb03_projecao_2026.png) | ![](relatorios/nb03_mapa_risco_preditivo.png) |

| Simulador Interativo de Risco |
|---|
| ![](relatorios/nb03_simulador_risco.png) |

## 🧠 Metodologia — 3 Notebooks Encadeados

```
NB01 → EDA, Governança e Análise Espacial
       GLM Poisson · Mapas KDE · Trechos críticos · Exporta parquet

NB02 → Modelagem Estatística Avançada
       Regressão Ordinal · GLMM · Hotspot Binomial · XGBoost + SHAP

NB03 → Predição de Risco para 2026
       Validação temporal · Score de risco · Projeção GLM · Simulador
```

## 🏗️ Arquitetura

```
01_EDA_Governanca.ipynb
  └─ exporta df_pa_final.parquet
        └─ 02_Modelagem_Estatistica.ipynb
              └─ 03_Predicao_Risco_2026.ipynb
                    └─ Simulador interativo de risco
```

**Validação temporal estrita:** modelo treinado em 2024, testado em 2025 — sem data leakage.

## 📄 Documentação

Cada notebook possui documento Word correspondente em `documentacao/`:
- `Parte1_EDA_Governanca.docx`
- `Parte2_Modelagem_Estatistica.docx`
- `Parte3_Predicao_2026.docx`

## 🛠️ Stack

- **Modelagem:** statsmodels (GLM, GLMM, Ordinal), XGBoost, scikit-learn
- **Explicabilidade:** SHAP
- **Visualização:** matplotlib, seaborn, folium
- **Dados:** pandas, NumPy, pyarrow
- **Ambiente:** Google Colab / Jupyter

## ▶️ Como executar

```bash
pip install pandas numpy scipy matplotlib seaborn xgboost shap \
            statsmodels folium scikit-learn pyarrow mord pymer4
```

**Dados:** baixe `datatran2024.csv` e `datatran2025.csv` em
[dados.gov.br — PRF Acidentes](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf)

Execute em ordem: `NB01 → NB02 → NB03`

## ⚠️ Limitações

- Dataset restrito ao Pará (n=1.977) — poder limitado para trechos individuais
- Hotspots: nenhum significativo após Bonferroni — FDR recomendado como próximo passo
- Simulador baseado em padrões históricos 2024–2025 — não substitui avaliação profissional

## 🔗 Projetos relacionados

- [Inferência Bayesiana Aplicada — A/B Testing](https://github.com/gilsonmm6/bayesian-ab-marketing)
- [Análise de Fairness — COMPAS](https://github.com/gilsonmm6/compas-fairness-analysis)
- [Aprendizado por Reforço — DPI/MARL](https://github.com/gilsonmm6/iterated-prisoners-dilemma-marl)
- [Previsão TSLA com LSTM](https://github.com/gilsonmm6/tesla-lstm-forecast)

## 👤 Autor

**Gilson Machado Monteiro**  
Data Analyst & BI Analyst | Especialização em Estatística Aplicada (PUC Minas)  
[LinkedIn](https://linkedin.com/in/gilsonmachadomonteiro) · [GitHub](https://github.com/gilsonmm6)
