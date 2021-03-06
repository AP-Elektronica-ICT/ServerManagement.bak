# 3. Monitoring en logging

## 3.1 Analyse logbestanden
Logbestanden vind je op Linux systemen terug in de map ``/var/log``.

In deze folder staan de logbestanden van verschillende services.
Voor enkele services kan je de bestanden in een aparte folder terugvinden. (bijv. 'apache2', 'mysql', 'squid',...)
Welke folders en bestanden hier beschikbaar zijn hangt af van de geïnstalleerde software op je systeem.

Jammer genoeg is er niet één exact formaat waarin alle logfiles worden neergeschreven, maar de meeste logbestanden volgen wel een relatief vast stramien qua naamgeving.

De meeste processen hebben een aantal verschillende logbestanden.
 * .err / error.log: foutmeldingen (fouten bij werking van een service, fouten bij opstarten,...)
 * .info / info.log: informatieve boodschappen (om te zien wat een service doet tijdens de normale werking)
 * .warn / warning.log: waarschuwingen

De recente logbestanden zijn steeds rechtstreeks te lezen als tekstbestand.
Als je systeem al een langere tijd actief is zullen er gecomprimeerde archieven van de oude logbestanden aangemaakt worden. (bijv. 'daemon.log.2.gz')

Meer info: 
 * http://www.debianhelp.co.uk/logwatch.htm
 * https://help.ubuntu.com/community/LinuxLogFiles
 * http://askubuntu.com/questions/186276/where-are-all-the-major-log-files-located

Bestanden bekijken:
 * ``nano`` open een bestand in een teksteditor (dit is meestal niet wat je wil wanneer je logfiles bekijkt)
 * ``cat`` print de volledige inhoud van een logfile af (dit werkt nu, maar als je logbestand zeer groot is zal dit zeer lang duren)
 * ``tail`` print de laatste 10 regels van een bestand af
 * ``grep`` filter de output van cat (of tail) om te zoeken naar een bepaalde string.
 * Sommige logbestanden mag je als normale user niet bekijken. (met ``sudo su`` kan je snel als root user de bestanden bekijken)
 
Voorbeeld: ``cat /var/log/apache2/access.log | grep 'Mozilla'``

Zoek volgende informatie op in de logbestanden van je server.
Moesten deze events nog niet zijn opgetreden, doe dit dan even zelf of vraag aan een collega student om dit voor je te doen.
 * Wie heeft je website bezocht? (wanneer?, welke pagina's)
 * Wie heeft geprobeerd een niet-bestaande pagina op je website te openen?
 * Wanneer is de laatste login via ssh gebeurd?
 * Zijn er al pogingen tot inbraak op je systeem via ssh opgetreden? (een 'onbekende' die probeert je wachtwoord te raden)

## 3.2 Live Monitoring tools
Installeer ``htop``, ``iftop`` en bekijk de activiteit van je systeem.

Genereer zelf een aantal events zodat de grafieken nuttige informatie tonen.
 * Verhoog CPU/RAM gebruik door een programma te draaien dat de CPU/RAM zwaar belast [cpu.py](/Software/cpu.py), [ram.py](/Software/ram.py)
 * Genereer internet trafiek door bestanden te downloaden. [download.py](/Software/download.py)
 
Uitvoeren van de python code -> commando: ``python cpu.py``
Python programma afsluiten: ``ctrl-c``

### Optie 1: download bestanden apart via wget
Download de bestanden naar je server m.b.v. het ``wget`` commando. (https://www.gnu.org/software/wget)
Om een directe link naar de Python bestanden te krijgen klik je op de knop "RAW" op de Github paga.

Commando: ``wget https://raw.githubusercontent.com/AP-Elektronica-ICT/ServerManagement/master/Software/cpu.py``

### Optie 2: download all bestanden tegelijk via git
Je kan ook meteen alle bestanden naar je server downloaden door gebruik te maken van git. (http://git-scm.com)

Commando: ``git clone https://github.com/AP-Elektronica-ICT/ServerManagement.git``

Hierdoor worden alle bestanden van de Github repository op je server gezet.
Om deze bestanden later te updaten voer je het commando ``git pull`` uit. (in de "ServerManagement" folder)

## 3.3 Logging tools
Installeer Cacti/RRDtool en maak grafieken van onderstaande gegevens. 
 * CPU gebruik
 * RAM gebruik

Na de installatie van het "cacti" pakket kan je de website openen via "http://uwdomeinnaam/cacti"
De eerste keer zal daar een installatie wizard verschijnen.

De standaard credentials om deze wizard uit te voeren zijn:
 * username: admin
 * paswoord: admin

Zorg er voor dat de grafieken voldoende informatie tonen.
Zorg er voor dat je machine niet wordt afgesloten door het volgende script in een aparte tab uit te voeren in de web interface. [awake.py](/Software/awake.py)



Meer info: 
 * http://www.cacti.net

## 3.4 DOS aanval
Werk met drie personen samen om een DOS aanval uit te voeren op één van je Apache servers.
Zorg er zo veel gelijktijdige dataconnecties naar de webserver worden geopend dat hij geen extra connecties meer zal toelaten.
Het gevolg zal zijn dat de target server niet meer bereikbaar is.

Stel de target server zelf in om relatief gevoelig te zijn voor DOS aanvallen. (limiteer het maximaal aantal gelijktijdige connecties)
Indien je dit niet doet zou het kunnen dat de Amazon/Koding.com firewall je DOS aanval zullen detecteren.

Installeer volgende apache2 package om meer instellingen i.v.m. bandbreedte mogelijk te maken.
 * libapache2-mod-bw

Gebruik volgende tools:
 * [download.py](/Software/download.py)
 * [dos.py](/Software/dos.py)
 * https://github.com/evert/slowdeath

## Verslag & evaluatie
Screenshots met onderstaande gegevens en een kort woordje uitleg om toe te lichten wat er in de screenshot te zien is.
 * Antwoorden op de vragen i.v.m. logbestanden (licht voor elke regel in twee zinnen toe waar de informatie staat en hoe je deze kan interpreteren)
 * Screenshot van htop en iftop met CPU/RAM/netwerk load
 * Screenshot van Cacti met CPU/RAM load
 * Screenshots die aantonen dat de DOS aanval gelukt is.
 
De upload link kan je op Blackboard terugvinden.
