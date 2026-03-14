# УРОЧЕН ПЛАН №5
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** 128-мо СУ "Алберт Айнщайн", гр.София
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** RAID масиви - конфигурация и управление
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Комбиниран
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат концепцията и целите на RAID технологията
2. Да усвоят различните RAID нива и техните характеристики
3. Да научат как се конфигурират хардуерни и софтуерни RAID масиви
4. Да разбират изчисленията за капацитет, производителност и надеждност
5. Да познават процедурите за възстановяване при отказ

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на отговорност към съхранението на данни
2. Възпитаване на системен подход при планиране на storage
3. Развиване на критично мислене при избор на RAID ниво
4. Изграждане на навици за редовни backup процедури

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за анализ на рискове
2. Усъвършенстване на способности за техническо планиране
3. Формиране на умения за disaster recovery
4. Развитие на компетенции за управление на данни

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- RAID концепция - Redundant Array of Independent Disks
- Стандартни RAID нива: 0, 1, 5, 6, 10, 50, 60
- Nested и hybrid RAID конфигурации
- Хардуерни vs софтуерни RAID контролери
- Hot spare и hot swap функционалност
- Изчисления за капацитет, IOPS, MTBF

#### Умения:
- Конфигуриране на RAID масиви в BIOS/UEFI
- Създаване на софтуерни RAID в Windows и Linux
- Мониторинг на RAID здравето
- Възстановяване на RAID при disk failure
- Избор на оптимално RAID ниво според нуждите

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Математика** - вероятности, комбинаторика, XOR операции
2. **Информационна сигурност** - data protection, business continuity
3. **Бази данни** - висока достъпност, производителност
4. **Икономика** - cost-benefit анализ, TCO
5. **Статистика** - MTBF, reliability calculations

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Визуална презентация** с анимации на RAID операции
2. **Демонстрация** на реална RAID конфигурация
3. **Практическа работа** със софтуерен RAID
4. **Симулация** на disk failure и recovery
5. **Изчислителни задачи** за капацитет и производителност

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Хардуер:**
   - Демонстрационен RAID контролер
   - Минимум 4 диска за демонстрация
   - Сървър или workstation с RAID поддръжка
   
2. **Софтуер:**
   - Intel RST (Rapid Storage Technology)
   - Windows Storage Spaces
   - Linux mdadm
   - RAID калкулатори
   - Мониторинг софтуер
   
3. **Учебни материали:**
   - Схеми на различни RAID нива
   - Таблици за сравнение
   - Работни листове за изчисления

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Подготовка на демонстрационните системи
- Въвеждащ сценарий: "Сървърът на фирмата съхранява критични данни. Как да осигурим надеждност?"

**Дейност на учениците:**
- Подготовка за работа
- Обсъждане на проблема

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (8 минути)**

**Дейност на учителя:**
- Преговор на storage технологии от предишни уроци

**Въпроси за преговор:**
1. Какви са рисковете при single disk storage?
2. Как се измерва надеждността на дисковете (MTBF)?
3. Какво е throughput и IOPS?
4. Защо backup не е достатъчен?

**Проблемна ситуация:**
"Имате 4 диска по 1TB. Как да постигнете:
- Максимална скорост?
- Максимална надеждност?
- Баланс между двете?"

### **3. НОВ МАТЕРИАЛ (42 минути)**

#### **Част 1: Основи на RAID технологията (10 мин)**

**История и концепция:**
```
1987 - UC Berkeley представя RAID концепцията
Цели на RAID:
- Повишена надеждност (Redundancy)
- Подобрена производителност (Striping)
- Увеличен капацитет (Spanning)
- Икономическа ефективност

Методи за постигане:
- Mirroring - огледално копиране
- Striping - разделяне на данните
- Parity - контролни суми за възстановяване
```

**Терминология:**
```
- Array: Група дискове работещи заедно
- Stripe: Блок данни разпределен между дискове
- Stripe size: Размер на блока (64KB, 128KB...)
- Parity: XOR контролна сума
- Hot spare: Резервен диск в готовност
- Rebuild: Възстановяване след отказ
- Degraded mode: Работа с повреден диск
```

**Hardware vs Software RAID:**

| Характеристика | Hardware RAID | Software RAID |
|----------------|---------------|---------------|
| Производителност | Отлична | Добра |
| CPU натоварване | Минимално | Умерено |
| Цена | Висока ($200-2000) | Безплатно |
| Преносимост | Зависи от контролер | Универсална |
| Boot support | Да | Ограничен |
| Cache + BBU | Да | Не |
| Възстановяване | Сложно | По-лесно |

