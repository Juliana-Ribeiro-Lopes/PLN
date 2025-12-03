# **Processamento de Linguagem Natural [2025-Q3] - UFABC**

---

# **PROJETO PRÁTICO – COP30**

Este projeto implementa um pipeline completo de **Processamento de Linguagem Natural (PLN)** utilizando o framework **LangChain**, integrado ao modelo **Gemini (Google Generative AI)**, com o objetivo de analisar como a mídia internacional tem discutido a **COP30**, que ocorreu em Belém (PA).

As notícias são coletadas **em tempo real** por meio da **NewsAPI**. A partir desse corpus, foram aplicadas três técnicas principais de PLN:

---

## 🔍 **1. Busca Semântica**
Utiliza embeddings do modelo **gemini-embedding-001** e o indexador **FAISS** para recuperar as notícias mais relevantes sobre a COP30.  
A busca se baseia no *significado* dos textos, não apenas em palavras-chave.

---

## 🧠 **2. Extração de Tópicos**
Aplicada sobre as notícias recuperadas pela busca semântica.  
Foi criado um **esquema Pydantic (ExtracaoDados)** para extrair informações estruturadas:

- Tópico principal  
- Decisões associadas  
- Países citados  
- Órgãos envolvidos  
- Categoria (ambiental, econômica, diplomática)  
- Fonte

O modelo LLM utilizado na extração foi o **Gemini 2.5-flash**, com **temperature=0.0** para garantir respostas determinísticas e sem criatividade.

---

## ✂️ **3. Sumarização de Textos**
Gera um resumo condensado das principais notícias, destacando:

- temas recorrentes  
- padrões narrativos  
- pontos de atenção da imprensa  
- insights sobre impactos da COP30  

Essa etapa utiliza novamente o **Gemini 2.5-flash**, desta vez com **temperature=0.2**, para permitir maior fluidez textual sem perder coerência.

---

## 🧩 **Integração Final**
O pipeline completo resulta em uma **análise meta-sintética**, combinando:

- dados coletados em tempo real  
- busca semântica  
- extração estruturada  
- sumarização global  

Essa integração demonstra como ferramentas modernas de PLN podem apoiar:

- estudos sobre políticas climáticas  
- análises jornalísticas  
- tomada de decisão estratégica  
- monitoramento de narrativas internacionais  

---

# **Equipe**

- Ana Luísa Costa Nunes | 11202420185
- Juliana Ribeiro Lopes | 21075612

---

# **Grande Modelo de Linguagem (LLM)**

**LLM:** Gemini 2.5-flash  
**Documentação:**  
https://ai.google.dev/gemini-api/docs/models?hl=pt-br  
https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash

---

# **API**

**API utilizada:** NewsAPI  
**Site oficial:** https://newsapi.org/  
**Documentação:** https://newsapi.org/docs  

A API foi utilizada para coletar notícias relacionadas à *COP30*, entre os dias **10/11/2025 e 21/11/2025**, no idioma **português**.

---

# **DESCRIÇÃO DO PROJETO**

Implementar um **notebook no Google Colab** que faça uso do framework **LangChain** e de um **LLM**, aplicando **de três técnicas de PLN** em dados obtidos via API ou página web.

Este projeto utiliza **três técnicas**:

✔️ Busca Semântica  
✔️ Extração Estruturada  
✔️ Sumarização de Textos  

O LLM e a API utilizados foram informados na planilha oficial do professor.


---

# Coleta de Notícias via NewsAPI

Requisição contendo os filtros de:

- período da COP30 (de 10/11 a 21/11/2025)

- idioma PT

- ordenação por popularidade

* Por favor verificar o período de busca, pois a API libera somente notícias publicadas há no máximo 30 dias no plano gratuito

# **Implementação**

## 📦 Instalação das Dependências

```python
!pip install -U --force-reinstall langchain langchain-google-genai google-generativeai newsapi-python tiktoken langchain-community langchain-text-splitters
!pip install -U langchain-google-genai
!pip install faiss-cpu

