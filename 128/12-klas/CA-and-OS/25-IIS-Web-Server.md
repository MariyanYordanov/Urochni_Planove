# УРОЧЕН ПЛАН №25
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
| **Тема на урока:** | IIS Web Server - инсталация и управление |
| **Дата:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Упражнение |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат архитектурата на IIS
2. Да инсталират и конфигурират IIS Web Server
3. Да създават и управляват уеб сайтове
4. Да конфигурират SSL/TLS сертификати
5. Да управляват application pools

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на разбиране за уеб инфраструктура
2. Развиване на внимание към сигурността
3. Изграждане на професионален подход
4. Насърчаване на документиране на конфигурации

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на практически умения за уеб администрация
2. Усъвършенстване на troubleshooting умения
3. Формиране на способност за оптимизация
4. Развитие на умения за работа с GUI и CLI

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**IIS архитектура:**
- Internet Information Services компоненти
- Application Pools и Worker Processes
- Sites, Applications, Virtual Directories
- Bindings (HTTP, HTTPS, ports)
- Modules и Handlers

**Основни функции:**
- Хостване на статично съдържание
- ASP.NET приложения
- PHP поддръжка
- SSL/TLS конфигурация
- Logging и мониторинг

### ОСНОВНИ УМЕНИЯ:
- Инсталиране на IIS роля
- Създаване на уеб сайтове
- Конфигуриране на bindings
- Настройка на SSL сертификати
- Управление на application pools

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Уеб програмиране** - HTML, ASP.NET
2. **Мрежови технологии** - HTTP/HTTPS протоколи
3. **Информационна сигурност** - SSL/TLS, сертификати
4. **Бази данни** - свързване с SQL Server

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Демонстрация на инсталация и конфигурация
2. Практическа работа стъпка по стъпка
3. Лабораторни упражнения
4. Самостоятелни задачи
5. Troubleshooting сценарии

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Windows Server 2022 VM
- IIS Manager конзола
- Примерни HTML файлове
- PowerShell скриптове (Приложение 2)
- Работни листове

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Стартиране на лабораторната среда
- Представяне на целите

**Мотивация:**
"IIS е уеб сървърът на Microsoft, който захранва милиони уебсайтове по света. Той е втори по пазарен дял след Nginx."

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Преговор:**
```
Въпроси:
1. Какво е уеб сървър?
2. Кои са основните HTTP методи?
3. Каква е разликата между HTTP и HTTPS?
4. Спомняте ли си Apache/Nginx от Linux?
```

**IIS vs Apache/Nginx:**

| Характеристика | IIS | Apache | Nginx |
|----------------|-----|--------|-------|
| Платформа | Windows | Cross-platform | Cross-platform |
| Конфигурация | GUI + XML | Text files | Text files |
| ASP.NET | Native | Чрез Mono | Reverse proxy |
| Лиценз | Windows Server | Open-source | Open-source |

---

### **3. НОВ МАТЕРИАЛ И ПРАКТИКА (55 минути)**

#### **Част 1: Инсталиране на IIS (10 минути)**

**PowerShell метод:**
```powershell
# Инсталиране на IIS с основни функции
Install-WindowsFeature -Name Web-Server -IncludeManagementTools

# Инсталиране на допълнителни модули
Install-WindowsFeature -Name Web-Asp-Net45, Web-Http-Logging, `
    Web-Request-Monitor, Web-Mgmt-Console, Web-Scripting-Tools

# Проверка на инсталацията
Get-WindowsFeature Web-*

# Стартиране на IIS Manager
Start-Process "inetmgr"
```

**GUI метод:**
```
Server Manager → Add Roles and Features
→ Web Server (IIS) → Select features → Install
```

**Тест на инсталацията:**
```
Отворете браузър → http://localhost
Трябва да видите: IIS Welcome Page
```

---

#### **Част 2: Архитектура на IIS (10 минути)**

**IIS компоненти:**
```
┌─────────────────────────────────────────────────────────────┐
│                         IIS Server                          │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Site 1    │  │   Site 2    │  │   Site 3    │         │
│  │  (Port 80)  │  │  (Port 81)  │  │  (Port 443) │         │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘         │
│         │                │                │                 │
│  ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐         │
│  │ Application │  │ Application │  │ Application │         │
│  │   Pool 1    │  │   Pool 2    │  │   Pool 1    │         │
│  │ (w3wp.exe)  │  │ (w3wp.exe)  │  │ (w3wp.exe)  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
├─────────────────────────────────────────────────────────────┤
│                     HTTP.sys (Kernel)                       │
└─────────────────────────────────────────────────────────────┘
```

**Ключови понятия:**

| Компонент | Описание |
|-----------|----------|
| Site | Уеб сайт с уникален binding |
| Application | Част от сайт с отделна конфигурация |
| Virtual Directory | Alias към физическа папка |
| Application Pool | Изолирана среда за изпълнение |
| Binding | IP:Port:Hostname комбинация |

---

#### **Част 3: Създаване на уеб сайт (15 минути)**

**Практическа задача 3.1: Подготовка на съдържание**

```powershell
# Създаване на директория за сайта
New-Item -Path "C:\WebSites\MyFirstSite" -ItemType Directory

