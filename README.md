# DOM и События

## Цель урока
Научиться менять HTML-страницу через JavaScript и реагировать на действия пользователя.

## Что такое DOM?

**DOM** (Document Object Model) — дерево всех элементов на странице. JavaScript может читать и менять это дерево.

**Аналогия из CS2:** DOM — это раунд в режиме реального времени. HTML — статичная карта, а DOM + JS — это то, что происходит **во время игры**: двери открываются, дым рассеивается, аптечки исчезают.

## Поиск элементов

```javascript
// По id (один элемент)
const title = document.getElementById('main-title');

// По классу (коллекция)
const cards = document.getElementsByClassName('card');

// Универсальный (CSS-селектор)
const title = document.querySelector('#main-title');       // первый
const allCards = document.querySelectorAll('.card');        // все

// Рекомендуется: querySelector / querySelectorAll
```

## Изменение элементов

### Текст
```javascript
const title = document.querySelector('#player-name');
title.textContent = 's1mple';          // Только текст
title.innerHTML = '<strong>s1mple</strong>';  // HTML
```

### Стили
```javascript
const card = document.querySelector('.card');
card.style.backgroundColor = '#1a1a2e';
card.style.border = '2px solid #e94560';
card.style.borderRadius = '12px';
```

### Классы (лучше, чем style напрямую)
```javascript
card.classList.add('active');
card.classList.remove('active');
card.classList.toggle('active');    // Переключить
card.classList.contains('active'); // Проверить
```

### Атрибуты
```javascript
const img = document.querySelector('img');
img.setAttribute('src', 'new-avatar.png');
img.getAttribute('alt');
```

## Создание элементов

```javascript
// Создать элемент
const newCard = document.createElement('div');
newCard.classList.add('card');
newCard.textContent = 'Новая карточка';

// Добавить на страницу
document.querySelector('.container').appendChild(newCard);

// Удалить элемент
newCard.remove();
```

## События

### addEventListener

```javascript
const btn = document.querySelector('#search-btn');

btn.addEventListener('click', () => {
  console.log('Кнопка нажата!');
});
```

### Частые события

| Событие | Когда |
|---------|-------|
| `click` | Клик мышкой |
| `dblclick` | Двойной клик |
| `mouseover` | Наведение мыши |
| `mouseout` | Мышь ушла |
| `keydown` | Клавиша нажата |
| `keyup` | Клавиша отпущена |
| `input` | Ввод текста |
| `change` | Значение изменилось |
| `submit` | Отправка формы |
| `load` | Страница загрузилась |

### Объект события (event)
```javascript
btn.addEventListener('click', (event) => {
  console.log(event.target);     // Элемент, по которому кликнули
  console.log(event.type);       // Тип события ('click')
});
```

### Обработка формы
```javascript
const form = document.querySelector('#search-form');

form.addEventListener('submit', (e) => {
  e.preventDefault();  // Отменить перезагрузку страницы

  const input = document.querySelector('#steam-id');
  const steamId = input.value;

  console.log(`Ищем игрока: ${steamId}`);
});
```

### Делегирование событий
Вместо привязки к каждому элементу — привяжи к родителю:

```javascript
// ❌ Плохо — событие на каждую карточку
document.querySelectorAll('.card').forEach(card => {
  card.addEventListener('click', () => { ... });
});

// ✅ Хорошо — одно событие на контейнер
document.querySelector('.cards').addEventListener('click', (e) => {
  const card = e.target.closest('.card');
  if (card) {
    console.log('Клик по карточке:', card.textContent);
  }
});
```

## Работа с данными: fetch + DOM

```javascript
async function loadPlayer(steamId) {
  try {
    const res = await fetch(`https://api.opendota.com/api/players/${steamId}`);
    const data = await res.json();

    document.querySelector('#player-name').textContent = data.profile.personaname;
    document.querySelector('#avatar').src = data.profile.avatarfull;
  } catch (error) {
    console.error('Ошибка:', error);
  }
}
```

---

## Чеклист "Я понял"
- [ ] Умею находить элементы (querySelector)
- [ ] Умею менять текст, стили, классы
- [ ] Умею создавать и удалять элементы
- [ ] Умею обрабатывать события (click, submit, input)
- [ ] Понимаю `e.preventDefault()`
- [ ] Умею загружать данные с API и вставлять в DOM
