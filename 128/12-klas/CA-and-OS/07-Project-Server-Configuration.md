# УРОЧЕН ПЛАН №7
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** ПГИ „Професор д-р Асен Златаров"
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Проект: Планиране на сървърна конфигурация
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Упражнение (проектна работа)
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да приложат знанията си за планиране на сървърни системи
2. Да усвоят методологията за анализ на изисквания
3. Да научат как се калкулират ресурси и капацитет
4. Да разберат принципите на high availability и redundancy
5. Да могат да създават професионална документация

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на проектно мислене
2. Възпитаване на отговорност при планиране
3. Развиване на екипни умения
4. Изграждане на професионална етика

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на аналитични способности
2. Усъвършенстване на презентационни умения
3. Формиране на бизнес-ориентиран подход
4. Развитие на умения за техническо документиране

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- Сървърни форм-фактори: Tower, Rack, Blade
- Enterprise компоненти и характеристики
- Методология за capacity planning
- High availability концепции: clustering, failover
- Virtualization considerations
- Budget planning и TCO калкулации

#### Умения:
- Анализ на бизнес изисквания
- Изчисляване на необходими ресурси
- Избор на подходящ хардуер
- Планиране на redundancy и backup
- Създаване на техническа спецификация
- Презентиране на решение

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Икономика** - ROI, TCO анализ, бюджетиране
2. **Бизнес информатика** - бизнес процеси и нужди
3. **Проектен мениджмънт** - планиране и документация
4. **Мрежова администрация** - интеграция в инфраструктура
5. **Презентационни умения** - представяне на проекта

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Проектно-базирано обучение**
2. **Работа в екипи** от 3-4 ученика
3. **Case study** анализ
4. **Ролеви игри** (клиент-консултант)
5. **Peer review** и обратна връзка

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Софтуер:**
   - Конфигуратори (Dell, HP, Lenovo)
   - Spreadsheet за калкулации
   - Diagramming tools (draw.io)
   - Presentation software
   
2. **Ресурси:**
   - Vendor спецификации
   - Pricing информация
   - Best practices документи
   - Sample RFP документи
   
3. **Templates:**
   - Requirement analysis форма
   - Budget calculation spreadsheet
   - Technical specification template

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Формиране на екипи
- Раздаване на проектни задания

**Дейност на учениците:**
- Организиране в екипи
- Получаване на заданието
- Разпределение на роли

### **2. ПРЕДСТАВЯНЕ НА ПРОЕКТНОТО ЗАДАНИЕ (10 минути)**

**Сценарии за избор (всеки екип получава различен):**

**Сценарий A: Стартъп компания**
```
Профил:
- Software development firm
- 25 служители, растеж до 50 за 2 години
- Нужди: Git server, CI/CD, файлов сървър
- Бюджет: 15,000 EUR
- Критично: Бързо deployment, scalability
```

**Сценарий B: Счетоводна кантора**
```
Профил:
- 10 счетоводители
- Нужди: Database server, backup, file storage
- Regulatory compliance изисквания
- Бюджет: 10,000 EUR
- Критично: Data integrity, security, backup
```

**Сценарий C: Училище**
```
Профил:
- 500 ученици, 50 учители
- Нужди: Domain controller, file server, web
- E-learning платформа
- Бюджет: 20,000 EUR
- Критично: Reliability, ease of management
```

**Сценарий D: Медицински център**
```
Профил:
- 5 лекари, 10 персонал
- PACS система за imaging
- Patient records database
- Бюджет: 25,000 EUR
- Критично: HIPAA compliance, availability
```

### **3. МЕТОДОЛОГИЯ И ПРОЦЕС (15 минути)**

**Фази на проекта:**

#### **Фаза 1: Requirements Analysis**
```
1. Business requirements:
   - Брой потребители
   - Тип на услугите
   - Performance expectations
   - Growth projections
   
2. Technical requirements:
   - Applications и workloads
   - Storage нужди (TB, IOPS)
   - Network bandwidth
   - Uptime requirements (99.9%?)
   
3. Constraints:
   - Budget limitations
   - Physical space
   - Power и cooling
   - Expertise за поддръжка
```

