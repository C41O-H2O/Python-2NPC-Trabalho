# HelpDesk Pro

Sistema interno de gestão de chamados desenvolvido em Python com orientação a objetos e exposto via API REST com Flask.

## Estrutura

- `helpdesk_TRIO_NOMES.py` - classes de dominio, excecoes e demonstracao executavel.
- `app.py` - API Flask com todos os endpoints JSON.
- `core.py` - wrapper de compatibilidade para a implementacao principal.
- `requirements.txt` - dependencia da API.

## Execucao

Instale as dependencias:

```bash
pip install -r requirements.txt
```

Execute a demonstracao do dominio:

```bash
python helpdesk_TRIO_NOMES.py
```

Execute a API:

```bash
python app.py
```

## Decisao de estrutura de dados

Os chamados sao armazenados em um dicionario, permitindo busca por numero em tempo constante $O(1)$, mesmo com grande volume de registros.