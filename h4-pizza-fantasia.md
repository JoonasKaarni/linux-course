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

a) Räpylä
