# 🤖 Projeto Final — Componente de LLM | CETAM

## 📌 Sobre o Projeto

Este projeto foi desenvolvido como **Projeto Final do componente de LLM (Large Language Models)** do **CETAM — Centro de Educação Tecnológica do Amazonas**.

O objetivo principal é realizar um **experimento comparativo entre dois modelos de Inteligência Artificial**, utilizando **um mesmo conjunto de dados (dataset)** para treinamento e avaliação.

A proposta consiste em aplicar a mesma metodologia aos dois modelos, analisar seus resultados e, com base em **métricas objetivas de desempenho**, identificar qual deles apresenta melhor desempenho para a tarefa proposta.

---

## 🎯 Objetivo

Treinar e avaliar **dois modelos de Machine Learning/Inteligência Artificial** utilizando o mesmo dataset, mantendo as condições do experimento equivalentes para permitir uma comparação justa entre os modelos.

### Objetivos específicos

* 📊 Utilizar um único dataset como base para os experimentos;
* 🧹 Realizar o pré-processamento dos dados;
* 🔀 Dividir os dados em conjuntos de treinamento e teste;
* 🤖 Treinar dois modelos distintos;
* 🧪 Avaliar os modelos utilizando as mesmas métricas;
* 📈 Comparar os resultados obtidos;
* 🔍 Analisar pontos fortes e limitações de cada modelo;
* 🏆 Identificar o modelo que apresentou melhor desempenho no experimento.

---

## 🧠 Pergunta de Pesquisa

> **Qual dos dois modelos apresenta melhor desempenho quando treinado e avaliado utilizando o mesmo conjunto de dados e a mesma metodologia experimental?**

A comparação será realizada considerando métricas quantitativas de avaliação, evitando que a escolha seja baseada apenas em uma métrica isolada.

---

## 🧪 Metodologia

O experimento seguirá as seguintes etapas:

```text
                 ┌──────────────────┐
                 │      Dataset     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Pré-processamento│
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Divisão dos dados│
                 │ Treino / Teste   │
                 └────────┬─────────┘
                          │
                ┌─────────┴─────────┐
                ▼                   ▼
       ┌────────────────┐   ┌────────────────┐
       │    Modelo 1    │   │    Modelo 2    │
       └───────┬────────┘   └───────┬────────┘
               │                    │
               ▼                    ▼
       ┌────────────────┐   ┌────────────────┐
       │    Avaliação   │   │    Avaliação   │
       └───────┬────────┘   └───────┬────────┘
               │                    │
               └─────────┬──────────┘
                         ▼
                ┌──────────────────┐
                │    Comparação    │
                │   dos modelos    │
                └────────┬─────────┘
                         │
                         ▼
                ┌──────────────────┐
                │     Conclusão    │
                └──────────────────┘
```

### 1. Dataset

Será utilizado um único dataset como fonte de dados para os dois experimentos.

Os dois modelos receberão **os mesmos dados**, garantindo que a comparação seja realizada sob condições equivalentes.

**Dataset utilizado:**

> `NOME_DO_DATASET`

**Quantidade de registros:**

> `XXXX registros`

**Principais características:**

* Número de atributos: `XX`
* Variável-alvo: `NOME_DA_VARIAVEL`
* Tipo de problema: `Classificação / Regressão / NLP`
* Número de classes: `XX`

---

### 2. Pré-processamento

Antes do treinamento, os dados passarão por etapas de preparação, que podem incluir:

* Tratamento de valores ausentes;
* Remoção de dados inconsistentes;
* Normalização ou padronização;
* Conversão de variáveis;
* Tokenização, quando aplicável;
* Transformação dos textos em representações numéricas;
* Separação entre características e variável-alvo.

O mesmo processo de preparação será aplicado aos dois modelos.

---

### 3. Divisão dos dados

O dataset será dividido em conjuntos destinados ao treinamento e à avaliação.

Exemplo:

```text
Dataset
   │
   ├── 80% → Treinamento
   │
   └── 20% → Teste
```

Quando necessário, também poderá ser utilizado um conjunto de validação para acompanhar o desempenho durante o treinamento e identificar possíveis problemas como **overfitting**.

---

## 🤖 Modelos Utilizados

O experimento utilizará dois modelos diferentes.

### Modelo 1

**Nome:** `MODELO 1`

**Descrição:**

> Descrição resumida do primeiro modelo utilizado no experimento.

---

### Modelo 2

**Nome:** `MODELO 2`

**Descrição:**

> Descrição resumida do segundo modelo utilizado no experimento.

---

## ⚖️ Comparação Experimental

Para garantir uma comparação adequada, os modelos serão submetidos às mesmas condições sempre que tecnicamente possível.

| Condição               | Modelo 1       | Modelo 2       |
| ---------------------- | -------------- | -------------- |
| Dataset                | Mesmo dataset  | Mesmo dataset  |
| Dados de treinamento   | Mesmos dados   | Mesmos dados   |
| Dados de teste         | Mesmos dados   | Mesmos dados   |
| Pré-processamento      | Mesmo processo | Mesmo processo |
| Critérios de avaliação | Mesmos         | Mesmos         |
| Métricas               | Mesmas         | Mesmas         |

O objetivo é fazer com que a principal diferença do experimento seja o **modelo utilizado**.

---

## 📊 Métricas de Avaliação

Os modelos serão avaliados utilizando métricas adequadas ao problema.

Entre as métricas que poderão ser utilizadas estão:

### Accuracy

Mede a proporção de previsões corretas em relação ao total de previsões.

```text
Accuracy = Previsões corretas / Total de previsões
```

### Precision

Indica, entre as previsões positivas realizadas pelo modelo, quantas realmente eram positivas.

### Recall

Indica a capacidade do modelo de identificar corretamente os exemplos positivos.

### F1-Score

Combina Precision e Recall em uma única métrica.

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

### Matriz de Confusão

Será utilizada para visualizar a distribuição dos acertos e erros cometidos pelos modelos.

Exemplo:

```text
                  Predito
               Negativo Positivo
Real Negativo     TN        FP
     Positivo     FN        TP
```

---

## 📈 Resultados

Os resultados dos dois modelos serão apresentados de forma comparativa.

### Resultados obtidos

| Métrica   | Modelo 1 | Modelo 2 |
| --------- | -------: | -------: |
| Accuracy  |   XX,XX% |   XX,XX% |
| Precision |   XX,XX% |   XX,XX% |
| Recall    |   XX,XX% |   XX,XX% |
| F1-Score  |   XX,XX% |   XX,XX% |

> **Observação:** Os valores acima deverão ser substituídos pelos resultados
