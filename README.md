Quelles sont les structures de données à utiliser ?

****Structures pour les arguments des threads (ThreadArgs) :
ThreadArgs est une structure qui contient les arguments passés aux threads producer et consumer. Ces arguments incluent des informations sur la plage de lignes à traiter, les matrices B, C et A, ainsi que d'autres détails nécessaires pour effectuer les calculs.
****Mutex pour les matrices B et C (matrix_B_mutex et matrix_C_mutex) :
Ces mutex sont utilisés pour synchroniser l'accès aux matrices B et C lors des calculs dans la fonction producer. Ils garantissent qu'un seul thread peut accéder à ces matrices à la fois.
**** Sémaphores (buffer_semaphore et result_matrix_semaphore) :
Les sémaphores sont utilisés pour coordonner l'accès au tampon (buffer) entre les threads. Le sémaphore buffer_semaphore est utilisé pour protéger l'accès concurrent au tampon, tandis que le sémaphore result_matrix_semaphore est utilisé pour coordonner l'accès à la matrice résultante A.
****Tableaux pour les matrices B, C et le tampon (B, C, A et buffer) :
Ces tableaux contiennent les données des matrices B, C et le tampon intermédiaire utilisé pour stocker les résultats partiels.

q2: Comment allez-vous protéger l'accès à ces données?

****Matrices B et C (mutex) :
Les matrices B et C sont protégées par des mutex (matrix_B_mutex et matrix_C_mutex) dans la fonction producer. Avant d'accéder à chaque élément de ces matrices, le thread acquiert les verrous correspondants. Une fois les calculs effectués, les verrous sont relâchés.
****Tampon (sémaphore) :
L'accès au tampon est protégé par un sémaphore (buffer_semaphore). Avant d'écrire dans le tampon, le thread producteur attend que le sémaphore soit disponible en utilisant sem_wait. Après avoir écrit dans le tampon, le sémaphore est libéré avec sem_post.
****Matrice résultante A (sémaphore) :
L'accès à la matrice résultante A est également protégé par un sémaphore (result_matrix_semaphore). Avant de copier les données du tampon vers la matrice A, le thread consommateur attend que le sémaphore soit disponible. Une fois la copie effectuée, le sémaphore est libéré.

3q quels sont les risques
****Le code fourni utilise des mécanismes de synchronisation tels que les mutex et les sémaphores pour éviter les conditions de course et garantir un accès sûr aux données partagées entre les threads pas des resque
resume
Le programme en question réalise une multiplication matricielle parallèle à l'aide de threads producteurs et consommateurs. Les matrices B et C sont générées aléatoirement et stockées dans des tableaux. Des threads producteurs calculent les produits partiels et les stockent dans un tampon, tandis que des threads consommateurs copient ces résultats dans la matrice résultante A. La synchronisation est assurée par des mutex pour les matrices B et C, ainsi que des sémaphores pour le tampon et la matrice résultante

