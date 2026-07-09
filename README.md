# Veille OSINT Chine / Défense — kit de démarrage

Ce kit contient tout le nécessaire pour mettre en place la veille
automatisée avec Claude Code Routines, telle que décrite dans l'échange
précédent.

## Contenu

- `CLAUDE.md` — instructions permanentes (méthodologie RENS MIL, format du
  bulletin, règles de mise à jour des documents). À placer à la racine du
  dépôt.
- `sources.md` — liste des sources OSINT prioritaires. À placer à la racine.
- `daily_routine_prompt.md` — prompt à coller dans la routine quotidienne.
- `weekly_routine_prompt.md` — prompt à coller dans la routine hebdomadaire.

## Mise en place, étape par étape

### 1. Créer le dépôt GitHub
Créez un dépôt (public ou privé — privé recommandé vu la nature du sujet),
par exemple `veille-chine-defense`, avec cette arborescence :

```
veille-chine-defense/
├── CLAUDE.md
├── sources.md
├── documents/
│   ├── Capacites_Militaires_Chinoises_RPC.xlsx
│   ├── Analyse_Capacites_Militaires_Chinoises.docx
│   └── Synthese_Capacites_Militaires_Chinoises.pptx
└── bulletins/
    └── _a_traiter.md   (fichier vide au départ)
```

Copiez `CLAUDE.md` et `sources.md` de ce kit à la racine du dépôt, et vos
trois documents déjà produits dans `documents/`.

### 2. Connecter le dépôt à Claude Code
Rendez-vous sur `claude.ai/code/routines`, connectez votre compte GitHub si
ce n'est pas déjà fait, et autorisez l'accès au dépôt `veille-chine-defense`.

### 3. Configurer le connecteur d'envoi d'e-mail
Le connecteur Gmail natif de Claude ne permet que la création de brouillons,
pas l'envoi automatique. Deux options :
- **Envoi automatique complet** : ajoutez un connecteur MCP tiers avec droit
  d'envoi réel (ex. via un service comme Composio, connecté à votre compte
  Gmail avec le scope d'envoi, ou un service dédié type Resend/SendGrid) et
  sélectionnez-le comme connecteur de la routine.
- **Envoi semi-manuel** : gardez le connecteur Gmail natif — la routine
  créera un brouillon quotidien, que vous envoyez d'un clic le matin.

### 4. Créer la routine quotidienne
Sur `claude.ai/code/routines` → New Routine :
- Nom : `Bulletin OSINT Chine — quotidien`
- Dépôt : `veille-chine-defense`
- Déclencheur : planifié, quotidien, heure de votre choix
- Connecteurs : recherche web + connecteur e-mail choisi à l'étape 3
- Prompt : collez le contenu de `daily_routine_prompt.md`

### 5. Créer la routine hebdomadaire
Même procédure :
- Nom : `Mise à jour documents — hebdomadaire`
- Dépôt : `veille-chine-defense`
- Déclencheur : planifié, hebdomadaire (ex. lundi 7h)
- Connecteurs : recherche web (les documents sont déjà dans le dépôt, pas
  besoin du connecteur e-mail ici sauf si vous voulez une notification)
- Prompt : collez le contenu de `weekly_routine_prompt.md`

### 6. Tester avant d'automatiser
Lancez chaque routine manuellement une première fois (option disponible
dans l'interface) avant de la laisser tourner seule. Vérifiez :
- que le bulletin respecte le format attendu et ne contient pas
  d'information non sourcée
- que l'e-mail arrive correctement formaté (les clients mail suppriment
  souvent le CSS avancé — un Markdown simple passe mieux qu'un HTML élaboré)
- que la première pull request hebdomadaire est cohérente avant de fusionner

### 7. Ajuster dans le temps
Les routines étant en aperçu de recherche, comportement et fiabilité
peuvent varier. Prévoyez une relecture des premiers bulletins pendant 1 à 2
semaines pour affiner `CLAUDE.md` et `sources.md` si le ton, le niveau de
détail ou les sources retenues ne correspondent pas à vos attentes.

## Rappel des limites
- Les routines sont en aperçu de recherche (comportement/disponibilité non
  garantis à long terme).
- Chaque exécution clone le dépôt à froid : aucune mémoire ne persiste
  entre deux runs en dehors de ce qui est écrit dans le dépôt lui-même.
- Nécessite un abonnement Claude Pro ou supérieur, et Claude Code configuré
  sur ce dépôt.
