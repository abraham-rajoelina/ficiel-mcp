# Rien ne part sans un humain

Kord est l'agent IA de Ficiel : il relit les conversations, retrouve les prospects qui dormaient, prépare les relances avec la vraie voix de l'utilisateur, et c'est toujours l'humain qui valide l'envoi. Le serveur MCP applique la même logique à l'assistant que vous y branchez : il ne peut écrire que si un humain lui en a donné le droit, et à qui il a nommé.

## Deux portées, choisies par vous

Une clé, ou une connexion OAuth, porte la lecture seule ou la lecture et l'écriture. En lecture seule, aucun outil d'écriture n'est appelable, quoi que l'assistant demande : il peut lire, chercher, résumer, compter, et rien d'autre.

## Un destinataire nommé, confronté au contact réel

Les outils qui écrivent à quelqu'un (`ficiel_send_message`, `ficiel_send_media`, `ficiel_schedule_message`) exigent le paramètre `recipient` : le nom affiché, le `@pseudo`, le numéro WhatsApp ou le nom du groupe. Avant tout envoi, il est comparé au contact réel de la conversation visée. S'ils ne correspondent pas, l'envoi est refusé (`recipient_mismatch`) et rien ne part. Un contact sans aucune identité connue exige `recipient = "sans nom"` : l'absence de vérification est un choix déclaré, jamais un cas par défaut.

## Écrire le premier : une fonction à part, encadrée

Par défaut, l'assistant écrit dans des conversations qui existent déjà. Écrire le premier à quelqu'un passe par deux portes seulement, chacune avec ses limites : le premier contact (`ficiel_start_conversation`, `ficiel_import_first_contacts`), réservé à la formule Intégral, sur WhatsApp et LinkedIn, jamais sur Instagram, à un rythme plafonné qui protège le compte, et lancé par liste en deux temps avec confirmation ; et l'écriture en privé à un membre de l'un de vos groupes WhatsApp (`ficiel_message_group_member`), avec les limites de « Nouvelle conversation » de l'application. Le destinataire est nommé et vérifié dans les deux cas.

## Kord Intégral : l'exception que vous choisissez

En formule Intégral, Kord Intégral peut répondre et relancer seul, selon votre trame et vos règles, sous les plafonds du compte. L'assistant peut lire ses réglages, son journal et ses règles, le mettre en pause ou l'éteindre à toute formule ; l'allumer et le régler demande la formule Intégral. Un message qu'il a mis en attente se voit et se retire avant son départ (`ficiel_list_queued_sends`, `ficiel_cancel_queued_send`).

## Les mêmes garde-fous que l'application

Liste noire, étapes protégées, tags bloquants, pause d'un canal, plafonds d'envoi par canal : un envoi par le MCP passe par le même chemin qu'un envoi depuis l'application, avec les mêmes refus, et « envoyé » veut dire accepté par le canal, pas « pris en charge ».

## Préparer sans envoyer

`ficiel_prepare_followup` prépare une carte de relance sans rien envoyer. Vous la validez dans Ficiel, ou l'assistant l'approuve avec `ficiel_approve_card` (ou la refuse avec `ficiel_reject_card`, la reporte avec `ficiel_defer_card`) si vous lui avez donné le droit d'écriture. `ficiel_simulate_reply` rédige ce que Kord répondrait, pour relecture, sans aucun outil d'envoi dans la simulation.

## Tout est tracé, tout se coupe

Chaque appel est journalisé (qui, quoi, quand, avec quelle clé). Une clé ou une connexion se révoque en un clic dans vos réglages Ficiel et est refusée dès l'appel suivant.
