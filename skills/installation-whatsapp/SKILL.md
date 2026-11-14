---
name: installation-whatsapp
description: Installation guidée, une seule fois par ordinateur, pour /whatsapp-factures — vérifie Node.js, enregistre les autorisations de Claude, ouvre Chrome, connecte WhatsApp Web et l'application PFC, et crée la liste des discussions clients. Utiliser pour "/installation-whatsapp", "installe whatsapp factures", "configure whatsapp".
---

# /installation-whatsapp

**Réponds en français simple. Une action à la fois.** Dis exactement sur quel bouton cliquer, avec le libellé entre « ».
La personne ne tape aucune commande et n'ouvre aucun fichier : tu fais le reste.

## 1. Node.js

Lance `node --version`.
- Version 20.19 ou plus récente → continue.
- Erreur ou version plus ancienne → dis : « Ouvrez https://nodejs.org, cliquez sur le bouton vert « LTS », ouvrez le
  fichier téléchargé, cliquez sur « Continuer » jusqu'à « Installer », tapez le mot de passe du Mac, puis « Fermer ».
  Ensuite, quittez Claude (⌘Q) et rouvrez-le, et relancez /installation-whatsapp. » Arrête-toi.

## 2. Autorisations de Claude

Le fichier `autorisations/settings-pfc.json` du plugin contient la liste des actions que Claude peut faire sans
demander à chaque fois (outils Chrome du plugin, lecture du dossier Téléchargements, écriture dans `~/PFC-WhatsApp`).
1. Lis ce fichier (il est dans le dossier du plugin : cherche `settings-pfc.json` sous `~/.claude/plugins/`).
2. Lis `~/.claude/settings.json` (s'il n'existe pas, pars de `{}`).
3. Montre à la personne, en une phrase, ce que tu ajoutes. Puis **ajoute** chaque règle de `permissions.allow` qui
   manque, sans rien supprimer ni modifier d'autre. Claude Code demandera l'accord pour modifier ce fichier :
   dis à la personne de cliquer « Autoriser ».
4. Dis : « Quittez Claude (⌘Q) et rouvrez-le une fois, pour que les autorisations s'appliquent. » Si elle le fait,
   elle relance /installation-whatsapp : saute alors les étapes 1 et 2 si elles sont déjà faites.

## 3. Ouvrir Chrome

`list_pages` (outil du plugin). Une fenêtre Chrome s'ouvre (profil réservé). Si l'outil échoue :
- « Chrome introuvable » → dis d'installer Google Chrome depuis https://www.google.com/chrome ;
- autre erreur → montre le texte exact et arrête-toi.

## 4. Connecter WhatsApp Web

1. `new_page` sur `https://web.whatsapp.com`, puis `take_snapshot`.
2. Si un QR code s'affiche, dis : « Prenez le téléphone du cabinet. Ouvrez WhatsApp › ⋮ (Android) ou Réglages (iPhone)
   › « Appareils connectés » › « Connecter un appareil ». Scannez le code dans la fenêtre Chrome. Dites "c'est fait". »
3. Attends. Vérifie que la liste des discussions s'affiche.

## 5. Connecter l'application

1. Demande l'adresse de l'application (elle commence par `https://` et finit souvent par `.up.railway.app`).
2. `new_page` sur cette adresse. Dis : « Cliquez sur « Se connecter avec Google » et choisissez votre adresse.
   Dites "c'est fait". » Ne tape jamais de mot de passe toi-même.
3. Vérifie que l'application s'affiche (menu de gauche avec « Tâches »).

## 6. Liste des discussions clients

1. Demande : « Quelles discussions WhatsApp contiennent des factures de clients ? Donnez les noms tels qu'ils
   s'affichent dans WhatsApp. » (On peut laisser vide : Claude regardera toutes les discussions récentes et demandera
   chaque fois.)
2. Pour chaque nom, cherche la discussion dans WhatsApp Web, ouvre le panneau « Infos » (clic sur l'en-tête) et lis le
   numéro. Ne tape rien dans la zone de message.
3. Montre la liste (nom, numéro) et demande confirmation.

## 7. Écrire la configuration

Crée `~/PFC-WhatsApp/config.json` :
```json
{ "adresse_app": "<adresse>", "dernier_passage": null, "discussions": [ … ], "deja_importes": [] }
```

## 8. Réglage de Chrome pour les téléchargements

Dans la fenêtre Chrome du plugin : `navigate_page` sur `chrome://settings/downloads`, `take_snapshot`. Si
« Toujours demander où enregistrer les fichiers » est activé, dis à la personne de le désactiver (clic sur
l'interrupteur). Sinon, rien à faire.

## 9. Fin

Récapitulatif : Node OK, autorisations OK, WhatsApp connecté oui/non, application connectée oui/non, nombre de
discussions dans la liste. Puis : « Pour récupérer les factures, tapez /whatsapp-factures. »

Facultatif, si la personne le demande : une tâche planifiée chaque matin. Dans l'app Claude (onglet Code),
elle peut demander : « Planifie /whatsapp-factures chaque jour à 9 h ». L'ordinateur doit être allumé, Chrome peut être
fermé (le plugin le rouvre).
