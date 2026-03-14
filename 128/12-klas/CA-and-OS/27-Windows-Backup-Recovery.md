# УРОЧЕН ПЛАН №15
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
| **Тема на урока:** | Linux потребители, групи и sudo управление |
| **Дата:** | ____________ |
| **Час:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Упражнение |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разбират системата за потребители и групи в Linux
2. Да усвоят командите за управление на потребители (useradd, usermod, userdel)
3. Да могат да създават и управляват групи (groupadd, groupmod, groupdel)
4. Да конфигурират sudo достъп за потребители
5. Да разбират файловете /etc/passwd, /etc/shadow, /etc/group

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на отговорност при работа с административни права
2. Развиване на разбиране за принципа на минималните привилегии
3. Изграждане на осъзнатост за системна сигурност
4. Насърчаване на документиране на административни действия

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на практически умения за системна администрация
2. Усъвършенстване на работа с командния ред
3. Формиране на troubleshooting умения
4. Развитие на логическо мислене при управление на права

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**Концепции за потребители:**
- UID (User ID) и GID (Group ID)
- Root потребител (UID 0)
- Системни vs обикновени потребители
- Home директории и login shell

**Файлове за конфигурация:**
- /etc/passwd - информация за потребители
- /etc/shadow - криптирани пароли
- /etc/group - информация за групи
- /etc/sudoers - sudo конфигурация

**Команди за управление:**
- useradd, usermod, userdel
- groupadd, groupmod, groupdel
- passwd, chage
- sudo, visudo

### ОСНОВНИ УМЕНИЯ:
- Създаване и премахване на потребители
- Управление на групи и членство
- Конфигуриране на sudo достъп
- Проверка и промяна на пароли

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Информационна сигурност** - контрол на достъпа, криптиране на пароли
2. **Програмиране** - shell скриптове за автоматизация
3. **Мрежови технологии** - отдалечен достъп и SSH
4. **Бази данни** - структура на системните файлове

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Демонстрация с обяснение
2. Практически упражнения стъпка по стъпка
3. Самостоятелна работа с наблюдение
4. Решаване на практически сценарии
5. Дискусия на best practices

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Компютри с Ubuntu 24.04 LTS (VM или native)
- Терминален достъп с root права
- Работни листове (Приложение 1)
- Справочник с команди (Приложение 2)
- Презентация "Linux User Management"

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Стартиране на Ubuntu VM
- Цели на урока

**Мотивиращ въпрос:**
"В корпоративна среда с 500 служители, как се управляват техните акаунти на Linux сървърите?"

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Преговор:**
```bash
# Въпроси от предходни уроци:
# 1. Какво е root потребител?
# 2. Каква е командата за показване на текущия потребител?
whoami

# 3. Как се сменят правата на файл?
chmod 755 file.txt

# 4. Какво означава rwx?
# r = read (4), w = write (2), x = execute (1)
```

---

### **3. НОВ МАТЕРИАЛ И ПРАКТИКА (55 минути)**

#### **Част 1: Структура на потребителската система (10 минути)**

**Теория - UID и GID:**
```
Linux потребителска йерархия:
├── root (UID 0) - суперпотребител
├── Системни потребители (UID 1-999)
│   ├── daemon, bin, sys, sync...
│   └── Използват се от услуги
└── Обикновени потребители (UID 1000+)
    └── Реални хора
```

**Практика 1.1: Преглед на /etc/passwd**
```bash
# Структура на /etc/passwd
cat /etc/passwd

# Формат на ред:
# username:x:UID:GID:comment:home:shell
# Пример:
# student:x:1000:1000:Student User:/home/student:/bin/bash

# Преглед на конкретен потребител
grep "^student" /etc/passwd

# Брой потребители в системата
wc -l /etc/passwd
```

**Практика 1.2: Преглед на /etc/shadow**
```bash
# Само root може да чете
sudo cat /etc/shadow

# Формат:
# username:password_hash:last_change:min:max:warn:inactive:expire

# Проверка на хеширания алгоритъм
# $6$ = SHA-512
# $5$ = SHA-256
# $1$ = MD5 (остарял)
```

**Практика 1.3: Преглед на /etc/group**
```bash
# Структура на /etc/group
cat /etc/group

# Формат:
# groupname:x:GID:members

# Групи на текущия потребител
groups
id
```

---

#### **Част 2: Създаване на потребители (15 минути)**

