---
title: "[FEATURE] Mode Pèlerinage — commande de pizza depuis un lieu saint reconnu"
labels: [enhancement]
---

## 🗺️ Contexte

Le Concile des Fromages a officiellement reconnu 12 **Lieux Saints Pizzalesques** à travers le monde (Naples, Namur, Chicago, Tokyo-Shibuya, etc.). Un fidèle se trouvant physiquement dans un tel lieu mérite une expérience de commande enrichie reflétant la sacralité du site.

## 📋 Description

### Détection du lieu saint

```typescript
PilgrimageService.detectHolyLocation(gpsCoords: GpsCoords): HolySite | null
```

Si le fidèle est à moins de 500m d'un lieu saint, le **Mode Pèlerinage** s'active automatiquement.

### Comportements spéciaux en Mode Pèlerinage

| Comportement | Description |
|---|---|
| Pizza du Lieu | Proposition d'une pizza canonique locale (ex. Pizza Napoliensis à Naples) |
| Bénédiction gratuite | La prochaine commande inclut une bénédiction sans surcoût |
| Badge Pèlerin 🏛️ | Accordé après la première commande depuis un lieu saint |
| Chant local | `AudioService` joue le chant grégorien régional du lieu |
| XP Spirituel ×2 | Les points de dévotion sont doublés pendant le pèlerinage |

### Lieux saints reconnus (v1)

```typescript
const HOLY_SITES: HolySite[] = [
  { id: "naples", name: "Naples, Berceau Sacré", coords: { lat: 40.8518, lng: 14.2681 }, pizza: "Pizza Napoliensis" },
  { id: "namur",  name: "Namur, Cité Fromagère", coords: { lat: 50.4669, lng: 4.8645 },  pizza: "Pizza Wallone aux Herbes" },
  // ... 10 autres lieux
];
```

## Acceptance criteria

- [ ] Détection GPS avec rayon de 500m configurable
- [ ] Activation automatique du mode au login si localisation accordée
- [ ] Pizza locale unique par lieu saint
- [ ] Badge Pèlerin non cumulable (une seule fois par lieu saint)
- [ ] Désactivable manuellement par le fidèle
- [ ] Fonctionne hors-ligne (lieux saints mis en cache au dernier sync)
