# Design System Tiny Houses — Fondations et composants d'interface

Version 10.5 — 14 septembre 2026

## Périmètre

Ce document fixe les fondations du Design System du site Tiny Houses. Il ne modifie pas l'identité visuelle : la palette, le logo et la famille typographique restent ceux du site de référence.

L'objectif est de disposer d'une source de vérité stable pour l'ensemble de l'interface. La version 2 fixe la hiérarchie typographique et la grille des icônes fonctionnelles. La version 3 standardise les boutons et la priorité des actions. La version 4 harmonise les formulaires, filtres et retours de saisie. La version 5 rationalise les cartes, les lignes de contenu et les états vides. La version 6 unifie les modales et les panneaux superposés. La version 7 fixe le layout, les en-têtes de page et la navigation responsive. La version 8 standardise les retours utilisateur, les confirmations et les états de chargement. La version 9 clôt la rationalisation par un audit transversal d'accessibilité, de responsive et de cohérence CSS. La version 10 ajoute le format application installable sur iPhone sans créer une interface ou une base de données distincte.

## Règles obligatoires

1. Toute nouvelle couleur d'interface doit utiliser un token `--color-*`.
2. Tout nouvel espacement structurant doit utiliser l'échelle `--space-*`.
3. Tout nouveau rayon doit utiliser un token `--radius-*`.
4. Toute nouvelle ombre doit utiliser un token `--shadow-*`.
5. Les valeurs directes sont réservées aux illustrations, aux tailles intrinsèques d'éléments et aux états métier qui seront tokenisés dans un lot ultérieur.
6. Les alias historiques (`--ink`, `--forest`, `--sage`, etc.) restent disponibles pendant la migration, mais ne doivent plus être utilisés dans du nouveau CSS.
7. Les `!important` existants ne doivent jamais être supprimés en masse. Ils seront retirés composant par composant, après vérification du rendu et des comportements.
8. Une migration ne doit pas modifier simultanément la structure HTML, la logique JavaScript et l'apparence d'un composant sauf nécessité fonctionnelle démontrée.
9. La famille `Inter, "Segoe UI", Arial, sans-serif` reste l'unique pile typographique du produit.
10. Tout nouveau texte doit reprendre un rôle typographique existant ; aucune taille isolée ne doit être ajoutée.
11. Toute nouvelle icône fonctionnelle doit utiliser la grille 16/20/24/32 px, un dessin linéaire cohérent et `currentColor`.
12. Une icône décorative doit porter `aria-hidden="true"`. Une icône seule dans un bouton exige un nom accessible sur le bouton.
13. Une zone d'action ne contient qu'une seule action principale. Les autres actions sont secondaires, discrètes ou destructives.
14. Une suppression, un refus ou une suspension ne doit jamais reprendre le style de l'action principale.
15. Tout nouveau bouton doit fournir les états normal, survol, focus clavier, actif, désactivé et, si nécessaire, chargement.
16. Un champ suit toujours l'ordre libellé, contrôle, aide facultative, puis message d'état.
17. Le placeholder illustre le format attendu mais ne remplace jamais le libellé.
18. Un message dynamique doit être annoncé avec `aria-live="polite"` et relié aux champs concernés avec `aria-describedby`.
19. Les filtres utilisent les mêmes dimensions et états que les autres contrôles.
20. Une carte informative reste visuellement stable au survol ; seule une carte entièrement cliquable peut gagner une légère élévation.
21. Une liste utilise un rythme de ligne, un séparateur et un alignement constants dans un même contexte.
22. Toute collection vide affiche l'état vide commun et conserve un message explicite.
23. Toute modale utilise l'overlay `.modal-shell` et un dialogue nommé avec `role="dialog"`, `aria-modal="true"` et `aria-labelledby`.
24. Une modale se ferme avec son bouton de fermeture, un clic sur l'arrière-plan lorsque l'action est réversible, et la touche Échap.
25. Le focus clavier reste dans la modale ouverte et revient au déclencheur après fermeture.
26. Tout panneau contextuel reste dans les marges de l'écran et restitue le focus à son déclencheur lorsqu'il est fermé avec Échap.
27. Le logo, le contenu principal et les actions du compte utilisent les mêmes limites horizontales.
28. Chaque page fonctionnelle utilise l'en-tête `.page-header` avec un titre unique, une introduction facultative et au maximum une action principale.
29. La navigation mobile reste sur une seule ligne scrollable et ne provoque jamais de débordement horizontal de la page.
30. L'entrée de navigation active porte `aria-current="page"` et reste visible lors d'un changement de page.
31. Un résultat global utilise une notification non bloquante ; une erreur de saisie reste placée près du champ concerné.
32. Toute notification indique explicitement son niveau : succès, erreur, avertissement ou information.
33. Toute action destructive importante utilise la confirmation commune et décrit précisément l'objet concerné.
34. Un bouton déclenchant une opération asynchrone devient indisponible, affiche un chargement et porte `aria-busy="true"` jusqu'à la fin de l'opération.
35. Une notification temporaire peut être fermée, se met en pause au survol ou au focus et reste annoncée aux technologies d'assistance.
36. Tout texte courant et tout placeholder conservent un contraste minimal de 4,5:1 sur leur surface canonique.
37. Tout contrôle, y compris lorsqu'il est généré en JavaScript, possède un nom accessible indépendant de son placeholder.
38. Une interaction disponible à la souris reste disponible au clavier avec un focus visible, notamment dans le calendrier.
39. Un groupe d'onglets utilise les rôles `tablist`, `tab` et `tabpanel`, expose l'onglet sélectionné et accepte les flèches, Début et Fin.
40. Aucun parcours normal ne dépend d'une boîte de dialogue JavaScript native ; les retours et solutions de repli réutilisent les composants du Design System.
41. L’application installée et le site web partagent strictement la même interface, la même authentification et les mêmes données Firebase.
42. Toute publication conserve `manifest.webmanifest`, `service-worker.js`, `apple-touch-icon.png` et le dossier `icons` à côté de `index.html`.
43. Le service worker ne met jamais en cache les requêtes Firebase, les données privées ni les opérations d’écriture.
44. Les écrans iPhone respectent les zones sûres du système avec les variables `env(safe-area-inset-*)`.
45. Une fonctionnalité nécessitant le réseau reste explicitement présentée comme indisponible hors connexion ; l’application ne simule jamais une synchronisation réussie.

## Palette canonique

