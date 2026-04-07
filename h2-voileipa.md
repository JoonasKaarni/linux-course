# H2 Voileipä

# Sudo ilman salasanaa
- Aloitetaan lisäämässä uusi käyttäjä antero komennolla **$ sudo adduser antero** 
- Lisätään myös ryhmä nimeltä sudoless komennolla **$ sudo groupass sudoless**
- Sitten luodaan uusi sudoers sääntö komennolla **$ sudo visudo /etc/sudoers.d/sudoless**
- Sinne sisälle kirjoitaan **%sudoless ALL= (ALL) NOPASSWD: ALL**
- Lopuksi vielä testataan toimintaa. Ennen sitä kirjaudutaan ulos, jotta uudet ryhmät             päivittyvät.
- Sen jälkeen kirjaudutaan uuteen käyttäjään komennolla **$ ssh antero@localhost**
- Ja unohdetaan salasana komennolla **$ sudo -k**
- Sitten testiksi **$ sudo echo "See you at TeroKarvinen.com"**
- Ja lopputuloksen pitäisi näyttää tältä:
<img width="798" height="100" alt="image" src="https://github.com/user-attachments/assets/2586e360-3f5a-4f41-9412-0d1b499ffc51" />

# Salasanaton Sudo Ansiblen kanssa
- Aloitetaan luomalla kaksi roolia, jotka ovat **world** ja **antero**. Niille tulee molemmille alakansio **tasks**, sekä molemmille **main.yml-tiedosto**, tähän malliin:
<img width="355" height="250" alt="image" src="https://github.com/user-attachments/assets/911bb5dc-f5f4-4d19-be78-36bed7c7d231" />
- Sitten kirjoitellaan antero-roolin mainiin vähäsen tekstiä. Sinne tulee ryhmä, käyttäjä, avain ja copy.
- Seuraavana puun pohjalla olevaan site.yml-tiedostoon kirjoitetaan tekstiä: - hosts: all, become: true, roles: - world, - antero
- Nyt kun laittaa $ ansible-playbook site.yml niin saa valituksen, että sudo tarvitsee salasanan. Se onnistuu komennolla **$ ansible-playbook site.yml --ask-become-password** tai lyhennettynä **$ ansible-playbook site.yml -K** tekee saman asian. Näyttää tältä:
<img width="893" height="332" alt="image" src="https://github.com/user-attachments/assets/f6c39627-87d0-4aab-acf7-6d80460d1a56" />


# Ansiblen sisäänrakenntettu dokumentaatio
- Ansiblen sisäänrakennettua dokumentaatiota tarkastellaan komennolla $ ansible-doc (moduuli esim. copy)

# copy-moduuli
- Moduulia käytetään tiedostojen kopioimiseen hallintakoneelta kohdekoneelle. Sillä voidaan asettaa tiedoston omistaja, ryhmä ja käyttöoikeudet.
- Optiot ovat:
    - content, kirjoittaa tiedoston sisällön suoraan playbookkiin ilman erillistä lähdetiedostoa.
    - dest, kohdekoneen polku, johon tiedosto kopioidaan.
    - src, lähdetiedoston sijainti Ansible-hallintakoneella.
    - owner, määrittää tiedoston omistajan.
    - group, määrittää tiedoston ryhmän.
    - mode, määrittää tiedoston käyttöoikeudet, kuten tehtävässä käytetty 0644.
  esimerkki:
- name: Copy role
  ansible.builtin.copy:
    src: main.yml
    dest: /roles/antero2
    owner: root
    group: root
    mode: "0644"

# apt-moduuli
- Moduulia käytetään pakettien hallintaan Debian-pohjaisissa järjestelmissä. Sen avulla voidaan asentaa, päivittää tai poistaa paketteja sekä päivittää pakettivarastojen välimuisti.
- Optiot ovat:
    - name, asennettavan tai poistettavan paketin nimi.
    - state, määrittää paketin tilan. Yleiset arvot ovat: present, absent, latest.
    - update_cache, päivittää pakettilistan ennen paketin asennusta.
  esimerkki:
- name: Install nginx
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: yes

# file-moduuli
- Moduulia käytetään tiedostojen ja hakemistojen ominaisuuksien hallintaan. Sillä voidaan luoda hakemistoja, poistaa tiedostoja, asettaa oikeuksia tai luoda symbolisia linkkejä.
- Optiot ovat:
    - path, tiedoston tai hakemiston polku.
    - recurse, jos asetettu tru, oikeudet muutetaan rekursiivisesti hakemiston sisällä.
    - src, lädhepolku symboliselle linkille.
    - state, määrittää objektin tilan.
    - owner, omistaja.
    - group, ryhmä.
    - mode, tiedoston käyttöoikeudet.
  esimerkiksi:
- name: Create directory
  ansible.builtin.file:
    path: /tmp/testdir
    state: directory
    owner: root
    group: root
    mode: "0644"

# user-moduuli
- Moduulia käytetään käyttäjien hallintaan Linux-järjestelmissä. Sen avulla voidaan luoda tai poistaa käyttäjiä.
- Optiot ovat:
    - name, nimi.
    - create_home, määrittää luodaanko kotihakemisto.
    - comment, kuvaus, usein koko nimi.
    - groups, lista ryhmistä joihin käyttäjä lisätään.
    - shell, käyttäjän oletusshell.
    - state, käyttäjän tila.
    - system, jos true, luodaan järjestelmäkäyttäjä.
  esimerkiksi:
- mame: Create user
  ansible.builtin.user:
    name: antero
    comment: "Antero Antero"
    create_home: yes
    groups: ansible
    shell: /bin/bash
    state: present

# authorized_key
- Moduulia käytetään SSH-avainten lisäämiseen käyttäjän authorized_keys-tiedostoon.
- Optiot ovat:
    - user, käyttäjä, jonka avain lisätään.
    - key, lisättävä julkinen SSH-avain.
 esimerkiksi:
- name: Add SSH key
  ansible.builtin.authorized_key:
    user: antero
    key: "ssh-ed25519 AAAAbhbhdhCCdhdhd..."

# Lähteet
Tero Karvinen 2026 https://terokarvinen.com/palvelinten-hallinta/#h1-hei-ansiblen-maailma
ChatGPT, osittain tekstin luonnissa ja kääntämisessä.
