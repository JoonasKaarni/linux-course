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



# b) Dolly.



# c) Doh!



# e) Gitanbile.
