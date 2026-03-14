# УРОЧЕН ПЛАН №11
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** ПГИ „Професор д-р Асен Златаров"
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Docker контейнери - основни концепции и практическа работа
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Комбиниран (нови знания + практическа работа)
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат концепцията за контейнеризация
2. Да усвоят разликата между виртуални машини и контейнери
3. Да научат основните Docker команди
4. Да могат да създават и управляват Docker контейнери
5. Да разбират концепцията за Docker images и Docker Hub

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на мислене за ефективно използване на ресурси
2. Възпитаване на креативност при решаване на проблеми
3. Развиване на екипни умения при работа с DevOps инструменти
4. Изграждане на професионални навици

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на абстрактно мислене
2. Усъвършенстване на умения за работа с команден ред
3. Развитие на способности за автоматизация
4. Формиране на DevOps култура

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- Концепция за контейнеризация и нейните предимства
- Архитектура на Docker - Docker Engine, Images, Containers
- Docker Hub и регистри на образи
- Dockerfile синтаксис и best practices
- Docker networking и volumes
- Docker Compose основи

#### Умения:
- Инсталиране и конфигуриране на Docker
- Изпълнение на основни Docker команди
- Създаване на Docker images чрез Dockerfile
- Управление на контейнери и техните ресурси
- Работа с Docker Hub
- Създаване на multi-container приложения

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Програмиране** - контейнеризиране на приложения
2. **Мрежови технологии** - Docker networking, port mapping
3. **Бази данни** - контейнеризиране на database сървъри
4. **Информационна сигурност** - изолация на приложения
5. **Уеб технологии** - deployment на web приложения
6. **Икономика** - оптимизация на инфраструктурни разходи

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Визуална демонстрация** с диаграми и схеми
2. **Практическа работа** стъпка по стъпка
3. **Сравнителен анализ** VM vs Containers
4. **Проектно-базирано обучение**
5. **Peer learning** - взаимно обучение

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Хардуер и софтуер:**
   - Компютри с Linux/Windows + WSL2
   - Docker Desktop / Docker CE
   - Visual Studio Code
   - Git
   - Интернет достъп
   
2. **Учебни материали:**
   - Docker команди cheat sheet
   - Примерни Dockerfile файлове
   - Схема на Docker архитектура
   - Готови проектни задания

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Проверка на Docker инсталацията
- Раздаване на материали

**Дейност на учениците:**
- Проверка на Docker с команда:
```bash
docker --version
docker run hello-world
```

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (10 минути)**

**Дейност на учителя:**
- Преговор на виртуализацията от предишния урок
- Въпроси за VM технологии

**Примерни въпроси:**
1. Какво е виртуална машина?
2. Какви са предимствата на виртуализацията?
3. Какво е hypervisor?
4. Какви ресурси използва една VM?

**Въвеждащ проблем:**
"Имаме 10 микросервиса, всеки изисква различна среда. Как да ги deploy-нем ефективно?"

### **3. НОВ МАТЕРИАЛ (40 минути)**

#### **Част 1: Концепция за контейнеризация (10 мин)**

**Дейност на учителя:**
- Представяне на еволюцията:
  - Физически сървъри → Виртуални машини → Контейнери
  
**Визуална демонстрация:**
```
Traditional Deployment:
┌─────────────────────┐
│     Application     │
├─────────────────────┤
│    Dependencies     │
├─────────────────────┤
│   Guest OS (5GB)    │
├─────────────────────┤
│     Hypervisor      │
├─────────────────────┤
│      Host OS        │
├─────────────────────┤
│     Hardware        │
└─────────────────────┘

Container Deployment:
┌──────┬──────┬──────┐
│ App1 │ App2 │ App3 │
├──────┴──────┴──────┤
│  Docker Containers  │
├─────────────────────┤
│   Docker Engine     │
├─────────────────────┤
│      Host OS        │
├─────────────────────┤
│     Hardware        │
└─────────────────────┘
```

**Предимства на контейнерите:**
- Бързо стартиране (секунди vs минути)
- По-малък размер (MB vs GB)
- Преносимост между среди
- Ефективно използване на ресурси
- Версиониране и rollback