**Команда useradd:**
```bash
# Синтаксис
useradd [опции] username

# Основни опции:
# -m    Създава home директория
# -d    Указва home директория
# -s    Указва shell
# -g    Основна група
# -G    Допълнителни групи
# -c    Коментар (пълно име)
# -e    Дата на изтичане
# -u    Конкретен UID
```

**Практика 2.1: Създаване на потребител**
```bash
# Създаване на прост потребител
sudo useradd -m -s /bin/bash -c "Test User" testuser

# Проверка
grep testuser /etc/passwd
ls -la /home/testuser

# Задаване на парола
sudo passwd testuser
# Въведете: Test@2025

# Алтернатива - adduser (по-интерактивен)
sudo adduser testuser2
```

**Практика 2.2: Създаване на потребител с опции**
```bash
# Създаване с конкретни параметри
sudo useradd -m \
  -d /home/developer \
  -s /bin/bash \
  -g developers \
  -G sudo,docker \
  -c "Senior Developer" \
  -e 2025-12-31 \
  devuser

# Първо трябва да създадем групата developers
sudo groupadd developers

# След това потребителя
sudo useradd -m -d /home/developer -s /bin/bash -g developers -c "Senior Developer" devuser
sudo passwd devuser
```

**Практика 2.3: Промяна на потребител (usermod)**
```bash
# Промяна на shell
sudo usermod -s /bin/zsh testuser

# Добавяне към група (append!)
sudo usermod -aG sudo testuser

# Промяна на home директория
sudo usermod -d /home/newdir -m testuser

# Заключване на акаунт
sudo usermod -L testuser

# Отключване
sudo usermod -U testuser

# Промяна на username
sudo usermod -l newname oldname
```

**Практика 2.4: Изтриване на потребител**
```bash
# Изтриване без home директория
sudo userdel testuser

# Изтриване с home директория
sudo userdel -r testuser2

# Проверка
grep testuser /etc/passwd
ls /home/
```

---

#### **Част 3: Управление на групи (10 минути)**

**Команди за групи:**
```bash
# Създаване на група
sudo groupadd developers
sudo groupadd -g 2000 admins    # с конкретен GID

# Промяна на група
sudo groupmod -n newname oldname    # преименуване
sudo groupmod -g 2001 admins        # промяна на GID

# Изтриване на група
sudo groupdel developers

# Преглед на групи
cat /etc/group
getent group developers
```

**Практика 3.1: Създаване на групова структура**
```bash
# Сценарий: IT отдел с няколко екипа

# Създаване на групи
sudo groupadd itdept
sudo groupadd webdevs
sudo groupadd sysadmins
sudo groupadd dbadmins

# Създаване на потребители и добавяне към групи
sudo useradd -m -G itdept,webdevs -c "Web Developer 1" webdev1
sudo useradd -m -G itdept,sysadmins -c "System Admin 1" sysadmin1
sudo useradd -m -G itdept,dbadmins -c "DBA 1" dba1

# Задаване на пароли
echo "webdev1:WebDev@2025" | sudo chpasswd
echo "sysadmin1:SysAdmin@2025" | sudo chpasswd
echo "dba1:DBA@2025" | sudo chpasswd

# Проверка
id webdev1
id sysadmin1
groups dba1
```

**Практика 3.2: Управление на членство в групи**
```bash
# Добавяне на потребител към група
sudo gpasswd -a webdev1 docker

# Премахване от група
sudo gpasswd -d webdev1 docker

# Задаване на администратор на група
sudo gpasswd -A sysadmin1 itdept

# Списък на членове
getent group itdept
```

---

#### **Част 4: Sudo конфигурация (15 минути)**

**Теория - sudo:**
```
SUDO (Superuser Do):
├── Позволява изпълнение на команди като друг потребител
├── По подразбиране като root
├── Логва всички действия в /var/log/auth.log
└── Конфигурира се в /etc/sudoers

Принцип на минималните привилегии:
"Давайте само необходимите права, нищо повече"
```

**Практика 4.1: Основни sudo команди**
```bash
# Изпълнение на команда като root
sudo apt update

# Изпълнение като друг потребител
sudo -u postgres psql

# Отваряне на root shell
sudo -i
# или
sudo su -

# Проверка на sudo права
sudo -l

# Редактиране на sudoers (НИКОГА с nano/vim директно!)
sudo visudo
```

