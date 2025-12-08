# IT Professions Web App
Приложение на FastAPI, демонстрирующее IT-профессии через интерактивные плитки.

Главная страница — 6 анимированных плиток (DevOps, Backend, Frontend, PM, Design, QA).
Каждая открывает страницу с описанием профессии

## Запуск
#### 1. Клонировать/создать структуру
```bash
mkdir it-professions && cd it-professions
mkdir templates static
```
#### 2. Установить зависимости
```bash
python3 -m pip3 install fastapi jinja2 uvicorn
```
#### 3. Запустить
```bash
python3 main.py
```
ИЛИ
```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```
