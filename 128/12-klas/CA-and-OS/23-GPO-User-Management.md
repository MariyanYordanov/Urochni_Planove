# УРОЧЕН ПЛАН №23
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
| **Тема на урока:** | Управление на потребители и групови политики в Windows Server |
| **Дата:** | ____________ |
| **Час:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Упражнение |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да усвоят управлението на потребители в Active Directory
2. Да разберат концепцията за групови политики (GPO)
3. Да научат създаването и прилагането на GPO
4. Да разберат наследяването и приоритета на политиките
5. Да могат да прилагат политики за сигурност

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на отговорност при управление на корпоративни акаунти
2. Развиване на разбиране за корпоративна сигурност
3. Изграждане на системен подход към администрацията
4. Насърчаване на добри практики в IT управлението

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за работа с Windows Server
2. Усъвършенстване на способността за планиране на политики
3. Формиране на troubleshooting умения
4. Развитие на документационни навици

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**Active Directory потребители и групи:**
- User accounts - атрибути и свойства
- Security groups vs Distribution groups
- Organizational Units (OU) структура
- ADUC (Active Directory Users and Computers)

**Group Policy:**
- Group Policy Objects (GPO)
- Локални vs Домейн политики
- GPMC (Group Policy Management Console)
- Наследяване и приоритет (LSDOU)

### ОСНОВНИ УМЕНИЯ:
- Създаване и управление на потребители в AD
- Създаване на организационни единици
- Конфигуриране на групови политики
- Прилагане на политики за сигурност

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Информационна сигурност** - политики за пароли, достъп
2. **Мрежови технологии** - домейн структура
3. **Бизнес администрация** - корпоративна йерархия
4. **Програмиране** - PowerShell скриптове

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Демонстрация с обяснение
2. Практическа работа в Windows Server
3. Лабораторни упражнения по сценарии
4. Самостоятелна работа с проверка
5. Групова дискусия на best practices

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Виртуални машини с Windows Server 2022
- Active Directory Domain Services
- Group Policy Management Console
- Проектор за демонстрация
- Работен лист (Приложение 2)

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Стартиране на Windows Server VM
- Проверка на Active Directory статуса

**Мотивиращ въпрос:**
"Как да наложим единни правила за 1000 компютъра без да конфигурираме всеки поотделно?"

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Преговор на Active Directory:**
```
Active Directory структура:
┌─────────────────────────────────────────────────────────────┐
│                        FOREST                                │
│  ┌───────────────────────────────────────────────────────┐  │
│  │                      DOMAIN                           │  │
│  │    company.local                                      │  │
│  │  ┌─────────────────────────────────────────────────┐  │  │
│  │  │              Organizational Units (OU)          │  │  │
│  │  │  ┌─────────┐  ┌─────────┐  ┌─────────┐         │  │  │
│  │  │  │   IT    │  │  Sales  │  │   HR    │         │  │  │
│  │  │  │ Users   │  │ Users   │  │ Users   │         │  │  │
│  │  │  │ Groups  │  │ Groups  │  │ Groups  │         │  │  │
│  │  │  │Computers│  │Computers│  │Computers│         │  │  │
│  │  │  └─────────┘  └─────────┘  └─────────┘         │  │  │
│  │  └─────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Въпроси за проверка:**
1. Какво е Organizational Unit (OU)?
2. Каква е разликата между Security и Distribution група?
3. Какво съдържа един User account?

---

### **3. НОВ МАТЕРИАЛ И ПРАКТИКА (55 минути)**

#### **Част 1: Управление на потребители в AD (18 минути)**

**Отваряне на Active Directory Users and Computers:**
```
Метод 1: Start → Administrative Tools → ADUC
Метод 2: dsa.msc
Метод 3: Server Manager → Tools → ADUC
```

**Практическа задача 1.1: Създаване на OU структура**

```powershell
# PowerShell метод за създаване на OU
# Отворете PowerShell като Administrator

# Създаване на главни OU
New-ADOrganizationalUnit -Name "Company" -Path "DC=company,DC=local"
New-ADOrganizationalUnit -Name "IT" -Path "OU=Company,DC=company,DC=local"
New-ADOrganizationalUnit -Name "Sales" -Path "OU=Company,DC=company,DC=local"
New-ADOrganizationalUnit -Name "HR" -Path "OU=Company,DC=company,DC=local"

