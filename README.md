# Luo-kotiverkko-ja-asenna-Samba-palvelin

1. Tee pääkoneen IPv4 asetukset kuvan kaltaisiksi. Voit kohdassa Tiedot nimetä verkkoyhteyden haluamasi kaltaiseksi, mutta se ei ole merkityksellistä. (Kuvassa Linux Bazzite Gnome)
<img width="804" height="660" alt="Kuvakaappaus - 2026-01-07 01-10-23" src="https://github.com/user-attachments/assets/deb2551c-cceb-4bf7-84e7-0fb165d144d8" />

2. Tee 2-näyttökoneen IPv4 asetukset kuvan kaltaisiksi. (Kuvassa Linux Mint 22 Cinnamon)
<img width="712" height="488" alt="Kuvakaappaus 2026-01-07 01-32-19" src="https://github.com/user-attachments/assets/fdea503e-5c33-4197-b08c-aae71c31746f" />


_Huomaa ero: Pääkoneen osoite on 10.0.0.0 ja 2-koneen osoite on 10.0.0.1_

3. Se on siinä. Verkkoyhteys on luotu. (Muistit kai yhdistää koneet Ethernet-piuhalla). Joissakin Linux jakeluissa tulee vielä kohdassa Tiedot erikseen ruksia vaihtoehto "Yhdistä automaattisesti".

4. Halutessasi tarkista yhteyden toimivuus kirjoittamalla pääkoneen päätteessä komennon
```
ping 10.0.0.1
```
tai näyttökoneen päätteessä komennon
```
ping 10.0.0.0
```
5. Asenna Samba palvelin näyttökoneeseen

(Tämä ohje pätee Debian-pohjaisiin Linux jakeluihin, kuten: Debian, Linux Mint, Ubuntu, Kubuntu, MX-Linux, Pop OS ym.)

```
sudo apt install samba
```
5.1 Luo hakemisto Sambaa varten näyttökoneen kotihakemistoon (nimeä se haluamaksesi - tässä esimerkissä sen nimi on oma-samba)
```
mkdir ~/oma-samba
```

5.2 Muokkaa Samban asetustiedostoa niin että se tunnistaa uuden Samba-jakotiedostosi
```
sudo nano /etc/samba/smb.conf
```
Lisää sen loppuun seuraavat tiedot (tässä esimerkissä nimenä on oma-samba)
```
Comment = Oma Samba
[oma-samba]
read-only = no
browsable = yes
```
Paina sitten Ctrl+O tallentaaksesi ja Ctrl+X poistuaksesi