#### **Фаза 2: Capacity Planning**
```
CPU калкулации:
- vCPU to pCPU ratio (4:1 typical)
- Application requirements
- Peak load considerations
- Growth buffer (20-30%)

RAM калкулации:
- Per VM/user allocation
- OS overhead
- Cache requirements
- Memory overcommit ratio

Storage калкулации:
- Raw capacity needs
- RAID overhead
- Snapshot space
- Growth rate (GB/month)
- IOPS requirements

Пример калкулация:
25 users × 2 VMs × 4GB RAM = 200GB RAM
Add 20% overhead = 240GB RAM
Round up to 256GB (8×32GB modules)
```

#### **Фаза 3: Component Selection**
```
CPU избор:
- Intel Xeon Silver/Gold/Platinum
- AMD EPYC 7003 series
- Core count vs frequency
- TDP и cooling requirements

Storage strategy:
- All-flash vs hybrid
- RAID configuration
- Hot-swap capability
- Enterprise vs consumer SSDs

Redundancy planning:
- Dual power supplies
- RAID за storage
- ECC RAM
- Hot-spare drives
- Dual NICs за teaming
```

### **4. ПРАКТИЧЕСКА РАБОТА (45 минути)**

#### **Работа по проектите (35 мин)**

**Задачи за всеки екип:**

**1. Requirement Analysis (10 мин)**
```
Попълнете формата:
┌─────────────────────────────────┐
│ REQUIREMENTS ANALYSIS FORM       │
├─────────────────────────────────┤
│ Current users: ___              │
│ Projected growth: ___           │
│ Critical applications:          │
│ 1. _______________             │
│ 2. _______________             │
│ Storage needs: ___ TB          │
│ Uptime requirement: ___%       │
│ Budget: EUR ___                │
└─────────────────────────────────┘
```

**2. Server Configuration (15 мин)**

Използвайте vendor конфигуратор:
- Dell PowerEdge Server Configurator
- HPE Server Configurator
- Lenovo Data Center Configurator

**Примерна конфигурация:**
```
Dell PowerEdge R750xs
- 2× Intel Xeon Silver 4314 (16C/32T)
- 256GB RAM (8×32GB DDR4-3200 ECC)
- 2× 480GB SSD SATA (OS, RAID 1)
- 6× 4TB HDD SAS (Data, RAID 10)
- PERC H755 RAID Controller
- Dual 800W PSU (redundant)
- iDRAC9 Enterprise
- 3Yr ProSupport
Price: ~12,000 EUR
```

**3. Диаграма на решението (5 мин)**
```
┌─────────────┐
│   Internet  │
└──────┬──────┘
       │
┌──────┴──────┐
│   Firewall  │
└──────┬──────┘
       │
┌──────┴──────┐     ┌─────────────┐
│   Switch    ├─────┤  Backup NAS │
└──────┬──────┘     └─────────────┘
       │
┌──────┴──────┐
│Main Server  │
│ ┌─────────┐ │
│ │   VMs   │ │
│ └─────────┘ │
└─────────────┘
```

**4. Budget Breakdown (5 мин)**
```
Hardware:
- Server: EUR 12,000
- UPS: EUR 1,500
- Network: EUR 800
- Rack: EUR 500
Subtotal: EUR 14,800

Software:
- Windows Server: EUR 1,200
- Backup software: EUR 500
- Antivirus: EUR 300
Subtotal: EUR 2,000

Services:
- Installation: EUR 1,000
- Training: EUR 500
Subtotal: EUR 1,500

TOTAL: EUR 18,300
Reserve: EUR 1,700 (10%)
```

#### **Презентации (10 мин)**

Всеки екип представя (2-3 мин):
1. Анализ на нуждите
2. Предложена конфигурация
3. Обосновка на избора
4. Бюджет и ROI

**Оценка от съучениците:**
- Техническа адекватност
- Съответствие с изискванията
- Cost-effectiveness
- Презентационни умения

### **5. ОБОБЩЕНИЕ И АНАЛИЗ (12 минути)**

**Сравнителен анализ на решенията:**

| Екип | CPU | RAM | Storage | Redundancy | Цена | Score |
|------|-----|-----|---------|------------|------|-------|
| A | | | | | | |
| B | | | | | | |
| C | | | | | | |
| D | | | | | | |

**Ключови изводи:**
- Balance между performance и цена
- Важността на growth planning
- Redundancy vs budget trade-offs
- Vendor lock-in съображения

**Best Practices:**
```
1. Always план за 3-5 години напред
2. Никога не използвайте 100% capacity
3. Redundancy за критични компоненти
4. Считайте TCO, не само initial cost
5. Планирайте maintenance windows
6. Документирайте всичко
```