| Token | Valeur | Usage |
|---|---:|---|
| `--color-text` | `#203a31` | Texte principal |
| `--color-text-strong` | `#18352d` | Titres et emphase |
| `--color-text-muted` | `#637169` | Texte secondaire, contraste 4,55:1 minimum sur le fond de page |
| `--color-background` | `#f5f1e8` | Fond général |
| `--color-page-start` | `#f8f5ee` | Début du dégradé de page |
| `--color-surface` | `#fffdf9` | Surface standard |
| `--color-surface-elevated` | `#fffdf8` | Menus et surfaces élevées |
| `--color-surface-soft` | `#faf7f0` | Surface secondaire douce |
| `--color-primary` | `#23483c` | Action principale et navigation |
| `--color-primary-hover` | `#31594b` | Survol de l'action principale |
| `--color-sage` | `#879d76` | Accent végétal |
| `--color-sage-soft` | `#dfe6d6` | Fond végétal doux |
| `--color-sage-subtle` | `#eef2e9` | Fond végétal très léger |
| `--color-sand` | `#e8d8ba` | Accent sable |
| `--color-accent` | `#bd6748` | Accent terracotta |
| `--color-border` | `#ded9cd` | Bordure standard |
| `--color-success` | `#2f6755` | Succès |
| `--color-danger` | `#a75f50` | Erreur et suppression |

Les variantes de surface, bordure, navigation et overlay présentes dans le bloc `:root` sont des tokens techniques destinés à préserver exactement le rendu actuel.

Le placeholder utilise `--color-field-placeholder: #6c7973`, soit un contraste de 4,5:1 sur `--color-surface-input`. Les textes désactivés restent volontairement distincts et ne doivent jamais porter une information indispensable seuls.

## Espacements

| Token | Valeur |
|---|---:|
| `--space-1` | `4px` |
| `--space-2` | `8px` |
| `--space-3` | `12px` |
| `--space-4` | `16px` |
| `--space-5` | `20px` |
| `--space-6` | `24px` |
| `--space-7` | `32px` |
| `--space-8` | `40px` |
| `--space-9` | `64px` |

`--page-gutter` gère les marges horizontales fluides de la page. `--container-max` fixe la largeur maximale commune à `1380px`.

## Rayons

| Token | Valeur | Usage |
|---|---:|---|
| `--radius-sm` | `8px` | Petit contrôle |
| `--radius-control` | `9px` | Bouton et champ |
| `--radius-md` | `12px` | Menu et surface intermédiaire |
| `--radius-card` | `18px` | Carte |
| `--radius-dialog` | `20px` | Grande fenêtre |
| `--radius-pill` | `999px` | Pastille et badge |

## Ombres

| Token | Usage |
|---|---|
| `--shadow-card` | Carte standard |
| `--shadow-header` | En-tête fixe |
| `--shadow-popover` | Menu déroulant et panneau flottant |
| `--shadow-dialog` | Fenêtre modale |

## Hiérarchie typographique

La hiérarchie conserve la police et la personnalité existantes. Elle limite les variations aux rôles ci-dessous.

| Rôle | Token | Valeur | Usage |
|---|---|---:|---|
| Légende | `--font-size-caption` | `12px` | Étiquette courte, statut, date secondaire |
| Métadonnée | `--font-size-meta` | `13px` | Auteur, aide, description compacte |
| Libellé | `--font-size-label` | `14px` | Navigation, bouton, champ, titre de ligne |
| Texte courant | `--font-size-body` | `16px` | Paragraphes et contenus principaux |
| Texte introductif | `--font-size-body-lg` | `17px` | Introduction ou texte éditorial important |
| Titre de carte | `--font-size-card-title` | `18px` | Carte, bloc fonctionnel, mois du calendrier |
| Titre de section | `--font-size-section-title` | `22px` | Groupe important, fenêtre modale |
| Titre de page | `--font-size-page-title` | `28–32px` | Titre principal d'une page |
| Titre d'accueil | `--font-size-display` | `40–58px` | Nom du projet dans le hero uniquement |
| Sous-titre d'accueil | `--font-size-display-subtitle` | `22–29px` | Signature du hero uniquement |

### Graisses et interlignages

| Token | Rôle |
|---|---|
| `--font-weight-regular` | Texte courant |
| `--font-weight-medium` | Navigation et commandes discrètes |
| `--font-weight-bold` | Titres et emphase |
| `--font-weight-extra-bold` | Titres de page et petits libellés structurants |
| `--line-height-tight` | Titre de page |
| `--line-height-heading` | Titre de section ou carte |
| `--line-height-body` | Texte fonctionnel |
| `--line-height-relaxed` | Texte éditorial et introduction |

Règles d'usage :

- le texte courant est fixé à 16 px et reste compatible avec l'agrandissement du navigateur ;
- les textes utiles à une action ne descendent jamais sous 14 px ;
- 12 et 13 px sont réservés aux métadonnées non essentielles à la décision ;
- les paragraphes d'introduction sont limités à `--text-measure` (`68ch`) pour rester lisibles ;
- les capitales espacées sont réservées aux `eyebrow`, catégories et statuts courts ;
- le logotype conserve ses proportions, son espacement et son traitement typographique propres.

## Icônes

### Grille canonique

| Token | Taille | Usage |
|---|---:|---|
| `--icon-size-sm` | `16px` | Sous-menu, chevron, contrôle compact |
| `--icon-size-md` | `20px` | Navigation principale et indicateur standard |
| `--icon-size-lg` | `24px` | Action mise en avant |
| `--icon-size-xl` | `32px` | Illustration fonctionnelle exceptionnelle |

Les icônes fonctionnelles utilisent la classe `.ui-icon`, un `viewBox` de `24 × 24`, `currentColor`, des extrémités arrondies et le trait `--icon-stroke` (`1.75`). Elles héritent ainsi automatiquement de la couleur normale, du survol et de l'état actif.

### Accessibilité et interaction

- la zone interactive minimale est `--control-target-min` (`44px`) pour la navigation, la cloche, le compte et les boutons constitués d'une icône seule ;
- une icône accompagnée d'un texte est décorative et reçoit `aria-hidden="true"` ;
- un bouton sans texte visible reçoit un `aria-label` explicite, par exemple « Mois précédent » ;
- aucune information ne doit être transmise uniquement par une icône ou par une couleur ;
- entre 901 et 1 180 px, les icônes principales de navigation peuvent être masquées pour préserver les libellés et les marges ;
- les pictogrammes éditoriaux des valeurs, axes du projet et ressources restent autorisés, mais ne sont jamais utilisés comme unique libellé d'une action.

## Boutons et priorité des actions

### Rôles canoniques