#### **Част 2: Стандартни RAID нива (15 мин)**

**RAID 0 - Striping:**
```
Дискове: Минимум 2
Капацитет: N × disk_size
Скорост четене: N × disk_speed
Скорост запис: N × disk_speed
Fault tolerance: NONE ❌

Data distribution:
Disk 1: [A1][A3][A5][A7]
Disk 2: [A2][A4][A6][A8]

Приложение: Временни данни, video editing, gaming
```

**RAID 1 - Mirroring:**
```
Дискове: 2 (или четен брой)
Капацитет: disk_size (50% efficiency)
Скорост четене: 2 × disk_speed
Скорост запис: 1 × disk_speed
Fault tolerance: N-1 дискове ✓

Data distribution:
Disk 1: [A][B][C][D]
Disk 2: [A][B][C][D] (копие)

Приложение: OS, критични данни, бази данни
```

**RAID 5 - Striping with Parity:**
```
Дискове: Минимум 3
Капацитет: (N-1) × disk_size
Скорост четене: (N-1) × disk_speed
Скорост запис: < single disk (parity calc)
Fault tolerance: 1 диск ✓

Data distribution:
Disk 1: [A1][A2][Ap] [B3]
Disk 2: [A3][Bp][B1] [B2]
Disk 3: [Ap][B3][C1] [C2]
(Ap = A1 XOR A2 XOR A3)

Приложение: File servers, архиви, общо предназначение
```

**RAID 6 - Double Parity:**
```
Дискове: Минимум 4
Капацитет: (N-2) × disk_size
Скорост четене: (N-2) × disk_speed
Скорост запис: < RAID 5
Fault tolerance: 2 диска ✓✓

Parity calculation:
P = XOR parity
Q = Reed-Solomon parity

Приложение: Критични данни, големи масиви
```

**RAID 10 (1+0) - Mirrored Stripes:**
```
Дискове: Минимум 4 (четен брой)
Капацитет: N/2 × disk_size
Скорост четене: N × disk_speed
Скорост запис: N/2 × disk_speed
Fault tolerance: 1 диск от всяка двойка ✓

Structure:
[RAID 0]
  ├── [RAID 1: Disk1 + Disk2]
  └── [RAID 1: Disk3 + Disk4]

Приложение: Бази данни, виртуализация, high-performance
```

**Сравнителна таблица:**

| RAID | Min диска | Капацитет | Read | Write | Fault | Приложение |
|------|-----------|-----------|------|-------|-------|------------|
| 0 | 2 | N×size | Отл. | Отл. | 0 | Temp/Speed |
| 1 | 2 | size | Добра | Норм. | N-1 | Critical |
| 5 | 3 | (N-1)×size | Добра | Слаба | 1 | General |
| 6 | 4 | (N-2)×size | Добра | Слаба | 2 | Archive |
| 10 | 4 | N/2×size | Отл. | Добра | 1 per pair | Database |

#### **Част 3: Изчисления и планиране (8 мин)**

**Формули за капацитет:**
```python
# RAID 0
capacity = num_disks × disk_size

# RAID 1
capacity = disk_size

# RAID 5
capacity = (num_disks - 1) × disk_size
usable_percentage = ((num_disks - 1) / num_disks) × 100

# RAID 6
capacity = (num_disks - 2) × disk_size

# RAID 10
capacity = (num_disks / 2) × disk_size
```

**IOPS калкулации:**
```
RAID 0:
Read IOPS = N × disk_IOPS
Write IOPS = N × disk_IOPS

RAID 1:
Read IOPS = 2 × disk_IOPS
Write IOPS = disk_IOPS

RAID 5:
Read IOPS = N × disk_IOPS
Write IOPS = disk_IOPS / 4 (write penalty)

RAID 6:
Read IOPS = N × disk_IOPS
Write IOPS = disk_IOPS / 6 (double parity penalty)
```

**Reliability (MTBF) изчисления:**
```
RAID 0:
MTBF_array = MTBF_disk / N (по-лошо!)

RAID 1:
MTBF_array = MTBF_disk × 1.5

RAID 5:
MTBF_array = MTBF_disk × (N-1) / N

Rebuild risk:
P(failure) = 1 - (1 - BER × capacity)^num_reads
BER = Bit Error Rate (10^-14 за enterprise)
```

#### **Част 4: Практическа конфигурация (9 мин)**