### **6. ДОМАШНА РАБОТА (3 минути)**

**Задачи:**

1. **Финализиране на проекта:**
   - Пълна техническа спецификация (3-5 страници)
   - Детайлна диаграма на архитектурата
   - Implementation timeline
   - Risk assessment

2. **Алтернативно решение:**
   - Cloud-based алтернатива (AWS/Azure)
   - Сравнение on-premise vs cloud
   - 3-year TCO analysis

3. **Презентация:**
   - 10 слайда PowerPoint
   - Executive summary
   - Подготовка за "client meeting"

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Requirements анализ | 20% |
| Техническо решение | 25% |
| Budget планиране | 15% |
| Документация | 20% |
| Презентация | 15% |
| Екипна работа | 5% |

### ОЦЕНЪЧНА РУБРИКА:

**Отличен (6):**
- Comprehensive анализ на всички requirements
- Оптимално техническо решение с обосновка
- Точен budget с contingency
- Професионална документация
- Отлична презентация

**Много добър (5):**
- Добър анализ с малки пропуски
- Работещо решение, малки неоптималности
- Budget в рамките, basic breakdown
- Добра документация
- Ясна презентация

**Добър (4):**
- Основен анализ на главните нужди
- Функционално решение
- Budget калкулация с грешки
- Приемлива документация
- Разбираема презентация

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Успях ли да анализирам всички изисквания?
2. Оптимално ли е моето решение?
3. Реалистичен ли е бюджетът?
4. Мога ли да защитя избора си?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 100% от екипите създават работещо решение
- [ ] 90% спазват бюджета
- [ ] 85% включват подходяща redundancy
- [ ] 80% правят добра презентация
- [ ] 75% документират професионално

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: SERVER QUICK REFERENCE

**CPU Guidelines:**
```
Workload Type         | Cores | Clock | RAM/Core
---------------------|-------|-------|----------
Virtualization       | 16-32 | 2.4+  | 8-16GB
Database             | 8-16  | 3.0+  | 16-32GB
Web Server           | 4-8   | 2.8+  | 4-8GB
File Server          | 4-8   | 2.0+  | 2-4GB
Domain Controller    | 4     | 2.4+  | 8GB min

vCPU Oversubscription Ratios:
Light workload: 6:1
Medium workload: 4:1
Heavy workload: 2:1
Critical: 1:1
```

**Storage Sizing:**
```
RAID Capacity Formulas:
RAID 0: N × disk_size
RAID 1: disk_size
RAID 5: (N-1) × disk_size
RAID 6: (N-2) × disk_size
RAID 10: (N/2) × disk_size

IOPS Estimation:
SATA HDD: 75-150 IOPS
SAS HDD: 150-200 IOPS
SATA SSD: 5,000-10,000 IOPS
NVMe SSD: 100,000+ IOPS

Typical Requirements:
Exchange: 0.1 IOPS/user
SQL OLTP: 50-100 IOPS/user
VDI: 10-25 IOPS/desktop
File Server: 1-5 IOPS/user
```

### ПРИЛОЖЕНИЕ 2: BUDGET TEMPLATE

```excel
SERVER CONFIGURATION BUDGET
===========================

HARDWARE
--------
Item                    | Qty | Unit Price | Total
-----------------------|-----|------------|-------
Server Chassis         |     |            |
CPU                    |     |            |
RAM                    |     |            |
Storage - SSD          |     |            |
Storage - HDD          |     |            |
RAID Controller        |     |            |
Network Cards          |     |            |
Power Supplies         |     |            |
                       |     | Subtotal:  |

SOFTWARE
--------
Operating System       |     |            |
Virtualization         |     |            |
Backup Software        |     |            |
Monitoring             |     |            |
Security               |     |            |
                       |     | Subtotal:  |

INFRASTRUCTURE
--------------
Rack/Cabinet           |     |            |
UPS                    |     |            |
PDU                    |     |            |
Switches               |     |            |
Cables                 |     |            |
                       |     | Subtotal:  |

SERVICES
--------
Installation           |     |            |
Configuration          |     |            |
Training               |     |            |
Support Contract       |     |            |
                       |     | Subtotal:  |

TOTAL:
Contingency (10%):
GRAND TOTAL:
```

### ПРИЛОЖЕНИЕ 3: VENDOR COMPARISON