| Rôle | Classe | Usage | Exemples |
|---|---|---|---|
| Principal | `.btn` | Créer, enregistrer, publier ou poursuivre le parcours | Enregistrer, Publier, Ajouter, Rejoindre |
| Secondaire | `.btn.secondary` | Annuler ou effectuer une action auxiliaire | Annuler, Modifier, Copier le lien |
| Discret | `.btn.ghost` ou composant textuel documenté | Action contextuelle qui ne doit pas concurrencer le CTA | Réinitialiser, Voir l'historique |
| Destructif | `.btn.danger` | Supprimer, refuser ou suspendre | Supprimer une note, Refuser un compte |
| Icône seule | `.btn.btn-icon` | Navigation ou action représentée par une icône nommée | Mois précédent/suivant |

Règles de décision :

- une modale possède au maximum un bouton principal, placé après les actions secondaires dans l'ordre de lecture ;
- « Annuler » et « Fermer » sont toujours secondaires ou neutres ;
- les commandes « Modifier », « Copier » et « Voir le détail » sont secondaires ;
- les liens d'ouverture ou de poursuite peuvent être principaux lorsqu'ils constituent l'objectif de la carte ;
- les suppressions persistantes utilisent toujours `.danger` et restent séparées du bouton de validation ;
- les boutons textuels ne doivent pas imiter un lien souligné en permanence : leur zone d'action reste visible au focus et au survol.

### Dimensions et tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--control-height-sm` | `36px` | Commande exceptionnellement compacte |
| `--control-height-md` | `44px` | Hauteur standard et cible tactile minimale |
| `--control-height-lg` | `48px` | CTA renforcé |
| `--control-padding-inline` | `16px` | Marge interne horizontale standard |
| `--control-gap` | `8px` | Espace entre icône et libellé |
| `--control-transition` | `160ms` | Transition commune des états |
| `--shadow-control` | ombre légère | Survol d'une action principale |
| `--shadow-focus` | anneau de 3 px | Focus clavier commun |

Les couleurs des variantes et des états sont définies par les tokens `--color-primary-*`, `--color-secondary-*`, `--color-danger-*` et `--color-disabled-*`. Aucune nouvelle couleur directe ne doit être ajoutée dans un bouton.

### États obligatoires

- **survol** : changement mesuré de surface ; seul le bouton principal peut gagner une légère élévation ;
- **focus clavier** : anneau commun `--shadow-focus`, visible sans dépendre de la couleur du fond ;
- **actif** : retour à la position initiale et surface légèrement renforcée ;
- **désactivé** : contraste atténué, curseur bloqué et aucune élévation ;
- **chargement** : `aria-busy="true"` ou `.is-loading`, curseur d'attente et indicateur animé ;
- **mouvement réduit** : suppression des transitions lorsque le système demande `prefers-reduced-motion`.

### Composants spécialisés

Les filtres de ressources, réactions et réponses de participation conservent leur forme de pastille, mais reprennent désormais les mêmes tailles, bordures, transitions et focus. Les actions de menu, onglets de compte et commandes de ligne utilisent la cible minimale de 44 px.

## Formulaires et filtres

### Anatomie canonique

Chaque champ suit le même ordre visuel et sémantique :

1. libellé explicite ;
2. contrôle de saisie ;
3. aide facultative ;
4. message d'erreur ou de succès.

Les astérisques restent réservés aux champs obligatoires. Les exemples et formats attendus peuvent apparaître dans le placeholder, mais l'information indispensable reste dans le libellé ou l'aide.

### Tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--field-height` | `44px` | Hauteur standard des champs et listes |
| `--field-padding-inline` | `12px` | Marge interne horizontale |
| `--field-padding-block` | `10px` | Marge interne verticale |
| `--field-gap` | `8px` | Espace entre libellé, contrôle et aide |
| `--form-row-gap` | `16px` | Espace vertical entre deux champs |
| `--textarea-min-height` | `112px` | Hauteur minimale d'une zone de texte |
| `--color-field-placeholder` | `#7d8983` | Texte d'exemple dans un champ |
| `--color-success-surface` | `#eef5f1` | Fond d'une confirmation |
| `--color-success-border` | `#bed2c9` | Bordure d'une confirmation |

Les champs réutilisent `--color-border-input`, `--color-surface-input`, `--color-focus`, `--shadow-focus` et les couleurs désactivées déjà définies dans les lots précédents.

### États obligatoires

- **normal** : bordure neutre, fond clair et texte principal ;
- **survol** : bordure sauge, sans mouvement ni ombre ;
- **focus clavier** : bordure renforcée et anneau `--shadow-focus` ;
- **erreur** : `aria-invalid="true"` ou `.is-invalid`, bordure terracotta et anneau discret ;
- **désactivé / lecture seule** : surface grisée, texte atténué et curseur bloqué ;
- **succès** : message vert sur une surface douce, jamais par la couleur seule.

Les cases à cocher et boutons radio utilisent `--color-primary` et conservent un focus clavier visible. Les sélecteurs utilisent un chevron SVG issu de la grille d'icônes du lot 2.

### Filtres

- un groupe de filtres possède un nom accessible ;
- les listes de filtres ont la même hauteur de 44 px que les champs ;
- le filtre actif est perceptible autrement que par la couleur avec `aria-pressed` lorsqu'il s'agit de boutons ;
- la commande « Réinitialiser » reste une action discrète ;
- sur mobile, les filtres passent sur une colonne et occupent toute la largeur disponible ;
- une modification de filtre ne change jamais la structure des données ni la logique Firebase.

### Messages et accessibilité

Les messages utilisent `.error`, `.password-success` ou la classe utilitaire `.form-message`. Un message vide est masqué ; lorsqu'il reçoit du texte, il est annoncé avec `aria-live="polite"`. Les champs concernés le référencent avec `aria-describedby`.

Le texte saisi reste à 16 px afin de préserver la lisibilité et d'éviter le zoom automatique sur mobile. Les contrôles spécialisés — statut rapide d'une action, interrupteurs, fichiers et choix de sondage — conservent leur comportement existant tout en reprenant les couleurs de focus communes.

## Cartes et listes de contenu

### Familles de surfaces

| Famille | Composants | Comportement |
|---|---|---|
| Carte informative | accueil, axes, ressources, sondages, notes | surface stable, aucune translation au survol |
| Carte interactive | fiche d'un membre | bordure renforcée et légère élévation au survol |
| Conteneur de liste | actions, budget, prochains événements | regroupe des lignes sans transformer chacune en carte |
| Ligne autonome | historique | bordure et surface légères, sans ombre ni faux affordance |
| Ligne imbriquée | commentaires, participants, notifications | densité compacte, séparateurs et focus cohérents |

