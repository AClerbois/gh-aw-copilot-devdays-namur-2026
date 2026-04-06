---
title: "[BUG] Notifications doublées les jours de fête du calendrier liturgique"
labels: [bug]
---

## 🔔 Description du problème

Le `LiturgicalCalendarService` envoie deux notifications identiques les jours de **fête de niveau 2 et supérieur** (ex. Sainte Margherita, La Diavola des Ténèbres).

Les fidèles reçoivent deux fois le même message push, deux fois le même email, et deux fois la notification in-app. Lors de la fête de Noël de la Pizza Royale, certains fidèles ont reçu jusqu'à 6 notifications.

## 🔁 Étapes pour reproduire

1. Configurer la date système au **1er janvier** (jour de Sainte Margherita)
2. Déclencher manuellement : `LiturgicalCalendarService.triggerDailyNotifications()`
3. Observer les notifications reçues : **2 notifications identiques**

## ✅ Comportement attendu

Une seule notification par canal (push, email, in-app) par jour de fête.

## ❌ Comportement actuel

```
[SACRED] Notification sent: "Aujourd'hui, nous honorons Sainte Margherita."
[SACRED] Notification sent: "Aujourd'hui, nous honorons Sainte Margherita." ← doublon
```

## Analyse

Le `NotificationService` est appelé deux fois :
1. Par `LiturgicalCalendarService.onFeastDay()` (scheduler)
2. Par `DailyDigestJob.run()` qui inclut également les jours de fête

Les deux jobs s'exécutent à `12:00:00` sans mécanisme de déduplication.

## Fix suggéré

Ajouter une clé d'idempotence `feast_day_<date>_<userId>` dans `NotificationService.send()` pour éviter les doublons dans une fenêtre de 1h.