**Практика 4.2: Конфигуриране на sudoers**
```bash
# Отворете с visudo
sudo visudo

# Структура на sudoers файла:
# ─────────────────────────────────────────
# Defaults        env_reset
# Defaults        mail_badpass
# Defaults        secure_path="..."
#
# # User privilege specification
# root    ALL=(ALL:ALL) ALL
#
# # Members of the admin group may gain root privileges
# %admin ALL=(ALL) ALL
#
# # Allow members of group sudo to execute any command
# %sudo   ALL=(ALL:ALL) ALL

# Формат:
# WHO WHERE=(AS_WHOM) WHAT
# user host=(runas) commands
```

**Практика 4.3: Добавяне на sudo права**
```bash
# Метод 1: Добавяне към sudo група
sudo usermod -aG sudo webdev1

# Метод 2: Директно в sudoers
sudo visudo
# Добавете:
# webdev1 ALL=(ALL:ALL) ALL

# Метод 3: Файл в /etc/sudoers.d/
sudo nano /etc/sudoers.d/webdev1
# Съдържание:
# webdev1 ALL=(ALL:ALL) ALL

# Задайте правилни права
sudo chmod 440 /etc/sudoers.d/webdev1
```

**Практика 4.4: Ограничени sudo права**
```bash
# Създаване на ограничен sudoers файл
sudo nano /etc/sudoers.d/sysadmins

# Съдържание:
# ─────────────────────────────────────────
# # Sysadmins могат да рестартират услуги
# %sysadmins ALL=(ALL) /bin/systemctl restart *
# %sysadmins ALL=(ALL) /bin/systemctl status *
#
# # Могат да четат логове
# %sysadmins ALL=(ALL) /bin/cat /var/log/*
# %sysadmins ALL=(ALL) /bin/tail /var/log/*
#
# # Не могат да спират системата
# %sysadmins ALL=(ALL) !/sbin/shutdown
# %sysadmins ALL=(ALL) !/sbin/reboot
# ─────────────────────────────────────────

sudo chmod 440 /etc/sudoers.d/sysadmins
```

**Практика 4.5: Sudo без парола (за автоматизация)**
```bash
# ВНИМАНИЕ: Използвайте внимателно!
sudo nano /etc/sudoers.d/automation

# Съдържание:
# automation ALL=(ALL) NOPASSWD: /usr/bin/apt update
# automation ALL=(ALL) NOPASSWD: /usr/bin/apt upgrade -y

sudo chmod 440 /etc/sudoers.d/automation
```

---

#### **Част 5: Управление на пароли (5 минути)**

**Практика 5.1: Команда passwd**
```bash
# Смяна на собствена парола
passwd

# Смяна на парола на друг потребител (като root)
sudo passwd webdev1

# Заключване на парола
sudo passwd -l webdev1

# Отключване
sudo passwd -u webdev1

# Изтриване на парола (не е препоръчително)
sudo passwd -d webdev1

# Принудителна смяна при следващ login
sudo passwd -e webdev1
```

**Практика 5.2: Команда chage (password aging)**
```bash
# Преглед на информация за парола
sudo chage -l webdev1

# Задаване на изтичане на парола след 90 дни
sudo chage -M 90 webdev1

# Минимален период между смени
sudo chage -m 7 webdev1

# Предупреждение преди изтичане
sudo chage -W 14 webdev1

# Изтичане на акаунта
sudo chage -E 2025-12-31 webdev1
```

---

### **4. ЗАТВЪРЖДАВАНЕ (12 минути)**

**Практически сценарий:**
```
ЗАДАЧА: Настройка на IT екип

Създайте следната структура:
1. Група "devops" с GID 3000
2. Трима потребители:
   - devops1 (член на devops и docker)
   - devops2 (член на devops)
   - devops_lead (член на devops, с пълен sudo достъп)
3. Паролите да изтичат след 60 дни
4. devops_lead да може да рестартира docker услугата без парола
```

**Решение:**
```bash
# 1. Създаване на група
sudo groupadd -g 3000 devops

# 2. Създаване на потребители
sudo useradd -m -G devops,docker -c "DevOps Engineer 1" devops1
sudo useradd -m -G devops -c "DevOps Engineer 2" devops2
sudo useradd -m -G devops,sudo -c "DevOps Team Lead" devops_lead

# 3. Задаване на пароли
echo "devops1:DevOps1@2025" | sudo chpasswd
echo "devops2:DevOps2@2025" | sudo chpasswd
echo "devops_lead:Lead@2025" | sudo chpasswd

# 4. Настройка на изтичане
sudo chage -M 60 devops1
sudo chage -M 60 devops2
sudo chage -M 60 devops_lead

# 5. Sudo без парола за docker
sudo nano /etc/sudoers.d/devops_lead
# devops_lead ALL=(ALL) NOPASSWD: /bin/systemctl restart docker
sudo chmod 440 /etc/sudoers.d/devops_lead

# Проверка
id devops1
id devops_lead
sudo -l -U devops_lead
```

