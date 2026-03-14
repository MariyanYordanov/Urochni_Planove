# УРОЧЕН ПЛАН №4
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** ПГИ „Професор д-р Асен Златаров"
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** SSD технологии - NVMe, M.2, производителност
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Нови знания
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат принципа на работа на SSD дисковете
2. Да усвоят различията между NAND flash технологиите
3. Да познават интерфейсите и протоколите (SATA, NVMe, PCIe)
4. Да разбират форм-факторите M.2, U.2, mSATA
5. Да могат да оценяват производителността и издръжливостта

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на разбиране за важността на storage технологиите
2. Възпитаване на отговорност при избор на storage решения
3. Развиване на критично мислене при анализ на спецификации
4. Изграждане на навици за data management

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за анализ на технически параметри
2. Усъвършенстване на способността за бенчмарк тестове
3. Формиране на умения за диагностика на storage устройства
4. Развитие на компетенции за планиране на storage системи

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- NAND Flash технологии: SLC, MLC, TLC, QLC, PLC
- Контролери и firmware в SSD
- Интерфейси: SATA III, PCIe 3.0/4.0/5.0, NVMe протокол
- M.2 форм-фактор: 2280, 2260, 2242, keying
- Производителност: sequential/random, IOPS, латентност
- Износване и технологии за удължаване на живота

#### Умения:
- Идентифициране на различни типове SSD
- Инсталиране на M.2 NVMe дискове
- Benchmark тестване с различни инструменти
- Мониторинг на здравето на SSD (SMART)
- Оптимизация на операционната система за SSD

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Бази данни** - производителност на database операции
2. **Физика** - полупроводникови технологии, електронни схеми
3. **Математика** - алгоритми за wear leveling, error correction
4. **Информационна сигурност** - криптиране, secure erase
5. **Икономика** - TCO анализ, цена за GB

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Интерактивна лекция** с визуални материали
2. **Демонстрация** на различни SSD форм-фактори
3. **Практическа работа** с benchmark инструменти
4. **Сравнителен анализ** HDD vs SSD vs NVMe
5. **Лабораторно упражнение** по инсталация

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Хардуер:**
   - Различни типове SSD (SATA, M.2, U.2)
   - Демонстрационна дънна платка с M.2 слотове
   - USB към M.2 адаптери
   
2. **Софтуер:**
   - CrystalDiskMark
   - AS SSD Benchmark
   - Samsung Magician / WD Dashboard
   - CrystalDiskInfo
   - ATTO Disk Benchmark
   
3. **Учебни материали:**
   - Схеми на NAND cell структури
   - Сравнителни таблици
   - Спецификации на производители

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Подготовка на демонстрационните SSD дискове
- Въвеждащ въпрос: "Защо SSD са по-бързи от HDD?"

**Дейност на учениците:**
- Подготовка за урока
- Споделяне на опит със SSD

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (8 минути)**

**Дейност на учителя:**
- Преговор на storage йерархията
- Припомняне на HDD технологията

**Въпроси за преговор:**
1. Как работи традиционният HDD?
2. Какви са недостатъците на механичните дискове?
3. Какво е cache памет в storage контекст?
4. Какво е IOPS и защо е важен?

**Сравнение HDD vs SSD:**
```
HDD:                    SSD:
- Механични части       - Без движещи се части
- 100-200 IOPS         - 100,000+ IOPS
- 150 MB/s sequential  - 7000+ MB/s (PCIe 4.0)
- ~10ms latency        - ~0.1ms latency
- Fragmentation issues - No fragmentation
```

### **3. НОВ МАТЕРИАЛ (45 минути)**

#### **Част 1: NAND Flash технологии (12 мин)**

**Типове NAND Flash:**

