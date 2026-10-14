# Ficiel MCP : brancher Claude sur vos DM Instagram, WhatsApp et LinkedIn

[English version](README.en.md)

Ficiel est une boîte de réception IA pour coachs et setters : elle ressort les anciennes conversations Instagram, WhatsApp et LinkedIn à relancer, prépare le message, et rien ne part sans validation humaine.

Ce dépôt documente son serveur MCP (Model Context Protocol) : l'adresse qui permet à Claude, Cursor ou tout client MCP de lire vos conversations, retrouver un contact, repérer les prospects qui dorment et préparer une relance, avec votre autorisation. Il ne contient que de la documentation : le serveur est un service hébergé par Ficiel, son code n'est pas publié ici.

- Adresse du serveur : `https://bridge.ficiel.io/mcp` (Streamable HTTP)
- Outils : 73 au 14 octobre 2026, dont 17 qui affichent un écran interactif, et 12 demandes prêtes à l'emploi (prompts) dans le menu de votre assistant ; aucun vocal n'est généré, un vocal envoyé est toujours un de vos vocaux enregistrés (statistiques, entonnoir, cash, contacts à relancer, relance prête, fiche, analyse…), liste complète dans [TOOLS.md](TOOLS.md)
- Écrans interactifs (MCP Apps, depuis le 8 octobre 2026) : « qui m'a laissé en vu ? » affiche la liste des contacts à relancer avec un bouton Relancer, la relance préparée s'ouvre dans le même écran et part d'un clic sur Envoyer ; aussi la fiche d'un prospect et la synthèse du mois
- Textes jamais coupés : messages, vocaux, notes, instructions de Kord sortent en entier ; une réponse longue se pagine (`next_cursor`)
- Médias lisibles : une image porte sa description et son texte visible, un document son texte, une vidéo sa durée et ses paroles ; `ficiel_get_media` rend l'image ou le document lui-même
- Vu / non vu : l'état de lecture de votre dernier message, relu chez le canal au moment où l'assistant ouvre la conversation
- Canaux : Instagram, WhatsApp, LinkedIn
- Page officielle : https://ficiel.io/mcp/
- Registre officiel MCP : `io.ficiel/ficiel`

## Brancher l'application Claude (claude.ai, ordinateur, téléphone)

1. Connectez vos canaux à Ficiel (https://app.ficiel.io).
2. Dans Claude, ouvrez Réglages puis Connecteurs, et ajoutez un connecteur personnalisé avec l'adresse `https://bridge.ficiel.io/mcp`.
3. Claude vous envoie sur Ficiel : connectez-vous et choisissez ce que l'assistant a le droit de faire (lecture seule, ou lecture et envoi).

Aucune clé à copier : la connexion passe par OAuth, et elle apparaît dans vos réglages Ficiel, où vous la coupez quand vous voulez.

## Claude Code

Créez une clé dans vos réglages Ficiel, puis :

```bash
claude mcp add --transport http ficiel https://bridge.ficiel.io/mcp --header "Authorization: Bearer VOTRE_CLE"
```

## Cursor et autres clients MCP

```json
{
  "mcpServers": {
    "ficiel": {
      "url": "https://bridge.ficiel.io/mcp",
      "headers": { "Authorization": "Bearer VOTRE_CLE" }
    }
  }
}
```

Les clés commencent par `fk_live_`. Une clé appartient à une seule organisation et ne voit jamais qu'elle.

## ChatGPT

ChatGPT accepte les serveurs MCP distants en mode développeur, sur le web, pour les formules Plus, Pro, Business, Enterprise et Éducation ([documentation d'OpenAI](https://developers.openai.com/api/docs/guides/developer-mode)) :

1. Dans ChatGPT, Réglages, Sécurité et connexion : activez le mode développeur.
2. Créez une application de mode développeur avec l'adresse `https://bridge.ficiel.io/mcp`, authentification OAuth.
3. ChatGPT vous envoie sur Ficiel : connectez-vous et choisissez lecture seule, ou lecture et envoi.

Ce chemin suit la documentation d'OpenAI, mais il n'a pas encore été joué de bout en bout par Ficiel : les clients vérifiés sont Claude (application et Claude Code) et Cursor.

## Exemples de demandes

- « Liste les conversations où mon dernier message a été vu sans réponse depuis plus de trois jours. »
- « Lis tout l'échange avec `@prenom` et dis-moi ce qui l'a fait hésiter. »
- « Prépare une relance pour les cinq prospects qui m'ont demandé mon prix en septembre, je les validerai dans Ficiel. »
- « Ajoute à mes critères de qualification : a déjà un compte Instagram de plus de 5 000 abonnés. »

## Rien ne part sans un humain

Le serveur a été conçu pour qu'un assistant puisse tout lire et presque rien faire seul. Les règles sont détaillées dans [HUMAIN.md](HUMAIN.md) : clé en lecture seule par défaut, destinataire nommé obligatoire et confronté au contact réel, aucun message à un inconnu, mêmes garde-fous que dans l'application.

## Exemples

Des requêtes réelles et ce que l'assistant fait derrière : [examples/EXEMPLES.md](examples/EXEMPLES.md).

## Accès

Le serveur est ouvert aux organisations en essai (10 jours offerts : https://ficiel.io) ou abonnées. Sans essai démarré, en pause, ou si l'abonnement est impayé ou échu, chaque outil répond par un refus avec le lien pour réactiver l'accès.

Ce que l'assistant peut faire dépend de la formule. **Essentiel** : tout le quotidien, c'est-à-dire lire, chercher, préparer, envoyer et programmer les relances, ranger ses contacts (tags, étapes, notes, un par un ou en lot) et ajuster Kord. **Intégral** : en plus, créer et régler les automatisations, l'IA par canal et le montant de l'offre. Lire ces réglages, couper un canal ou éteindre une automatisation restent ouverts à tous. Un outil réservé répond par un refus qui dit ce que la formule permet déjà et donne le lien pour en changer.

## Contact

Abraham Rajoelina, fondateur de Ficiel : abraham@ficiel.io

Documentation sous licence CC BY 4.0 (voir [LICENSE](LICENSE)).

## Où trouver Ficiel MCP

- Registre officiel MCP : `io.ficiel/ficiel`
- [Glama](https://glama.ai/mcp/connectors/io.ficiel/ficiel)
- [LobeHub](https://lobehub.com/mcp/ficiel)
- [Cursor Directory](https://cursor.directory/plugins/ficiel-mcp)
- [mcpservers.org](https://mcpservers.org/servers/ficiel-io-mcp)
- Page officielle : https://ficiel.io/mcp/

## Licence

La documentation de ce dépôt est sous licence Creative Commons Attribution 4.0 International (CC BY 4.0, texte complet dans [LICENSE](LICENSE)), © 2026 Ficiel.io, Abraham Rajoelina. Elle ne couvre que les fichiers de ce dépôt : le service Ficiel, son serveur MCP et leur code ne sont pas concernés et restent la propriété de Ficiel.io.
