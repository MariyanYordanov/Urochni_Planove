# УРОЧЕН ПЛАН №9
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XI КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** 128-мо СУ "Алберт Айнщайн", гр.София
- **Клас:** XI клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Многоядрена технология и 64-битови процесори
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Комбиниран
- **Място на провеждане:** Компютърен кабинет

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат концепцията за многоядрени процесори
2. Да усвоят разликите между 32-битова и 64-битова архитектура
3. Да познават технологии като SMT/Hyper-Threading
4. Да разбират паралелното изпълнение и thread scheduling
5. Да могат да оценяват ефективността на многоядрените системи

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на разбиране за паралелна обработка
2. Възпитаване на системно мислене
3. Развиване на интерес към съвременни процесорни технологии
4. Изграждане на навици за оптимално използване на ресурси

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за анализ на паралелни задачи
2. Усъвършенстване на разбирането за софтуерна оптимизация
3. Формиране на способности за избор на хардуер
4. Развитие на компетенции за системна администрация

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- Еволюция от single-core към many-core процесори
- Архитектурни подходи: SMP, NUMA, big.LITTLE
- 64-битови разширения: x86-64, AMD64, Intel 64
- Hyper-Threading и SMT технологии
- Thread scheduling и CPU affinity
- Amdahl's Law и паралелна ефективност

#### Умения:
- Мониторинг на core/thread utilization
- Конфигуриране на CPU affinity
- Анализ на multi-threaded производителност
- Избор между 32-bit и 64-bit системи
- Оптимизация на приложения за multi-core

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Програмиране** - паралелно програмиране, threads
2. **Операционни системи** - процеси, нишки, scheduling
3. **Математика** - паралелни алгоритми, графи
4. **Физика** - квантови ефекти, термодинамика
5. **История на технологиите** - еволюция на процесорите

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Визуална презентация** с анимации на core работа
2. **Демонстрация** на task manager и affinity
3. **Практическа работа** с benchmark софтуер
4. **Експерименти** с single vs multi-thread
5. **Сравнителен анализ** на различни архитектури

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Хардуер:**
   - Компютри с multi-core процесори
   - Различни CPU за демонстрация
   
2. **Софтуер:**
   - Task Manager, Process Explorer
   - CPU-Z, Core Temp
   - Cinebench R23, Geekbench
   - Prime95, HandBrake
   - VMware/VirtualBox
   
3. **Учебни материали:**
   - Диаграми на CPU архитектури
   - Таблици за сравнение
   - Графики на scaling ефективност

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Подготовка на системите
- Мотивиращ въпрос: "Защо телефонът ви има 8 ядра, но не е 8 пъти по-бърз от стар single-core?"

**Дейност на учениците:**
- Подготовка за работа
- Дискусия за паралелизъм

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (8 минути)**

**Дейност на учителя:**
- Преговор на CPU основи

**Въпроси за преговор:**
1. Какво е процесорно ядро?
2. Как се изпълняват инструкциите?
3. Какво е процес и нишка?
4. Защо има лимит на честотата?

**Демонстрация:**
```
Task Manager → Performance → CPU
- Показване на cores и logical processors
- Наблюдение на individual core usage
- Демонстрация на thread migration
```

### **3. НОВ МАТЕРИАЛ (45 минути)**

#### **Част 1: Еволюция към многоядрени процесори (12 мин)**

**История и причини:**
```
Timeline на развитие:
1971: Intel 4004 - Single-core, 740 kHz
1985: Intel 386 - 32-bit, до 40 MHz
2000: Pentium 4 - Peak на честотата (~4 GHz)
2005: Pentium D - Първи dual-core x86
2006: Core 2 Duo - True dual-core
2017: Threadripper - 16 cores mainstream
2023: Threadripper 7995WX - 96 cores!

Защо multi-core вместо по-висока честота?
- Power wall: P = CV²f
- Memory wall: RAM не може да следва
- ILP wall: Instruction-level parallelism limit
```

**Архитектурни подходи:**

