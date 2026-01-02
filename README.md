# TP 29 : RabbitMQ (Management) via Docker

## Objectif
Mise en place de RabbitMQ avec Docker et manipulation de l'interface web (Exchange, Queue, Binding, Pub/Sub).

## Prérequis
*   Docker & Navigateur web.

## Étape 1 — Identifier l'image
Repérer le tag `3.12.9-management` sur Docker Hub.

![Docker Hub Tags](screens/2025-12-26_09h47_33.png)

## Étape 2 — Télécharger l'image
```bash
docker pull rabbitmq:3.12.9-management
```
![Docker Pull](screens/2025-12-26_09h54_13.png)

## Étape 3 — Lancer le conteneur
```bash
docker run -d --hostname rabbit --name rabbit-server -p 15672:15672 -p 5672:5672 rabbitmq:3.12.9-management
```
*Port UI : 15672 | Port AMQP : 5672*

## Étape 4 — Vérification
Vérifier dans Docker Desktop que `rabbit-server` est **Running**.

![Docker Desktop Running](screens/2026-01-02_06h01_53.png)

## Étape 5 — Interface Web
Accéder à [http://localhost:15672](http://localhost:15672) (Login: `guest` / `guest`).

![RabbitMQ Login](screens/2026-01-02_06h03_28.png)

## Étape 6 — Overview
Aperçu des connexions et de l'état du nœud.

![Overview Page](screens/2026-01-02_06h03_54.png)
![Overview Details](screens/2026-01-02_06h04_30.png)

## Étape 7 — Créer Exchange
Onglet **Exchanges** > **Add a new exchange**.
*   **Name** : `2iteExchange`
*   **Type** : `direct`
*   **Durability** : `Durable`

![Add Exchange](screens/2026-01-02_06h04_55.png)

## Étape 8 — Détails Exchange
Vérifier les propriétés de `2iteExchange`.

![Exchange Details](screens/2026-01-02_06h10_01.png)

## Étape 9 — Créer Queue
Onglet **Queues** > **Add a new queue**.
*   **Name** : `2iteQueue`
*   **Type** : `Classic`

![Add Queue](screens/2026-01-02_06h10_18.png)

## Étape 10 — Binding
Dans **Exchanges** > `2iteExchange` > **Bindings**.
*   **To queue** : `2iteQueue`
*   **Routing key** : laisser vide.
Cliquer **Bind**.

![Add Binding](screens/2026-01-02_06h11_32.png)
![Binding Created](screens/2026-01-02_06h11_50.png)

## Étape 11 — Publier un message
Dans `2iteExchange` > **Publish message**.
*   **Payload** : `Hi I'm Oussama from RabbitMQ WebUI`
Cliquer **Publish message**.

![Publish Message](screens/2026-01-02_06h12_59.png)
![Message Published](screens/2026-01-02_06h13_14.png)

## Étape 12 — Vérification Queue
Dans **Queues** > `2iteQueue`.
Vérifier `Ready > 0`.

![Queue Status](screens/2026-01-02_06h13_52.png)

## Étape 13 — Lire le message
Dans `2iteQueue` > **Get messages**.
*   **Ack Mode** : `Nack message requeue true`
Cliquer **Get Message(s)** pour voir le payload.

![Get Message Payload](screens/2026-01-02_06h15_18.png)