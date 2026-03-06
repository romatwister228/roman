# Заметки: DOM и События

## 💡 Ключевые мысли

### querySelector — твой основной инструмент
Используй `querySelector` и `querySelectorAll` вместо `getElementById/ClassName`. Они принимают CSS-селекторы.

### classList вместо style
```css
/* В CSS файле */
.active { background: #e94560; color: white; }
```
```javascript
// В JS
element.classList.add('active');     // ✅ Чистый код
element.style.background = 'red';   // ❌ Грязный код
```

### e.preventDefault() — запомни!
На собесе 100% спросят. Отменяет стандартное поведение (перезагрузку страницы при submit, переход по ссылке).

---

## ⚠️ Типичные ошибки

- **DOMContentLoaded** — скрипт должен ждать загрузки DOM. Подключай скрипт перед `</body>` или используй `defer`
- **innerHTML для пользовательского ввода** — XSS-уязвимость! Используй `textContent`
- **Забыли await для fetch**

---

## ✅ Чек-лист
- [ ] querySelector/querySelectorAll
- [ ] textContent, innerHTML, classList
- [ ] addEventListener, event.target
- [ ] e.preventDefault()
- [ ] Fetch + DOM обновление
- [ ] Выполнил 6+ заданий
