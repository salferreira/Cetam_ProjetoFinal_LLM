# 🤖 Validação de Sentimento do Mercado Financeiro

## Projeto Final — Componente de LLM | CETAM

Projeto desenvolvido como atividade final do componente de **LLM (Large Language Models)** do **CETAM — Centro de Educação Tecnológica do Amazonas**.

O projeto tem como objetivo analisar o **sentimento presente em textos relacionados ao mercado financeiro**, classificando as frases em três categorias:

* 🟦 **Neutral**
* 🟩 **Positive**
* 🟥 **Negative**

Para realizar a comparação, são utilizadas diferentes técnicas de representação textual sobre o **mesmo conjunto de dados**, mantendo o mesmo classificador e os mesmos critérios de avaliação.

---

## 🎯 Objetivo

Avaliar e comparar o desempenho de diferentes abordagens de representação textual aplicadas a um problema de **classificação de sentimentos em textos financeiros**.

O experimento utiliza:

* **TF-IDF**
* **Word2Vec customizado**
* **GloVe pré-treinado**

Todas as representações são utilizadas como entrada para um classificador de **Regressão Logística**.

O objetivo é verificar qual abordagem apresenta melhor desempenho na classificação dos sentimentos presentes nas frases.

---

## 🔬 Pergunta do Projeto

> **Qual abordagem de representação textual apresenta melhor desempenho na classificação de sentimentos de textos financeiros utilizando o mesmo dataset, a mesma divisão dos dados e o mesmo classificador?**

---

## 📊 Dataset

Foi utilizado o dataset **Financial Sentiment Analysis**, composto por frases relacionadas ao mercado financeiro.

O dataset carregado no projeto possui:

| Característica     | Informação  |
| ------------------ | ----------- |
| Total de registros | 5.842       |
| Colunas            | 2           |
| Texto              | `Sentence`  |
| Classe             | `Sentiment` |
| Número de classes  | 3           |
| Idioma             | Inglês      |

As classes disponíveis são:

```text
neutral
positive
negative
```

O notebook identifica 5.322 frases únicas no conjunto original, indicando a existência de algumas repetições no dataset.

---

## 🧠 Classes de Sentimento

### 🟦 Neutral

Representa informações consideradas neutras, sem indicação clara de sentimento positivo ou negativo.

### 🟩 Positive

Representa informações associadas a perspectivas ou acontecimentos positivos.

### 🟥 Negative

Representa informações associadas a perspectivas ou acontecimentos negativos.

---

# 🧪 Metodologia

O experimento foi dividido em etapas de preparação dos dados, processamento textual, representação vetorial, treinamento e avaliação.

```text
                  DATASET
                     │
                     ▼
           ┌──────────────────┐
           │ Seleção da amostra│
           └─────────┬────────┘
                     │
                     ▼
           ┌──────────────────┐
           │ Limpeza dos dados│
           └─────────┬────────┘
                     │
                     ▼
           ┌──────────────────┐
           │ Tokenização      │
           └─────────┬────────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       TF-IDF    Word2Vec      GloVe
          │          │          │
          └──────────┼──────────┘
                     ▼
            REGRESSÃO LOGÍSTICA
                     │
                     ▼
                 PREVISÕES
                     │
                     ▼
              ┌──────────────┐
              │  AVALIAÇÃO   │
              └──────┬───────┘
                     │
                     ▼
             COMPARAÇÃO FINAL
```

---

# 1. Seleção da Amostra

Para o experimento executado no notebook, foram selecionadas:

**200 frases de cada classe**

Total inicial:

```text
Neutral    → 200
Positive   → 200
Negative   → 200
-----------------
Total      → 600
```

A amostragem foi realizada utilizando `random_state = 42`, garantindo maior reprodutibilidade do experimento.

---

# 2. Limpeza dos Dados

Após a seleção da amostra, foi realizada uma etapa de análise e limpeza.

Foram verificadas:

* Valores nulos;
* Frases duplicadas;
* Caracteres especiais;
* Pontuação;
* Espaços extras;
* Contrações da língua inglesa;
* Tags HTML.

No experimento registrado:

```text
Valores nulos: 0

Duplicatas encontradas: 6

Registros antes da limpeza: 600
Registros após a limpeza: 594
```

---

# 3. Pré-processamento

As frases foram convertidas para letras minúsculas e passaram por limpeza textual.

Também foram removidos:

