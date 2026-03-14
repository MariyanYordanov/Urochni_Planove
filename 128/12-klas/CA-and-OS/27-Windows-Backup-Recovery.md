# УРОЧЕН ПЛАН №27
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
| **Тема на урока:** | Windows Server Backup и възстановяване |
| **Дата:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Комбиниран |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат стратегиите за backup (3-2-1 правило)
2. Да инсталират и конфигурират Windows Server Backup
3. Да създават backup планове (пълен, инкрементален, диференциален)
4. Да възстановяват данни от backup
5. Да разбират System State и Bare Metal Recovery

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на отговорност към защита на данни
2. Развиване на предвидливост и планиране
3. Изграждане на систематичен подход към disaster recovery
4. Насърчаване на документиране на процедури

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за планиране на инфраструктура
2. Усъвършенстване на troubleshooting умения
3. Формиране на способност за оценка на рискове
4. Развитие на критично мислене

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**Backup стратегии:**
- 3-2-1 правило (3 копия, 2 медии, 1 offsite)
- Типове backup: Full, Incremental, Differential
- RPO (Recovery Point Objective)
- RTO (Recovery Time Objective)

**Windows Server Backup:**
- Инсталация на feature
- Backup destinations
- Scheduled backups
- System State backup
- Bare Metal Recovery

### ОСНОВНИ УМЕНИЯ:
- Конфигуриране на backup планове
- Изпълнение на ръчни backups
- Възстановяване на файлове и папки
- System State recovery

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Информационна сигурност** - защита на данни, криптиране
2. **Мрежови технологии** - network storage, replication
3. **Икономика** - TCO на backup решения
4. **Математика** - изчисляване на storage нужди

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Интерактивна лекция с примери
2. Демонстрация на конфигурация
3. Практически упражнения
4. Симулация на disaster recovery
5. Групова дискусия

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Windows Server 2022 VM
- Допълнителен виртуален диск за backup
- Windows Server Backup console
- PowerShell скриптове
- Работни листове

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Стартиране на лабораторната среда
- Представяне на целите

**Мотивация:**
"Данните на една компания са нейният най-ценен актив. Един ransomware атака или хардуерна повреда може да унищожи всичко за секунди. Backup е последната линия на защита."

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Въпроси:**
```
1. Какво се случва при хардуерна повреда на сървър?
2. Как ransomware засяга бизнеса?
3. Колко струва загубата на данни?
```

**Статистика за размисъл:**
```
• 60% от компаниите без backup план фалират 
  в рамките на 6 месеца след загуба на данни
• Средна цена на downtime: $5,600/минута
• 93% от компаниите с major data loss се 
  възстановяват само ако имат добър backup
```

---

### **3. НОВ МАТЕРИАЛ (40 минути)**

#### **Част 1: Backup стратегии и теория (15 минути)**

**3-2-1 Правило:**
```
┌─────────────────────────────────────────────────────────────┐
│                    3-2-1 BACKUP RULE                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│    3 КОПИЯ           2 ТИПА МЕДИИ         1 OFFSITE        │
│    на данните        за съхранение         копие           │
│                                                             │
│    ┌─────────┐       ┌─────────┐          ┌─────────┐      │
│    │Original │       │  Local  │          │  Cloud  │      │
│    │  Data   │       │  Disk   │          │ Backup  │      │
│    └─────────┘       └─────────┘          └─────────┘      │
│    ┌─────────┐       ┌─────────┐                           │
│    │ Backup  │       │  Tape   │                           │
│    │   #1    │       │  /NAS   │                           │
│    └─────────┘       └─────────┘                           │
│    ┌─────────┐                                              │
│    │ Backup  │                                              │
│    │   #2    │                                              │
│    └─────────┘                                              │
└─────────────────────────────────────────────────────────────┘
```

**Типове Backup:**

| Тип | Описание | Време за backup | Време за restore | Storage |
|-----|----------|-----------------|------------------|---------|
| Full | Всички данни | Дълго | Бързо | Много |
| Incremental | Само промените от последния backup | Бързо | Бавно | Малко |
| Differential | Промените от последния Full | Средно | Средно | Средно |

**RPO vs RTO:**
```
RPO (Recovery Point Objective)
= Колко данни можем да загубим?
= Време между последния backup и инцидента
Пример: RPO = 4 часа означава backup на всеки 4 часа

RTO (Recovery Time Objective)
= Колко бързо трябва да се възстановим?
= Максимален допустим downtime
Пример: RTO = 2 часа означава системата трябва да работи 
        до 2 часа след инцидента

Timeline:
|----RPO----|----RTO----|
  Last        Incident    Recovery
  Backup                  Complete
```

---

#### **Част 2: Windows Server Backup - Инсталация (10 минути)**

