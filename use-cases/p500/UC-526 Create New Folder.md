Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-526 Create New Folder

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu einen neuen Ordner anzulegen. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. Der/Die Benutzer/in verfügt über benötigte Rechte um  dieses Use Case ausführen zu können.

**Minimal quarantee:** None.

**Success quarantee:** Der gewünschte Ordner ist angelegt.

**Main success szenario:** 

1. Der/Die Benutzer/in startet das Anlegen eines neuen Ordners.
2. Das System fordert dem/der Benutzer/in die Eingabe der Name des neuen Ordners .
3. Der/Die Benutzer/in gibt die Name ein und bestätigt diese.
4. Das System erzeugt und zeigt den neuen Ordner.

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 4a. Das System weist auf fehlerhafte und/oder nicht vollständige Eingaben hin z.B. Namenkonflikte, ungültige Buchstaben, etc.:
 * 1. Weiter mit Schritt 3. (Main success szenario).
 
            
      