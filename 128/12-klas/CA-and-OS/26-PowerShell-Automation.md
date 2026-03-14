# УРОЧЕН ПЛАН №26
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

| Параметър | Стойност |
|-----------|----------|
| **Училище:** | 128-мо СУ "Алберт Айнщайн", гр.София |
| **Клас:** | XII клас |
| **Учител:** | Мариян Йорданов |
| **Предмет:** | Учебна практика: Компютърни архитектури и операционни системи |
| **Тема на урока:** | PowerShell за системна автоматизация |
| **Дата:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Упражнение |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат основите на PowerShell scripting
2. Да създават скриптове за автоматизация на задачи
3. Да работят с cmdlets, variables и pipeline
4. Да управляват Active Directory чрез PowerShell
5. Да планират задачи с Task Scheduler

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на разбиране за ефективност чрез автоматизация
2. Развиване на логическо мислене при scripting
3. Изграждане на навици за документиране на код
4. Насърчаване на DRY принцип (Don't Repeat Yourself)

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за програмиране
2. Усъвършенстване на problem-solving умения
3. Формиране на способност за debugging
4. Развитие на аналитично мислене

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**PowerShell основи:**
- Cmdlets (Verb-Noun синтаксис)
- Pipeline (|) оператор
- Variables ($variable)
- Типове данни
- Control structures (if, foreach, while)

**Автоматизация:**
- Скриптове (.ps1 файлове)
- Functions
- Parameters
- Error handling
- Task Scheduler интеграция

### ОСНОВНИ УМЕНИЯ:
- Писане на PowerShell скриптове
- Автоматизиране на системни задачи
- Управление на AD обекти
- Планиране на задачи

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Програмиране** - синтаксис, логика, структури
2. **Бази данни** - SQL-подобни заявки
3. **Системна администрация** - AD, IIS, Services
4. **Мрежови технологии** - отдалечено управление

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Демонстрация на скриптове
2. Live coding с обяснения
3. Практически упражнения
4. Debugging сесии
5. Code review

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Windows Server 2022 / Windows 11
- PowerShell 7.x / Windows PowerShell 5.1
- VS Code с PowerShell extension
- Примерни скриптове (Приложение 2)
- Работни листове

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Отваряне на PowerShell ISE / VS Code
- Представяне на целите

**Мотивация:**
"Един добре написан скрипт може да замени часове ръчна работа. PowerShell е езикът на Windows администрацията."

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Преговор - основни cmdlets:**
```powershell
# Помощ
Get-Help Get-Process -Examples
Get-Command -Verb Get

# Основни cmdlets
Get-Process
Get-Service
Get-EventLog -LogName System -Newest 10
Get-ChildItem C:\
```

**Pipeline концепция:**
```powershell
# Без pipeline (традиционен подход)
$processes = Get-Process
$filtered = Where-Object -InputObject $processes {$_.CPU -gt 100}

# С pipeline (PowerShell начин)
Get-Process | Where-Object CPU -gt 100 | Sort-Object CPU -Descending
```

---

### **3. НОВ МАТЕРИАЛ И ПРАКТИКА (55 минути)**

#### **Част 1: Variables и Data Types (10 минути)**

```powershell
# Деклариране на променливи
$name = "Server01"
$port = 8080
$isEnabled = $true
$servers = @("Server01", "Server02", "Server03")
$config = @{
    Name = "WebApp"
    Port = 80
    SSL = $true
}

# Типове данни
$name.GetType()      # String
$port.GetType()      # Int32
$servers.GetType()   # Object[] (Array)
$config.GetType()    # Hashtable

# String операции
$message = "Server name is $name on port $port"
$upper = $name.ToUpper()
$contains = $name.Contains("Server")

# Array операции
$servers += "Server04"
$first = $servers[0]
$count = $servers.Count
```

**Практическа задача 1.1:**
```powershell
# Създайте hashtable с информация за вашия компютър
$myComputer = @{
    Name = $env:COMPUTERNAME
    User = $env:USERNAME
    OS = (Get-CimInstance Win32_OperatingSystem).Caption
    RAM = [math]::Round((Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory/1GB, 2)
}

$myComputer | Format-Table -AutoSize
```

---

#### **Част 2: Control Structures (12 минути)**

**If/Else:**
```powershell
$diskUsage = (Get-CimInstance Win32_LogicalDisk -Filter "DeviceID='C:'").Size
$freeSpace = (Get-CimInstance Win32_LogicalDisk -Filter "DeviceID='C:'").FreeSpace
$percentFree = [math]::Round(($freeSpace / $diskUsage) * 100, 2)

if ($percentFree -lt 10) {
    Write-Warning "CRITICAL: Only $percentFree% free space!"
} elseif ($percentFree -lt 20) {
    Write-Warning "WARNING: Low disk space - $percentFree% free"
} else {
    Write-Host "OK: $percentFree% free space" -ForegroundColor Green
}
```

**Foreach:**
```powershell
$services = @("W32Time", "BITS", "Spooler")

foreach ($service in $services) {
    $status = (Get-Service -Name $service).Status
    Write-Host "$service : $status"
}

# Или с pipeline
$services | ForEach-Object {
    $svc = Get-Service -Name $_
    [PSCustomObject]@{
        Name = $svc.Name
        Status = $svc.Status
        StartType = $svc.StartType
    }
} | Format-Table
```

**While:**
```powershell
# Изчакване на услуга да стартира
$maxAttempts = 10
$attempt = 0

while ((Get-Service -Name "Spooler").Status -ne "Running" -and $attempt -lt $maxAttempts) {
    Write-Host "Waiting for Spooler service... Attempt $attempt"
    Start-Sleep -Seconds 2
    $attempt++
}
```

---

#### **Част 3: Functions и Parameters (15 минути)**

**Практическа задача 3.1: Проста функция**

```powershell
function Get-DiskInfo {
    param(
        [string]$ComputerName = $env:COMPUTERNAME,
        [string]$DriveLetter = "C"
    )
    
    $disk = Get-CimInstance Win32_LogicalDisk -ComputerName $ComputerName `
        -Filter "DeviceID='$DriveLetter`:'"
    
    [PSCustomObject]@{
        Computer = $ComputerName
        Drive = $DriveLetter
        SizeGB = [math]::Round($disk.Size / 1GB, 2)
        FreeGB = [math]::Round($disk.FreeSpace / 1GB, 2)
        PercentFree = [math]::Round(($disk.FreeSpace / $disk.Size) * 100, 2)
    }
}

