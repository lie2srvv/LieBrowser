# LieBrowser

<p align="center">
  <img src="app/src/forkRelease/res/mipmap-xxxhdpi/ic_launcher.png" width="96" height="96" alt="LieBrowser Logo">
</p>

<p align="center">
  <b>Быстрый, приватный Android-браузер на базе GeckoView и Fenix без слежки и телеметрии.</b>
</p>

---

## 🚀 О проекте

**LieBrowser** — это независимый форк Mozilla Firefox (Fenix) / GeckoView для Android, созданный для максимальной скорости, безопасности и конфиденциальности пользователя.

В отличие от официального Firefox, в браузере полностью вырезана навязчивая телеметрия, отключены партнёрские промо-блоки, предустановлен независимый поисковик **LieWeb**, а также усилена защита от трекеров и фингерпринтинга на уровне движка Gecko.

---

## ⚡ Ключевые отличия от стандартного Firefox

### 1. 🔍 Встроенный поисковик LieWeb (LieSearch)
* По умолчанию используется независимый приватный поисковый движок **LieWeb** (`search.lie2srvv.com`).
* Поддержка быстрых поисковых подсказок (autocompletion) через API без передачи личных идентификаторов и истории поиска сторонним корпорациям.

### 2. 🛡️ Полное отключение телеметрии и слежки
* Отключены встроенные механизмы сбора аналитики: `toolkit.telemetry.enabled = false`, `toolkit.telemetry.unified = false`.
* Отключены удалённые эксперименты и телеметрические зонды Nimbus (`experiments.supported = false`).
* Заблокирован сбор метрик производительности и пользовательских действий.

### 3. 🔒 Усиленные настройки приватности (Hardened Gecko Engine)
* **Total Cookie Protection (dFPI):** изоляция куков для каждого домена (`network.cookie.cookieBehavior = 5`), предотвращающая межсайтовую слежку.
* **Защита от WebRTC IP-утечек:** скрытие локального IP-адреса устройства при WebRTC-соединениях (`media.peerconnection.ice.no_host = true`).
* **Анти-фингерпринтинг и анти-майнинг:** включена нативная блокировка сбора цифрового отпечатка браузера (`privacy.trackingprotection.fingerprinting.enabled = true`) и криптомайнеров.
* **Запрет предзагрузки DNS:** предотвращение скрытых DNS-запросов до реального перехода по ссылке (`network.dns.disablePrefetch = true`, `network.prefetch-next = false`).
* **Корректная работа с VPN:** DNS-over-HTTPS по умолчанию не перехватывает системный DNS, что гарантирует работу кастомных DNS-маршрутов и туннелей.

### 4. 🧹 Чистый домашний экран без рекламы
* Удалены рекламные блоки Pocket и спонсируемые статьи («Sponsored Stories»).
* Отключены спонсируемые поисковые подсказки («Sponsored Suggestions»).
* Удалены промо-вставки Mozilla VPN и сторонних сервисов.
* Предустановлены быстрые закладки на сервисы экосистемы Lie (`vpn.lie2srvv.com`, `cord.lie2srvv.com`, `mail.lie2srvv.com`).

### 5. 🧩 Расширенная поддержка аддонов и `about:config`
* Доступен встроенный `about:config` для тонкой настройки параметров движка прямо с телефона.
* Расширенный каталог дополнений (uBlock Origin, Dark Reader и др.) с возможностью установки из локального файла `.xpi`.

---

## 📦 Сборка из исходников

### Требования
* **JDK 17+**
* **Android SDK** (API Level 34+, build-tools 34.0.0+)
* Переменная окружения `ANDROID_HOME` или `ANDROID_SDK_ROOT`

### Команды для сборки

```bash
# Клонирование репозитория
git clone https://github.com/lie2srvv/LieBrowser.git
cd LieBrowser

# Сборка Release APK (архитектуры arm64-v8a, armeabi-v7a, x86_64)
./gradlew app:assembleForkRelease

# Готовые APK появятся в каталоге:
# gradle/build/app/outputs/apk/forkRelease/
```

### Подпись APK для установки на устройство

```bash
apksigner sign --ks ~/.android/debug.keystore \
  --ks-pass pass:android \
  --ks-key-alias androiddebugkey \
  --key-pass pass:android \
  --out LieBrowser-arm64.apk \
  gradle/build/app/outputs/apk/forkRelease/app-arm64-v8a-forkRelease-unsigned.apk
```

---

## 📄 Лицензия

Исходный код распространяется под лицензией **Mozilla Public License 2.0 (MPL-2.0)**.
Ознакомиться с текстом лицензии можно в файле `LICENSE` или по адресу: http://mozilla.org/MPL/2.0/
