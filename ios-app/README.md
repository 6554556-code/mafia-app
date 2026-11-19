# Мафия — обёртка для iPhone (Capacitor 8)

Приложение стартует со своей страницы `www/index.html` (лежит внутри, работает без сети):
за 6 секунд проверяет, отвечает ли сервер, и открывает игру с https://app.iplaymafia.com —
или показывает «Деревня осталась без связи». Сама игра живёт на сервере (`../`),
здесь — только «рамка»: иконка, заставка, экраны «нет сети» и мостик к функциям iPhone.

| | |
|---|---|
| Название под иконкой | Мафия |
| Bundle ID | `com.iplaymafia.app` |
| Адрес игры | `GAME` в `www/index.html` + `server.allowNavigation` в `capacitor.config.json` |
| Нет сети при запуске | `www/index.html` (проверка связи, 6 с) |
| Связь оборвалась во время загрузки | `www/offline.html` (`server.errorPath`) |
| Связь оборвалась в игре | карточка в `public/index.html`, кнопка ведёт на `www/index.html` |
| Опознавалка для сервера | к User-Agent добавляется `MafiaApp-iOS` |

## Функции iPhone (зовутся из `public/index.html`, на сайте их нет)
- **Вибро** (`@capacitor/haptics`): твой ход — лёгкий щелчок, тебя убили — «ошибка», конец партии — победа/поражение.
- **Поделиться** (`@capacitor/share`): кнопка 📤 под «Сыграть ещё».
- **Напоминание в 20:00** (`@capacitor/local-notifications`): предлагаем один раз после первой партии; без сервера.

## Первая сборка на Маке
```
git clone https://github.com/6554556-code/mafia-app
cd mafia-app/ios-app
npm i
npx cap add ios
npm run assets
npx cap sync ios
npx cap open ios
```
В Xcode: App → Signing & Capabilities → Team = твой аккаунт → выбрать iPhone → ▶ Run.

## Когда что-то поменялось
- Игра (сервер, страницы) — **пересобирать приложение не нужно**, обновится само.
- `server.url` специально не используем: без сети iPhone ждёт его 30+ секунд на тёмном экране.
- Этот каталог (настройки, иконка, `offline.html`) — `git pull`, затем `npx cap sync ios`, затем ▶ в Xcode.
- Иконка или заставка — заменить файлы в `assets/`, затем `npm run assets` и `npx cap sync ios`.

Папка `ios/` создаётся командой `npx cap add ios` и в git не хранится.
