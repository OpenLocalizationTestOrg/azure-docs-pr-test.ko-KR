---
title: "Azure에서 PHP 및 MySQL 웹 앱 aaaBuild | Microsoft Docs"
description: "자세한 내용은 방법 tooget Azure에서 작업 하는 PHP 응용 프로그램 연결 tooa로 MySQL 데이터베이스를 Azure입니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Azure에서 PHP 및 MySQL 웹앱 빌드

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다. 이 자습서에서는 toocreate PHP Azure에서 응용 프로그램을 구성 하 고 tooa MySQL 데이터베이스를 연결 하는 방법을 보여 줍니다. 완료되면 [Laravel](https://laravel.com/) 앱이 Azure App Service Web Apps에서 실행됩니다.

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure에서 MySQL 데이터베이스 만들기
> * PHP 응용 프로그램 tooMySQL 연결
> * Hello 앱 tooAzure 배포
> * Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure에서 진단 로그 스트림
> * Hello Azure 포털에서에서 hello 응용 프로그램 관리

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

* [Git 설치](https://git-scm.com/)
* [PHP 5.6.4 이상 설치](http://php.net/downloads.php)
* [작성기 설치](https://getcomposer.org/doc/00-intro.md)
* PHP 확장 Laravel 요구에 따라 hello를 사용 하도록 설정: OpenSSL, PDO MySQL, Mbstring, 토크 나이저, XML
* [MySQL 설치 및 시작](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>로컬 MySQL 준비

이 단계에서는 이 자습서에서 사용할 데이터베이스를 로컬 MySQL 서버에 만듭니다.

### <a name="connect-toolocal-mysql-server"></a>Toolocal MySQL 서버 연결

터미널 창에서 tooyour 로컬 MySQL 서버를 연결 합니다. 이 자습서에서는이 터미널 윈도우 toorun 모든 hello 명령을 사용할 수 있습니다.

```bash
mysql -u root -p
```

암호에 대 한 메시지가 hello에 대 한 hello 암호 입력 `root` 계정. 참조 루트 계정 암호를 기억 하지 못하는 경우 [MySQL: tooReset 루트 암호를 hello 어떻게](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)합니다.

명령이 성공적으로 실행되면 MySQL 서버가 실행되고 있습니다. 그렇지 않은 경우 로컬 MySQL 서버의 다음 hello에서 시작 되었는지 확인 [MySQL 사후 설치 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)합니다.

### <a name="create-a-database-locally"></a>로컬에서 데이터베이스 만들기

Hello에 `mysql` 요청에서 데이터베이스를 만듭니다.

```sql 
CREATE DATABASE sampledb;
```

`quit`을 입력하여 서버 연결을 종료합니다.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>로컬에서 PHP 앱 만들기
이 단계에서는 Laravel 샘플 응용 프로그램 가져오고, 해당 데이터베이스를 구성한 후 로컬로 실행합니다. 

### <a name="clone-hello-sample"></a>복제 hello 예제

Hello 터미널 창에서 `cd` tooa 작업 디렉터리입니다.

다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`tooyour 복제 된 디렉터리입니다.
Hello 필요한 패키지를 설치 합니다.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>MySQL 연결 구성

Hello 리포지토리 루트 라는 파일을 만들어 *.env*합니다. Hello에 변수를 다음 복사 hello *.env* 파일입니다. Hello 대체  _&lt;root_password >_ 자리 표시자 hello MySQL 루트 사용자의 암호를 사용 합니다.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Laravel hello를 사용 하는 방법에 대 한 내용은 _.env_ 파일, 참조 [Laravel 환경 구성](https://laravel.com/docs/5.4/configuration#environment-configuration)합니다.

### <a name="run-hello-sample-locally"></a>Hello 샘플을 로컬로 실행

실행 [Laravel 데이터베이스 마이그레이션을](https://laravel.com/docs/5.4/migrations) toocreate hello 테이블 hello 응용 프로그램 요구 합니다. 어떤 테이블에서에서 생성 됩니다 hello 마이그레이션에서 봐 hello toosee _데이터베이스/마이그레이션_ hello Git 리포지토리에 디렉터리입니다.

```bash
php artisan migrate
```

새 Laravel 응용 프로그램 키를 생성합니다.

```bash
php artisan key:generate
```

Hello 응용 프로그램을 실행 합니다.

```bash
php artisan serve
```

너무 이동`http://localhost:8000` 브라우저에서 합니다. Hello 페이지에서 몇 가지 작업을 추가 합니다.

![PHP tooMySQL 성공적으로 연결](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Azure에서 MySQL 만들기

이 단계에서는 [MySQL용 Azure 데이터베이스(미리 보기)](/azure/mysql)에서 MySQL 데이터베이스를 만듭니다. 나중 hello PHP 응용 프로그램 tooconnect toothis 데이터베이스를 구성 합니다.

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>MySQL 서버 만들기

Hello로 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 서버 만들기 [az mysql server 만들기](/cli/azure/mysql/server#create) 명령입니다.

Hello에 hello 나타나는 MySQL 서버 이름을 대체 다음 명령을,  _&lt;mysql_server_name >_ 자리 표시자 (유효한 문자는 `a-z`, `0-9`, 및 `-`). 이 이름은의 hello MySQL 서버 호스트 이름 부분입니다 (`<mysql_server_name>.database.windows.net`), toobe 전역적으로 고유 해야 합니다.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Hello MySQL 서버를 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>서버 방화벽 구성

방화벽 규칙 만들기 MySQL 서버 tooallow 클라이언트에 대 한 연결 hello를 사용 하 여 [az mysql 서버 방화벽 규칙 만들기](/cli/azure/mysql/server/firewall-rule#create) 명령입니다.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> MySQL (미리 보기)에 대 한 azure 데이터베이스 연결만 tooAzure 서비스를 제한할 현재 하지 않습니다. Azure의 IP 주소를 동적으로 할당 것이 더 나은 tooenable 모든 IP 주소입니다. hello 서비스가 미리 보기입니다. 데이터베이스를 보호하기 위해 더 나은 방법을 제공하도록 계획되어 있습니다.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>MySQL 서버를 로컬로 tooproduction 연결

Hello 터미널 창에서 Azure의 toohello MySQL 서버를 연결 합니다. 에 대 한 이전에 지정 된 값이 hello를 사용 하 여  _&lt;mysql_server_name >_합니다.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

암호를 입력 하는 경우 사용 _tr0ngPa $$ w0rd!_, hello 데이터베이스를 만들 때 지정 합니다.

### <a name="create-a-production-database"></a>프로덕션 데이터베이스 만들기

Hello에 `mysql` 요청에서 데이터베이스를 만듭니다.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>사용 권한이 있는 사용자 만들기

라는 데이터베이스 사용자 만들기 _phpappuser_ hello에서 모든 권한을 지정 `sampledb` 데이터베이스입니다.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

입력 하 여 hello 서버 연결을 종료 `quit`합니다.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>응용 프로그램 tooAzure MySQL 연결

이 단계에서는 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 만든 hello PHP 응용 프로그램 toohello MySQL 데이터베이스를 연결 합니다.

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Hello 데이터베이스 연결 구성

Hello 리포지토리 루트에서 만듭니다는 _. env.production_ 파일과 복사본 hello에 변수를 수행 합니다. Hello 자리 표시자 대체  _&lt;mysql_server_name >_합니다.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Hello 변경 내용을 저장 합니다.

> [!TIP]
> MySQL 연결 정보를이 파일 hello Git 저장소에서 이미 제외 되었습니다. toosecure (참조 _.gitignore_ hello 리포지토리 루트에). 이상에서는 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 데이터베이스 응용 프로그램 서비스 tooconnect tooyour에서 환경 변수 tooconfigure 방법 방법을 배웁니다. 환경 변수를 사용 하면 hello을 필요가 없습니다 *.env* 앱 서비스에서 파일입니다.
>

### <a name="configure-ssl-certificate"></a>SSL 인증서 구성

기본적으로 MySQL용 Azure 데이터베이스에는 클라이언트로부터의 SSL 연결이 적용됩니다. 사용 해야 tooconnect tooyour Azure의 MySQL 데이터베이스를 한 _.pem_ SSL 인증서입니다.

열기 _config/database.php_ hello 추가 _sslmode_ 및 _옵션_ 매개 변수가 너무`connections.mysql`hello 코드 다음에 나온 것 처럼 합니다.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn 어떻게 toogenerate이 _certificate.pem_, 참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](../mysql/howto-configure-ssl.md)합니다.

> [!TIP]
> hello 경로 _/ssl/certificate.pem_ tooan 기존 가리키는 _certificate.pem_ hello Git 리포지토리에서 파일입니다. 이 파일은 이 자습서의 편의를 위해 제공됩니다. 최상의 방법으로 _.pem_ 인증서를 원본 제어에 커밋하지 않아야 합니다. 
>

### <a name="test-hello-application-locally"></a>로컬로 hello 응용 프로그램 테스트

데이터베이스 마이그레이션에 Laravel 실행 _. env.production_ MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 MySQL 데이터베이스의 환경 파일 toocreate hello 테이블 hello으로 합니다. 에 유의 해야 _. env.production_ Azure의 hello 연결 정보 tooyour MySQL 데이터베이스 사용 하는 합니다.

```bash
php artisan migrate --env=production --force
```

_.env.production_에는 아직 유효한 응용 프로그램 키가 없습니다. Hello 터미널에 것에 대 한 새를 생성 합니다.

```bash
php artisan key:generate --env=production --force
```

Hello 샘플 응용 프로그램을 실행 _. env.production_ hello 환경 파일로 합니다.

```bash
php artisan serve --env=production
```

너무 이동`http://localhost:8000`합니다. 오류 없이 hello 페이지가 로드 되 면 hello PHP 응용 프로그램이 Azure에서 MySQL 데이터베이스 사용 toohello 연결 합니다.

Hello 페이지에서 몇 가지 작업을 추가 합니다.

![PHP 성공적으로 연결 tooAzure 데이터베이스 MySQL (미리 보기)에 대 한](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.

### <a name="commit-your-changes"></a>변경 내용을 커밋합니다

변경 내용을 Git 명령을 toocommit 다음 hello를 실행 합니다.

```bash
git add .
git commit -m "database.php updates"
```

앱 배포 준비 toobe입니다.

## <a name="deploy-tooazure"></a>TooAzure 배포

이 단계에서는 hello PHP MySQL에 연결 된 응용 프로그램 tooAzure 앱 서비스를 배포합니다.

### <a name="create-an-app-service-plan"></a>App Service 계획 만들기

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>웹앱 만들기

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Set hello PHP 버전

응용 프로그램 hello set hello PHP 버전 hello를 사용 하 여 필요한 [az webapp 구성 집합](/cli/azure/webapp/config#set) 명령입니다.

hello 다음 명령은 설정 hello PHP 버전 too_7.0_ 합니다.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>데이터베이스 설정 구성

이전에 지적으로 환경 변수를 사용 하 여 앱 서비스에서 tooyour Azure의 MySQL 데이터베이스를 연결할 수 있습니다.

앱 서비스 환경 변수를 설정 _앱 설정_ hello를 사용 하 여 [az webapp 구성 appsettings 세트](/cli/azure/webapp/config/appsettings#set) 명령입니다.

hello 다음 명령을 hello 응용 프로그램 설정을 구성 `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, 및 `DB_PASSWORD`합니다. Hello 자리 표시자를 대체  _&lt;응용 프로그램 이름 >_ 및  _&lt;mysql_server_name >_합니다.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Hello PHP를 사용할 수 있습니다 [getenv](http://www.php.net/manual/function.getenv.php) 메서드 tooaccess hello 설정 합니다. 사용 하 여 hello Laravel 코드는 [env](https://laravel.com/docs/5.4/helpers#method-env) hello PHP 통해 래퍼 `getenv`합니다. 에 MySQL 구성 예를 들어 hello _config/database.php_ 코드 다음 hello 같습니다.

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Laravel 환경 변수 구성

Laravel에는 App Service의 응용 프로그램 키가 필요합니다. 앱 설정을 사용하여 키를 구성할 수 있습니다.

사용 하 여 `php artisan` toogenerate too_.env_ 저장 하지 않고 새 응용 프로그램 키입니다.

```bash
php artisan key:generate --show
```

Hello 응용 프로그램 키에에서 설정 hello 앱 서비스 웹 앱 hello를 사용 하 여 [az webapp 구성 appsettings 세트](/cli/azure/webapp/config/appsettings#set) 명령입니다. Hello 자리 표시자를 대체  _&lt;응용 프로그램 이름 >_ 및  _&lt;outputofphpartisankey: 생성 >_합니다.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`지시 Laravel tooreturn 디버깅 정보 hello 웹 앱을 배포할 때 오류가 발생 합니다. 프로덕션 응용 프로그램을 실행할 때 설정 너무`false`, 변수인 더 안전 합니다.

### <a name="set-hello-virtual-application-path"></a>Hello 가상 응용 프로그램 경로 설정 합니다

Hello 웹 앱에 대 한 hello 가상 응용 프로그램 경로 설정 합니다. 이 단계는 필요 하기 때문에 hello [Laravel 응용 프로그램 수명 주기](https://laravel.com/docs/5.4/lifecycle) hello에서 시작 _공용_ hello 응용 프로그램의 루트 디렉터리가 아닌 디렉터리입니다. Hello 루트 디렉터리에서 해당 수명 주기를 시작 하는 다른 PHP 프레임 워크는 hello 가상 응용 프로그램 경로 수동으로 구성 하지 않고 작업할 수 있습니다.

Hello를 사용 하 여 hello 가상 응용 프로그램 경로 설정 [az 리소스 업데이트](/cli/azure/resource#update) 명령입니다. Hello 대체  _&lt;응용 프로그램 이름 >_ 자리 표시자입니다.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

기본적으로 Azure 앱 서비스는 hello 루트 가상 응용 프로그램 경로 가리키는 (_/_) hello의 toohello 루트 디렉터리는 응용 프로그램 파일 배포 (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>배포 사용자 구성

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>로컬 Git 배포 구성

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Git에서 tooAzure 푸시

Azure 원격 tooyour 로컬 Git 리포지토리를 추가 합니다.

```bash
git remote add azure <paste_copied_url_here>
```

Toohello Azure 원격 toodeploy hello PHP 응용 프로그램을 푸시하십시오. 이전 hello 배포 사용자의 hello 만들기의 일부로 제공한 hello 암호를 묻는 메시지가 나타납니다.

```bash
git push azure master
```

배포하는 동안 Azure App Service는 진행 상황을 Git에 전합니다.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Hello 배포 프로세스를 설치 한다는 것을 알 수 있습니다 [작성기](https://getcomposer.org/) hello 끝에 패키지 합니다. 앱 서비스 기본 배포 하는 동안 이러한 자동화가 실행 되지 않으면, 하므로이 샘플 리포지토리에는 3 개의 추가 파일의 루트 디렉터리 tooenable에서:
>
> - `.deployment`-이 파일을 통해 앱 서비스 toorun 알 `bash deploy.sh` hello 사용자 지정 배포 스크립트로 합니다.
> - `deploy.sh`-사용자 지정 배포 스크립트 hello 합니다. Hello 파일을 검토 하는 경우 실행 되는지 표시 됩니다 `php composer.phar install` 후 `npm install`합니다.
> - `composer.phar`-hello 작성기 패키지 관리자.
>
> 이 접근 방식을 tooadd 모든 단계 tooyour Git 기반 배포 tooApp 서비스를 사용할 수 있습니다. 자세한 내용은 [사용자 지정 배포 스크립트](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)를 참조하세요.
>

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure 웹 앱을 찾아보기

너무 찾아보기`http://<app_name>.azurewebsites.net` 몇 가지 작업 toohello 목록을 추가 합니다.

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

축하합니다! Azure App Service에서 데이터 기반 PHP 앱을 실행하고 있습니다.

## <a name="update-model-locally-and-redeploy"></a>로컬에서 모델 업데이트 및 다시 배포

이 단계에서는 간단 하 게 변경 toohello 잘못 수행 `task` 데이터 모델 및 hello webapp, 한 다음 업데이트 tooAzure hello를 게시 합니다.

Hello 작업 시나리오에 대 한 작업을 완료로 표시할 수 있도록 hello 응용 프로그램을 수정 합니다.

### <a name="add-a-column"></a>열 추가

Hello 터미널, toohello 루트 hello Git 리포지토리를 이동 합니다.

Hello에 대 한 새 데이터베이스 마이그레이션을 생성 `tasks` 테이블:

```bash
php artisan make:migration add_complete_column --table=tasks
```

이 명령은 생성 되는 hello 마이그레이션 파일의 이름을 hello를 표시 합니다. _database/migrations_에서 이 파일을 찾아서 엽니다.

Hello 대체 `up` 메서드 코드 다음 hello로:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

hello 이전 부울 열에에서 추가 hello `tasks` 라는 테이블 `complete`합니다.

Hello 대체 `down` hello 롤백 작업에 대 한 코드 다음 hello로 메서드:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

Hello 터미널, Laravel 데이터베이스 마이그레이션을 toomake hello 변경 hello 로컬 데이터베이스에서 실행 합니다.

```bash
php artisan migrate
```

Hello에 따라 [Laravel ô ä ¢](https://laravel.com/docs/5.4/eloquent#defining-models), hello 모델 `Task` (참조 _app/Task.php_) toohello 매핑합니다 `tasks` 기본적으로 테이블입니다.

### <a name="update-application-logic"></a>응용 프로그램 논리 업데이트

열기 hello *routes/web.php* 파일입니다. hello 응용 프로그램의 경로 및 여기에 비즈니스 논리를 정의합니다.

Hello 파일의 hello 끝 코드 다음 hello로 경로 추가 합니다.

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

hello 위의 코드는 간단한 업데이트 toohello 데이터 모델의 hello 값을 토글하 여 `complete`합니다.

### <a name="update-hello-view"></a>Hello 뷰 업데이트

열기 hello *resources/views/tasks.blade.php* 파일입니다. Hello `<tr>` 여는 태그과 바꿉니다.

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

코드 변경 내용을 hello 행 색 hello 작업이 완료 되었는지 여부에 따라 앞에 오는 번호입니다.

Hello 다음 줄에 다음 코드는 hello를 사용할 수 있습니다.

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

코드 다음 hello hello 줄을 전체를 바꿉니다.

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

hello 앞의 코드에서는 앞에서 정의한 hello 경로 참조 하는 hello 전송 단추

### <a name="test-hello-changes-locally"></a>Hello 변경 내용을 로컬 테스트

Hello Git 리포지토리의 루트 디렉터리 hello hello 개발 서버를 실행 합니다.

```bash
php artisan serve
```

toosee hello 작업을 상태 변경, 탐색 너무`http://localhost:8000` 및 선택 hello 확인란을 선택 합니다.

![추가 된 확인란 tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.

### <a name="publish-changes-tooazure"></a>변경 내용을 tooAzure 게시

Hello 터미널, hello Azure 데이터베이스 hello 프로덕션 연결 문자열 toomake hello 변경 Laravel 데이터베이스 마이그레이션을 실행 합니다.

```bash
php artisan migrate --env=production --force
```

Git에서 모든 hello 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

한 번 hello `git push` 를 마치면 toohello Azure 웹 앱과 테스트 hello 새로운 기능을 탐색 합니다.

![모델 및 데이터베이스 변경 내용이 게시 tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

모든 작업을 추가한 hello 데이터베이스에 유지 됩니다. 업데이트 toohello 데이터 스키마 기존 데이터는 그대로 둡니다.

## <a name="stream-diagnostic-logs"></a>진단 로그 스트림

PHP 응용 프로그램 hello Azure 앱 서비스에서 실행 되는 동안 hello 콘솔 로그 파이프 된 tooyour 터미널 얻을 수 있습니다. 이런 방식으로 가져올 수 있습니다 hello 같은 진단 메시지 toohelp 응용 프로그램 오류를 디버깅 합니다.

스트리밍을 사용 하 여 hello toostart 로그 [az webapp 비상 로그](/cli/azure/webapp/log#tail) 명령입니다.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

스트리밍 로그 시작 된 후 일부 웹 트래픽을 hello 브라우저 tooget의 hello Azure 웹 앱을 새로 고칩니다. 이제 콘솔 로그 파이프 된 toohello 터미널을 볼 수 있습니다. 콘솔 로그가 즉시 표시되지 않으면 30초 후에 다시 확인합니다.

언제 든 지에서 스트리밍을 toostop 로그 형식 `Ctrl` + `C`합니다.

> [!TIP]
> PHP 응용 프로그램 hello 표준 צ ְ ײ [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello 콘솔. hello 샘플 응용 프로그램에서이 접근 방식을 사용 하 여 _app/Http/routes.php_합니다.
>
> 웹 프레임 워크로 [Laravel Monolog 사용 하 여](https://laravel.com/docs/5.4/errors) hello 로깅 공급자입니다. toosee tooget Monolog toooutput toohello 콘솔 메시지는 방법 참조 [PHP: 어떻게 toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)합니다.
>
>

## <a name="manage-hello-azure-web-app"></a>Hello Azure 웹 앱 관리

Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toomanage hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-php-mysql/access-portal.png)

웹앱의 개요 페이지가 표시됩니다. 여기서 중지, 시작, 다시 시작, 찾아보기 및 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.

왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 페이지를 제공 합니다.

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure에서 MySQL 데이터베이스 만들기
> * PHP 응용 프로그램 tooMySQL 연결
> * Hello 앱 tooAzure 배포
> * Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure에서 진단 로그 스트림
> * Hello Azure 포털에서에서 hello 응용 프로그램 관리

다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap tooa 웹 앱의 이름을 합니다.

> [!div class="nextstepaction"]
> [지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램](app-service-web-tutorial-custom-domain.md)