# Използване
Get-DiskInfo
Get-DiskInfo -DriveLetter "D"
```

**Практическа задача 3.2: AD User Creation Script**

```powershell
function New-LabUser {
    param(
        [Parameter(Mandatory=$true)]
        [string]$FirstName,
        
        [Parameter(Mandatory=$true)]
        [string]$LastName,
        
        [string]$Department = "IT",
        
        [string]$OU = "OU=Users,DC=lab,DC=local"
    )
    
    $username = "$($FirstName.Substring(0,1).ToLower())$($LastName.ToLower())"
    $displayName = "$FirstName $LastName"
    $email = "$username@lab.local"
    $password = ConvertTo-SecureString "Welcome2025!" -AsPlainText -Force
    
    try {
        New-ADUser -Name $displayName `
            -GivenName $FirstName `
            -Surname $LastName `
            -SamAccountName $username `
            -UserPrincipalName $email `
            -EmailAddress $email `
            -Department $Department `
            -Path $OU `
            -AccountPassword $password `
            -Enabled $true `
            -ChangePasswordAtLogon $true
        
        Write-Host "User $username created successfully!" -ForegroundColor Green
    }
    catch {
        Write-Error "Failed to create user: $_"
    }
}

# Използване
New-LabUser -FirstName "Ivan" -LastName "Petrov" -Department "Sales"
```

---

#### **Част 4: Error Handling (8 минути)**

```powershell
function Test-ServiceHealth {
    param(
        [string[]]$ServiceNames = @("W32Time", "BITS", "NonExistent")
    )
    
    foreach ($name in $ServiceNames) {
        try {
            $service = Get-Service -Name $name -ErrorAction Stop
            
            if ($service.Status -eq "Running") {
                Write-Host "[OK] $name is running" -ForegroundColor Green
            } else {
                Write-Warning "[WARN] $name is $($service.Status)"
            }
        }
        catch [Microsoft.PowerShell.Commands.ServiceCommandException] {
            Write-Error "[ERROR] Service '$name' not found"
        }
        catch {
            Write-Error "[ERROR] Unexpected error: $_"
        }
    }
}

Test-ServiceHealth
```

---

#### **Част 5: Автоматизация със скриптове (10 минути)**

**Практическа задача 5.1: System Health Report**

```powershell
# SystemHealthReport.ps1

param(
    [string]$OutputPath = "C:\Reports",
    [string]$ComputerName = $env:COMPUTERNAME
)

# Създаване на директория ако не съществува
if (!(Test-Path $OutputPath)) {
    New-Item -ItemType Directory -Path $OutputPath | Out-Null
}

$reportDate = Get-Date -Format "yyyy-MM-dd_HHmmss"
$reportFile = "$OutputPath\HealthReport_$reportDate.html"

# Събиране на данни
$os = Get-CimInstance Win32_OperatingSystem
$cpu = Get-CimInstance Win32_Processor
$disk = Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3"
$services = Get-Service | Where-Object {$_.StartType -eq "Automatic" -and $_.Status -ne "Running"}

