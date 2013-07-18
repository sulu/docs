Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-532 Share Link

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu, den Link einer Datei beim Cloud Provider an einer oder mehreren Person/en freizugeben. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. Der/Die Benutzer/in verfügt über benötigte Rechte um dieses Use Case ausführen zu können.

**Minimal quarantee:** None.

**Success quarantee:** Die Datei wurde für die Zielperson/en freigegeben.

**Main success szenario:** 

1. Der/Die Benutzer/in wählt die freizugebende Datei aus.
2. Das System zeichnet die Datei aus
3. Der/Die Benutzer/in startet die Freigabe des Linkes.
4. Das System fordert dem/der Benutzer/in die Eingabe von Empfänger/n des Linkes.
5. Der/Die Benutzer/in gibt die benötigten Daten ein. z.B. E-Mail/s von Empfänger/n und bestätigt das Freigeben des Linkes.
6. Das System erzeugt den Link, sendet ihn und gibt eine Meldung zurück. 

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 6a. Das System weist auf fehlerhafte und/oder nicht vollständige Eingaben hin:
 * 1. Weiter mit Schritt 5. (Main success szenario).  
      