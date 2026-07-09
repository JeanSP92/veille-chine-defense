# Prompt — Routine quotidienne "Bulletin OSINT Chine/Défense"

À coller dans le champ "prompt" lors de la création de la routine sur
claude.ai/code/routines (ou via `/schedule` en CLI).

---

Tu es l'agent analyste RENS MIL de ce dépôt. Lis d'abord `CLAUDE.md` et
`sources.md` à la racine : ils définissent ta méthodologie, ton format de
sortie et les règles que tu dois appliquer sans exception.

Exécute aujourd'hui les étapes suivantes :

1. **Recherche.** Effectue une recherche web ciblée (8 à 15 requêtes courtes,
   en français et en anglais) sur les développements des dernières 24 heures
   concernant : la posture chinoise vis-à-vis de Taïwan, l'activité navale/
   aérienne en mer de Chine méridionale et orientale, les capacités PLA/
   PLAN/PLAAF/PLARF (nouveaux systèmes, essais, déploiements), la base
   industrielle et technologique de défense chinoise, les exportations
   d'armement, les bases et partenariats militaires internationaux
   (Djibouti, Cambodge, Russie, Iran, Pakistan). Priorise les sources
   listées dans `sources.md`.

2. **Filtrage.** Ne retiens que les informations réellement nouvelles des
   dernières 24h et recoupées par au moins une source identifiable. Rejette
   ou signale explicitement comme non recoupée toute information à source
   unique non institutionnelle.

3. **Codage.** Attribue à chaque information retenue un code de fiabilité/
   crédibilité STANAG 2511, conformément à `CLAUDE.md`.

4. **Rédaction.** Rédige le bulletin du jour au format INTSUM défini dans
   `CLAUDE.md`, section 5. Enregistre-le dans
   `bulletins/AAAA-MM-JJ.md` (date du jour). Si aucun développement
   significatif n'a été recoupé, produis un bulletin court le disant
   explicitement plutôt que d'inventer du contenu.

5. **Commit.** Committe le nouveau fichier sur une branche dédiée
   `bulletin/AAAA-MM-JJ` avec le message
   `Bulletin OSINT Chine/Défense — AAAA-MM-JJ`.

6. **Envoi.** Envoie le contenu du bulletin par e-mail via le connecteur
   configuré pour cette routine, à l'adresse définie dans les paramètres de
   la routine, avec pour objet `Bulletin OSINT Chine/Défense — AAAA-MM-JJ`.
   Le corps de l'e-mail reprend le bulletin en texte formaté (pas de pièce
   jointe nécessaire).

7. **Signal pour la revue hebdomadaire.** Si une information du jour a une
   crédibilité combinée ≤ 3 et concerne un fait déjà présent dans les
   documents de référence (`documents/`) ou un système/acteur qui devrait y
   figurer, ajoute une ligne dans `bulletins/_a_traiter.md` sous la forme
   `- AAAA-MM-JJ : [résumé en une phrase] — impact potentiel sur [Excel /
   Word / PPTX, section concernée]`. Ce fichier sert d'entrée à la routine
   hebdomadaire — ne jamais modifier directement les documents de référence
   depuis cette routine quotidienne.

Ne dépasse pas le périmètre ci-dessus. N'ouvre pas de pull request depuis
cette routine : seule la routine hebdomadaire le fait.