**Дейност на учениците:**
- Сравнителна таблица VM vs Containers
- Дискусия за use cases

#### **Част 2: Docker архитектура и команди (15 мин)**

**Дейност на учителя:**
- Обяснение на компонентите:
  - Docker Daemon
  - Docker Client
  - Docker Registry
  - Images vs Containers

**Основни команди - демонстрация:**

```bash
# Управление на images
docker images                    # Списък на образи
docker pull nginx:latest         # Изтегляне на образ
docker rmi nginx                # Изтриване на образ

# Управление на контейнери
docker ps                        # Активни контейнери
docker ps -a                     # Всички контейнери
docker run -d -p 80:80 nginx    # Стартиране
docker stop container_id        # Спиране
docker rm container_id          # Изтриване

# Интерактивна работа
docker exec -it container_id /bin/bash
docker logs container_id
docker inspect container_id
```

**Практическо упражнение 1:**
Стартиране на Nginx web сървър:

```bash
# Стъпка 1: Изтегляне на образа
docker pull nginx:alpine

# Стъпка 2: Стартиране с port mapping
docker run -d -p 8080:80 --name my-nginx nginx:alpine

# Стъпка 3: Проверка
docker ps
curl localhost:8080

# Стъпка 4: Влизане в контейнера
docker exec -it my-nginx sh
ls -la /usr/share/nginx/html/
exit

# Стъпка 5: Спиране и изтриване
docker stop my-nginx
docker rm my-nginx
```

**Дейност на учениците:**
- Изпълнение на командите
- Експериментиране с различни образи
- Документиране на резултатите

#### **Част 3: Създаване на Docker образи (15 мин)**

**Дейност на учителя:**
- Обяснение на Dockerfile синтаксиса
- Демонстрация на създаване на custom image

**Пример: Node.js приложение**

1. **Създаване на просто приложение:**
```javascript
// app.js
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
    res.json({ 
        message: 'Hello from Docker!',
        timestamp: new Date()
    });
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

2. **package.json:**
```json
{
  "name": "docker-demo",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  }
}
```

3. **Dockerfile:**
```dockerfile
# Базов образ
FROM node:16-alpine

# Работна директория
WORKDIR /app

# Копиране на dependencies
COPY package*.json ./

# Инсталиране на dependencies
RUN npm install

# Копиране на кода
COPY . .

# Експониране на порт
EXPOSE 3000

# Стартиране на приложението
CMD ["npm", "start"]
```

4. **Build и Run:**
```bash
# Build на образа
docker build -t my-node-app .

# Стартиране
docker run -d -p 3000:3000 --name node-container my-node-app

# Тестване
curl localhost:3000
```

**Дейност на учениците:**
- Създаване на приложението
- Писане на Dockerfile
- Build и тестване

### **4. ЗАТВЪРЖДАВАНЕ (25 минути)**

#### **Практическа задача: Multi-container приложение**

**Задание:** Създайте TODO приложение с:
- Frontend (HTML/JS)
- Backend (Node.js/Express)
- Database (MongoDB)

**Docker Compose файл:**
```yaml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend
    
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    environment:
      - MONGO_URL=mongodb://database:27017/todoapp
    depends_on:
      - database
    
  database:
    image: mongo:5
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

**Работа в екипи:**
- Екип 1: Frontend контейнер
- Екип 2: Backend контейнер
- Екип 3: Database конфигурация
- Екип 4: Docker Compose интеграция

**Дейност на учениците:**
- Разделяне на задачите
- Имплементация
- Тестване на интеграцията
- Презентация на решението

### **5. DOCKER HUB И BEST PRACTICES (8 минути)**

**Дейност на учителя:**
- Демонстрация на Docker Hub
- Push на образ в registry

```bash
# Login в Docker Hub
docker login

# Tag на образа
docker tag my-node-app username/my-node-app:v1

# Push към registry
docker push username/my-node-app:v1

# Pull от друг компютър
docker pull username/my-node-app:v1
```

**Best Practices:**
1. Използвайте официални base images
2. Минимизирайте layers в Dockerfile
3. Използвайте .dockerignore
4. Не включвайте secrets в images
5. Използвайте multi-stage builds
6. Tag-вайте версиите правилно