* Caracteres especiais;
* Pontuação;
* Espaços desnecessários;
* Algumas palavras muito curtas;
* Stopwords da língua inglesa.

Em seguida, foi realizada a tokenização das frases.

---

# 4. Divisão dos Dados

Os dados foram divididos em:

```text
80% → Treinamento
20% → Teste
```

A divisão utilizou:

```python
random_state = 42
```

e estratificação das classes (`stratify`), buscando manter a proporção das categorias entre treinamento e teste.

No experimento executado, após a limpeza, foram utilizados:

```text
Treinamento → aproximadamente 80%
Teste       → aproximadamente 20%
```

---

# 🧮 5. Representação dos Textos

Foram utilizadas três abordagens diferentes para transformar textos em representações numéricas.

---

## 5.1 TF-IDF

O **TF-IDF (Term Frequency–Inverse Document Frequency)** transforma os textos em vetores numéricos considerando a importância das palavras dentro dos documentos.

No projeto foi utilizado:

```python
TfidfVectorizer(max_features=5000)
```

O vocabulário foi ajustado somente sobre os dados de treinamento:

```python
X_train_tfidf = tfidf_vec.fit_transform(X_train_text)
```

e posteriormente aplicado aos dados de teste:

```python
X_test_tfidf = tfidf_vec.transform(X_test_text)
```

---

## 5.2 Word2Vec

O segundo método utilizado foi o **Word2Vec**, treinado especificamente com os textos do conjunto de treinamento.

Configuração utilizada:

```text
vector_size = 100
window      = 5
min_count   = 2
workers     = 4
seed        = 42
```

Cada frase é representada pela **média dos vetores das palavras presentes na frase**.

---

## 5.3 GloVe

Também foi utilizado o modelo **GloVe pré-treinado**:

```text
glove-wiki-gigaword-100
```

O modelo possui vetores de dimensão 100.

Assim como no Word2Vec, a representação final de cada frase foi obtida através da média dos vetores das palavras encontradas no vocabulário.

---

# 🤖 6. Classificador

Para tornar a comparação mais controlada, as três representações foram utilizadas com o mesmo classificador:

## Regressão Logística

Configuração utilizada:

```python
LogisticRegression(
    max_iter=1000,
    random_state=42
)
```

Dessa forma, o experimento compara principalmente o efeito da **representação dos textos**, mantendo o algoritmo de classificação constante.

---

# 📏 7. Métricas de Avaliação

Foram utilizadas três métricas principais.

### Accuracy

Representa a proporção de classificações corretas realizadas pelo modelo.

### F1-Score Macro

Calcula o F1-Score individualmente para cada classe e depois realiza a média, dando o mesmo peso às três categorias.

Essa métrica é especialmente útil para avaliar o desempenho considerando todas as classes.

### MCC — Matthews Correlation Coefficient

O **Matthews Correlation Coefficient** fornece uma medida adicional de qualidade das classificações, considerando os acertos e erros entre as diferentes classes.

O notebook também utiliza:

* Classification Report;
* Matriz de Confusão.

---

# 📈 8. Resultados

Os resultados registrados no experimento foram:

| Abordagem                        | Accuracy | F1 Macro |        MCC |
| -------------------------------- | -------: | -------: | ---------: |
| **TF-IDF + Regressão Logística** | **0,66** | **0,65** | **0,4905** |
| Word2Vec + Regressão Logística   |     0,34 |     0,17 |     0,0000 |
| GloVe + Regressão Logística      |     0,59 |     0,58 |     0,3859 |

Os valores foram obtidos no conjunto de teste utilizado pelo notebook.

---

# 🔎 9. Análise dos Resultados

### TF-IDF

A abordagem TF-IDF apresentou:

```text
Accuracy  = 66%
F1 Macro  = 65%
MCC       = 0,4905
```

O relatório de classificação mostrou desempenho relativamente equilibrado entre as três classes, embora a classe positiva tenha apresentado maior recall.

---

### Word2Vec

O Word2Vec apresentou:

```text
Accuracy  = 34%
F1 Macro  = 17%
MCC       = 0,0000
```

O relatório registrado mostra que o classificador praticamente concentrou suas previsões em uma única classe:

```text
neutral  → F1 = 0,00
positive → F1 = 0,00
negative → F1 = 0,50
```

Isso demonstra uma baixa capacidade de discriminação entre as três classes nesse experimento específico.

