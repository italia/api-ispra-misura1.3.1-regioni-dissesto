# API di ISPRA - Misura 1.3.1 - Atti e Interventi per il Dissesto 🌍

## Panoramica 🔎

Queste specifiche API definiscono dei template standard per l'esposizione di dati relativi agli atti e agli interventi di difesa del suolo finanziati da vari enti erogatori regionali. Questi template sono destinati all'uso sulla Piattaforma Digitale Nazionale Dati (PDND), permettendo a ISPRA (Istituto Superiore per la Protezione e la Ricerca Ambientale) di recuperare i dati per alimentare il sistema ReNDiS (Repertorio Nazionale degli interventi per la Difesa del Suolo).

## Implementazione 🛠️

Ogni regione implementerà queste API sulla PDND sotto forma di e-service, esponendo i propri dati specifici seguendo questa struttura comune. Questo permetterà a ISPRA di accedere a informazioni coerenti e strutturate da tutte le regioni, facilitando l'aggiornamento e la gestione del database nazionale ReNDiS.

## Documentazione Dettagliata 📚

Per informazioni dettagliate sugli e-service da implementare, fare riferimento alle interfacce OpenAPI nella cartella `docs`:

- [Elenco Atti di Dissesto](docs/README_atti_dissesto.md) 📄
- [Elenco Interventi di Dissesto](docs/README_interventi_dissesto.md) 🏗️

## Gestione degli Errori ⚠️

Le API utilizzano il formato problem+json per comunicare gli errori. In caso di errore, verrà restituito un oggetto con i seguenti campi:

- `status`: Codice di stato HTTP
- `title`: Breve descrizione del problema
- `detail`: Descrizione dettagliata del problema

## Riferimenti 🔗

- PDND (Piattaforma Digitale Nazionale Dati): [qui](https://www.interop.pagopa.it)
- ReNDiS (Repertorio Nazionale degli interventi per la Difesa del Suolo): [qui](http://www.rendis.isprambiente.it/rendisweb/)
- ISPRA (Istituto Superiore per la Protezione e la Ricerca Ambientale): [qui](https://www.isprambiente.gov.it/it)