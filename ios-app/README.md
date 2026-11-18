# Мафия — обёртка для iPhone (Capacitor 8)

Приложение открывает игру с https://app.iplaymafia.com. Сама игра живёт на сервере (`../`),
здесь — только «рамка»: иконка, заставка запуска, экран «нет сети» и мостик к функциям iPhone.

| | |
|---|---|
| Название под иконкой | Мафия |
| Bundle ID | `com.iplaymafia.app` |
| Адрес игры | `server.url` в `capacitor.config.json` |
| Нет сети | `www/offline.html` (`server.errorPath`) |
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
- Этот каталог (настройки, иконка, `offline.html`) — `git pull`, затем `npx cap sync ios`, затем ▶ в Xcode.
- Иконка или заставка — заменить файлы в `assets/`, затем `npm run assets` и `npx cap sync ios`.

Папка `ios/` создаётся командой `npx cap add ios` и в git не хранится.
