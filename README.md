# Switch PHP ver of Xserver by directory
XserverでディレクトリごとにPHPバージョンを変える方法です。  
このリポジトリのファイルをサーバにアップロードすることで確認できるかと思います。  
ドキュメントルートの`index.php`では5.6、`php74/index.php`だと7.4になると思います。

## 手順
おおまかな手順は以下の4つです。

1. エックスアクセラレータの無効化
1. ディレクトリのパーミッション変更
1. 必要ファイルの設置
2. 待つ

## 1. エックスアクセラレータの無効化
- 設定をしたいドメインに対して、エックスアクセラレータを無効化してください。
- サーバーキャッシュを無効化してください。
- ブラウザキャッシュを無効化してください。

## 2. ディレクトリのパーミッション変更
- 該当ディレクトリのパーミッションを`755`に変更してください。

## 3. 必要ファイルの設置
該当ディレクトリに以下の2ファイルを設置してください。

### `.htaccess`
パーミッションはデフォルトのままでOKです。  
※ パスは場所によって合わせてください。

```cgi
AddHandler myphp-script .php .fphp
Action myphp-script "/php.fcgi"
```

### `php.fcgi`
パーミッションは755に変更してください。  
使いたいPHPバージョンに合わせてください。
```cgi=
#!/usr/bin/sh
exec /usr/bin/php-fcgi5.6
```

※ 以下がPHPバージョンのパス一覧になります。

#### PHPのパス一覧

| PHPバージョン | パス | 
| -------- | -------- | 
| PHP 8.2.x(CGI)     | /usr/bin/php8.2-cgi 又は /usr/bin/php-fcgi8.2     | 
| PHP 8.2.x(CLI)     | /usr/bin/php8.2     | 
| PHP 8.1.x(CGI)	 | /usr/bin/php8.1-cgi 又は /usr/bin/php-fcgi8.1     | 
| PHP 8.1.x(CLI)     | /usr/bin/php8.1     | 
| PHP 8.0.x(CGI)     | /usr/bin/php8.0-cgi 又は /usr/bin/php-fcgi8.0     | 
| PHP 8.0.x(CLI)     | /usr/bin/php8.0     | 
| PHP 7.4.x(CGI)     | /usr/bin/php7.4-cgi 又は /usr/bin/php-fcgi7.4     | 
| PHP 7.4.x(CLI)     | /usr/bin/php7.4     | 
| PHP 7.3.x(CGI)     | /usr/bin/php7.3-cgi 又は /usr/bin/php-fcgi7.3     | 
| PHP 7.3.x(CLI)     | /usr/bin/php7.3     | 
| PHP 7.2.x(CGI)     | /usr/bin/php7.2-cgi 又は /usr/bin/php-fcgi7.2     | 
| PHP 7.2.x(CLI)     | /usr/bin/php7.2     | 
| PHP 7.1.x(CGI)	 | /usr/bin/php7.1-cgi 又は /usr/bin/php-fcgi7.1     | 
| PHP 7.1.x(CLI)     | /usr/bin/php7.1     | 
| PHP 7.0.x(CGI)     | /usr/bin/php7.0-cgi 又は /usr/bin/php-fcgi7.0     | 
| PHP 7.0.x(CLI)     | /usr/bin/php7.0     | 
| PHP 5.6.x(CGI)     | /usr/bin/php5.6-cgi 又は /usr/bin/php-fcgi5.6     | 
| PHP 5.6.x(CLI)     | /usr/bin/php5.6     | 
| PHP 5.5.x(CGI)     | /usr/bin/php-fcgi5.5     | 
| PHP 5.5.x(CLI)     | /usr/bin/php5.5     | 
| PHP 5.4.x(CGI)     | /usr/bin/php-fcgi5.4     | 
| PHP 5.4.x(CLI)     | /usr/bin/php5.4     | 
| PHP 5.3.x(CGI)     | /usr/bin/php-fcgi5.3     | 
| PHP 5.3.x(CLI)     | /usr/bin/php5.3     | 
| PHP 5.1.x(CGI)     | /usr/bin/php-fcgi5.1    | 
| PHP 5.1.x(CLI)     | /usr/bin/php5.1     | 
---

## 4. 待つ
すぐにバージョンが変わらない場合があります。
5分ほど、コーヒーでも飲んで待ってみてください。
