# 内容
laravelの[公式ドキュメント](https://laravel.com/docs/11.x)を読んで実際に手を動かしてみるためのリポジトリです。

# まとめ
## Getting Started
### Configuration

- aboutコマンドでアプリケーションの設定、ドライバ、環境の概要を表示できる。 特定の環境の設定を表示するには、`--only`オプションを使用する。
```
php artisan about
```

- .envについて
  - ファイル内のどの環境変数も、サーバーレベルやシステムレベルの環境変数などの外部環境変数によって上書きが可能。
  - .envファイルは機密情報が含まれるためソースコード管理に含めるべきではない。ただ、暗号化を用いることで安全に管理することも可能
  - laravelはAPP_ENV環境変数が外部から提供されているか、もしくは起動コマンドの引数に指定されている場合は.env.[APP_ENV]ファイルを読み込むようになる

    ```
    php artisan env:encrypt
    ```
    
    環境変数の呼び出しとデフォルト値
    ```
    'debug' => env('APP_DEBUG', false),
    ```

- 現在の環境の取得方法
```
$environment = App::environment();
```

- configファイルの設定値にアクセスする方法。ファイル名と設定値のキーをドットでつなげる。

```
use Illuminate\Support\Facades\Config;
 
$value = Config::get('app.timezone');
 
$value = config('app.timezone');
 
// Retrieve a default value if the configuration value does not exist...
$value = config('app.timezone', 'Asia/Seoul');
```

- 静的解析を支援するために型付きで値を取得することも可能

```
Config::string('config-key');
Config::integer('config-key');
Config::float('config-key');
Config::boolean('config-key');
Config::array('config-key');
```

- configファイルのキャッシュ
  - 本番環境などではconfigファイルをキャッシュすることでパフォーマンスを向上させることができる
  - configファイルをキャッシュすると.envファイルの内容はそれ以降はロードされなくなる。そのため、env関数はconfigファイルからのみ使用されるようにするべき。
  - キャッシュ以降はenv関数は外部のシステムレベルの環境変数のみを返すようになる
```
php artisan config:cache
```

