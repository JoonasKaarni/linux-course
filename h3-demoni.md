# H3-Demoni

# x) Lue ja tiivistä

# Karvinen 2026: Apache installed with Ansible - quick notes
- Apache voidaan asentaa ja configata automaattisesti Ansiblella ja se antaa nettisivun osoitteessa http://localhost. Sivujen muokkaus onnistuu normaalikäyttäjänä ilman sudoa.
- Apache noudattaa package-file-service mallia, jossa ensin asennetaan paketti, muutetaan tiedoston asetuksia ja lopuksi käynnistetään palvelu.
- Daemonit kuten Apache noudattaa samaa toimintamallia. Konfiguraatiomuutokset astuu voimaan uudelleenkäynnistyksen jälkeen.

- Oma kysymys: Onko olemassa muunlaisia daemoneja?

# Ansible Community Documentation: Handlers: running operations on change
- Handlerit on tehtäviä, jotka suoritetaan pelkästään silloin, kun task aiheuttaa muutoksen.
- Handlereitä käytetään tyypillisesti palveluiden uudelleenkännistykseen konfiguraation muuttuessa.
- notify-avainsanalla task voi kutsua yhtä tai useampaa handleria.
- Handlerit suoritetaan määrittelyjärjestyksessä, ei notify-listan mukaan.
- Handlerit täytyy nimetä.
- Kaksi samannimistä handleria voi aiheuttaa konflikteja, jonka takia vain viimeisin määritelmä jää voimaan.
- Suoritus tapahtuu automaattisesti playn lopussa, mutta voidaan pakottaa aiemmin.

- Oma kysymys: Miksi handlerit suoritetaan määrittelyjärjestyksessä?

# Ansible-doc service
- Service-moduuli tarjoaa yhtenäisen tavan hallita palveluita eri käyttöjärjestelmissä ilman, että tarvitsee välittää taustalla olevasta init-järjestelmästä.
- Sillä varmistetaan palvelun tila sekä hallitsemaan palvelun elinkaarta automaation avulla.

enabled
- Määrittää, käynnistyykö palvelu automaattisesti järjestelmän käynnityessä.
- Arvot joko true, jolloin se käynnityy bootissa tai false jolloin se ei käynnisty.

name
- Kertoo, mitä palvelua hallitaan.
- Arvo on palvelun nimi kohdejärjestelmässä.

state
- Määrittää palvelun halutun tilan.
- Yleisimmät arvot ovat started, stopped, restarted ja reloaded.

EXAMPLES
<img width="275" height="153" alt="image" src="https://github.com/user-attachments/assets/21fbcf20-e08c-441b-a4af-9ebe464fe6dc" />

- Oma kysymys: onko reloaded yhtä yleisin käytetty kuin restarted?

# a) Apassi. Asenna Apache 2 käsin.

