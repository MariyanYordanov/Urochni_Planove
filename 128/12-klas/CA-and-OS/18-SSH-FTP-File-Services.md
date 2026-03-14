# УРОЧЕН ПЛАН №18
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
| **Тема на урока:** | SSH, FTP и файлови услуги |
| **Дата:** | ____________ |
| **Час:** | ____________ |
| **Продължителност:** | 90 минути (2 учебни часа) |
| **Тип урок:** | Упражнение |
| **Място на провеждане:** | Компютърен кабинет |

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разбират SSH протокола и неговата сигурност
2. Да конфигурират и използват SSH сървър и клиент
3. Да създават и използват SSH ключове за автентикация
4. Да разбират FTP/SFTP протоколите и разликите между тях
5. Да конфигурират файлови услуги за споделяне

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на осъзнатост за мрежова сигурност
2. Развиване на разбиране за криптирани комуникации
3. Изграждане на отговорност при отдалечен достъп
4. Насърчаване на сигурни практики за автентикация

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на практически умения за отдалечено администриране
2. Усъвършенстване на troubleshooting на мрежови услуги
3. Формиране на умения за сигурна конфигурация
4. Развитие на систематичен подход към мрежови услуги

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ:

**SSH (Secure Shell):**
- SSH протокол - версии и сигурност
- Автентикация с парола vs ключове
- SSH клиент и сървър конфигурация
- SSH тунелиране и port forwarding
- SCP и SFTP за файлов трансфер

**FTP/SFTP:**
- FTP протокол - активен vs пасивен режим
- Проблеми със сигурността на FTP
- SFTP като сигурна алтернатива
- vsftpd конфигурация

**Файлови услуги:**
- Samba за Windows споделяне
- NFS за Linux мрежово споделяне

### МЕЖДУПРЕДМЕТНИ ВРЪЗКИ:
1. **Мрежови технологии** - TCP/IP, портове, firewall
2. **Информационна сигурност** - криптография, ключове
3. **Програмиране** - автоматизация с SSH
4. **Операционни системи** - файлови системи и права

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. Демонстрация с обяснение
2. Практически упражнения
3. Лабораторна работа по двойки
4. Решаване на проблеми
5. Дискусия на сигурност

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
- Две Ubuntu VM за тестване на връзки
- PuTTY (Windows) или терминал (Linux/Mac)
- FileZilla за FTP/SFTP тестване
- Конфигурационни шаблони

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Въведение:**
- Проверка на присъстващите
- Стартиране на две VM за практика
- Цели на урока

**Мотивиращ въпрос:**
"Как системните администратори управляват хиляди сървъри, разположени в различни части на света?"

---

### **2. АКТУАЛИЗАЦИЯ (8 минути)**

**Преговор на мрежови основи:**
```
Важни портове за днешния урок:
• SSH:  22/TCP
• FTP:  21/TCP (control), 20/TCP (data)
• SFTP: 22/TCP (използва SSH)
• Samba: 445/TCP, 139/TCP
• NFS:  2049/TCP/UDP

Въпрос: Защо FTP се счита за несигурен?
Отговор: Изпраща пароли и данни в plain text
```

---

### **3. НОВ МАТЕРИАЛ И ПРАКТИКА (55 минути)**

#### **Част 1: SSH - Secure Shell (25 минути)**

**Теория - SSH архитектура:**
```
SSH (Secure Shell) - Порт 22

Функции:
├── Отдалечен достъп до командния ред
├── Сигурен файлов трансфер (SCP, SFTP)
├── Port forwarding (тунелиране)
└── X11 forwarding (графичен достъп)

Автентикация:
├── Password - парола (по-малко сигурно)
└── Public Key - криптографски ключове (препоръчително)

Криптиране:
├── Asymmetric: RSA, ECDSA, Ed25519 (за автентикация)
└── Symmetric: AES, ChaCha20 (за данните)
```

