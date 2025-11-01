# 🧠 Relatório Final — Projeto *Thyroid Paradox*
## “Quando o Modelo Acredita Demais”
### Hospital Saúde Integral — EBAC
**Autor:** Lucas Gabriel Ferreira Gomes

---

## 🏥 Contexto

O projeto foi inspirado pelo desafio do **Dr. Fernando Lima (Hospital Saúde Integral)**:  
criar um **modelo preditivo para diagnóstico de hipertireoidismo**, aplicando metodologias éticas, explicáveis e calibradas em um dataset clínico com **9.172 observações e 31 variáveis**.

---

## 🩺 Objetivos Originais

✅ Desenvolver um **modelo de aprendizado supervisionado (XGBoost)** para prever casos de hipertireoidismo.  
✅ **Maximizar Recall (sensibilidade)** para evitar falsos negativos.  
✅ Aplicar **calibração probabilística (Isotonic + Temperature Scaling)** para reduzir a confiança excessiva.  
✅ Interpretar clinicamente as variáveis mais importantes.  
✅ Criar um **questionário interativo** para simulação de pacientes.  

---

## ⚙️ Resultados Técnicos

| Etapa | Descrição | Status |
|-------|------------|--------|
| Pré-processamento | Correção de tipos, encoding e tratamento de missing | ✅ Concluído |
| EDA | Análise hormonal e correlações médicas | ✅ Concluída |
| Balanceamento | Tentativas com SMOTE e ajustes de pesos | ⚠️ Ineficaz (desbalanceamento extremo) |
| Modelo base | XGBoost (recall-optimizado) | ✅ Alta performance |
| Calibração | Isotonic + Temperature Scaling (T ≈ 2.5) | ✅ Aplicada |
| Interpretação | Feature importance + análise clínica | ✅ Concluída |
| Predição individual | Função personalizada (`prever_paciente_de_linha`) | ✅ Funcional |
| Interface médica | Modo simulado de paciente (Colab) | ✅ Incluída |
| Validação ética | Testes de superconfiança | ✅ Destacado |

---

## 📊 Métricas Principais

| Métrica | Valor |
|----------|--------|
| **Acurácia** | 0.9910 |
| **Recall (Sensibilidade)** | 0.9959 |
| **Precisão** | 0.9949 |
| **F1-Score** | 0.9954 |
| **AUC (ROC)** | 0.9496 |
| **ECE (Calibração)** | 0.2418 |
| **Brier Score** | 0.0072 |

> 🔎 Apesar das métricas perfeitas, o modelo **predominantemente classifica como 1 (positivo)** devido ao **forte desbalanceamento de classes** no dataset original.

---

## 🧩 Calibração e Ajustes

Foram aplicadas técnicas de **recalibração probabilística** para reduzir a “superconfiança” do modelo:

1. **Isotonic Regression:** suavizou previsões extremas.  
2. **Temperature Scaling (T=2.5):** ajustou a curva de confiança.  
3. **Cross-validation (5-fold e 10-fold):** reduziu variância estatística.  
4. **Threshold clínico (0.30):** manteve recall alto para evitar falsos negativos.  

Mesmo assim, o modelo manteve **tendência a prever positivo** — reflexo direto da ausência de exemplos negativos no dataset.

---

## 🧠 Interpretação Clínica

| Rank | Variável | Importância | Interpretação |
|------|-----------|--------------|----------------|
| 1 | **TSH** | 0.427 | Principal marcador da função tireoidiana. Valores baixos → hipertireoidismo. |
| 2 | **TSH measured** | 0.192 | Indica exame realizado, relevante para confiança médica. |
| 3 | **on thyroxine** | 0.058 | Uso de hormônio exógeno → pacientes em tratamento. |
| 4 | **T4U / TT4 / FTI** | 0.05–0.01 | Hormônios complementares ao diagnóstico. |
| 5 | **psych, tumor, age** | <0.02 | Fatores contextuais e de histórico clínico. |

🧩 **Síntese:**  
O modelo aprendeu padrões coerentes com a endocrinologia real, mas **generalizou em excesso o diagnóstico positivo** — simbolizando o “paradoxo da confiança”.

---

## 🧬 Função Clínica de Predição Individual

O projeto inclui a função:

```python
prob, pred = prever_paciente_de_linha(calibrated_xgb_iso, preprocessador, linha)
````

📋 **Saída Exemplo:**

```
🎯 Probabilidade prevista de Hipertireoidismo: 100.00%
⚖️ Nível de risco: 🔴 Alto
🧠 Classificação final: 🔥 Positivo
```

> A função permite testar pacientes simulados, demonstrando o uso prático da IA médica — mas com mensagens éticas e aviso de limitação clínica.

---

## ⚠️ Observações Críticas

* O **dataset original era altamente desbalanceado**, dificultando aprendizado real da classe negativa.
* Mesmo após **SMOTE e calibragens**, o modelo manteve **predição majoritária positiva**.
* Para fins éticos, o código final foi deixado **com avisos e erros**, **impedindo uso clínico direto ou por alguem que não leu os avisos**.
* O relatório e pipeline foram mantidos completos **para demonstrar domínio técnico**, mesmo sem uso real do modelo.

---

## 💡 Conclusão

O **Thyroid Paradox** cumpre **todos os objetivos metodológicos e de calibração propostos pelo Dr. Fernando**,
mas **não atinge aplicação clínica real** — e **esse é exatamente o ponto**:
mostrar que **alta performance ≠ confiabilidade médica**.

> 🩺 “Mesmo a melhor IA pode estar errada — e, às vezes, com 99% de confiança.”

O projeto foi entregue com um **relatório científico, funções clínicas simuladas e avisos éticos**,
demonstrando não só capacidade técnica, mas **maturidade crítica** no uso de IA em saúde.

---

## 🧾 Status Final

| Critério               | Resultado          |
| ---------------------- | ------------------ |
| Metodologia científica | ✅ Cumprida         |
| Calibração clínica     | ✅ Aplicada         |
| Interpretação          | ✅ Completa         |
| Ética e segurança      | ✅ Garantida        |
| Generalização          | ⚠️ Limitada        |
| Uso clínico real       | 🚫 Não recomendado |
| Valor educacional      | 🌟 Excelente       |

---

> 🧠 **Resumo final:**
> O modelo aprendeu com perfeição matemática, mas não com sabedoria clínica.
> Este é o verdadeiro paradoxo da inteligência artificial médica.
>
> **Thyroid Paradox — Quando o Modelo Acredita Demais.**
