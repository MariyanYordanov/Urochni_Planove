# УРОЧЕН ПЛАН №28
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
| **Тема на урока:** | Проект: Изграждане на корпоративна среда |
| **Дата:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Проект |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да приложат интегрирано знанията от целия курс
2. Да изградят пълна корпоративна IT инфраструктура
3. Да конфигурират взаимосвързани Windows Server услуги
4. Да документират техническа инфраструктура
5. Да представят и защитят проекта си

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на екипна работа и комуникация
2. Развиване на отговорност за краен продукт
3. Изграждане на професионални презентационни умения
4. Насърчаване на творчески подход към проблемите

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за планиране на проекти
2. Усъвършенстване на интеграционни умения
3. Формиране на способност за самостоятелна работа
4. Развитие на критично мислене и самооценка

---

## 3. СЪДЪРЖАНИЕ

### ПРОЕКТНО ЗАДАНИЕ:

**Сценарий:**
```
Компания "TechStart БГ" е стартъп с 50 служители.
Вашата задача е да изградите IT инфраструктурата на компанията.

Изисквания:
• Централизирано управление на потребители
• Файлов сървър с различни нива на достъп
• Уеб сървър за вътрешен портал
• Автоматично IP конфигуриране
• Backup стратегия
• Документация на инфраструктурата
```

### КОМПОНЕНТИ НА ПРОЕКТА:

| Компонент | Услуги | Точки |
|-----------|--------|-------|
| Domain Controller | AD DS, DNS | 20 |
| Network Services | DHCP, DNS records | 15 |
| File Server | Shares, Permissions | 15 |
| Web Server | IIS, Internal site | 15 |
| Automation | PowerShell scripts | 15 |
| Documentation | Diagram, procedures | 20 |

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Всички предходни теми** - интеграция на знания
2. **Проектен мениджмънт** - планиране и изпълнение
3. **Техническо чертане** - мрежови диаграми
4. **Комуникативни умения** - документация и презентация

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Проектно-базирано обучение
2. Самостоятелна/екипна работа
3. Консултации и насоки от учителя
4. Peer review между екипи
5. Финална презентация

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Windows Server 2022 VM (минимум 2)
- Windows 11 клиентски VM
- Виртуална мрежа
- Проектна документация шаблон
- Оценъчна рубрика

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Представяне на проектното задание
- Формиране на екипи (2-3 ученика)

**Разпределение на времето:**
```
Урок 28 (днес): Планиране и начало на изпълнение
• 5 мин - Въведение
• 10 мин - Преглед на заданието
• 60 мин - Работа по проекта
• 15 мин - Checkpoint и въпроси

(Проектът може да продължи като домашна работа)
```

---

### **2. ПРЕГЛЕД НА ЗАДАНИЕТО (10 минути)**

#### **Архитектура на решението:**

```
                    ┌─────────────────────────────────────┐
                    │         INTERNET                     │
                    └─────────────────┬───────────────────┘
                                      │
                              ┌───────▼───────┐
                              │    Router     │
                              │ 192.168.1.1   │
                              └───────┬───────┘
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        │                             │          CORPORATE LAN      │
        │                             │          192.168.1.0/24     │
        │     ┌───────────────────────┼───────────────────────┐     │
        │     │                       │                       │     │
        │     ▼                       ▼                       ▼     │
┌───────────────────┐   ┌───────────────────┐   ┌───────────────────┐
│   DC01 (Primary)  │   │    FILE01         │   │     WEB01         │
│ ─────────────────│   │ ─────────────────│   │ ─────────────────│
│ • AD DS           │   │ • File Server     │   │ • IIS             │
│ • DNS             │   │ • DFS (optional)  │   │ • Internal Portal │
│ • DHCP            │   │ • Shared Folders  │   │                   │
│ ─────────────────│   │ ─────────────────│   │ ─────────────────│
│ IP: 192.168.1.10  │   │ IP: 192.168.1.20  │   │ IP: 192.168.1.30  │
└───────────────────┘   └───────────────────┘   └───────────────────┘
        │                       │                       │
        └───────────────────────┼───────────────────────┘
                                │
                    ┌───────────▼───────────┐
                    │     CLIENT01          │
                    │   (Windows 11)        │
                    │   DHCP Client         │
                    │   Domain Joined       │
                    └───────────────────────┘
```

#### **Чеклист за изпълнение:**

