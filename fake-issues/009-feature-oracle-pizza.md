---
title: "[FEATURE] Oracle de la Pizza — prédictions mystiques basées sur les garnitures"
labels: [enhancement, fun]
---

## 🔮 Contexte

Le Livre des Lamentations Fromagères, Appendice IX, affirme que *« les garnitures de la pizza révèlent le destin de celui qui les choisit »*. Il est temps d'implémenter cette prophétie sous forme de fonctionnalité.

## 📋 Description

### Point d'entrée

```typescript
OracleService.consult(pizza: Pizza, devoteeId: string): OracleProphecy
```

### Logique de prédiction

L'oracle analyse les ingrédients de la pizza commandée et génère une prophétie personnalisée. Les règles de base :

| Ingrédient | Présage |
|---|---|
| Truffe | Grande prospérité spirituelle à venir |
| Anchois | Des épreuves fromagères se profilent |
| Gorgonzola | Transformation profonde de l'âme |
| Champignons | Un secret sera révélé sous terre |
| Piments | Passion dévorante, prendre garde au feu |
| Quatre fromages | Équilibre parfait — période de grâce |
| Jambon | Confort du quotidien, attention à la routine |
| Œuf | Nouveau départ, renaissance prochaine |

### Format de la prophétie

```typescript
interface OracleProphecy {
  text: string;           // Texte mystique de la prophétie
  omen: "FAVORABLE" | "NEUTRAL" | "OMINOUS";
  duration: string;       // "jusqu'à la prochaine lune fromagère"
  luckyIngredient: string; // Ingrédient porte-bonheur du moment
  warningIngredient?: string; // Ingrédient à éviter
}
```

### Exemple de sortie

```json
{
  "text": "Les anchois révèlent une tourmente imminente, mais le gorgonzola promet une métamorphose glorieuse. Navigue avec foi, fils de la Pâte.",
  "omen": "NEUTRAL",
  "duration": "jusqu'à la prochaine pleine lune fromagère",
  "luckyIngredient": "gorgonzola",
  "warningIngredient": "anchois"
}
```

## Acceptance criteria

- [ ] `OracleService` analyse tous les ingrédients de la pizza
- [ ] Les combinaisons d'ingrédients peuvent modifier la prophétie (ex. truffe + anchois = destin ambigu)
- [ ] La prophétie est affichée dans une modale après la confirmation de commande
- [ ] Option pour partager la prophétie sur le fil communautaire
- [ ] Un historique des prophétie est conservé dans le profil (`OracleHistory`)
- [ ] L'oracle ne fonctionne pas pour les pizzas hérétiques (score HDE > 0.5)
