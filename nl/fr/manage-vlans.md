---

copyright:
  years: 2017
lastupdated: "2017-10-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Gérer les réseaux locaux virtuels (VLAN)
Vous pouvez effectuer toute une série d'actions à partir de l'[écran des détails du dispositif de passerelle](access-gateway-details.html).

## Associer un VLAN à un dispositif de passerelle

Un VLAN doit être associé à un dispositif de passerelle pour permettre son routage. L'association d'un VLAN consiste à lier un VLAN éligible à un dispositif de passerelle, de sorte à ce qu'il puisse être routé via un dispositif de passerelle par la suite. Le processus d'association n'effectue pas le routage automatique d'un VLAN à un dispositif de passerelle. Le VLAN continue à utiliser les routeurs FCR et BCR jusqu'à ce qu'il soit routé vers la passerelle. 

Les VLAN peuvent être associés à une seule passerelle à la fois et ne doivent pas avoir de pare-feu. Pour associer un VLAN à une passerelle réseau, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client. 
2. Sélectionnez le VLAN désiré dans la liste déroulante **Associer un VLAN**.
3. Cliquez sur le bouton **Associer** pour associer le VLAN.

Après avoir associé un VLAN au dispositif de passerelle, il apparaît dans la section VLAN associés de l'écran des détails du dispositif de passerelle. Dans cette section, le VLAN peut être routé vers la passerelle ou être dissocié de la passerelle. D'autres VLAN éligibles peuvent être associés à un dispositif de passerelle à tout moment en répétant la procédure ci-dessus.

## Router un VLAN associé

Les VLAN associés sont liés à un dispositif de passerelle, mais le trafic entrant et sortant du VLAN n'atteint pas la passerelle tant que le VLAN n'a pas été routé. Une fois que le VLAN associé a été routé, tous le trafic dorsal et frontal est routé via le dispositif de passerelle au lieu d'utiliser les routeurs client. 

Pour router un VLAN associé, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client. 
2. Localisez le VLAN désiré dans la section VLAN associés.
3. Sélectionnez **Router le VLAN** dans le menu déroulant Actions.
4. Cliquez sur **Oui** pour procéder au routage du VLAN. 

Après le routage d'un VLAN, tout le trafic frontal et dorsal passe des routeurs client à la passerelle réseau. D'autres commandes liées au trafic et au dispositif de passerelle même peuvent être exécutées en accédant à l'outil de gestion de la passerelle. Le routage via la passerelle réseau peut être interrompu à tout moment en [contournant le dispositif de passerelle](#bypass-gateway-appliance-routing-for-a-vlan).

## Contourner le routage du dispositif de passerelle d'un VLAN

Une fois le VLAN routé, tout le trafic frontal et dorsal passe par la passerelle réseau. A tout moment, le dispositif de passerelle peut être contourné de sorte que le trafic soit réorienté sur les routeurs client FCR et BCR. 

Le contournement du VLAN permet au VLAN de rester associé à la passerelle réseau. Si le VLAN ne doit plus être associé au dispositif de passerelle, reportez-vous à la section [Dissocier un VLAN d'un dispositif de passerelle](#disassociate-a-vlan-from-a-gateway-appliance). 

Pour ignorer le routage de la passerelle d'un VLAN, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client. 
2. Localisez le VLAN désiré dans la section VLAN associés.
3. Sélectionnez **Contourner le VLAN** dans le menu déroulant Actions.
4. Cliquez sur **Oui** pour contourner la passerelle. 

Après le contournement de la passerelle réseau, tout le trafic frontal et dorsal circule via les routeurs FCR et BCR associés au VLAN. Le VLAN reste associé au dispositif de passerelle et peut être rerouté vers ce dispositif à tout moment.

## Dissocier un VLAN d'un dispositif de passerelle

Les VLAN peuvent être liés à un dispositif de passerelle à la fois par [association](#associate-a-vlan-to-a-gateway-appliance). Une association permet au VLAN d'être routé vers le dispositif de passerelle à tout moment. Si un VLAN doit être associé à un autre dispositif de passerelle ou s'il ne doit plus être associé à sa passerelle, une dissociation est requise. La dissociation supprime le "lien" du VLAN au dispositif de passerelle, permettant ainsi au VLAN d'être associé à une autre passerelle, si nécessaire. 

Pour dissocier un VLAN d'un dispositif de passerelle, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client. 
2. Localisez le VLAN désiré dans la section VLAN associés.
3. Sélectionnez **Dissocier** dans le menu déroulant **Actions**.  
4. Cliquez sur **Oui** pour dissocier le VLAN. 

Après avoir dissocié un VLAN d'un dispositif de passerelle, le VLAN peut être associé à une autre passerelle. Le VLAN peut également être réassocié au dispositif de passerelle à tout moment. Après avoir dissocié un VLAN d'un dispositif de passerelle, le trafic du VLAN ne peut pas être routé via la passerelle. Les VLAN doivent être associés à un dispositif de passerelle pour pouvoir être routés.

## Router plusieurs VLAN via la même interface réseau
Virtual Router Appliance (VRA) peut router plusieurs VLAN via la même interface réseau (par exemple, `dp0bond0` ou `dp0bond1`). Cette opération s'effectue en définissant le port de commutation en mode de liaison et en configurant des interfaces virtuelles (VIF) sur l'unité.

Par exemple : 

```
set interfaces bonding dp0bond0 vif 1432 address 10.0.10.1/24
set interfaces bonding dp0bond0 vif 1693 address 10.0.20.1/24
```

Les commandes ci-dessus créent deux interfaces virtuelles sur l'interface `dp0bond0`. L'interface `dp0bond0.1432` traite le trafic du VLAN 1432 alors que l'interface `dp0bond0.1693` traite le trafic du VLAN 1693.