Une surface entièrement cliquable doit être un vrai contrôle clavier. Une carte contenant seulement des boutons internes ne réagit pas comme si toute sa surface était cliquable.

### Tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--card-padding-sm` | `16px` | Carte compacte ou mobile |
| `--card-padding-md` | `20px` | Carte de contenu standard |
| `--card-padding-lg` | `24px` | Carte importante ou aérée |
| `--card-grid-gap` | `16px` | Espace entre cartes d'une grille |
| `--card-content-gap` | `16px` | Espace entre zones internes |
| `--list-row-padding-block` | `16px` | Marge verticale d'une ligne |
| `--list-row-padding-inline` | `16px` | Marge horizontale d'une ligne |
| `--list-row-gap` | `12px` | Espace entre les colonnes d'une ligne |
| `--list-row-min-height` | `64px` | Hauteur minimale d'une ligne de contenu |
| `--empty-state-min-height` | `120px` | Hauteur minimale d'un état vide |
| `--shadow-card-hover` | ombre renforcée | Survol d'une carte entièrement cliquable |
| `--surface-transition` | `160ms` | Transition des surfaces interactives |

Les cartes réutilisent `--color-surface-card`, `--color-border-card`, `--radius-card` et `--shadow-card` du lot 1. Les textes, icônes, actions et champs qu'elles contiennent suivent les lots 2 à 4.

### Structure d'une carte

L'ordre recommandé est :

1. en-tête avec catégorie, titre et éventuel pictogramme ;
2. contenu principal ;
3. métadonnées ou statut ;
4. zone d'actions séparée par une bordure lorsque nécessaire.

Une carte ne contient qu'un CTA principal, conformément au lot 3. Les titres reprennent le niveau « titre de carte » du lot 2. Les hauteurs ne sont pas figées : le contenu peut grandir et les actions restent alignées en bas des cartes d'une même grille.

### Structure d'une liste

- les lignes d'une même liste partagent les mêmes marges internes ;
- le séparateur disparaît après la dernière ligne ;
- un survol n'est ajouté que si la ligne entière est cliquable ;
- `:focus-within` peut signaler la ligne contenant le contrôle actif ;
- les informations essentielles restent lisibles à 200 % de zoom ;
- sur mobile, les colonnes se réorganisent sans tronquer les actions ni les montants.

### États vides

L'état `.empty-state` occupe toute la largeur de sa grille, utilise une bordure discontinue et un fond doux. Il explique clairement l'absence de contenu sans simuler une erreur. La variante `.compact` est réservée aux listes placées dans une carte existante.

Les états vides dynamiques portent `role="status"`. Ils sont appliqués aux actions filtrées, au budget, aux membres, à l'historique, au calendrier, aux ressources, aux notes, aux sondages et aux notifications.

## Retours utilisateur, confirmations et chargements

Le système distingue les retours locaux, liés à un formulaire précis, des retours globaux confirmant le résultat d'une opération. Il remplace les boîtes de dialogue natives disparates sans modifier les validations ni les opérations Firebase.

### Tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--feedback-width` | `420px` | Largeur maximale d'une notification |
| `--feedback-gap` | `12px` | Espace entre notifications simultanées |
| `--feedback-padding` | `16px` | Marge interne d'un message |
| `--feedback-duration` | `4500ms` | Durée standard avant disparition |
| `--color-warning-surface` | jaune sable très clair | Fond d'avertissement |
| `--color-warning-border` | sable soutenu | Bordure d'avertissement |
| `--color-warning-text` | brun doré | Texte d'avertissement |
| `--color-info-surface` | bleu très clair | Fond d'information |
| `--color-info-border` | bleu grisé | Bordure d'information |
| `--color-info-text` | bleu profond | Texte d'information |

Les états succès et erreur réutilisent les tokens sémantiques définis dans les lots 1 et 4. Les nouvelles teintes d'information et d'avertissement sont dérivées des couleurs sauge, sable, or et bleu de l'identité existante.

### Notifications globales

Le composant `.toast` comporte :

1. un indicateur de niveau ;
2. un titre explicite ;
3. un message textuel ;
4. un bouton de fermeture de 44 px.

Quatre niveaux sont disponibles :

| Niveau | Usage |
|---|---|
| Succès | création, modification ou suppression terminée |
| Erreur | opération impossible ou échec de synchronisation |
| Avertissement | opération réussie partiellement, notamment notification non envoyée |
| Information | état neutre ou instruction temporaire |

La zone de notifications porte `aria-live="polite"`. Une erreur individuelle utilise également `role="alert"`. Quatre messages maximum restent visibles simultanément. Le délai s'interrompt au survol et lorsque le clavier entre dans la notification.

### Retours locaux

Les erreurs de validation restent dans la modale ou le formulaire, près du contrôle concerné. Les messages utilisent toujours `aria-live`, `aria-describedby` et les styles du lot 4.

La bannière `.feedback-banner` est réservée à une information persistante qui structure le parcours, comme l'attente d'approbation d'un compte. Un traitement intermédiaire, tel que la compression d'une image, utilise l'état information et non le style d'erreur.

### Confirmations

La confirmation commune reprend la structure de modale du lot 6. Son titre nomme l'action et son message identifie l'objet concerné : action, ligne de budget, note, événement, ressource, sondage, rôle ou membre.

- Annuler et Échap produisent le même résultat sans modification ;
- le clic sur l'arrière-plan annule la demande ;
- le bouton destructif reprend le style danger du lot 3 ;
- une confirmation non destructive, comme une promotion administrateur, utilise le bouton principal ;
- le focus reste dans la confirmation puis revient au parcours d'origine.

### États de chargement

`setActionLoading` applique le même comportement aux boutons asynchrones :

- libellé temporaire explicite ;
- indicateur circulaire intégré ;
- désactivation contre les doubles soumissions ;
- attribut `aria-busy="true"` ;
- restauration automatique du libellé initial dans le bloc `finally`.

Ce comportement est appliqué aux actions, au profil, aux notes, au calendrier, aux ressources, aux sondages, aux valeurs de charte, au mot de passe et à l'administration.

## Audit transversal et règles de clôture

Le lot 9 vérifie l'ensemble des composants après leur rationalisation. Les corrections restent limitées aux écarts démontrés ; le CSS historique n'est jamais supprimé en masse.

### Accessibilité

