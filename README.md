# 🤖 BotSense: Análise de Sentimentos em Avaliações de E-commerce

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Google Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)

## 🎯 O Problema de Negócio

Em operações logísticas e ecossistemas de atendimento digital, monitorar a satisfação do cliente em tempo real é fundamental. Quando uma empresa gerencia milhares de contatos e pedidos diariamente, ler avaliações manualmente torna-se um processo lento e ineficiente. 

A **dor real** resolvida por este projeto é a automação da triagem de feedback: construir um modelo de Inteligência Artificial capaz de ler textos em linguagem natural (Português) e classificar automaticamente a satisfação do cliente. Isso permite que equipes de suporte ajam rapidamente sobre detratores e que a área de negócios identifique gargalos operacionais.

---

## 🛠️ Passo a Passo do Desenvolvimento

Este projeto foi construído no Google Colab, utilizando a base de dados pública da Olist. Abaixo está a explicação detalhada de cada etapa da construção do modelo.

### Passo 1: Autenticação e Coleta de Dados via API
Para garantir a reprodutibilidade do projeto, a coleta de dados foi automatizada. Em vez de downloads manuais, utilizei a API do Kaggle diretamente no Colab para extrair o dataset `brazilian-ecommerce`.

> ![Código de Extração dos Dados](https://github.com/user-attachments/assets/6993dc79-d812-472f-ba06-08acb7ec46c3)
> 

### Passo 2: Limpeza e Preparação dos Dados (Pré-processamento)
Modelos de Machine Learning precisam de dados estruturados. Nesta etapa, isolei apenas as avaliações que continham texto. Em seguida, criei a variável alvo (Target) agrupando as notas de 1 a 5 em três categorias de sentimento: `Negativo` (1 e 2), `Neutro` (3) e `Positivo` (4 e 5). 
Também apliquei uma função de limpeza no texto usando Expressões Regulares (`re`) para remover pontuações e padronizar tudo em letras minúsculas.

> ![Código de Limpeza de Dados](https://github.com/user-attachments/assets/436b2d83-b419-46d9-8841-e12d06e94b6b)

### Passo 3: Transformando Texto em Matemática (Vetorização)
O algoritmo não lê palavras, ele lê matrizes numéricas. Utilizei o `TfidfVectorizer` da biblioteca Scikit-Learn para transformar as frases limpas em números. O método TF-IDF calcula a relevância de cada palavra no contexto geral, dando menos peso a palavras comuns e mais peso a palavras que definem o sentimento (ex: "excelente", "quebrado"). O vocabulário foi limitado às 5.000 palavras mais relevantes para otimizar o processamento.

> ![Código de Vetorização TF-IDF](https://github.com/user-attachments/assets/7fe55216-aedf-465b-9a72-cbdedcede442)

### Passo 4: Treinamento do Modelo Preditivo
Com os dados vetorizados, treinei um algoritmo de **Random Forest Classifier**. O modelo aprendeu os padrões linguísticos associados a cada classificação de sentimento utilizando 80% da base de dados (dados de treino). Os 20% restantes (dados de teste) foram isolados para avaliar a capacidade do modelo de prever sentimentos em mensagens inéditas.

> ![Código de Treinamento do Modelo](https://github.com/user-attachments/assets/0bef20b4-595c-4ad4-84d1-6c4a503098e1)
 ![Simulação](https://github.com/user-attachments/assets/1ae00a0b-7b9d-418c-9915-001de5abd3c2)

### Passo 5: Avaliação Visual dos Resultados
Para interpretar o desempenho da IA de forma clara para o negócio, gerei visualizações utilizando as bibliotecas `Seaborn` e `Matplotlib`. 
A Matriz de Confusão demonstra visualmente os acertos (diagonal principal) e os falsos positivos/negativos, provando a eficácia do modelo em separar, principalmente, as reclamações mais críticas.

> ![Código e Gráficos de Avaliação](https://github.com/user-attachments/assets/63edd259-2cdc-4090-b441-4a545b6b63ec)
> ![Código e Gráficos de Avaliação](https://github.com/user-attachments/assets/ca08c9cb-0e06-4c9b-903a-1f194f0211a0)
> ![Código e Gráficos de Avaliação](https://github.com/user-attachments/assets/9bec57ec-3ed5-4259-92ca-ef5ac6cba8d3)
---
  
## 🚀 Como Executar o Projeto

Você pode visualizar e testar este projeto diretamente no seu navegador, sem precisar instalar nada, utilizando o Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1PtHBW1dTOKXodsDkRjnJQkreFfDEjYR3?usp=sharing)

**Instruções de uso:**
1. Clique no botão acima para abrir o notebook interativo.
2. Gere o seu token de API (`KAGGLE_API_TOKEN`) na sua conta do [Kaggle](https://www.kaggle.com/).
3. Insira o token na variável correspondente no primeiro bloco de código.
4. No menu superior do Colab, clique em **Ambiente de execução > Executar tudo** para iniciar o download dos dados, treinar o modelo e visualizar os resultados.