# Създаване на под-OU за Users и Computers
$departments = @("IT", "Sales", "HR")
foreach ($dept in $departments) {
    New-ADOrganizationalUnit -Name "Users" -Path "OU=$dept,OU=Company,DC=company,DC=local"
    New-ADOrganizationalUnit -Name "Computers" -Path "OU=$dept,OU=Company,DC=company,DC=local"
    New-ADOrganizationalUnit -Name "Groups" -Path "OU=$dept,OU=Company,DC=company,DC=local"
}

# Проверка
Get-ADOrganizationalUnit -Filter * | Select-Object Name, DistinguishedName
```

**GUI метод:**
```
1. ADUC → Десен клик върху домейна
2. New → Organizational Unit
3. Име: Company
4. ☑ Protect container from accidental deletion
5. OK
6. Повторете за под-OU
```

**Практическа задача 1.2: Създаване на потребители**

```powershell
# Създаване на единичен потребител
New-ADUser -Name "Ivan Petrov" `
    -GivenName "Ivan" `
    -Surname "Petrov" `
    -SamAccountName "ipetrov" `
    -UserPrincipalName "ipetrov@company.local" `
    -Path "OU=Users,OU=IT,OU=Company,DC=company,DC=local" `
    -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
    -Enabled $true `
    -ChangePasswordAtLogon $true

# Масово създаване от CSV
# users.csv съдържание:
# FirstName,LastName,Department,Title
# Maria,Ivanova,Sales,Manager
# Georgi,Dimitrov,HR,Specialist

Import-Csv "C:\users.csv" | ForEach-Object {
    $username = ($_.FirstName.Substring(0,1) + $_.LastName).ToLower()
    New-ADUser -Name "$($_.FirstName) $($_.LastName)" `
        -GivenName $_.FirstName `
        -Surname $_.LastName `
        -SamAccountName $username `
        -UserPrincipalName "$username@company.local" `
        -Path "OU=Users,OU=$($_.Department),OU=Company,DC=company,DC=local" `
        -Title $_.Title `
        -Department $_.Department `
        -AccountPassword (ConvertTo-SecureString "Welcome2025!" -AsPlainText -Force) `
        -Enabled $true `
        -ChangePasswordAtLogon $true
}
```

**Практическа задача 1.3: Създаване на групи**

```powershell
# Създаване на Security група
New-ADGroup -Name "IT-Admins" `
    -GroupScope Global `
    -GroupCategory Security `
    -Path "OU=Groups,OU=IT,OU=Company,DC=company,DC=local" `
    -Description "IT Department Administrators"

New-ADGroup -Name "Sales-Team" `
    -GroupScope Global `
    -GroupCategory Security `
    -Path "OU=Groups,OU=Sales,OU=Company,DC=company,DC=local"

# Добавяне на членове
Add-ADGroupMember -Identity "IT-Admins" -Members "ipetrov"

# Проверка на членство
Get-ADGroupMember -Identity "IT-Admins"
```

---

#### **Част 2: Group Policy Objects (GPO) (22 минути)**

**Какво е Group Policy?**
```
┌─────────────────────────────────────────────────────────────┐
│                    GROUP POLICY                              │
├─────────────────────────────────────────────────────────────┤
│ Позволява централизирано управление на:                     │
│                                                              │
│ • Настройки за сигурност (пароли, заключване)               │
│ • Софтуерна инсталация                                       │
│ • Desktop настройки                                          │
│ • Scripts (startup, shutdown, logon, logoff)                │
│ • Folder redirection                                         │
│ • Административни шаблони                                    │
└─────────────────────────────────────────────────────────────┘

GPO се прилагат към:
├── Sites
├── Domains
└── Organizational Units (OU)

Ред на прилагане (LSDOU):
Local → Site → Domain → OU (parent) → OU (child)
```

**Отваряне на Group Policy Management Console:**
```
Метод 1: Start → Administrative Tools → GPMC
Метод 2: gpmc.msc
Метод 3: Server Manager → Tools → GPMC
```

**Практическа задача 2.1: Създаване на GPO за политика за пароли**

```
1. GPMC → Forest → Domains → company.local
2. Десен клик → Create a GPO in this domain
3. Име: "Password Policy"
4. Десен клик върху GPO → Edit

5. Computer Configuration → Policies → Windows Settings 
   → Security Settings → Account Policies → Password Policy

