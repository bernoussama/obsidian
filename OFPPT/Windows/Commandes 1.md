#### Desactiver FIREWALL
```powershell
set-NetFirewallProfile -profile Domain,Public,Private -Enabled False
```

## Ajouter addresse IP
```powershell
get-NetIPInterface
$Interface = Read-Host "interface: "
$Ip = Read-Host "add ip: "
$Gateway = Read-Host "gateway: "
new-NetIPAddress –InterfaceIndex $Interface –IPAdress
$Ip –PrefixLength 24 – DefaultGateway $Gateway
```
## Modifier addr IP
```powershell
$Interface = Read-Host "interface: "
$Ip = Read-Host "add ip: "
$Gateway = Read-Host "gateway: "
Remove-NetIPAddress –InterfaceIndex $Interface –IPAddress $Ip – PrefixLength 24 –DefaultGateway  $Gateway
```
## Creer disque virtuel VHD (Virtual Hard Disk)
```powershell
New-VHD -path c:\base.vhd -SizeBytes (Size b bytes)
```

## Convertir VHD au VHDX
---
```powershell
convert-VHD -path c:\test\testvhd.vhd -DestinationPath c:\test\tsetvhdx.vhdx
```

## Creer switch virtuel
---
```powershell
New-VMswitch -Name "NAT" -switchtype <Internal,Private>
```

```powershell
Get-VM * | Format-table name-version
```

```powershell
Update-Vm Version Vm name
```

```powershell
Set-VMFirmware "nom VM" -secureBoottemplate MicrosoftUEFIcertificate Authority
```

```powershell
Enter-pssession -vmname NomVM
Invoke-command -VMName NomVM -scriptBlock {commands}
```

```powershell
Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest
```
