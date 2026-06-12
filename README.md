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

---

## 📚 Documentação da API

A API foi desenvolvida seguindo o padrão REST e troca de dados via **JSON**.
**URL Base Local:** `http://127.0.0.1:5000`

### 1. 📊 Painel (Dashboard)
- **`GET /painel`**: Retorna as estatísticas da central (chamados em atendimento, em atraso, técnicos disponíveis e top clientes).

### 2. 👨‍💻 Técnicos
- **`POST /tecnicos`**: Registra um novo técnico. *(Body: `nome` (str), `especialidades` (list), `capacidade_maxima` (int, opcional))*
- **`GET /tecnicos`**: Lista os técnicos. *(Query param opcional: `?disponivel=true|false`)*
- **`GET /tecnicos/ranking`**: Lista os técnicos ordenados pela quantidade de chamados resolvidos.

### 3. 🎫 Chamados
- **`POST /chamados`**: Abre a ocorrência. *(Body: `titulo` (str), `descricao` (str), `cliente` (str), `prioridade` (str - baixa, media, alta, critica))*
- **`GET /chamados`**: Lista chamados. *(Query params opcionais: `?status={status}` ou `?numero={id}`)*
- **`GET /chamados/<numero>`**: Busca exata de um chamado pelo seu ID.
- **`GET /chamados/em-atraso`**: Lista chamados cujo tempo decorrido ultrapassou o SLA estipulado pela prioridade.

### 4. 🔀 Andamento e Finalização
- **`PATCH /chamados/<numero>/status`**: Altera manualmente o status. *(Body: `novo_status` (str), `responsavel` (str))*
- **`PATCH /chamados/<numero>/resolver`**: Resolve um chamado. *(Body: `id_tecnico` (int), `descricao_solucao` (str))*

### 5. 🤖 Ativação do Sistema Automático
- **`POST /atribuicao/automatica`**: Varre chamados com status `aberto` e tenta designá-los dinamicamente aos técnicos com vagas e especialidades requeridas.