**PowerShell инсталация:**
```powershell
# Инсталиране на Windows Server Backup feature
Install-WindowsFeature Windows-Server-Backup -IncludeManagementTools

# Проверка
Get-WindowsFeature Windows-Server-Backup

# Отваряне на конзолата
wbadmin.msc
```

**Подготовка на backup destination:**
```powershell
# Добавяне на нов диск към VM (в Hyper-V/VMware)
# След добавяне:

# Инициализиране на диска
Initialize-Disk -Number 1 -PartitionStyle GPT

# Създаване на partition
New-Partition -DiskNumber 1 -UseMaximumSize -DriveLetter E

# Форматиране
Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "Backup"
```

---

#### **Част 3: Конфигуриране на Backup (15 минути)**

**GUI метод - Scheduled Backup:**
```
Windows Server Backup → Backup Schedule

1. Getting Started → Next

2. Select Backup Configuration:
   ○ Full server (recommended)
   ○ Custom → Изберете конкретни volumes/folders
   → Next

3. Specify Backup Time:
   ○ Once a day: 21:00
   ○ More than once a day: 12:00, 21:00
   → Next

4. Specify Destination Type:
   ○ Back up to a hard disk dedicated for backups
   ○ Back up to a volume
   ○ Back up to a shared network folder
   → Next

5. Select Destination Disk:
   → Show All Available Disks
   → Select backup disk (E:)
   → Next

6. Confirmation → Finish
```

**PowerShell метод:**
```powershell
# Импортиране на модула
Import-Module WindowsServerBackup

# Създаване на backup policy
$policy = New-WBPolicy

# Добавяне на всички critical volumes
$volumes = Get-WBVolume -AllVolumes
Add-WBVolume -Policy $policy -Volume $volumes

# System State backup
Add-WBSystemState -Policy $policy

# Bare Metal Recovery
Add-WBBareMetalRecovery -Policy $policy

# Задаване на destination
$backupDisk = Get-WBDisk | Where-Object { $_.DiskNumber -eq 1 }
$target = New-WBBackupTarget -Disk $backupDisk
Add-WBBackupTarget -Policy $policy -Target $target

# Schedule (ежедневно в 21:00)
Set-WBSchedule -Policy $policy -Schedule 21:00

# Прилагане на политиката
Set-WBPolicy -Policy $policy -AllowDeleteOldBackups
```

**Ръчен backup:**
```powershell
# Еднократен backup
wbadmin start backup -backupTarget:E: -include:C: -allCritical -quiet

# Само System State
wbadmin start systemstatebackup -backupTarget:E: -quiet

# Проверка на статус
wbadmin get status

# Преглед на backup история
wbadmin get versions
```

---

### **4. ПРАКТИКА (25 минути)**

#### **Практическа задача 4.1: Backup на папка (10 минути)**

```powershell
# Създаване на тестови данни
New-Item -Path "C:\ImportantData" -ItemType Directory
1..10 | ForEach-Object { 
    "Document $_" | Out-File "C:\ImportantData\Doc$_.txt" 
}

# Backup на конкретна папка
wbadmin start backup -backupTarget:E: -include:C:\ImportantData -quiet

# Изчакване и проверка
wbadmin get versions
```

#### **Практическа задача 4.2: Възстановяване (10 минути)**

```powershell
# Симулиране на загуба на данни
Remove-Item -Path "C:\ImportantData\Doc5.txt" -Force
Remove-Item -Path "C:\ImportantData\Doc6.txt" -Force

# Възстановяване чрез GUI:
# Windows Server Backup → Recover
# 1. Getting Started → This server → Next
# 2. Select Backup Date → Изберете датата → Next
# 3. Select Recovery Type → Files and folders → Next
# 4. Select Items to Recover → Browse → C:\ImportantData → Select files
# 5. Specify Recovery Options → 
#    ○ Original location / Another location
#    ○ Create copies / Overwrite
# 6. Confirmation → Recover

# Или с PowerShell:
# Намиране на версията
$version = Get-WBBackupSet | Select-Object -First 1

# Start recovery (интерактивен процес)
Start-WBFileRecovery -BackupSet $version -FileOrFolder "C:\ImportantData\Doc5.txt" `
    -SourcePath "C:\ImportantData" -TargetPath "C:\ImportantData" -Recursive
```

#### **Практическа задача 4.3: Мониторинг и отчети (5 минути)**

```powershell
# PowerShell скрипт за мониторинг
function Get-BackupStatus {
    $backups = Get-WBBackupSet
    
    if ($backups) {
        $latest = $backups | Select-Object -First 1
        $age = (Get-Date) - $latest.BackupTime
        
        [PSCustomObject]@{
            LastBackup = $latest.BackupTime
            AgeHours = [math]::Round($age.TotalHours, 2)
            Status = if ($age.TotalHours -gt 25) { "WARNING" } else { "OK" }
            BackupLocation = $latest.BackupTarget
        }
    } else {
        Write-Warning "No backups found!"
    }
}