- le logo est un bouton natif et conserve son apparence de marque ;
- chaque champ statique ou généré possède un libellé visible ou un nom accessible ;
- les dates et événements du calendrier sont de vrais boutons, nommés avec leur date et utilisables au clavier ;
- la date du jour expose `aria-current="date"` ;
- les panneaux de notifications et du compte sont identifiés comme régions ;
- les onglets Profil et Sécurité exposent leur sélection, leur panneau associé et la navigation par flèches, Début et Fin ;
- les boutons d'affichage du mot de passe exposent leur état avec `aria-pressed` ;
- le mode de contraste forcé conserve des bordures et des focus identifiables.

### Responsive

Le calendrier conserve sept colonnes sans imposer une largeur minimale susceptible de créer un débordement. Les boutons de date occupent la largeur disponible de leur cellule, les événements restent tronqués visuellement mais conservent un nom complet pour les technologies d'assistance, et les règles existantes de tablette et mobile restent prioritaires.

### Nettoyage CSS ciblé

Cinq déclarations strictement identiques ont été supprimées : `box-sizing` universel, largeur du menu de compte, largeur de la ligne complète du formulaire calendrier, règle de paragraphe des titres de valeurs et flexibilité du champ mot de passe. Toutes les autres surcharges historiques sont conservées lorsqu'une suppression nécessiterait une validation visuelle ou risquerait de modifier la cascade.

## Migration réalisée dans la version 9

- amélioration du contraste du texte secondaire et des placeholders sans changer la palette de marque ;
- ajout des noms accessibles manquants aux commentaires, au budget, aux responsables, aux réponses de sondage et à l'icône de ressource ;
- transformation du logo en bouton sémantique sans modification visuelle ;
- navigation clavier complète du calendrier et des onglets du compte ;
- ajout de la sémantique des régions, de la grille calendrier et de la fenêtre de connexion ;
- suppression du dernier `prompt` natif au profit d'une copie de secours et d'un avertissement commun ;
- prise en charge du contraste forcé ;
- suppression de cinq doublons CSS strictement identiques ;
- maintien de tous les identifiants métier, données, permissions et échanges Firebase.

## Migration réalisée dans la version 8

- création d'une zone globale de notifications accessible et responsive ;
- définition des quatre niveaux succès, erreur, avertissement et information ;
- remplacement de toutes les alertes JavaScript natives par des retours non bloquants ;
- remplacement de toutes les confirmations natives par une modale commune ;
- ajout d'une confirmation à la suppression d'une ligne de budget ;
- ajout de confirmations explicites aux suspensions, refus, rôles administrateur et suppressions ;
- ajout d'états de chargement aux principales écritures et suppressions asynchrones ;
- harmonisation des succès pour les actions, le budget, le profil, les notes, le calendrier, les ressources, les sondages, la charte, le mot de passe et l'administration ;
- correction de l'état visuel pendant la compression d'une image ;
- conservation du dialogue natif uniquement comme solution de secours lorsque le navigateur interdit toute copie automatique d'un lien ;
- maintien intégral des formats de données, permissions, règles et chemins Firebase.

## Layout, en-têtes de page et navigation

Le layout du site repose sur un conteneur central unique. La barre supérieure peut occuper toute la largeur de l'écran, mais son logo, sa navigation et ses actions restent alignés avec les limites du contenu principal.

### Tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--container-half` | `690px` | Moitié technique du conteneur de 1380 px |
| `--layout-edge` | marge fluide calculée | Limite commune du logo et des actions du header |
| `--header-min-height` | `68px` | Hauteur minimale de la barre desktop |
| `--header-padding-block` | `12px` | Marge verticale du header |
| `--header-column-gap` | `16–32px` | Espace entre logo, navigation et compte |
| `--content-padding-top` | `32px` | Début du contenu principal |
| `--content-padding-bottom` | `96px` | Marge basse des pages |
| `--page-header-gap` | `24px` | Espace entre le texte et l'action d'un en-tête |
| `--page-header-margin-bottom` | `24px` | Espace après un en-tête de page |
| `--mobile-nav-offset` | `112px` | Position verticale des panneaux sous le header mobile |
| `--mobile-submenu-top` | `112px`, recalculé à l'ouverture | Bord supérieur du sous-menu tactile sous le header |

`--layout-edge` combine `--page-gutter` et `--container-max`. Sur un grand écran, le logo se déplace donc vers la droite et les actions du compte vers la gauche pour suivre exactement les marges du contenu, sans valeur de positionnement arbitraire.

### Barre supérieure

Sur ordinateur, la barre utilise trois zones :

1. logo aligné à gauche du conteneur ;
2. navigation centrée ;
3. notifications et compte alignés à droite du conteneur.

Sous 1080 px, le logo et le compte occupent la première ligne et la navigation la seconde. Sous 720 px, le libellé du compte est masqué mais son avatar et les notifications conservent une cible de 44 px.

La balise structurelle est un `header`. La navigation possède un nom accessible et les menus déroulants sont reliés à leurs déclencheurs avec `aria-controls`.

### En-tête de page

La structure `.page-header` est appliquée à la feuille de route, aux actions, aux membres, au budget, à l'historique, au calendrier, aux sondages, aux ressources, à la charte et aux notes.

Elle contient :

- un bloc texte avec une catégorie facultative, un titre `h1` et une introduction ;
- une seule commande contextuelle facultative : CTA ou filtre principal ;
- une marge basse constante avant le contenu de la page.

Sur mobile, le texte et l'action passent en colonne. Le CTA ou le filtre occupe alors toute la largeur disponible. L'accueil conserve son hero éditorial spécifique, car il ne s'agit pas d'un en-tête fonctionnel standard.

### Navigation responsive et accessibilité

- un lien d'évitement permet d'atteindre directement le contenu principal ;
- l'entrée active porte `aria-current="page"` ;
- la navigation recentre automatiquement l'entrée active lorsqu'elle doit défiler ;
- le changement de page replace le viewport au début du contenu ;
- la navigation mobile défile horizontalement sans élargir la page ;
- les sous-menus et le panneau de notifications restent dans les marges du viewport ;
- la préférence de réduction des animations désactive le défilement doux.

## Migration réalisée dans la version 7

- création d'une limite horizontale commune au contenu, au logo, aux notifications et au compte ;
- déplacement contrôlé du logo vers la droite et des actions vers la gauche sur les grands écrans ;
- remplacement du rôle latéral historique par un véritable en-tête de page ;
- standardisation des dix en-têtes de pages fonctionnelles ;
- harmonisation des espacements verticaux et horizontaux du contenu principal ;
- passage automatique de la navigation sur une seconde ligne aux formats tablette et mobile ;
- maintien des entrées mobiles sur une rangée scrollable sans débordement ;
- ajout du lien d'évitement, de `aria-current`, `aria-controls` et du nom de navigation ;
- recentrage automatique de l'entrée active et retour en haut après navigation ;
- maintien intégral des identifiants, permissions, listeners fonctionnels et échanges Firebase.