```
Bits per cell & Характеристики:

SLC (Single-Level Cell) - 1 bit
├── Издръжливост: 100,000 P/E cycles
├── Скорост: Най-бърза
├── Цена: Най-скъпа ($$$$$)
└── Приложение: Enterprise, cache

MLC (Multi-Level Cell) - 2 bits
├── Издръжливост: 10,000 P/E cycles
├── Скорост: Много добра
├── Цена: Висока ($$$$)
└── Приложение: Professional

TLC (Triple-Level Cell) - 3 bits
├── Издръжливост: 3,000 P/E cycles
├── Скорост: Добра
├── Цена: Умерена ($$$)
└── Приложение: Consumer mainstream

QLC (Quad-Level Cell) - 4 bits
├── Издръжливост: 1,000 P/E cycles
├── Скорост: Средна
├── Цена: Ниска ($$)
└── Приложение: Bulk storage

PLC (Penta-Level Cell) - 5 bits
├── Издръжливост: <500 P/E cycles
├── Скорост: По-бавна
├── Цена: Най-ниска ($)
└── Приложение: Cold storage
```

**3D NAND технология:**
```
Planar NAND → 3D NAND
2D структура → Вертикално подреждане

Предимства на 3D NAND:
- По-висока плътност (повече GB)
- По-добра издръжливост
- По-ниска консумация
- По-ниска цена за GB

Layers evolution:
32L → 64L → 96L → 128L → 176L → 232L → 500L+
```

**SSD Controller функции:**
- Wear leveling - равномерно износване
- Error correction (ECC) - корекция на грешки
- Bad block management - управление на дефекти
- Garbage collection - освобождаване на място
- Over-provisioning - резервно пространство
- Thermal throttling - температурен контрол

#### **Част 2: Интерфейси и протоколи (13 мин)**

**SATA III (AHCI протокол):**
```
Характеристики:
- Максимална скорост: 6 Gb/s (600 MB/s)
- Реална скорост: ~550 MB/s
- Латентност: ~100 μs
- Съвместимост: Universal
- Форм-фактори: 2.5", mSATA, M.2 (SATA)

Ограничения:
- Bottleneck за модерни SSD
- Дизайн за HDD (legacy)
- Една опашка за команди
```

**NVMe (Non-Volatile Memory Express):**
```
Характеристики:
- Дизайн специално за SSD
- 64K команди в 64K опашки
- Директна връзка с CPU през PCIe
- Латентност: ~10 μs
- Паралелна обработка

PCIe версии и скорости:
PCIe 3.0 x4: 4 GB/s (3.5 GB/s real)
PCIe 4.0 x4: 8 GB/s (7 GB/s real)
PCIe 5.0 x4: 16 GB/s (14 GB/s real)
```

**M.2 форм-фактор:**
```
Размери (Width × Length):
- 2230: 22mm × 30mm (малки лаптопи)
- 2242: 22mm × 42mm (ultrabooks)
- 2260: 22mm × 60mm (рядко)
- 2280: 22mm × 80mm (стандарт)
- 22110: 22mm × 110mm (enterprise)

Keying (ключове):
- B-key: PCIe x2 / SATA
- M-key: PCIe x4
- B+M key: Universal (x2 speed)

Socket типове:
- Socket 1: Wi-Fi/Bluetooth
- Socket 2: WWAN/SSD (B-key)
- Socket 3: SSD (M-key)
```

**Демонстрация:**
- Показване на различни M.2 дискове
- Обяснение на keying системата
- Идентифициране на слотове на дънна платка

#### **Част 3: Производителност и метрики (10 мин)**

**Основни параметри:**
```
Sequential Read/Write:
- Големи файлове, видео editing
- MB/s измерване
- PCIe 4.0: до 7000/6800 MB/s
- PCIe 5.0: до 14000/12000 MB/s

Random 4K Read/Write:
- OS операции, програми
- IOPS измерване
- NVMe: 600K/700K IOPS
- Най-важно за реална производителност

Латентност:
- HDD: 10-15ms
- SATA SSD: 0.1ms
- NVMe: 0.02ms
- Optane: 0.01ms
```

**TBW и издръжливост:**
```
TBW (Total Bytes Written):
- Колко TB може да запише диска
- 250GB TLC: ~150 TBW
- 1TB TLC: ~600 TBW
- 2TB TLC: ~1200 TBW

DWPD (Drive Writes Per Day):
DWPD = TBW / (Capacity × Days × Years)

Пример: 600 TBW, 1TB, 5 години
DWPD = 600 / (1 × 365 × 5) = 0.33
```

**SLC Cache технология:**
```
Динамичен SLC cache:
- Част от TLC работи като SLC
- Ускорява burst writes
- Размер: 10-100GB типично

Поведение:
1. Пише в SLC режим (бързо)
2. При запълване → директно TLC (бавно)
3. Background: SLC → TLC migration
```