Get-BackupStatus | Format-List

# Event Log проверка
Get-EventLog -LogName "Microsoft-Windows-Backup" -Newest 10 | 
    Format-Table TimeGenerated, EntryType, Message -AutoSize
```

---

### **5. ОБОБЩЕНИЕ (10 минути)**

**Ключови точки:**
```
✓ 3-2-1 правило за backup
✓ RPO = колко данни губим
✓ RTO = колко бързо се възстановяваме
✓ Full vs Incremental vs Differential
✓ System State = AD, Registry, Boot files
✓ Bare Metal Recovery = пълно възстановяване
✓ Тестване на backups е задължително!
```

**Чеклист за backup стратегия:**
```
□ Дефинирани RPO и RTO
□ 3-2-1 правило спазено
□ Автоматизиран schedule
□ Offsite копие (cloud/tape)
□ Редовно тестване на restore
□ Документирани процедури
□ Мониторинг и alerting
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

```
1. Създайте backup план за малка фирма:
   - 1 файлов сървър, 1 AD контролер
   - RPO: 4 часа, RTO: 2 часа
   - Бюджет: ограничен

2. Изчислете нужното storage за:
   - 500 GB данни
   - 30 дни retention
   - Daily incremental + Weekly full

3. Проучете: Какво е Veeam Backup?

Време: 40-50 минути
```

---

## 6. ОЦЕНЯВАНЕ

| Компонент | Точки | Процент |
|-----------|-------|---------|
| Теоретични знания | 15 | 20% |
| Конфигуриране на backup | 25 | 35% |
| Възстановяване на данни | 20 | 30% |
| Домашна работа | 10 | 15% |
| **ОБЩО** | **70** | **100%** |

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли 3-2-1 правилото?
2. Мога ли да конфигурирам backup план?
3. Мога ли да възстановя данни от backup?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 90% разбират backup стратегии
- [ ] 85% конфигурират scheduled backup
- [ ] 80% успешно възстановяват файлове

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: РАБОТЕН ЛИСТ

```
╔════════════════════════════════════════════════════════════╗
║              РАБОТЕН ЛИСТ: BACKUP СТРАТЕГИЯ               ║
╠════════════════════════════════════════════════════════════╣
║ Име: _______________________ Клас: ______ Дата: _________ ║
╚════════════════════════════════════════════════════════════╝

ЗАДАЧА 1: BACKUP ПЛАН

Целеви RPO: _____________ RTO: _____________

Backup Schedule:
| Ден | Тип Backup | Време | Destination |
|-----|------------|-------|-------------|
| Пон |            |       |             |
| Вто |            |       |             |
| Сря |            |       |             |
| Чет |            |       |             |
| Пет |            |       |             |
| Съб |            |       |             |
| Нед |            |       |             |

ЗАДАЧА 2: ПРАКТИКА

Backup създаден: [ ] Да [ ] Не
Backup версия: _________________________
Файлове възстановени: [ ] Да [ ] Не

ЗАДАЧА 3: ИЗЧИСЛЕНИЯ

Данни за backup: _________ GB
Daily change rate: _________ %
Retention: _________ дни

Нужно storage:
Full backups: _________ GB
Incrementals: _________ GB
ОБЩО: _________ GB

═══════════════════════════════════════════════════════════
```

### ПРИЛОЖЕНИЕ 2: POWERSHELL BACKUP СКРИПТОВЕ

```powershell
# ══════════════════════════════════════════════════════════
#          WINDOWS SERVER BACKUP СКРИПТОВЕ
# ══════════════════════════════════════════════════════════

# BACKUP COMMANDS
wbadmin start backup -backupTarget:E: -include:C: -quiet
wbadmin start systemstatebackup -backupTarget:E: -quiet
wbadmin get versions
wbadmin get status

# MONITORING SCRIPT
$lastBackup = Get-WBBackupSet | Select-Object -First 1
$age = (Get-Date) - $lastBackup.BackupTime
if ($age.TotalHours -gt 25) {
    Send-MailMessage -To "admin@company.com" -Subject "Backup Warning"
}

# RESTORE COMMANDS
wbadmin start recovery -version:<version> -itemType:File -items:C:\Data
wbadmin start systemstaterecovery -version:<version>

# ══════════════════════════════════════════════════════════
```

---

*Документът е създаден за учебната 2025/2026 година*
*Специалност: Икономическо информационно осигуряване (код 482021)*