**SMP (Symmetric Multi-Processing):**
```
┌─────────────────────────────────┐
│         Shared Memory            │
├─────┬─────┬─────┬─────┬─────┐  │
│Core0│Core1│Core2│Core3│ ... │  │
├─────┴─────┴─────┴─────┴─────┤  │
│         Shared L3 Cache         │
└─────────────────────────────────┘

Характеристики:
✓ Всички ядра равноправни
✓ Споделена памет и cache
✓ Uniform Memory Access
✗ Scalability проблеми >8 cores
```

**NUMA (Non-Uniform Memory Access):**
```
┌──────────┐    ┌──────────┐
│  Node 0  │────│  Node 1  │
│ 4 Cores  │QPI │ 4 Cores  │
│ Local RAM│    │ Local RAM│
└──────────┘    └──────────┘

AMD Infinity Fabric / Intel QPI:
- Local memory: Fast access
- Remote memory: Slower access
- Better scalability
```

**big.LITTLE / Intel P+E cores:**
```
ARM big.LITTLE → Intel Alder Lake

Performance cores (P-cores):
- Сложни, мощни
- Out-of-order, wide execution
- За single-thread performance

Efficiency cores (E-cores):
- Прости, ефективни
- In-order или narrow OoO
- За background tasks

Thread Director:
- Hardware scheduler hints
- OS awareness (Windows 11)
```

#### **Част 2: 64-битова архитектура (13 мин)**

**32-bit vs 64-bit:**

```
32-bit (x86) лимитации:
- 4GB RAM максимум (2³² bytes)
- По-малки регистри
- Limited instruction set
- PAE workarounds за >4GB

64-bit (x86-64/AMD64) предимства:
- 16 EB теоретичен лимит (2⁶⁴)
- 48-bit физически адрес (256TB)
- 16 general-purpose регистри (vs 8)
- Нови SIMD инструкции
- Mandatory SSE2
```

**Регистри и разширения:**
```
32-bit регистри → 64-bit регистри:
EAX → RAX (64-bit)
EBX → RBX
ECX → RCX
...
Нови: R8-R15

Pointer размери:
32-bit: 4 bytes per pointer
64-bit: 8 bytes per pointer

Влияние върху паметта:
~30% повече RAM usage за същата програма!
```

**Съвместимост:**
```
64-bit CPU може:
✓ 64-bit OS + 64-bit apps
✓ 64-bit OS + 32-bit apps (WoW64)
✓ 32-bit OS + 32-bit apps
✗ 32-bit OS + 64-bit apps

Проверка на системата:
Windows: System Information → System Type
Linux: uname -m (x86_64 = 64-bit)
```

**Performance разлики:**
```python
# Пример: Обработка на голям масив
# 32-bit: множество memory accesses
# 64-bit: по-малко iterations

# Encryption/Compression:
# 64-bit: 2-3x по-бърз за някои операции

# Gaming:
# Minimal разлика освен за >4GB RAM
```

#### **Част 3: SMT/Hyper-Threading (10 мин)**

**Концепция на SMT:**
```
Simultaneous Multi-Threading (SMT)
Intel: Hyper-Threading (HT)
AMD: SMT

1 Physical Core → 2 Logical Cores

Споделени ресурси:
- Execution units
- Cache памет
- Branch predictors

Дублирани ресурси:
- Architectural state
- Register sets
- Instruction pointers
```

**Как работи:**
```
Without HT:          With HT:
Cycle Core           Cycle Core
1     Thread1        1     Thread1+Thread2
2     [Stall]        2     Thread2
3     Thread1        3     Thread1+Thread2
4     [Stall]        4     Thread1
5     Thread1        5     Thread1+Thread2

Използване на "празни" цикли
15-30% performance gain typically
```

**Кога е ефективен:**
```
Добре работи за:
✓ Mixed integer/float операции
✓ Memory-bound задачи
✓ I/O intensive работа
✓ Различни instruction mix

Не помага при:
✗ Purely compute-bound
✗ Идентични threads
✗ Cache-sensitive работа
```

#### **Част 4: Паралелна ефективност (10 мин)**

**Amdahl's Law:**
```
Speedup = 1 / ((1-P) + P/N)

Където:
P = Parallel portion (0 до 1)
N = Number of processors

Пример:
90% паралелизируема програма (P=0.9)
N=2: Speedup = 1.82x (91% efficiency)
N=4: Speedup = 3.08x (77% efficiency)
N=8: Speedup = 4.71x (59% efficiency)
N=∞: Speedup = 10x максимум!
```