```
ФАЗА 1: Domain Controller (DC01)
□ Инсталиране на Windows Server 2022
□ Задаване на static IP: 192.168.1.10
□ Инсталиране на AD DS роля
□ Промоция на Domain Controller (techstart.local)
□ Инсталиране на DNS роля
□ Инсталиране на DHCP роля
□ Конфигуриране на DHCP scope

ФАЗА 2: Organizational Structure
□ Създаване на OU структура:
  └─ techstart.local
     ├─ OU=Departments
     │  ├─ OU=IT
     │  ├─ OU=Sales
     │  └─ OU=Management
     ├─ OU=Servers
     └─ OU=Workstations
□ Създаване на security groups
□ Създаване на потребители (минимум 5)

ФАЗА 3: File Server (FILE01)
□ Инсталиране на Windows Server
□ Join to domain
□ Създаване на споделени папки:
  └─ D:\Shares
     ├─ Company (всички - Read)
     ├─ IT (IT group - Full)
     ├─ Sales (Sales group - Modify)
     └─ Management (Mgmt - Full, Others - No access)
□ NTFS и Share permissions

ФАЗА 4: Web Server (WEB01)
□ Инсталиране на Windows Server
□ Join to domain
□ Инсталиране на IIS
□ Създаване на intranet сайт
□ DNS запис: intranet.techstart.local

ФАЗА 5: Client Configuration
□ Windows 11 VM
□ Join to domain
□ Тест на DHCP
□ Тест на file shares
□ Тест на intranet

ФАЗА 6: Documentation
□ Мрежова диаграма
□ IP адресна схема
□ Списък на потребители/групи
□ Процедури за backup
□ Troubleshooting guide
```

---

### **3. РАБОТА ПО ПРОЕКТА (60 минути)**

#### **Стъпка 1: Domain Controller Setup (20 минути)**

```powershell
# На DC01 - след инсталация на Windows Server

# 1. Задаване на hostname
Rename-Computer -NewName "DC01" -Restart

# 2. Конфигуриране на static IP
New-NetIPAddress -InterfaceAlias "Ethernet" `
    -IPAddress 192.168.1.10 `
    -PrefixLength 24 `
    -DefaultGateway 192.168.1.1

Set-DnsClientServerAddress -InterfaceAlias "Ethernet" `
    -ServerAddresses 127.0.0.1,8.8.8.8

# 3. Инсталиране на AD DS
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

# 4. Промоция на DC
Install-ADDSForest `
    -DomainName "techstart.local" `
    -DomainNetbiosName "TECHSTART" `
    -InstallDns:$true `
    -SafeModeAdministratorPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
    -Force

# 5. След рестарт - DHCP
Install-WindowsFeature DHCP -IncludeManagementTools
Add-DhcpServerInDC -DnsName "dc01.techstart.local" -IPAddress 192.168.1.10

Add-DhcpServerv4Scope -Name "Corporate LAN" `
    -StartRange 192.168.1.100 -EndRange 192.168.1.200 `
    -SubnetMask 255.255.255.0 -State Active

Set-DhcpServerv4OptionValue -ScopeId 192.168.1.0 `
    -Router 192.168.1.1 `
    -DnsServer 192.168.1.10 `
    -DnsDomain "techstart.local"
```

#### **Стъпка 2: AD Structure (15 минути)**

```powershell
# Създаване на OU структура
$OUs = @(
    "OU=Departments,DC=techstart,DC=local",
    "OU=IT,OU=Departments,DC=techstart,DC=local",
    "OU=Sales,OU=Departments,DC=techstart,DC=local",
    "OU=Management,OU=Departments,DC=techstart,DC=local",
    "OU=Servers,DC=techstart,DC=local",
    "OU=Workstations,DC=techstart,DC=local"
)

foreach ($ou in $OUs) {
    $name = ($ou -split ",")[0] -replace "OU=",""
    $path = ($ou -split ",",2)[1]
    New-ADOrganizationalUnit -Name $name -Path $path
}

# Създаване на групи
New-ADGroup -Name "IT-Team" -GroupScope Global -Path "OU=IT,OU=Departments,DC=techstart,DC=local"
New-ADGroup -Name "Sales-Team" -GroupScope Global -Path "OU=Sales,OU=Departments,DC=techstart,DC=local"
New-ADGroup -Name "Managers" -GroupScope Global -Path "OU=Management,OU=Departments,DC=techstart,DC=local"

