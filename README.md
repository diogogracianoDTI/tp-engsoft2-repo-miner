# repo-maintenance-miner

Ferramenta de linha de comando para minerar repositórios e identificar sinais de problemas de manutenção/evolução, analisando atividade recente e estado das dependências (desatualização e vulnerabilidades conhecidas).

## Membros do Grupo

- Guilherme Gomes Palhares Gomide
- Diogo Alves Graciano
- Victor Yuji Yano
- Guilherme Novais de Souza

## Objetivo da Ferramenta

A CLI calcula um “termômetro de manutenção” a partir de:

- Atividade recente: total de commits em uma janela de tempo, dias desde o último commit, mediana de dias entre commits, merges, top autores com mais commits e mais recentes.
- Dependências: quais estão desatualizadas (comparação com o PyPI) e vulnerabilidades reportadas (OSV).

Os resultados podem ser exibidos no terminal ou exportados em JSON/CSV.

## Tecnologias Utilizadas

- Python 3.9+
- Typer (CLI)
- PyDriller (mineração de commits Git)
- Requests (HTTP)
- OSV API (vulnerabilidades)
- PyPI JSON API (últimas versões)
- Rich (tabelas bonitas no terminal)
- Pytest (testes)
- GitHub Actions (CI)

## Instalação

Pré‑requisitos: Python 3.9+ e pip.

1. Clone o repositório e acesse a pasta do projeto.
2. Instale em modo editável:

   ```bash
   pip install -e .
   ```

Isso instalará o comando `repo-miner`.

## Uso

Ajuda geral:

```bash
repo-miner --help
```

- Analisar atividade do repositório (ex.: últimos 365 dias):

```bash
repo-miner activity /caminho/para/repo --since-days 365
repo-miner activity /caminho/para/repo --since-days 365 --json-out atividade.json
```

Exemplo de saída (campos principais):

```json
{
  "commits_total": 123,
  "authors_total": 8,
  "days_since_last_commit": 2,
  "median_days_between_commits": 1,
  "merge_commits": 10,
  "top_authors": [
    { "author": "dev1@example.com", "commits": 40 },
    { "author": "dev2@example.com", "commits": 30 },
    { "author": "dev3@example.com", "commits": 20 },
    { "author": "dev4@example.com", "commits": 18 },
    { "author": "dev5@example.com", "commits": 15 }
  ],
  "recent_authors": [
    {
      "author": "dev2@example.com",
      "days_since_last_commit": 0,
      "commits": 30
    },
    {
      "author": "dev3@example.com",
      "days_since_last_commit": 1,
      "commits": 20
    },
    {
      "author": "dev5@example.com",
      "days_since_last_commit": 3,
      "commits": 15
    },
    {
      "author": "dev4@example.com",
      "days_since_last_commit": 4,
      "commits": 18
    },
    { "author": "dev1@example.com", "days_since_last_commit": 5, "commits": 40 }
  ]
}
```

- Analisar dependências do projeto atual (detecta `requirements.txt` e/ou `pyproject.toml`):

```bash
repo-miner deps /caminho/para/repo --offline                 # apenas parse, sem rede
repo-miner deps /caminho/para/repo --json-out deps.json      # JSON completo
repo-miner deps /caminho/para/repo --csv-out deps.csv        # CSV com lista de pacotes
```

- Rodar análise combinada (atividade + dependências) e obter um score 0–100:

```bash
repo-miner analyze /caminho/para/repo --since-days 365
repo-miner analyze /caminho/para/repo --json-out relatorio.json
```

Também é possível executar via `python main.py` durante o desenvolvimento.

## Como Executar os Testes Localmente

Instale as dependências de desenvolvimento e rode o pytest:

```bash
pip install -e .
pip install pytest
pytest -q
```

## Integração Contínua (CI)

Os testes são executados automaticamente no GitHub Actions em Python 3.9–3.12 a cada push e pull request (arquivo `.github/workflows/ci.yml`).
