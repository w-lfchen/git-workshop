---
marp: true
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

# Was ist git?

- Das am weitesten verbreitete Versionsverwaltungssystem
- Ein verteiltes Versionsverwaltungssystem
- Free und open source
- Fokus auf Geschwindigkeit und nicht-lineare Workflows

Kann sowohl als Terminal-Applikation als auch mit GUIs genutzt werden (z.B. durch Editor-Plugins)

---

# git und GitHub

- git ist das System, auf dem GitHub basiert
- GitHub ermöglicht die Veröffentlichung von git-Verzeichnissen
  (sog. Repos, kurz für "Repository")
- Es gibt hierfür auch andere Plattformen
  GitLab, Codeberg, SourceHut, Gitea, ...
- GitHub ist "nur" die populärste Plattform

Solche Plattformen haben meist noch weitere Features, die bei der Entwicklung unterstützen, aber mit git nicht unbedingt verknüpft sind
(z.B. Issue Trackers)

---

# Erste Schritte mit git

Repo erstellen:
- `git clone <url>` klont ein Repo von einer gegebenen URL
- `git init` initialisiert ein neues git-Repo im aktuellen Verzeichnis

git speichert alles, was es braucht, im Unterverzeichnis `.git`

---

# Commits

---

# Branches

---

# Arbeiten mit Remotes