6. Настройки:
   ┌────────────────────────────────────┬────────────────┐
   │ Политика                          │ Стойност       │
   ├────────────────────────────────────┼────────────────┤
   │ Enforce password history           │ 24 passwords   │
   │ Maximum password age               │ 90 days        │
   │ Minimum password age               │ 1 day          │
   │ Minimum password length            │ 12 characters  │
   │ Password must meet complexity      │ Enabled        │
   └────────────────────────────────────┴────────────────┘

7. Затворете редактора
8. Десен клик върху домейна → Link an Existing GPO
9. Изберете "Password Policy"
```

**Практическа задача 2.2: GPO за Desktop настройки**

```
1. Създайте нов GPO: "IT Department Settings"

2. User Configuration → Policies → Administrative Templates
   → Desktop
   
3. Настройки:
   - Remove Recycle Bin icon from desktop: Enabled
   - Hide and disable all items on the desktop: Disabled

4. User Configuration → Policies → Administrative Templates
   → Control Panel
   
5. Prohibit access to Control Panel and PC settings: Enabled
   (за обикновени потребители)

6. Свържете GPO към OU=Users,OU=Sales
```

**Практическа задача 2.3: GPO за Drive Mapping**

```
1. Създайте GPO: "Drive Mappings"

2. User Configuration → Preferences → Windows Settings
   → Drive Maps

3. Десен клик → New → Mapped Drive
   - Action: Create
   - Location: \\server\shared
   - Drive Letter: S:
   - Label: Shared Drive
   - ☑ Reconnect

4. Item-level targeting (за филтриране):
   - Common tab → ☑ Item-level targeting → Targeting...
   - New Item → Security Group
   - Group: Sales-Team

5. Свържете към домейна
```

**Практическа задача 2.4: Логон скрипт**

```
1. Създайте GPO: "Logon Scripts"

2. User Configuration → Policies → Windows Settings 
   → Scripts (Logon/Logoff) → Logon

3. Add → Browse
   - Създайте скрипт logon.bat:
   
   @echo off
   net use S: \\server\shared /persistent:yes
   echo Welcome, %USERNAME%! > C:\Users\%USERNAME%\Desktop\welcome.txt

4. Копирайте скрипта в:
   \\company.local\SYSVOL\company.local\Policies\{GPO-GUID}\User\Scripts\Logon

5. Свържете GPO към желаната OU
```

---

#### **Част 3: Наследяване и филтриране (10 минути)**

**Ред на прилагане (LSDOU):**
```
┌─────────────────────────────────────────────────────────────┐
│               ПРИОРИТЕТ НА ГРУПОВИ ПОЛИТИКИ                 │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   1. LOCAL POLICY (най-нисък приоритет)                     │
│      ↓                                                       │
│   2. SITE POLICY                                             │
│      ↓                                                       │
│   3. DOMAIN POLICY                                           │
│      ↓                                                       │
│   4. OU POLICY (Parent OU)                                   │
│      ↓                                                       │
│   5. OU POLICY (Child OU) ← НАЙ-ВИСОК ПРИОРИТЕТ            │
│                                                              │
│ По-късно приложените политики презаписват по-ранните!       │
└─────────────────────────────────────────────────────────────┘
```

**Block Inheritance и Enforced:**
```
Block Inheritance (на OU):
- Блокира наследяването на политики от по-горни нива
- Десен клик на OU → Block Inheritance

Enforced (на GPO link):
- Принуждава политиката да се прилага въпреки Block Inheritance
- Десен клик на GPO link → Enforced

Приоритет: Enforced > Block Inheritance
```

**Security Filtering:**
```
По подразбиране: Authenticated Users

За ограничаване:
1. GPMC → Изберете GPO
2. Scope tab → Security Filtering
3. Remove "Authenticated Users"
4. Add конкретна група (например IT-Admins)

Само членовете на тази група ще получат политиката!
```

**WMI Filtering:**
```powershell
# Филтриране по характеристики на компютъра
# Пример: Само за Windows 11

1. GPMC → WMI Filters → New
2. Име: "Windows 11 Only"
3. Query:
   SELECT * FROM Win32_OperatingSystem 
   WHERE Version LIKE "10.0.22%" AND ProductType = "1"

4. Свържете WMI filter към GPO
```

---

#### **Част 4: Диагностика и Troubleshooting (5 минути)**

**Полезни команди:**
```cmd
:: Принудително обновяване на политиките
gpupdate /force

:: Показва приложените политики
gpresult /r

:: Детайлен HTML отчет
gpresult /h C:\gpresult.html