**Windows Storage Spaces:**
```powershell
# Създаване на storage pool
New-StoragePool -FriendlyName "MyPool" `
  -StorageSubsystemFriendlyName "Windows Storage*" `
  -PhysicalDisks (Get-PhysicalDisk -CanPool $true)

# Създаване на virtual disk (RAID 5)
New-VirtualDisk -StoragePoolFriendlyName "MyPool" `
  -FriendlyName "MyRAID5" `
  -ResiliencySettingName "Parity" `
  -Size 2TB

# Инициализация и форматиране
Initialize-Disk -FriendlyName "MyRAID5"
New-Partition -DiskNumber 3 -UseMaximumSize -DriveLetter R
Format-Volume -DriveLetter R -FileSystem NTFS
```

**Linux mdadm:**
```bash
# Създаване на RAID 5
sudo mdadm --create /dev/md0 --level=5 --raid-devices=3 \
  /dev/sdb /dev/sdc /dev/sdd

# Проверка на статус
sudo mdadm --detail /dev/md0
cat /proc/mdstat

# Създаване на filesystem
sudo mkfs.ext4 /dev/md0
sudo mount /dev/md0 /mnt/raid5

# Запазване на конфигурация
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```

**BIOS/UEFI RAID конфигурация:**
```
1. Enter BIOS (F2/Del при boot)
2. Advanced → SATA Configuration
3. SATA Mode: RAID
4. Save & Exit
5. Ctrl+I за Intel RST при boot
6. Create RAID Volume
7. Select RAID Level
8. Select Disks
9. Set Stripe Size
10. Create Volume
```

### **4. ЗАТВЪРЖДАВАНЕ (30 минути)**

#### **Практическа работа: Конфигуриране и тестване**

**Задача 1: Планиране на RAID (10 мин)**

**Сценарии за решаване:**

**A. Web Server:**
```
Изисквания:
- 2TB полезно пространство
- Висока надеждност
- Умерена производителност
- Бюджет за 4 диска

Решение:
RAID 5 с 4×1TB диска
Капацитет: 3TB
Redundancy: 1 диск
```

**B. Video Editing:**
```
Изисквания:
- Максимална скорост
- 4TB пространство
- Backup отделно

Решение:
RAID 0 с 2×2TB NVMe
Отделен backup storage
```

**C. Database Server:**
```
Изисквания:
- Висока IOPS
- Redundancy
- 1TB достатъчно

Решение:
RAID 10 с 4×512GB SSD
Капацитет: 1TB
Отлична производителност
```

**Таблица за планиране:**
| Параметър | Стойност | Обосновка |
|-----------|----------|-----------|
| RAID ниво | | |
| Брой дискове | | |
| Тип дискове | | |
| Общ капацитет | | |
| Полезен капацитет | | |
| Estimated IOPS | | |

**Задача 2: Софтуерен RAID в VM (15 мин)**

**Linux mdadm практика:**
```bash
# Създаване на виртуални дискове (loop devices)
for i in {1..4}; do
  dd if=/dev/zero of=/tmp/disk$i.img bs=1G count=1
  sudo losetup /dev/loop$i /tmp/disk$i.img
done

# RAID 5 създаване
sudo mdadm --create /dev/md127 --level=5 \
  --raid-devices=3 /dev/loop1 /dev/loop2 /dev/loop3 \
  --spare-devices=1 /dev/loop4

# Мониторинг на rebuild
watch cat /proc/mdstat

# Симулация на failure
sudo mdadm --fail /dev/md127 /dev/loop2
sudo mdadm --remove /dev/md127 /dev/loop2

# Автоматичен rebuild със spare
# Наблюдавайте процеса
```

**Задача 3: Performance тестване (5 мин)**

**Benchmark на различни RAID:**
```bash
# За всяко RAID ниво:

# Sequential read
sudo hdparm -t /dev/md0

# Sequential write  
dd if=/dev/zero of=/mnt/raid/test bs=1G count=1 oflag=direct

# Random IOPS
fio --name=randread --ioengine=libaio --iodepth=16 \
  --rw=randread --bs=4k --direct=1 --size=1G \
  --numjobs=4 --runtime=60 --group_reporting \
  --filename=/mnt/raid/test