# Създаване на потребители
$users = @(
    @{First="Ivan";Last="Petrov";Dept="IT";Group="IT-Team"},
    @{First="Maria";Last="Ivanova";Dept="IT";Group="IT-Team"},
    @{First="Georgi";Last="Dimitrov";Dept="Sales";Group="Sales-Team"},
    @{First="Elena";Last="Todorova";Dept="Sales";Group="Sales-Team"},
    @{First="Petar";Last="Georgiev";Dept="Management";Group="Managers"}
)

foreach ($user in $users) {
    $sam = "$($user.First.Substring(0,1).ToLower())$($user.Last.ToLower())"
    $upn = "$sam@techstart.local"
    $ou = "OU=$($user.Dept),OU=Departments,DC=techstart,DC=local"
    
    New-ADUser -Name "$($user.First) $($user.Last)" `
        -GivenName $user.First -Surname $user.Last `
        -SamAccountName $sam -UserPrincipalName $upn `
        -Path $ou -Department $user.Dept `
        -AccountPassword (ConvertTo-SecureString "Welcome2025!" -AsPlainText -Force) `
        -Enabled $true -ChangePasswordAtLogon $true
    
    Add-ADGroupMember -Identity $user.Group -Members $sam
}
```

#### **Стъпка 3: File Server (15 минути)**

```powershell
# На FILE01 - след join to domain

# Създаване на структура
New-Item -Path "D:\Shares" -ItemType Directory
New-Item -Path "D:\Shares\Company" -ItemType Directory
New-Item -Path "D:\Shares\IT" -ItemType Directory
New-Item -Path "D:\Shares\Sales" -ItemType Directory
New-Item -Path "D:\Shares\Management" -ItemType Directory

# Company - всички могат да четат
New-SmbShare -Name "Company" -Path "D:\Shares\Company" `
    -FullAccess "TECHSTART\Domain Admins" `
    -ReadAccess "TECHSTART\Domain Users"

# IT - само IT team
New-SmbShare -Name "IT" -Path "D:\Shares\IT" `
    -FullAccess "TECHSTART\IT-Team","TECHSTART\Domain Admins" `
    -NoAccess "Everyone"

# Sales - Sales team modify
New-SmbShare -Name "Sales" -Path "D:\Shares\Sales" `
    -FullAccess "TECHSTART\Domain Admins" `
    -ChangeAccess "TECHSTART\Sales-Team" `
    -ReadAccess "TECHSTART\Managers"

# Management - само мениджъри
New-SmbShare -Name "Management" -Path "D:\Shares\Management" `
    -FullAccess "TECHSTART\Managers","TECHSTART\Domain Admins" `
    -NoAccess "Everyone"

# DNS запис
Add-DnsServerResourceRecordA -ZoneName "techstart.local" `
    -Name "files" -IPv4Address "192.168.1.20"
```

#### **Стъпка 4: Web Server (10 минути)**

```powershell
# На WEB01

# Инсталиране на IIS
Install-WindowsFeature Web-Server -IncludeManagementTools

# Създаване на intranet сайт
New-Item -Path "C:\inetpub\intranet" -ItemType Directory

$html = @"
<!DOCTYPE html>
<html>
<head>
    <title>TechStart BG - Intranet</title>
    <style>
        body { font-family: Arial; margin: 0; padding: 0; }
        .header { background: #0066cc; color: white; padding: 20px; text-align: center; }
        .nav { background: #333; padding: 10px; }
        .nav a { color: white; margin: 0 15px; text-decoration: none; }
        .content { padding: 20px; }
        .footer { background: #333; color: white; text-align: center; padding: 10px; position: fixed; bottom: 0; width: 100%; }
    </style>
</head>
<body>
    <div class="header">
        <h1>TechStart BG - Вътрешен портал</h1>
    </div>
    <div class="nav">
        <a href="#">Начало</a>
        <a href="\\\\files.techstart.local\\Company">Файлове</a>
        <a href="#">Контакти</a>
        <a href="#">IT Support</a>
    </div>
    <div class="content">
        <h2>Добре дошли!</h2>
        <p>Това е вътрешният портал на TechStart BG.</p>
        <h3>Бързи връзки:</h3>
        <ul>
            <li><a href="\\\\files\\Company">Споделени документи</a></li>
            <li><a href="mailto:it@techstart.local">IT Support</a></li>
        </ul>
    </div>
    <div class="footer">
        &copy; 2025 TechStart BG - Internal Use Only
    </div>
</body>
</html>
"@

$html | Out-File "C:\inetpub\intranet\index.html" -Encoding UTF8

# Създаване на IIS сайт
Import-Module WebAdministration
New-Website -Name "Intranet" -PhysicalPath "C:\inetpub\intranet" `
    -Port 80 -HostHeader "intranet.techstart.local"

# DNS запис (на DC01)
Add-DnsServerResourceRecordA -ZoneName "techstart.local" `
    -Name "intranet" -IPv4Address "192.168.1.30"
```

---

### **4. CHECKPOINT И ВЪПРОСИ (15 минути)**

**Проверка на напредъка:**

| Екип | DC01 | AD Structure | FILE01 | WEB01 | Client |
|------|------|--------------|--------|-------|--------|
| 1 | □ | □ | □ | □ | □ |
| 2 | □ | □ | □ | □ | □ |
| 3 | □ | □ | □ | □ | □ |

**Въпроси за обсъждане:**
1. Какви проблеми срещнахте?
2. Какво би подобрило инфраструктурата?
3. Какво липсва за production среда?

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Компонент | Точки | Описание |
|-----------|-------|----------|
| Domain Controller | 20 | AD, DNS, DHCP работят |
| AD Structure | 15 | OUs, Groups, Users |
| File Server | 15 | Shares с правилни permissions |
| Web Server | 15 | IIS сайт достъпен |
| Automation | 15 | PowerShell скриптове |
| Documentation | 20 | Диаграма, процедури |
| **ОБЩО** | **100** | |

### ОЦЕНЪЧНА СКАЛА:

| Точки | Оценка |
|-------|--------|
| 90-100 | Отличен 6 |
| 75-89 | Много добър 5 |
| 60-74 | Добър 4 |
| 50-59 | Среден 3 |
| 0-49 | Слаб 2 |

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: ШАБЛОН ЗА ДОКУМЕНТАЦИЯ

```
╔════════════════════════════════════════════════════════════╗
║      ПРОЕКТНА ДОКУМЕНТАЦИЯ: TECHSTART BG INFRASTRUCTURE   ║
╠════════════════════════════════════════════════════════════╣
║ Екип: _________________________ Дата: ___________________ ║
║ Членове: ________________________________________________ ║
╚════════════════════════════════════════════════════════════╝

1. МРЕЖОВА ДИАГРАМА
   (Прикачете диаграма)

2. IP АДРЕСНА СХЕМА
   | Устройство | IP адрес | Роля |
   |------------|----------|------|
   | DC01       |          |      |
   | FILE01     |          |      |
   | WEB01      |          |      |
   | DHCP Range |          |      |

3. ПОТРЕБИТЕЛИ И ГРУПИ
   | Потребител | Група | Department |
   |------------|-------|------------|
   |            |       |            |

4. СПОДЕЛЕНИ ПАПКИ
   | Папка | Път | Permissions |
   |-------|-----|-------------|
   |       |     |             |

5. BACKUP ПЛАН
   RPO: _____________ RTO: _____________
   Schedule: _____________________________
   Destination: __________________________

6. TROUBLESHOOTING GUIDE
   Проблем 1: _____________________________
   Решение: _______________________________
   
   Проблем 2: _____________________________
   Решение: _______________________________

═══════════════════════════════════════════════════════════
```

### ПРИЛОЖЕНИЕ 2: ТЕСТОВИ СЦЕНАРИИ

```powershell
# ══════════════════════════════════════════════════════════
#              ТЕСТОВИ СКРИПТ ЗА ПРОЕКТА
# ══════════════════════════════════════════════════════════

# Тест 1: DNS Resolution
Resolve-DnsName "dc01.techstart.local"
Resolve-DnsName "files.techstart.local"
Resolve-DnsName "intranet.techstart.local"

# Тест 2: AD Connectivity
Get-ADDomain
Get-ADUser -Filter * | Select-Object Name, Department

# Тест 3: DHCP
Get-DhcpServerv4Scope
Get-DhcpServerv4Lease -ScopeId 192.168.1.0

# Тест 4: File Shares
Test-Path "\\files.techstart.local\Company"
Get-SmbShare

# Тест 5: Web Server
Invoke-WebRequest "http://intranet.techstart.local" -UseBasicParsing

Write-Host "All tests completed!" -ForegroundColor Green

# ══════════════════════════════════════════════════════════
```

---

*Документът е създаден за учебната 2025/2026 година*
*Специалност: Икономическо информационно осигуряване (код 482021)*
