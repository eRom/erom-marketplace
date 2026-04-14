# erom-marketplace

> Plugins Claude Code de [Romain Ecarnot](https://github.com/eRom) — agents, skills et MCP servers pour orchestration multi-projets et productivité.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-plugins-8B5CF6)](https://docs.claude.com/en/docs/claude-code)

---

## Installation

Ajoute cette marketplace à ton Claude Code :

```
/plugin marketplace add eRom/erom-marketplace
```

Puis installe le plugin de ton choix :

```
/plugin install gerber-caserne@erom-marketplace
```

Pour lister tout ce qui est dispo :

```
/plugin marketplace browse erom-marketplace
```

---

## Plugins disponibles

### `gerber-caserne`

Brain & productivity MCP server. Stocke tes notes, tâches et issues avec recherche sémantique, et permet à plusieurs sessions Claude Code de communiquer entre elles via un bus de messages.

- **Catégorie** : productivity
- **Repo** : [eRom/gerber-caserne](https://github.com/eRom/gerber-caserne)
- **Usage** : orchestration agent, mémoire cross-session, gestion de connaissances projet

Installation directe :

```
/plugin install gerber-caserne@erom-marketplace
```

---

## Ajouter un nouveau plugin à la marketplace

1. Crée/prépare ton plugin dans son propre repo GitHub (doit contenir idéalement `.claude-plugin/plugin.json` à la racine, sinon laisse `strict: false` dans l'entrée marketplace).
2. Ajoute une entrée dans [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json) :

```json
{
  "name": "mon-plugin",
  "source": {
    "source": "github",
    "repo": "eRom/mon-plugin"
  },
  "description": "Description courte du plugin.",
  "version": "0.1.0",
  "license": "MIT",
  "category": "productivity",
  "keywords": ["tag1", "tag2"],
  "strict": false
}
```

3. Commit, push, et les utilisateurs qui ont déjà ajouté la marketplace peuvent rafraîchir avec :

```
/plugin marketplace update erom-marketplace
```

### Sources supportées

- **GitHub** : `{ "source": "github", "repo": "user/repo", "ref"?: "v1.0.0" }`
- **Git URL** : `{ "source": "url", "url": "https://gitlab.com/…/plugin.git" }`
- **Git sous-dossier** : `{ "source": "git-subdir", "url": "…", "path": "tools/plugin" }`
- **npm** : `{ "source": "npm", "package": "@scope/plugin" }`
- **Chemin local** (dev uniquement) : `"source": "./plugins/mon-plugin"`

### Mode strict

- `strict: true` (défaut) — l'entrée marketplace ne sert qu'à pointer vers le plugin ; les métadonnées viennent de son `.claude-plugin/plugin.json`.
- `strict: false` — l'entrée marketplace est auto-suffisante (utile tant que le repo plugin n'a pas encore son `plugin.json`).

---

## Roadmap

- [ ] Ajouter `plugin.json` dans chaque repo plugin et passer `strict: true`.
- [ ] Publier un workflow CI pour valider `marketplace.json` à chaque PR.
- [ ] Ajouter des captures d'écran / démos pour chaque plugin.
- [ ] Ajouter les plugins complémentaires (`trinity-lifeos-agent`, `ccc-system`, …).

---

## Contribution

Les PR sont les bienvenues. Voir [CONTRIBUTING.md](./CONTRIBUTING.md) pour le protocole.

## Licence

[MIT](./LICENSE) © 2026 Romain Ecarnot
