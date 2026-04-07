# H2 Voileipä

# Sudo ilman salasanaa
Aloitetaan lisäämässä uusi käyttäjä antero komennolla $ sudo adduser antero. Lisätään myös ryhmä nimeltä sudoless komennolla $ sudo groupass sudoless. Sitten luodaan uusi sudoers sääntö komennolla $ sudo visudo /etc/sudoers.d/sudoless. Sinne sisälle kirjoitaan %sudoless ALL= (ALL) NOPASSWD: ALL. Lopuksi vielä testataan toimintaa. Ennen sitä kirjaudutaan ulos, jotta uudet ryhmät päivittyvät. Sen jälkeen kirjaudutaan uuteen käyttäjään komennolla $ ssh antero@localhost ja unohdetaan salasana komennolla $ sudo -k. Sitten testiksi $ sudo echo "See you at TeroKarvinen.com" ja lopputuloksen pitäisi näyttää tältä:
<img width="798" height="100" alt="image" src="https://github.com/user-attachments/assets/2586e360-3f5a-4f41-9412-0d1b499ffc51" />

# Salasanaton Sudo Ansiblen kanssa
