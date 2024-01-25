1. Installer LVM :
 `sudo apt-get install lvm2`.

2. Ajouter des disques physiques :
vous pouvez le configurer comme un disque physique en utilisant la commande `pvcreate /dev/sdc`.
`sudo mount /dev/sdc /mnt/disk`

3. Créer des partitions :
pour créer une partition sur le disque `/dev/sdc`, vous pouvez utiliser `fdisk /dev/sdc` et suivre les instructions pour créer une nouvelle partition.

4. Convertir les partitions en LVM :
Une fois les partitions créées, vous pouvez les convertir en volumes physiques LVM en utilisant la commande `pvcreate`. Par exemple, pour convertir la partition `/dev/sdc1` en un volume physique LVM, vous pouvez exécuter la commande `pvcreate /dev/sdc1`.

5. Convertir les partitions physiques en volumes physiques :
Par exemple, pour créer un groupe de volumes appelé "myvg" à partir des volumes physiques `/dev/sdc1` et `/dev/sdd1`, vous pouvez utiliser la commande `vgcreate myvg /dev/sdc1 /dev/sdd1`.

6. Créer des volumes logiques :
 pour créer un volume logique appelé "mylv" avec une taille de 100 Go dans le groupe de volumes "myvg", vous pouvez utiliser la commande `lvcreate -L 100G -n mylv myvg`.

7. Supprimer un volume logique :
Si vous souhaitez supprimer un volume logique existant, vous pouvez utiliser la commande `lvremove`. Par exemple, pour supprimer le volume logique "mylv" du groupe de volumes "myvg", vous pouvez exécuter `lvremove myvg/mylv`.

8. Ajouter un disque à un groupe de volumes :
Si vous souhaitez ajouter un nouveau disque à un groupe de volumes existant, vous pouvez utiliser la commande `vgextend`. Par exemple, pour ajouter le disque physique `/dev/sde1` au groupe de volumes "myvg", vous pouvez exécuter `vgextend myvg /dev/sde1`.

9. Étendre un volume logique :
Par exemple, pour étendre le volume logique "mylv" du groupe de volumes "myvg" de 50 Go, vous pouvez exécuter `lvextend -L +50G myvg/mylv`.

10. Réduire un volume logique :
puis utiliser la commande `lvreduce` pour réduire le volume logique lui-même. La procédure détaillée peut varier en fonction du système de fichiers utilisé.