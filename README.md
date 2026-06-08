# Power Gym — тренажерний зал

Демо-сайт тренажерного залу Power Gym (статична вёрстка, UA/EN).

## Локальный просмотр

Сайт нельзя открывать как `file://` — ES-модули в `js/main.js` требуют HTTP-сервер.

```bash
python -m http.server 8080
```

Откройте http://localhost:8080

## GitHub Pages

1. Создайте репозиторий на GitHub (например `Power-Gym` в организации `Lyr1cU`).
2. Привяжите remote и запушьте `main`:

   ```bash
   git init
   git add .
   git commit -m "Initial Power Gym site"
   git branch -M main
   git remote add origin https://github.com/Lyr1cU/Power-Gym.git
   git push -u origin main
   ```

3. В репозитории: **Settings → Pages → Build and deployment → Source** выберите **GitHub Actions** (если деплой упал с `Get Pages site failed` — это обязательный шаг).
4. После push workflow опубликует сайт по адресу:

   `https://lyr1c1.github.io/Power-Gym/`

## Админка (Decap CMS)

Адрес: `https://lyr1c1.github.io/Power-Gym/admin/` (после деплоя).

Редактируются `content/*.json`: абонементи, галерея, відгуки, контакти. Новые фото загружаются в `img/uploads/`.

### Локально (без GitHub-входа)

Два терминала:

```bash
# 1 — прокси для записи в репозиторий
npx decap-server

# 2 — сайт
python -m http.server 8080
```

Откройте http://localhost:8080/admin/ — вход не нужен (`local_backend: true` в `admin/config.yml`).

### Продакшн (вход через GitHub)

Можно использовать **тот же OAuth-прокси на Vercel**, что и для Zerno (`netlify-cms-oauth-rust.vercel.app`), либо задеплоить свой fork [ublabs/netlify-cms-oauth](https://github.com/ublabs/netlify-cms-oauth).

1. **OAuth-прокси на Vercel** (если ещё не настроен для Zerno):
   - [vercel.com/new](https://vercel.com/new) → Import → `ublabs/netlify-cms-oauth`
   - Deploy → URL прокси, например `https://netlify-cms-oauth-rust.vercel.app`

2. **GitHub OAuth App** (Settings → Developer settings → OAuth Apps):
   - Application name: `Power Gym CMS`
   - Homepage URL: `https://lyr1c1.github.io/Power-Gym/`
   - Authorization callback URL: `https://netlify-cms-oauth-rust.vercel.app/callback` (URL прокси + `/callback`)

   > Если прокси уже используется для Zerno с тем же callback URL — можно **переиспользовать тот же OAuth App** (Client ID / Secret в Vercel). Достаточно write-доступа к репозиторию `Lyr1cU/Power-Gym`.

3. **Переменные в Vercel** (Project → Settings → Environment Variables):
   - `OAUTH_GITHUB_CLIENT_ID`
   - `OAUTH_GITHUB_CLIENT_SECRET`
   - Redeploy после изменений

4. В `admin/config.yml` поле `base_url` должно совпадать с URL прокси (без `/callback`) — уже настроено.

5. У GitHub-аккаунта для входа в админку должен быть **write** доступ к `Lyr1cU/Power-Gym`.

После **Publish** в админке изменения попадают в `main` → GitHub Actions обновляет сайт (1–2 мин).

## Структура

- `content/*.json` — абонементи, галерея, відгуки, контакти
- `js/i18n/` — переклади UI (UA/EN)
- `css/` — стилі (акцент `#FFD400`, база `#1a1a1a`)
- `img/` — фото залу (webp)
- `admin/` — Decap CMS
