# API di ISPRA - Misura 1.3.1 - Atti e Interventi per il Dissesto

## Panoramica

Questa specifica API definisce un template standardizzato per l'esposizione di dati relativi agli atti e agli interventi di difesa del suolo finanziati da vari enti erogatori regionali. Questo template è destinato all'uso sulla Piattaforma Digitale Nazionale Dati (PDND), permettendo a ISPRA (Istituto Superiore per la Protezione e la Ricerca Ambientale) di recuperare i dati per alimentare il sistema ReNDiS (Repertorio Nazionale degli interventi per la Difesa del Suolo).

## Implementazione

Ogni regione implementerà questa API sulla PDND sotto forma di e-service, esponendo i propri dati specifici seguendo questa struttura comune. Questo permetterà a ISPRA di accedere a informazioni coerenti e strutturate da tutte le regioni, facilitando l'aggiornamento e la gestione del database nazionale ReNDiS.

## Endpoint

### 1. Elenco Atti di Dissesto

**GET** `/elenco-atti-dissesto`

Recupera l'elenco degli atti di dissesto per un determinato ente erogatore regionale.

#### Parametri Query

- `id_ente` (obbligatorio): Codice identificativo ente erogatore (max 6 caratteri)
- `id_atto_fin` (opzionale): Codice/Denominazione sintetica atto di finanziamento (max 40 caratteri)
- `data_agg` (opzionale): Data ultimo aggiornamento informazioni dell'atto (formato: YYYY-MM-DD)

#### Risposta

La risposta è un array di oggetti `AttoDissesto`.

### 2. Elenco Interventi di Dissesto

**GET** `/elenco-interventi-dissesto`

Recupera l'elenco degli interventi di difesa del suolo per un determinato atto di finanziamento.

#### Parametri Query

- `id_ente` (obbligatorio): Codice identificativo ente erogatore (max 6 caratteri)
- `id_atto_fin` (obbligatorio): Codice/Denominazione sintetica atto di finanziamento (max 40 caratteri)
- `cup` (opzionale): Codice Unico di Progetto (CUP) associato al singolo intervento (max 15 caratteri)
- `clp` (opzionale): Codice Locale Progetto (CLP) (max 30 caratteri)
- `data_agg` (opzionale): Data ultimo aggiornamento informazioni dell'intervento (formato: YYYY-MM-DD)

#### Risposta

La risposta è un array di oggetti `InterventoDissesto`.

### 3. Stato dell'Applicazione

**GET** `/status`

Ritorna lo stato dell'applicazione in formato problem+json.

## Modelli di Dati

### AttoDissesto

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

### InterventoDissesto

- `id_ente`: string (max 6 caratteri)
  - Descrizione: Codice identificativo ente erogatore servizio (regioni = cod. ISTAT; Bolzano = 21; Trento = 22)
- `id_atto_fin`: string (max 40 caratteri)
  - Descrizione: Codice/Denominazione sintetica atto di finanziamento
- `cup`: string (max 15 caratteri)
  - Descrizione: Codice Unico di Progetto (CUP) associato al singolo intervento
- `clp`: string (max 30 caratteri)
  - Descrizione: Codice Locale Progetto (CLP) utilizzato per identificare il progetto nell'applicazione WEB MOP (Monitoraggio Opere Pubbliche del MEF-RGS)
- `imp_fin`: number (double)
  - Descrizione: Importo assegnato all'ente proponente dall'atto di finanziamento
- `cat_diss`: string (1 carattere)
  - Descrizione: Categoria dissesto (vedi sezione "Codici e Valori" per i dettagli)
- `tipo_diss`: string (codice)
  - Descrizione: Codice della tipologia prevalente del dissesto
- `tipo_opere`: string (codice)
  - Descrizione: Codice della tipologia prevalente di opere
- `id_passo`: string (codice)
  - Descrizione: Codice id_passo corrispondente allo stato di attuazione
- `id_altro`: string (max 200 caratteri)
  - Descrizione: Altro codice o descrizione utilizzati per identificare il singolo intervento nell'atto di finanziamento
- `id_rendis`: string (max 15 caratteri)
  - Descrizione: Codice ReNDiS associato all'intervento
- `istat_prop`: string (max 20 caratteri)
  - Descrizione: Codice ISTAT dell'ente proponente
- `istat_att`: string (max 20 caratteri)
  - Descrizione: Codice ISTAT dell'ente attuatore (solo se diverso da proponente)
- `lat`: number (double)
  - Descrizione: Latitudine (N) del punto baricentrico dell'intervento
- `long`: number (double)
  - Descrizione: Longitudine (E) del punto baricentrico dell'intervento
- `titolo`: string
  - Descrizione: Titolo dell'intervento
- `località`: string
  - Descrizione: Località dell'intervento
- `provincia`: string
  - Descrizione: Provincia dell'intervento
- `comune`: string
  - Descrizione: Comune dell'intervento
- `data_agg`: string (formato date)
  - Descrizione: Data ultimo aggiornamento informazioni dell'intervento

## Codici e Valori

### cat_diss (Categoria Dissesto)

- `F`: Frana
- `C`: Dissesto costiero
- `A`: Idraulico-alluvionale
- `I`: Incendio
- `V`: Valanga
- `M`: Misto
- `N`: Non definito

### tipo_diss (Tipo Dissesto)

Il campo `tipo_diss` utilizza codici specifici per indicare il tipo di dissesto. Esempi includono codici per dissesti costieri, erosioni da incendio, frane, dissesti idraulici e valanghe.

### tipo_opere (Tipo Opere)

Il campo `tipo_opere` utilizza codici specifici per indicare il tipo di intervento, includendo categorie per interventi in aree costiere, su frane, idraulici, relativi a incendi e su valanghe.

### id_passo (Stato di Attuazione)

Il campo `id_passo` utilizza codici numerici per indicare lo stato di avanzamento dell'intervento, coprendo fasi di finanziamento, progettazione, esecuzione lavori, sospensione, revoca o conclusione.

### Vocabolari Controllati

È importante notare che i campi `tipo_diss`, `tipo_opere` e `id_passo` fanno riferimento a vocabolari controllati che saranno pubblicati sul National Data Catalog (NDC) italiano, accessibile tramite schema.gov.it. Questi vocabolari controllati garantiscono la standardizzazione e l'interoperabilità dei dati tra le diverse regioni e sistemi.

Gli utenti di questa API dovrebbero fare riferimento ai vocabolari pubblicati su NDC per ottenere l'elenco completo e aggiornato dei codici validi per questi campi. Questo approccio assicura che tutti gli enti utilizzino la stessa terminologia e codifica, facilitando l'aggregazione e l'analisi dei dati a livello nazionale.

## Gestione degli Errori

L'API utilizza il formato problem+json per comunicare gli errori. In caso di errore, verrà restituito un oggetto con i seguenti campi:

- `status`: Codice di stato HTTP
- `title`: Breve descrizione del problema
- `detail`: Descrizione dettagliata del problema

## Riferimenti

- PDND (Piattaforma Digitale Nazionale Dati): [qui](https://www.interop.pagopa.it)
- ReNDiS (Repertorio Nazionale degli interventi per la Difesa del Suolo): [qui](http://www.rendis.isprambiente.it/rendisweb/)
- ISPRA (Istituto Superiore per la Protezione e la Ricerca Ambientale): [qui](https://www.isprambiente.gov.it/it)