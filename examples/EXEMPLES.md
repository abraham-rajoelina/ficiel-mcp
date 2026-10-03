# Exemples d'usage

Des questions telles qu'on les tape, et ce que l'assistant fait derrière.

## « Sors-moi les contacts qui ont parlé budget sans réserver d'appel. »

L'assistant cherche « budget », « tarif », « prix » dans vos messages (`ficiel_search`), croise avec l'étape de chaque contact et vous rend la liste de ceux qui n'ont jamais atteint « RDV pris ».

## « Liste mes dormants de plus de 30 jours les plus prometteurs. »

Il appelle la détection de dormants (`ficiel_find_dormant_leads`) avec votre seuil, filtre vos étapes protégées et vos listes noires, puis les classe du dernier signe de vie le plus récent au plus ancien.

## « Résume tout mon historique avec ce lead avant mon call. »

Il lit le contexte chronologique du contact, tous canaux confondus (`ficiel_get_lead_context`), et vous rend un résumé en quelques lignes : ce qu'il a demandé, ce que vous avez proposé, où ça s'est arrêté.

## « Prépare une relance pour @prenom sur Instagram, je la validerai. »

Il prépare une carte de relance (`ficiel_prepare_followup`), sans rien envoyer : vous la relisez et l'envoyez depuis Ficiel.

## « Combien de conversations ont repris cette semaine, par canal ? »

Il lit les statistiques par canal (`ficiel_get_stats_by_channel`) et compare avec la semaine précédente (`ficiel_compare_periods`).
