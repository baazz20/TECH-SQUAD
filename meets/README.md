# EduConnect - Architecture Backend et Infrastructure

Ce dépôt contient la documentation de l'architecture backend et de l'infrastructure pour la plateforme EduConnect.

## À propos d'EduConnect

EduConnect est une plateforme éducative conçue pour connecter les établissements scolaires, les enseignants, les élèves et leurs parents. Elle offre des fonctionnalités complètes de gestion scolaire, d'apprentissage en ligne et de communication.

Le projet, inspiré de systèmes comme Pronote, vise à centraliser les informations scolaires pour faciliter les échanges entre enseignants et élèves. La première phase cible les écoles privées en Côte d'Ivoire, avec une approche progressive et adaptée au contexte local.

## Approches architecturales

Nous présentons deux approches architecturales pour EduConnect :

1. **Architecture microservices** - Adaptée pour un déploiement à grande échelle
2. **Architecture monolithique modulaire** - Optimisée pour le contexte africain

Après analyse et discussions (voir résumé de la réunion du 6 avril 2025), nous recommandons l'approche monolithique modulaire pour le lancement initial, avec une évolution potentielle vers les microservices selon la croissance des besoins.

## Résumés des réunions

### Réunion du 6 avril 2025 (Première session)

#### Points clés abordés

La discussion a porté sur la structuration de l'architecture en microservices pour optimiser la gestion des requêtes et des services. Orville a souligné l'importance des tests de simulation pour évaluer la performance de la plateforme avant son lancement, tandis que Stéphane a exprimé des réserves sur l'adoption de la solution sans une infrastructure adéquate. Yao N'goran Eloge a proposé qu'un seul VPS suffise pour leurs besoins, tout en restant ouvert à l'augmentation de la capacité en fonction du trafic. Il a également suggéré un modèle monolithique modulé avec des modules fonctionnant comme des services, ainsi que la nécessité d'un API Gateway et d'un service d'authentification pour gérer les identités.

Yao N'goran Eloge a détaillé les services nécessaires à la gestion d'une institution éducative, tels que la messagerie, le suivi des absences et la gestion des notes. Il a également présenté des services analytiques et d'intelligence artificielle, en mettant l'accent sur l'analyse prédictive. Bah Mouctar a insisté sur l'importance d'une base solide pour l'utilisateur et a proposé de créer un schéma pour visualiser les besoins du projet, tout en avertissant que des analyses incomplètes pourraient compliquer le codage. La nécessité d'optimiser le système pour les utilisateurs avec des connexions Internet limitées a également été discutée, ainsi que les avantages et les risques associés à l'architecture modulaire et aux microservices.

### Réunion du 6 avril 2025 (Deuxième session)

#### Points clés abordés

La discussion a porté sur divers aspects techniques et stratégiques liés au projet EduConnect en Côte d'Ivoire. Stéphane Zanle a soulevé des préoccupations concernant la gestion de la partie chat du projet et l'importance d'une architecture robuste pour éviter des problèmes de maintenance. Yao N'goran Eloge a suggéré que la fréquence des séances de travail devrait être augmentée, car une réunion hebdomadaire semble insuffisante. Les participants ont également débattu de l'architecture de l'application, avec Orville proposant l'utilisation de microservices et d'une API Gateway, tandis que Pierre a recommandé de se concentrer d'abord sur les fonctionnalités essentielles avant d'aborder les aspects techniques.

Le projet de plateforme de centralisation de l'information pour les écoles, inspiré de systèmes comme Pronote, a été présenté par Stéphane. Ce projet cible initialement les écoles privées en Côte d'Ivoire et vise à faciliter les échanges entre enseignants et élèves. Stéphane et Moro Kone ont discuté de l'importance d'une approche adaptée pour gagner l'acceptation des parties prenantes, tout en reconnaissant les obstacles passés. Moro a proposé de tester le projet dans une ou deux écoles avant un lancement officiel, soulignant que le succès de cette phase initiale pourrait faciliter l'acceptation de futurs projets éducatifs.

### Chapitres et sujets de la première session