:: RSoP (Resultant Set of Policy)
rsop.msc
```

```powershell
# PowerShell команди
Get-GPO -All | Select-Object DisplayName, GpoStatus
Get-GPResultantSetOfPolicy -ReportType Html -Path "C:\rsop.html"
```

---

### **4. ЗАТВЪРЖДАВАНЕ (12 минути)**

**Практическа проверка:**

| Задача | Команда/Действие |
|--------|------------------|
| Списък на всички потребители в OU | `Get-ADUser -Filter * -SearchBase "OU=IT,..."` |
| Проверка на GPO връзки | GPMC → Domain → Linked GPOs |
| Обновяване на политики | `gpupdate /force` |
| Отчет за приложени политики | `gpresult /h report.html` |

**Въпроси за дискусия:**
1. Защо използваме OU вместо да слагаме всички потребители в една контейнер?
2. Каква е разликата между Computer и User Configuration?
3. Кога бихме използвали Block Inheritance?

---

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови концепции:**
```
AD ПОТРЕБИТЕЛИ:
├── Създават се в OU за лесно управление
├── Свойства: име, парола, членство в групи
└── PowerShell: New-ADUser, Get-ADUser

ГРУПОВИ ПОЛИТИКИ:
├── GPO = контейнер за настройки
├── Свързват се към Site/Domain/OU
├── LSDOU определя приоритета
└── Филтриране: Security, WMI

ДИАГНОСТИКА:
├── gpupdate /force
├── gpresult /r или /h
└── GPMC → Group Policy Results
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задание:**
```
1. Създайте следната структура в AD:
   Company
   ├── Finance
   │   ├── Users (3 потребители)
   │   ├── Computers
   │   └── Groups (Finance-Team)
   └── Marketing
       ├── Users (2 потребители)
       └── Groups (Marketing-Team)

2. Създайте GPO "Finance Restrictions":
   - Забранете достъп до Control Panel
   - Задайте тапет (wallpaper) за Finance

3. Създайте GPO "Drive Mapping":
   - Mapped drive F: към \\server\finance
   - Само за групата Finance-Team

4. Документирайте с команди и скрийншотове

Очаквано време: 45-60 минути
```

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Компонент | Точки | Процент |
|-----------|-------|---------|
| Създаване на OU и потребители | 15 | 25% |
| Създаване на групи | 10 | 15% |
| Конфигуриране на GPO | 25 | 45% |
| Домашна работа | 10 | 15% |
| **ОБЩО** | **60** | **100%** |

### ОЦЕНЪЧНА РУБРИКА:

| Критерий | Отличен (6) | Много добър (5) | Добър (4) | Среден (3) |
|----------|-------------|-----------------|-----------|------------|
| AD структура | Пълна и правилна | С минимални пропуски | Основна структура | Непълна |
| GPO конфигурация | Работещи политики | Малки проблеми | Частично работещи | Не работят |
| Разбиране | Обяснява наследяването | Разбира основите | Частично разбиране | Слабо |

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Мога ли да създам потребител и група в AD?
2. Разбирам ли как се прилагат GPO?
3. Мога ли да диагностицирам проблеми с политики?
4. Знам ли реда на прилагане LSDOU?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 85% от учениците създават AD обекти успешно
- [ ] 80% конфигурират работещи GPO
- [ ] 75% разбират наследяването на политики
- [ ] Учениците използват gpresult за диагностика

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: POWERSHELL КОМАНДИ ЗА AD

```powershell
# ═══════════════════════════════════════════════════════════
#           ACTIVE DIRECTORY POWERSHELL КОМАНДИ
# ═══════════════════════════════════════════════════════════

# ПОТРЕБИТЕЛИ
# ───────────
# Създаване
New-ADUser -Name "Име" -SamAccountName "username" -Enabled $true

# Търсене
Get-ADUser -Filter {Name -like "*Петров*"}
Get-ADUser -Identity "username" -Properties *

# Промяна
Set-ADUser -Identity "username" -Title "Manager"

# Изтриване
Remove-ADUser -Identity "username" -Confirm:$false

# Смяна на парола
Set-ADAccountPassword -Identity "username" -Reset `
    -NewPassword (ConvertTo-SecureString "NewPass123!" -AsPlainText -Force)

# ГРУПИ
# ─────
# Създаване
New-ADGroup -Name "GroupName" -GroupScope Global -GroupCategory Security

# Добавяне на член
Add-ADGroupMember -Identity "GroupName" -Members "user1","user2"

