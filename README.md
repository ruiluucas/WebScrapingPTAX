# PTAX / WDOFUT — API de coleta e análise

Coleta de dados cambiais brasileiros via **API oficial do Banco Central (PTAX)** e correlação com o
**WDOFUT** (mini-dólar futuro da B3), exposta como API Flask.

## Componentes

| arquivo | o que faz |
|---|---|
| `app.py` | API Flask com endpoints `/ptax` e `/economic-calendar` |
| `bcb` | cliente da API do BCB (endpoint `CotacaoMoedaDia`), consulta por data |
| `investpy` | calendário econômico (EUA + Brasil) por intervalo de datas |
| `dol.ipynb` | notebook de análise: correlação, estatísticas, séries |
| `WDOFUT_F_0_Diário.csv` | base histórica do mini-dólar |
| `base.xlsx` | base auxiliar de trabalho |

## Endpoints

**`GET /ptax?date=MM/DD/AAAA`**
Retorna a cotação de **venda do dólar (PTAX)** para a data informada. Sem parâmetro, usa o **último dia
útil** (calculado com `BDay` do pandas).

```json
{ "code": 200, "date": "...", "cotacaoVenda": ... }
```

**`GET /economic-calendar`**
Calendário econômico dos EUA e Brasil em JSON.

## Uso

```bash
pip install flask flask-cors bcb pandas investpy
python app.py
```

## Nota sobre dependências

`investpy` **quebrou** (descontinuado — dependia de scraping do investing.com, que bloqueou). Esse endpoint
não funciona mais como está; a parte do BCB (`bcb`) permanece válida porque usa a API oficial.

## Stack

`Python` · `Flask` · `flask-cors` · `bcb` (BCB) · `investpy` · `pandas` · `numpy` · `Selenium`

## Contexto

Projeto de 2023 para alimentar análise cambial com dado oficial do BCB em vez de scraping de site.
