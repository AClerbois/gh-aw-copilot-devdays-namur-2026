---
title: "[FEATURE] Implémenter le module de confession numérique"
labels: [enhancement]
---

## 📿 Contexte

Actuellement, les fidèles qui ont commis une infraction mineure (ex. avoir pensé à la calzone, avoir regardé une publicité pour pizza surgelée) n'ont aucun moyen de se racheter sans passer par le processus lourd d'excommunication/réintégration.

Le **module de confession numérique** permettrait d'expier les fautes légères directement depuis l'application.

## 📋 Description de la fonctionnalité

### Interface utilisateur

Un bouton **« Se Confesser »** accessible depuis le menu principal, disponible uniquement les mardis et jeudis (jours de confession définis par le Dogme Fromager).

### Flux de confession

```
Fidèle ouvre la confession
         ↓
ConfessionService.startSession(userId)
         ↓
Affichage du formulaire : "Quelle est ta faute, fils de la Pâte ?"
         ↓
Sélection dans le catalogue des péchés (PeccatumCatalog)
         ↓
Attribution d'une pénitence par PenanceEngine
         ↓
Exécution de la pénitence (voir ci-dessous)
         ↓
AbsolutionService.absolve(userId) → badge "Purifié ✨"
```

### Catalogue des péchés (`PeccatumCatalog`)

| Péché | Pénitence |
|---|---|
| Pensée involontaire à la calzone | Commander une Margherita dans les 24h |
| Retard de 5 min sur une livraison | Réciter 1 _Ave Fromage_ |
| Oubli du chant grégorien | Écouter `kyrie_pizza_eleison.mp3` 3 fois |
| Utilisation de ketchup | Jeûne de 2h + don de 1€ au Fonds Fromager |
| Regard concupiscent sur une pizza hawaïenne | Séance de purification (5 _Ave Fromage_) |

### Acceptance criteria

- [ ] Confession disponible mardis et jeudis uniquement (retourner `CONFESSION_NOT_AVAILABLE_TODAY` sinon)
- [ ] `PeccatumCatalog` extensible via fichier YAML
- [ ] Pénitences exécutables in-app (relecture audio, commande forcée, etc.)
- [ ] Badge « Purifié ✨ » valide 7 jours
- [ ] Pas de confession si le compte est en statut `EXCOMMUNICATED` (cas non éligible)
