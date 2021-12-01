
## Vagrant просит PowerShel версии 3
```ps
root@Sergey-PC:/mnt/c/Users/Sergey/Vagrant-project/Alfa/vagrant#
root@Sergey-PC:/mnt/c/Users/Sergey/Vagrant-project/Alfa/vagrant# vagrant up
Vagrant failed to initialize at a very early stage:

The version of powershell currently installed on this host is less than
the required minimum version. Please upgrade the installed version of
powershell to the minimum required version and run the command again.

  Installed version:

  Minimum required version: 3
root@Sergey-PC:/mnt/c/Users/Sergey/Vagrant-project/Alfa/vagrant#
```
## Запуск PowerShell v 3.0
```ps
-Version
    Запускает указанную версию Windows PowerShell.
    Введите с этим параметром номер версии, например: "-version 2.0".
```

```ps
PS C:\WINDOWS\system32> powershell -Version 3.0
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)
```
