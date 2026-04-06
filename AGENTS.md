# AGENTS.md — Contexte du projet pour les agents IA

Ce fichier fournit le contexte nécessaire aux agents IA (GitHub Copilot, Claude, Codex…) qui travaillent sur ce repository. Maintenu automatiquement par le workflow `agents-md-maintainer`.

---

## À propos du projet fictif : Marabou 🍕

**Marabou** est un logiciel de gestion de culte dédié à la **Pizza Sacrée** — un projet fictif utilisé comme fil conducteur pour illustrer les exemples d'agentic workflows lors de la session GitHub Copilot DevDays Namur 2026.

### Lore du projet

La communauté Marabou voue un culte fervent à la Pizza Sacrée. Elle est organisée en :

- **Fidèles** (`Devotee`) : membres du culte, possèdent un compte et peuvent commander des offrandes pizzalesques
- **Prêtres Fromagers** (`CheesePriest`) : gardiens de la doctrine, valident les bénédictions et prononcent les excommunications
- **Grand Prêtre Fromager** (`HighPriest`) : autorité suprême, peut signer des certificats de bénédiction
- **Conseil des Fromages** (`CheeseCouncil`) : organe délibératif, édicte les dogmes et révise la liste des ingrédients maudits

### Textes sacrés de référence

| Document | Rôle |
|---|---|
| **Dogme Fromager** | Règles canoniques sur les ingrédients autorisés et interdits |
| **Livre des Lamentations Fromagères** | Protocoles de gestion des incidents (pizza brûlée, hérésie, etc.) |
| **Liste Noire des Ingrédients Maudits (LNIM)** | Référentiel des ingrédients hérétiques (ananas, crème fraîche, ketchup…) |
| **Décrets du Concile des Fromages** | Évolutions doctrinales validées par le Conseil |

---

## Architecture du logiciel (fictive)

```
marabou/
├── src/
│   ├── core/
│   │   ├── SacredWheel.ts          # Roulette de sélection de la pizza sacrée
│   │   ├── HeresyDetectionEngine.ts # Détection des ingrédients hérétiques
│   │   └── BlessingRitual.ts        # Gestion des rituels de bénédiction
│   ├── services/
│   │   ├── DevoteeService.ts        # Gestion des fidèles
│   │   ├── OrderService.ts          # Commandes d'offrandes
│   │   ├── PricingService.ts        # Tarification (avec réductions sacrées)
│   │   ├── AudioService.ts          # Chants grégoriens et rituels sonores
│   │   ├── NotificationService.ts   # Notifications liturgiques
│   │   └── LiturgicalCalendarService.ts # Calendrier des Saints Pizzas
│   ├── models/
│   │   ├── Pizza.ts                 # Modèle pizza (ingrédients, type de pâte, etc.)
│   │   ├── Devotee.ts               # Modèle fidèle
│   │   ├── BlessingCertificate.ts   # Certificat de bénédiction (avec QR code)
│   │   └── SaintPizza.ts            # Pizza canonisée du calendrier liturgique
│   └── rituals/
│       ├── BoxOpeningRitual.ts      # Cérémonie d'ouverture de la boîte
│       ├── ExpiationMode.ts         # Jeûne expiatoire (pizza brûlée)
│       └── MarabouSession.ts        # Session de prière hebdomadaire
├── config/
│   └── heresy-config.yaml           # Scores d'hérésie par ingrédient et type de pâte
└── tests/
```

---

## Conventions de code

- **Langage** : TypeScript (ESM)
- **Tests** : convention `NomMéthode_Scénario_ComportementAttendu`
- **Nommage** : PascalCase pour les classes, camelCase pour les méthodes, SCREAMING_SNAKE pour les constantes sacrées
- **Erreurs** : toutes les exceptions métier héritent de `MarabouException`
- **Logs** : tout événement liturgique est loggé au niveau `INFO` avec le préfixe `[SACRED]`

## Ingrédients hérétiques connus (LNIM v4.2)

| Ingrédient | Niveau d'hérésie | Score HDE |
|---|---|---|
| Ananas | 3 — Hérésie grave | 0.9 |
| Ketchup | 3 — Hérésie grave | 0.95 |
| Crème fraîche | 2 — Hérésie modérée | 0.6 (v4.2) |
| Pâte fine | ⚖️ Débat doctrinal en cours | 0.4 (provisoire) |
| Calzone | 0 — Autorisée hors vendredi | 0.0 / 0.8 selon jour |

---

## Issues actives (contexte pour l'agent)

Ces issues sont utilisées comme données d'exemple dans les démonstrations d'agentic workflows :

- Bugs sur `SacredWheel`, `DevoteeCounter`, `AudioService`, `HeresyDetectionEngine`
- Features : calendrier liturgique, bénédiction di bufala, jeûne expiatoire
- Débat doctrinal : pâte fine hérésie vs ascèse

L'agent ne doit **pas** fermer ces issues automatiquement — elles servent de données de démonstration.

---

## Contexte de la session

Ce repository est utilisé lors de la session **GitHub Agentic Workflows** au Copilot DevDays Namur (7 avril 2026). Les exemples de workflows gh-aw s'appuient sur les issues Marabou pour démontrer le triage, la labellisation et la génération de rapports.
