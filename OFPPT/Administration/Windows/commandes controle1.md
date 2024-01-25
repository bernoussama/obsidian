## renommer pc
```powershell
Rename-Computer -NewName "TRI-DC" -Restart
```

## Desactiver Firewall
---
```powershell
set-NetFirewallProfile -profile Domain,Public,Private -Enabled False
```

## Ajouter addresse IP
---
```powershell
get-NetIPInterface
new-NetIPAddress –InterfaceIndex 12 –IPAdress
172.16.0.200 –PrefixLength 24 – DefaultGateway 172.16.0.1
```

## Modifier addr IP
---
```powershell
Remove-NetIPAddress –InterfaceIndex 12 –IPAddress 10.10.10.10 – PrefixLength –DefaultGateway 10.10.10.254
```

## Creer disque virtuel VHD (Virtual Hard Disk)
---
```powershell
New-VHD -path c:\base.vhd -SizeBytes (Size b bytes)
```

## Convertir VHD au VHDX
---
```powershell
convert-VHD -path c:\test\testvhd.vhd -DestinationPath c:\test\tsetvhdx.vhdx
```
>`resize-partition` et `resize-vhd` pour effectuer le
compactage d’un disque dur virtuel dynamique

## Creer switch virtuel
---
```powershell
New-VMswitch -Name "NAT" -switchtype <Internal,Private>
```

## Afficher les VMs
---
```powershell
Get-VM * | Format-table name-version
```

## mettre a jour vm
---
```powershell
Update-Vm Version Vm name
```

## activer boot securiser
---
```powershell
Set-VMFirmware "nom VM" -secureBoottemplate MicrosoftUEFIcertificateAuthority
```

## exécuter commande/script PowerShell sur machine virtuelle depuis l’hôte
---
```powershell
Enter-pssession -vmname NomVM
Invoke-command -VMName NomVM -scriptBlock {commands}
```

## Deplacer VM
---
```powershell
Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest
```
