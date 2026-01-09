# TP – Service Web SOAP avec Apache CXF

## 1. Objectif du TP

* Comprendre le principe des services web SOAP et du WSDL
* Implémenter un service SOAP en Java avec Apache CXF
* Publier un service SOAP via un serveur HTTP embarqué
* Consommer le service à l’aide d’un client Java
* Tester le service avec l’outil SoapUI
* Comprendre les notions SOA (WSDL, UDDI, client/serveur)

---

## 2. Architecture du TP

### 2.1 Stack technologique

| Technologie         | Version / Détails    | Rôle                                        |
| ------------------- | -------------------- | ------------------------------------------- |
| Java                | JDK 17+              | Implémentation du service SOAP et du client |
| Maven               | 3.x                  | Gestion des dépendances et du cycle de vie  |
| Apache CXF          | 4.0.3                | Implémentation JAX-WS (SOAP)                |
| Jakarta JAX-WS      | 3.x                  | API standard pour services SOAP             |
| Jakarta JAXB        | 4.x                  | Sérialisation / désérialisation XML ↔ Java  |
| Jetty (embarqué)    | via CXF              | Publication du service HTTP                 |
| WS-Security (WSS4J) | via CXF              | Authentification UsernameToken              |
| SoapUI              | Open Source          | Test des opérations SOAP                    |
| IntelliJ IDEA       | Ultimate / Community | Développement et exécution                  |

### 2.2 Structure du projet

<img width="490" height="670" alt="image" src="https://github.com/user-attachments/assets/9c46b983-ff62-4300-9f5b-0c083d35df33" />


## 3. Résultat attendu

### 3.1 Build du projet

<img width="922" height="868" alt="1" src="https://github.com/user-attachments/assets/a936b4cf-322b-4ec7-a549-1adc0bd395fe" />


### 3.2 Publication du service

* Le serveur démarre sans erreur
* Le WSDL est accessible à l’URL :

```
http://localhost:9080/services/hello?wsdl
```
<img width="876" height="1008" alt="web" src="https://github.com/user-attachments/assets/ed3c4781-fb7f-42e0-8aa1-099d420328cc" />

<img width="306" height="219" alt="image" src="https://github.com/user-attachments/assets/5d243af3-786d-4276-9a1f-f5acf4a97633" />

---

### 3.3 Test avec SoapUI

* Le projet SoapUI est créé à partir du WSDL
* Les opérations SOAP `SayHello` et `FindPerson` sont générées

**`SayHello`**

<img width="1911" height="907" alt="sayhello" src="https://github.com/user-attachments/assets/534f948a-c9b7-4167-836d-0858f6ececd1" />

**`FindPerson`**

<img width="1858" height="877" alt="findPerson" src="https://github.com/user-attachments/assets/9a59b811-42d6-409e-a01a-183c265ad916" />

---

### 3.4 Exécution du client Java

Lors de l’exécution de la classe `ClientDemo`, la sortie suivante est attendue dans la console :


<img width="905" height="263" alt="javamin" src="https://github.com/user-attachments/assets/291d1722-8f8e-4435-a967-baf4c826aa42" />


---

### 3.5 Vérification  WSDL sécurisé avec SoapUI

Cette étape permet de tester le service SOAP sécurisé par **WS-Security (UsernameToken)** à l’aide de l’outil **SoapUI**.

#### Import du WSDL sécurisé
```
http://localhost:8080/services/hello-secure?wsdl
```
#### Configuration WS-Security

| Paramètre        | Valeur        |
|------------------|---------------|
| Username         | student       |
| Password         | secret123     |
|  WSS-Type        | PasswordText  |

<img width="1863" height="488" alt="secure" src="https://github.com/user-attachments/assets/83fdd93b-f9f9-4cd5-81cc-f8959b0c3949" />

- L’appel SOAP réussit lorsque le **UsernameToken** est correctement configuré.

<img width="1817" height="560" alt="res-secure" src="https://github.com/user-attachments/assets/1c3b5858-b45f-48d0-95bb-aec3bb886393" />

- Sans UsernameToken (ou avec des identifiants incorrects), le serveur renvoie une **SOAP Fault** indiquant un échec d’authentification.

<img width="1777" height="507" alt="result-secure-fault" src="https://github.com/user-attachments/assets/f56f9776-e481-40f8-bd12-e6d8c70dacde" />

---

## Auteur

**Réalisé par :**  Abla MARGHOUB <br>
**Encadré par :**  Pr. Mohamed LACHGAR <br> 
**Module :**  Techniques de Programmation Avancée <br> 
**Cours :**  Architecture Microservices : Conception, Déploiement et Orchestration <br>
**Établissement :**  École Normale Supérieure - Université Cadi Ayyad <br>
---
