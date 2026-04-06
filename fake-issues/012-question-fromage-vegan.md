---
title: "[QUESTION] Le fromage vegan constitue-t-il un sacrilège ou une tolérance pastorale ?"
labels: [question, doctrinal]
---

## 🌱 Contexte

Depuis l'essor des régimes alimentaires végétaliens, plusieurs fidèles ont demandé la possibilité de commander des pizzas avec du **fromage vegan** (base cajou ou coco). Cette requête a provoqué une fracture théologique inédite au sein du Conseil des Fromages.

## Les deux positions

### Position A — Le Sacrilège (Frères Laitiers)
> *« Le fromage vegan n'est pas du fromage. C'est une poudre d'escroquerie enrobée dans de la tristesse. Utiliser le mot "fromage" pour décrire cette substance est la plus grande hérésie culinaire du XXIe siècle. »*

— Mgr. Goudarin III, Archevêque du Pavé de Bruxelles

Le `HeresyDetectionEngine` devrait classer le fromage vegan en **hérésie de niveau 3** (identique au ketchup).

### Position B — La Tolérance Pastorale (Frères Ouverts)
> *« Le Fromage, dans son essence spirituelle, transcende sa forme physique. Ce qui compte est l'intention fromagère du cœur, non la composition biochimique du produit. »*

— Sœur Mozzarella du Plateau, Diacresse de Lyon

Le fromage vegan devrait être autorisé avec un score HDE de `0.1` (acceptable avec avertissement).

## Impact sur le code

```yaml
# heresy-config.yaml — que mettre ici ?

vegan_cheese:
  heresy_score: ???        # 0.0, 0.1, ou 0.9 ?
  label: ???               # "CANONICAL", "TOLERATED", ou "HERESY_LEVEL_3"
  allow_in_ceremony: ???   # true ou false
```

## Questions associées

- Faut-il créer un label distinct `VEGAN_TOLERATED` vs `CANONICAL` ?
- Les pizzas vegan peuvent-elles recevoir une bénédiction officielle ?
- Le `LiturgicalCalendarService` doit-il proposer des alternatives vegan les jours de jeûne ?

## Votre avis

- 🧀 = Sacrilège total (score 0.9, hérésie de niveau 3)
- 🌱 = Tolérance pastorale (score 0.1, label TOLERATED)
- ✅ = Totalement canonique (score 0.0)
- ⚖️ = Voter blanc et convoquer un Concile extraordinaire