**Практика 1.1: Инсталация и стартиране на SSH сървър**
```bash
# Проверка дали OpenSSH е инсталиран
dpkg -l | grep openssh

# Инсталация на OpenSSH сървър
sudo apt install openssh-server -y

# Проверка на статуса
sudo systemctl status ssh

# Стартиране (ако не е стартиран)
sudo systemctl start ssh
sudo systemctl enable ssh

# Проверка на порта
sudo ss -tlnp | grep 22
```

**Практика 1.2: Свързване чрез SSH**
```bash
# Основен синтаксис
ssh username@hostname_or_ip

# Пример (към localhost)
ssh student@localhost

# С конкретен порт
ssh -p 2222 user@host

# Първо свързване - fingerprint потвърждение
# The authenticity of host 'X' can't be established.
# ED25519 key fingerprint is SHA256:xxxxx
# Are you sure you want to continue connecting? yes
```

**Практика 1.3: Генериране на SSH ключове**
```bash
# Генериране на Ed25519 ключ (препоръчителен)
ssh-keygen -t ed25519 -C "student@school.local"

# Ще попита:
# Enter file: /home/student/.ssh/id_ed25519 (Enter за default)
# Enter passphrase: (парола за защита на ключа)

# Генериране на RSA ключ (по-стар, съвместим)
ssh-keygen -t rsa -b 4096 -C "student@school.local"

# Преглед на генерираните ключове
ls -la ~/.ssh/
# id_ed25519      - частен ключ (НИКОГА не споделяйте!)
# id_ed25519.pub  - публичен ключ (споделяте го)

# Преглед на публичния ключ
cat ~/.ssh/id_ed25519.pub
```

**Практика 1.4: Копиране на публичен ключ**
```bash
# Автоматично копиране
ssh-copy-id username@remote_host

# Или ръчно:
# 1. Покажете публичния ключ
cat ~/.ssh/id_ed25519.pub

# 2. На отдалечения сървър
mkdir -p ~/.ssh
chmod 700 ~/.ssh
echo "публичния_ключ" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys

# След това свързване без парола
ssh username@remote_host
```

**Практика 1.5: SSH конфигурация**
```bash
# Сървърна конфигурация
sudo nano /etc/ssh/sshd_config

# Важни настройки:
# ─────────────────────────────────────────
Port 22                          # Порт (може да се смени)
PermitRootLogin no               # Забрана на root login
PasswordAuthentication yes       # Позволи парола (no за по-сигурно)
PubkeyAuthentication yes         # Позволи ключове
MaxAuthTries 3                   # Макс опити
AllowUsers student admin         # Позволени потребители
# ─────────────────────────────────────────

# Рестартиране след промени
sudo systemctl restart ssh
```

**Практика 1.6: SSH клиентска конфигурация**
```bash
# Създаване на ~/.ssh/config
nano ~/.ssh/config

# Съдържание:
# ─────────────────────────────────────────
Host webserver
    HostName 192.168.1.100
    User admin
    Port 22
    IdentityFile ~/.ssh/id_ed25519

Host dbserver
    HostName 192.168.1.101
    User postgres
    Port 22

Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
# ─────────────────────────────────────────

# Сега можете да се свържете с:
ssh webserver
# вместо
ssh -i ~/.ssh/id_ed25519 admin@192.168.1.100
```

**Практика 1.7: SCP - Secure Copy**
```bash
# Копиране на файл към сървър
scp file.txt user@server:/path/to/destination/

# Копиране от сървър
scp user@server:/path/to/file.txt ./local/

# Копиране на директория
scp -r directory/ user@server:/path/

# С конкретен порт
scp -P 2222 file.txt user@server:/path/
```

---

#### **Част 2: SFTP и FTP (15 минути)**