#### **Част 4: Реални приложения и оптимизация (10 мин)**

**Избор на SSD за различни нужди:**

```
Gaming:
- Капацитет: 1-2TB
- Тип: TLC NVMe PCIe 3.0/4.0
- Примери: Samsung 980 Pro, WD Black SN850X

Professional (video/photo):
- Капацитет: 2-4TB
- Тип: MLC/TLC с висок TBW
- Sustained write важна
- Примери: Samsung 990 Pro, Sabrent Rocket 4 Plus

Server/Enterprise:
- U.2/U.3 форм-фактор
- Power loss protection
- Висока издръжливост
- Примери: Intel DC P5520, Samsung PM9A3

Boot drive:
- Капацитет: 256-512GB
- Тип: Бюджетен NVMe
- Примери: Kingston NV2, WD Blue SN580
```

**Оптимизация на Windows за SSD:**
```powershell
# Проверка на TRIM
fsutil behavior query DisableDeleteNotify
# 0 = TRIM enabled

# Изключване на дефрагментация
schtasks /Change /DISABLE /TN "\Microsoft\Windows\Defrag\ScheduledDefrag"

# Оптимизация на power plan
powercfg -h off  # Disable hibernation
```

**Linux оптимизация:**
```bash
# Проверка на TRIM
sudo hdparm -I /dev/nvme0n1 | grep TRIM

# Enable periodic TRIM
sudo systemctl enable fstrim.timer

# Mount опции в /etc/fstab
/dev/nvme0n1p1 / ext4 defaults,noatime,discard 0 1

# I/O Scheduler за NVMe
echo none | sudo tee /sys/block/nvme0n1/queue/scheduler
```

### **4. ЗАТВЪРЖДАВАНЕ (25 минути)**

#### **Практическа работа: Тестване и анализ**

**Задача 1: Benchmark тестване (15 мин)**

**CrystalDiskMark тест:**
```
1. Стартирайте CrystalDiskMark
2. Настройки:
   - Test size: 1GiB
   - Test count: 5
   - Test drive: C: (или SSD)

3. Изпълнете тестовете:
   - SEQ1M Q8T1 - Sequential multi-queue
   - SEQ128K Q32T1 - Sequential single-queue  
   - RND4K Q32T16 - Random multi-thread
   - RND4K Q1T1 - Random single-thread

4. Запишете резултатите
```

**Таблица за резултати:**
| Тест | Read (MB/s) | Write (MB/s) | Очаквано |
|------|-------------|--------------|----------|
| Seq Q8T1 | | | 3500/3000 |
| Seq Q32T1 | | | 550/520 |
| 4K Q32T16 | | | 650/600 |
| 4K Q1T1 | | | 70/180 |

**Задача 2: SMART мониторинг (5 мин)**

**CrystalDiskInfo анализ:**
```
1. Стартирайте CrystalDiskInfo
2. Проверете:
   - Health Status
   - Temperature
   - Power On Hours
   - Total Host Writes
   - Available Spare
   - Percentage Used

3. Изчислете оставащ живот:
   Remaining = TBW - Host_Writes
   Days_left = Remaining / Daily_writes
```

**Задача 3: Сравнителен анализ (5 мин)**

**Попълнете сравнителна таблица:**

| Параметър | HDD 7200rpm | SATA SSD | NVMe PCIe 3.0 | NVMe PCIe 4.0 |
|-----------|------------|----------|---------------|---------------|
| Seq Read | 150 MB/s | | | |
| 4K Random | 100 IOPS | | | |
| Латентност | 10ms | | | |
| Цена/GB | $0.02 | | | |
| Консумация | 6W | | | |

### **5. ОБОБЩЕНИЕ (10 минути)**

**Ключови изводи:**
- NVMe е бъдещето на storage
- TLC е оптималният баланс цена/производителност
- M.2 2280 е стандартният форм-фактор
- Random 4K е най-важната метрика за OS

**Дискусионни въпроси:**
1. Ще изчезнат ли HDD напълно?
2. Какво е следващото след PCIe 5.0?
3. Как ще се развият цените на SSD?
4. Нужен ли е PCIe 4.0/5.0 за gaming?