#### Planification de l'architecture logicielle
Orville propose de développer une architecture en microservices, permettant à chaque service d'avoir sa spécialité. Stéphane souligne le risque d'une adoption rapide de la solution sans préparation, ce qui pourrait nuire à sa réputation. Il insiste sur l'importance de bien gérer le lancement et les retours des utilisateurs.
- Choix de l'architecture logicielle (modulaire vs microservices).
- Stratégie de gestion des utilisateurs simultanés sur la plateforme.

#### Proposition de solutions VPS et tests de stress
Orville Beranger souligne l'importance de réaliser des tests de stress sur la plateforme pour évaluer sa capacité à gérer un grand nombre d'utilisateurs. Il propose de simuler jusqu'à 20 000 connexions pour déterminer si la plateforme peut supporter cette charge avant d'augmenter les ressources si nécessaire.
- Utilisation d'un VPS pour l'hébergement des services.
- Importance des tests de stress pour évaluer la performance de la plateforme.

#### Stratégie de développement et architecture des services
Orville Beranger met en avant la nécessité de créer des packages pour faciliter la réutilisabilité des services dans les projets futurs. Il explique que les backend exposeront des API pour différentes interfaces, y compris mobile et front-end. Yao N'goran Eloge, quant à lui, propose une architecture monolithique modulée, où chaque module peut fonctionner comme un service, avec un API Gateway pour gérer les routes.

#### Gestion des services éducatifs
Yao N'goran Eloge décrit plusieurs services essentiels pour le bon fonctionnement d'une école. Le service messagerie gère la communication entre parents et enseignants, tandis que le service notes s'occupe de l'enregistrement et du calcul des notes. Le service absence suit les présences et absences des élèves, avec des alertes automatiques pour les parents.

#### Infrastructure et Architecture du Système
Yao N'goran Eloge a détaillé les services analytiques, de notification et d'IA qui seront mis en place, ainsi que les 12 composants d'infrastructure identifiés. Il a souligné l'importance d'un cluster Kubernetes pour gérer la charge des utilisateurs et a expliqué le fonctionnement d'une architecture backend modulée. La mise en cache, la sécurité et le monitoring ont également été abordés.

#### Proposition de schéma et analyse des besoins
Bah Mouctar a exprimé des préoccupations concernant la base de l'utilisateur et a suggéré de développer un schéma pour mieux comprendre les besoins. Il a souligné que le codage ne devrait pas prendre beaucoup de temps si l'analyse initiale est bien faite. Il a également mentionné l'importance d'établir un flot clair pour le projet afin d'obtenir de bons résultats.

#### Discussion sur l'architecture des services
Yao N'goran Eloge a discuté des choix architecturaux entre microservices et applications modulaires, en mettant en avant l'utilisation de solutions cloud comme Cloud Run et Amazon Lambda. Il a également mentionné les défis liés à la complexité et aux coûts de maintenance des microservices, tout en proposant une approche modulaire comme alternative.

### Chapitres et sujets de la deuxième session

#### Discussion sur l'architecture du projet
BI Stéphane Zanle a discuté de la nécessité d'une bonne architecture pour le projet afin d'éviter des problèmes de maintenance et de garantir une expérience utilisateur optimale. Yao N'goran Eloge a proposé d'augmenter la fréquence des séances de travail, tandis que Pierre Sekredou a souligné l'importance de synchroniser les outils technologiques utilisés.
- Stratégies de mise en œuvre et de test du projet.

#### Discussion sur l'architecture des API et des microservices
Orville explique le fonctionnement du Co-API et comment il gère les requêtes pour des services comme la gestion des absences. Pierre remet en question la nécessité de séparer les services en microservices, arguant que cela pourrait compliquer la gestion des ressources. Yao mentionne avoir identifié plusieurs services, mais Pierre s'inquiète de l'impact sur la gestion du code.
- Choix de l'architecture technique (monolithique vs microservices).

#### Architecture et fonctionnalités de l'application
Orville explique que l'application sera composée de plusieurs front-ends interagissant avec une API unique, et il souligne l'importance de l'API Gateway pour des fonctionnalités comme le rate limiting. Pierre insiste sur le fait qu'il est préférable de ne pas anticiper des problèmes techniques qui ne se sont pas encore manifestés et de se concentrer sur les fonctionnalités à développer.
- Identification des services nécessaires pour l'application.

