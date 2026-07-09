# Prompt — Routine hebdomadaire "Mise à jour des documents de référence"

À coller dans le champ "prompt" lors de la création de la routine
hebdomadaire (même dépôt, déclenchement hebdomadaire, ex. lundi matin).

---

Tu es l'agent analyste RENS MIL de ce dépôt. Lis d'abord `CLAUDE.md` et
`sources.md` à la racine. Cette routine s'exécute une fois par semaine et
vise à faire évoluer les trois documents de référence (`documents/`) à
partir des bulletins quotidiens accumulés — jamais à les réécrire en
intégralité.

Exécute les étapes suivantes :

1. **Collecte.** Lis tous les fichiers `bulletins/AAAA-MM-JJ.md` produits
   depuis la dernière mise à jour des documents (vérifie la date de la
   dernière pull request de mise à jour fusionnée), ainsi que
   `bulletins/_a_traiter.md`.

2. **Sélection.** Ne retiens que les informations dont la crédibilité
   combinée est ≤ 3 (STANAG 2511) et qui apportent une évolution réelle par
   rapport au contenu actuel des documents : nouveau système identifié,
   changement de statut d'un programme déjà recensé, nouvel export
   d'armement confirmé, changement de posture documenté par un indicateur
   concret. Écarte tout le reste.

3. **Excel** (`documents/Capacites_Militaires_Chinoises_RPC.xlsx`). Pour
   chaque évolution retenue concernant un système déjà recensé : mets à
   jour la ligne concernée (nombre, statut, description) et actualise la
   colonne Sources avec la nouvelle référence et son code STANAG 2511, sans
   supprimer l'historique de sourcing existant. Pour un système absent du
   classeur : ajoute une nouvelle ligne dans l'onglet approprié (PLA / PLAN
   / PLAAF / PLARF / Etranger) en respectant exactement les colonnes et le
   style déjà en place.

4. **Word** (`documents/Analyse_Capacites_Militaires_Chinoises.docx`). Pour
   chaque évolution retenue : identifie la section analytique concernée et
   ajoute un paragraphe ou amende un paragraphe existant, avec citation de
   la source. Ne touche pas à la structure des titres, à la page de garde
   ni à la mise en forme. Si une évolution modifie un jugement clé de la
   synthèse exécutive (section 1), mets-le à jour en conservant le niveau
   de confiance ICD 203 réévalué si nécessaire.

5. **PowerPoint**
   (`documents/Synthese_Capacites_Militaires_Chinoises.pptx`). Ne modifie
   que les slides dont un chiffre, un fait ou un jugement affiché est
   devenu obsolète. Conserve strictement la charte graphique (palette,
   polices, structure) déjà en place. N'ajoute pas de nouvelle slide sauf
   instruction explicite ultérieure.

6. **Cohérence croisée.** Vérifie qu'un même fait mis à jour dans un
   document l'est de façon cohérente dans les deux autres s'il y figure
   également (ex. un nombre de silos ICBM doit être identique dans
   l'Excel, le Word et le PPTX).

7. **Pull request.** Ouvre une pull request `maj-hebdo/AAAA-MM-JJ` avec :
   - les trois documents modifiés en pièces jointes de la PR (fichiers
     modifiés du dépôt)
   - une description structurée en changelog : une ligne par modification,
     au format `[Document] Section/onglet — ce qui a changé — source
     (code STANAG 2511)`
   - ne fusionne pas la pull request toi-même : elle doit être validée par
     un humain.

8. **Nettoyage.** Vide `bulletins/_a_traiter.md` des lignes traitées dans
   cette mise à jour (conserve celles jugées encore insuffisamment
   recoupées, avec une note expliquant pourquoi elles sont reportées).

Si aucune évolution ne franchit le seuil de crédibilité ≤ 3 cette semaine,
n'ouvre pas de pull request et indique-le simplement dans le résumé de fin
de routine.
