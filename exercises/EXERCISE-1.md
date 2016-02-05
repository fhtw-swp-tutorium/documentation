# Time-Management

Sie werden im Zuge dieser Übung folgende Pattern implementieren:

- Singleton
- Observer
- Command

Es soll eine Kommandozeilenapplikation entstehen, mit der die Arbeitszeit von verschiedenen Benutzern in verschiedenen Projekten aufgezeichnet werden kann. Die Anwendung bietet eine interaktive Konsole, auf der Kommandos eingegeben werden können. 

# 1. Kommandos

Folgende Kommandos sollen zur Verfügung stehen:

- **adduser** `username`  
Legt einen neuen User an. Benutzernamen sind eindeutig und dürfen nur aus Kleinbuchstaben bestehen.

- **addproject** `#project-tag` [`description`]  
Legt ein neues Project mit dem Tag `project-tag` an. Project-Tags müssen immer mit einer Raute gekennzeichnet werden. Ein Project-Tag muss eindeutig sein und darf nur aus Kleinbuchstaben bestehen. Die Beschreibung des Projektes ist optional. 

- **addtime** [`username`] [`#project-tag`] `duration` `description`  
Bucht die angegebene Zeit `duration` für den Benutzer `username` auf das Projekt mit Tag `project-tag`. `duration` gibt die zu buchende Zeit in Minuten und als Ganzzahl an. Der Benutzername und der Projekt-Tag sind optional und werden, falls nicht angegeben, vom letzten _addtime_ Command übernommen. Falls das Projekt oder der Benutzer beim Absetzen eines _addtime_ Commands noch nicht existieren, soll ein Fehler ausgegeben werden. 

- **undo**  
Kehrt das letzte Kommando um, falls möglich. _Undo_ selbst wird nicht in der History gespeichert.

- **redo**  
Führt das letzte, rückgängig gemachte Kommando wieder aus, falls vorhanden. _Redo_ selbst wird nicht in der History gespeichert.

- **help**  
Zeigt eine Liste aller verfügbaren Kommandos mit einer Beschreibung an. (zB Parameter) Hint: Orientieren Sie sich an bekannten Unix-Tools bzgl. der Formatierung und Informationen. (zB Git)

- **stats** `username`  
Zeigt die Summe aller Zeitbuchungen des aktuellen Tages eines Users in Minuten auf der Console an.

# 2. Implementierungsdetails

## 2.1 Singleton-Pattern

Verwenden Sie das Singleton-Pattern um Daten zu speichern/halten. zB User, Projekte, Zeitbuchungen, Kommando-Historie.

## 2.2 Command-Pattern

Verwenden Sie das Command-Pattern um die einzelnen Kommandos umzusetzen.

## 2.3 Observer-Pattern

Mithilfe des Observer-Patterns sollen 2 Usecases umgesetzt werden:

### 2.3.1 Arbeitszeit-Warnung

Wenn die Arbeitszeit eines Users 8h pro Tag überschreitet, soll folgende Meldung auf der Konsole erscheinen:  
"Achtung! Arbeitszeit von User XX um Y Minuten überschritten."

### 2.3.2 Arbeitszeit-Logger

Sobald ein neuer User angelegt wird, soll auch ein Observer erzeugt werden, der alle Zeitbuchungen dieses Users in einer Datei protokolliert. Natürlich müssen die Zeitbuchungen auch im Speicher gehalten werden (siehe _stats_ Kommando). 

#### 2.3.2.1 Format

Jede Zeitbuchung soll in folgendem Format in die Datei geschrieben werden:  
"`timestamp` `#project-tag` `duration` `description`".

- Der `timestamp` soll dem ISO8601-Format entsprechen. zB 2007-12-24T18:21Z  
- Die `duration` soll in Minuten abgespeichert werden.    
- Der `project-tag` soll mit der Raute abgespeichert werden. 

#### 2.3.2.2 Zusätzliche Anforderungen

- Das File-Handle sollte nur so lange wie nötig "offen" bleiben.
- Der Name des Files entspricht dem `username`.
- Jede Zeile darf nur einen Datensatz beinhalten.
- Sobald eine Zeile einmal in die Datei geschrieben wurde, darf diese Zeile nicht mehr verändert werden, daher ist nur das Hinzufügen von neuen Zeilen möglich.

#### 2.3.2.3 Stornierung

Da eine bereits protokollierte Zeile niemals verändert werden darf, soll im Falle eines `Undo`s für ein `addtime` Kommando DIESELBE Zeile nocheinmal protokolliert werden, allerdings diesmal mit einem `-` am Beginn. 

# 3. Kennzeichnung der Patterns:

Damit die Übung erfolgreich automatisiert getestet werden kann, müssen Sie folgende Annotationen/Attribute in Ihrem Projekt verwenden:

- Java Annotationen: link
- .Net Attribute: [nuget-link](#)

__Folgende Patterns__ müssen dadurch gekennzeichnet werden:
- Singleton:  
    - durch das Kennzeichnen der jeweiligen Klasse mit `[Singleton]`.
- Observer: 
    - durch das Kennzeichnen der jeweiligen Klasse mit `[Observer]`.
- Command: 
    - tbd

# 4. Bearbeitungshistorie

04.02.2016 - Initiale Angabe

[detaillierte Historie](https://github.com/fhtw-swp-tutorium/documentation/wiki/3.1-Abgabe:-TimeManagement/_history)
