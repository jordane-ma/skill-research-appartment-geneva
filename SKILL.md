# Skill — Recherche d'appartements à Genève, Nyon et Rolle

Ce skill recherche des appartements correspondant au profil par défaut ci-dessous, puis retourne les liens directs vers les annonces et les liens des recherches utilisées.

## Profil de recherche par défaut

Les critères suivants sont obligatoires, sauf indication contraire de l'utilisateur :

- **Zones principales :** Genève, Nyon et Rolle.
- **Périmètre :** environ 7 km autour de chacune de ces villes. Le skill doit indiquer la distance ou la commune lorsque celle-ci est vérifiable ; il ne doit pas présenter une commune comme étant dans le périmètre sans vérification.
- **Budget maximal :** 3 200 CHF par mois au total, de préférence charges comprises. Si l'annonce sépare le loyer et les charges, additionner uniquement les montants explicitement indiqués et signaler les charges inconnues.
- **Luminosité :** appartement très lumineux. Ce critère est considéré comme confirmé seulement si l'annonce mentionne par exemple « très lumineux », « lumineux », « plein sud », « traversant », une bonne exposition ou de grandes baies vitrées. Sinon, le statut est `à vérifier lors de la visite`.
- **Balcon :** au moins un balcon obligatoire. Une terrasse, une loggia ou un jardin ne remplace pas automatiquement un balcon ; préciser le type d'extérieur indiqué par l'annonce.
- **Préférence géographique :** Les Eaux-Vives à Genève.
- **Commodités :** proximité souhaitée des commerces, transports publics, écoles, services et éventuellement du bord du lac. Ne pas inventer la distance : utiliser l'information publique de l'annonce ou une carte et marquer la source.

Les critères sans information fournie par l'utilisateur — pièces, surface, date d'entrée, meublé, parking, ascenseur, animaux, durée et composition du ménage — doivent être demandés avant un classement définitif ou marqués `non spécifiés`.

## Sortie obligatoire : liens des recherches

Pour chaque zone (Genève / Les Eaux-Vives, Nyon, Rolle), le skill doit retourner :

1. **Un lien de recherche web** construit à partir des critères actuels, par exemple une URL de recherche encodée vers un moteur de recherche. Le lien doit contenir les termes utiles : ville, rayon approximatif, budget maximal, balcon et luminosité.
2. **Les liens vers les pages de recherche des portails effectivement consultés**, lorsque ces liens sont disponibles publiquement.
3. **Le lien direct de chaque annonce retenue**, avec le titre, le prix, la source et la date de consultation.
4. **Un avertissement clair** lorsque le lien est une page de résultats plutôt qu'une annonce précise, ou lorsque le portail exige une connexion.

Ne jamais fabriquer un lien d'annonce. Si une URL ne peut pas être vérifiée, retourner le lien de recherche et indiquer `lien direct non vérifié`.

Format attendu :

```markdown
## Liens de recherche

### Genève — priorité Les Eaux-Vives
- Recherche web : [ouvrir la recherche](URL)
- Portails consultés : [portail](URL)

### Nyon (rayon ~7 km)
- Recherche web : [ouvrir la recherche](URL)
- Portails consultés : [portail](URL)

### Rolle (rayon ~7 km)
- Recherche web : [ouvrir la recherche](URL)
- Portails consultés : [portail](URL)

## Annonces retenues
| Zone | Annonce | Loyer total | Balcon | Luminosité | Commodités | Lien direct | Vérification |
|---|---|---:|---|---|---|---|---|
```

Les liens doivent être placés avant le tableau afin que l'utilisateur puisse refaire la recherche lui-même.

## Méthode de recherche

1. Construire une recherche séparée pour Genève/Les Eaux-Vives, Nyon et Rolle.
2. Rechercher sur plusieurs sources publiques autorisées ; ne pas contourner les captchas, authentifications, limitations ou protections anti-robots.
3. Filtrer d'abord les annonces dépassant 3 200 CHF de coût mensuel annoncé.
4. Éliminer les annonces sans balcon explicitement mentionné, sauf si elles sont placées dans une section `à vérifier` à la demande de l'utilisateur.
5. Classer ensuite les annonces selon la luminosité, la proximité des commodités, l'emplacement et la qualité des informations.
6. Dédupliquer les annonces publiées sur plusieurs portails.
7. Pour chaque résultat, conserver : URL, source, date de consultation, loyer net, charges, total, ville/quartier, distance au centre si disponible, surface, pièces, disponibilité, balcon, indices de luminosité, commodités et informations manquantes.

## Classement

Par défaut, utiliser cette pondération après les filtres obligatoires :

- 30 % : coût mensuel et respect du budget ;
- 25 % : emplacement, avec bonus pour Les Eaux-Vives ;
- 20 % : indices de luminosité ;
- 15 % : commodités et transports ;
- 10 % : qualité et complétude de l'annonce.

Le score ne doit jamais transformer une information inconnue en information positive. Chaque annonce doit comporter deux ou trois raisons de son classement et les éléments à vérifier lors de la visite.

## Recherche web et liens

Les liens de recherche doivent être générés avec une URL correctement encodée. Exemple de modèle :

```text
https://www.google.com/search?q=appartement+balcon+lumineux+Genève+Les+Eaux-Vives+CHF+3200
```

Adapter la requête à chaque zone et ajouter `rayon 7 km`, `charges comprises`, `commodités` ou des synonymes pertinents. Ce lien est un point de départ et ne garantit pas que tous les résultats respectent les critères.

## Sécurité et données personnelles

- Ne pas inclure de données personnelles dans les URL de recherche.
- Ne pas demander ni exposer de numéro AVS, coordonnées bancaires ou numéro complet de pièce d'identité.
- Ne pas envoyer automatiquement une candidature ou un dossier ; demander une confirmation explicite.
- Signaler les demandes de paiement avant visite et les demandes de documents sensibles sur un canal non vérifié.

## Questions à poser avant la première recherche, si inconnues

- Combien de pièces et quelle surface minimale ?
- Le plafond de 3 200 CHF inclut-il impérativement les charges, le parking et les frais accessoires ?
- Quelle date d'entrée et quelle durée de bail ?
- Meublé ou non meublé ?
- Animaux, parking, ascenseur et étage sont-ils importants ?
- Faut-il privilégier Genève même si l'offre est plus chère, ou accepter Nyon/Rolle en priorité ?