**SFTP - SSH File Transfer Protocol:**
```bash
# Свързване чрез SFTP
sftp user@server

# SFTP команди:
# pwd         - текуща директория на сървъра
# lpwd        - текуща локална директория
# ls          - списък на сървъра
# lls         - локален списък
# cd dir      - смяна на директория
# lcd dir     - локална смяна
# get file    - изтегляне
# put file    - качване
# mkdir dir   - създаване на директория
# rm file     - изтриване
# exit        - изход

# Пример:
sftp> pwd
sftp> ls
sftp> get document.pdf
sftp> put report.txt
sftp> exit
```

**FTP с vsftpd:**
```bash
# Инсталация на vsftpd
sudo apt install vsftpd -y

# Конфигурация
sudo nano /etc/vsftpd.conf

# Важни настройки:
# ─────────────────────────────────────────
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
pasv_enable=YES
pasv_min_port=30000
pasv_max_port=30100
# ─────────────────────────────────────────

# Рестартиране
sudo systemctl restart vsftpd
sudo systemctl enable vsftpd

# Firewall (ако е активен)
sudo ufw allow 21/tcp
sudo ufw allow 30000:30100/tcp
```

**Тестване с FTP клиент:**
```bash
# Команден ред
ftp server_ip
# Username: your_user
# Password: your_password

ftp> ls
ftp> get file.txt
ftp> put localfile.txt
ftp> bye

# Или с lftp (по-мощен)
lftp user@server
```

---

#### **Част 3: Samba - Windows споделяне (10 минути)**

**Инсталация и конфигурация:**
```bash
# Инсталация
sudo apt install samba -y

# Създаване на споделена директория
sudo mkdir -p /srv/samba/shared
sudo chmod 777 /srv/samba/shared

# Конфигурация
sudo nano /etc/samba/smb.conf

# Добавете в края:
# ─────────────────────────────────────────
[shared]
   comment = Shared Folder
   path = /srv/samba/shared
   browseable = yes
   read only = no
   guest ok = no
   valid users = student
# ─────────────────────────────────────────

# Добавяне на Samba потребител
sudo smbpasswd -a student

# Рестартиране
sudo systemctl restart smbd
sudo systemctl enable smbd

# Проверка
sudo testparm

# Firewall
sudo ufw allow samba
```

**Достъп от Windows:**
```
В Explorer: \\IP_ADDRESS\shared
Или: \\hostname\shared

Въведете потребител и парола
```

**Достъп от Linux:**
```bash
# Инсталация на клиент
sudo apt install smbclient cifs-utils

# Преглед на споделяния
smbclient -L //server_ip -U username

# Свързване
smbclient //server_ip/shared -U username

# Монтиране
sudo mount -t cifs //server_ip/shared /mnt/samba -o username=student
```

---

#### **Част 4: NFS - Network File System (5 минути)**

**NFS сървър:**
```bash
# Инсталация
sudo apt install nfs-kernel-server -y

# Създаване на споделяне
sudo mkdir -p /srv/nfs/share
sudo chown nobody:nogroup /srv/nfs/share
sudo chmod 777 /srv/nfs/share

# Конфигурация
sudo nano /etc/exports
# Добавете:
/srv/nfs/share 192.168.1.0/24(rw,sync,no_subtree_check)

# Приложете промените
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

**NFS клиент:**
```bash
# Инсталация
sudo apt install nfs-common -y

# Монтиране
sudo mount server_ip:/srv/nfs/share /mnt/nfs

# Постоянно монтиране (fstab)
echo "server_ip:/srv/nfs/share /mnt/nfs nfs defaults 0 0" | sudo tee -a /etc/fstab
```

---

### **4. ЗАТВЪРЖДАВАНЕ (12 минути)**

**Практическа задача:**
```
СЦЕНАРИЙ: Настройка на файлов сървър

1. Конфигурирайте SSH с key-based автентикация
   между две машини (или localhost)

2. Създайте Samba споделяне "documents"
   - Достъпно само за потребител "fileuser"
   - С права за четене и писане

3. Тествайте трансфер на файл чрез:
   - SCP
   - SFTP
   - Samba (ако е възможно)