## Modales et panneaux superposés

Les couches superposées reprennent les fondations des lots précédents : surface élevée et ombre du lot 1, titre du lot 2, hiérarchie des actions du lot 3, champs du lot 4 et structure de surface du lot 5.

### Inventaire rationalisé

| Famille | Composants | Règle commune |
|---|---|---|
| Dialogue compact | profil d'un membre | largeur maximale de 480 px |
| Dialogue standard | calendrier, sondage, ressource, valeur, note, mot de passe | largeur maximale de 620 à 720 px selon le contenu |
| Dialogue étendu | paramètres du compte, administration | largeur maximale de 900 px |
| Panneau contextuel | notifications, compte, sous-menus | surface élevée ancrée au déclencheur et contenue dans le viewport |

Toutes les fenêtres emploient désormais `.modal-shell`. Les anciens overlays écrits individuellement dans les attributs `style` ne constituent plus des variantes autorisées.

### Tokens

| Token | Valeur | Usage |
|---|---:|---|
| `--overlay-padding` | `24px` | Marge de sécurité autour d'un dialogue |
| `--dialog-width-sm` | `480px` | Dialogue compact |
| `--dialog-width-md` | `680px` | Dialogue standard |
| `--dialog-width-lg` | `900px` | Dialogue étendu |
| `--dialog-max-height` | hauteur écran moins 48 px | Hauteur maximale avec défilement interne |
| `--dialog-header-padding` | `24px` | Marges de l'en-tête |
| `--dialog-body-padding` | `24px` | Marges du contenu |
| `--dialog-footer-gap` | `12px` | Espace entre actions |
| `--popover-width` | `380px` | Largeur du panneau de notifications |
| `--popover-max-height` | `520px` | Hauteur maximale d'un panneau |
| `--popover-offset` | `8px` | Décalage avec le déclencheur |

Les dialogues réutilisent `--radius-dialog`, `--shadow-dialog`, `--color-overlay`, `--color-surface-elevated` et `--color-border-card`. Les panneaux réutilisent `--radius-md` et `--shadow-popover`.

### Anatomie d'une modale

L'ordre obligatoire est :

1. overlay `.modal-shell` ;
2. surface portant le rôle de dialogue et son nom accessible ;
3. en-tête avec titre et bouton de fermeture de 44 px ;
4. contenu principal, formulaire ou détail ;
5. zone d'actions séparée du contenu lorsque nécessaire.

Sur mobile, l'overlay conserve une marge de 12 px, le dialogue ne dépasse pas la hauteur visible et ses boutons d'action occupent toute la largeur. Le contenu défile dans la fenêtre sans déplacer la page arrière.

### Variante complémentaire : dialogue structuré

La variante `.dialog-structured` complète les trois largeurs de dialogue existantes. Elle est réservée aux fenêtres complexes comportant des onglets, plusieurs sections ou un formulaire susceptible de dépasser la hauteur disponible.

Elle utilise quatre classes complémentaires :

- `.dialog-structured` sur la surface du dialogue ;
- `.dialog-structured-body` sur la zone centrale ;
- `.dialog-structured-scroll` sur la zone qui peut défiler ;
- `.dialog-structured-footer` sur la zone d'actions.

Son en-tête et son pied de page restent toujours visibles. Seul le contenu central défile. La modale des paramètres du compte constitue l'implémentation de référence : largeur maximale de 900 px, largeur fluide sur tablette, onglets horizontaux sous 820 px et actions pleine largeur sur petit mobile.

### Comportement et accessibilité

- Échap ferme toujours la couche supérieure ;
- la tabulation boucle entre les contrôles de la modale ouverte ;
- le focus initial vise le premier champ pertinent, sinon le premier contrôle ;
- le focus revient au contrôle ayant ouvert la fenêtre ;
- le clic sur l'arrière-plan ferme les fenêtres réversibles en déclenchant leur gestionnaire existant ;
- l'ouverture d'une modale bloque le défilement de la page arrière ;
- Échap ferme aussi les notifications, le menu du compte et les sous-menus de navigation ;
- tous les panneaux conservent une marge minimale de 12 px avec les bords de l'écran.

## Migration réalisée dans la version 6

- remplacement des overlays individuels par la structure commune `.modal-shell` ;
- définition de trois largeurs cohérentes pour les dialogues compacts, standards et étendus ;
- harmonisation des en-têtes, contenus, séparateurs, boutons de fermeture et zones d'actions ;
- alignement des marges et du défilement sur ordinateur, tablette et mobile ;
- ajout des rôles, noms accessibles et états `aria-hidden` à toutes les fenêtres ;
- fermeture par Échap, confinement du focus et restitution au déclencheur ;
- fermeture cohérente par l'arrière-plan pour les fenêtres qui ne le proposaient pas ;
- rationalisation des panneaux de notifications, de compte et des sous-menus sans débordement hors écran ;
- maintien de tous les identifiants, gestionnaires métier, permissions et échanges Firebase existants.

## Migration réalisée dans la version 5

- création d'une échelle commune de marges, espacements et hauteurs pour les cartes et lignes ;
- harmonisation des cartes de l'accueil, ressources, sondages, notes et membres ;
- suppression de l'effet de survol trompeur sur les cartes informatives des axes du projet ;
- maintien d'un retour de survol et de focus uniquement sur les fiches membres entièrement cliquables ;
- standardisation des lignes d'actions, budget, calendrier et historique ;
- harmonisation des commentaires, participations et notifications ;
- ajout d'un état vide commun aux neuf collections et vues concernées ;
- adaptation des lignes de budget et des cartes de contenu au mobile ;
- remplacement sémantique des conteneurs d'actions, d'événements et de sondages par des articles, sans modification des gestionnaires ;
- maintien intégral des données, permissions, listeners et écritures Firebase.

## Migration réalisée dans la version 4

- unification des hauteurs, marges internes, rayons, bordures et tailles de texte des champs ;
- ajout d'un chevron cohérent aux listes déroulantes ;
- harmonisation des états de survol, focus, erreur, lecture seule et désactivation ;
- unification des libellés et aides des actions, du calendrier, des sondages, des ressources, des valeurs, des notes, du profil et du mot de passe ;
- harmonisation des filtres des actions, ressources, historique et administration ;
- standardisation visuelle et sémantique des messages d'erreur et de succès ;
- ajout de relations `aria-describedby`, de zones `aria-live` et d'un état `aria-pressed` aux filtres de ressources ;
- maintien des identifiants, validations JavaScript, écritures Firestore et parcours fonctionnels existants.

