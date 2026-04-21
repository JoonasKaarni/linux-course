# h4 Pizza Fantasia

# x) Lue ja tiivistä
4.12.1 Size and Complexity of Some DSLs
- DSL:t voivat olla erittäin laajoja ja monimutkaisia. Esimerkkinä Saltin DSL sisältää satoja toimintoja ja kymmeniä tuhansia rivejä dokumentaatiota.
- Salt hyödyntää Jinja2-mallipohjia koodin generoinnissa ja se isää abstraktiotasoa ja vaikeuttaa kokonaisuuden hahmottamista.
- Puppet tarjoaa vähemmän toimintoja, mutta käyttää omia erityisiä käsitteitä perinteisten ohjelmointirakenteiden sijaan.

4.12.2 Use of DSL Functions in Case Configuration
- Vaikka johtavat konfiguraatiohallintatyökalut tarjoaa huomattavan määrän funktiota järjestelmän hallintaan, näyttää siltä että pieni joukko funktioita kattaa suuren osan käytännön käyttötapauksista.
- Yleisimmiten käytetyt funktiot ovat sellaisia, joita voitaisi odottaa tavallisten ohjelmointimallien perusteella, kuten daemonien asennus package-file-service -mallilla.
-Analyysin osoittaa, että vain harvoja funktioita ja kontrollirakenteita käytetään usein, vaikka DSL tarjoaa laajan valikoiman erilaisia toimintoja.

4.12.3.1 Dependencies Between Main Functions
- Järjestelmän tulisi olla idempotentti, eli muutoksia tehdään ainoastaan silloin, kun järjestelmä ei ole jo halutussa tilassa.
- Suurin osa konfiguraatiofunktioista suorittaa lopulta natiivin komennon kohdejärjestelmässä, kuten pakettihallinnan komentoja.
- Vaikka tarjolla on monia toimintoja, suurin osa konfiguraatiosta voidaan rakentaa pienen joukon perusfunktioiden varaan.

# a) Räpylä. Asenna itse valitsemasi demoni käsin.
Valitsin demoniksi fail2ban:in. Aloitin päivittämällä ja sen jälkeen lataamalla demonin.
~~~
sudo apt update
sudo apt install fail2ban
~~~
Latauksen valmistuttua testasin toimiiko se.
~~~
sudo systemctl status fail2ban
sudo fail2ban-client status
~~~
Demoni toimii käsin asennettuna.

<img width="871" height="281" alt="image" src="https://github.com/user-attachments/assets/96348a8d-e0b1-4ed3-b119-fe4d9786b3ab" />

.

<img width="566" height="76" alt="image" src="https://github.com/user-attachments/assets/dc60a8af-3db1-4445-b9c9-b2433b3aa988" />

# b) Automaatti. Automatisoi valitsemasi demonin asennus Ansiblella.
Aloitetaan automatisointi lisäämällä fail2ban playbookkiin.

<img width="184" height="184" alt="image" src="https://github.com/user-attachments/assets/fe614158-cb34-420c-aa3b-120a0a154946" />

Sitten loin fail2ban roolin seuraavalla komennolla. Loin myös ansibleen tiedoston inventory.
~~~
ansible-galaxy init ansible/roles/fail2ban
cd ansible
micro inventory
~~~
Sitten kirjoittelin fail2ban/tasks/main.yml:iin juttuja.

<img width="350" height="298" alt="image" src="https://github.com/user-attachments/assets/8011fd73-c7f5-4212-9873-9707ef8a1de3" />

Lopuksi ajan sen ja hyvältä ne näyttääkin.
~~~
ansible-playbook -i inventory site.yml -K
~~~

<img width="419" height="119" alt="image" src="https://github.com/user-attachments/assets/bb07ef2e-1920-441a-ab3e-25914e266f47" />

# c) Asetus. Muuta asetustiedostoa herralla (master, "control node") ja aja ansible uudestaan.

fail2bannin config lötyy paikasta /etc/fail2ban/jail.local. Teen aluksi templaten paikkaan ansible/roles/fail2ban/templates/jail.local.j2. Sisältö näyttää tältä:

<img width="291" height="119" alt="image" src="https://github.com/user-attachments/assets/f008939f-0448-47fb-9775-a0b3f0ab34bc" />

Sitten lisätään b-kohdassa tehtyyn ansible/roles/fail2ban/tasks/main.yml:iin uusi kohta.

<img width="385" height="130" alt="image" src="https://github.com/user-attachments/assets/a6a1c15b-24ef-4fc4-ad72-30602ead0dc0" />

Lisätään tekstiä myös handlersiin ja defaultsiin.

<img width="371" height="192" alt="image" src="https://github.com/user-attachments/assets/f27ef0cc-d6c0-4e08-aabe-8a19516b0718" />
.
<img width="361" height="133" alt="image" src="https://github.com/user-attachments/assets/4fcd0891-2990-409f-9df9-b75b551250c9" />

Suoritin playbookin ja laitettu bantime näkyy tuossa.
<img width="869" height="454" alt="image" src="https://github.com/user-attachments/assets/42229514-38cf-4738-92d7-63a6b4b48a3d" />

Vaihdan sitten bantimeksi 1200 ja playbookin jälkeen siinä se on!
<img width="781" height="444" alt="image" src="https://github.com/user-attachments/assets/724b863e-a4af-4c7b-8dd3-6b43a6fa78ef" />

# d) Paikka remonttiin. Riko jotain asetuksia.

Rikoin paikkoja poistamalla demonin seuraavasti.
~~~
sudo apt purge fail2ban -y
sudo rm -rf /etc/fail2ban
~~~
<img width="873" height="437" alt="image" src="https://github.com/user-attachments/assets/70c7370f-b678-407f-a050-5fef6cb2fc49" />

Sitten suoritin playbookin uudestaan ja checkasin fail2banin statuksen heti sen jälkeen. Tilanne korjattu ja kaikki ok!

<img width="875" height="652" alt="image" src="https://github.com/user-attachments/assets/728b198e-8823-499b-97d2-3a99702c9240" />

# e) Idempotentti. Osoita, että tilasi on idempotentti.

Kuvan teksti on pientä, jotta sain koko homman näkymään. Tässä eka playbook ja sitten toinen perään.
<img width="932" height="692" alt="image" src="https://github.com/user-attachments/assets/c0308fb5-ca59-4823-91ca-10b45f0e5997" />
.
<img width="717" height="705" alt="image" src="https://github.com/user-attachments/assets/5b33bdcf-82e8-4b70-808b-35e86f0373cb" />
.

# Lähteet
Karvinen 2026: https://terokarvinen.com/palvelinten-hallinta/#h3-demoni
ChatGPT: Ongelmien ratkonta, varsinkin idempotentti osiossa...