---

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови концепции:**
```
✓ /etc/passwd - информация за потребители
✓ /etc/shadow - криптирани пароли
✓ /etc/group - групи и членство
✓ useradd/usermod/userdel - управление на потребители
✓ groupadd/groupmod/groupdel - управление на групи
✓ sudo/visudo - административен достъп
✓ passwd/chage - управление на пароли
```

**Best Practices:**
```
1. Винаги използвайте visudo за редактиране на sudoers
2. Прилагайте принципа на минималните привилегии
3. Задавайте изтичане на пароли
4. Използвайте групи вместо индивидуални права
5. Документирайте всички административни промени
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задание:**
```
1. Създайте shell скрипт, който:
   - Приема username като аргумент
   - Създава потребител с home директория
   - Добавя го към група "students"
   - Задава парола, която изтича след 30 дни
   - Извежда информация за създадения потребител

2. Проучете:
   - Какво е PAM (Pluggable Authentication Modules)?
   - Как да настроите password complexity в Linux?

Очаквано време: 30-45 минути
```

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Компонент | Точки | Процент |
|-----------|-------|---------|
| Създаване на потребители | 15 | 25% |
| Управление на групи | 15 | 25% |
| Конфигуриране на sudo | 15 | 25% |
| Практически сценарий | 10 | 15% |
| Домашна работа | 5 | 10% |
| **ОБЩО** | **60** | **100%** |

### ОЦЕНЪЧНА РУБРИКА:

| Критерий | Отличен (6) | Много добър (5) | Добър (4) | Среден (3) |
|----------|-------------|-----------------|-----------|------------|
| Потребители | Всички команди правилни | Малки грешки | Основните команди | Частично изпълнение |
| Групи | Пълно управление | С минимална помощ | Базово управление | Нуждае се от помощ |
| Sudo | Сложни конфигурации | Стандартни конфигурации | Базов достъп | Само добавяне към sudo |
| Сценарий | Напълно решен | С малки пропуски | Частично решен | Нерешен |

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Мога ли да създам потребител с всички необходими опции?
2. Разбирам ли структурата на /etc/passwd и /etc/shadow?
3. Мога ли да конфигурирам ограничен sudo достъп?
4. Знам ли как да управлявам изтичането на пароли?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 90% от учениците могат да създават потребители
- [ ] 80% разбират групите и членството
- [ ] 75% могат да конфигурират базов sudo достъп
- [ ] 60% могат да създават сложни sudo правила

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: РАБОТЕН ЛИСТ

```
╔══════════════════════════════════════════════════════════════╗
║     РАБОТЕН ЛИСТ: LINUX ПОТРЕБИТЕЛИ И ГРУПИ                 ║
╠══════════════════════════════════════════════════════════════╣
║ Име: _________________________ Клас: ______ Дата: _________ ║
╚══════════════════════════════════════════════════════════════╝

ЗАДАЧА 1: Анализ на /etc/passwd
───────────────────────────────
Изпълнете: cat /etc/passwd | head -5

Попълнете за първия потребител:
Username: _________________
UID: _________________
GID: _________________
Home: _________________
Shell: _________________

ЗАДАЧА 2: Създаване на потребител
───────────────────────────────
Създайте потребител "labuser" с:
- Home директория: /home/labuser
- Shell: /bin/bash
- Коментар: "Lab User"
- Член на група: students

Команда: ________________________________________________
________________________________________________________

ЗАДАЧА 3: Проверка
───────────────────────────────
Използвайте id labuser и запишете:
UID: _________________
GID: _________________
Groups: _________________

ЗАДАЧА 4: Sudo конфигурация
───────────────────────────────
Създайте файл /etc/sudoers.d/labuser, който позволява
на labuser да изпълнява само apt update и apt upgrade.

Съдържание на файла:
________________________________________________________
________________________________________________________

═══════════════════════════════════════════════════════════════
```

---

### ПРИЛОЖЕНИЕ 2: СПРАВОЧНИК С КОМАНДИ

```
╔══════════════════════════════════════════════════════════════╗
║              LINUX USER MANAGEMENT - КОМАНДИ                 ║
╚══════════════════════════════════════════════════════════════╝

