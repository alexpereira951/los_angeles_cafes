# ☕🤖 Análise de Mercado de Cafeterias em Los Angeles

Análise exploratória do mercado de estabelecimentos alimentícios de **Los Angeles**, com foco na avaliação de oportunidades para uma cafeteria com **garçons robôs**. O projeto investiga composição do mercado, presença de redes, capacidade dos estabelecimentos e concentração geográfica para apoiar uma análise de posicionamento e localização.

## 🎯 Objetivo do Projeto

O objetivo é compreender as características do mercado alimentício de Los Angeles e identificar padrões relevantes para o planejamento de uma cafeteria inovadora.

As principais questões investigadas foram:

- Qual é a participação dos cafés em relação aos demais tipos de estabelecimentos?
- Qual é a proporção de estabelecimentos independentes e de rede?
- Como os estabelecimentos de rede se diferenciam dos independentes em relação ao número de assentos?
- Qual é a capacidade média dos diferentes tipos de estabelecimentos?
- Quais ruas concentram mais estabelecimentos alimentícios?
- Como se distribui o número de assentos nas principais ruas?

---

## 🧠 Abordagem / Arquitetura Técnica

O projeto foi desenvolvido como um fluxo de **análise exploratória de dados (EDA)**, estruturado nas seguintes etapas:

### 1. Preparação e otimização dos dados

O dataset `rest_data_us_upd.csv` contém informações sobre **9.651 registros inicialmente carregados**, com as seguintes variáveis principais:

| Coluna | Descrição |
|---|---|
| `id` | Identificador do estabelecimento |
| `object_name` | Nome do estabelecimento |
| `address` | Endereço |
| `chain` | Indica se o estabelecimento pertence a uma rede |
| `object_type` | Tipo de estabelecimento |
| `number` | Número de assentos |

Durante a preparação:

- `object_type` foi convertido para o tipo categórico;
- `chain` foi carregada como tipo booleano;
- foram identificados **3 valores ausentes** em `chain`;
- os registros com valores ausentes foram removidos;
- não foram encontradas linhas completamente duplicadas;
- foram identificados **7 estabelecimentos com inconsistência na classificação de rede**, aparecendo simultaneamente como rede e não rede, e esses registros foram removidos;
- estabelecimentos com mais de um tipo de negócio foram identificados, mas não removidos por representarem uma característica possível do mercado.

Ao final do tratamento, foram analisados **9.648 estabelecimentos**.

### 2. Análise da composição do mercado

Foi calculada a quantidade e a participação percentual de cada tipo de estabelecimento.

Os principais resultados foram:

| Tipo | Quantidade | Participação |
|---|---:|---:|
| Restaurant | 7.238 | 75,16% |
| Fast Food | 1.066 | 11,07% |
| Cafe | 434 | 4,51% |
| Pizza | 317 | 3,29% |
| Bar | 292 | 3,03% |
| Bakery | 283 | 2,94% |

### 3. Redes versus estabelecimentos independentes

A análise identificou:

- **5.963 estabelecimentos independentes**;
- **3.667 estabelecimentos de rede**.

Isso corresponde aproximadamente a **62% de independentes** e **38% de estabelecimentos de rede**.

Também foi investigada a participação dos cafés entre os estabelecimentos de rede. O notebook registra aproximadamente **7,2%** de participação para cafés nesse recorte.

### 4. Capacidade dos estabelecimentos

A distribuição do número de assentos foi comparada entre estabelecimentos de rede e independentes.

Como os dados não apresentaram distribuição normal, foi utilizada uma abordagem não paramétrica. A função estatística desenvolvida no notebook:

1. verifica a normalidade;
2. avalia a homogeneidade de variâncias quando aplicável;
3. seleciona entre teste t de Student, teste t de Welch ou Mann-Whitney;
4. utiliza nível de significância de **5%**.

Para a comparação entre redes e independentes, o teste de Mann-Whitney apresentou **p-valor < 0,05**, levando à rejeição da hipótese nula definida no notebook.

As medianas observadas foram:

- **25 assentos** para estabelecimentos de rede;
- **28 assentos** para estabelecimentos independentes.

### 5. Análise geográfica por rua

Uma função baseada em **expressões regulares (regex)** foi criada para extrair o nome da rua a partir do endereço.

Foram identificadas **975 ruas únicas**.

As ruas com maior concentração de estabelecimentos foram:

1. Sunset Blvd — 388 estabelecimentos
2. Wilshire Blvd — 372 estabelecimentos
3. Pico Blvd — 363 estabelecimentos

Também foram identificadas **646 ruas com apenas um estabelecimento**, equivalentes a **66,26%** das ruas analisadas.

### 6. Capacidade nas principais ruas

As 10 ruas com maior concentração de estabelecimentos foram analisadas quanto à distribuição de assentos.

O notebook observa uma concentração relevante entre **22 e 36 assentos** nas principais ruas e utiliza a mediana para representar os grupos devido à presença de distribuições assimétricas.

---

## 📁 Estrutura do Repositório

```text
los_angeles_cafes/
│
├── apresentacao/
│   └── apresentacao.pdf
│
├── datasets/
│   └── rest_data_us_upd.csv
│
├── notebook.ipynb
│
└── requirements.txt
```

### 📂 Principais arquivos e diretórios

- `apresentacao/` — contém a apresentação do projeto em PDF.
- `datasets/` — armazena o conjunto de dados utilizado na análise.
- `notebook.ipynb` — notebook Jupyter com todo o processo de preparação, análise, visualização e interpretação dos dados.
- `requirements.txt` — arquivo destinado às dependências necessárias para reprodução do projeto.

