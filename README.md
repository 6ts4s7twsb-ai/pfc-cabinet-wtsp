# pfc-cabinet — plugin Claude du cabinet PFC du Nord

Ce plugin ajoute trois commandes à Claude (Claude Code) :

| Commande | Ce qu'elle fait |
|---|---|
| `/installation-whatsapp` | Une seule fois par ordinateur : Node.js, autorisations, Chrome, WhatsApp Web, application, liste des clients. |
| `/whatsapp-factures` | Cherche les PDF et photos reçus sur le WhatsApp du cabinet, les télécharge (avec votre accord) et les ajoute dans l'application PFC. Claude les lit, puis **vérifie la lecture** (montants, TVA, ICE, client) contre le fichier et signale les écarts ; l'équipe approuve. |
| `/verifier-app` | Ouvre chaque page de l'application dans Chrome et signale ce qui ne marche pas (page cassée, erreurs, connexions Gmail / WhatsApp / Drive coupées). Lecture seule. Lancé chaque matin à 8 h par une tâche planifiée. |

Claude ne fait **que lire et télécharger** dans WhatsApp : il n'écrit, ne répond et ne supprime jamais rien.
Il ne tape jamais de mot de passe : vous scannez le QR code et vous vous connectez vous-même.

## Installer (une fois par ordinateur)

Il faut : un Mac, Google Chrome, l'application Claude (onglet **Code**) ou Claude Code, et votre abonnement Claude.

1. Ouvrez l'application **Terminal** (⌘ + Espace, tapez `Terminal`, Entrée).
2. Copiez cette ligne, collez-la dans le Terminal, appuyez sur Entrée :
   ```
   claude plugin marketplace add 6ts4s7twsb-ai/pfc-cabinet-wtsp
   ```
3. Puis celle-ci :
   ```
   claude plugin install pfc-cabinet@pfc-cabinet
   ```
4. Ouvrez Claude (onglet **Code**) et tapez `/installation-whatsapp`. Suivez les étapes.

## Utiliser

Chaque matin (ou quand un client envoie des factures) : tapez `/whatsapp-factures` dans Claude.
Claude montre la liste des fichiers trouvés ; répondez « oui » pour les ajouter.

## Contrôle automatique du matin

Une tâche planifiée de l'application Claude lance `/verifier-app` chaque jour à 8 h (Mac allumé, application Claude
ouverte). Le rapport est dans `~/PFC-WhatsApp/rapports/verif-AAAA-MM-JJ.md`.

## Mettre à jour

```
claude plugin marketplace update pfc-cabinet
```

## Attention

- WhatsApp n'autorise pas officiellement l'usage d'un robot sur WhatsApp Web. Utilisez cette commande une ou deux fois
  par jour, pas en boucle, pour limiter le risque de restriction du numéro.
- Les factures restent dans le dossier Téléchargements de l'ordinateur. Supprimez-les à la fin de l'essai.
