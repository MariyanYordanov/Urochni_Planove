# УРОЧЕН ПЛАН №3
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** 128-мо СУ "Алберт Айнщайн", гр.София
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** GPU технологии - NVIDIA CUDA и OpenCL приложения
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Комбиниран
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат архитектурата на съвременните GPU
2. Да усвоят концепцията за паралелни изчисления с CUDA
3. Да познават приложенията на GPU за общи изчисления (GPGPU)
4. Да разберат разликата между CUDA и OpenCL
5. Да научат областите на приложение на GPU computing

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на интерес към паралелно програмиране
2. Развиване на иновативно мислене
3. Възпитаване на стремеж към оптимизация
4. Изграждане на визия за бъдещето на изчисленията

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за анализ на паралелни задачи
2. Усъвършенстване на разбирането за хардуерна архитектура
3. Формиране на способности за оценка на производителност
4. Развитие на компетенции за избор на технологии

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- GPU архитектура - SIMD, streaming multiprocessors
- NVIDIA CUDA платформа и програмен модел
- OpenCL стандарт за хетерогенни системи
- Tensor cores и RT cores в модерните GPU
- Приложения: AI/ML, rendering, научни изчисления, mining
- Сравнение CPU vs GPU за различни задачи

#### Умения:
- Идентифициране на паралелизируеми задачи
- Разбиране на CUDA терминология
- Анализ на GPU спецификации
- Оценка на производителност TFLOPS/TOPS
- Избор на подходящ GPU за конкретни нужди

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Програмиране** - паралелни алгоритми, threads
2. **Математика** - матрични операции, линейна алгебра
3. **Физика** - симулации, ray tracing
4. **Изкуствен интелект** - deep learning, neural networks
5. **Компютърна графика** - rendering, shaders

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Визуална презентация** с архитектурни диаграми
2. **Демонстрация** на CUDA и OpenCL примери
3. **Сравнителен анализ** на CPU vs GPU производителност
4. **Практически примери** с реални приложения
5. **Интерактивна дискусия** за use cases

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Хардуер и софтуер:**
   - Компютри с NVIDIA GPU (ако е налично)
   - CUDA Toolkit 12.x
   - Visual Studio Code
   - GPU-Z за мониторинг
   - Python с PyTorch/TensorFlow
   
2. **Учебни материали:**
   - Архитектурни диаграми
   - Сравнителни таблици
   - Примерен CUDA код
   - Benchmark резултати

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Подготовка на демонстрациите
- Въвеждащ въпрос: "Защо видеокартите са толкова важни за AI?"

**Дейност на учениците:**
- Подготовка за урока
- Отговори на въвеждащия въпрос

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (10 минути)**

**Дейност на учителя:**
- Преговор на CPU архитектура от предишните уроци
- Въпроси за паралелизъм

**Примерни въпроси:**
1. Какво е паралелно изпълнение?
2. Колко ядра има съвременен CPU?
3. Какво е SIMD (Single Instruction, Multiple Data)?
4. За какво се използват видеокартите освен за игри?

**Проблемна ситуация:**
"Имате задача да обработите 1 милион изображения. Защо GPU ще я свърши 100x по-бързо от CPU?"

### **3. НОВ МАТЕРИАЛ (45 минути)**

#### **Част 1: GPU Архитектура (15 мин)**

**Еволюция на GPU:**
```
1999: GeForce 256 - първи GPU
2006: CUDA - general purpose GPU
2012: Kepler - dynamic parallelism
2016: Pascal - HBM memory
2018: Turing - RT & Tensor cores
2020: Ampere - 2nd gen RT cores
2022: Ada Lovelace - 3rd gen RT
2024: Blackwell - AI focus
```

**Сравнение CPU vs GPU:**

```
CPU (Latency-optimized)          GPU (Throughput-optimized)
┌─────────────────────┐          ┌─────────────────────┐
│  4-24 Cores         │          │  10,000+ Cores      │
│  Complex cores      │          │  Simple cores       │
│  Large cache        │          │  Small cache        │
│  Branch prediction  │          │  No prediction      │
│  Out-of-order exec  │          │  In-order exec      │
│  Few threads        │          │  Massive threads    │
└─────────────────────┘          └─────────────────────┘
```

