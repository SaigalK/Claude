# Zoho MCP Servers для Claude

Дата дослідження: 2026-04-25

## Що таке MCP для Zoho?

MCP (Model Context Protocol) дозволяє Claude напряму працювати з Zoho через природну мову — читати контакти, угоди, інвойси, створювати записи без ручного перемикання між вкладками.

---

## Найкращий варіант: Unified CRM + Books

**[Mgabr90/zoho-mcp-server](https://github.com/Mgabr90/zoho-mcp-server)**

### Що підтримує:

| Модуль | Дії |
|--------|-----|
| CRM — Контакти | Читання, створення, оновлення |
| CRM — Акаунти | Читання, створення, оновлення |
| CRM — Угоди | Читання, створення, оновлення |
| CRM — Ліди | Читання, створення, оновлення |
| CRM — Задачі / Нотатки | Читання, створення |
| Books — Клієнти | Читання, створення |
| Books — Інвойси | Читання, створення |
| Books — Платежі | Читання |
| Books — Кошториси | Читання, створення |

### Особливості:
- Двостороння синхронізація CRM ↔ Books
- Генерація інвойсу напряму з угоди CRM
- Пошук по всіх системах одночасно
- OAuth 2.0 (безпечна авторизація з автооновленням токену)

### Встановлення:
```bash
git clone https://github.com/Mgabr90/zoho-mcp-server.git
cd zoho-mcp-server
npm install
cp .env.example .env
# Заповнити .env: ZOHO_CLIENT_ID, ZOHO_CLIENT_SECRET, ZOHO_REFRESH_TOKEN
npm run build
npm start
```

### Підключення до Claude Code:
```bash
claude mcp add zoho -- node /path/to/zoho-mcp-server/dist/index.js
```

---

## Альтернативи

### Тільки CRM (читання)
**[CDataSoftware/zoho-crm-mcp-server-by-cdata](https://github.com/CDataSoftware/zoho-crm-mcp-server-by-cdata)**
- Read-only доступ через JDBC
- Підходить якщо потрібно тільки переглядати дані

### Тільки CRM (повний CRUD)
**[junnaisystems/zoho-crm-mcp](https://github.com/junnaisystems/Zoho-CRM-MCP)**
- Повна робота з CRM: створення, читання, оновлення, видалення
- OAuth-базована авторизація

### Офіційна аналітика від Zoho
**[zoho/analytics-mcp-server](https://github.com/zoho/analytics-mcp-server)**
- Офіційний від Zoho
- Тільки Zoho Analytics (не CRM)

### Офіційний Zoho MCP
**[zoho.com/mcp](https://www.zoho.com/mcp/)**
- Офіційний протокол від Zoho для підключення LLM до всіх Zoho-продуктів

---

## Що потрібно для налаштування

1. Зайти в [Zoho Developer Console](https://api-console.zoho.com/)
2. Створити новий Client (Server-based Application)
3. Отримати: `Client ID`, `Client Secret`
4. Пройти OAuth і отримати `Refresh Token`
5. Заповнити `.env` файл
6. Підключити до Claude Code

---

## Рекомендація

Для роботи з САНЕКО-БУД найбільш корисний **Mgabr90/zoho-mcp-server** — дає доступ і до CRM (клієнти, угоди) і до Books (інвойси, кошториси) в одному сервері.
