# h5 Gitar Hero

# x) Lue ja tiivistä.
# Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?
- Git tallentaa tilannekuvia koko projekista, ei pelkkiä muutoksia.
- Lähes kaikki toiminnot on paikallisia, eli Git on nopea ja toimii vaikka et ole yhteydessä nettiin.
- Git lisää dataa, joten historiatiedon menettäminen on vaikeaa.

Oma kysymys: Kuinka Git käsittelee tilanteen, jossa pushataan samaan tiedostoon samoihin kohtiin erilaisia muutoksia usealta tekijältä.

# Gitin käyttö on lähinnä 'git add --all && git commit; git pull && git push'.
- git add --all Lisää kaikki muutokset staging areaan, jossa on uudet, muokatut ja poistetut tiedot.
- && suorittaa seuraavan komennon, mutta pelkästään silloin kun edellinen osuus onnistui.
- git commit tallentaa staging arean muutokset uutena snapshottina eli tilannekuvana repositoryyn.
- ; puolipiste on erotin, eli seuraava komento suoritetaan riippumatta edellisen onnistumisesta.
- git pull hakee muutokset etärepositorysta ja mergee eli yhdistää ne paikalliseen haaraan. Komennot git fetch + git merge tekee saman.
- && sama kuin aikaisemmin.
- git push lähettää paikalliset commitit etärepositoryyn, kuten Githubiin. Sitten kaikki muut, joilla on access repositoryyn pääsevät näkemään sen.

# a) Online. Tee uusi varasto GitHubiin
Aloitin menemäällä Githubiin ja luomalla tuon uuden repon. Kaikki tiedot täytetty oikein ja siinä se on:
<img width="808" height="594" alt="image" src="https://github.com/user-attachments/assets/180c5d4a-70bc-4ccf-b16d-70c3f62894ab" />



# b) Dolly.
Aloitin kloonaamalla repon komennolla:
~~~
git clone git@github.com:JoonasKaarni/sunshine.git
~~~
<img width="848" height="137" alt="image" src="https://github.com/user-attachments/assets/c6ddf064-9884-4af6-98f8-c80c0f09883c" />

Sitten mentiin uuden repon sisään.
~~~
cd sunshine
~~~
Ja aloitin muutosten teon muokkaamalla README.md:tä

<img width="597" height="140" alt="image" src="https://github.com/user-attachments/assets/ace9736e-6299-49a4-b67b-cc7d9857ad31" />

Sitten pitää puskea muutokset Githubiin seuraavilla komennoilla:
~~~
git add --all
git commit
git pull
git push
~~~
Sitten voidaan katsoa muutoksia suoraan terminaalista komennolla:
~~~
git log --patch
~~~
Mutta enemmän kiinnostaa tuliko ne sinne githubiin. Katsotaanpas!

<img width="547" height="584" alt="image" src="https://github.com/user-attachments/assets/765bfb39-57a0-4542-abee-514831a37d5e" />

Ja siellähän ne onkin. Toimi!

# c) Doh!
Aloitin tekemälle huonon muutoksen README.md. Nyt siellä on pelottava virus!

<img width="574" height="112" alt="image" src="https://github.com/user-attachments/assets/82b2e159-c0a4-4185-b7ea-0644f4b51a49" />

Tarkistan tilanteen komennolla:
~~~
git status
~~~
Tilanne on tämä:

<img width="728" height="219" alt="image" src="https://github.com/user-attachments/assets/10e0448f-dfd3-4fc6-8913-97fd63eece0a" />

Tämä virus on poistettava heti!!! Sen takia resetoin gitin ja poistan tämän kamalan viruksen, jota en ole vielä pushannut onneksi.
~~~
git reset --hard
~~~

<img width="611" height="144" alt="image" src="https://github.com/user-attachments/assets/262107e6-812b-466d-b461-03d3145c0db7" />

Huh... Virus poistettu ja päivä pelastettu.

# d) Tukki
Ensin tarkistetaan commit-historia komennolla:
~~~
git log --patch
~~~
Siinä näkyy muutokset:

<img width="899" height="578" alt="image" src="https://github.com/user-attachments/assets/300ce5c2-b188-45ea-9ff3-9f99af498c42" />

Tarkistin myös käyttäjätiedot ja ne ovat oikein!

<img width="636" height="99" alt="image" src="https://github.com/user-attachments/assets/c5582308-168d-46cd-bcf1-ac08b1c3a335" />


# e) Gitanbile.
Hommat alkavat sillä, että luon sunshine repoon ansible kansion:
<img width="657" height="58" alt="image" src="https://github.com/user-attachments/assets/dceed4d6-df85-4217-a526-bdbc362bcde9" />
site.yml:iin tuli sisälle erittäin simppeli playbook:
~~~
# site.yml
- hosts: localhost
  tasks:
    - name: Hello
      debug:
        msg: "Hello World"
~~~
Sitten ajettiin ansible ja tulokset olivat hyvät!
<img width="917" height="361" alt="image" src="https://github.com/user-attachments/assets/18922842-c1c9-4839-ab6d-6fbdd4f41fb5" />

Sitten mentiin ulos ansible kansiosta ja lisättiin gitillä kansio GitHubiinkin.
~~~
cd ..
git add ansible/
git commit
git pull
git push
~~~
Pushin jälkeen ansible näkyykin Githubissa!
<img width="528" height="313" alt="image" src="https://github.com/user-attachments/assets/0bf01952-12e3-4867-aeb0-492895394ed8" />

Sitten tein muutoksen site.yml:iin ja ajoin playbookin uudelleen:
<img width="908" height="385" alt="image" src="https://github.com/user-attachments/assets/7946c6b9-373d-443a-b93b-5a4a0cc9d92b" />

Se toimi, sitten pitääkin vain committaa ja pushata, jonka jälkeen checkasin Githubin ja sinne se texti tuli!
<img width="492" height="374" alt="image" src="https://github.com/user-attachments/assets/30219387-c610-49bd-a389-59cb29f1944d" />

# f) Pari
Pari on!!

# Lähteet
Karvinen 2026: https://terokarvinen.com/palvelinten-hallinta/
Chacon and Straub 2014: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
ChatGPT: Ongelmien ratkonta rankkoina aikoina.