**Демонстрация:**
- Game loading: HDD vs SATA SSD vs NVMe
- Windows boot време сравнение
- File copy test с голям файл

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задачи:**

1. **Изследователска:**
   - Проучете Intel Optane технологията
   - Сравнете 3D XPoint с NAND
   - Защо Optane се провали? (2 страници)

2. **Практическа:**
   - Тествайте домашния SSD/HDD
   - Използвайте поне 3 benchmark tool-а
   - Създайте детайлен отчет

3. **Конфигурационна:**
   - Планирайте storage за:
     - Gaming PC (бюджет 300€)
     - Video editing workstation
     - NAS сървър
   - Обосновете избора

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Познаване на NAND технологии | 20% |
| Разбиране на интерфейси и протоколи | 25% |
| Правилно изпълнение на benchmark | 20% |
| Анализ на резултати | 15% |
| SMART интерпретация | 10% |
| Избор на подходящ SSD | 10% |

### ОЦЕНЪЧНА РУБРИКА:
- **Отличен (6):** Детайлно познава технологиите, правилно анализира benchmark, предлага оптимални решения
- **Много добър (5):** Добро разбиране, малки грешки в анализа
- **Добър (4):** Основни познания, нуждае се от насочване
- **Среден (3):** Минимални знания, затруднения с практическата част

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли разликите между NAND типовете?
2. Мога ли да избера подходящ SSD за конкретни нужди?
3. Умея ли да интерпретирам benchmark резултати?
4. Знам ли как да оптимизирам OS за SSD?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 90% разбират NVMe предимствата
- [ ] 85% могат да изпълнят benchmark
- [ ] 80% правилно интерпретират SMART данни
- [ ] 75% избират подходящ SSD за нуждите

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: SSD СПЕЦИФИКАЦИИ 2025

**Popular NVMe SSD models:**
```
PCIe 5.0:
- Crucial T700: 12,400/11,800 MB/s, 1.5M IOPS
- Corsair MP700: 10,000/10,000 MB/s
- Gigabyte Aorus 12000: 11,700/9,500 MB/s

PCIe 4.0:
- Samsung 990 Pro: 7,450/6,900 MB/s
- WD Black SN850X: 7,300/6,600 MB/s
- Kingston Fury Renegade: 7,300/7,000 MB/s

PCIe 3.0:
- Samsung 980: 3,500/3,000 MB/s
- WD Blue SN570: 3,500/3,000 MB/s
- Crucial P3: 3,500/3,000 MB/s

SATA:
- Samsung 870 EVO: 560/530 MB/s
- Crucial MX500: 560/510 MB/s
- WD Blue 3D: 560/530 MB/s
```

### ПРИЛОЖЕНИЕ 2: BENCHMARK КОМАНДИ

**Windows команди:**
```powershell
# Тест с Diskspd
diskspd -b4K -d60 -r -w30 -t4 -o8 -Sh C:\test.dat

# WinSAT тест
winsat disk -drive c

# Проверка на TRIM
fsutil behavior query DisableDeleteNotify
```

**Linux команди:**
```bash
# FIO benchmark
sudo fio --name=randread --ioengine=libaio \
  --iodepth=16 --rw=randread --bs=4k --direct=1 \
  --size=4G --numjobs=4 --runtime=60 \
  --group_reporting --filename=/dev/nvme0n1

# hdparm тест
sudo hdparm -Tt /dev/nvme0n1

# dd тест
dd if=/dev/zero of=test bs=1G count=1 oflag=dsync
```

### ПРИЛОЖЕНИЕ 3: SMART АТРИБУТИ

**Критични SMART параметри:**
```
NVMe SMART:
- Available Spare: Резервни блокове (%)
- Percentage Used: Изхабеност (%)
- Data Written: Total TB written
- Power On Hours: Работни часове
- Temperature: Текуща/максимална
- Unsafe Shutdowns: Некоректни изключвания
- Media Errors: Грешки при четене/запис

SATA SSD SMART:
- ID 5: Reallocated Sectors
- ID 9: Power On Hours
- ID 12: Power Cycle Count
- ID 177: Wear Leveling Count
- ID 179: Used Reserved Blocks
- ID 181: Program Fail Count
- ID 182: Erase Fail Count
- ID 194: Temperature
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