## Migration réalisée dans la version 3

- création de quatre rôles d'action explicites : principal, secondaire, discret et destructif ;
- harmonisation de la hauteur, des marges internes, des graisses et des transitions ;
- ajout d'états cohérents pour le survol, le focus, l'activation, la désactivation et le chargement ;
- différenciation visuelle des suppressions dans le calendrier, les sondages, les ressources, les notes, le profil et l'administration ;
- différenciation des actions administratives « Refuser » et « Suspendre » ;
- standardisation des filtres, réactions, réponses de participation, boutons de ligne et boutons à icône seule ;
- ajout de libellés accessibles aux suppressions d'actions, de budget, de responsables et de réponses de sondage ;
- harmonisation des actions de connexion et de récupération après erreur ;
- maintien intégral des gestionnaires JavaScript et des opérations Firebase existantes.

## Migration réalisée dans la version 2

- ajout de l'échelle typographique complète, de ses graisses, interlignages et espacements de lettres ;
- harmonisation des titres de page, titres de section, cartes, modales, textes courants, libellés et métadonnées ;
- relèvement des textes fonctionnels trop petits afin d'améliorer la lisibilité ;
- remplacement des symboles disparates de la navigation, des notifications, des indicateurs et du calendrier par un langage SVG linéaire cohérent ;
- ajout de noms accessibles aux boutons de navigation mensuelle ;
- masquage sémantique des symboles décoratifs pour les lecteurs d'écran ;
- conservation du logo, de la police, des couleurs et des pictogrammes éditoriaux propres à l'identité Tiny Houses.

## Migration réalisée dans la version 1

- fusion des deux déclarations `:root` en une source de vérité unique ;
- conservation de tous les anciens alias pour garantir la compatibilité ;
- migration du fond général et de la typographie de base ;
- migration du conteneur de page et de ses marges ;
- migration de la carte standard ;
- migration des fondations des boutons et champs ;
- migration de l'en-tête, de la navigation et de son état actif ;
- migration de l'overlay de base, de l'ombre de dialogue et du menu de compte ;
- maintien intégral du HTML fonctionnel, du JavaScript et de Firebase.

## Méthode de maintenance continue

Pour chaque famille de composants :

1. identifier la règle finale réellement appliquée ;
2. rattacher les valeurs aux tokens canoniques ;
3. supprimer uniquement les doublons devenus inutiles ;
4. vérifier ordinateur, tablette et mobile ;
5. contrôler les états normal, survol, focus, désactivé, chargement et erreur ;
6. conserver les alias historiques jusqu'à la fin de tous les lots.

Les neuf lots sont désormais intégrés. Toute évolution ultérieure doit conserver ces règles, limiter les nouvelles surcharges et faire l'objet des mêmes contrôles statiques avant publication.

## Version 10 — Application installable sur iPhone

Tiny Houses est une Progressive Web App installable depuis Safari. Ce format complète le site web : il ne constitue ni une seconde application ni une copie des données. L’icône de l’écran d’accueil ouvre la même version GitHub Pages dans une fenêtre dédiée et Firebase reste l’unique source des données communautaires.

### Fichiers obligatoires

| Fichier | Rôle |
|---|---|
| `index.html` | Interface et enregistrement de l’application |
| `manifest.webmanifest` | Nom, couleurs, lancement plein écran et icônes |
| `service-worker.js` | Mise en cache limitée à la coque publique de l’interface |
| `apple-touch-icon.png` | Icône utilisée par l’écran d’accueil iOS |
| `icons/icon-192.png` | Icône d’application standard |
| `icons/icon-512.png` | Icône haute définition et maskable |

Ces chemins sont relatifs afin de fonctionner sous le sous-dossier GitHub Pages `/lieu-communautaire/`. Tous les fichiers sont publiés ensemble à la racine de ce sous-site.

### Comportement iPhone

- la balise viewport accepte `viewport-fit=cover` ;
- les zones sûres iOS utilisent `--safe-area-top`, `--safe-area-right`, `--safe-area-bottom` et `--safe-area-left` ;
- la couleur d’interface du système reprend `--color-primary` ;
- le nom court affiché sous l’icône est « Tiny Houses » ;
- le menu du compte propose « Installer l’application » tant que le site n’est pas déjà lancé en mode autonome ;
- le guide intégré explique le parcours Safari « Partager » puis « Sur l’écran d’accueil » ;
- sur les navigateurs prenant en charge une invite d’installation native, le même bouton utilise cette invite.

### Icône d’application

L’icône canonique représente trois personnes réunies sous un toit, avec un cœur terracotta au centre. Le fond ivoire occupe toute la surface carrée : aucun arrondi, masque ou coin noir n’est intégré dans le fichier source, car iOS et les autres systèmes appliquent eux-mêmes la forme finale de l’icône.

Le symbole reste dans la zone centrale sûre afin de conserver le toit, les silhouettes et le cœur lorsque le système utilise un masque arrondi. Les trois fichiers 180, 192 et 512 px doivent toujours être dérivés du même master `app-icon-master.png`.

### Cache et données

Le cache contient uniquement l’interface publique, le manifeste et les icônes. Les requêtes externes, Firebase, l’authentification et toutes les écritures restent en accès réseau direct. En cas de coupure, la coque déjà chargée peut s’ouvrir, mais aucune donnée privée n’est présentée comme synchronisée sans connexion.

Chaque nouvelle publication modifiant l’un des fichiers statiques doit incrémenter `CACHE_NAME` dans `service-worker.js` afin que l’ancienne coque soit supprimée lors de l’activation de la nouvelle version.

## Correctif 9.3 — Modale structurée et événements à venir

Le dialogue des paramètres utilise désormais trois zones explicites : en-tête, contenu défilable et pied de page. Sa hauteur est définie à partir de la hauteur réellement disponible afin de réserver systématiquement la place des boutons « Annuler » et « Enregistrer ». Sur un écran peu haut, seuls les onglets et le formulaire défilent.

L'ancienne limite de largeur à 520 px et les styles directement inscrits dans le HTML ont été neutralisés. Le dialogue peut atteindre 900 px sur ordinateur et occupe la largeur disponible sur tablette. Sous 820 px, la navigation Profil/Sécurité devient horizontale pour libérer la largeur du formulaire.

Les boutons de fermeture utilisent désormais un SVG unique dans le HTML ; l'ancien pictogramme généré par CSS est désactivé. Le nom accessible « Fermer » est conservé sur les onze dialogues.

