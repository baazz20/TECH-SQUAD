### Entités principales :
1. **Users** : Utilisateurs (élèves, enseignants, parents)
2. **Classes** : Classes d'élèves
3. **Subjects** : Matières enseignées
4. **Assignments** : Devoirs et évaluations
5. **Absences** : Absences des élèves
6. **Grades** : Notes des élèves
7. **Messages** : Messagerie entre utilisateurs
8. **Events** : Événements scolaires
9. **Resources** : Ressources pédagogiques
10. **Notifications** : Notifications envoyées aux utilisateurs
11. **Groups** : Groupes de travail pour les projets
12. **Levels** : Niveaux de classe

### 1. **Users** (pour gérer les enseignants, élèves et parents)

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key (UUID)                                          |
| first_name     | VARCHAR(30)  | Nom de l'utilisateur                                  |
| last_name      | VARCHAR(30)  | Nom de l'utilisateur                                  |
| email          | VARCHAR(100) | Email (unique)                                        |
| password       | VARCHAR(255) | Mot de passe                                          |
| role_id           | ENUM('student', 'teacher', 'parent', 'admin') | Rôle de l'utilisateur (élève, enseignant, parent) |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 2. **Levels**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| name           | VARCHAR(30)  | Nom de la classe (par exemple, "6ème")                |
| code           | VARCHAR(15)  | Nom de la classe (par exemple, "6EME")                |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 2. **Classes**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| name           | VARCHAR(30) | Nom de la classe (par exemple, "6ème1")               |
| year           | YEAR         | Année scolaire                                        |
| level_id       | INT          | Foreign Key vers le niveau responsable (Level.id)     |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 3. **Subjects**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| name           | VARCHAR(255)  | Nom de la matière (par exemple, "Mathématiques")      |
| teacher_id     | INT          | Foreign Key vers l'enseignant responsable (User.id)   |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 4. **Assignments**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| title          | VARCHAR(255)  | Titre du devoir ou de l'évaluation                    |
| description    | TEXT         | Description du devoir                                 |
| due_date       | DATETIME     | Date limite de remise du devoir                       |
| class_id       | INT          | Foreign Key vers la classe concernée                  |
| teacher_id     | INT          | Foreign Key vers l'enseignant assigné                 |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 5. **Absences**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| student_id     | INT          | Foreign Key vers l'élève (User.id)                    |
| class_id       | INT          | Foreign Key vers la classe concernée                  |
| date           | DATE         | Date de l'absence                                     |
| justification  | TEXT         | Justification de l'absence (optionnelle)              |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 6. **Grades**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| student_id     | INT          | Foreign Key vers l'élève (User.id)                    |
| assignment_id  | INT          | Foreign Key vers le devoir (Assignments.id)           |
| grade          | DECIMAL(5,2) | Note obtenue (par exemple, 15.5/20)                   |
| created_at     | TIMESTAMP    | Date de la note                                       |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 7. **Messages**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| sender_id      | INT          | Foreign Key vers l'utilisateur expéditeur (User.id)   |
| receiver_id    | INT          | Foreign Key vers l'utilisateur destinataire (User.id) |
| content        | TEXT         | Contenu du message                                    |
| created_at     | TIMESTAMP    | Date d'envoi du message                               |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 8. **Events**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| title          | VARCHAR(255)  | Titre de l'événement                                  |
| description    | TEXT         | Description de l'événement                            |
| event_date     | DATETIME     | Date et heure de l'événement                          |
| location       | VARCHAR(255)  | Lieu de l'événement                                   |
| created_at     | TIMESTAMP    | Date de création                                      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 9. **Resources**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| teacher_id     | INT          | Foreign Key vers l'enseignant responsable (User.id)   |
| title          | VARCHAR(255)  | Titre de la ressource                                 |
| file_url       | VARCHAR(255)  | Lien vers le fichier ou ressource                     |
| description    | TEXT         | Description de la ressource                            |
| created_at     | TIMESTAMP    | Date de mise à disposition de la ressource             |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 10. **Notifications**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| user_id        | INT          | Foreign Key vers l'utilisateur concerné (User.id)     |
| content        | TEXT         | Contenu de la notification                             |
| type           | ENUM('assignment', 'event', 'absence') | Type de notification (devoir, événement, absence) |
| created_at     | TIMESTAMP    | Date d'envoi de la notification                        |
| read           | BOOLEAN      | Statut de lecture de la notification (TRUE ou FALSE)  |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 11. **Groups**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| name           | VARCHAR(100) | Nom du groupe (par exemple, "Projet de Mathématiques") |
| created_at     | TIMESTAMP    | Date de création                                      |
| created_by     | INT          | Foreign Key vers l'enseignant créateur (User.id)      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 12. **Student_Classe**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| student_id     | INT          | Foreign Key vers l'élève (User.id)                    |
| class_id       | INT          | Foreign Key vers l'élève (Classe.id)                  |
| created_at     | TIMESTAMP    | Date de création                                      |
| created_by     | INT          | Foreign Key vers l'enseignant créateur (User.id)      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

### 12. **Teacher_Classe**

| Column         | Type         | Description                                           |
|----------------|--------------|-------------------------------------------------------|
| id             | INT          | Primary Key                                           |
| teacher_id     | INT          | Foreign Key vers l'enseignant (Teacher.id)            |
| class_id       | INT          | Foreign Key vers la classe (Classe.id)                |
| subject_id     | INT          | Foreign Key vers la matière (Classe.id)               |
| role           | ENUM('normal', 'principal')                    | Rôle du professeur  |
| created_at     | TIMESTAMP    | Date de création                                      |
| created_by     | INT          | Foreign Key vers l'enseignant créateur (User.id)      |
| updated_at     | TIMESTAMP    | Date de dernière mise à jour                          |

---

### Relations entre les tables :

- **Users ↔ Classes** : Un enseignant peut être associé à plusieurs classes, un élève appartient à une classe.
- **Users ↔ Subjects** : Un enseignant peut enseigner plusieurs matières.
- **Users ↔ Messages** : Les utilisateurs peuvent échanger des messages privés entre eux.
- **Assignments ↔ Classes** : Chaque devoir est attribué à une classe spécifique.
- **Grades ↔ Assignments** : Les notes sont associées aux devoirs (Assignments).
- **Absences ↔ Users** : Chaque absence est liée à un élève (User).
- **Events ↔ Classes** : Un événement peut concerner plusieurs classes, ou une classe spécifique.
- **Resources ↔ Users** : Les ressources pédagogiques sont téléchargées et partagées par les enseignants.
- **Notifications ↔ Users** : Les notifications sont envoyées à des utilisateurs spécifiques.
- **Groups ↔ Users** : Les élèves peuvent être ajoutés à des groupes de travail.

---
