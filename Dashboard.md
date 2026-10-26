---
title: Dashboard
tags: [index]
---
# Dashboard

Нужен плагин Dataview. Таблицы строятся из frontmatter заметок в `Books/` и `Articles/`.

## Читаю сейчас
```dataview
TABLE author AS "Автор", format AS "Формат", date_started AS "Начал"
FROM "Books" OR "Articles"
WHERE status = "reading"
SORT date_started DESC
```

## Очередь
```dataview
TABLE author AS "Автор", direction AS "Направление"
FROM "Books"
WHERE status = "to-read"
SORT file.ctime ASC
```

## Прочитано
```dataview
TABLE author AS "Автор", rating AS "Оценка", date_finished AS "Дочитал"
FROM "Books"
WHERE status = "read"
SORT date_finished DESC
```

## По направлениям
```dataview
TABLE length(rows) AS "Книг", length(filter(rows, (r) => r.status = "read")) AS "Прочитано"
FROM "Books"
FLATTEN direction AS dir
GROUP BY dir
```

## Inbox ждёт разбора
```dataview
LIST
FROM "00-Inbox"
WHERE file.name != "Как пользоваться Inbox"
```

Up: [[Home]]
