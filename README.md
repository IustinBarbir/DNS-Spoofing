# Securitatea retelelor de calculatoare: Tema 2 - DNS Spoofing
## Barbir Iustin MSI1

### 1.	Configurarea mediului de test:
Am folosit doua masini virtuale:
1.	Masina atacatorului: Kali Linux (IP 192.168.56.7)
2.	Masina victimei: Ubuntu (IP 192.168.56.4)
Mașinile au fost conectate printr-un NAT (MyNAT, configurat pentru laboratoarele precedente), permițând comunicația între ele
Pe mașina atacatorului s-a configurat un server Apache pentru a servi o pagină web falsă. In plus, s-a folosit dsniff. 
Pe masina atacatorului am modificat fisierele:
-	/etc/hosts (adaugand linia 192.168.56.7 www.victima.com) 
-	/etc/ettercap/etter.dns (www.victima.com A 192.168.56.7)
-	/etc/apache2/sites-available/000-default.conf (ServerName www.victima.com)
-	/etc/apache2/ports.conf (Listen 80)


### 2.	Atacul de DNS Spoofing:
S-a folosit Ettercap pentru a efectua un atac de tip ARP spoofing și DNS spoofing. 
Ettercap a fost configurat pentru a intercepta cererile DNS și a redirecționa traficul către serverul Apache fals, folosind fișierul de configurare etter.dns.
S-au folosit doua terminale:
-	unul pentru ettercap: 
> sudo ettercap -T -M arp:remote /192.168.56.4// /192.168.56.1// -P dns_spoof
-	unul pentru dnsiff:
> sudo dnsspoof -i eth0

### 3.	Redirecționarea HTTP:
Pentru a asigura că traficul HTTP este redirecționat către serverul fals, s-a modificat configurația serverului Apache pentru a servi conținutul web fals doar prin HTTP.
Ettercap a fost rulat cu opțiunea de redirecționare HTTP activată.
sudo a2dissite default-ssl

### Rezultatul
Atacatorul a reușit să redirecționeze traficul DNS și HTTP către serverul fals, astfel încât când victima a încercat să acceseze un site web legitim, in cazul nostru tryhackme.com, a fost îndrumată către pagina web falsificată găzduită de serverul Apache al atacatorului.

 

![](https://github.com/IustinBarbir/DNS-Spoofing/blob/main/Spoof.gif)
