### ST_DevOps2_2019_Dubovik_Dmitry_Module2_TASK3

**1.	Создайте сценарии .ps1 для задач из labwork 2, проверьте их работоспостобность. Каждый сценарий должен иметь параметры.**  

**1.1.	Сохранить в текстовый файл на диске список запущенных(!) служб. Просмотреть содержимое диска. Вывести содержимое файла в консоль PS.**  
Param  
(  
$Disk='d:',  
$File='d:\running-services.txt'  
)  
Get-Service | Where {$_.Status -eq 'running'} | Out-File $File  
Get-ChildItem $Disk | Write-output  
Get-Content $File | Write-output  

**1.2.	Просуммировать все числовые значения переменных среды Windows. (Параметры не нужны)**  
$sum = 0;  
Get-Variable | Where {$_.Value -match '^[\d\.]+$' -and $_.Name -ne 'sum'} |  
foreach {'name=' + $_.Name + ' value=' + $_.value; $sum += $_.value};  
'sum=' + $sum;  

**1.3.	Вывести список из 10 процессов занимающих дольше всего процессор. Результат записывать в файл.**  
Param  
(  
$Count='10',  
$File='d:\processes.txt'  
)  
Get-Process | Sort-Object TotalProcessorTime -Descending -EA 0| Select -First $Count | Format-list Name, TotalProcessorTime | Out-file $File  

**1.3.1.	Организовать запуск скрипта каждые 10 минут**  
$atStartupeveryTenMinutesTrigger = New-JobTrigger -once -At $(get-date) -RepetitionInterval $([timespan]::FromMinutes("10")) -RepeatIndefinitely  
$scriptPath = "d:\dubovik13.PS1"  
Register-ScheduledJob -Name CheckProcessor -FilePath $scriptPath -Trigger $atStartupeveryTenMinutesTrigger  

**1.4.	Подсчитать размер занимаемый файлами в папке (например C:\windows) за исключением файлов с заданным расширением(например .tmp)**  
Param  
(  
$Mask='*tmp',  
$Dir='d:\BEPT',  
$File='d:\size.txt'  
)  
$size=0; dir $Dir -Recurse | Where {!($_.Name -like $mask)} |  
ForEach {$size+=$_.Length};  
'size='+ $size;  

**1.5.	Создать один скрипт, объединив 3 задачи:**  

**1.5.1.	Сохранить в CSV-файле информацию обо всех обновлениях безопасности ОС.**  

**1.5.2.	Сохранить в XML-файле информацию о записях одной ветви реестра HKLM:\SOFTWARE\Microsoft.**  

**1.5.3.	Загрузить данные из полученного в п.1.5.1 или п.1.5.2 файла и вывести в виде списка  разным разными цветами**  
Param  
(  
$File_CSV='d:\fix.csv',  
$File_XML='d:\registr.xml',  
$Number='1'  
)  
Get-WmiObject -Class win32_quickfixengineering | Export-csv $File_CSV  
Get-ChildItem HKLM:\SOFTWARE\Microsoft | Export-Clixml $File_XML  
if ($Number -eq '1') {Import-csv $File_CSV | Foreach {Write-host -foregroundcolor $(get-random -minimum 6 -maximum 15) $_}}  
else {Import-clixml $File_XML | Foreach {Write-host -foregroundcolor $(get-random -minimum 6 -maximum 15) $_}}  

**2.	Работа с профилем**  

**2.1.	Создать профиль**  
New-Item -ItemType file -Path $profile -force  

**2.2 В профиле изненить цвета в консоли PowerShell (Здесь и до п. 2.7 через команду notepad $profile добавляем строчки в профиль)**  
(Get-Host).UI.RawUI.ForegroundColor = 'green'    
(Get-Host).UI.RawUI.BackgroundColor = 'black'    

**2.3.	Создать несколько собственный алиасов**  
Set-Alias Export-xml Export-clixml  
Set-Alias Import-xml Import-clixml  

**2.4.	Создать несколько констант**  
$Pi = '3.14'  
$LightSpeed = '299792458'  

**2.5.	Изменить текущую папку**  
Set-Location 'D:\'  

**2.6.	Вывести приветствие**
Write-Output 'Hello, Dubovik'  

**2.7.	Проверить применение профиля**  
Закрываем-открываем powershell - всё работает  
notepad $profile    
– всё сохранилось     

**3.	Получить список всех доступных модулей**  
Get-Module –list  





