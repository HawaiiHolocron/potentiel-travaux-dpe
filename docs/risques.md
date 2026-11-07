# Risques et défis

## Juridiques

| Risque | Position retenue |
|---|---|
| **Extraction d'annonces** (sites d'annonces) | Protection anti-robots, et jurisprudence protégeant les bases de données d'annonces (Cass. civ. 1ʳᵉ, 5 octobre 2022, droit *sui generis*). Pistes : extension de navigateur déclenchée par l'utilisateur sur la page qu'il consulte, capture d'écran lue par IA, copier-coller en secours. Le mode agent n'a pas ce problème. |
| **Données personnelles** | Les données DPE sont publiques, mais un logement identifié reste lié à une personne. **Aucune adresse n'est jamais affichée** ; seule l'étiquette et le détail technique sont utilisés (RGPD). |
| **Relation avec les agents** | L'outil ne doit jamais permettre de contourner un mandat : il n'affiche que ce qui sert au diagnostic. C'est aussi une condition pour que les agents l'adoptent. |
| **Visuels « après » générés par IA** | Risque de pratique commerciale trompeuse s'ils sont mal encadrés : mention « visualisation non contractuelle, générée par IA » et filigrane obligatoires. |
| **Licence du moteur** | Open3CL est sous GPL-3.0 : à intégrer côté serveur, ou à publier sous licence compatible. |
| **Chiffres présentés** | Toujours « estimation indicative, pas un devis », hors aides, prix sourcés. |

## Techniques

- **Accès aux données détaillées** : le téléchargement du détail complet des DPE n'est
  accessible que depuis la France, d'où un hébergement français (Clever Cloud,
  Scaleway, OVH). Les conditions d'utilisation de ce service sont à vérifier avant
  industrialisation.
- **API ADEME capricieuse** : refus ponctuels sur certains codes postaux ; prévoir des
  relances et un cache.
- **DPE de première génération** (2021–2022) : environ 50 % du parc local, sans
  enveloppe détaillée.
- **Prix** : la grille actuelle est simulée. La crédibilité de l'outil dépend d'une
  grille calée sur de vrais devis locaux.

## Produit

- **Lettre ≠ confort ≠ facture.** Un parcours peut gagner deux lettres pour presque
  rien sur la facture. L'interface doit le dire clairement, sinon l'utilisateur se
  sentira trompé.
- **Volet esthétique.** Les travaux qui changent la lettre (doublage, combles, PAC,
  chauffe-eau) ne se voient presque pas. Des photos « après » n'ont de sens qu'avec un
  bloc esthétique distinct (peinture, sols, cuisine, salle d'eau, home staging),
  **chiffré à part et présenté comme sans effet sur la lettre**.
- **Confiance.** Une estimation trop optimiste peut fausser une offre d'achat. Le mode
  agent, à partir de données exactes, est le terrain le plus sûr pour démarrer.
