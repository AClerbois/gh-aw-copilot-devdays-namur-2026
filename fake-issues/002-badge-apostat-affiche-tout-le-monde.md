---
title: "[BUG] Le badge « Apostat » s'affiche sur tous les fidèles après la mise à jour 1.4.1"
labels: [bug, critical]
---

## 🚨 Description du problème

Depuis le déploiement de `v1.4.1-hotfix`, le badge 🔥 **Apostat** s'affiche sur **tous les profils** dans le tableau de bord communautaire — y compris sur le profil du Grand Prêtre lui-même.

La communauté est en état de choc. Le nombre de tickets de support spirituel a augmenté de 847 % en 2 heures.

## 🔁 Étapes pour reproduire

1. Se connecter avec n'importe quel compte fidèle
2. Naviguer vers **Communauté > Annuaire des Fidèles**
3. Tous les profils affichent le badge 🔥 Apostat

## ✅ Comportement attendu

Le badge Apostat ne s'affiche que sur les comptes ayant reçu une sentence d'apostasie formelle via `ExcommunicationService.markApostate(userId)`.

## ❌ Comportement actuel

```typescript
// BadgeService.getBadges() retourne pour TOUS les users :
[{ id: "apostate", label: "Apostat", icon: "🔥", visible: true }]
```

## Analyse préliminaire

Le commit `3f7a92b` de la branche `hotfix/1.4.1` a accidentellement inversé la condition dans `BadgeService.ts` :

```typescript
// Avant (correct) :
if (user.status === "APOSTATE") showBadge("apostate");

// Après le hotfix (incorrect) :
if (user.status !== "APOSTATE") showBadge("apostate");
```

## Impact

**CRITIQUE** — Toute la communauté est marquée comme apostate. Réversion immédiate requise.
