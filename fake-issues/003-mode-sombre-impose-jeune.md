---
title: "[BUG] Activer le mode sombre déclenche un jeûne non consenti de 24h"
labels: [bug, ux]
---

## 🌙 Description du problème

Lorsqu'un fidèle active le **mode sombre** dans ses préférences (`Settings > Apparence > Mode sombre`), le système appelle accidentellement `ExpiationMode.activate(userId)` — déclenchant un jeûne expiatoire de 24h et verrouillant le compte.

L'utilisateur ne peut plus commander de pizza pendant 24h simplement parce qu'il préfère un fond noir.

## 🔁 Étapes pour reproduire

1. Se connecter avec un compte fidèle actif
2. Aller dans **Paramètres > Apparence**
3. Activer **Mode sombre**
4. Observer le message : *« Ton âme a sombré dans les ténèbres. Jeûne expiatoire de 24h engagé. »*

## ✅ Comportement attendu

Le mode sombre change uniquement le thème visuel de l'interface. Aucun impact liturgique.

## ❌ Comportement actuel

```
[SACRED] ExpiationMode activated for user #8823
[INFO]   Reason: DARK_MODE_ENABLED
[INFO]   Expiation duration: 24h
[WARN]   OrderService: account locked for user #8823
```

## Cause probable

Dans `ThemeService.ts`, l'import de `ExpiationMode` a été ajouté par erreur lors d'un refactoring. La méthode `setDarkMode()` appelle `this.expiationMode.activate()` au lieu de `this.themeEngine.setDark()`.

```typescript
// ThemeService.ts - ligne 42 (incorrect)
async setDarkMode(userId: string) {
  await this.expiationMode.activate(userId); // ← mauvais import !
}
```

## Note

Dix-neuf fidèles sont actuellement en jeûne forcé involontaire. Une compensation spirituelle est recommandée.