# Създаване на index.html
@"
<!DOCTYPE html>
<html>
<head>
    <title>My First IIS Site</title>
    <style>
        body { font-family: Arial; text-align: center; margin-top: 50px; }
        h1 { color: #0066cc; }
    </style>
</head>
<body>
    <h1>Welcome to My First IIS Website!</h1>
    <p>Server: $env:COMPUTERNAME</p>
    <p>Time: $(Get-Date)</p>
</body>
</html>
"@ | Out-File -FilePath "C:\WebSites\MyFirstSite\index.html" -Encoding UTF8
```

**Практическа задача 3.2: Създаване на сайт (GUI)**

```
IIS Manager → Sites → Add Website

Name: MyFirstSite
Physical path: C:\WebSites\MyFirstSite
Binding:
  Type: http
  IP address: All Unassigned
  Port: 8080
  Host name: (празно)

→ OK
```

**Практическа задача 3.3: Създаване на сайт (PowerShell)**

```powershell
# Импортиране на IIS модула
Import-Module WebAdministration

# Създаване на Application Pool
New-WebAppPool -Name "MyFirstSitePool"
Set-ItemProperty -Path "IIS:\AppPools\MyFirstSitePool" -Name "managedRuntimeVersion" -Value "v4.0"

# Създаване на сайта
New-Website -Name "MyFirstSite" `
    -PhysicalPath "C:\WebSites\MyFirstSite" `
    -Port 8080 `
    -ApplicationPool "MyFirstSitePool"

# Стартиране на сайта
Start-Website -Name "MyFirstSite"

# Проверка
Get-Website
```

**Тест:**
```
Браузър → http://localhost:8080
```

---

#### **Част 4: Host Headers и множество сайтове (10 минути)**

**Практическа задача 4.1: Конфигуриране на host headers**

```powershell
# Създаване на втори сайт
New-Item -Path "C:\WebSites\SecondSite" -ItemType Directory
"<h1>Second Site</h1>" | Out-File "C:\WebSites\SecondSite\index.html"

# Създаване с host header
New-Website -Name "SecondSite" `
    -PhysicalPath "C:\WebSites\SecondSite" `
    -Port 80 `
    -HostHeader "secondsite.local"

# Добавяне на binding към съществуващ сайт
New-WebBinding -Name "MyFirstSite" `
    -Protocol "http" `
    -Port 80 `
    -HostHeader "myfirstsite.local"

# Конфигуриране на hosts файла за тестване
Add-Content -Path "C:\Windows\System32\drivers\etc\hosts" `
    -Value "127.0.0.1 myfirstsite.local"
Add-Content -Path "C:\Windows\System32\drivers\etc\hosts" `
    -Value "127.0.0.1 secondsite.local"
```

**Binding визуализация:**
```
IIS Server (един IP адрес)
├── Port 80 + Host: myfirstsite.local → MyFirstSite
├── Port 80 + Host: secondsite.local  → SecondSite
└── Port 8080 (без host header)       → MyFirstSite
```

---

#### **Част 5: SSL/HTTPS конфигурация (10 минути)**

**Практическа задача 5.1: Self-signed сертификат**

```powershell
# Създаване на self-signed сертификат
$cert = New-SelfSignedCertificate `
    -DnsName "myfirstsite.local", "localhost" `
    -CertStoreLocation "Cert:\LocalMachine\My" `
    -NotAfter (Get-Date).AddYears(1)

# Преглед на сертификата
$cert | Format-List

# Добавяне на HTTPS binding
New-WebBinding -Name "MyFirstSite" `
    -Protocol "https" `
    -Port 443 `
    -HostHeader "myfirstsite.local" `
    -SslFlags 1

# Свързване на сертификата с binding
$binding = Get-WebBinding -Name "MyFirstSite" -Protocol "https"
$binding.AddSslCertificate($cert.Thumbprint, "My")
```

**GUI метод:**
```
IIS Manager → Server → Server Certificates
→ Create Self-Signed Certificate

После:
Sites → MyFirstSite → Bindings → Add
Type: https
SSL certificate: избор на сертификата
```

---

### **4. ЗАТВЪРЖДАВАНЕ (12 минути)**

**Самостоятелни задачи:**

| № | Задача |
|---|--------|
| 1 | Създайте нов сайт "CompanySite" на порт 9090 |
| 2 | Добавете host header "company.local" на порт 80 |
| 3 | Създайте custom index.html с вашето име |
| 4 | Конфигурирайте SSL за сайта |

**Въпроси:**
1. Каква е разликата между Site и Application Pool?
2. Защо използваме host headers?
3. Как IIS различава заявките към различни сайтове на порт 80?

---

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови точки:**
```
✓ IIS е Windows уеб сървър
✓ Application Pools изолират приложения
✓ Bindings = IP:Port:HostHeader
✓ Host headers позволяват множество сайтове
✓ HTTPS изисква SSL сертификат
✓ PowerShell за автоматизация
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

```
1. Създайте трети сайт с PHP поддръжка:
   - Инсталирайте PHP за IIS
   - Създайте phpinfo.php файл

2. Документирайте конфигурацията на всички сайтове

3. Отговорете: Как се конфигурира IIS URL Rewrite?

Време: 40-50 минути
```

---

## 6. ОЦЕНЯВАНЕ

| Компонент | Точки | Процент |
|-----------|-------|---------|
| Инсталация на IIS | 10 | 15% |
| Създаване на сайт | 20 | 30% |
| Host headers конфигурация | 15 | 20% |
| SSL конфигурация | 15 | 20% |
| Домашна работа | 10 | 15% |
| **ОБЩО** | **70** | **100%** |

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Мога ли да създам IIS сайт самостоятелно?
2. Разбирам ли application pools?
3. Мога ли да конфигурирам HTTPS?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 90% инсталират IIS успешно
- [ ] 85% създават работещ сайт
- [ ] 75% конфигурират SSL

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: РАБОТЕН ЛИСТ

```
╔════════════════════════════════════════════════════════════╗
║              РАБОТЕН ЛИСТ: IIS WEB SERVER                 ║
╠════════════════════════════════════════════════════════════╣
║ Име: _______________________ Клас: ______ Дата: _________ ║
╚════════════════════════════════════════════════════════════╝

СЪЗДАДЕНИ САЙТОВЕ:

| Site Name | Physical Path | Port | Host Header | App Pool |
|-----------|---------------|------|-------------|----------|
|           |               |      |             |          |
|           |               |      |             |          |
|           |               |      |             |          |

SSL СЕРТИФИКАТ:
Thumbprint: _______________________________________________
Валиден до: _______________________________________________

ТЕСТОВЕ:
http://localhost:8080  - работи: [ ] Да [ ] Не
https://localhost:443  - работи: [ ] Да [ ] Не

═══════════════════════════════════════════════════════════
```

### ПРИЛОЖЕНИЕ 2: IIS POWERSHELL КОМАНДИ

```powershell
# ══════════════════════════════════════════════════════════
#              IIS POWERSHELL СПРАВОЧНИК
# ══════════════════════════════════════════════════════════

Import-Module WebAdministration

# САЙТОВЕ
Get-Website
New-Website -Name "Site" -PhysicalPath "C:\path" -Port 80
Start-Website -Name "Site"
Stop-Website -Name "Site"
Remove-Website -Name "Site"

# APPLICATION POOLS
Get-WebAppPool
New-WebAppPool -Name "Pool"
Start-WebAppPool -Name "Pool"
Stop-WebAppPool -Name "Pool"
Remove-WebAppPool -Name "Pool"

# BINDINGS
Get-WebBinding -Name "Site"
New-WebBinding -Name "Site" -Protocol "http" -Port 80 -HostHeader "host"
Remove-WebBinding -Name "Site" -Protocol "http" -Port 80

# SSL
New-SelfSignedCertificate -DnsName "domain" -CertStoreLocation "Cert:\LocalMachine\My"
Get-ChildItem Cert:\LocalMachine\My

# ══════════════════════════════════════════════════════════
```

---

*Документът е създаден за учебната 2025/2026 година*
*Специалност: Икономическо информационно осигуряване (код 482021)*