**NVIDIA GPU Architecture (RTX 4090):**
```
Ada Lovelace AD102:
- 76.3 billion transistors
- 16,384 CUDA cores
- 512 Tensor cores (4th gen)
- 128 RT cores (3rd gen)
- 24GB GDDR6X memory
- 1008 GB/s bandwidth
- 82.6 TFLOPS FP32
```

**Streaming Multiprocessor (SM):**
```
┌──────────────────────────┐
│     SM Architecture       │
├──────────────────────────┤
│  128 CUDA Cores          │
│  4 Tensor Cores          │
│  1 RT Core               │
│  256KB Register File     │
│  128KB L1/Shared Memory  │
│  Warp Scheduler (×4)     │
└──────────────────────────┘
```

#### **Част 2: CUDA Програмен модел (15 мин)**

**CUDA йерархия:**
```
Grid → Blocks → Threads

Grid (1D, 2D, 3D)
  ├── Block (0,0)
  │     ├── Thread (0,0,0)
  │     ├── Thread (0,1,0)
  │     └── ...
  ├── Block (0,1)
  └── ...
```

**Прост CUDA пример - векторно събиране:**
```cuda
// Kernel function
__global__ void vectorAdd(float *a, float *b, float *c, int n) {
    int idx = blockDim.x * blockIdx.x + threadIdx.x;
    if (idx < n) {
        c[idx] = a[idx] + b[idx];
    }
}

// Host код
int main() {
    int n = 1000000;
    size_t size = n * sizeof(float);
    
    // Allocate device memory
    cudaMalloc(&d_a, size);
    cudaMalloc(&d_b, size);
    cudaMalloc(&d_c, size);
    
    // Copy data to device
    cudaMemcpy(d_a, h_a, size, cudaMemcpyHostToDevice);
    cudaMemcpy(d_b, h_b, size, cudaMemcpyHostToDevice);
    
    // Launch kernel
    int blockSize = 256;
    int numBlocks = (n + blockSize - 1) / blockSize;
    vectorAdd<<<numBlocks, blockSize>>>(d_a, d_b, d_c, n);
    
    // Copy result back
    cudaMemcpy(h_c, d_c, size, cudaMemcpyDeviceToHost);
}
```

**CUDA Memory йерархия:**
```
Fastest → Slowest:
1. Registers (per thread) - 0 cycles
2. Shared Memory (per block) - ~5 cycles  
3. L1 Cache - ~28 cycles
4. L2 Cache - ~200 cycles
5. Global Memory - ~400 cycles
6. Host Memory - ~10,000 cycles
```

#### **Част 3: OpenCL и алтернативи (8 мин)**

**OpenCL характеристики:**
```
✓ Cross-platform (AMD, Intel, NVIDIA, ARM)
✓ Open standard (Khronos Group)
✓ Поддържа CPU, GPU, FPGA, DSP
✗ По-сложен от CUDA
✗ По-малка общност
✗ По-бавно development
```

**Сравнение CUDA vs OpenCL:**

| Характеристика | CUDA | OpenCL |
|----------------|------|--------|
| Платформи | Само NVIDIA | Всички |
| Производителност | Отлична | Много добра |
| Екосистема | Богата | Ограничена |
| Learning curve | По-лесна | По-трудна |
| Библиотеки | cuDNN, cuBLAS | По-малко |
| Популярност в AI | Доминира | Рядко |

**Други технологии:**
- **ROCm (AMD)** - CUDA алтернатива за AMD
- **SYCL** - C++ abstraction layer
- **Vulkan Compute** - Graphics API с compute
- **DirectML** - Microsoft за Windows
- **Metal** - Apple за macOS/iOS

#### **Част 4: Приложения на GPU Computing (7 мин)**

