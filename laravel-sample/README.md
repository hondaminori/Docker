# Laravel用のフォルダ一式

 - このフォルダをローカルPCの適当な場所に保存する。
 - フォルダ名を適当なものに変える(設定ファイル等、変更不要)
 - docker-compose.ymlを編集する（※1）
 - VSCodeでトップフォルダーを開く（問題なくフォルダが開いても、何も存在していない）
 - コンテナ内の/var/www/htmlが空で開くので、以下コマンドを実行

composer create-project laravel/laravel .
実行後、数分待つ

　- .envのDBの部分を以下のように書き換える

DB_CONNECTION=pgsql
DB_HOST=db
DB_PORT=5432
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=secret

 - config/app.phpを編集する。

'timezone' => 'UTC',
　→　'timezone' => 'Asia/Tokyo',

Laravelのアプリ設定変更
config/app.phpを編集する。

'timezone' => 'UTC',
　→　'timezone' => 'Asia/Tokyo',
'locale' => env('APP_LOCALE', 'en'),
　→    'locale' => env('APP_LOCALE', 'ja'),
'fallback_locale' => env('APP_FALLBACK_LOCALE', 'ja'),
　→　'faker_locale' => env('APP_FAKER_LOCALE', 'ja_JP'),

デバッグバーをインストール
composer require barryvdh/laravel-debugbar

 - src/public/php/info.php というフォルダとファイルを作る。
 - 中身は <?php phpinfo(); ?> だけ。
 - http://localhost:8000/php/info.phpにアクセス。
 - 入ったバージョンを確認

phpのバージョンは上記のURLにアクセスしたら判明する。（2025/07/07 8.3.23）
Laravelのバージョンは以下
php artisan --version  （2025/07/07 12.21.0）



完了！


（※1）
既存のコンテナの中に同名のコンテナがあれば、初回コンテナ起動時にエラーになる。
それを回避するために既存にはないコンテナ名を指定する必要がある。
AP/DB/pgAdmin と、全部のコンテナを名前を変える必要がある。

ポート番号やDB名も既存のものと被らないように工夫が必要。


エラー発生時（順次追記）

```Failed to open stream: Permission denied```
パーミッションの問題なので、以下を実行。
chmod -R 777 storage bootstrap/cache

