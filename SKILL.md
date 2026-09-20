# Skill — Recherche d'appartements à Genève

Ce skill aide à trouver des logements à Genève et dans les communes voisines, à comparer les annonces et à préparer un dossier de candidature prêt à envoyer.

## Capacités

- Clarifier les critères de recherche : budget, communes, date d'entrée, surface, pièces, étage, ascenseur, balcon, parking, animaux, transports et contraintes particulières.
- Rechercher des annonces publiques sur le web et conserver l'URL, la date de consultation et les informations visibles.
- Dédupliquer les annonces et signaler les informations manquantes, incohérences ou risques d'arnaque.
- Classer les résultats selon une note explicable, sans inventer les données absentes.
- Produire un tableau comparatif exportable en Markdown ou CSV.
- Générer un dossier de candidature personnalisé : checklist, lettre de motivation, résumé candidat et noms de fichiers cohérents.
- Vérifier le dossier avant envoi et rappeler les données sensibles qui ne doivent pas être transmises inutilement.

## Utilisation

Exemples :

- `Je cherche un 3 pièces à Genève, maximum 2 200 CHF charges comprises, dès le 1er décembre.`
- `Recherche dans Carouge, Lancy, Onex et Genève, proche d'un tram, avec balcon et sans agence si possible.`
- `Analyse ces annonces et classe-les selon mes critères : ...`
- `Prépare mon dossier pour l'annonce X à partir des documents que je fournis.`
- `Vérifie que mon dossier est complet et rédige le message de candidature.`

## Déroulement recommandé

1. **Profil et contraintes**
   - Demander uniquement les informations nécessaires.
   - Distinguer les critères obligatoires, préférés et rédhibitoires.
   - Confirmer la devise, le budget maximal et si les charges/parking sont inclus.

2. **Recherche**
   - Utiliser des recherches web ciblées par commune, type de logement et budget.
   - Respecter les conditions d'utilisation des sites et ne pas contourner les protections anti-robots, les connexions ou les captchas.
   - Ne pas prétendre avoir accès à des annonces privées ou à des données derrière authentification.
   - Pour chaque annonce, relever : titre, URL, source, date de consultation, loyer net, charges, total annoncé, pièces, surface, adresse/quartier, disponibilité, étage, équipements, bailleur/régie et contact lorsqu'ils sont publics.

3. **Validation et classement**
   - Marquer chaque valeur comme `confirmée`, `déduite` ou `inconnue`.
   - Ne jamais déduire une adresse exacte, un montant ou une disponibilité à partir d'une information ambiguë.
   - Détecter les doublons avec l'URL, le titre, le prix et les caractéristiques.
   - Signaler les demandes de paiement avant visite, les coordonnées incohérentes, les prix anormalement bas et les demandes de documents sensibles sur un canal non vérifié. Ne pas déclarer une fraude avec certitude sans preuve.
   - Utiliser par défaut la pondération suivante, à ajuster avec l'utilisateur : budget 30 %, emplacement/transports 25 %, date d'entrée 15 %, surface/pièces 15 %, équipements 10 %, qualité des informations 5 %.

4. **Dossier**
   - Demander à l'utilisateur quels documents ils possèdent avant de produire la checklist.
   - Préparer une checklist adaptée au bailleur/régie et à la situation personnelle ; les exigences peuvent varier.
   - Ne pas fabriquer d'attestation, de fiche de salaire, de signature ou d'information personnelle.
   - Préparer des versions avec les données sensibles minimisées lorsque c'est acceptable.
   - Garder les documents dans un dossier local privé, avec des noms sans données sensibles, par exemple `01_identite.pdf`, `02_revenus.pdf`, `03_attestation_poursuites.pdf`.

5. **Sorties**
   Produire, selon la demande :
   - un tableau de résultats ;
   - un tableau des critères manquants ;
   - une checklist du dossier ;
   - une lettre de motivation ou un e-mail en français, sobre et personnalisé ;
   - une fiche récapitulative du candidat ;
   - une liste des prochaines actions et des échéances.

## Format du tableau d'annonces

| Score | Annonce | Loyer total | Pièces/surface | Commune/quartier | Entrée | Transports | Source et date | Statut |
|---:|---|---:|---|---|---|---|---|---|

Le score doit être accompagné de deux ou trois raisons positives et des points à vérifier.

## Protection des données

- Traiter les pièces d'identité, revenus, coordonnées bancaires et attestations comme hautement sensibles.
- Ne pas afficher de numéro complet, date de naissance, numéro AVS ou coordonnées bancaires dans un tableau de comparaison.
- Ne pas envoyer automatiquement un dossier ou un e-mail : demander une confirmation explicite avant tout envoi.
- Vérifier le destinataire, l'annonce et les pièces jointes avant l'envoi.
- Respecter les demandes de suppression et ne conserver que les informations nécessaires à la recherche.

## Limites

Le skill fournit une aide à la recherche et à la préparation administrative ; il ne garantit ni la disponibilité d'un logement, ni l'acceptation du dossier, ni l'exactitude d'une annonce. Les exigences légales et celles des régies doivent être vérifiées auprès de la source officielle ou du bailleur.