**1. Изкуствен интелект:**
```python
# PyTorch пример - neural network training
import torch

# Проверка за CUDA
if torch.cuda.is_available():
    device = torch.device("cuda")
    print(f"Using GPU: {torch.cuda.get_device_name()}")
    
# Преместване на модел и данни на GPU
model = model.to(device)
data = data.to(device)

# Training е 50-100x по-бързо на GPU
```

**2. Cryptocurrency Mining:**
```
Ethereum hashrate:
- RTX 4090: 120 MH/s
- RTX 3080: 95 MH/s
- CPU i9: 0.5 MH/s
```

**3. Scientific Computing:**
- Molecular dynamics
- Weather simulation
- Protein folding (Folding@Home)
- Астрономически симулации

**4. Content Creation:**
- Video encoding (NVENC)
- 3D Rendering (OptiX)
- Image processing
- Ray tracing

### **4. ЗАТВЪРЖДАВАНЕ (25 минути)**

#### **Практическа работа: Анализ и benchmark**

**Задача 1: GPU спецификации (10 мин)**

Използване на GPU-Z:
```
1. Стартирайте GPU-Z
2. Запишете:
   - GPU модел и архитектура
   - Брой CUDA cores
   - Memory size и bandwidth
   - Compute capability
   - TDP и температури
```

**Таблица за попълване:**
| Параметър | Стойност | Обяснение |
|-----------|----------|-----------|
| CUDA Cores | | |
| Base Clock | | |
| Memory | | |
| Bandwidth | | |
| TDP | | |

**Задача 2: Производителност - CPU vs GPU (10 мин)**

**Python тест с NumPy vs CuPy:**
```python
import numpy as np
import time

# CPU версия
def cpu_matrix_multiply(size=5000):
    a = np.random.randn(size, size)
    b = np.random.randn(size, size)
    
    start = time.time()
    c = np.dot(a, b)
    cpu_time = time.time() - start
    return cpu_time

# GPU версия (ако има CuPy)
try:
    import cupy as cp
    
    def gpu_matrix_multiply(size=5000):
        a = cp.random.randn(size, size)
        b = cp.random.randn(size, size)
        
        start = time.time()
        c = cp.dot(a, b)
        cp.cuda.Stream.null.synchronize()
        gpu_time = time.time() - start
        return gpu_time
except:
    print("CuPy not available")

# Сравнение
cpu_time = cpu_matrix_multiply()
gpu_time = gpu_matrix_multiply()
print(f"CPU: {cpu_time:.2f}s")
print(f"GPU: {gpu_time:.2f}s")  
print(f"Speedup: {cpu_time/gpu_time:.1f}x")
```

**Задача 3: Избор на GPU за различни нужди (5 мин)**

**Сценарии:**

A. **AI Researcher:**
```
Нужди: Training large models
Препоръка: RTX 4090 или A100
Причина: Tensor cores, 24GB+ VRAM
```

B. **Game Developer:**
```
Нужди: Ray tracing development
Препоръка: RTX 4070 Ti
Причина: RT cores, DLSS testing
```

C. **Data Scientist (budget):**
```
Нужди: Local experiments
Препоръка: RTX 3060 12GB
Причина: Достъпна цена, достатъчно VRAM
```

D. **Video Editor:**
```
Нужди: 4K/8K encoding
Препоръка: RTX 4080
Причина: NVENC, AV1 support
```

### **5. ОБОБЩЕНИЕ (8 минути)**

**Ключови моменти:**
- GPU са оптимизирани за паралелни задачи
- CUDA доминира в AI/ML областта
- OpenCL е cross-platform алтернатива
- Избор на GPU зависи от конкретните нужди

**Дискусионни въпроси:**
1. Ще заменят ли GPU процесорите CPU?
2. Защо NVIDIA доминира в AI пазара?
3. Какво е бъдещето - специализирани чипове или универсални GPU?

**Демонстрация на реално приложение:**
- Stable Diffusion image generation
- Real-time ray tracing в игра
- AI upscaling с DLSS

