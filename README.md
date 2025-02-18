# Vue Jobs

## 📌 Описание
Vue Jobs - это веб-приложение для управления вакансиями, созданное на основе Vue 3, Vue Router, Tailwind CSS и JSON Server для имитации backend API.

## 📂 Структура проекта
```
vue-jobs/
│── .vscode/                     # Настройки VS Code
│── node_modules/                # Установленные npm пакеты
│── public/                      # Статические файлы
│── src/                         # Исходный код проекта
│   │── assets/                  # Статические ресурсы
│   │   │── images/              # Изображения
│   │   │── main.css             # Стили
│   │── components/              # Повторно используемые компоненты
│   │   │── BackButton/          # Кнопка "Назад"
│   │   │── Card/                # Компонент карточки
│   │   │── Hero/                # Главный экран
│   │   │── HomeCards/           # Карточки на главной странице
│   │   │── JobListings/         # Список вакансий
│   │   │── Navbar/              # Навигационная панель
│   │── docs/                    # Документация по Vue
│   │   │── vue_composition_api.md
│   │   │── vue_lifecycle.md
│   │   │── vue_options_api.md
│   │── router/                   # Файл маршрутов
│   │   │── index.js
│   │── views/                    # Основные страницы
│   │   │── AddJobView.vue        # Страница добавления вакансии
│   │   │── EditJobView.vue       # Страница редактирования вакансии
│   │   │── HomeView.vue          # Главная страница
│   │   │── JobsView.vue          # Страница со списком вакансий
│   │   │── JobView.vue           # Страница просмотра вакансии
│   │   │── NotFoundView.vue      # Страница 404
│   │── App.vue                   # Основной компонент приложения
│   │── App2.vue                  # Альтернативный App.vue
│   │── jobs.json                 # Данные о вакансиях (JSON Server)
│   │── jobs2.json                # Альтернативный JSON файл
│   │── main.js                   # Входная точка приложения
│── package.json                  # Список зависимостей
│── vite.config.js                 # Конфигурация Vite
│── README.md                     # Документация проекта
```

## 🚀 Установка и запуск
### 1. Установите зависимости
```sh
npm install
```

### 2. Запуск приложения в режиме разработки
```sh
npm run dev
```

### 3. Запуск JSON сервера (backend API)
```sh
npm run server
```

### 4. Сборка для продакшена
```sh
npm run build
```

## 🔗 Основные зависимости
- `vue` (3.5.13) - основа фреймворка
- `vue-router` (4.5.0) - маршрутизация
- `tailwindcss` (3.4.17) - стилизация
- `json-server` (1.0.0-beta.3) - фейковый backend API
- `axios` (1.7.9) - работа с API
- `vue-toastification` (2.0.0-rc.5) - всплывающие уведомления

## 🌍 API Эндпоинты (JSON Server)
- `GET /api/jobs` - получить список вакансий
- `GET /api/jobs/:id` - получить вакансию по ID
- `POST /api/jobs` - создать вакансию
- `PUT /api/jobs/:id` - обновить вакансию
- `DELETE /api/jobs/:id` - удалить вакансию

## 📌 Фичи
✅ Добавление вакансии через форму  
✅ Редактирование вакансии  
✅ Удаление вакансии с подтверждением  
✅ Перенаправление после добавления/редактирования  
✅ Интеграция с `vue-toastification`  
✅ Навигация через `vue-router`  
✅ Стилизация с `tailwindcss`  
✅ JSON Server как mock API  
