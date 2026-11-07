# Méthode et chaîne de calcul

La chaîne a été testée de bout en bout sur des DPE réels de l'Indre (36).

## 1. De l'annonce au DPE officiel

L'outil retrouve **le DPE officiel correspondant à l'annonce** dans la base publique
de l'ADEME, sans demander à l'utilisateur le numéro du diagnostic. La méthode de
rapprochement n'est pas publiée.

- Testé sur des annonces réelles de deux sites différents : DPE retrouvé à chaque fois.
- En mode agent, cette étape disparaît : le numéro DPE est saisi directement.

## 2. Du DPE au modèle thermique

Pour les DPE récents (méthode 3CL, depuis juillet 2021), la base ADEME fournit le
détail du logement paroi par paroi : surfaces et isolation des murs, planchers et
plafonds, menuiseries, systèmes de chauffage et d'eau chaude.

Ce modèle est recalculé avec **[Open3CL](https://github.com/Open3CL/engine)**,
implémentation libre de la méthode officielle. Écart avec les DPE d'origine : 1 à
2 % sur les cas testés (par exemple E 286 → 287, F 407 → 405, G 445 → 434).

## 3. Les gestes de travaux

Chaque geste modifie le modèle, qui est ensuite recalculé :

| Geste | Hypothèse |
|---|---|
| Isolation des murs (intérieur ou extérieur) | R = 3,7 m²·K/W |
| Isolation des combles | R = 7, ou renfort si U > 0,3 |
| Isolation du plancher bas | R = 3 |
| Remplacement des fenêtres | Uw = 1,3 |
| Pompe à chaleur air/eau | sur émetteurs existants |
| Pompe à chaleur air/air | dimensionnée selon la surface |
| Chauffe-eau thermodynamique | 200 L |

Exclus pour l'instant : parois donnant sur un local chauffé, planchers sur
terre-plein, portes.

**L'étiquette retenue est la plus mauvaise des deux classes, énergie et CO₂**, comme
dans le DPE officiel. Le moteur ne renvoie que la classe énergie ; la règle du CO₂ est
réappliquée. C'est elle qui explique certains « sauts » très bon marché.

Chaque scénario est aussi recalculé avec le **coefficient électrique de 2027**
(1,7), pour montrer l'étiquette que le logement aura après la réforme.

## 4. Chiffrage

- Quantités tirées des surfaces du DPE (m² de murs, de combles, de fenêtres…).
- Multipliées par une **grille de prix simulée** : TTC, TVA à 5,5 %, zone rurale de
  l'Indre, hors aides (MaPrimeRénov', CEE). À remplacer par des prix d'artisans réels.
- Ventilées par corps de métier (plaquiste-isolateur, chauffagiste, frigoriste,
  plombier, menuisier, électricien, peintre), avec les travaux induits : un doublage
  intérieur oblige à déplacer les prises et à repeindre.

## 5. Facture et retour sur investissement

La facture est recalculée aux prix de l'énergie utilisés par le DPE officiel
(écart ≤ 3 % avec la facture d'origine). Le temps de retour est calculé hors aides :
c'est un plancher prudent.

## 6. Composition des trois parcours

- **Express** : le meilleur rapport « classes gagnées / euro ».
- **Équilibre** : le meilleur compromis entre facture, lettre et budget.
- **Grand saut** : viser B et sortir des énergies fossiles.

Des alertes contextuelles signalent les cas trompeurs : lettre gagnée sans économies,
copropriété à consulter, bâti patrimonial, budget proche du prix du bien.

## Limites connues

- Les DPE de 2021–2022 (première version de la méthode) n'ont pas toujours le détail
  de l'enveloppe ; ils représentent environ la moitié du parc de l'Indre. Ils
  demanderont un modèle simplifié, signalé comme « fiabilité réduite ».
- La méthode 3CL pénalise davantage l'isolation par l'extérieur que par l'intérieur
  (traitement des ponts thermiques), ce qui ne reflète pas toujours la réalité.
- Le DPE est un calcul conventionnel : les économies affichées sont celles du DPE, pas
  une promesse de facture réelle.