La zone « À venir » utilise désormais une liste espacée de cartes compactes. L’espace vertical entre deux événements est fixé par `--calendar-upcoming-gap` à **14 px**, sur ordinateur comme sur mobile. Chaque événement possède sa propre bordure, son propre rayon et une barre latérale colorée : vert pour une réunion, terracotta pour une action. Les blocs restent informatifs et ne gagnent aucun survol trompeur ; les boutons internes conservent leurs comportements existants.

## Correctif 10.3 — Sous-menus tactiles et dialogues d'authentification

Sur les écrans de 1080 px ou moins, le sous-menu ouvert est temporairement placé au niveau du document, juste sous l'en-tête. Ce portail mobile empêche Safari iOS de le rogner dans la navigation horizontale. Le menu conserve son identifiant, sa relation `aria-controls` et l'état `aria-expanded` de son bouton. Un toucher extérieur, la touche Échap, un changement de page ou un changement de largeur referme le sous-menu et le replace dans son groupe d'origine.

La connexion et l'inscription utilisent deux dialogues indépendants qui reprennent les surfaces, bordures, espacements, champs et boutons du Design System. Le premier contient uniquement l'adresse e-mail, le mot de passe, l'action « Se connecter » et l'accès « Inscrivez-vous ». Ce dernier ouvre le second dialogue sans dépendre des valeurs saisies dans la connexion.

Le dialogue d'inscription demande sa propre adresse e-mail, un mot de passe d'au moins six caractères et une seconde saisie de confirmation. Il ne comporte aucune acceptation de conditions générales, politique de confidentialité ou certification d'âge. Après création, le parcours d'approbation existant reste inchangé : le compte est enregistré avec le statut `pending` jusqu'à validation par un administrateur.

La version 10.4 remplace le titre et l'introduction de connexion par un intitulé unique : « Communauté solidaire des Gens de confiance ». Les champs et les actions restent inchangés.

La version 10.5 fixe ce titre sur deux lignes équilibrées : « Communauté solidaire des » puis « Gens de confiance ». Cette composition est identique sur ordinateur et mobile, interdit tout mot orphelin et utilise une taille fluide sur les plus petits écrans. Un espacement de 20 px sépare le titre du premier champ.

## Validation transversale réalisée

La phase de validation finale a contrôlé le rendu à 1363 px, 768 px et 375 px, le parcours clavier, le lien d'évitement, les zones tactiles, les contrastes canoniques, la structure ARIA, les titres, les dialogues, les onglets, les tokens et la syntaxe JavaScript.

Deux ajustements ciblés ont été appliqués sans modifier l'identité visuelle ni les parcours métier :

- la zone cliquable du logo atteint désormais 44 px sur mobile ;
- les libellés éditoriaux terracotta utilisent une nuance déjà présente dans la palette afin d'atteindre au moins 4,5:1 sur les surfaces claires.
- le bouton du compte utilise désormais une couleur lisible sur l'en-tête clair et une cible de 44 px, tandis que sa version mobile reste limitée à l'avatar.

Résultats : aucun débordement horizontal du document aux trois largeurs contrôlées, navigation mobile volontairement défilable, lien d'évitement fonctionnel, cinq scripts valides, 182 identifiants uniques, 11 pages avec un titre principal, 11 dialogues nommés, une seule racine de tokens et aucune référence ARIA orpheline.

Les parcours authentifiés et les écritures Firebase doivent encore être rejoués sur l'instance déployée avec un compte de test membre et un compte administrateur : l'environnement de prévisualisation n'accède pas aux données de production et ne remplace pas une recette métier connectée.

## Critères de validation

- une seule déclaration `:root` ;
- aucune valeur canonique dupliquée dans un second bloc de tokens ;
- aucun changement de couleur, dimension ou comportement involontaire ;
- chaque niveau typographique correspond à un token documenté ;
- toute icône fonctionnelle nouvelle respecte la grille 16/20/24/32 px ;
- chaque bouton à icône seule possède un nom accessible ;
- chaque zone d'action comporte au maximum un CTA principal ;
- toute action destructive utilise la variante dédiée ;
- les boutons conservent une cible interactive d'au moins 44 px ;
- les champs et listes standard utilisent une hauteur de 44 px ;
- les messages dynamiques sont reliés aux champs et annoncés aux technologies d'assistance ;
- les filtres restent lisibles, réinitialisables et utilisables sur mobile ;
- les cartes informatives ne simulent pas une interaction au survol ;
- les cartes interactives restent entièrement utilisables au clavier ;
- les listes conservent un rythme de ligne constant et un dernier élément sans séparateur ;
- chaque collection vide utilise l'état commun adapté à son contexte ;
- chaque modale possède un rôle de dialogue, un nom accessible et un bouton de fermeture identifiable ;
- Échap ferme la couche supérieure et la tabulation ne quitte pas une modale ouverte ;
- le focus revient au déclencheur après fermeture ;
- aucun dialogue ou panneau contextuel ne sort des marges de l'écran ;
- la page arrière ne défile pas lorsqu'une modale est ouverte ;
- le logo et les actions du compte sont alignés avec les limites du contenu principal ;
- chaque page fonctionnelle utilise l'en-tête standard et ne présente qu'un seul titre principal ;
- la navigation mobile ne provoque aucun débordement horizontal ;
- l'entrée active de navigation porte `aria-current="page"` et reste visible ;
- le lien d'évitement atteint directement le contenu principal ;
- chaque résultat global utilise l'un des quatre niveaux de feedback documentés ;
- aucune alerte ou confirmation JavaScript native ne subsiste ;
- aucun champ statique ou généré ne repose uniquement sur un placeholder comme nom accessible ;
- chaque action du calendrier est utilisable au clavier et expose un libellé complet ;
- les onglets du compte exposent leur état et acceptent les touches directionnelles ;
- les contrastes du texte courant et des placeholders atteignent au moins 4,5:1 sur leurs surfaces canoniques ;
- chaque confirmation destructive nomme l'objet concerné et reste utilisable au clavier ;
- tout bouton asynchrone traité porte `aria-busy="true"` pendant son chargement ;
- les notifications temporaires peuvent être fermées et leur délai se suspend au focus ;
- syntaxe CSS et JavaScript valide ;
- toutes les fonctionnalités Firebase conservées ;
- les nouvelles règles utilisent exclusivement les tokens documentés ;
- le manifeste utilise des chemins relatifs compatibles avec GitHub Pages ;
- les icônes 180, 192 et 512 px sont présentes et lisibles ;
- le service worker ne traite que les requêtes `GET` de la même origine ;
- les requêtes Firebase et toutes les écritures restent hors cache ;
- la séparation entre événements à venir reste exactement de 14 px à toutes les largeurs.
