# УРОЧЕН ПЛАН №32
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XI КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** 128-мо СУ "Алберт Айнщайн", гр.София
- **Клас:** XI клас
- **Учител:** Мариян Йорданов
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Управление на дисково пространство
- **Дата:** ____________
- **Продължителност:** 90 минути
- **Тип урок:** Упражнение

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Да могат да анализират използването на дисково пространство
2. Да управляват дялове и томове
3. Да използват инструменти за дискова диагностика
4. Да разбират RAID концепции (въведение)

---

## 5. ХОД НА УРОКА

### **НОВ МАТЕРИАЛ (35 минути)**

#### **Анализ на дисково пространство:**

**Linux команди:**
```bash
# Използване на дялове
df -h                     # Human-readable
df -Th                    # С тип на FS

# Използване по директории
du -sh /home/*            # Размер на директории
du -sh * | sort -h        # Сортирано по размер
du -h --max-depth=1       # Само първо ниво

# Намиране на големи файлове
find / -type f -size +100M 2>/dev/null
find /home -type f -size +50M -exec ls -lh {} \;

# ncdu - интерактивен инструмент
ncdu /home
```

**Windows команди и инструменти:**
```powershell
# PowerShell
Get-PSDrive -PSProvider FileSystem
Get-ChildItem C:\ -Recurse | 
    Measure-Object -Property Length -Sum

# TreeSize, WinDirStat - GUI инструменти

# Disk Cleanup
cleanmgr

# Storage Sense (Windows 10/11)
Settings → System → Storage
```

#### **Управление на дялове:**

**Linux (fdisk, parted):**
```bash
# Преглед на дялове
sudo fdisk -l
sudo parted -l
lsblk

# Интерактивно управление
sudo fdisk /dev/sdX
# n - нов дял
# d - изтрий дял
# p - покажи дялове
# w - запиши и излез

# parted (поддържа GPT)
sudo parted /dev/sdX
# mklabel gpt
# mkpart primary ext4 0% 100%
```

**Windows:**
```
Disk Management:
Win + R → diskmgmt.msc

Операции:
├── Shrink Volume (намали)
├── Extend Volume (разшири)
├── New Simple Volume
├── Delete Volume
├── Format
└── Change Drive Letter

DiskPart (command line):
diskpart
list disk
select disk 0
list partition
create partition primary size=10000
format fs=ntfs quick
assign letter=E
```

#### **Квоти:**

**Linux:**
```bash
# Включване на квоти в /etc/fstab
# /dev/sda1 /home ext4 defaults,usrquota,grpquota 0 2

# Създаване на quota файлове
sudo quotacheck -cug /home
sudo quotaon /home

# Задаване на квота
sudo edquota -u username
# soft limit, hard limit

# Преглед
quota -u username
repquota /home
```

**Windows:**
```
Disk Management → Properties → Quota
- Enable quota management
- Limit disk space to: X GB
- Set warning level at: Y GB
```

---

### **ПРАКТИЧЕСКА РАБОТА (35 минути)**

**Задача 1: Анализ на дисково пространство**
```bash
# Linux
df -h
du -sh /var/*
find /home -type f -size +10M 2>/dev/null | head -10

# Windows PowerShell
Get-PSDrive C
Get-ChildItem C:\Users -Recurse -ErrorAction SilentlyContinue | 
    Sort-Object Length -Descending | 
    Select-Object FullName, Length -First 20
```

**Задача 2: Почистване**
```bash
# Linux
sudo apt clean                    # apt cache
sudo journalctl --vacuum-time=7d  # стари логове
rm -rf ~/.cache/thumbnails/*      # thumbnails

# Windows
cleanmgr /d C
# Settings → Storage → Temporary files
```

---

### **ОБОБЩЕНИЕ**

```
КЛЮЧОВИ ТОЧКИ:

1. df показва използване на дялове
2. du показва използване по директории
3. fdisk/parted за управление на дялове в Linux
4. Disk Management за Windows
5. Квотите ограничават дисковото пространство по потребител
6. Редовно почистване предотвратява препълване
```

---

### **ДОМАШНА РАБОТА**

1. Намерете 5-те най-големи файла на вашия компютър
2. Колко свободно място има на всеки дял?
3. Почистете временни файлове и запишете освободеното място

---

**Изготвил:** Мариян Йорданов  
**Дата на изготвяне:** Януари 2025 г.
