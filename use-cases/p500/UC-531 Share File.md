Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-531 Share File

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu, eine Kopie einer Datei beim Cloud Provider an eine oder mehrere Person/en zu senden. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. Der/Die Benutzer/in verfügt über benötigte Rechte um dieses Use Case ausführen zu können.

**Minimal quarantee:** None.

**Success quarantee:** Die Datei ist an die Zielperson/en gesendet worden.

**Main success szenario:** 

1. Der/Die Benutzer/in wählt die zu sendende Datei aus.
2. Das System zeichnet die Datei aus.
3. Der/Die Benutzer/in startet das Senden der Datei.
4. Das System fordert dem/der Benutzer/in die Eingabe von Empfänger/n der Datei.
5. Der/Die Benutzer/in gibt die benötigten Daten ein, z.B. E-Mail/s von Empfänger/n, und bestätigt das Senden der Datei.
6. Das System sendet die Datei und gibt eine Meldung zurück. 

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 6a. Das System weist auf fehlerhafte und/oder nicht vollständige Eingaben hin:
 * 1. Weiter mit Schritt 5. (Main success szenario)  
* 6b. Das System meldet, dass die Datei zu groß ist um gesendet werden zu können.
 
 
      