#### Projets de plateforme éducative
Stéphane a expliqué que le projet de plateforme éducative sera lancé en deux phases, avec un premier projet axé sur la centralisation des informations scolaires. Inspiré de systèmes existants comme Pronote, il permettra aux enseignants, élèves et parents d'accéder aux notes et aux informations scolaires. L'objectif est de cibler d'abord les écoles privées avant d'envisager une extension au secteur public.

#### Discussion sur un projet éducatif en Côte d'Ivoire
BI Stéphane Zanle et Moro Kone abordent un projet éducatif, insistant sur l'importance de se concentrer d'abord sur le secteur privé pour garantir le succès. Ils discutent des défis passés et de la nécessité de comprendre les besoins des écoles avant de lancer le projet. Moro Kone souligne l'importance de sonder le marché pour identifier les véritables préoccupations des établissements.
- Discussion sur le modèle économique du projet éducatif.

### Tâches identifiées

#### Première session
- Orville Beranger va commencer à faire des calculs pour estimer les ressources nécessaires en fonction du nombre d'utilisateurs et des abonnements.
- Orville Beranger va garder à l'œil le point concernant l'architecture logicielle dans le développement futur.
- Yao N'goran Eloge va mettre la proposition d'architecture modulaire dans le groupe pour que les participants puissent la lire et faire des suggestions.
- Yao N'goran Eloge va partager le lien vers le nouveau coin de discussion avec les participants.

#### Deuxième session
- Yao N'goran Eloge identifiera les services nécessaires pour le projet et les présentera lors de la prochaine réunion.
- Pierre Sekredou et les autres participants travailleront sur les user stories et les fonctionnalités à partir de mercredi.
- BI Stephane Zanle demandera à Mathias de clarifier la logique de l'API et de l'architecture lors de la prochaine réunion.

### Questions clés en suspens

- Quelle est la stratégie pour gérer le nombre d'utilisateurs simultanés sur la plateforme ?
- Quel langage de programmation sera utilisé pour le développement ?
- Comment les services seront-ils organisés dans l'architecture ?
- Quels services doivent être séparés dans l'architecture du projet ?
- Quelle approche technique devrions-nous adopter pour le développement ?
- Quel est le meilleur modèle économique à adopter pour le projet éducatif ?

## Structure de la documentation

Le document principal d'architecture contient les sections suivantes :

1. **Architecture Backend** - Détail des services et composants
2. **Infrastructure Cloud** - Composants d'infrastructure et déploiement
3. **Architecture de Données** - Structure et flux de données
4. **Sécurité et Conformité** - Mesures de sécurité et conformité réglementaire
5. **Intégrations Tierces** - Intégrations avec des services externes
6. **Stratégie de Déploiement** - Approche CI/CD et environnements
7. **Considérations Spécifiques pour l'Afrique** - Adaptations au contexte africain
8. **Architecture Backend Monolithique Modulaire** - Alternative recommandée

## Technologies recommandées

- **Backend**: Node.js, Express.js, TypeScript
- **Base de données**: PostgreSQL
- **Cache**: Redis
- **File de tâches**: Bull
- **Stockage**: Solution compatible S3

## Plan de mise à l'échelle

1. **Phase Initiale** - Monolithe unique avec base de données unique
2. **Phase de Croissance** - Scaling vertical et optimisations
3. **Phase d'Expansion** - Multiple instances et séparation des workers
4. **Phase de Maturité** - Extraction potentielle de modules en microservices

## Prochaines étapes

1. Finaliser les choix technologiques et l'architecture (monolithique modulaire vs microservices)
2. Mettre en place l'environnement de développement
3. Développer les user stories et définir clairement les fonctionnalités prioritaires
4. Développer les premiers modules core (Authentification, Utilisateurs)
5. Tester le projet dans une ou deux écoles pilotes
6. Réaliser des tests de performance et de charge (simuler jusqu'à 20 000 connexions)
7. Préparer le déploiement initial pour les écoles privées en Côte d'Ivoire

---

Document préparé par l'équipe architecture d'EduConnect, avril 2025.