**Scaling ефективност:**
```
Ideal vs Real scaling:

Cores  Ideal  Typical  Gaming
1      1.0x   1.0x     1.0x
2      2.0x   1.8x     1.3x
4      4.0x   3.2x     1.5x
8      8.0x   5.5x     1.6x
16     16.0x  9.0x     1.65x

Причини за загуби:
- Serial portions (Amdahl)
- Synchronization overhead
- Cache contention
- Memory bandwidth
- Thermal limits
```

**CPU Affinity:**
```
Закачане на процес към specific cores:

Windows:
- Task Manager → Details → Set Affinity
- start /affinity FF program.exe

Linux:
- taskset -c 0-3 ./program
- numactl --cpunodebind=0

Приложения:
- Изолиране на критични процеси
- Избягване на cache pollution
- NUMA optimization
- Latency-sensitive задачи
```

### **4. ЗАТВЪРЖДАВАНЕ (25 минути)**

#### **Практическа работа: Multi-core тестване**

**Задача 1: Core Scaling тест (10 мин)**

**Cinebench R23 тестване:**
```
Процедура:
1. Отворете Cinebench R23
2. Advanced Options → CPU (Multi Core)
3. File → Preferences → Advanced Benchmark
4. Задайте различен брой threads:

Тестове:
- 1 thread (single-core)
- 2 threads
- 4 threads
- All threads

Запишете резултатите:
```

| Threads | Score | Scaling | Efficiency |
|---------|-------|---------|------------|
| 1 | | 1.0x | 100% |
| 2 | | | |
| 4 | | | |
| All | | | |

**Задача 2: Process Affinity (8 мин)**

**Експеримент с CPU affinity:**
```
1. Стартирайте CPU-intensive програма
   (Prime95 или CPU-Z bench)

2. Task Manager → Details → Set Affinity
   - Тест 1: Само Core 0
   - Тест 2: Cores 0-3
   - Тест 3: All cores

3. Наблюдавайте:
   - Performance разлика
   - Temperature per core
   - Clock speeds

4. Опитайте с 2 програми:
   - Program A: Cores 0-3
   - Program B: Cores 4-7
   - Сравнете с двете на all cores
```

**Задача 3: 32-bit vs 64-bit (7 мин)**

**Сравнителен тест:**
```
Ако имате 32-bit и 64-bit версии:

1. 7-Zip Benchmark:
   - 32-bit версия: Tools → Benchmark
   - 64-bit версия: Tools → Benchmark
   - Сравнете MIPS резултатите

2. Memory usage сравнение:
   - Отворете същата програма в двете версии
   - Task Manager → Memory usage
   - Изчислете % разлика

3. Large Address Aware test:
   - Програма с >2GB RAM нужда
   - Работи ли в 32-bit?
```

### **5. ОБОБЩЕНИЕ (10 минути)**

**Ключови концепции:**
```
Multi-core не означава автоматично N× performance
- Зависи от паралелизацията
- Ограничения от Amdahl's Law
- Overhead от synchronization

64-bit е стандарт за модерни системи
- Повече RAM достъп
- По-добра performance за някои задачи
- Compatibility слой за legacy software

SMT/HT е "безплатна" performance
- 15-30% gain в подходящи задачи
- Почти без extra power/heat
```

**Въпроси за дискусия:**
1. Защо gaming не се подобрява много от повече ядра?
2. Има ли смисъл от 128-core desktop CPU?
3. Кога би избрал 32-bit система днес?
4. Защо някои изключват Hyper-Threading?

**Best practices:**
```
За gaming:
- 6-8 cores достатъчно за 2025
- High single-thread > many cores
- HT/SMT обикновено ON

За productivity:
- Колкото повече cores, толкова по-добре
- NUMA-aware за >16 cores
- Process affinity за критични задачи

За servers:
- Core count според workload
- Consider disable HT за security
- NUMA optimization critical
```

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задачи:**

1. **Паралелизация анализ:**
   - Изберете 5 програми които използвате
   - Проверете core utilization при работа
   - Категоризирайте: single/lightly/heavily threaded
   - График и анализ (2 страници)

