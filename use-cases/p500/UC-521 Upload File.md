Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-513 Upload File

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu, lokale Daten optional mit Metadaten beim Cloud Provider hochzuladen. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. Der/Die Benutzer/in verfügt über benötigte Rechte um diese Use Case ausführen zu können. Die zu hochladende Datei entspricht der Voraussetzung (Dateigroße, Dateityp, etc.) vom Cloud Provider.

**Success quarantee:** Die Datei ist beim Cloud Provider hochgeladen.

**Main success szenario:** 

1. Der/Die Benutzer/in startet das Hochladen einer Datei.
2. Das System fordert dem/der Benutzer/in die Datei auszuwählen.
3. Der/Die Benutzer/in wählt die Datei aus und bestätigt seine/Ihre Auswahl.
4. Das System zeigt die ausgewählte Datei an, liest und ergänzt die Datei um Metadaten(z.B. Aus Geodaten falls vorhanden).
5. Der/Die Benutzer/in ergänzt die Datei händisch um Metadaten.
6. Der/Die Benutzer/in bestätigt das Hochladen der Datei. 
7. Das System lädt die Datei hoch und zeigt diese an.

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 5a. Der/Die Benutzer/in macht mit Schritt 6. Weiter (Main success szenario). 
* 7a. Das System weist auf fehlerhafte und/oder fehlende Eingaben hin:
 * 1. Weiter mit Schritt 5. (Main success szenario).
     * 1a.Der/Die Benutzer/in ignoriert den Hinweis. 
* 7b. Das System meldet, dass das Hochladen der Datei fehlgeschlagen ist.z.B. Wegen fehlendem Speicherplatz, Dateigroße, Dateiformat, etc.

 
	 