# Диаграммы: DOM и События

## DOM-дерево

```
document
└── html
    ├── head
    │   ├── title
    │   └── link
    └── body
        ├── header
        │   └── nav
        │       ├── a (Профиль)
        │       └── a (Матчи)
        ├── main
        │   ├── h1 ("CS2 Stats")
        │   └── div.cards
        │       ├── div.card
        │       └── div.card
        └── footer
```

## Поток событий

```mermaid
graph TD
    A[Пользователь кликает] --> B[Браузер создаёт Event]
    B --> C["addEventListener callback"]
    C --> D{Что делать?}
    D --> E[Изменить DOM]
    D --> F[Загрузить данные]
    D --> G[Показать/скрыть элемент]
    
    E --> H[Пользователь видит изменение]
    F --> H
    G --> H
```

## Fetch + DOM

```
1. Пользователь вводит Steam ID
           ↓
2. JS: fetch('api/players/...')
           ↓
3. API возвращает JSON данные
           ↓
4. JS: createElement, textContent = data
           ↓
5. JS: appendChild → страница обновляется
           ↓
6. Пользователь видит данные игрока
```
