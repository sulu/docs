Use Cases
####![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)UC-522 Download File

**Primary Actor:** [Endbenutzer](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Short Description:** Dieses Use Case dient dazu, eine Datei beim Cloud Provider zu herunterladen. 

**Scope:** [P500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p500-assets "500 ASSETS") 

**Level:** Activity

**Precondition:** Das Use Case "Daten Auslesen" wurde erfolgreich ausgeführt. Der/Die Benutzer/in verfügt über benötigte Rechte um dieses Use case ausführen zu können.

**Minimal quarantee:** None.

**Success quarantee:** Die Datei ist heruntergeladen.

**Main success szenario:** 

1. Der/Die Benutzer/in wählt die herunterzuladende Datei aus.
2. Das System zeichnet diese Datei aus.
3. Der/Die Benutzer/in startet das Herunterladen der Datei.
4. Das System lädt die Datei herunter und zeigt diese an.

**Extensions:**
* *a. Zu jeder Zeit bricht der/die Benutzer/in das Use Case ab oder das System schlägt fehl:	
Um einen konsistenten Zustand gewährleisten zu können müssen alle Transaktion sensitiven Zustände in jedem Schritt von Szenario wiederhergestellt werden können.
* 4a. Das System meldet, dass das Herunterladen der Datei fehlgeschlagen ist.z.B. keine Netzwerkverbindung mehr