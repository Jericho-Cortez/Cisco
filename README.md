# Cisco Packet Tracer — routage IPv4

Exercice d’initiation à l’adressage IPv4 et au test de connectivité. La topologie comporte deux postes et un routeur. Chaque poste est relié à une interface routée dans un sous-réseau distinct.

## Documents

- [Prise en main de Packet Tracer](Job%201.md)

## Exemple d’adressage

| Liaison | Interface du routeur | Adresse du poste | Passerelle |
| --- | --- | --- | --- |
| PC1 vers G0/0 | `192.0.2.1/24` | `192.0.2.10/24` | `192.0.2.1` |
| PC2 vers G0/1 | `198.51.100.1/24` | `198.51.100.10/24` | `198.51.100.1` |

Vérifier l’état des interfaces avec `show ip interface brief`, puis tester chaque passerelle et la connexion entre les deux postes avec `ping`. Utiliser le tableau pour les deux liaisons directes.
