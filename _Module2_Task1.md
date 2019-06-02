### ST_DevOps2_2019_Dubovik_Dmitry_Module2_TASK1

**1.	Получите справку о командлете справки**  
Get-help Get-help

**2.	Пункт 1, но детальную справку, затем только примеры**  
Get-help Get-help –Full  
Get-help Get-help -Examples  

**3.	Получите справку о новых возможностях в PowerShell4.0 (или выше)**  
Get-help about_Windows_PowerShell_5.0  

**4.	Получите все командлеты установки значений**  
Get-Command -Type Cmdlet set-*  

**5.	Получить список команд работы с файлами**  
Get-Command -Type Cmdlet \*item*  

**6.	Получить список команд работы с объектами**  
Get-Command -Type Cmdlet \*object*  

**7.	Получите список всех псевдонимов**  
Get-Alias  

**8.	Создайте свой псевдоним для любого командлета**  
Set-Alias -Name psevdo -Value Set-Alias  

**9.	Просмотреть список методов и свойств объекта типа процесс**  
Get-Process | Get-Member -MemberType property, method  

**10.	Просмотреть список методов и свойств объекта типа строка**  
"Dubovik" | Get-Member -MemberType property, method  

**11.	Получить список запущенных процессов, данные об определённом процессе**  
Get-Process  
Get-Process powershell  

**12.	Получить список всех сервисов, данные об определённом сервисе**  
Get-Service  
Get-Service BITS  

**13.	Получить список обновлений системы**  
Get-Hotfix  

**14.	Узнайте, какой язык установлен для UIWindows**  
(Get-WmiObject -Class Win32_OperatingSystem).MUILanguages  

**15.	Получите текущее время и дату**  
Get-Date  

**16.	Сгенерируйте случайное число (любым способом)**   
Get-Random  

**17.	Выведите дату и время, когда был запущен процесс «explorer». Получите какой это день недели.**  
(Get-Process -Name explorer).StartTime.DayOfWeek  

**18.	Откройте любой документ в MSWord (не важно как) и закройте его с помощью PowerShell**  
$Filename='d:\dubovik.docx'  
$Word=NEW-Object -comobject Word.Application  
$Document=$Word.documents.open($Filename)  
$Word.Visible = $true  
$Document.Close()  
$Word.Quit()  

**19.	Подсчитать значение выражения S=Σ(3*i) для i=(1..N). N – изменяемый параметр. Каждый шаг выводить в виде строки. (Пример: На шаге 2 сумма S равна 9)**  
>>$n=2; $s=0;  
>> for ($i=1; $i -le $n; $i++)  
>> {  
>> $s = $s+$i*3;  
>> 'На шаге ' + $i + ' сумма S равна '+$s  
}  

**20.	Напишите функцию для предыдущего задания. Запустите её на выполнение.**  
>> function summa {  
>> $n=$args[0]; $s=0;  
>> for ($i=1; $i -le $n; $i++)  
>> {  
>> $s = $s+$i*3;  
>> 'На шаге ' + $i + ' сумма S равна '+$s}  
>> }  

>> Summa 2