### **6. ОБОБЩЕНИЕ И ДОМАШНА РАБОТА (7 минути)**

**Обобщение на ключовите концепции:**
- Контейнерите са по-леки от VM
- Docker улеснява deployment на приложения
- Dockerfile дефинира как се build-ва образ
- Docker Compose управлява multi-container apps

**Домашна работа:**

1. **Проект 1: Контейнеризирайте съществуващо приложение**
   - Вземете ваш проект по Програмиране
   - Създайте Dockerfile
   - Push към Docker Hub
   - Документирайте процеса

2. **Проект 2: Microservices архитектура**
   - Създайте 3 микросервиса
   - Свържете ги с Docker Compose
   - Имплементирайте logging

3. **Изследване:**
   - Проучете Kubernetes
   - Сравнете с Docker Swarm
   - Подготовка за представяне (5 мин)

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Правилно използване на Docker команди | 20% |
| Създаване на работещ Dockerfile | 25% |
| Успешен build на образ | 20% |
| Работа в екип | 15% |
| Документация и коментари | 10% |
| Креативност и инициатива | 10% |

### ИНДИКАТОРИ ЗА ПОСТИГНАТИ РЕЗУЛТАТИ:
- Успешно стартиране на контейнери - 100% от учениците
- Създаване на custom image - 80% от учениците
- Работа с Docker Compose - 60% от учениците
- Push към Docker Hub - 50% от учениците

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли разликата между VM и контейнер?
2. Мога ли да създам Dockerfile?
3. Умея ли да управлявам контейнери?
4. Готов ли съм за продължение с Kubernetes?

### ОЧАКВАНИ ТРУДНОСТИ И РЕШЕНИЯ:
- **Проблем:** Недостатъчна RAM за Docker Desktop
  **Решение:** Използване на cloud среда или споделени ресурси

- **Проблем:** Сложност на networking концепциите
  **Решение:** Допълнителни визуални материали

- **Проблем:** Грешки при build на images
  **Решение:** Debugging сесия, разглеждане на чести грешки

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: DOCKER КОМАНДИ CHEAT SHEET

```bash
# Container Lifecycle
docker create    # Create container
docker run       # Create and start
docker start     # Start container
docker stop      # Stop gracefully
docker kill      # Stop immediately
docker restart   # Restart container
docker pause     # Pause processes
docker unpause   # Resume processes
docker rm        # Remove container

# Container Interaction
docker ps        # List running
docker ps -a     # List all
docker logs      # View logs
docker exec      # Execute command
docker attach    # Attach to container
docker cp        # Copy files
docker export    # Export filesystem
docker port      # Show port mappings

# Images
docker images    # List images
docker pull      # Download image
docker push      # Upload image
docker build     # Build from Dockerfile
docker commit    # Create from container
docker rmi       # Remove image
docker tag       # Tag image
docker history   # Show history

# Registry & Repository
docker login     # Login to registry
docker logout    # Logout
docker search    # Search images

# Information
docker version   # Show version
docker info      # Show system info
docker inspect   # Detailed info
docker events    # Real-time events
docker top       # Show processes
docker stats     # Show statistics
docker diff      # Show changes

# Cleanup
docker container prune   # Remove stopped
docker image prune       # Remove unused
docker system prune      # Clean everything
docker volume prune      # Remove volumes
```

### ПРИЛОЖЕНИЕ 2: DOCKERFILE TEMPLATE

```dockerfile
# Multi-stage build example
# Stage 1: Build
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Stage 2: Runtime
FROM node:16-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .

# Security
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
USER nodejs

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD node healthcheck.js

EXPOSE 3000
CMD ["node", "server.js"]
```

### ПРИЛОЖЕНИЕ 3: ПОЛЕЗНИ РЕСУРСИ

1. [Docker Official Documentation](https://docs.docker.com/)
2. [Docker Hub](https://hub.docker.com/)
3. [Play with Docker](https://labs.play-with-docker.com/)
4. [Docker Compose Documentation](https://docs.docker.com/compose/)
5. [Best Practices Guide](https://docs.docker.com/develop/dev-best-practices/)
6. [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Септември 2025 г.