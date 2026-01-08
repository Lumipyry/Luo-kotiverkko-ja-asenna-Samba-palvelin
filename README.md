# Luo-kotiverkko-ja-asenna-Samba-palvelin

1. Tee pääkoneen IPv4 asetukset kuvan kaltaisiksi. Voit kohdassa Tiedot nimetä verkkoyhteyden haluamasi kaltaiseksi, mutta se ei ole merkityksellistä. (Kuvassa Linux Bazzite Gnome)

<img width="804" height="660" alt="Kuvakaappaus - 2026-01-07 01-10-23" src="https://github.com/user-attachments/assets/deb2551c-cceb-4bf7-84e7-0fb165d144d8" />

2. Tee 2-näyttökoneen IPv4 asetukset kuvan kaltaisiksi. (Kuvassa Linux Mint 22 Cinnamon)

<img width="712" height="488" alt="Kuvakaappaus 2026-01-07 01-32-19" src="https://github.com/user-attachments/assets/fdea503e-5c33-4197-b08c-aae71c31746f" />

*
_Huomaa ero: Pääkoneen osoite on 10.0.0.0 ja 2-koneen osoite on 10.0.0.1_. Molemmissa yhteysmuodon tulee olla _Manuaalinen_.

*

3. Se on siinä. Verkkoyhteys on luotu. (Muistit kai yhdistää koneet Ethernet-piuhalla). Joissakin Linux jakeluissa tulee vielä kohdassa Tiedot erikseen ruksia vaihtoehto "Yhdistä automaattisesti".

4. Halutessasi tarkista yhteyden toimivuus kirjoittamalla pääkoneen päätteessä komennon
```
ping 10.0.0.1
```
tai näyttökoneen päätteessä komennon
```
ping 10.0.0.0
```
# Asenna Samba palvelin näyttökoneeseen

1. Asenna Samba. (Tämä ohje pätee Debian-pohjaisiin Linux jakeluihin, kuten: Debian, Linux Mint, Ubuntu, Kubuntu, MX-Linux, Pop OS ym.)

```
sudo apt install samba
```
2. Luo hakemisto Sambaa varten näyttökoneen kotihakemistoon (nimeä se haluamaksesi - tässä esimerkissä sen nimi on XXXXXX) YYYYY on käyttäjätunnuksesi
```
mkdir /home/YYYYY/XXXXXX
```

3. Muokkaa Samban asetustiedostoa niin että se tunnistaa uuden Samba-jakotiedostosi
```
sudo nano /etc/samba/smb.conf
```
4. Lisää sen loppuun seuraavat tiedot (tässä esimerkissä Sambajaon nimenä on XXXXXX). YYYYY on käyttäjätunnuksesi
```
[XXXXXX]
path = /home/YYYYY/XXXXXX
read-only = no
browsable = yes
writable = yes
guest ok = yes
```
<img width="798" height="612" alt="Kuvakaappaus 2026-01-08 23-45-46" src="https://github.com/user-attachments/assets/4eb3cec9-a481-4ece-b2cf-96df7a07e22a" />


*
5. Paina sitten `Ctrl+O` tallentaaksesi ja `Ctrl+x` poistuaksesi

*

6. Käynnistä Samba
```
sudo service smbd restart
```

7. Aseta Samba käyttäjä ja salasana (`XXXXXX on käyttäjätunnuksesi näyttökoneessa`)
```
sudo smbpasswd -a XXXXXXX
```
8. Jos sinulla on ufw-palomuuri käytössä - salli Samba
```
sudo ufw allow samba
``````
9. Käynnistä kone uudelleen.

Pääkoneen tiedostonhallinnassa kohdassa Verkko pitäisi nyt näkyä Samba-hakemistosi (esimerkissä oma-samba). Avattaessa se kysyy käyttäjätunnusta ja salasanaa.

Käyttäjätunnus on
```
Näyttökoneen käyttäjätunnus eli XXXXXX
```
ja salasana on juuri lisäämäsi sambasalasana 
```
eli salasana jonka lisäsit komentoon smbpasswd
```
