{
    "date": "2016-02-01",
    "description": null,
    "draft": false,
    "id": 134,
    "image": null,
    "meta_title": null,
    "slug": "keep-running-app",
    "tags": [
        "online"
    ],
    "title": "Держим приложение запущенным(macos x)",
    "type": "post"
}
Если у вас есть приложение которое вы бы хотели держать всегда запущенным, вам поможет этот рецепт:

-	Прописываем агент в ~/Library/LaunchAgents

Например telegram.plist

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>Label</key>
  <string>user.telegram</string>
  <key>KeepAlive</key>
  <true/>
  <key>Program</key>  <string>/Applications/Telegram.app/Contents/MacOS/Telegram</string>
</dict>
</plist>
```

-	Запускаем наш агент

```
launchctl load ~/Library/LaunchAgents/telegram.plist
```

После этого наше приложение будет постоянно запускаться после закрытия.

-	Вернуть как было, можно командой:

```
launchctl remove user.telegram
```
