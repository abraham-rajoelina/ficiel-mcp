# Rien ne part sans un humain

Kord est l'agent IA de Ficiel : il relit les conversations, retrouve les prospects qui dormaient, prépare les relances avec la vraie voix de l'utilisateur, et c'est toujours l'humain qui valide l'envoi. Le serveur MCP applique la même logique à l'assistant que vous y branchez : il ne peut écrire que si un humain lui en a donné le droit, à qui il a nommé, dans une conversation qui existe déjà.

## Deux portées, choisies par vous

Une clé, ou une connexion OAuth, porte la lecture seule ou la lecture et l'écriture. En lecture seule, aucun outil d'écriture n'est appelable, quoi que l'assistant demande : il peut lire, chercher, résumer, compter, et rien d'autre.

## Un destinataire nommé, confronté au contact réel

Les outils qui écrivent à quelqu'un (`ficiel_send_message`, `ficiel_send_media`, `ficiel_schedule_message`) exigent le paramètre `recipient` : le nom affiché, le `@pseudo`, le numéro WhatsApp ou le nom du groupe. Avant tout envoi, il est comparé au contact réel de la conversation visée. S'ils ne correspondent pas, l'envoi est refusé (`recipient_mismatch`) et rien ne part. Un contact sans aucune identité connue exige `recipient = "sans nom"` : l'absence de vérification est un choix déclaré, jamais un cas par défaut.

## Aucun message à un inconnu

L'assistant n'écrit que dans des conversations qui existent déjà. Il ne démarre jamais une prospection à froid.

## Les mêmes garde-fous que l'application

Liste noire, étapes protégées, tags bloquants, pause d'un canal, plafonds d'envoi par canal : un envoi par le MCP passe par le même chemin qu'un envoi depuis l'application, avec les mêmes refus, et « envoyé » veut dire accepté par le canal, pas « pris en charge ».

## Préparer sans envoyer

`ficiel_prepare_followup` prépare une carte de relance sans rien envoyer. Vous la validez dans Ficiel, ou l'assistant l'approuve avec `ficiel_approve_card` (ou la refuse avec `ficiel_reject_card`, la reporte avec `ficiel_defer_card`) si vous lui avez donné le droit d'écriture. `ficiel_simulate_reply` rédige ce que Kord répondrait, pour relecture, sans aucun outil d'envoi dans la simulation.

## Tout est tracé, tout se coupe

Chaque appel est journalisé (qui, quoi, quand, avec quelle clé). Une clé ou une connexion se révoque en un clic dans vos réglages Ficiel et est refusée dès l'appel suivant.
