# УРОЧЕН ПЛАН №25
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XI КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** 128-мо СУ "Алберт Айнщайн", гр.София
- **Клас:** XI клас
- **Учител:** Мариян Йорданов
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Linux файлова система и права за достъп
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Упражнение
- **Място на провеждане:** Компютърен кабинет

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Да познават структурата на Linux файловата система (FHS)
2. Да разбират системата за права (permissions)
3. Да могат да променят права с chmod
4. Да разбират концепцията за собственик и група
5. Да използват chown и chgrp команди

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:
- FHS (Filesystem Hierarchy Standard)
- Важни директории: /, /home, /etc, /var, /tmp, /usr, /bin
- Права за достъп: read (r), write (w), execute (x)
- Собственик, група, други (owner, group, others)
- chmod - symbolic и numeric режими
- chown, chgrp команди
- umask

---

## 5. ХОД НА УРОКА

### **3. НОВ МАТЕРИАЛ (40 минути)**

#### **Част 1: Linux Filesystem Hierarchy (12 мин)**

```
/                           # Root - коренът на всичко
├── bin/                    # Essential binaries (ls, cp, cat...)
├── boot/                   # Boot loader files, kernel
├── dev/                    # Device files (sda, tty...)
├── etc/                    # Configuration files
│   ├── passwd              # User accounts
│   ├── shadow              # Encrypted passwords
│   ├── hosts               # Static hostname resolution
│   └── fstab               # Filesystem mount table
├── home/                   # User home directories
│   ├── user1/
│   └── user2/
├── lib/                    # Essential shared libraries
├── media/                  # Mount point for removable media
├── mnt/                    # Temporary mount point
├── opt/                    # Optional/third-party software
├── proc/                   # Virtual filesystem (process info)
├── root/                   # Root user's home directory
├── sbin/                   # System binaries (admin commands)
├── srv/                    # Service data
├── sys/                    # Virtual filesystem (system info)
├── tmp/                    # Temporary files (cleared on reboot)
├── usr/                    # User programs
│   ├── bin/                # User binaries
│   ├── lib/                # Libraries
│   ├── local/              # Locally compiled software
│   └── share/              # Shared data
└── var/                    # Variable data
    ├── log/                # Log files
    ├── mail/               # Mail storage
    └── www/                # Web server files
```

**Ключови директории:**
```
/etc    - Конфигурации (Edit To Configure)
/home   - Потребителски файлове
/var    - Променящи се данни (логове, бази данни)
/tmp    - Временни файлове
/usr    - Програми и библиотеки
/root   - Home на root потребителя
```

#### **Част 2: Permissions - Права за достъп (15 мин)**

**Трите типа права:**
```
r (read)    = 4  - четене на съдържание
w (write)   = 2  - промяна на съдържание
x (execute) = 1  - изпълнение (за файлове) / достъп (за директории)

За директории:
r = list съдържанието (ls)
w = създаване/изтриване на файлове вътре
x = влизане в директорията (cd)
```

**Трите категории:**
```
Owner (u)  - собственик на файла
Group (g)  - група на файла
Others (o) - всички останали

ls -l изход:
-rwxr-xr-- 1 user group 1024 Jan 15 10:30 file.txt
│├─┤├─┤├─┤
│ │  │  └── Others: r-- (само четене)
│ │  └── Group: r-x (четене и изпълнение)
│ └── Owner: rwx (всички права)
└── Тип: - (файл), d (directory), l (link)
```

**chmod - промяна на права:**

```bash
# Symbolic mode (символен)
chmod u+x file.txt      # Добави execute за owner
chmod g-w file.txt      # Премахни write за group
chmod o=r file.txt      # Задай само read за others
chmod a+x script.sh     # Добави execute за всички (all)
chmod u+rwx,g+rx,o+r file.txt   # Комбинация

# Numeric mode (числен) - по-бърз
chmod 755 file.txt      # rwxr-xr-x
chmod 644 file.txt      # rw-r--r--
chmod 700 private.txt   # rwx------
chmod 777 public.txt    # rwxrwxrwx (опасно!)

# Изчисляване:
# r=4, w=2, x=1
# rwx = 4+2+1 = 7
# r-x = 4+0+1 = 5
# r-- = 4+0+0 = 4

# 755 означава:
# Owner: 7 = rwx
# Group: 5 = r-x
# Others: 5 = r-x
```