# HTML Report
$html = @"
<!DOCTYPE html>
<html>
<head>
    <title>System Health Report - $ComputerName</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        h1 { color: #333; }
        table { border-collapse: collapse; width: 100%; margin: 20px 0; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #4CAF50; color: white; }
        .warning { background-color: #ffcc00; }
        .critical { background-color: #ff6666; }
    </style>
</head>
<body>
    <h1>System Health Report</h1>
    <p><strong>Computer:</strong> $ComputerName</p>
    <p><strong>Generated:</strong> $(Get-Date)</p>
    
    <h2>System Information</h2>
    <table>
        <tr><th>Property</th><th>Value</th></tr>
        <tr><td>OS</td><td>$($os.Caption)</td></tr>
        <tr><td>CPU</td><td>$($cpu.Name)</td></tr>
        <tr><td>Total RAM</td><td>$([math]::Round($os.TotalVisibleMemorySize/1MB, 2)) GB</td></tr>
        <tr><td>Free RAM</td><td>$([math]::Round($os.FreePhysicalMemory/1MB, 2)) GB</td></tr>
    </table>
    
    <h2>Disk Space</h2>
    <table>
        <tr><th>Drive</th><th>Size (GB)</th><th>Free (GB)</th><th>% Free</th></tr>
"@

foreach ($d in $disk) {
    $pctFree = [math]::Round(($d.FreeSpace / $d.Size) * 100, 2)
    $class = if ($pctFree -lt 10) {"critical"} elseif ($pctFree -lt 20) {"warning"} else {""}
    
    $html += @"
        <tr class="$class">
            <td>$($d.DeviceID)</td>
            <td>$([math]::Round($d.Size/1GB, 2))</td>
            <td>$([math]::Round($d.FreeSpace/1GB, 2))</td>
            <td>$pctFree%</td>
        </tr>
"@
}

$html += @"
    </table>
    
    <h2>Stopped Automatic Services ($($services.Count))</h2>
    <table>
        <tr><th>Service Name</th><th>Display Name</th><th>Status</th></tr>
"@

foreach ($svc in $services) {
    $html += "<tr class='warning'><td>$($svc.Name)</td><td>$($svc.DisplayName)</td><td>$($svc.Status)</td></tr>"
}

$html += @"
    </table>
</body>
</html>
"@

$html | Out-File $reportFile -Encoding UTF8
Write-Host "Report saved to: $reportFile" -ForegroundColor Green
Start-Process $reportFile
```

**Планиране с Task Scheduler:**
```powershell
# Създаване на scheduled task
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
    -Argument "-ExecutionPolicy Bypass -File C:\Scripts\SystemHealthReport.ps1"

$trigger = New-ScheduledTaskTrigger -Daily -At "08:00"

$principal = New-ScheduledTaskPrincipal -UserId "SYSTEM" -LogonType ServiceAccount

Register-ScheduledTask -TaskName "DailyHealthReport" `
    -Action $action -Trigger $trigger -Principal $principal `
    -Description "Generate daily system health report"
```

---

### **4. ЗАТВЪРЖДАВАНЕ (12 минути)**

**Самостоятелна задача:**

Създайте скрипт `Get-UserReport.ps1` който:
1. Приема параметър -Department
2. Намира всички AD потребители в този department
3. Генерира CSV отчет с: Name, Email, LastLogon, Enabled

```powershell
# Шаблон за начало
param(
    [string]$Department = "IT",
    [string]$OutputPath = "C:\Reports"
)

# Вашият код тук...
```

---

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови точки:**
```
✓ PowerShell = Cmdlets + Pipeline
✓ Variables: $name, @array, @{hashtable}
✓ Control: if/else, foreach, while
✓ Functions: param(), try/catch
✓ Automation: .ps1 скриптове
✓ Task Scheduler за планиране
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

```
1. Създайте скрипт за backup на важни папки

2. Добавете error handling и logging

3. Планирайте скрипта да се изпълнява седмично

Време: 45-60 минути
```

---

## 6. ОЦЕНЯВАНЕ

| Компонент | Точки | Процент |
|-----------|-------|---------|
| Functions и Parameters | 20 | 30% |
| Control Structures | 15 | 20% |
| Error Handling | 15 | 20% |
| Automation Script | 15 | 20% |
| Домашна работа | 5 | 10% |
| **ОБЩО** | **70** | **100%** |

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: POWERSHELL CHEAT SHEET

```powershell
# ══════════════════════════════════════════════════════════
#              POWERSHELL БЪРЗ СПРАВОЧНИК
# ══════════════════════════════════════════════════════════

# ОСНОВНИ CMDLETS
Get-Help <cmdlet> -Examples    # Помощ
Get-Command -Verb Get          # Търсене на cmdlets
Get-Member                     # Свойства и методи

# ФАЙЛОВЕ
Get-ChildItem                  # ls/dir
New-Item -ItemType File        # touch
Copy-Item                      # cp
Move-Item                      # mv
Remove-Item                    # rm
Get-Content                    # cat
Set-Content                    # echo >
Add-Content                    # echo >>

# ПРОЦЕСИ И УСЛУГИ
Get-Process
Stop-Process -Name "notepad"
Get-Service
Start-Service -Name "Spooler"
Stop-Service -Name "Spooler"

# ACTIVE DIRECTORY
Get-ADUser -Filter *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
New-ADUser
Set-ADUser
Remove-ADUser

# REMOTE
Enter-PSSession -ComputerName Server01
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Process }

# OPERATORS
-eq  # равно
-ne  # различно
-gt  # по-голямо
-lt  # по-малко
-like # wildcard match
-match # regex match
-and, -or, -not # логически

# ══════════════════════════════════════════════════════════
```

---

*Документът е създаден за учебната 2025/2026 година*
*Специалност: Икономическо информационно осигуряване (код 482021)*
