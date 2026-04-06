# Fake Issues — Marabou 🍕

Issues fictives du projet **Marabou** prêtes à être créées sur le repository pendant la session live.

Chaque fichier est nommé `NNN-titre-court.md` et contient le titre, les labels suggérés et le corps de l'issue au format GitHub.

## Comment créer une issue depuis un fichier

### Via GitHub CLI
```bash
gh issue create \
  --title "$(head -1 fake-issues/001-*.md | sed 's/^# //')" \
  --body-file fake-issues/001-*.md \
  --label bug
```

### Via l'interface web
Copier le contenu du fichier dans le formulaire de création d'issue sur github.com.

---

## Issues disponibles

| Fichier | Type | Titre court |
|---|---|---|
| `001-portail-prieres-timeout.md` | 🐛 Bug | Portail de prières — timeout après 3 Ave Fromage |
| `002-badge-apostat-affiche-tout-le-monde.md` | 🐛 Bug | Badge Apostat affiché sur tous les fidèles |
| `003-mode-sombre-impose-jeune.md` | 🐛 Bug | Le mode sombre déclenche un jeûne non désiré |
| `004-notifications-doublon-fete.md` | 🐛 Bug | Doublon de notifications les jours de fête |
| `005-pizza-sans-fromage-acceptee.md` | 🐛 Bug | Une pizza sans fromage passe la validation |
| `006-feature-confession-numerique.md` | ✨ Feature | Module de confession numérique |
| `007-feature-mode-pelerinage.md` | ✨ Feature | Mode pèlerinage — commande depuis un lieu saint |
| `008-feature-rang-pretre-fromager.md` | ✨ Feature | Système de rangs pour les Prêtres Fromagers |
| `009-feature-oracle-pizza.md` | ✨ Feature | Oracle de la Pizza — prédictions basées sur les garnitures |
| `010-feature-blockchain-reliques.md` | ✨ Feature | Enregistrement des reliques fromagères sur blockchain |
| `011-question-margherita-dogme.md` | ❓ Question | La Margherita peut-elle être servie tiède lors d'un concile ? |
| `012-question-fromage-vegan.md` | ❓ Question | Le fromage vegan est-il un sacrilège ou une tolérance ? |
| `013-docs-rituel-ouverture-boite.md` | 📖 Docs | Documenter le rituel d'ouverture de la boîte sacrée |
| `014-docs-guide-excommunication.md` | 📖 Docs | Rédiger le guide d'excommunication pour les modérateurs |
| `015-perf-roulette-sacree-lente.md` | ⚡ Perf | La Roulette Sacrée met 8 secondes à tourner |
