# Elenco Atti di Dissesto 📄

Per tornare al README introduttivo, clicca [qui](../README.md).

## Endpoint 🔗

**GET** `/elenco-atti-dissesto`

Recupera l'elenco degli atti di dissesto per un determinato ente erogatore regionale.

### Parametri Query 🔍

- `id_ente` (obbligatorio): Codice identificativo ente erogatore (max 6 caratteri)
- `id_atto_fin` (opzionale): Codice/Denominazione sintetica atto di finanziamento (max 40 caratteri)
- `data_agg` (opzionale): Data ultimo aggiornamento informazioni dell'atto (formato: YYYY-MM-DD)

### Risposta 📊

La risposta è un array di oggetti `AttoDissesto`.

## Modello di Dati: AttoDissesto 📋

- `id_ente`: string (max 6 caratteri)
  - Descrizione: Codice identificativo ente erogatore servizio (regioni = cod. ISTAT; Bolzano = 21; Trento = 22)
- `id_atto_fin`: string (max 40 caratteri)
  - Descrizione: Codice/Denominazione sintetica atto di finanziamento
- `attoesteso`: string (max 250 caratteri)
  - Descrizione: Denominazione estesa dell'atto di finanziamento
- `data_fin`: string (formato date)
  - Descrizione: Data di approvazione dell'atto di finanziamento
- `guri_bur`: string (max 250 caratteri)
  - Descrizione: Riferimenti della Gazzetta o Bollettino ufficiale della eventuale pubblicazione
- `link_atto`: string (max 250 caratteri)
  - Descrizione: Indirizzo web da cui è consultabile/scaricabile l'atto di finanziamento
- `data_agg`: string (formato date)
  - Descrizione: Data ultimo aggiornamento informazioni dell'atto