Oui. Pour le **Job 1**, il faut faire un réseau simple avec **1 routeur Cisco** et **2 PC**, puis leur donner des **IP fixes** dans le réseau `[IP masqué]/24` et tester avec `ping`. Le sujet demande ensuite de sauvegarder le fichier sous `step1.pkt`.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Matériel exact à mettre

Tu dois placer :

- **1 routeur**.
    
- **2 PC**.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]
    

Pour rester simple et cohérent avec un premier lab Packet Tracer, prends un routeur Cisco classique disponible dans Packet Tracer, par exemple un **Cisco 1941** ou un **Cisco 2911** si ton environnement le propose. L’important ici n’est pas le modèle exact, mais d’avoir un routeur avec au moins deux interfaces Ethernet utilisables pour relier les deux PC.[[youtube]([lien retiré])][[cisco](https://www.cisco.com/c/fr_fr/solutions/small-business/resource-center/networking/how-to-set-up-router.html)]

## Topologie à créer

Fais une topologie linéaire très simple :

- **PC1** → **Routeur**
    
- **PC2** → **Routeur**[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]
    

Si ton routeur a deux ports Ethernet libres, tu peux connecter :

- PC1 sur `G0/0`
    
- PC2 sur `G0/1`
    

C’est la façon la plus propre pour ce job.[[cisco](https://www.cisco.com/c/fr_fr/solutions/small-business/resource-center/networking/how-to-set-up-router.html)][[youtube]([lien retiré])]

## Plan d’adressage

Utilise ce plan :

| Équipement                 | Adresse IP    | Masque          | Passerelle    |
| -------------------------- | ------------- | --------------- | ------------- |
| Routeur interface vers PC1 | `[IP masqué]` | `[IP masqué]` | —             |
| PC1                        | `[IP masqué]` | `[IP masqué]` | `[IP masqué]` |
| PC2                        | `[IP masqué]` | `[IP masqué]` | `[IP masqué]` |

Ce choix correspond à un LAN privé simple en `/24`, ce qui est exactement ce que demande le sujet.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Connexions physiques

Tu peux utiliser :

- **Copper Straight-Through** entre chaque PC et le routeur.
    

Si les interfaces sont en auto-MDIX dans Packet Tracer, ça passe sans souci. Sinon, le câble droit est le bon choix classique pour PC vers routeur/switch dans un petit lab de base.[[hs.windows.microsoft]([lien retiré])]

## Cas conseillé

- PC1 → `GigabitEthernet0/0` du routeur.
    
- PC2 → `GigabitEthernet0/1` du routeur.
    

## Configuration du routeur

## Objectif du routeur

Le routeur doit servir de **passerelle** du réseau `[IP masqué]/24`.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Configuration dans Packet Tracer

Va dans le routeur, onglet **CLI**, puis saisis :

bash

`enable configure terminal hostname R1 interface gigabitEthernet0/0 ip address [IP masqué] [IP masqué] no shutdown exit interface gigabitEthernet0/1 ip address [IP masqué] [IP masqué] no shutdown exit end write memory`

## Explication

- `hostname R1` : donne un nom clair au routeur.
    
- `interface g0/0` : première interface, utilisée pour le premier PC.
    
- `ip address [IP masqué] [IP masqué]` : adresse de la passerelle du réseau.
    
- `no shutdown` : active l’interface, sinon elle reste éteinte.
    
- `g0/1` reçoit une autre IP du même sous-réseau si tu veux brancher le second PC directement dessus.[[youtube]([lien retiré])][[cisco](https://www.cisco.com/c/fr_fr/solutions/small-business/resource-center/networking/how-to-set-up-router.html)]
    

## Remarque importante

Dans un vrai réseau, on met souvent un switch entre le routeur et les PC. Mais ici, pour le Job 1, le sujet veut surtout comprendre le principe de base : un réseau local simple avec adressage fixe et test de connectivité.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Configuration de PC1

Va dans **PC1** puis :

- **Desktop** → **IP Configuration**
    
- choisis **Static**
    
- mets :
    

text

`IP Address: [IP masqué] Subnet Mask: [IP masqué] Default Gateway: [IP masqué]`

## Explication

- L’IP doit être unique.
    
- Le masque `/24` signifie que tous les appareils en `192.168.0.x` sont dans le même réseau.
    
- La passerelle est l’adresse du routeur, donc `[IP masqué]`.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]
    

## Configuration de PC2

Va dans **PC2** puis :

- **Desktop** → **IP Configuration**
    
- choisis **Static**
    
- mets :
    

text

`IP Address: [IP masqué] Subnet Mask: [IP masqué] Default Gateway: [IP masqué]`

## Explication

PC2 est dans le même réseau que PC1, donc il peut communiquer directement avec lui sans passer par une autre architecture. La passerelle reste nécessaire pour sortir du sous-réseau plus tard, même si ici le test principal est la communication locale.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Vérification des interfaces

Avant de tester, vérifie que :

- les liens sont bien verts,
    
- les interfaces du routeur sont en **up**,
    
- les PC ont bien reçu leurs IP statiques.[[cisco](https://www.cisco.com/c/fr_fr/solutions/small-business/resource-center/networking/how-to-set-up-router.html)][[youtube]([lien retiré])]
    

Tu peux vérifier côté routeur avec :

bash

`show ip interface brief`

Tu dois voir les interfaces configurées et actives.

## Test de ping

## Depuis PC1 vers PC2

Ouvre :

- **PC1** → **Desktop** → **Command Prompt**
    

Tape :

bash

`ping [IP masqué]`

## Résultat attendu

Tu dois recevoir des réponses du type :

- `Reply from 192.168.0.3...`
    

## Si ça ne marche pas

Vérifie dans cet ordre :

- IP de PC1.
    
- IP de PC2.
    
- masque de sous-réseau.
    
- passerelle.
    
- état des interfaces du routeur.
    
- câbles utilisés.[[youtube]([lien retiré])][[cisco](https://www.cisco.com/c/fr_fr/solutions/small-business/resource-center/networking/how-to-set-up-router.html)]
    

## Ce qu’il faut capturer

Pour ton rendu, prends au minimum :

- une capture de la topologie complète,
    
- une capture de la config IP de PC1,
    
- une capture de la config IP de PC2,
    
- une capture du ping réussi.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]
    

## Fichier à enregistrer

Enregistre ton projet sous :

text

`step1.pkt`

C’est le nom demandé dans le sujet.[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]

## Version simple à retenir

Si tu veux aller vite, retiens cette logique :

- **Routeur = [IP masqué]**
    
- **PC1 = [IP masqué]**
    
- **PC2 = [IP masqué]**
    
- **Masque = [IP masqué]**
    
- **Gateway = [IP masqué]**
    
- **Ping PC1 → PC2**[[ppl-ai-file-upload.s3.amazonaws]([lien retiré])]
    

Je peux maintenant te faire le **Job 2** aussi en mode ultra détaillé, avec le serveur DHCP/DNS, le laptop et les PC.