**Major Server Vendors:**
```
Dell EMC PowerEdge:
- Wide range (R250 to R950)
- iDRAC management
- OpenManage software
- Good support

HPE ProLiant:
- DL series (rack)
- ML series (tower)
- iLO management
- InfoSight AI ops

Lenovo ThinkSystem:
- SR series
- XClarity management
- Good price/performance
- TruDDR4 memory

Supermicro:
- Best price/performance
- Wide customization
- Less integrated management
- Popular for storage servers

Comparison Matrix:
              | Dell | HPE | Lenovo | Supermicro
--------------|------|-----|--------|------------
Price         | $$$ | $$$$ | $$    | $
Management    | +++  | +++  | ++    | +
Support       | +++  | +++  | ++    | +
Flexibility   | ++   | ++   | ++    | +++
Performance   | +++  | +++  | +++   | +++
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
4. Развитие на умения за техническо документиране

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- Сървърни форм-фактори: Tower, Rack (1U-4U), Blade
- Процесорни платформи: Intel Xeon, AMD EPYC
- Memory: ECC, RDIMM, LRDIMM, Persistent Memory
- Storage системи: SAS, NVMe, SAN, NAS
- Redundancy: PSU, RAID, clustering
- Управление: IPMI, iDRAC, iLO

#### Умения:
- Анализ на бизнес изисквания
- Sizing на хардуерни ресурси
- TCO (Total Cost of Ownership) калкулации
- Създаване на техническа спецификация
- Презентиране на решения
- Работа с конфигуратори на производители

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Икономика** - ROI, TCO, капиталови разходи
2. **Проектен мениджмънт** - планиране, ресурси
3. **Бази данни** - изисквания за DB сървъри
4. **Виртуализация** - VMware, Hyper-V изисквания
5. **Английски език** - техническа документация

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Проектно-базирано обучение** 
2. **Работа в екипи** по 3-4 ученика
3. **Ролева игра** - клиент и консултант
4. **Презентации** на решения
5. **Peer review** между екипите

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Онлайн ресурси:**
   - Dell PowerEdge конфигуратор
   - HPE QuickSpecs
   - Lenovo Data Center конфигуратор
   - Supermicro product selector
   
2. **Софтуер:**
   - Excel/LibreOffice за калкулации
   - Draw.io за диаграми
   - PowerPoint за презентации
   
3. **Документи:**
   - Примерни RFP (Request for Proposal)
   - Server спецификации
   - Price lists

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Разделяне на класа на 4-5 екипа
- Разпределение на сценариите
- Обяснение на задачата и критериите

**Дейност на учениците:**
- Формиране на екипи
- Избор на team leader
- Организиране на работното място

### **2. ПРЕДСТАВЯНЕ НА ПРОЕКТНАТА ЗАДАЧА (10 минути)**

**Дейност на учителя:**
- Представяне на методологията
- Обяснение на deliverables
- Timeline и milestones

**Структура на проекта:**
```
1. Анализ на изисквания (15 мин)
2. Техническо решение (25 мин)
3. Финансова калкулация (15 мин)
4. Документация (15 мин)
5. Презентации (15 мин)
```

### **3. ПРОЕКТНА РАБОТА (55 минути)**

#### **СЦЕНАРИЙ А: Малка софтуерна компания (Екип 1)**

**Бизнес изисквания:**
```
Компания: IT startup, 50 служители
Нужди:
- Domain controller и file server
- Git repository server
- CI/CD pipeline server
- Database server (PostgreSQL)
- Backup решение
Бюджет: 15,000 EUR
Растеж: 100% за 2 години
```

**Анализ и решение:**
```
Предложена конфигурация:

1. Primary Server (AD + File):
- Dell PowerEdge T440
- 2× Intel Xeon Silver 4210R
- 64GB ECC RAM (4×16GB)
- RAID controller PERC H730P
- 6× 2TB SATA (RAID 10 за data)
- 2× 480GB SSD (RAID 1 за OS)
- Dual PSU 495W
Цена: ~5,500 EUR

2. Application Server (Git + CI/CD):
- HPE ProLiant ML350 Gen10
- 1× Intel Xeon Silver 4208
- 32GB ECC RAM
- 4× 1TB SSD (RAID 10)
- Single PSU с резервен наличен
Цена: ~3,500 EUR

3. Database Server:
- Lenovo ThinkSystem ST250
- Intel Xeon E-2288G
- 64GB ECC RAM
- 2× 960GB NVMe (RAID 1)
- 4× 4TB SATA (RAID 10)
- Redundant PSU
Цена: ~4,000 EUR

