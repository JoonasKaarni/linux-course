<img width="769" height="399" alt="image" src="https://github.com/user-attachments/assets/f993cec0-4b97-4163-ab4e-95c98c1aecd7" /># H3-Demoni

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
Aloitetaan asennus laittamalla muutaman komento.
~~~
sudo apt-get update
sudo apt-get install apache2
~~~
Kun se on ladannut käynnistetään ja tarkistetaan sen tila komennoilla:
~~~
sudo systemctl start apache2
sudo systemctl status apache2
~~~
<img width="697" height="103" alt="image" src="https://github.com/user-attachments/assets/d27723eb-5e4a-4bec-995d-c5762f7da5f8" />


Sitten testataan nettiselaimessa sivun toimivuus menemälle osoitteeseen http://localhost

<img width="912" height="297" alt="image" src="https://github.com/user-attachments/assets/794df87a-0a40-4ed9-aadb-df534088d5f9" />


Sitten loin oman sivun käyttäjälle. Ensin tein kansion komennolla
~~~
mkdir -p /home/joonas/publicsite
micro -p /home/joonas/publicsite/index.html
~~~
Sinne kirjoittelin pienen tekstin:
~~~
<h1>Hello Apache</h1>
~~~
Apache config seuraavaksi
~~~
sudo micro /etc/apache2/sites-available/publicsite.conf
~~~
Sinne tuli sisälle tämmöistä tekstiä:
~~~
<VirtualHost *:80>
    ServerName localhost
    DocumentRoot /home/joonas/publicsite/

    <Directory /home/joonas/publicsite/>
        Require all granted
    </Directory>
</VirtualHost>
~~~
Uudelleenkäynnistyksen jälkeen nettisivu toimii!!
<img width="507" height="215" alt="image" src="https://github.com/user-attachments/assets/867d700c-4f22-4797-9c6f-ad1ec5649209" />

# b) Moottorix. Asenna Nginx käsin
Ensin sammutin apachen, koska nginx ei toimi sen kanssa samanaikaisesti.
~~~
sudo systemctl stop apache2
sudo systemctl disable apache2
~~~
Sitten asennetaan Nginx seuraavasti:
~~~
sudo apt-get update
sudo apt-get install nginx
~~~
<img width="768" height="398" alt="image" src="https://github.com/user-attachments/assets/a47ddabe-db9d-48fa-b2a8-bda27da6a421" />

Käynnistetään Nginx seuraavaksi:
~~~
sudo systemctl enable nginx
sudo systemctl status nginx
~~~
<img width="801" height="215" alt="image" src="https://github.com/user-attachments/assets/da6b7a5d-9c2b-4c22-b28c-d803b204ae00" />


Pienien ongelmien jälkeen sain näkymän tällaiseksi:
<img width="849" height="312" alt="image" src="https://github.com/user-attachments/assets/37af6c0c-7b60-491e-a60a-97550f6494a7" />

Sitten muokataan sivun teksti sanomaan "Moottorix" ja tallennuksen jälkeen mennään Nginx sivun configiin komennolla 
~~~
sudo micro /etc/nginx/sites-available/default
~~~
Sinne lisäsin root kohtaan publicsiten ja indexin. Sitten testissä sivulla näkyy Moottorix!
<img width="512" height="200" alt="image" src="https://github.com/user-attachments/assets/c2cb6adc-0eef-4c61-b2e7-5ce6e331b181" />



