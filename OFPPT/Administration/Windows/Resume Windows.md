- Outils administrations windows server:
`Powershell, Telnet, SSH, RSAT(Remote Server Administration Tools), RDP(bureau a distance)`

- modifier addresse ip:
```powershell
new-netipaddress -interfaceIndex 12 -ipaddress 10.10.10.10 -PrefixLength 24 -DefaultGateway 10.10.10.1
SetDNSClientServerAddresses -InterfaceIndex 12 -Serveraddresses

# install adds
Install-windowsFeature -Name AD-Domain-Services -IncludeManagementTools

```