4. Backup:
- Synology RS1221+
- 8× 4TB drives (RAID 6)
- 10GbE карта
Цена: ~2,000 EUR

Total: 15,000 EUR
```

#### **СЦЕНАРИЙ B: E-commerce платформа (Екип 2)**

**Бизнес изисквания:**
```
Компания: Онлайн магазин
Нужди:
- High availability web servers
- Database cluster (MySQL)
- Redis cache servers
- Elasticsearch за търсене
- 99.9% uptime SLA
Трафик: 100,000 посещения/ден
Бюджет: 30,000 EUR
```

**Анализ и решение:**
```
High Availability Architecture:

1. Web Server Cluster (2 nodes):
2× Dell PowerEdge R440
- Intel Xeon Silver 4214 (12C)
- 32GB RAM each
- 2× 480GB SSD RAID 1
- Dual PSU
- 4× 1GbE + 2× 10GbE
Цена: 8,000 EUR (total)

2. Database Cluster (2 nodes):
2× HPE ProLiant DL360 Gen10
- 2× Intel Xeon Gold 5218
- 128GB RAM each
- 4× 960GB NVMe (RAID 10)
- Dual PSU
- 2× 10GbE
Цена: 12,000 EUR (total)

3. Cache/Search Servers:
2× Supermicro 1U servers
- AMD EPYC 7302
- 64GB RAM
- 2× 480GB NVMe
Цена: 6,000 EUR (total)

4. Load Balancer:
- F5 BIG-IP Virtual Edition
- или HAProxy на dedicated server
Цена: 2,000 EUR

5. Storage:
- NetApp AFF A250
- 12× 960GB SSD
- Dual controllers
Цена: 2,000 EUR

Total: 30,000 EUR
```

#### **СЦЕНАРИЙ C: Образователна институция (Екип 3)**

**Бизнес изисквания:**
```
Училище: 500 ученици, 50 преподаватели
Нужди:
- VDI инфраструктура (Virtual Desktop)
- E-learning платформа
- Административни системи
- Student информационна система
- File storage за проекти
Бюджет: 25,000 EUR
```

**Анализ и решение:**
```
VDI-Focused Infrastructure:

1. VDI Host Servers (2 nodes):
2× Dell PowerEdge R740
- 2× Intel Xeon Gold 6230
- 256GB RAM per node
- 8× 480GB SSD (RAID 10)
- VMware vSphere Essentials Plus
- Dual 10GbE
Цена: 14,000 EUR

2. Management Server:
- HPE ProLiant DL380 Gen10
- Intel Xeon Silver 4210
- 64GB RAM
- Windows Server 2022 Datacenter
- vCenter, AD, DNS, DHCP
Цена: 4,500 EUR

3. Storage Server:
- TrueNAS system
- 128TB raw (RAID-Z2)
- 10GbE connectivity
- Backup capability
Цена: 4,500 EUR

4. Network Infrastructure:
- 48-port 10GbE switch
- Redundant 1GbE switches
Цена: 2,000 EUR

Total: 25,000 EUR

Capacity:
- 150 concurrent VDI sessions
- 3GB RAM per desktop
- Persistent desktops for teachers
- Non-persistent for students
```

#### **СЦЕНАРИЙ D: Media Production компания (Екип 4)**

**Бизнес изисквания:**
```
Видео продукция: 4K/8K content
Нужди:
- Render farm (10+ nodes)
- Shared storage (200TB+)
- Media Asset Management
- Proxy generation
- 10GbE+ network backbone
Бюджет: 50,000 EUR
```

**Анализ и решение:**
```
High-Performance Computing:

1. Render Nodes (10×):
10× Custom 2U servers
- AMD Threadripper PRO 5975WX
- 128GB RAM
- RTX 4090 или A5000
- 1TB NVMe for cache
- 10GbE networking
Цена: 35,000 EUR

2. Storage System:
- 45Drives Storinator
- 240TB raw (RAID-Z3)
- 200TB usable
- 100GbE capable
- ZFS filesystem
Цена: 10,000 EUR

3. Management Node:
- Dell Precision 7920
- Orchestration software
- Asset management
Цена: 3,000 EUR

4. Network:
- 100GbE backbone switch
- 10GbE to nodes
Цена: 2,000 EUR

