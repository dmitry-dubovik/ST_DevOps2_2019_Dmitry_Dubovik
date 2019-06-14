### ST_DevOps2_2019_Dubovik_Dmitry_Module2_TASK4

**1.	Вывести список всех классов WMI на локальном компьютере.**   
Get-WmiObject -list  

**2.	Получить список всех пространств имён классов WMI.**  
Get-wmiobject -namespace root -class "__namespace" | ft name  

**3.	Получить список классов работы с принтером.**  
Get-wmiobject -list | Where {$_.Name -like '*print*'}  

**4.	Вывести информацию об операционной системе, не менее 10 полей.**  
Get-WmiObject -Class Win32_OperatingSystem | Format-list Name, FreePhysicalMemory, FreeVirtualMemory, LastBootUp
Time, Version, MUILanguages, Locale, BuildNumber, BootDevice, OSType  

**5.	Получить информацию о BIOS.**  
Get-WmiObject -Class Win32_Bios  

**6.	Вывести свободное место на локальных дисках. На каждом и сумму.**  
$AllFree=0;   
Get-Wmiobject -class Win32_LogicalDisk | ForEach {$_.DeviceID, $_.FreeSpace; $AllFree+= $_.FreeSpace};   
'AllFree =' + $AllFree;  

**7.	Написать сценарий, выводящий суммарное время пингования компьютера (например 10.0.0.1) в сети.**  
Param (  
$ip='10.0.0.1’,  
$count=5)  

$time=0  
for($i=0;$i -lt $count;$i++) {  
$TimeSum=0;   
For ($i=0; $i -lt $count; $i++) {$GPS = Get-WmiObject -Class win32_pingstatus -f "Address='$ip'"; $TimeSum+= $GPS.responsetime;};   
'Count=' + $Count; 'TimeSum=' + $TimeSum; 'AverageTime=' + $TimeSum/$count;  
}  

**8.	Создать файл-сценарий вывода списка установленных программных продуктов в виде таблицы с полями Имя и Версия.**  
Get-WmiObject -Class Win32_Product | Format-list Name, Version  

**9.	Выводить сообщение при каждом запуске приложения MS Word.**  
register-wmiEvent -query "select * from __instancecreationevent within 5 where targetinstance isa 'Win32_Process' and targetinstance.name='WINWORD.EXE'" -sourceIdentifier "WordStarted" -Action {Write-output "Word started" }  


