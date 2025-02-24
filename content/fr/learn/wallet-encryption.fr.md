---
title: Cryptage du portefeuille
type: article
long_title: Comment crypter votre portefeuille via la console
cta_to: Read
meta:
  description: Comment crypter votre portefeuille via la console
  og:
    title: Wallet encryption
    description: Comment crypter votre portefeuille via la console
    site_name: DeFiChain
    image: /img/og/ogimage_en.png
    image_type: image/png
    locale: fr
content:
  sections:
    hero:
      name: hero
      headline: Cryptage du portefeuille
      subhead: Comment crypter votre portefeuille via la console
---

**Notice** : Le cryptage de votre portefeuille via la console entraînera un changement de votre phrase mnémonique, ne comptez pas sur votre phrase mnémonique comme sauvegarde si vous suivez ce guide, faites plutôt une sauvegarde après avoir activé le cryptage en utilisant des fichiers de sauvegarde et stockez-les dans un endroit sûr.

Au moment de la rédaction de ce document, v2.1.4, l'application ne dispose pas encore d'une interface graphique intégrée pour faciliter le cryptage ou le verrouillage des portefeuilles. Cela peut constituer un risque sérieux car vos portefeuilles peuvent être compromis par toute personne ou système ayant accès à votre fichier `wallet.dat` dans votre dossier DeFi. 

Comme le nœud DeFiChain est un fork de Bitcoin Core, il dispose d'un cryptage de portefeuille hérité que vous êtes en mesure de gérer avec une relative facilité.

Ce guide montre comment vous pouvez effectuer le cryptage et le décryptage du portefeuille, également connu sous le nom de verrouillage et déverrouillage du portefeuille par l'accès à la console disponible via l'application DeFi Wallet

**Disclaimer** : Vérifiez et comprenez toutes les commandes que vous vous apprêtez à saisir dans la console, en particulier celles provenant de sources non fiables. L'auteur de ce guide n'est pas responsable de toute perte de fonds.

## 1. Sécuriser votre portefeuille

1. Faites une sauvegarde de votre `wallet.dat` existant dans un endroit sûr. Ce fichier est très important pour récupérer vos DFI et vos tokens standards DeFi (DST) si les choses tournent mal. Le fichier se trouve généralement dans les chemins suivants :
  `~/.defi/wallets` pour Linux
  `~/Library/Application Support/DeFi/wallets` pour Mac
  `<root>\Users\<username>\AppData\Roaming\DeFi Blockchain\wallets` pour Windows.
  N'oubliez pas que ce fichier est _non crypté_ ! Gardez-le absolument en sécurité !

2. Pour sécuriser votre portefeuille pour la première fois, générez un mot de passe aléatoire long et agréable. À titre d'illustration, ce guide utilisera les phrases de passe suivantese `REMPLACER_CECI_PAR_UNE_LONGUE_PHRASE_DE_PASSE_SÉCURE`. Vous pouvez utiliser n'importe quel générateur de mot de passe aléatoire, idéalement hors ligne. Notez-la en toute sécurité.

3. Verrouillez votre portefeuille en tapant ce qui suit dans la console : 

    ```
    encryptwallet REMPLACER_CECI_PAR_UNE_LONGUE_PHRASE_DE_PASSE_SÉCURE
    ```

    Cela devrait prendre quelques secondes et vous devriez voir un message `wallet encrypted`.  À partir de ce moment, votre portefeuille, c'est-à-dire `wallet.dat` sera crypté par défaut. 

    Votre application DeFi fonctionnera comme d'habitude en affichage seul, et vos récompenses de liquidity mining DeFi afflueront comme d'habitude. Essayez d'envoyer des DFI ou DST, vous devriez maintenant voir le message suivant : `Add-on auth TX failed : Can't sign TX`. Cela montre que les clés de votre portefeuille sont maintenant cryptées. Un pirate ayant accès à votre portefeuille à ce stade serait seulement capable de voir vos avoirs, mais incapable de les dépenser.

## 2. Déverrouillage de votre portefeuille

Comme l'état de votre portefeuille est maintenant verrouillé et crypté par défaut, vous devez maintenant déverrouiller votre portefeuille chaque fois que vous voulez effectuer une transaction, par exemple envoyer des DFI ou DST, effectuer un échange DEX, ajouter des liquidités, etc.

Pour déverrouiller, allez à Console, et entrez :

```
walletpassphrase REMPLACER_CECI_PAR_UNE_LONGUE_PHRASE_DE_PASSE_SÉCURE 60
```

Cela déverrouillera votre portefeuille pendant 60 secondes. Ensuite, il se remettra automatiquement en état de verrouillage.

Vous pouvez désormais vous rendre dans votre application et effectuer toutes les transactions que vous souhaitez, en 60 secondes. Si vous vous retrouvez à recevoir le message `Add-on auth TX failed: Can't sign TX` alors que vous essayez d'effectuer une transaction, cela signifie que votre portefeuille est à nouveau verrouillé, vous devrez le déverrouiller à nouveau avec `walletpassphrase` comme ci-dessus.

## 3. Verrouillage de votre portefeuille

Si vous constatez que vous effectuez votre transaction en un temps plus court et que vous voulez vous assurer que votre portefeuille est verrouillé immédiatement sans attendre le délai d'attente, il suffit d'entrer

```
walletlock
```

Cela verrouille immédiatement votre portefeuille et empêche toute autre transaction !

## 4. Vérification de l'état de cryptage de votre portefeuille

Pour vous assurer que votre portefeuille est réellement verrouillé et crypté, vous pouvez entrer :

```
getwalletinfo
```

Pour un portefeuille crypté, vous devriez voir une réponse qui inclut `"unlocked_until": 1609145224`. Lorsqu'un portefeuille est verrouillé, `unlocked_until` doit afficher `0`. Lorsqu'il est déverrouillé, il affiche un [horodatage UNIX].(https://www.epochconverter.com).

Pour un portefeuille non crypté, `unlocked_until` est absent. Il n'afficherait même pas `0`.

---

## Conseils

1. Une fois que vous êtes sûr que votre portefeuille est bien crypté, assurez-vous de vous débarrasser de votre `wallet.dat` non crypté que vous avez fait une sauvegarde plus tôt. Vous n'en avez plus besoin.

2. Pour changer de mot de passe, utilisez `walletpassphrasechange "oldpassphrase" "newpassphrase"`.

3. Les étapes décrites dans ce guide seront intégrées dans les futures versions de l'application DeFi Wallet. En outre, le support du portefeuille matériel via Ledger est également en cours de réalisation.
