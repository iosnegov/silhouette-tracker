# Silhouette Tracker: Оценка позы человека в реальном времени с аппаратным ускорением CUDA

*Конвейер оценки позы человека в реальном времени, полностью настроенный в изолированном Conda-окружении для простой установки, воспроизводимости и переносимости.*

> [!WARNING]
> **Репозиторий заархивирован**
> 
> Этот проект больше не поддерживается. 
> 
> **Контекст:**  
> Изначально этот репозиторий начался как учебное задание в университете. Вместо того чтобы просто выполнить задачу и удалить код, я решил расширить его до структурированного мини-проекта, чтобы глубже изучить концепции оценки позы человека (human pose estimation) и компьютерного зрения. Тем не менее, это был исключительно личный эксперимент, и он никогда не задумывался как решение, готовое к использованию в реальных проектах (production-ready), или как учебное пособие.
> 
> **Причина архивации:**  
> В связи с этим у меня больше нет планов по дальнейшей поддержке этой кодовой базы. Данный репозиторий заархивирован исключительно как исторический артефакт: он служит своеобразным срезом моего начального этапа обучения и напоминанием о том, с чего я начинал свой путь в разработке программного обеспечения.

## Доступная документация / Available Documentation

- [English Documentation](README.md) (current document / текущий документ)
- [Документация на русском языке](README_RU.md)

## Структура проекта

```
silhouette-tracker/
├── .env.example    # Шаблон конфигурации
├── SBOMs/          # Метаданные зависимостей
├── app/            # Исходный код приложения
├── models/         # Модели YOLOv8 для работы
└── videos/         # Видео для работы
```

## Инструкция по установке и запуску

### I. Предварительные требования

| Компонент | Требование |
| :--- | :--- |
| **Менеджер пакетов** | [`Micromamba`](https://github.com/mamba-org/mamba) |
| **Операционная система** | GNU/Linux-система |
| **Архитектура** | `x86_64` |
| **Аппаратное обеспечение** | Видеокарта NVIDIA с драйвером, поддерживающим CUDA >= 12.6.3 |
| **Инструменты разработки** *(Опционально)* | [`conda-lock`](https://github.com/conda/conda-lock) и [`pip-licenses`](https://github.com/raimon49/pip-licenses) |

> **Примечание:**  
> Это не строгие требования, а базовое окружение, в котором код гарантированно работает «из коробки». Возможны альтернативные настройки, но они могут потребовать ручной конфигурации.

### II. Клонирование репозитория

```bash
git clone https://github.com/snegoviol/silhouette-tracker.git
cd silhouette-tracker
```

### III. Создание и активация виртуальной среды

```bash
micromamba env create -p ./.venv -f SBOMs/conda-linux-64-lock.yml
micromamba activate ./.venv
```

### IV. Подготовка данных

Модели и видео не включены в репозиторий из-за ограничений размера. Чтобы скачать модели, выполните следующие команды:

```bash
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8n-pose.pt && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8s-pose.pt && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8m-pose.pt && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8l-pose.pt && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8x-pose.pt
```

В директорию `videos` вы можете добавить любое видео. В качестве демонстрации вы можете скачать видео с сайта [Pexels Free Stock Videos](https://www.pexels.com/videos/).  
Например: [Mother and daughter with face masks at the park by Gustavo Fring from Pexels](https://www.pexels.com/video/mother-and-daughter-with-face-masks-at-the-park-4265036/).

### V. Настройка конфигурации через `.env`

1. Создайте файл `.env` из шаблона:

    ```bash
    cp .env.example .env
    ```

2. Отредактируйте `.env` в любом текстовом редакторе (например, `nano`, `VSCode`):

    ```bash
    nano .env
    ```

3. Настройте параметры: файл разделен на секции — измените значения в соответствии с вашими задачами. Например:

    ```bash
    # === MODEL CONFIGURATION ===
    MODEL_NAME=yolov8m-pose.pt
    CONFIDENCE=0.8

    # === VIDEO CONFIGURATION ===
    VIDEO_NAME=example-pexels.mp4

    # === DISPLAY SETTINGS ===
    DISPLAY_WIDTH=1020
    DISPLAY_HEIGHT=720

    # === PATH CONFIGURATION ===
    MODELS_DIR=models
    VIDEOS_DIR=videos
    ```

### VI. Запуск приложения

```bash
python -m app.main
```

## Лицензия

Каждый файл в этом репозитории распространяется под лицензией [MIT No Attribution License](LICENSE.txt).
