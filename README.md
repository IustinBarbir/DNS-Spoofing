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

 

![](https://github.com/IustinBarbir/DNS-Spoofing/blob/main/Spoof.gif)