**Таблица с права:**
```
Число  Binary  Права
0      000     ---
1      001     --x
2      010     -w-
3      011     -wx
4      100     r--
5      101     r-x
6      110     rw-
7      111     rwx
```

#### **Част 3: Собственост (8 мин)**

```bash
# Промяна на собственик
chown newowner file.txt
chown newowner:newgroup file.txt   # Собственик и група
chown -R user:group directory/     # Рекурсивно

# Промяна на група
chgrp newgroup file.txt
chgrp -R newgroup directory/

# Преглед
ls -l file.txt
# -rw-r--r-- 1 owner group 1024 Jan 15 10:30 file.txt
```

#### **Част 4: Специални права (5 мин)**

```bash
# SUID (Set User ID) - изпълни като собственик
chmod u+s program        # или chmod 4755 program
ls -l: -rwsr-xr-x
# Пример: /usr/bin/passwd - обикновен user променя паролата си

# SGID (Set Group ID) - изпълни като група
chmod g+s directory      # или chmod 2755 directory
# Нови файлове наследяват групата на директорията

# Sticky bit - само собственикът може да трие
chmod +t /tmp           # или chmod 1777 /tmp
ls -l: drwxrwxrwt
```

---

### **4. ПРАКТИЧЕСКА РАБОТА (30 минути)**

**Задача 1: Изследване на файловата система**
```bash
# Разгледайте важни директории
ls /
ls /etc | head -20
ls /home
ls -la /tmp

# Намерете конфигурационни файлове
cat /etc/hostname
cat /etc/passwd | head -5
```

**Задача 2: Работа с права**
```bash
cd ~
mkdir permissions_lab
cd permissions_lab

# Създайте файлове
touch private.txt public.txt script.sh
echo "Private data" > private.txt
echo "Public data" > public.txt
echo "#!/bin/bash" > script.sh
echo "echo Hello" >> script.sh

# Задайте права
chmod 600 private.txt    # Само собственикът чете/пише
chmod 644 public.txt     # Всички четат, собственик пише
chmod 755 script.sh      # Изпълним скрипт

# Проверете
ls -l
./script.sh              # Изпълнете скрипта
```

**Задача 3: Декодиране на права**
```
Преобразувайте:
1. rwxr-xr-- = _____ (числено)
2. 640 = __________ (символно)
3. rw-rw-r-- = _____
4. 711 = __________
```

---

### **5. ОБОБЩЕНИЕ (8 минути)**

```
КЛЮЧОВИ ТОЧКИ:

1. / е коренът на файловата система
2. /home - потребителски файлове, /etc - конфигурации
3. rwx права: read(4), write(2), execute(1)
4. chmod 755 = rwxr-xr-x
5. chown променя собственик, chgrp - група
6. 644 = стандартни права за файл
7. 755 = стандартни права за директория/скрипт
```

---

### **6. ДОМАШНА РАБОТА**

1. Създайте директория с три файла с различни права
2. Обяснете какво означава chmod 750
3. Изследвайте правата в /etc - какви са и защо?

---

## 7. ПРИЛОЖЕНИЯ

### CHMOD СПРАВОЧНИК

```
Типични права:
644 - обикновен файл (rw-r--r--)
755 - директория/скрипт (rwxr-xr-x)
600 - частен файл (rw-------)
700 - частна директория (rwx------)
777 - достъп за всички (опасно!)
```

### SYMBOLIC MODE СПРАВОЧНИК

```
u = user (owner)
g = group
o = others
a = all

+ = добави
- = премахни
= = задай точно

Примери:
chmod u+x file    # добави x за owner
chmod go-w file   # премахни w за group и others
chmod a=r file    # задай само r за всички
```

---

**Изготвил:** Мариян Йорданов  
**Дата на изготвяне:** Януари 2025 г.
