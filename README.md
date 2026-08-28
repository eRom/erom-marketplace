# erom-marketplace

> Plugins Claude Code et Codex de [Romain Ecarnot](https://github.com/eRom) - agents, skills et MCP servers pour orchestration multi-projets et productivité.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-plugins-8B5CF6)](https://docs.claude.com/en/docs/claude-code)

---

## Installation Claude Code

Ajoute cette marketplace à ton Claude Code :

```
/plugin marketplace add eRom/erom-marketplace
```

Puis installe le plugin de ton choix :

```
/plugin install erom-caserne@erom-marketplace
```

Pour lister tout ce qui est dispo :

```
/plugin marketplace browse erom-marketplace
```

## Installation Codex

La marketplace Codex vit dans [`.agents/plugins/marketplace.json`](./.agents/plugins/marketplace.json).

Elle expose `caserne`, qui pointe vers le repo `eRom/erom-caserne` (dont le `.codex-plugin/plugin.json`
sert de manifeste côté Codex) :

```json
{
  "name": "caserne",
  "source": {
    "source": "url",
    "url": "https://github.com/eRom/erom-caserne.git"
  }
}
```

Note : côté Codex l'entrée garde le nom court `caserne` (le préfixe `erom-` ne sert qu'à grouper les
plugins dans l'autocomplete Claude Code, où ils côtoient les plugins officiels).

---

## Plugins disponibles

| Plugin | Repo | Skills | Ce qu'il fait |
|---|---|---|---|
| `erom-caserne` | [eRom/erom-caserne](https://github.com/eRom/erom-caserne) | `control`, `inbox`, `network`, `orchestrate`, `relay` | L'agence : identité Linear / Slack / mail via le MCP Caserne, swarm tmux de salariés IA, relais d'idées |
| `erom-devil` | [eRom/erom-devil](https://github.com/eRom/erom-devil) | `spec`, `brain`, `code`, `review` (+ `-swarm`) | Avocats du diable externes (Gemini, GLM, Deepseek, Opus, Kimi) sur specs, brainstorms et changements de code, plus la porte de merge : porte déterministe, grille de stack, vérification contradictoire, verdict GO/NO-GO et rapport persistant |
| `erom-research` | [eRom/erom-research](https://github.com/eRom/erom-research) | `deep-gemini`, `deep-claude`, `deep-grok`, `deep-notebook` | Quatre moteurs de deep research : multi-rounds piloté, moteur natif sans dépendance externe, moteur indépendant asynchrone, référentiel NotebookLM persistant ; rapports centralisés dans `~/.claude/erom-plugin-artefacts/researchs/` |
| `erom-image` | [eRom/erom-image](https://github.com/eRom/erom-image) | `gpt`, `nanobanana`, `filigrane`, `qrcode` | Génération et édition d'images par MCP : texte exact et haute fidélité (OpenAI), volume et icônes (Gemini), puis filigrane image/PDF avant diffusion et QR-Code relu avant écriture |
| `erom-marketing` | [eRom/erom-agence-marketing](https://github.com/eRom/erom-agence-marketing) | `voix`, `draft-content`, `brand-review` | Voix de marque eRom : magasin de voix local (socle + personas institut, perso, business), rédaction qui refuse d'écrire sans la voix, review en six passes avec findings sourcés |
| `erom-gemini` | [eRom/erom-gemini](https://github.com/eRom/erom-gemini) | `transcribe`, `video`, `media`, `doc-to-md` | Les yeux et les oreilles de Claude Code : transcription audio/vidéo, breakdown visuel horodaté, Q&A sur un média, OCR document → markdown, offloadés vers Gemini |
| `erom-insight` | [eRom/erom-agence-insight](https://github.com/eRom/erom-agence-insight) | `harness`, `tool-claude`, `skill-claude` | Veille sur les repos tiers. `harness` explore les agents CLI concurrents : swarm de lecteurs sur facettes disjointes, réfutation des fausses trouvailles, rapport or/argent/bronze. `tool-claude` tranche l'installation d'un outil qui se branche sur Claude Code : brochure confrontée au code, coût d'installation chiffré, gestes repris mesurés sur le corpus local avant tout patch. `skill-claude` juge une skill ou un plugin tiers avant installation : scanner de sécurité bloquant, puis finalité, mécanisme, véracité, verdict installer / trash / refaire |
| `erom-dev-plugin` | [eRom/erom-agence-dev-plugin](https://github.com/eRom/erom-agence-dev-plugin) | `scaffold`, `illustrate`, `release` | Le cycle de vie d'un plugin Claude Code eRom : `scaffold` monte la structure du dépôt sans jamais écraser un fichier existant, `illustrate` dessine sa carte de présentation au fusain depuis l'inventaire réel lu par `claude plugin details`, `release` publie une version en tenant l'ordre plugin puis marketplace et vérifie la CI |

Installation :

```
/plugin install erom-devil@erom-marketplace
```

Invocation : `/erom-devil:code`, `/erom-research:deep-gemini`, `/erom-caserne:inbox`, `/erom-image:gpt`, `/erom-gemini:transcribe`.

## Convention de nommage

Actée le 2026-07-30, appliquée aux quatre plugins :

1. **Le repo GitHub, le plugin et son namespace portent le même nom** : `erom-<domaine>`. Aucun mapping
   à retenir entre ce qu'on installe, ce qu'on invoque et l'endroit où le code vit.
2. **La skill ne répète jamais le domaine** : elle nomme le moteur ou l'action (`agy`, `gpt`, `inbox`,
   `brain-swarm`), le namespace portant déjà le contexte. D'où `/erom-devil:brain-swarm` et non
   `/devil:devil-brain-swarm`.
3. **« agence » est réservé au réseau d'agents caserne**, jamais utilisé comme préfixe technique.

Les dossiers locaux de développement (`~/dev/erom-agence-*`) gardent leurs anciens noms : ils ne sont
visibles de personne d'autre, et les renommer casserait terminaux et scripts pour rien.

---

## Ajouter un nouveau plugin à la marketplace Claude

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

### Mode strict Claude

- `strict: true` (défaut) - l'entrée marketplace ne sert qu'à pointer vers le plugin ; les métadonnées viennent de son `.claude-plugin/plugin.json`.
- `strict: false` - l'entrée marketplace est auto-suffisante (utile tant que le repo plugin n'a pas encore son `plugin.json`).

## Ajouter un nouveau plugin à la marketplace Codex

Ajoute une entrée dans [`.agents/plugins/marketplace.json`](./.agents/plugins/marketplace.json) :

```json
{
  "name": "mon-plugin",
  "source": {
    "source": "git-subdir",
    "url": "https://github.com/eRom/mon-repo.git",
    "path": "mon-codex-plugin"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Coding"
}
```

Le plugin cible doit contenir `.codex-plugin/plugin.json`.

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
