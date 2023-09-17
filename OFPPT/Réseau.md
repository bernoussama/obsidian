Commandes Switch:

- redémarrer Switch(ne marche pas en mode config)
```
S1#reload
```

- enter en mode privilégié
```
Switch>en
```

- enter en mode configuration globale
```
Switch#conf t
```
- changer host-name a `S1`
```
Switch(config)#hostname S1
```

- ajouter mot de passe `123`
```
Switch(config)#enable secret 123
```

- ajouter mot de passe au lignes VTY
```
S1(config)#line vty 0 15

S1(config-line)#password 456

S1(config-line)#login
```

- crypter les mots de passe
```
S1(config)#service password-encryption
```

- afficher configuration actuelle (mode privilegie seulement)
```
S1#show run
```

- enregister la conf actuelle dans la NVRAM
```
S1#copy running-config startup-config
```
ou
```
S1#write
```

> **Mode Trunk <=> Mode agregee**

`show vtp status`