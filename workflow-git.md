# Git Workflow (локальный)

Автор: [Руслан Хуснетдинов](https://github.com/ruslankhh).

## Содержание

- [Предисловие](#Предисловие)
    - [Цель](#Цель)
    - [Профит](#Профит)
- [Инструкция](#Инструкция)
    - [1. Подтягиваем последние изменения в master](#1-Подтягиваем-последние-изменения-в-master)
    - [2. Создаем ветку](#2-Создаем-ветку)
    - [3. Работаем в ветке](#3-Работаем-в-ветке)
    - [4. Создаём PR на GitHub-е](#4-Создаём-pr-на-github-е)
    - [5. Review](#5-review)
    - [6. Проверяем наличие конфликтов на GitHub-е](#6-Проверяем-наличие-конфликтов-на-github-е)
    - [7. Мержим PR на GitHub-е](#7-Мержим-pr-на-github-е)
    - [8. Удаляем ветку на GitHub-е](#8-Удаляем-ветку-на-github-е)
    - [9. Проверяем карточку в CMS](#9-Проверяем-карточку-в-cms)
- [Changelog](#changelog)

## Предисловие

### Цель

Удобная работа с Git. Использование всех его возможностей.

### Профит

- удобная работа с Git;
- чистый master;
- удобное возвращение до нужно коммита (`git reset/revert <commit>`)
- review кода;
- не нужно ждать окончания сборки во время разработки;

## Инструкция

### 1. Подтягиваем последние изменения в master

```bash
# on branch master
git pull --rebase
```

### 2. Создаем ветку

1. Определяем имя ветки

    Название ветки для конкретной карточки и скрипта должно быть вида:

    - `card_<card_id>_<script_id>` — для новой карточки;

    - `card_<card_id>_<script_id>_fix` — для фикса карточки;

    - `card_<card_id>_<script_id>_new` — для доработки карточки;

    Последние два пункта для случаев, когда сложность задачи больше minor (уточнить у тимлида).

2. Проверяем, есть ли уже такая ветка

    ```bash
    # on branch master
    git checkout <branch name>
    ```

    - Если ветка есть, то git скачает её и перейдет в неё.

    - Если ветки нет, то git выдаст ошибку.

3. Создаём ветку, если такой ветки нет, из master-а

    ```bash
    # on branch master
    git checkout -b <branch name>
    ```

### 3. Работаем в ветке

1. Вносим изменения

    ```bash
    # on branch <branch name>
    git status
    git add .
    git commit -m "c#<card_id>#<chunk_number> <message>"
    ```

2. Пушим ветку в origin

    ```bash
    # on branch <branch name>
    git push origin <branch name>
    ```

### 4. Создаём PR на GitHub-е

PR — Pull Request. В качестве ревьювера назначаем ответственное по релизу лицо (тимлид или кто-то другой). Можно добавить комментарии.

![PR](./_assets/images/pr.png)

### 5. Review

Ревьювер проверяет, оставляет комментарии и ставит статус для PR в зависимости от результата проверки (Changes requested/Approved). В зависимости от результата проверки выполняем следующие действия:

- **Changes requested**: вносим изменения и уведомляем ревьювера об окончании.

    ![Approved](./_assets/images/changes-requested.png)

- **Approved**: идём дальше.

    ![Approved](./_assets/images/approved.png)

### 6. Проверяем наличие конфликтов на GitHub-е

- Если есть конфликты: исправляем их.

  ![Check conflicts 0](./_assets/images/check-conflicts-0.png)

  1. Мержим master в нашу ветку:

      ```bash
      # on branch <branch name>
      git pull origin master
      ```

  2. Устраняем конфликты в редакторе.

  3. Проверяем карточку на localhost-е:

      ```bash
      open http://localhost:4567/lessons/<card_id>
      ```

      - Если ошибки есть: исправляем их.

      - Если ошибок нет: идём дальше.

  4. Пушим изменения в origin:

      ```bash
      git add .
      git commit
      git push origin <branch name>
      ```
- Если нет конфликтов: идём дальше.

    ![Check conflicts 1](./_assets/images/check-conflicts-1.png)

### 7. Мержим PR на GitHub-е

![Check conflicts 1](./_assets/images/merge.png)

### 8. Удаляем ветку на GitHub-е

### 9. Проверяем карточку в CMS

## Changelog

#### 09.08.2017

- 1\. — добавил пункт с подтягиванием послених изменений в master
- 5\. — изменил названия статусов PR
- 6\. — добавил проверку на GitHub-е
- Добавил изображения