Total: 50,000 EUR
```

#### **СЦЕНАРИЙ E: Healthcare клиника (Екип 5)**

**Бизнес изисквания:**
```
Медицински център: 24/7 операция
Нужди:
- PACS system (medical imaging)
- Electronic Health Records
- HIPAA compliance
- Disaster recovery
- Zero downtime tolerance
Бюджет: 40,000 EUR
```

**Анализ и решение:**
```
Mission-Critical Infrastructure:

1. Primary Cluster (2 nodes):
2× Lenovo ThinkSystem SR650
- 2× Intel Xeon Gold 6242
- 192GB RAM each
- All-Flash storage
- Dual 10GbE + FC HBA
- VMware vSphere HA
Цена: 18,000 EUR

2. Storage SAN:
- Dell EMC Unity XT 380
- 30TB All-Flash
- Dual controllers
- Encryption at rest
Цена: 12,000 EUR

3. Backup Infrastructure:
- Veeam Backup & Replication
- Dell PowerEdge R540
- 48TB capacity
- Tape library for archival
Цена: 7,000 EUR

4. DR Site (minimal):
- Colocation или cloud
- Replica server
- Real-time replication
Цена: 3,000 EUR

Total: 40,000 EUR

Compliance features:
- Encryption everywhere
- Audit logging
- Access controls
- Regular backups
- Tested DR procedures
```

### **4. ДОКУМЕНТИРАНЕ НА РЕШЕНИЯТА (15 минути)**

**Всеки екип подготвя:**

**1. Executive Summary (1 страница):**
```
- Бизнес нужди
- Предложено решение
- Ключови предимства
- ROI очаквания
- Рискове и митигация
```

**2. Техническа спецификация (2-3 страници):**
```
- Детайлна конфигурация
- Мрежова диаграма
- Capacity planning
- Growth projections
- Performance metrics
```

**3. Финансов анализ:**
```
TCO калкулация (3 години):

Initial Investment:
- Hardware: X EUR
- Software licenses: Y EUR
- Implementation: Z EUR

Operational Costs (yearly):
- Power: ~2kW × 24 × 365 × 0.15 EUR
- Cooling: +40% от power
- Support contracts: 10% от hardware
- Admin time: 0.25 FTE

Total 3-year TCO: _______ EUR
```

**4. Implementation план:**
```
Week 1-2: Procurement
Week 3: Delivery и staging
Week 4: OS и base config
Week 5: Application deployment
Week 6: Testing и migration
Week 7: Go-live
Week 8: Stabilization
```

### **5. ПРЕЗЕНТАЦИИ (15 минути)**

**Формат на презентация (3 мин на екип):**
1. Проблем и изисквания (30 сек)
2. Предложено решение (1 мин)
3. Технически highlights (1 мин)
4. Бизнес обосновка (30 сек)

**Оценяване от съучениците:**
- Техническа адекватност
- Cost-effectiveness
- Scalability
- Презентационни умения

### **6. ОБОБЩЕНИЕ И ОБРАТНА ВРЪЗКА (5 минути)**

**Дейност на учителя:**
- Коментари по решенията
- Често срещани грешки
- Best practices
- Връзка с реалния бизнес

**Ключови изводи:**
- Винаги започвайте от бизнес нуждите
- Планирайте за растеж (3-5 години)
- Redundancy струва, но downtime струва повече
- Документацията е критична

### **7. ДОМАШНА РАБОТА (0 минути - проектът е завършен)**

**Допълнителна задача (по желание):**
- Разширете вашия проект с:
  - Cloud hybrid решение
  - Kubernetes cluster design
  - Disaster recovery site
  - Green IT съображения

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Техническа адекватност на решението | 30% |
| Финансова обосновка и TCO | 20% |
| Документация качество | 20% |
| Презентационни умения | 15% |
| Екипна работа | 10% |
| Иновативност на решението | 5% |

### ОЦЕНЪЧНА РУБРИКА:

**Отличен (6):**
- Оптимално решение за нуждите
- Детайлна финансова обосновка
- Професионална документация
- Отлична презентация

**Много добър (5):**
- Добро решение с малки пропуски
- Солидна финансова част
- Добра документация
- Ясна презентация

**Добър (4):**
- Работещо решение
- Базови калкулации
- Приемлива документация
- Разбираема презентация

**Среден (3):**
- Минимално решение
- Непълни калкулации
- Слаба документация
- Неясна презентация

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли как да анализирам бизнес нужди?
2. Мога ли да конфигурирам подходящ сървър?
3. Умея ли да калкулирам TCO?
4. Готов ли съм да презентирам техническо решение?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 100% от екипите завършват проекта
- [ ] 90% предлагат работещо решение
- [ ] 85% спазват бюджета
- [ ] 80% правят качествена документация
- [ ] 75% презентират убедително

### ТИПИЧНИ ГРЕШКИ:
- Over-provisioning (твърде мощен хардуер)
- Under-sizing на storage
- Липса на redundancy
- Забравени лицензи в бюджета
- Неглижиране на растежа

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: SERVER COMPARISON MATRIX

**CPU Платформи 2025:**
```
Intel Xeon Scalable (5th Gen):
- Bronze: 8-16 cores, budget
- Silver: 8-32 cores, mainstream
- Gold: 8-56 cores, advanced
- Platinum: 8-60 cores, mission-critical