---

## ⚙️ Instalação e Execução

### 1. Clonar o repositório

```bash
git clone https://github.com/alexpereira951/los_angeles_cafes
cd los_angeles_cafes
```

### 2. Criar um ambiente virtual

```bash
python -m venv .venv
```

Ativação no Windows:

```bash
.venv\Scripts\activate
```

Ativação no Linux/macOS:

```bash
source .venv/bin/activate
```

### 3. Instalar as dependências

```bash
pip install -r requirements.txt
```

### 4. Executar o notebook

```bash
jupyter notebook
```

Em seguida, abra:

```text
notebook.ipynb
```

> **Observação:** o notebook utiliza o dataset localizado em `datasets/rest_data_us_upd.csv` por meio de um caminho relativo. Portanto, mantenha a estrutura de diretórios do projeto conforme apresentada acima.

---

## 🛠️ Stack Tecnológica

| Tecnologia | Utilização |
|---|---|
| 🐍 **Python** | Linguagem principal da análise |
| 🐼 **Pandas** | Manipulação, limpeza e agregação dos dados |
| 🔢 **NumPy** | Operações numéricas |
| 📊 **Matplotlib** | Construção de visualizações |
| 📈 **Seaborn** | Visualizações estatísticas |
| 📉 **Plotly Express** | Gráficos interativos |
| 🧪 **SciPy** | Testes estatísticos |
| 📓 **Jupyter Notebook** | Desenvolvimento e documentação da análise |
| 🔎 **Regex (`re`)** | Extração e padronização dos nomes das ruas |

---

## 📊 Resultados e Conclusões

A análise encontrou alguns padrões relevantes no conjunto de dados:

### Participação dos cafés

Os cafés representam **4,51% dos estabelecimentos alimentícios** analisados, enquanto restaurantes representam **75,16%** e fast foods **11,07%**.

### Perfil de redes

A base analisada possui aproximadamente:

- **62% de estabelecimentos independentes**;
- **38% de estabelecimentos de rede**.

Entre os estabelecimentos de rede, cafés representam aproximadamente **7,2%**.

### Capacidade

Os estabelecimentos de rede apresentam mediana de **25 assentos**, enquanto os independentes apresentam mediana de **28 assentos**. O teste estatístico aplicado no notebook indicou diferença estatisticamente significativa entre os grupos ao nível de 5%.

### Concentração geográfica

As dez ruas com maior quantidade de estabelecimentos concentram uma parcela relevante do mercado analisado. Por outro lado, **646 das 975 ruas identificadas possuem apenas um estabelecimento**, indicando baixa concentração de estabelecimentos em grande parte das ruas da base.

### Capacidade nas ruas mais movimentadas

Nas dez ruas com maior concentração, o notebook identifica uma faixa de aproximadamente **22 a 36 assentos** como intervalo recorrente entre os estabelecimentos analisados.

### Síntese

Os resultados fornecem uma visão quantitativa do mercado de Los Angeles e podem servir como base para avaliar hipóteses de **posicionamento, capacidade e localização** de uma cafeteria. A proposta de garçons robôs aparece no projeto como hipótese de diferenciação, mas sua viabilidade econômica não é diretamente mensurada pelo dataset analisado.

---

## ⚠️ Limitações

O projeto apresenta limitações que devem ser consideradas na interpretação dos resultados:

1. **Recorte dos dados:** a análise utiliza um conjunto de dados aberto de estabelecimentos de Los Angeles e não incorpora, no notebook, uma série temporal capaz de avaliar a evolução do mercado ao longo dos anos.

2. **Informações removidas durante o tratamento:** foram eliminados **3 registros com valores ausentes** em `chain` e **7 estabelecimentos com classificação inconsistente de rede**. Essas decisões melhoram a consistência da análise, mas reduzem a quantidade de observações disponíveis.

3. **Ausência de variáveis econômicas e de demanda:** o dataset analisado não contempla, no notebook, informações como faturamento, aluguel, custos operacionais, fluxo de pessoas, ticket médio, perfil dos consumidores ou rentabilidade. Portanto, os resultados não constituem uma análise financeira de viabilidade do negócio.

4. **Limitação da análise estatística e geográfica:** a comparação de capacidade é baseada principalmente no número de assentos e em testes de distribuição, enquanto a análise de localização utiliza o nome das ruas extraído dos endereços. Isso não permite, isoladamente, estimar demanda, tráfego de pedestres ou potencial de receita de cada localização.

---

## 📌 Conclusão

Este projeto demonstra um fluxo completo de **análise exploratória de dados**, desde a leitura e otimização da base até a limpeza, tratamento de inconsistências, análise estatística, engenharia de atributos e visualização.

A análise identifica padrões de **composição do mercado, estrutura de redes, capacidade dos estabelecimentos e concentração geográfica**, oferecendo uma base quantitativa para discutir possíveis estratégias de entrada e posicionamento de uma cafeteria em Los Angeles.

> **Importante:** as conclusões sobre oportunidade comercial devem ser interpretadas como hipóteses derivadas dos dados analisados. Uma decisão de investimento exigiria análises adicionais de demanda, custos, concorrência, localização e viabilidade financeira.

---

## 📎 Materiais

- **Notebook:** `notebook.ipynb`
- **Dataset:** `datasets/rest_data_us_upd.csv`
- **Apresentação:** `apresentacao/apresentacao.pdf`
