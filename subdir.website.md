## [subdir.website.conf](subdir.website.conf)

Записать в переменную `$base` путь до директории с доменом:

```nginx
set $base /home/user/htdocs/domain.org;
```

Установить откуда будут браться файлы для корня:

```nginx
root $base/mainsite/public;
```

В случае выше, должно быть так:

```
- domain.org
  - mainsite
    - public
      - somefiles
```

При переходе на domain.org, будут открыты файлы из `/mainsite/public/`.

Другие сайты в поддиректориях:

```nginx
location ^~ /subdir1 {
  alias $base/subdir1/public;
}
```

```
- domain.org
  - subdir1
    - public
      - somefiles
```

Обработка ошибки 404, если файл `404.html` в корне домена `/home/user/htdocs/domain.org`:

```nginx
error_page 404 /404.html;
```

```
- domain.org
  - 404.html
```

Если файл `404.html` в поддиректории домена:

```nginx
error_page 404 /subdir/404.html;
```

```
- domain.org
  - subdir
    - public
      - 404.html
```

Это не переадресация. Файл откроется там, где ошибка, без `.html` в конце.

_Если отображается не кастомная страница ошибки 404, а обычная страница, вероятней всего это ошибка, означающая что не удалось найти файл с кастомной страницей ошибки._
