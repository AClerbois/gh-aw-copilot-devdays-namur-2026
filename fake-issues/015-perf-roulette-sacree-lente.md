---
title: "[PERF] La Roulette Sacrée met 8 secondes à retourner un résultat"
labels: [performance]
---

## ⚡ Description du problème

`SacredWheel.spin()` — l'opération de sélection aléatoire d'une pizza canonique — prenait **< 50ms** en v1.2. Depuis la v1.3, elle prend **7 à 9 secondes**, rendant la cérémonie de prière du vendredi particulièrement laborieuse.

## 📊 Mesures

| Version | p50 | p95 | p99 |
|---|---|---|---|
| v1.2 | 18ms | 42ms | 67ms |
| v1.3 | 7 200ms | 8 800ms | 9 400ms |

## 🔁 Étapes pour reproduire

```typescript
console.time("sacred-spin");
const pizza = await SacredWheel.spin();
console.timeEnd("sacred-spin");
// Output: sacred-spin: 7832ms
```

## 🔍 Analyse préliminaire

Le profiler révèle que 99 % du temps est passé dans `SacredWheel._loadCanonicalPizzas()` :

```
SacredWheel.spin()                    7 832ms
  └─ _loadCanonicalPizzas()           7 801ms   ← coupable
       └─ PizzaRepository.findAll()   7 798ms
            └─ DB query (no index)    7 795ms
```

La v1.3 a ajouté un filtre `WHERE heresy_score = 0.0 AND blessed = true` sur la table `pizzas` qui contient désormais **2,3 millions d'entrées** (historique de toutes les pizzas jamais créées) sans index sur ces colonnes.

## Fix proposé

1. Ajouter un index composite : `CREATE INDEX idx_canonical ON pizzas (heresy_score, blessed)`
2. Ou créer une table `canonical_pizzas` ne contenant que les pizzas validées (dénormalisation)
3. Mettre en cache le résultat de `_loadCanonicalPizzas()` avec TTL de 1h (`CacheService.set("canonical_pizzas", ...)`)

## Impact

La lenteur de la Roulette Sacrée rallonge les cérémonies du vendredi et provoque des abandons spirituels. Trois fidèles ont signalé avoir commandé sur une app concurrente pendant le temps d'attente.
