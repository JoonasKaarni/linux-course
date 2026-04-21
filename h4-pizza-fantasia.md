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

