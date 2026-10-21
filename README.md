# LogHive

Сервис сбора ошибок. Приложения отправляют свои ошибки по HTTP, LogHive склеивает одинаковые в группы со счётчиком и показывает их в веб-панели. О новых ошибках и всплесках сообщает в Mattermost.

Учебный проект по курсу «Прикладные аспекты DevOps».

## Команда

| Участник | Роль | Зона ответственности |
|---|---|---|
| Икромжонов Шодиёрбек | DevOps | Сервер, Docker, Gitea, Drone CI, Wiki, Prometheus и Grafana, пайплайн и автодеплой |
| Жидкова Валерия | Backend | API на C#, PostgreSQL, группировка ошибок, тесты, демо-магазин |
| Иванова Алёна | Frontend | Веб-панель на HTML, CSS и JavaScript |

## Структура

```
backend/     API на ASP.NET Core (.NET 10) и демо-магазин
frontend/    веб-панель: HTML, CSS, JavaScript
infra/       docker-compose, конфиги nginx, Prometheus, Grafana, Drone
docs/        архитектура, описание API, материалы для Wiki и защиты
```

## Стек

- **Backend:** C#, ASP.NET Core, PostgreSQL, Entity Framework Core, xUnit
- **Frontend:** HTML, CSS, JavaScript без сборки
- **Инфраструктура:** Ubuntu Server 24.04, Docker Compose, Gitea, Drone CI, Wiki.js, Prometheus, Grafana, nginx

## Как работаем с репозиторием

- Ветка `main` — то, что выкатывается на сервер. Напрямую в неё не пушим.
- Под каждую задачу — своя ветка: `backend/priem-oshibok`, `frontend/spisok-oshibok`, `infra/drone`.
- Изменения попадают в `main` через pull request, его одобряет хотя бы ещё один человек.
- Drone на каждый pull request собирает проект и прогоняет тесты, после слияния в `main` — выкатывает на сервер.

## Полный цикл

```
git push → Drone: сборка → тесты → Docker-образ → деплой → Grafana следит за работой
```
