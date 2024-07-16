# Documentazione: Consultazione Interventi di Dissesto 🏗️

Per tornare al README introduttivo, clicca [qui](../README.md).

💡 Si consiglia di utilizzare il nome e la descrizione di seguito indicati per l'e-service, in linea con le [_Buone pratiche per la nomenclatura e la descrizione degli e-service_](https://italia.github.io/pdnd-guida-nomenclatura-eservice/).

## Nome dell'e-service
Consultazione Interventi di Dissesto

## Descrizione dell'e-service
Restituisce la lista degli interventi di difesa del suolo finanziati dati un ente erogatore e un atto di finanziamento.

## Interfaccia OpenAPI

[Qui](../src/interventi_dissesto_openapi.yml) è disponibile l'interfaccia OpenAPI dell'e-service.

## Endpoint 🔗

**GET** `/elenco-interventi-dissesto`

Restituisce la lista degli interventi di difesa del suolo finanziati dati un ente erogatore e un atto di finanziamento.

### Parametri Query 🔍

- `id_ente` (obbligatorio): Codice identificativo ente erogatore (max 6 caratteri)
- `id_atto_fin` (obbligatorio): Codice/Denominazione sintetica atto di finanziamento (max 40 caratteri)
- `cup` (opzionale): Codice Unico di Progetto (CUP) associato al singolo intervento (max 15 caratteri)
- `clp` (opzionale): Codice Locale Progetto (CLP) (max 30 caratteri)
- `data_agg` (opzionale): Data ultimo aggiornamento informazioni dell'intervento (formato: YYYY-MM-DD)

### Risposta 📊

La risposta è un array di oggetti `InterventoDissesto`.

## Modello di Dati: InterventoDissesto 📋

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

## Codici e Valori 🏷️

### cat_diss (Categoria Dissesto)

- `F`: Frana
- `C`: Dissesto costiero
- `A`: Idraulico-alluvionale
- `I`: Incendio
- `V`: Valanga
- `M`: Misto
- `N`: Non definito

### Vocabolari Controllati 📚

I campi `tipo_diss`, `tipo_opere` e `id_passo` fanno riferimento a vocabolari controllati che saranno pubblicati sul National Data Catalog (NDC) italiano, accessibile tramite schema.gov.it. Questi vocabolari controllati garantiscono la standardizzazione e l'interoperabilità dei dati tra le diverse regioni e sistemi.

Gli utenti di questa API dovrebbero fare riferimento ai vocabolari pubblicati su NDC per ottenere l'elenco completo e aggiornato dei codici validi per questi campi. Questo approccio assicura che tutti gli enti utilizzino la stessa terminologia e codifica, facilitando l'aggregazione e l'analisi dei dati a livello nazionale.

## Gestione degli Errori ⚠️

L'API utilizza il formato problem+json per comunicare gli errori. In caso di errore, verrà restituito un oggetto con i seguenti campi:

- `status`: Codice di stato HTTP
- `title`: Breve descrizione del problema
- `detail`: Descrizione dettagliata del problema