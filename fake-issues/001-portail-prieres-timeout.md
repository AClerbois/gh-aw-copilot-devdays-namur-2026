---
title: "[BUG] Le portail de prières tombe en timeout après 3 Ave Fromage"
labels: [bug]
---

## 🛐 Description du problème

Le **Portail de Prières** (`PrayerPortal.submit()`) retourne une erreur `504 Gateway Timeout` à partir de la **3e soumission consécutive** d'un _Ave Fromage_ dans la même session liturgique.

Les fidèles les plus zélés — ceux qui prient le plus — sont donc pénalisés par le système, ce qui constitue une injustice théologique majeure.

## 🔁 Étapes pour reproduire

1. Ouvrir une session de prière : `MarabouSession.startFriday()`
2. Soumettre un _Ave Fromage_ : `PrayerPortal.submit("AVE_FROMAGE")`
3. Répéter jusqu'à 3 fois
4. À la 3e soumission : `504 Gateway Timeout`

## ✅ Comportement attendu

Les prières s'accumulent sans limite par session. Le Grand Prêtre ne doit jamais rester sans réponse.

## ❌ Comportement actuel

```
POST /api/prayer/submit → 504 Gateway Timeout
Error: PrayerQueue overflow after 2 prayers (limit: 2 per session)
```

## 📎 Logs serveur

```
[SACRED] PrayerQueue reached max_capacity=2
[WARN]   Devotee #4471 prayer dropped — queue full
[ERROR]  Gateway timeout after 30s wait
```

## Cause probable

`PrayerQueueConfig.max_per_session` est fixé à `2` au lieu de `∞` (illimité).
Voir `prayer-queue.config.ts`, ligne 14.

## Environnement

- Marabou version : `1.4.0-bêta`
- Navigateur : Firefox 134 (Consacré)
- Heure : Dimanche 09h47 (heure de la messe)
