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
# e) Gitanbile.

