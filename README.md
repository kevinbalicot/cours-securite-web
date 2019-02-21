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
