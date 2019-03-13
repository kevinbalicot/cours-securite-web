# Cours Sécurité Web

Présentations disponibles sur Google Drive
- [Partie chiffrement](https://docs.google.com/presentation/d/1FyXmidPlStw-xpbL8u_ae19vxrBYItBO3a-NaX3QrHM/edit?usp=sharing)
- [Partie failles de sécurité](https://docs.google.com/presentation/d/1g55QpCEWV-4vtthX_lvlMsRg75wkGwY7Gs8RE9ygKcU/edit?usp=sharing)

Lien vers la [VM](https://drive.google.com/open?id=1D96yUQFslDjB4YL7Vn2LY_xIDze8VhOR)

## TP 1

### Exercice 1

Objectif : Chiffrez un message avec un chiffrement symétrique avec une clé alphanumérique

Pour ce faire vous devez :
 - Utiliser `openssl`
 - Utiliser l'algorithme `aes-256-cbc`

Envoyez maintenant votre message chiffré à votre collègue.
N'oubliez pas de lui communiquer discrètement le clé secrète.

### Exercice 2

Objectif : Répétez l'exercice 1 mais avec un fichier, puis envoyez le à votre collègue qui doit le déchiffrer.

Réflexion : Vous venez de chiffrer un message ou un fichier. Ce procédé est relativement sécurisé si vous utilisez un mot de passe fort. Cependant vous devez transmettre ce mot de passe de façon sécurisé. Sur un réseau d'ordinateurs cela peut poser problème.

## TP 2

Objectif : Hachez un mot de passe de 4 caractères (Az2f, 2e4E, dlm9 ...) avec l'algorithme `sha256`.

Pour ce faire vous devez :
 - Utiliser `openssl`
 - Utiliser l'algorithme `sha256`

Ensuite utilisez le programme en python `password_cracker.py` pour tenter de retrouver le mot de passe depuis le hache.

Pour ce faire utilisez la commande `python password_cracker.py <hash> brute_force` en remplacement `<hash>` par celui généré plus haut.

Essayez maintenant avec un mot de passe de 6 caractères, puis 8.

Réflexion : Plus un mot de passe haché est long, plus il faudra de temps pour le retrouver. Vous pouvez être tenté de choisir des mots pour vous souvenir de votre mot de passe, cependant le programme `password_cracker.py` permet de faire des attaques par dictionnaire, rendant plus rapide le cassage de votre mot de passe. Préférez toujours un mot de passe long avec des caractères spéciaux (%$#!).

Le programme `password_cracker` vient de cette [vidéo](https://www.youtube.com/watch?v=Z8nGpUOQPaA&list=PLOapGKeH_KhFBC39ltMDhkEx1aI3hlwSK&index=4)

## TP 3

### Exercice 1

Objectif : Chiffrez un message avec un chiffrement asymétrique.

Pour ce faire vous devez :
 - Utiliser `openssl`
 - Créer une clé publique et une clé privée
 - Chiffrer un message avec un clé publique
 - Déchiffrer un message avec un clé privée

Créez 2 paires de clés pour chacun de vous et utilisez respectivement la clé publique A pour chiffrer un message à transmettre à l'utilisateur A et la clé publique B pour transmettre un message chiffré à l'utilisateur B.

Réflexion : Grace aux clés il n'y a plus de risque lors de la transmission de la clé de chiffrement. Cependant lorsque vous récupérez un message chiffré, comment être sur que le destinataire est bien votre collègue ? Imaginons que ce message chiffré vous transmet une nouvelle clé publique à utiliser, comment être certain que ce message ne provient pas d'un pirate ?

### Exercice 2

Objectif : Signez un fichier avec une clé privée

Pour ce faire vous devez :
 - Utiliser `openssl`
 - Utiliser une clé privée
 - Créer une empreint du fichier à transmettre
 - Créer la signature de l'empreint

Une fois la signature créée, vérifiez la avec votre clé publique.

Réflexion : Grace aux signatures, vous pouvez maintenant authentifier l'émetteur du fichier.

## TP 4

### Exercice 1

Objectif : Créez un certificat CSR et un certificat CA

Pour ce faire vous devez :
 - Utiliser `openssl`
 - Auto signer le certificat
 - Le `Common Name` dans le certificat doit être `monsite.com`

### Exercice 2

Objectif : Créez une configuration Apache pour votre site `monsite.com` et activez `HTTPS`

ATTENTION, modifiez votre fichier `hosts` (`/etc/hosts` sur linux) pour faire pointer `monsite.com` sur 127.0.0.1

Si vous pouvez accéder à `httpS://monsite.com`, bravo votre site est sécurisé !

# TP 5

Un client vous à demandé de prendre possession d'un site personnel, votre objectif est de vous connecter sur le site avec les permissions administrateur.

Vous savez que le site cible est sur une infrastructure Apache, PHP 5.x et MySQL 5.x.

Cadre du TP : [Une VM](https://drive.google.com/open?id=1D96yUQFslDjB4YL7Vn2LY_xIDze8VhOR) est fournie pour le TP, rédigez un compte rendu de chaque attaque avec des screenshot que vous fournirez comme preuve à votre client.

### Exercice 1

Type d'attaque : Injection SQL

Faites une tentative d'injection SQL pour vous connecter au site.

### Exercice 2

Type d'attaque : Cross-Site Scripting (XSS)

Le site possède un livre d'or apparemment non protégé, votre objectif est d'injecter un script JavaScript qui affiche les cookies de l'utilisateur (faites en sorte qu'on ne puisse ce douter de votre attaque).

Si un utilisateur connecté accède à la page du livre d'or, le script js affichera ses cookies, dérobez cette information puis avec un autre navigateur changez votre cookie avec celui de la cible, vous devriez être maintenant connecté en tant que l'utilisateur.

Info : Dans cet exercice nous nous contentons d'afficher le cookie, mais lors d'une vraie attaque, ce cookie est transmit secrètement vers un serveur frauduleux.

### Exercice 3

Type d'attaque : Violation d'Authentification

Trouvez le panneau d'administration et son formulaire d'authentification, ce formulaire est mieux protégé que celui de l'accueil et une injection SQL ne marchera pas. Cependant ce formulaire divulgue beaucoup trop d'information en cas d'échec d'authentification. Votre objectif : trouvez le login d'un administrateur.

Maintenant que vous possédez le login d'un administrateur, il sera facile (quoique potentiellement long) de tenter une attaque par brut de force sur le formulaire de connexion.

Mais on peut gagner du temps en utilisant des outils du site, en effet le site possède une fonctionnalité de "Mot de passe perdu" via réponse à une question secrète, il ce peut que la réponse à la question soit contenue dans les informations publiques de l'utilisateur. Cherchez sur le site la réponse permettant d'utiliser la fonctionnalité "mot de passe perdu" du compte administrateur.

Info : Sachez que cette pratique est très répandue, les informations utiles sont souvent récupérées sur les réseaux sociaux ou l'amorçage par email. On appelle ce principe le social engineering.

### Exercice 4

Type d'attaque : Défaillance dans la restriction des accès à une URL

Vous avez maintenant accès au panneau de configuration de l'administrateur. Cependant celui-ci est pauvre en fonctionnalité.

Votre objectif maintenant est de trouver les identifiants de la base de données pour récupérer toutes les informations utilisateurs de celle-ci.

Pour ce faire vous pouvez essayer de récupérer des fichiers du site via le lien de téléchargement de fichier join proposé sous chaque article du site. Tentez de revenir d'un ou deux dossiers en arrière et cherchez des fichiers comme `db`, `admin`, `config` avec des extensions comme `.txt`, `.php`, `.yml|yaml` etc ...

### Exercice 5

Maintenant que vous connaissez les faiblesses du site, proposez une correction de chaque bout de code vulnérable (code à fournir dans votre compte rendu). Vous trouverez le code source du site dans le dossier `/var/www/html`.