# Премахване на член
Remove-ADGroupMember -Identity "GroupName" -Members "user1"

# Членове на група
Get-ADGroupMember -Identity "GroupName"

# ORGANIZATIONAL UNITS
# ────────────────────
# Създаване
New-ADOrganizationalUnit -Name "OU-Name" -Path "DC=company,DC=local"

# Списък
Get-ADOrganizationalUnit -Filter *

# GROUP POLICY
# ────────────
# Списък на GPO
Get-GPO -All

# Създаване на GPO
New-GPO -Name "GPO Name"

# Свързване към OU
New-GPLink -Name "GPO Name" -Target "OU=Sales,DC=company,DC=local"

# Статус на GPO
Get-GPO -Name "GPO Name" | Select-Object DisplayName, GpoStatus

# ═══════════════════════════════════════════════════════════
```

---

### ПРИЛОЖЕНИЕ 2: РАБОТЕН ЛИСТ

```
╔══════════════════════════════════════════════════════════════╗
║     РАБОТЕН ЛИСТ: AD ПОТРЕБИТЕЛИ И ГРУПОВИ ПОЛИТИКИ         ║
╠══════════════════════════════════════════════════════════════╣
║ Име: _________________________ Клас: ______ Дата: _________ ║
╚══════════════════════════════════════════════════════════════╝

ЗАДАЧА 1: Създаване на AD структура (15 точки)

Създайте следните OU и обекти:

OU: Development
├── Users
│   ├── dev1 (Developer 1)
│   └── dev2 (Developer 2)
├── Computers
└── Groups
    └── Dev-Team (Security група)

PowerShell команди:
___________________________________________________________
___________________________________________________________
___________________________________________________________
___________________________________________________________

───────────────────────────────────────────────────────────

ЗАДАЧА 2: Group Policy (25 точки)

2.1. Създайте GPO "Security Settings" с:
     - Минимална дължина на парола: 10 символа
     - Максимална възраст на парола: 60 дни
     
     Път до настройката:
     _____________________________________________________

2.2. Създайте GPO "Desktop Lock" с:
     - Screen saver timeout: 10 минути
     - Password protected screen saver: Enabled
     
     Път до настройката:
     _____________________________________________________

2.3. Как да приложите GPO само за групата Dev-Team?
     _____________________________________________________
     _____________________________________________________

───────────────────────────────────────────────────────────

ЗАДАЧА 3: Диагностика (10 точки)

3.1. Команда за обновяване на политики:
     _____________________________________________________

3.2. Команда за HTML отчет на приложени политики:
     _____________________________________________________

3.3. Какво означава LSDOU?
     L: ___________________________________________________
     S: ___________________________________________________
     D: ___________________________________________________
     OU: __________________________________________________

═══════════════════════════════════════════════════════════════
                        ОЦЕНКА: _______
═══════════════════════════════════════════════════════════════
```

---

### ПРИЛОЖЕНИЕ 3: GPO BEST PRACTICES

```
╔══════════════════════════════════════════════════════════════╗
║              ГРУПОВИ ПОЛИТИКИ - ДОБРИ ПРАКТИКИ              ║
╚══════════════════════════════════════════════════════════════╝

ИМЕНУВАНЕ:
──────────
✓ Използвайте описателни имена
✓ Включете целта: "Security-PasswordPolicy"
✓ Избягвайте: "GPO1", "Test", "New Policy"

ОРГАНИЗАЦИЯ:
────────────
✓ Една GPO за една цел (Single Purpose)
✓ Не смесвайте Computer и User настройки
✓ Документирайте всяка политика

ТЕСТВАНЕ:
─────────
✓ Тествайте в отделна OU преди production
✓ Използвайте gpresult за верификация
✓ Планирайте rollback стратегия

ПРОИЗВОДИТЕЛНОСТ:
─────────────────
✓ Минимизирайте броя на GPO
✓ Деактивирайте неизползваната част (Computer/User)
✓ Избягвайте WMI филтри когато е възможно

СИГУРНОСТ:
──────────
✓ Ограничете кой може да редактира GPO
✓ Използвайте Security Filtering
✓ Редовно преглеждайте политиките

═══════════════════════════════════════════════════════════════
```

---

*Документът е създаден за учебната 2025/2026 година*
*Съответства на изискванията на МОН за професионална подготовка*
*Специалност: Икономическо информационно осигуряване (код 482021)*