ПОТРЕБИТЕЛИ
───────────────────────────────────────────────────────────────
useradd [options] username     # Създаване
  -m                           # Създай home директория
  -d /path                     # Посочи home директория
  -s /bin/bash                 # Посочи shell
  -g group                     # Основна група
  -G group1,group2             # Допълнителни групи
  -c "Comment"                 # Коментар/пълно име
  -e YYYY-MM-DD                # Дата на изтичане
  -u UID                       # Конкретен UID

usermod [options] username     # Промяна
  -aG group                    # Добави към група (append!)
  -L                           # Заключи акаунт
  -U                           # Отключи акаунт
  -l newname                   # Преименувай

userdel [options] username     # Изтриване
  -r                           # Изтрий и home директория

ГРУПИ
───────────────────────────────────────────────────────────────
groupadd [options] groupname   # Създаване
  -g GID                       # Конкретен GID

groupmod [options] groupname   # Промяна
  -n newname                   # Преименувай
  -g GID                       # Промени GID

groupdel groupname             # Изтриване

gpasswd [options] group        # Управление на членство
  -a user                      # Добави потребител
  -d user                      # Премахни потребител
  -A user                      # Направи администратор

ПАРОЛИ
───────────────────────────────────────────────────────────────
passwd [options] [username]    # Управление на парола
  -l                           # Заключи
  -u                           # Отключи
  -e                           # Принуди смяна
  -d                           # Изтрий парола

chage [options] username       # Password aging
  -l                           # Покажи информация
  -M days                      # Макс. дни валидност
  -m days                      # Мин. дни между смени
  -W days                      # Дни предупреждение
  -E YYYY-MM-DD                # Дата на изтичане

SUDO
───────────────────────────────────────────────────────────────
sudo command                   # Изпълни като root
sudo -u user command           # Изпълни като user
sudo -i                        # Root shell
sudo -l                        # Покажи права
visudo                         # Редактирай sudoers

ИНФОРМАЦИЯ
───────────────────────────────────────────────────────────────
id [username]                  # UID, GID, групи
groups [username]              # Групи на потребител
whoami                         # Текущ потребител
who                            # Логнати потребители
w                              # Подробна информация
last                           # История на логвания

═══════════════════════════════════════════════════════════════
```

---

### ПРИЛОЖЕНИЕ 3: ПРИМЕРЕН СКРИПТ ЗА АВТОМАТИЗАЦИЯ

```bash
#!/bin/bash
# create_user.sh - Скрипт за създаване на потребител
# Използване: ./create_user.sh username "Full Name" group

# Проверка за root права
if [ "$EUID" -ne 0 ]; then
    echo "Грешка: Изпълнете като root (sudo)"
    exit 1
fi

# Проверка на аргументите
if [ $# -lt 3 ]; then
    echo "Използване: $0 username \"Full Name\" group"
    exit 1
fi

USERNAME=$1
FULLNAME=$2
GROUP=$3

# Проверка дали групата съществува
if ! getent group "$GROUP" > /dev/null 2>&1; then
    echo "Създаване на група $GROUP..."
    groupadd "$GROUP"
fi

# Проверка дали потребителят съществува
if id "$USERNAME" > /dev/null 2>&1; then
    echo "Грешка: Потребител $USERNAME вече съществува"
    exit 1
fi

# Създаване на потребител
echo "Създаване на потребител $USERNAME..."
useradd -m -s /bin/bash -g "$GROUP" -c "$FULLNAME" "$USERNAME"

# Генериране на временна парола
TEMP_PASS=$(openssl rand -base64 12)
echo "$USERNAME:$TEMP_PASS" | chpasswd

# Принуждаване на смяна на парола
passwd -e "$USERNAME"

# Задаване на изтичане след 90 дни
chage -M 90 "$USERNAME"

# Извеждане на информация
echo ""
echo "══════════════════════════════════════════"
echo "Потребител създаден успешно!"
echo "══════════════════════════════════════════"
echo "Username: $USERNAME"
echo "Full Name: $FULLNAME"
echo "Group: $GROUP"
echo "Temp Password: $TEMP_PASS"
echo "Password expires: 90 days"
echo ""
id "$USERNAME"
echo "══════════════════════════════════════════"
```

---

*Документът е създаден за учебната 2025/2026 година*
*Съответства на изискванията на МОН за професионална подготовка*
*Специалност: Икономическо информационно осигуряване (код 482021)*
