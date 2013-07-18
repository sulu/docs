Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-525 Duplicate File

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu eine Kopie einer Datei in gleichen Ort zu erzeugen.

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt.Der/Die Benutzer/in verfügt über benötigte Rechte um dieses Use Case ausführen zu können.

**Minimal quarantee:** None.

**Success quarantee:** Die Datei wurde dupliziert.

**Main success szenario:** 

1. Der/Die Benutzer/in wählt die zu dupliziernde Datei aus.
2. Das System zeichnet die Datei aus.
3. Der/Die Benutzer/in startet das Duplizieren der Datei.
4. Das System erzeugt eine Kopie der Datei in gleichen Ort.

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.

 
	 