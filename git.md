---
marp: true
math: mathjax
---
<!-- theme: uncover -->

<!-- https://github.com/orgs/marp-team/discussions/459#discussioncomment-6430972 -->
<style>
  * {
    text-align: left;
    font-size: 30px;
  }
  h1 {
    text-align: left;
  }
  h6 {
    margin-top: -1.5em;
  }
  ul, ol {
    margin-left: 0;
    margin-right: 0;
  }
  section {
    place-content: safe center left;
  }
</style>

![bg 25%](https://git-scm.com/images/logos/downloads/Git-Logo-2Color.svg)

---

# Versionsverwaltung

- Organisation und Kontrolle über Versionshistorien
- Festhalten von verschiedenen Zeitpunkten und Historien

```
* remove feature A (it broke our coffee machine)
|
* add feature B
|
* fix something
|
* add feature A
|
```

---

# Versionsverwaltung

Versionsverwaltungssysteme ermöglichen u.a.:
- Das Einsehen alter Zustände und die Berechnung von Unterschieden zwischen Zuständen ("Diffs")
- Rollbacks
- Geregelte Zusammenarbeit

```
* remove feature A (it broke our coffee machine)
|
* add feature B
|
* fix something
|
* add feature A
```

---

# Was ist Git?

- Das am weitesten verbreitete Versionsverwaltungssystem
- Ein verteiltes Versionsverwaltungssystem
- Free und open source
- Fokus auf Geschwindigkeit und nicht-lineare Workflows

Kann sowohl als Terminal-Applikation als auch mit GUIs genutzt werden (z.B. durch Editor-Plugins)

Befehle in `teletext` sind Git-Befehle, die so ins Terminal eingegeben werden können, um sie auszuführen.
In VSCode kann man per Command Palette meistens die entsprechenden Commands finden, sonst muss man im GUI oder Internet suchen

---

# Git und GitHub

- Git ist das System, auf dem GitHub basiert
- GitHub ermöglicht die Veröffentlichung von Git-Verzeichnissen
  (sog. Repos, kurz für "Repository")
- Es gibt hierfür auch andere Plattformen
  GitLab, Codeberg, SourceHut, Gitea, ...
- GitHub ist "nur" die populärste Plattform

Solche Plattformen haben meist noch weitere Features, die bei der Entwicklung unterstützen, aber mit Git nicht unbedingt verknüpft sind
(z.B. Issue Trackers)

---

# Erste Schritte mit Git

Repo erstellen:
- `git clone <url>` klont ein Repo von einer gegebenen URL
- `git init` initialisiert ein neues Git-Repo im aktuellen Verzeichnis

git speichert alles, was es braucht, im Unterverzeichnis `.git`

---

# Staging

Vor dem Committen muss Git wissen, welche Änderungen festgehalten werden sollen (Befehl: `git add`)

![w:850](https://bobbyhadz.com/images/blog/vscode-highlight-modified-lines/stage-and-unstage-file-to-see-highlighted-changes.gif)

---

# Commits

- Ein Commit ist ein Snapshot des Repos zu einem Zeitpunkt
- Commits enthalten:
  - Eine Diff (über eine oder mehrere Dateien)
  - Eine Commit-Nachricht
  - Metadaten (Autor, Zeitpunkt, ...)
- `git commit` erstellt einen Commit
  - Hält die Änderungen fest, die staged sind

---

# Branches

###### Das Problem

Lineare Historien sind langweilig und sehr nicht flexibel
- Beispiel:
  Person A macht mit einem Commit das Projekt kaputt.
  Person B kann nun nicht mehr arbeiten.

```
* ???
|
* Person A breaks everything
|
* Person B adds something
|
* Person A adds something
|
```

---

# Branches

###### Kollaboration ohne Verlustgefahr

Vorheriges Beispiel, aber Personen A und B arbeiten auf eigenen Branches:

```
  * Person B continues their work
  |
* | Person A breaks everything
| |
| * Person B adds something
|/
* Person A adds something
|
```

Auch das Arbeiten ausgehend von alten Versionen ist möglich

---

# Branches

###### Arbeiten mit Branches

##### Commits werden immer an den aktuellen Branch angehängt

Jedes Repo muss mindestens einen branch (default-Branch) enthalten
- Dieser heißt häufig `main` oder `master`

Befehle für die Arbeit mit Branches:

- `git switch`/`git checkout`: Branch wechseln
- `git branch`: Branches verwalten (erstellen, löschen, auflisten, ...)
- `git merge`: Branches wieder zusammenführen

---

# Arbeiten mit Remote Repos

###### Motivation

##### Alles, was bisher passiert ist, war nur lokal!

- Git synchronisiert Änderungen nur mit anderen Repos, wenn man dies explizit anfordert (Gleich mehr hierzu)
- Git funktioniert somit auch bis auf diese Befehle vollständig offline
- Remote:
  Git-Verzeichnis, das nicht auf dem eigenen System vorhanden ist, welches aber von einem lokalen Repo "getracked" wird
  Beispiel: Die Hausübungsvorlagen der FOP (GitHub-Repos)

---

# Arbeiten mit Remote Repos

###### Remotes verwalten

- Wenn man ein Repo klont (`git clone`), wird dieses automatisch als Remote hinzugefügt
- Standardname für Remotes: `origin`
- Befehl zum Verwalten: `git remote <operation>`
  `git remote add <name> <url>` fügt Repo unter `<url>` als Remote `name` hinzu

---

# Arbeiten mit Remote Repos

###### Remotes aktualisieren

Recap:
- Git-Verzeichnisse enthalten Branches
- Git arbeitet komplett lokal
- Folge: Git speichert auch den Zustand der Remotes lokal

`git fetch`:
- Git aktualisiert den lokal gespeicherten Stand der Branches mit dem neuen Stand der Remotes
- Muss nach Hinzufügen einer neuen Remote ausgeführt werden
- An den lokalen Branches ändert sich nichts

---

# Arbeiten mit Remote Repos

###### Updates synchronisieren

`git pull <name> <branch>`:
- Führt ein `git fetch` auf Remote `<name>` aus
- Merged anschließend den Remote-Branch `<branch>` in den aktuellen Branch
$\to$ Updates "pullen"

`git push <name> <branch>`:
- Aktualisiert den Branch `<branch>` in Remote `<name>` auf den aktuellen, lokalen Stand
$\to$ Updates "pushen"
$\to$ Der einzige Weg, wie man Zustand in einer Remote verändert

---

# Arbeiten mit Remote Repos

###### Sicherheitsbelehrung

- Wenn `git push` auf einen bestehenden Branch ausgeführt wird, muss die History übereinstimmen
(alle Remote-Commits müssen im lokalen Branch vorhanden sein)
  **$\to$ Daher immer vor dem pushen pullen**
- **Force-Push nur nach Absprache und wenn man weiß, was man tut**
- **Warnungen beachten und durchlesen**
  Git tut nichts Destruktives ohne Bestätigung
- **`.git`-Verzeichnis nie löschen**
  Lieber Projekt nochmal klonen, aus dem `.git`-Verzeichnis kann man meistens noch alles recovern

---

# Merge-Konflikte

Merge-Konflikt:
Beim Mergen von Branches versucht Git automatisch, Stellen, die in beiden Branches bearbeitet werdem, zu kombinieren.
Wenn dies fehlschlägt, entsteht ein Merge-Konflikt.


```
*   Merge Conflict when attempting to merge branches
| \
* | File F, Line L is edited in a different way
| |
...
| |
| * File F, Line L is edited
|/
```

---

# Merge-Konflikte

###### Wie sehen Konflikte aus?

An allen Stellen (eine oder mehrere Zeilen) mit Konflikten findet sich in den Dateien in etwa folgender Inhalt:

```
 <<<<<<< HEAD
 Hier steht eine Version der Konfliktstelle
 =======
 Hier steht die andere Version der Stelle
 >>>>>>> <Quelle der alternativen Version>
```

---

# Merge-Konflikte

###### Konflikte auflösen

```
 <<<<<<< HEAD
 Hier steht eine Version der Konfliktstelle
 =======
 Hier steht die andere Version der Stelle
 >>>>>>> <Quelle der alternativen Version>
```

- Ersetzen der von Git eingefügten Markierungen und der Änderungen durch die korrekte Version (man muss eventuell nachdenken)
- Sobald alle Konflikte in einer Datei gelöst sind, ist diese zu stagen
- Wenn alle Dateien gestaged sind, `git commit` ausführen, um Merge abzuschließen

---

# Abschluss

- **Niemals Credentials (Passwörter, API-Keys, ...) comitten**

- Möglichst wenig Binärdateien comitten
  In der `.gitignore`-Datei können Dateien von Git ignoriert werden
  (Funktioniert nur, wenn zuvor Git nicht bekannt)

- Git lernt man am besten, indem man es kontinuierlich nutzt

- Dokumentation ist sehr angenehm zu lesen, Ressourcen zu Git gibt es ohne Ende

- Fragen wurden zu 99.9% schon auf Stack Overflow beantwortet
