---
title: "[QUESTION] La Margherita peut-elle être servie tiède lors d'un Concile ?"
labels: [question, doctrinal]
---

## 🌡️ Contexte de la question

Un débat a éclaté lors du dernier Concile des Fromages de Bruxelles (14 mars 2026). La question qui divise :

> *La Margherita — pizza canonique par excellence — peut-elle être servie **tiède** lors d'une réunion du Concile sans constituer une infraction au Dogme Fromager ?*

## 📜 Textes en tension

### Arguments pour (école « tolérantiste »)
Le Dogme Fromager impose que la pizza soit *préparée avec amour et fromage de qualité*, mais **ne mentionne pas explicitement la température de service**. Une Margherita tiède conserve ses qualités fromagères fondamentales.

### Arguments contre (école « rigoriste »)
Le Livre des Lamentations Fromagères, Chapitre 3, verse 7 stipule :
> *« Le fromage doit couler comme la sagesse du Grand Prêtre — chaud et abondant. »*

Une Margherita tiède ne respecterait donc pas ce principe fondamental.

## ❓ Question technique pour le `TemperatureValidator`

L'application doit-elle :

**Option A — Validation stricte**
```yaml
margherita:
  min_temp_celsius: 65
  on_violation: WARN_AND_LOG
  concile_exception: false
```

**Option B — Exception Concile**
```yaml
margherita:
  min_temp_celsius: 65
  on_violation: WARN_AND_LOG
  concile_exception: true   # tolérance pendant les réunions officielles
  concile_min_temp: 45
```

**Option C — Pas de validation de température**
Retirer la vérification de température du `SacredValidator` et laisser le jugement à l'appréciation humaine du Prêtre officiant.

## Vote du Concile

Merci de réagir :
- 🔥 = Option A (validation stricte)
- 🧀 = Option B (exception Concile)
- ❄️ = Option C (pas de validation)
- 😕 = Convoquer un nouveau Concile extraordinaire