### **6. ДОМАШНА РАБОТА (2 минути)**

**Задачи:**

1. **Изследователска:**
   - Проучете TPU (Tensor Processing Units) на Google
   - Сравнете с GPU за AI workloads
   - Напишете есе (2 страници)

2. **Практическа:**
   - Инсталирайте CUDA Toolkit
   - Компилирайте и пуснете CUDA samples
   - Документирайте резултатите

3. **Проектна:**
   - Изберете проблем подходящ за GPU
   - Опишете как би се паралелизирал
   - Оценете потенциалното ускорение

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Разбиране на GPU архитектура | 25% |
| Познаване на CUDA/OpenCL | 20% |
| Анализ на производителност | 20% |
| Избор на подходящ GPU | 15% |
| Практическа работа | 15% |
| Активност и участие | 5% |

### ИНДИКАТОРИ ЗА КАЧЕСТВО:
- Обяснява разликата CPU vs GPU
- Идентифицира паралелизируеми задачи
- Разбира CUDA програмен модел
- Може да оцени GPU производителност

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли защо GPU са по-бързи за някои задачи?
2. Мога ли да обясня CUDA архитектурата?
3. Знам ли кога да използвам GPU computing?
4. Готов ли съм да програмирам за GPU?

### ОЧАКВАНИ ТРУДНОСТИ:
- Абстрактност на паралелното програмиране
- Сложност на memory йерархията
- Липса на GPU хардуер за демонстрации

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: GPU СПЕЦИФИКАЦИИ 2025

**NVIDIA Gaming/Professional:**
```
RTX 4090: 16,384 cores, 24GB, 450W, $1599
RTX 4080: 9,728 cores, 16GB, 320W, $1199
RTX 4070 Ti: 7,680 cores, 12GB, 285W, $799
RTX 4060 Ti: 4,352 cores, 16GB, 165W, $499

A100: 6,912 cores, 80GB HBM2e, 400W, $10,000
H100: 16,896 cores, 80GB HBM3, 700W, $30,000
```

**AMD Radeon:**
```
RX 7900 XTX: 6,144 cores, 24GB, 355W
RX 7900 XT: 5,376 cores, 20GB, 315W
RX 7800 XT: 3,840 cores, 16GB, 263W
```

### ПРИЛОЖЕНИЕ 2: CUDA ПРИМЕРЕН КОД

**Matrix multiplication kernel:**
```cuda
#define TILE_SIZE 16

__global__ void matrixMul(float *A, float *B, float *C, 
                          int N) {
    __shared__ float sA[TILE_SIZE][TILE_SIZE];
    __shared__ float sB[TILE_SIZE][TILE_SIZE];
    
    int row = blockIdx.y * TILE_SIZE + threadIdx.y;
    int col = blockIdx.x * TILE_SIZE + threadIdx.x;
    
    float sum = 0.0f;
    
    for (int tile = 0; tile < N/TILE_SIZE; tile++) {
        // Load tiles into shared memory
        sA[threadIdx.y][threadIdx.x] = 
            A[row * N + tile * TILE_SIZE + threadIdx.x];
        sB[threadIdx.y][threadIdx.x] = 
            B[(tile * TILE_SIZE + threadIdx.y) * N + col];
        
        __syncthreads();
        
        // Compute partial product
        for (int k = 0; k < TILE_SIZE; k++) {
            sum += sA[threadIdx.y][k] * 
                   sB[k][threadIdx.x];
        }
        
        __syncthreads();
    }
    
    C[row * N + col] = sum;
}
```

### ПРИЛОЖЕНИЕ 3: AI FRAMEWORKS GPU SUPPORT

**Framework поддръжка:**
```python
# TensorFlow
import tensorflow as tf
print("GPUs:", tf.config.list_physical_devices('GPU'))

# PyTorch  
import torch
print("CUDA available:", torch.cuda.is_available())
print("GPU count:", torch.cuda.device_count())

# JAX
import jax
print("GPUs:", jax.devices())
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
