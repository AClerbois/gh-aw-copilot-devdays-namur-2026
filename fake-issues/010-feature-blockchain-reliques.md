---
title: "[FEATURE] Enregistrement des reliques fromagères sur la CheeseChain"
labels: [enhancement]
---

## ⛓️ Contexte

Certaines pizzas atteignent un niveau de perfection tel qu'elles sont déclarées **Reliques Fromagères** par le Grand Prêtre. Actuellement, ces déclarations n'existent que dans le livre physique du Grand Prêtre et ne sont pas traçables numériquement.

## 📋 Description

### Enregistrement d'une relique

```typescript
CheeseChainService.mintRelic(
  pizza: Pizza,
  declaration: RelicDeclaration,
  highPriestSignature: CryptoSignature
): RelicToken
```

### Structure d'une `RelicDeclaration`

```typescript
interface RelicDeclaration {
  pizzaId: string;
  reason: string;              // "Perfection fromagère absolue constatée le 12/03/2026"
  witnesses: string[];         // IDs de 3 prêtres témoins minimum
  heresyScore: number;         // Doit être 0.0
  blessingCertificateId: string;
}
```

### Token de relique

Chaque relique génère un **NFR** (_Non-Fungible Relic_) avec :
- Métadonnées immuables (ingrédients, lieu, prêtre officiant)
- QR code vérifiable
- Timestamp liturgique infalsifiable
- Lien vers la photo de la pizza (si disponible)

### Consultation du registre

```typescript
CheeseChainService.getRelicRegistry(): RelicToken[]
CheeseChainService.verifyRelic(tokenId: string): boolean
```

### Règles de validation

- Score HDE obligatoirement `0.0`
- Signature cryptographique du Grand Prêtre requise
- Minimum 3 prêtres témoins présents
- La pizza ne peut pas avoir été consommée avant la déclaration (vérification via `OrderService.getStatus()`)

## Acceptance criteria

- [ ] `mintRelic()` valide toutes les règles avant émission
- [ ] Le token est immuable une fois émis
- [ ] `verifyRelic()` accessible publiquement sans authentification
- [ ] Interface d'administration pour le Grand Prêtre
- [ ] Notification à toute la communauté lors d'une nouvelle relique
- [ ] Registre consultable depuis le profil public du repository
