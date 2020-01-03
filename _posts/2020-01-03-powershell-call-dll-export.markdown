---
layout: post
title:  "Calling C++ dll exported function in powershell"
date:   2020-01-03 22:26:29
categories: Powershell C++
---

Consider an exported function from a C++ dll `LiarDll.dll`
```C++
int Liar(int what);
```
To call this from powershell 

```powershell
$MethodDefinition = @'
   [DllImport("LiarDll.dll", CharSet = CharSet.Unicode, SetLastError = true)]

   public static extern int Liar(int what);
'@

$liardll = Add-Type -MemberDefinition $MethodDefinition -Name 'Liar' -Namespace 'Liar' -PassThru

$what = 15
$Result = $liardll::Liar($what)

Write-Host $Result
```
