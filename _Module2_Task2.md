### ST_DevOps2_2019_Dubovik_Dmitry_Module2_TASK2
**1. Просмотреть содержимое ветви реeстра HKCU.**  
Get-ChildItem HKCU:

**2. Создать, переименовать, удалить каталог на локальном диске.**  
New-Item c:\temp -ItemType dir  
Rename-Item c:\temp temp2  
Remove-Item c:\temp2  


**3. Создать папку C:\M2T2_ФАМИЛИЯ. Создать диск ассоциированный с папкой 
C:\M2T2_ФАМИЛИЯ.**  
New-Item c:\M2T2_DUBOVIK -ItemType dir  
New-PSDrive -Name 'h' -PSProvider FileSystem -Root "c:\M2T2_DUBOVIK" -Scope 'Global'

**4. Сохранить в текстовый файл на созданном диске список запущенных(!) служб. Просмотреть содержимое диска. Вывести содержимое файла в консоль PS.**  
Get-Service | Where {$_.Status -eq 'running'} | Out-File 'h:\running-services.txt'  
Get-ChildItem h:  
Get-Content h:\running-services.txt

**5. Просуммировать все числовые значения переменных текущего сеанса.**  
$sum = 0;  
Get-Variable | Where {$_.Value -match '^[\d\.]+$' -and $_.Name -ne 'sum'} |  
Foreach {'name=' + $_.Name + ' value=' + $_.value; $sum += $_.value};  
'sum=' + $sum;

**6. Вывести список из 6 процессов занимающих дольше всего процессор.**  
Get-Process | Sort-Object TotalProcessorTime -Descending -EA 0 |  
Select -First 6 | Format-list Name, TotalProcessorTime

**7. Вывести список названий и занятую виртуальную память (в Mb) каждого процесса, разделённые знаком тире, при этом если пцесс занимает более 100Mb – выводить информацию красным цветом, иначе зелёным.**  
Get-Process | ForEach  
{if ($_.VirtualMemorySize -gt 100MB) {Write-Host $_.Name, '-', $($_.VirtualMemorySize/1MB), 'MB' -ForegroundColor red}  
else {Write-Host $_.Name, '-', $($_.VirtualMemorySize/1MB),'MB' -ForegroundColor green}}

**9. Сохранить в CSV-файле информацию о записях одной ветви реестра HKLM:\SOFTWARE\Microsoft.**  
Get-ChildItem HKLM:\SOFTWARE\Microsoft | Export-csv h:\microsoft.csv

**10. Сохранить в XML -файле историческую информацию о командах выполнявшихся в текущем сеансе работы PS.**  
Get-History | Export-Clixml h:\history.xml

**11. Загрузить данные из полученного в п.10 xml-файла и вывести в виде списка информацию о каждой записи, в виде 5 любых (выбранных Вами) свойств.**  
Import-clixml h:\history.xml | Format-List Id, CommandLine, StartExecutionTime, EndExecutionTime, ExecutionStatus

**12. Удалить созданный диск и папку С:\M2T2_ФАМИЛИЯ.**  
Remove-PSDrive h  
Remove-Item c:\M2T2_DUBOVIK -Recurse

**13. Перевести фразу:**  
$str="g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. bmgle gr gl zw fylb gq
glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle. sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj."

$res = '';  
For ($i=0; $i -lt $str.length; $i++)  
{  
$ansi=[int]$str[$i];  
if ($ansi -gt 96 -and $ansi -lt 123)  
{$res+=\[char]($ansi+2-26*($ansi-($ansi%121))/121)}  
else{$res+=$str[$i]}  
}  
$res;

(Результат) i hope you didnt translate it by hand. thats what computers are for. doing it in by hand is inefficient and that's why this text is so long. using string.maketrans() is recommended. now apply on the url.
