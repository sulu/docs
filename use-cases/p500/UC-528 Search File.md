Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-528 Search File

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu eine gewünschte Datei anhand Ihre Name oder Ihren Metadaten zu suchen. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. 

**Minimal quarantee:** None. 

**Success quarantee:** Die gewünschte Datei ist gefunden und angezeigt. Wenn die Datei nicht vorhanden ist wird eine entsprechende Meldung angezeigt.

**Main success szenario:** 

1. Der/Die Benutzer/in startet das Suchen einer Datei.
2. Das System fordert dem/der Benutzer/in die Eingabe der Suchkriterien.
3. Der/Die Benutzer/in gibt die Suchkriterien ein und bestätigt diese.
4. Das System sucht die Datei, findet und zeigt sie an.

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 4a. weist auf fehlerhafte und/oder nicht vollständige Eingaben hin:
 * 1. Weiter mit Schritt 3. (Main success szenario).
* 4b. Das System zeigt mehrere Dateien an, welche möglichst viel die Suchkriterien erfüllen.
* 4c. Das System meldet, dass die gewünschte Datei nicht gefunden wurde. 
 
 
 