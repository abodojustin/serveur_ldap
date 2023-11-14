# Mettre en place un Serveur LDAP sous CentOS7

Nous allons configurer entièrement OpenLDAP sur CentOS7.

`LDAP (Lightweight Directory Access Protocol)` est un protocole standart d'accès à un service d'annuaire distribué, defini par la RFC 4511. Il permet de rassembler dans une arborescence d'annuaire l'ensemble des informations concernant différents objets d'une organisation (comptes utilisateurs, groupes, machines, service réseau,...), et de permettre aux clients LDAP d'accéder à ces informations via des requêtes normalisées.

`OpenLDAP`est un service d'annuaire informatique qui fonctionne sur le modèle client/serveur. Il contient des informations de n'importe quelle nature qui sont rangées de manières hiérarchiques. Il est souvent comparé aux pages jaunes.

En informatique il est utilisé pour enregistrer un grand nombre d'utilisateur ou de services. Il permet d'organiser hiérarchiquement les utilisateurs par département ou par n'importe quel autre critère.

## Première Étape: Mettre en place notre serveur DNS

Informations
- OS: CentOS 7
- Nom du Serveur: docker
- Nom de domaine: jafacorp.lan
- Adresse Réseau: 192.168.56.0/24
- Adresse du serveur: 192.168.56.7

Nous allons installer le paquet `bind` pour le DNS.
```
su
yum install -y bind
```

Puis on s'en va changer le nom du serveur :
```
vi /etc/hostname
```

On s'en va éditer le fichier `/etc/hosts` pour mettre le nom de notre serveur et le nom de notre domaine.
on va également éditer le fichier `/etc/resolv.conf` pour mettre l'adresse IP et le nom de domaine de notre machine.
Ensuite on s'en va dans le fichier `/etc/named.conf`, fichier de configuration principal du DNS pour ajouter l'adresse IP du serveur, et au niveau de la ligne `allow-query` nous allons ajouter l'adresse réseau

## Serveur OpenLDAP

```
yum install cyrus-sasl-devel make libtool autoconf libtool-ltdl-devel openssl-devel libdb-devel tar gcc perl perl-devel wget vim -y
```