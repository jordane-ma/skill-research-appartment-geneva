# Skill — Recherche d'appartements à Genève, Nyon et Rolle

Ce skill recherche, vérifie et classe des appartements correspondant au profil de l'utilisateur. Il ne retourne **que les 10 annonces les plus pertinentes au maximum** et exclut les liens non fonctionnels ou non vérifiés.

## Profil de recherche par défaut

Les critères suivants sont obligatoires, sauf indication contraire de l'utilisateur :

- **Zones principales :** Genève, Nyon et Rolle.
- **Périmètre :** environ 7 km autour de chacune de ces villes. Indiquer la distance ou la commune lorsque celle-ci est vérifiable.
- **Budget maximal :** 3 200 CHF par mois au total, de préférence charges comprises. Si le loyer et les charges sont séparés, calculer le total uniquement avec les montants explicitement indiqués. Si les charges sont inconnues, le signaler et ne pas considérer l'annonce comme pleinement validée.
- **Luminosité :** appartement très lumineux. Le critère est confirmé uniquement par une mention de l'annonce, des photos clairement exploitables ou une caractéristique explicite telle que « lumineux », « plein sud », « traversant » ou « grandes baies vitrées ». Sinon, indiquer `à vérifier`.
- **Balcon :** au moins un balcon obligatoire. Une terrasse, une loggia ou un jardin ne remplace pas automatiquement un balcon ; préciser le type d'extérieur indiqué.
- **Préférence géographique :** Les Eaux-Vives à Genève.
- **Commodités :** proximité souhaitée des commerces, transports publics, écoles et services. Ne jamais inventer une distance.

Les critères non fournis — pièces, surface, date d'entrée, meublé, parking, ascenseur, animaux, durée et composition du ménage — doivent être demandés ou marqués `non spécifiés`.

## Limite stricte de résultats

- Retourner **10 annonces exactement si 10 annonces valides sont disponibles**.
- Retourner moins de 10 annonces s'il n'y a pas suffisamment d'annonces qui respectent les critères et dont le lien est vérifié.
- Ne jamais compléter artificiellement la liste avec une annonce hors critères, un doublon, une annonce expirée ou un lien douteux.
- Dédupliquer les annonces identiques publiées sur plusieurs portails et conserver le lien direct le plus fiable.
- Classer les résultats par pertinence décroissante.

## Vérification obligatoire des liens

Une annonce ne peut apparaître dans les 10 résultats que si son URL est vérifiée immédiatement avant la réponse :

1. Ouvrir l'URL exacte de l'annonce, et non seulement un extrait du moteur de recherche ou une page générale.
2. Vérifier que la page répond normalement, sans erreur HTTP 404, 410 ou 5xx, et qu'elle ne redirige pas vers une page d'erreur, une page supprimée ou une recherche vide.
3. Suivre les redirections normales et afficher l'URL finale si elle est différente.
4. Confirmer que la page correspond bien à une annonce précise et que le titre, le logement ou le prix sont identifiables.
5. Vérifier que l'annonce n'est pas manifestement expirée ou retirée. Si son statut est incertain, la placer hors du top 10 avec la mention `lien ou disponibilité non vérifié`.
6. Si le contrôle est impossible à cause d'une connexion, d'un captcha, d'une restriction régionale ou d'un blocage, ne pas présenter le lien comme fonctionnel.
7. Ne jamais fabriquer, deviner, raccourcir ou reconstruire un lien d'annonce à partir d'un titre.

Un lien de recherche ou une page de résultats ne compte pas comme lien direct fonctionnel d'annonce. Les liens de recherche peuvent être fournis séparément comme points de départ, mais ne doivent pas remplacer les liens directs du tableau.

## Sortie obligatoire

Commencer par les liens de recherche utilisés, puis présenter au maximum 10 annonces directes validées.

```markdown
## Liens de recherche utilisés

### Genève — priorité Les Eaux-Vives
- Recherche web : [ouvrir la recherche](URL vérifiée)
- Portails consultés : [portail](URL vérifiée si possible)

### Nyon — rayon ~7 km
- Recherche web : [ouvrir la recherche](URL vérifiée)
- Portails consultés : [portail](URL vérifiée si possible)

### Rolle — rayon ~7 km
- Recherche web : [ouvrir la recherche](URL vérifiée)
- Portails consultés : [portail](URL vérifiée si possible)

## Top 10 des annonces

| Rang | Zone | Annonce | Loyer total | Balcon | Luminosité | Commodités | Lien direct fonctionnel | Vérifié le |
|---:|---|---|---:|---|---|---|---|---|
```

Pour chaque annonce, ajouter après le tableau ou dans une colonne dédiée : deux ou trois raisons du classement et les éléments à vérifier lors de la visite. Indiquer clairement `moins de 10 annonces valides trouvées` si nécessaire.

## Méthode de recherche

1. Construire une recherche séparée pour Genève/Les Eaux-Vives, Nyon et Rolle.
2. Rechercher sur plusieurs sources publiques autorisées ; ne pas contourner les captchas, authentifications, limitations ou protections anti-robots.
3. Filtrer les annonces dépassant 3 200 CHF de coût mensuel annoncé.
4. Écarter les annonces sans balcon explicitement mentionné, sauf si l'utilisateur demande une liste de pistes à vérifier.
5. Écarter les annonces dont la luminosité est incompatible ou impossible à évaluer si suffisamment de résultats confirmés existent.
6. Vérifier chaque URL candidate selon la procédure ci-dessus avant le classement final.
7. Dédupliquer les résultats, classer et conserver uniquement les 10 premiers.
8. Pour chaque résultat, conserver : URL finale, source, date et heure de vérification, loyer net, charges, total, commune/quartier, distance au centre si disponible, surface, pièces, disponibilité, balcon, indices de luminosité, commodités et informations manquantes.

## Classement

Après les filtres obligatoires, utiliser par défaut :

- 30 % : coût mensuel et respect du budget ;
- 25 % : emplacement, avec bonus pour Les Eaux-Vives ;
- 20 % : indices de luminosité ;
- 15 % : commodités et transports ;
- 10 % : qualité et complétude de l'annonce.

Une information inconnue ne doit jamais être traitée comme positive. En cas d'égalité, privilégier le lien fonctionnel le plus stable, l'annonce la plus récente et les informations les plus complètes.

## Liens de recherche

Générer des URLs correctement encodées, par exemple :

```text
https://www.google.com/search?q=appartement+balcon+lumineux+Genève+Les+Eaux-Vives+CHF+3200
```

Vérifier également les liens de recherche avant de les afficher. Un lien de recherche ne garantit pas que tous ses résultats respectent les critères et ne remplace jamais la validation des liens directs.

## Sécurité et données personnelles

- Ne pas inclure de données personnelles dans les URL de recherche.
- Ne pas demander ni exposer de numéro AVS, coordonnées bancaires ou numéro complet de pièce d'identité.
- Ne pas envoyer automatiquement une candidature ou un dossier ; demander une confirmation explicite.
- Signaler les demandes de paiement avant visite et les demandes de documents sensibles sur un canal non vérifié.

## Questions à poser si elles sont inconnues

- Combien de pièces et quelle surface minimale ?
- Le plafond de 3 200 CHF inclut-il impérativement les charges, le parking et les frais accessoires ?
- Quelle date d'entrée et quelle durée de bail ?
- Meublé ou non meublé ?
- Animaux, parking, ascenseur et étage sont-ils importants ?
- Faut-il privilégier Genève même si l'offre est plus chère, ou accepter Nyon/Rolle en priorité ?
