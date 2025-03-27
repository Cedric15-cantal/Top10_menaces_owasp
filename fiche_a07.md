# A07:2021 – Identification et authentification de mauvaise qualité 

Les 22 CWE (Faiblesses communes, détectées par le MITRE) liées aux échecs d'identification.

## Types de menances liées à l'identification (login, password)

Faiblesses d'authenticiation si l'application
* **Permits automated** : autorise le bourrage d'info par robot à partir de listes de login et mdp récurrents
* **Permits brute force** : permet les attaques en boucle automatisée testant toutes les combinaisons possibles ;
* **Permits default, weak, or well-known** : autorise les mdp par défaut, faibles ou bien connus (admin/admin, 1234, 0000...) ;
* **Uses weak or ineffective credential** : utilise des processus de récupérations des informations d'identification faibles ou inefficaces (processus de mot de passe oublié faible aussi) ;
* **Uses plain text, encrypted or weackly hashed**: utilise des mdp bruts ou faiblement cryptés ;
* **Multifactor Authentication** : double authentification absente ou inefficace ;
* **expose l'identifiant dans l'URL** ;
* **réutilisation de l'id de session après une connexion réussie** ;
* **mauvaise déconnexion ou absence de déconnexion automatique après période d'inactivité**.

## Prévention

* **Authentification multifacteur** (Double authentification) => lullte contre attaques automatisées, force brute, bourrage et réutilisation d'id volés
* **Livraison/Déploiement d'outils sans id par défaut**
* **Intégrer des tests de mdp** à la création ou au changement => Comparer ce mot de passe avec la liste des 10000 mots de passe les plus faibles
* **Critères d'un bon niveau de sécu de création et gestion des mdp** => longueur, complexité, rotation  (*directives du National Institute of Standards and Technology (NIST) 800-63 B à la section 5.1.1 ou autres directives modernes*)
* **Avoir un même message de refu pour mdp ou id invalides**
* **Limiter ou retardez de plus en plus les tentatives de connexion échouées, enregister tous les échecs et alerter l'admin**
* **Utiliser un gestionnaire de session sécurisé côté serveur** => générateur d'id de session alétoire avec une entropie élevée (glaçon dans le Ricard : le bordel pour lui et pour l'eau), pas d'ID dans l'URL, stockage sécu des ID, invalidés et supprimées après déconnexion, inactivité ou une certaine durée (renouvellement de mdp).

## Informations supp

#### Scénarios 
* **Scénario 1** : La réutilisation de mots de passe, l’utilisation de mots de passe connus, est une attaque classique. Supposons une application qui n’implémente pas une protection automatisée contre le bourrage d'informations ou l'utilisation des mots de passe connus. Dans ce cas, l'application peut être utilisée comme un oracle pour déterminer si les mots de passe sont valides.

* **Scénario 2** : La plupart des attaques d’authentification se produisent en raison de l’utilisation de mots de passe comme facteur unique. Un temps considérées comme de bonnes pratiques, les exigences de rotation et de complexité des mots de passe sont considérées comme encourageant les utilisateurs à utiliser et réutiliser des mots de passe faibles. Il est maintenant recommandé d’arrêter ces pratiques selon les directives NIST 800-63 et d’utiliser du multifacteur.

* **Scénario 3** : Les timeouts de session d’application ne sont pas paramétrés correctement. Un utilisateur utilise un ordinateur public pour accéder à une application. À la place de se déconnecter correctement, l’utilisateur ferme le navigateur et quitte l’ordinateur. Un attaquant utilise ensuite le même navigateur quelque temps après et l’utilisateur est toujours authentifié.
