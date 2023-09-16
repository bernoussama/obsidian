

```powershell
$user = Get-ADUser -Identity 'username'
#In this example, the Get-ADUser cmdlet returns an object representing the Active Directory user with the identity 'username'. The returned object is assigned to the variable $user. learn.microsoft.com


#Use the property in another command: You can use the property value in another command like this:
Write-Host "User's Given Name is: $($user.GivenName)"

$user | Get-Member
#This will list all the properties and methods available on the $user object. learn.microsoft.com
```
