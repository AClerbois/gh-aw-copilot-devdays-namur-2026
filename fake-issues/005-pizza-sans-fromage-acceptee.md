---
title: "[BUG] Une pizza sans aucun fromage est acceptée par le validateur sacré"
labels: [bug, critical]
---

## 🧀 Description du problème

Le `SacredValidator.validate()` accepte les pizzas dont la liste d'ingrédients ne contient **aucun fromage**. Une telle pizza est pourtant une abomination absolue selon le **Dogme Fromager, Principe Premier** : *« Toute pizza doit porter le Fromage en son cœur. »*

## 🔁 Étapes pour reproduire

```typescript
const pizza = new Pizza({
  name: "Pizza du Néant",
  ingredients: ["tomate", "basilic"],  // ← zéro fromage
  crustType: "THICK"
});

const result = SacredValidator.validate(pizza);
console.log(result); // { valid: true, heresyScore: 0.0 }
```

## ✅ Comportement attendu

```typescript
{ 
  valid: false, 
  heresyScore: 1.0, 
  reason: "NO_CHEESE_DETECTED",
  severity: "ABSOLUTE_HERESY",
  recommendation: "DESTROY_IMMEDIATELY"
}
```

## ❌ Comportement actuel

```typescript
{ valid: true, heresyScore: 0.0 }
```

## Cause probable

La règle `CHEESE_REQUIRED` dans `sacred-validation-rules.yaml` est présente mais le flag `enabled` est à `false` depuis le commit `a1b2c3d` (*"disable cheese check for unit test perf"*) — qui n'a jamais été réverté.

```yaml
rules:
  CHEESE_REQUIRED:
    enabled: false  # ← coupable
    min_cheese_ingredients: 1
```

## Impact

Des pizzas sans fromage circulent silencieusement dans la communauté. **Priorité : ABSOLUE.**
