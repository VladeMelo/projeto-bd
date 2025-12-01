# ETL & ELT para Data Warehouse de Turismo: Análise de Atendimentos (2022-2024)

Este repositório documenta a construção de um pipeline de engenharia de dados focado na análise de fluxo turístico, utilizando e comparando as abordagens **ETL** (Extract, Transform, Load) e **ELT** (Extract, Load, Transform). O projeto explora e compara essas duas metodologias essenciais — processamento em memória (Python/ETL) versus processamento em banco de dados (SQL/ELT) — para consolidar bases de dados dispersas em uma estrutura analítica robusta.

---

## 📋 Visão Geral

O projeto visa transformar dados brutos de atendimento ao turista, coletados ao longo de três anos, em um **Data Warehouse** modelado em **Esquema Estrela (Star Schema)**. Essa estrutura facilita a geração de insights sobre o perfil dos visitantes, suas origens e interesses.

### O Desafio dos Dados
Os dados originais apresentavam desafios típicos de cenários reais:
*   Fragmentação em múltiplos arquivos (2022, 2023, 2024).
*   Inconsistências de formatação (espaços extras, variações de escrita).
*   Alta incidência de valores nulos em campos não obrigatórios.

---

## ⚙️ Estratégias de Implementação

Para fins didáticos, o Data Warehouse foi construído utilizando duas abordagens distintas:

### 1. Pipeline ETL
*Foco no processamento via aplicação.*
Nesta abordagem, o **Pandas** é o motor de transformação. O script extrai os dados, realiza toda a limpeza, deduplicação e modelagem das dimensões na memória do Python e, por fim, carrega as tabelas prontas no banco de dados.
*   **Arquivo:** `ETL.ipynb`

### 2. Pipeline ELT
*Foco no processamento via banco de dados.*
Aqui, o Python atua apenas como um orquestrador de carga, inserindo os dados brutos em uma área de estágio (*Staging Area*). A inteligência do processo reside no **SQL**, que é utilizado para limpar, normalizar e estruturar as tabelas finais diretamente dentro do banco.
*   **Arquivo:** `ELT.ipynb`

---

## 🗂️ Estrutura do Banco de Dados

O modelo final é composto por uma tabela fato central cercada por dimensões descritivas:

*   **`fato_atendimentos`**: Tabela central que registra cada interação/atendimento, conectando todas as dimensões.
*   **`dim_perfil_turista`**: Consolida dados demográficos (Nacionalidade, Estado/País de origem, Faixa Etária, Gênero).
*   **`dim_detalhes_viagem`**: Caracteriza a viagem (Tipo de Hospedagem, Meio de Transporte, Motivação, Tempo de Estadia).
*   **`dim_local`**: Mapeia onde ocorreu o atendimento e qual o município de interesse do turista.
*   **`dim_tempo`**: Permite cortes temporais (Ano e Mês) nas análises.

---

## 💻 Stack

*   **Linguagem:** Python 3.x
*   **Bibliotecas:** Pandas (Manipulação de dados), SQLite3 (Interface de banco).
*   **Banco de Dados:** SQLite (Armazenamento local leve e eficiente).

---

## ▶️ Como Reproduzir

1.  **Pré-requisitos:** Certifique-se de ter o Python instalado e a biblioteca Pandas (`pip install pandas`).
2.  **Dados:** Garanta que a pasta `dados/` contenha os arquivos CSV dos anos 2022, 2023 e 2024.
3.  **Execução:**
    *   Abra o `ETL.ipynb` para ver a construção via Pandas.
    *   Abra o `ELT.ipynb` para ver a construção via SQL.
    *   Execute as células sequencialmente para gerar os arquivos `.db` correspondentes.