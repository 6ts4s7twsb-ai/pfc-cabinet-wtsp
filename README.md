# pfc-cabinet — plugin Claude du cabinet PFC du Nord

Ce plugin ajoute deux commandes à Claude (Claude Code) :

| Commande | Ce qu'elle fait |
|---|---|
| `/installation-whatsapp` | Une seule fois par ordinateur : Node.js, autorisations, Chrome, WhatsApp Web, application, liste des clients. |
| `/whatsapp-factures` | Cherche les PDF et photos reçus sur le WhatsApp du cabinet, les télécharge (avec votre accord) et les ajoute dans l'application PFC. Claude les lit ; l'équipe vérifie dans « À valider ». |

Claude ne fait **que lire et télécharger** dans WhatsApp : il n'écrit, ne répond et ne supprime jamais rien.
Il ne tape jamais de mot de passe : vous scannez le QR code et vous vous connectez vous-même.

## Installer (une fois par ordinateur)

Il faut : un Mac, Google Chrome, l'application Claude (onglet **Code**) ou Claude Code, et votre abonnement Claude.

1. Ouvrez l'application **Terminal** (⌘ + Espace, tapez `Terminal`, Entrée).
2. Copiez cette ligne, collez-la dans le Terminal, appuyez sur Entrée :
   ```
   claude plugin marketplace add 6ts4s7twsb-ai/pfc-cabinet
   ```
3. Puis celle-ci :
   ```
   claude plugin install pfc-cabinet@pfc-cabinet
   ```
4. Ouvrez Claude (onglet **Code**) et tapez `/installation-whatsapp`. Suivez les étapes.

## Utiliser

Chaque matin (ou quand un client envoie des factures) : tapez `/whatsapp-factures` dans Claude.
Claude montre la liste des fichiers trouvés ; répondez « oui » pour les ajouter.

## Mettre à jour

```
claude plugin marketplace update pfc-cabinet
```

## Attention

- WhatsApp n'autorise pas officiellement l'usage d'un robot sur WhatsApp Web. Utilisez cette commande une ou deux fois
  par jour, pas en boucle, pour limiter le risque de restriction du numéro.
- Les factures restent dans le dossier Téléchargements de l'ordinateur. Supprimez-les à la fin de l'essai.
