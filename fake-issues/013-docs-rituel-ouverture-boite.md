---
title: "[DOCS] Documenter le Rituel d'Ouverture de la Boîte Sacrée"
labels: [documentation]
---

## 📖 Description

Le `BoxOpeningRitual` est l'un des modules les plus utilisés de l'application, mais il ne dispose d'**aucune documentation** dans le wiki ni dans le code. Les nouveaux développeurs et les Prêtres Fromagers non techniques ne savent pas comment il fonctionne ni dans quel ordre les étapes se déroulent.

## 📋 Documentation à rédiger

### 1. Guide conceptuel (wiki)

Expliquer le rituel en langage accessible :
- Pourquoi ouvrir une boîte de pizza est un acte sacré
- Les 5 étapes du rituel dans l'ordre canonique
- Ce qui se passe si une étape échoue

### 2. Documentation de l'API (`BoxOpeningRitual.ts`)

```typescript
/**
 * Performs the Sacred Box Opening Ritual.
 *
 * Steps:
 * 1. Verify the box integrity (BoxIntegrityChecker)
 * 2. Play the Gregorian chant (AudioService → kyrie_pizza_eleison.mp3)
 * 3. Invoke the blessing (BlessingRitual.blessBox)
 * 4. Record the ritual in the liturgical log (LiturgicalLog.record)
 * 5. Notify the community (NotificationService.broadcastOpening)
 *
 * @param orderId - The ID of the sacred order
 * @param performerId - The devotee performing the ritual
 * @throws BoxIntegrityException if the box has been tampered with
 * @throws AudioUnavailableException if the chant cannot be played
 */
async perform(orderId: string, performerId: string): Promise<RitualResult>
```

### 3. Guide de dépannage

| Erreur | Cause probable | Solution |
|---|---|---|
| `AudioUnavailableException` | `kyrie_pizza_eleison.mp3` absent | Voir issue #3 — migration AudioService v2 |
| `BoxIntegrityException` | Boîte ouverte avant le rituel | Contacter le livreur hérétique |
| `BlessingTimeoutException` | Aucun prêtre disponible | `EmergencyBlessingProtocol` |

## Acceptance criteria

- [ ] Page wiki créée : `Rituels > Ouverture de la Boîte`
- [ ] JSDoc complet sur `BoxOpeningRitual.perform()`
- [ ] Diagramme de séquence ajouté dans `docs/rituals/`
- [ ] Guide de dépannage pour les 3 erreurs principales
- [ ] Relecture par un Prêtre Fromager certifié
