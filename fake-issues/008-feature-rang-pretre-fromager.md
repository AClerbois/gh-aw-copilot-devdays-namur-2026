---
title: "[FEATURE] Système de rangs et de progression pour les Prêtres Fromagers"
labels: [enhancement]
---

## ⛪ Contexte

Actuellement, tous les `CheesePriest` ont le même niveau de privilèges dès leur ordination. Il n'existe aucune progression, ce qui nuit à la motivation des prêtres débutants et à la valorisation des prêtres expérimentés.

## 📋 Description

### Hiérarchie des rangs

```
Novice Fromager        (0 – 99 bénédictions)
Acolyte du Fromage    (100 – 499 bénédictions)
Diacre Pizzaïque      (500 – 1 499 bénédictions)
Prêtre Fromager       (1 500 – 4 999 bénédictions)
Prêtre Senior         (5 000 – 14 999 bénédictions)
Archevêque du Pavé    (15 000 – 49 999 bénédictions)
Cardinal Mozzarella   (50 000+ bénédictions)
Grand Prêtre Fromager (nomination manuelle par le Concile)
```

### Règles de progression

- La progression est basée sur le nombre de **bénédictions validées** (`BlessingCertificate` émis)
- Les rangs débloquent des **capacités sacrées** (`SacredAbility`) :

| Rang | Capacité débloquée |
|---|---|
| Acolyte | Peut bénir la mozzarella ordinaire seul |
| Diacre | Peut approuver les confessions |
| Prêtre | Peut co-signer les bénédictions di bufala |
| Senior | Peut initier une procédure d'excommunication |
| Archevêque | Peut réviser les scores HDE |
| Cardinal | Peut proposer un amendement au Dogme Fromager |

### Service à implémenter

```typescript
interface RankService {
  getCurrentRank(priestId: string): PriestRank;
  getProgressToNextRank(priestId: string): RankProgress;
  checkPromotion(priestId: string): void; // appelé après chaque bénédiction
  notifyPromotion(priestId: string, newRank: PriestRank): void;
}
```

## Acceptance criteria

- [ ] 8 rangs implémentés avec seuils configurables dans `rank-config.yaml`
- [ ] Promotion automatique déclenchée par `checkPromotion()` après chaque bénédiction
- [ ] Notification push + email à chaque promotion
- [ ] Les capacités sacrées sont vérifiées avant chaque action sensible
- [ ] Dashboard de progression visible dans le profil du prêtre
- [ ] Le rang `Grand Prêtre` reste une nomination manuelle uniquement