AMD EPYC (4th Gen):
- 9004 Series "Genoa"
- Up to 96 cores per socket
- 12-channel DDR5
- 128 PCIe 5.0 lanes

Cores/Socket comparison:
Intel: Max 60 cores
AMD: Max 96 cores
Ampere: Max 128 cores (ARM)
```

**Memory конфигурации:**
```
DDR4 vs DDR5 за сървъри:

DDR4-3200 ECC:
- Mature, стабилна
- По-евтина (~$5/GB)
- До 256GB DIMMs
- 25.6 GB/s per channel

DDR5-4800 ECC:
- По-висока bandwidth
- По-скъпа (~$8/GB)
- До 128GB DIMMs днес
- 38.4 GB/s per channel

Capacity sweet spots:
- Web servers: 32-64GB
- Database: 128-256GB
- Virtualization: 256-512GB
- Big Data: 1TB+
```

### ПРИЛОЖЕНИЕ 2: RAID И STORAGE КАЛКУЛАТОР

```python
def raid_calculator(disks, disk_size, raid_level):
    """
    Калкулира usable space и performance
    """
    if raid_level == 0:
        usable = disks * disk_size
        read_perf = disks
        write_perf = disks
        fault_tolerance = 0
    elif raid_level == 1:
        usable = disk_size * (disks // 2)
        read_perf = disks
        write_perf = disks // 2
        fault_tolerance = disks // 2
    elif raid_level == 5:
        usable = (disks - 1) * disk_size
        read_perf = disks
        write_perf = disks // 4
        fault_tolerance = 1
    elif raid_level == 6:
        usable = (disks - 2) * disk_size
        read_perf = disks
        write_perf = disks // 6
        fault_tolerance = 2
    elif raid_level == 10:
        usable = (disks // 2) * disk_size
        read_perf = disks
        write_perf = disks // 2
        fault_tolerance = 1
        
    return {
        'usable_space': usable,
        'read_performance': read_perf,
        'write_performance': write_perf,
        'fault_tolerance': fault_tolerance,
        'efficiency': (usable / (disks * disk_size)) * 100
    }

# Пример използване:
config = raid_calculator(8, 4000, 6)  # 8×4TB RAID 6
print(f"Usable: {config['usable_space']/1000:.1f} TB")
print(f"Efficiency: {config['efficiency']:.1f}%")
```

### ПРИЛОЖЕНИЕ 3: VENDOR QUICK REFERENCE

**Enterprise Vendors:**
```
Dell Technologies:
- PowerEdge series (R/T/M)
- VxRail (HCI)
- PowerVault (storage)
- URL: dell.com/poweredge

HPE (Hewlett Packard Enterprise):
- ProLiant DL/ML series
- Apollo (HPC)
- Synergy (Blade)
- URL: hpe.com/servers

Lenovo:
- ThinkSystem SR series
- ThinkAgile (HCI)
- URL: lenovo.com/datacenter

Supermicro:
- Wide variety, customizable
- Good price/performance
- URL: supermicro.com

Cisco:
- UCS B-Series (Blade)
- UCS C-Series (Rack)
- HyperFlex (HCI)
- URL: cisco.com/go/ucs
```

**Budget Alternatives:**
```
Refurbished/Off-lease:
- Dell R730/R740 (previous gen)
- HPE DL380 Gen9/Gen10
- 50-70% cost savings
- Vendors: ServerMonkey, SaveMyServer

Whitebox builds:
- Supermicro barebones
- ASRock Rack motherboards
- Standard ATX components
- 30-40% cost savings
- Less support
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