4. Направете скрийншотове на успешни трансфери
```

---

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови концепции:**
```
SSH:
✓ Порт 22, криптирана комуникация
✓ Key-based автентикация е по-сигурна
✓ ssh-keygen за генериране на ключове
✓ ssh-copy-id за копиране на ключ
✓ SCP/SFTP за файлов трансфер

FTP/SFTP:
✓ FTP е несигурен (plain text)
✓ SFTP използва SSH (сигурен)
✓ vsftpd за FTP сървър

Споделяне:
✓ Samba за Windows клиенти
✓ NFS за Linux клиенти
```

---

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задание:**
```
1. Настройте SSH така, че:
   - Root login да е забранен
   - Само key-based автентикация
   - Максимум 2 опита за свързване

2. Създайте скрипт, който автоматично 
   прави backup на директория чрез SCP

3. Проучете: Какво е SSH agent и ssh-add?

Очаквано време: 30-45 минути
```

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Компонент | Точки | Процент |
|-----------|-------|---------|
| SSH конфигурация и ключове | 20 | 35% |
| SFTP/FTP използване | 10 | 15% |
| Samba конфигурация | 15 | 25% |
| Практическа задача | 10 | 15% |
| Домашна работа | 5 | 10% |
| **ОБЩО** | **60** | **100%** |

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: SSH КОМАНДИ СПРАВОЧНИК

```
╔══════════════════════════════════════════════════════════════╗
║                    SSH КОМАНДИ                               ║
╚══════════════════════════════════════════════════════════════╝

СВЪРЗВАНЕ
───────────────────────────────────────────────────────────────
ssh user@host                    # Основно свързване
ssh -p 2222 user@host            # Конкретен порт
ssh -i ~/.ssh/key user@host      # Конкретен ключ
ssh -v user@host                 # Verbose (debug)

КЛЮЧОВЕ
───────────────────────────────────────────────────────────────
ssh-keygen -t ed25519            # Генериране Ed25519
ssh-keygen -t rsa -b 4096        # Генериране RSA
ssh-copy-id user@host            # Копиране на ключ
ssh-add ~/.ssh/key               # Добавяне към agent
ssh-add -l                       # Списък на ключове в agent

ФАЙЛОВ ТРАНСФЕР
───────────────────────────────────────────────────────────────
scp file user@host:/path         # Копиране към сървър
scp user@host:/path/file ./      # Копиране от сървър
scp -r dir user@host:/path       # Рекурсивно копиране
sftp user@host                   # Интерактивен SFTP

ТУНЕЛИРАНЕ
───────────────────────────────────────────────────────────────
ssh -L 8080:localhost:80 user@host   # Local port forward
ssh -R 8080:localhost:80 user@host   # Remote port forward
ssh -D 1080 user@host                # SOCKS proxy

УПРАВЛЕНИЕ
───────────────────────────────────────────────────────────────
sudo systemctl status ssh        # Статус
sudo systemctl restart ssh       # Рестартиране
sudo nano /etc/ssh/sshd_config   # Конфигурация

═══════════════════════════════════════════════════════════════
```

### ПРИЛОЖЕНИЕ 2: КОНФИГУРАЦИОНЕН ШАБЛОН - СИГУРЕН SSH

```bash
# /etc/ssh/sshd_config - Сигурна конфигурация

# Основни настройки
Port 22
Protocol 2
AddressFamily inet

# Автентикация
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
MaxAuthTries 3
MaxSessions 5

# Сигурност
X11Forwarding no
AllowTcpForwarding no
PermitEmptyPasswords no
UsePAM yes

# Таймаути
ClientAliveInterval 300
ClientAliveCountMax 2
LoginGraceTime 60

# Позволени потребители (променете според нуждите)
AllowUsers admin developer

# Логване
SyslogFacility AUTH
LogLevel VERBOSE
```

---

*Документът е създаден за учебната 2025/2026 година*
*Съответства на изискванията на МОН за професионална подготовка*
*Специалност: Икономическо информационно осигуряване (код 482021)*