2. **Изследователска:**
   - Проучете ARM big.LITTLE технологията
   - Сравнете с Intel P+E cores
   - Предимства и недостатъци
   - 2 страници есе

3. **Практическа:**
   - Напишете прост Python/C++ код
   - Версия 1: Sequential
   - Версия 2: Parallel (threading)
   - Измерете speedup за различен брой threads

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Разбиране на multi-core концепции | 25% |
| Познаване на 64-bit архитектура | 20% |
| Практическа работа с affinity | 20% |
| Анализ на scaling ефективност | 15% |
| Интерпретация на резултати | 15% |
| Активност | 5% |

### ОЦЕНЪЧНА РУБРИКА:
- **Отличен (6):** Отлично разбира паралелизъм, прави точен анализ на scaling
- **Много добър (5):** Добро разбиране, малки грешки в изчисленията
- **Добър (4):** Основни познания, нуждае се от помощ при анализ
- **Среден (3):** Минимални знания, трудности с концепциите

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли защо повече ядра ≠ пропорционално по-бързо?
2. Мога ли да обясня предимствата на 64-bit?
3. Знам ли кога HT/SMT помага и кога не?
4. Умея ли да оптимизирам process affinity?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 90% разбират Amdahl's Law влиянието
- [ ] 85% могат да обяснят 64-bit предимства
- [ ] 80% разбират SMT концепцията
- [ ] 75% могат да анализират core scaling

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: CPU АРХИТЕКТУРИ 2025

**Desktop процесори:**
```
Intel Core i9-14900K:
- 8 P-cores + 16 E-cores
- 32 threads total
- P: 6.0 GHz, E: 4.4 GHz

AMD Ryzen 9 7950X:
- 16 cores (2× CCD)
- 32 threads (SMT)
- Up to 5.7 GHz boost

Apple M3 Max:
- 12 P-cores + 4 E-cores
- No SMT
- Unified memory architecture
```

**Server/HEDT:**
```
AMD EPYC 9754:
- 128 cores / 256 threads
- 256MB L3 cache
- 12-channel DDR5

Intel Xeon Max 9480:
- 56 cores / 112 threads
- 64GB HBM2e on-package
- 8-channel DDR5
```

### ПРИЛОЖЕНИЕ 2: BENCHMARK КОМАНДИ

**Windows testing:**
```powershell
# CPU cores info
wmic cpu get NumberOfCores,NumberOfLogicalProcessors

# Set affinity via PowerShell
$Process = Get-Process "processname"
$Process.ProcessorAffinity = 0xF  # Cores 0-3

# Measure execution time
Measure-Command { Your-Command }
```

**Linux testing:**
```bash
# CPU topology
lscpu -e

# Run on specific cores
taskset -c 0-3 ./program

# Monitor per-core usage
mpstat -P ALL 1

# NUMA statistics
numastat

# Benchmark with isolation
isolcpus=4-7  # Boot parameter
taskset -c 4-7 nice -n -20 ./bench
```

### ПРИЛОЖЕНИЕ 3: ПАРАЛЕЛИЗАЦИЯ ПРИМЕР

**Python multiprocessing:**
```python
import multiprocessing as mp
import time

def worker(n):
    """CPU-intensive task"""
    total = 0
    for i in range(n):
        total += i ** 2
    return total

# Sequential version
def sequential(iterations, count):
    start = time.time()
    results = [worker(iterations) for _ in range(count)]
    return time.time() - start

# Parallel version
def parallel(iterations, count):
    start = time.time()
    with mp.Pool() as pool:
        results = pool.map(worker, [iterations] * count)
    return time.time() - start

# Test
if __name__ == "__main__":
    iterations = 10_000_000
    tasks = 8
    
    seq_time = sequential(iterations, tasks)
    par_time = parallel(iterations, tasks)
    
    print(f"Sequential: {seq_time:.2f}s")
    print(f"Parallel: {par_time:.2f}s")
    print(f"Speedup: {seq_time/par_time:.2f}x")
    print(f"Efficiency: {(seq_time/par_time)/mp.cpu_count():.1%}")
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
