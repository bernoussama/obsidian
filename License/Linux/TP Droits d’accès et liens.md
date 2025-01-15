### Exercice 1

#### 1. Déterminez votre ou vos groupes d’appartenance (id)
```bash
id
```

Cela affichera votre identifiant utilisateur (UID) et votre identifiant de groupe (GID), ainsi que les groupes auxquels vous appartenez.

```bash
uid=1000(oussama) gid=1000(oussama)
```
#### 2. Utilisez la commande `ls -l` depuis votre répertoire personnel
```bash
ls -l
```
Cela affichera une liste de fichiers avec des informations telles que les permissions, le propriétaire, et le groupe d’appartenance. Par exemple :
```
-rw-rw-r--  1 oussama oussama       64 Jan  4 17:16  sample
```
- `-rw-r--r--` : Les permissions du fichier.
- `oussama` : Le propriétaire du fichier.
- `oussama` : Le groupe d’appartenance du fichier.

#### 3. Donnez les équivalents symboliques des droits d’accès suivants
- **744** : `rwxr--r--`
- **633** : `rw--wx-wx`
- **755** : `rwxr-xr-x`
- **722** : `rwx-w--w-`
- **700** : `rwx------`

### Exercice 2

#### 1. Créez un répertoire `test` et un fichier `essai`
```bash
mkdir test
cd test
echo "Ceci est une phrase de test" > essai
```

#### 2. Notez les permissions actuelles
```bash
ls -l
```
Cela affichera les permissions du répertoire `test` et du fichier `essai`.

#### 3. Retirez les droits en lecture et écriture sur `essai`
```bash
chmod u-rw essai
```
Essayez d’afficher le contenu :
```bash
cat essai
```
Essayez de modifier le contenu :
```bash
echo "Nouvelle phrase" > essai
```
Vous devriez obtenir des erreurs d’accès.

#### 4. Rétablissez le droit en écriture et modifiez le contenu
```bash
chmod u+w essai
echo "echo « Ceci est un essai »" > essai
chmod u+x essai
./essai
```
Le problème est que le fichier `essai` n’est pas un script exécutable valide. Pour qu’il soit exécutable, il doit commencer par un shebang (`#!/bin/bash`).

#### 5. Rétablissez le droit en lecture
```bash
chmod u+r essai
./essai
```
Cela devrait maintenant afficher le message.

#### 6. Retirez le droit en lecture pour le répertoire `test`
```bash
chmod u-r test
ls test
cat test/essai
```
Vous ne pourrez pas lister le contenu du répertoire, mais vous pourrez toujours accéder au fichier `essai` si vous connaissez son chemin.

#### 7. Retirez le droit en écriture au répertoire `test` et au fichier `nouveau`
```bash
chmod u-w test
chmod u-w test/nouveau
echo "Modification" > test/nouveau
```
Vous ne pourrez pas modifier le fichier. Rétablissez le droit en écriture au répertoire :
```bash
chmod u+w test
echo "Modification" > test/nouveau
rm test/nouveau
```
Vous pourrez maintenant modifier et supprimer le fichier.

#### 8. Retirez le droit en exécution du répertoire `test`
```bash
chmod u-x test
cd test
ls test
```
Vous ne pourrez pas vous déplacer dans le répertoire ni lister son contenu. Le droit en exécution pour un répertoire est nécessaire pour accéder à son contenu.

### Exercice : UMASK

#### 1. Donnez la commande pour connaître `umask`
```bash
umask
```

#### 2. Changez `umask` à 044
```bash
umask 044
```

#### 3. Définissez un `umask` équilibré
Un `umask` de `002` permet à l’utilisateur d’avoir tous les droits, et au groupe d’avoir uniquement la lecture :
```bash
umask 002
```
Testez avec un nouveau fichier et répertoire :
```bash
touch nouveau_fichier
mkdir nouveau_repertoire
ls -l
```

#### 4. Redémarrez et vérifiez `umask`
Après le redémarrage, vérifiez à nouveau la valeur de `umask` :
```bash
umask
```
La valeur peut avoir été réinitialisée selon la configuration de votre système.

### Exercice 3

#### 1. Faites deux copies du fichier `/etc/passwd`
```bash
cp /etc/passwd passwd1
cp /etc/passwd passwd2
```

#### 2. Comparez leurs numéros d’inœuds
```bash
ls -li passwd1 passwd2
```
Les numéros d’inœuds seront différents.

#### 3. Créez un lien physique pour `passwd1`
```bash
ln passwd1 passwdph
```

#### 4. Comparez leurs numéros d’inœuds
```bash
ls -li passwd1 passwdph
```
Les numéros d’inœuds seront identiques.

#### 5. Modifiez le contenu de `passwd1`
```bash
echo "Nouvelle ligne" >> passwd1
cat passwdph
```
Le fichier `passwdph` reflète les modifications car il s’agit d’un lien physique.

#### 6. Créez un lien symbolique pour `passwd2`
```bash
ln -s passwd2 passwdsy
```

#### 7. Comparez leurs numéros d’inœuds
```bash
ls -li passwd2 passwdsy
```
Le lien symbolique aura un numéro d’inœud différent.

#### 8. Modifiez le contenu de `passwd2`
```bash
echo "Nouvelle ligne" >> passwd2
cat passwdsy
```
Le fichier `passwdsy` reflète les modifications car il s’agit d’un lien symbolique.

#### 9. Éditez à nouveau `passwd2`
```bash
echo "Autre ligne" >> passwd2
cat passwdsy
```
Le fichier `passwdsy` continue de pointer vers `passwd2` et reflète les modifications.

---

Ces exercices vous permettent de manipuler les permissions, les liens, et les masques de création de fichiers sous Linux.