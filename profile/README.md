# Sitting Spot

![Architecture](https://drive.google.com/uc?id=1zdPsijnLdop0RNGODiwsK2JCv_GjBfz1)


## Sitting Spot Data Layer (Leo)

gestisce l'access al database dei sitting spot.

- GET sitting spot by parameters
- POST sitting spot

- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [x] Data model doc
- [x] Data model impl
- [ ] Docker

## Review Data Layer (Davide)

gestisce l'accesso al database delle review.

- GET list of review by sitting spot
- POST review of a sitting spot

- [x] Api doc
- [ ] Api impl
- [ ] Logic impl
- [ ] Data model doc
- [ ] Data model impl
- [ ] Docker

## Query Data Layer (Leo)

gestisce l'accesso al database delle query effettuate.

- GET query that are inside a range
Vari get per cercare roba
- POST new query

- [x] Api doc
- [ ] Api impl
- [ ] Logic impl
- [x] Data model doc
- [x] Data model impl
- [ ] Docker

## Search Adapter (Leo)

Permette di cercare sitting spot su OSM e dal database interno.
Dove per sitting spot si intende tutto ciò che potrebbe permettere di sedersi.
E salva le entrate su Sitting Spot Data Layer.

Lista di cose che cerca:
- 

- GET query (query: x,y,raggio,tag)

- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [ ] Docker

## Moderation (Davide)

Servizio che integra un servizio esterno per rilevare profanità nel testo.

- POST review -> si/no? oppure censura

- [x] Api doc
- [ ] Api impl
- [ ] Logic impl
- [ ] Docker

## Tag Extractor (Davide)

Dalla review cerca dei pattern predefiniti per aggiungere dei tag agli oggetti.
Tipo "comodo" "luminoso" ecc.

- POST review -> list<tag>

- [x] Api doc
- [ ] Api impl
- [ ] Logic impl
- [ ] Docker

## Search Logic (Leo)

Prende in carico una query di ricerca, utilizzando anche il query optimizer per fare short circuit del risultato, se no chiama search adapter.
Dopo che ha fatto una query aggiorna query optimizer.

- GET query (query: x,y,raggio,tag)

- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [ ] Docker

## Query Optimizer (Leo)

Prende in carico i dati di una query e determina se c'è un risultato precedente che può essere utilizzato per rispondere.

- GET optimization (query: x,y,raggio,tag)

- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [ ] Docker

## Search Process Layer (Leo)

permette di cercare sitting spots.

- GET sitting spot (parametri: x,y,raggio?,tag)

- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [ ] Docker

## Review Process Layer (Davide)

permette di aggiungere o leggere review.

- GET review da id
- POST review da id
- [x] Api doc
- [x] Api impl
- [ ] Logic impl
- [ ] Docker

- [ ] Api doc
- [ ] Api impl
- [ ] Logic impl
- [ ] Docker