```

**Резултати за сравнение:**
| RAID | Seq Read | Seq Write | 4K IOPS |
|------|----------|-----------|---------|
| Single | 150 MB/s | 150 MB/s | 200 |
| RAID 0 | | | |
| RAID 1 | | | |
| RAID 5 | | | |

### **5. ОБОБЩЕНИЕ (10 минути)**

**Ключови принципи:**
- RAID не замества backup!
- Избор според: Performance vs Redundancy vs Cost
- RAID 5/6 write penalty при random writes
- URE (Unrecoverable Read Errors) риск при rebuild

**Best practices:**
```
1. Използвайте еднакви дискове
2. Hot spare за критични системи
3. Regular scrubbing/patrol read
4. Monitor SMART статус
5. Тествайте recovery процедури
6. RAID + Backup стратегия
```

**Дискусионни въпроси:**
1. Защо RAID 5 не се препоръчва за големи дискове?
2. Кога да изберем hardware RAID?
3. Как облачните услуги променят нуждата от RAID?
4. Какво е RAID-Z в ZFS?

### **6. ДОМАШНА РАБОТА (5 минути)**

**Задачи:**

1. **Изчислителна задача:**
   - Имате 6×4TB диска
   - Сравнете капацитет и надеждност за:
     - RAID 5, RAID 6, RAID 10, RAID 50
   - Изчислете rebuild time при 150MB/s

2. **Изследователска:**
   - Проучете ZFS и RAID-Z/Z2/Z3
   - Сравнете с традиционен RAID
   - Какво е "RAID scrubbing"?

3. **Проектна:**
   - Проектирайте storage система за:
     - Малка фирма (50 служители)
     - Нужди: 20TB, висока надеждност
     - Бюджет: 5000€
   - Включете: RAID, backup, разширяемост

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Познаване на RAID нива | 25% |
| Правилни изчисления | 20% |
| Конфигуриране на RAID | 20% |
| Анализ и планиране | 15% |
| Решаване на сценарии | 15% |
| Активност | 5% |

### ИНДИКАТОРИ ЗА ПОСТИЖЕНИЯ:
- Различава и обяснява RAID нивата
- Изчислява капацитет и производителност
- Конфигурира софтуерен RAID
- Избира оптимално решение за конкретни нужди

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли кога кое RAID ниво да използвам?
2. Мога ли да изчисля капацитет и IOPS?
3. Умея ли да конфигурирам RAID масив?
4. Знам ли процедурите при disk failure?

### ОЧАКВАНИ ТРУДНОСТИ:
- Объркване между RAID 01 и RAID 10
- Разбиране на parity изчисления
- Write penalty концепцията
- Практическа липса на множество дискове

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: RAID WRITE PENALTIES

```
Write Penalty Factor:
RAID 0: 1 (no penalty)
RAID 1: 2 (write to both)
RAID 5: 4 (read-modify-write)
RAID 6: 6 (double parity)

Random Write IOPS:
IOPS = Raw_IOPS / Write_Penalty

Example (100 IOPS disk):
RAID 5: 100 / 4 = 25 IOPS
RAID 6: 100 / 6 = 17 IOPS
```

### ПРИЛОЖЕНИЕ 2: RAID КАЛКУЛАТОР

```python
def raid_calculator(num_disks, disk_size, raid_level):
    """Изчислява RAID параметри"""
    
    if raid_level == 0:
        capacity = num_disks * disk_size
        fault_tolerance = 0
    elif raid_level == 1:
        capacity = disk_size
        fault_tolerance = num_disks - 1
    elif raid_level == 5:
        capacity = (num_disks - 1) * disk_size
        fault_tolerance = 1
    elif raid_level == 6:
        capacity = (num_disks - 2) * disk_size
        fault_tolerance = 2
    elif raid_level == 10:
        capacity = (num_disks // 2) * disk_size
        fault_tolerance = num_disks // 2
    
    efficiency = (capacity / (num_disks * disk_size)) * 100
    
    return {
        'capacity': capacity,
        'fault_tolerance': fault_tolerance,
        'efficiency': efficiency
    }

# Пример:
result = raid_calculator(4, 2000, 5)  # 4×2TB RAID 5
print(f"Capacity: {result['capacity']}GB")
print(f"Can survive: {result['fault_tolerance']} disk failures")
print(f"Storage efficiency: {result['efficiency']:.1f}%")
```

### ПРИЛОЖЕНИЕ 3: RECOVERY ПРОЦЕДУРИ

**RAID 5 Recovery Steps:**
```
1. Identify failed disk:
   - Check RAID controller logs
   - mdadm --detail /dev/md0
   - Look for [F] or [_]

2. Remove failed disk:
   - mdadm --remove /dev/md0 /dev/sdX
   - Physically replace disk

3. Add new disk:
   - mdadm --add /dev/md0 /dev/sdX
   
4. Monitor rebuild:
   - watch cat /proc/mdstat
   - mdadm --monitor /dev/md0

5. Verify:
   - mdadm --detail /dev/md0
   - Check for "clean" state

Recovery time estimate:
Time = Disk_Size / Rebuild_Speed
2TB / 150MB/s = ~3.7 hours
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
