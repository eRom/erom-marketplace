# Contributing

Merci de l'intérêt pour cette marketplace 🙏

## Proposer un plugin externe

Cette marketplace est avant tout un catalogue personnel, mais les PR proposant des plugins tiers de qualité sont étudiées. Pour en soumettre un :

1. Ton plugin doit avoir un repo GitHub public (ou Git accessible).
2. Le repo doit contenir `.claude-plugin/plugin.json` à sa racine, avec au minimum `name`, `description`, `version`.
3. Ouvre une PR qui ajoute une entrée dans `.claude-plugin/marketplace.json` avec :
   - `name` (kebab-case, unique dans la marketplace)
   - `source` pointant vers ton repo
   - `description`, `version`, `license`, `keywords`, `category`
4. Mentionne dans la description de la PR : ce que fait le plugin, pourquoi il a sa place ici, ce qu'il demande comme permissions.

## Signaler un bug / une demande

Utilise les [Issues GitHub](https://github.com/eRom/erom-marketplace/issues) du repo. Précise :

- Version de Claude Code
- OS
- Plugin concerné
- Étapes pour reproduire

## Validation locale

Avant d'ouvrir une PR, valide que le JSON parse :

```bash
python3 -c "import json; json.load(open('.claude-plugin/marketplace.json'))"
```

Et que chaque `source.repo` est bien accessible publiquement.

## Code de conduite

Courtoisie, bienveillance, pas de contenu illégal ou malveillant dans les plugins proposés. Tout plugin suspect (exfiltration de données, appels réseau non documentés, etc.) sera refusé.