---

### GloVe

O GloVe apresentou:

```text
Accuracy  = 59%
F1 Macro  = 58%
MCC       = 0,3859
```

Seu desempenho ficou abaixo do TF-IDF, mas acima do Word2Vec no experimento realizado.

---

# 📊 Comparação Visual

O notebook também gera matrizes de confusão para as três abordagens, permitindo analisar como cada método distribuiu suas previsões entre:

```text
Neutral
Positive
Negative
```

Essa análise complementa as métricas numéricas e permite observar quais classes apresentam maior quantidade de erros.

---

# 🏁 Conclusão

O experimento demonstrou que diferentes formas de representação textual podem produzir resultados significativamente diferentes quando aplicadas ao mesmo problema de classificação.

No experimento realizado, as três abordagens foram avaliadas utilizando:

* O mesmo dataset;
* A mesma tarefa de classificação;
* A mesma divisão de treinamento e teste;
* O mesmo classificador;
* As mesmas métricas de avaliação.

Os resultados registrados apresentaram diferenças entre as abordagens, permitindo analisar o impacto da representação textual no desempenho da classificação de sentimentos financeiros.

A comparação deve ser interpretada dentro das condições específicas deste experimento, considerando também o tamanho reduzido da amostra utilizada na execução registrada.

---

# 🛠️ Tecnologias Utilizadas

* 🐍 Python
* 📓 Google Colab
* 📊 Pandas
* 🔢 NumPy
* 📈 Matplotlib
* 📉 Scikit-learn
* 🧠 Gensim
* 🔤 NLTK
* ☁️ Google Drive
* 🤗 Hugging Face Datasets

---

# 📂 Estrutura do Projeto

```text
projeto-final-llm-cetam/
│
├── Trabalho_Final.ipynb
├── README.md
│
├── data/
│   └── dataset/
│
├── results/
│   ├── confusion_matrix/
│   └── metrics/
│
└── requirements.txt
```

---

# 🚀 Como Executar

## 1. Clone o repositório

```bash
git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
```

## 2. Abra o notebook

Abra:

```text
Trabalho_Final.ipynb
```

preferencialmente no **Google Colab**.

## 3. Monte o Google Drive

O notebook utiliza arquivos armazenados no Google Drive.

A estrutura esperada deve ser configurada de acordo com o caminho utilizado no projeto.

## 4. Instale as dependências

As principais bibliotecas utilizadas são:

```bash
pip install pandas numpy matplotlib scikit-learn gensim nltk wordcloud kagglehub
```

## 5. Execute as células

Execute as células do notebook na ordem apresentada.

Durante a execução será solicitada a quantidade de frases por classe utilizada na amostragem.

---

# 🔁 Reprodutibilidade

O projeto utiliza a semente:

```python
RANDOM_STATE = 42
```

e:

```python
SEED = 42
```

A utilização de uma semente fixa permite reduzir a variação causada pela aleatoriedade na amostragem e na divisão dos dados.

---

# ⚠️ Limitações do Experimento

Algumas limitações devem ser consideradas na interpretação dos resultados:

* O experimento registrado utiliza apenas **200 frases por classe** inicialmente;
* Após a remoção de duplicatas, foram utilizados **594 registros**;
* O conjunto de teste possui aproximadamente 119 exemplos;
* Word2Vec foi treinado sobre uma quantidade relativamente pequena de textos;
* Word2Vec e GloVe utilizam a média dos vetores das palavras para representar uma frase, o que pode perder informações relacionadas à ordem e ao contexto das palavras;
* O GloVe utilizado é um modelo pré-treinado de domínio geral, enquanto o problema é específico do mercado financeiro.

Essas características podem influenciar os resultados obtidos.

---

# 🎓 Contexto Acadêmico

**Instituição:** CETAM — Centro de Educação Tecnológica do Amazonas

**Curso:** Técnico em Inteligência Artificial

**Componente:** LLM — Large Language Models

**Projeto:** Validação de sentimento do mercado financeiro com base em comentários de notícias

---

## 👨‍🎓 Autor

**Nome:** Seu Nome

**Curso:** Técnico em Inteligência Artificial — CETAM

---

## 📜 Licença

Projeto desenvolvido para fins acadêmicos e educacionais como parte das atividades do curso Técnico em Inteligência Artificial do CETAM.

---

⭐ **Projeto Final — Componente de LLM | CETAM**
