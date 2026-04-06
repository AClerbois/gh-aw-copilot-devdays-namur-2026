---
title: "[DOCS] Rédiger le guide d'excommunication à destination des modérateurs"
labels: [documentation]
---

## 📖 Description

Les modérateurs (Prêtres Fromagers de rang Diacre et supérieur) disposent du pouvoir d'excommunication depuis la v1.2, mais aucun guide n'explique la procédure à suivre. Des excommunications abusives ou mal exécutées ont déjà été recensées.

## 📋 Documentation à rédiger

### 1. Quand excommunier un fidèle

Le guide doit définir clairement les cas légitimes :

| Infraction | Niveau | Procédure |
|---|---|---|
| Pizza à l'ananas commandée intentionnellement | Niveau 3 — Grave | Excommunication directe |
| Récidive de pizza à la crème fraîche | Niveau 2 — Modéré | Avertissement + excommunication si récidive |
| Apostasie publique (déclaration contre le Fromage) | Niveau 4 — Extrême | Grand Prêtre requis |
| Oubli du chant grégorien | Niveau 0 — Léger | Confession, pas d'excommunication |

### 2. Procédure pas à pas

```
1. Constater l'infraction et la documenter dans InfractionLog
2. Vérifier que le fidèle a reçu au moins 1 avertissement (sauf niveau 3+)
3. Obtenir la co-signature d'un second prêtre (sauf urgence)
4. Appeler ExcommunicationService.excommunicate(userId, reason, evidence)
5. Notifier le fidèle via NotificationService (template EXCOMMUNICATION_NOTICE)
6. Archiver la sentence dans le SentenceArchive
```

### 3. Procédure de réintégration

Un fidèle excommunié peut être réintégré via `ReintegrationService.apply()` après :
- Une période de jeûne de 7 jours
- La soumission d'une Lettre de Contrition
- Validation par un Prêtre de rang Senior minimum

## Acceptance criteria

- [ ] Page wiki créée : `Administration > Guide d'Excommunication`
- [ ] Tableau des infractions avec niveaux et procédures
- [ ] Procédure de réintégration documentée
- [ ] FAQ : 5 questions fréquentes des modérateurs
- [ ] Exemples de logs attendus pour chaque étape
- [ ] Validé par le Grand Prêtre (ou délégué)
