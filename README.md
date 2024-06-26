# codespaces
codespacesの利用方法を学ぶ

## PHP環境構築まで

### デバッグ設定

1. 左側のアイコンからデバッグペインを開きます。

1. 「create a launch.json file」をクリックします。

1. 環境として「PHP」を選択してください。

```json
{
    // IntelliSense を使用して利用可能な属性を学べます。
    // 既存の属性の説明をホバーして表示します。
    // 詳細情報は次を確認してください: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 0,
            "runtimeArgs": [
                "-dxdebug.start_with_request=yes"
            ],
            "env": {
                "XDEBUG_MODE": "debug,develop",
                "XDEBUG_CONFIG": "client_port=${port}"
            }
        },
        {
            "name": "Launch Built-in web server",
            "type": "php",
            "request": "launch",
            "runtimeArgs": [
                "-dxdebug.mode=debug",
                "-dxdebug.start_with_request=yes",
                "-S",
                "localhost:0"
            ],
            "program": "",
            "cwd": "${workspaceRoot}",
            "port": 9003,
            "serverReadyAction": {
                "pattern": "Development Server \\(http://localhost:([0-9]+)\\) started",
                "uriFormat": "http://localhost:%s",
                "action": "openExternally"
            }
        }
    ]
}
```

### PHPの開発およびデバッグに必要なツールをインストール

```bash
sudo apt-get update
sudo apt-get install php php-cli php-zip unzip php-mbstring php-xml php-curl
sudo apt-get install php-xdebug
```

```bash
sudo vi /etc/php/7.x/cli/conf.d/20-xdebug.ini
```

```ini
zend_extension=xdebug.so
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.0.1
xdebug.client_port=9003
xdebug.log=/tmp/xdebug.log
```

## phpサーバー起動方法

### /workspaces/codespaces上で
```
php -S 127.0.0.1:8000 factorial.php
```