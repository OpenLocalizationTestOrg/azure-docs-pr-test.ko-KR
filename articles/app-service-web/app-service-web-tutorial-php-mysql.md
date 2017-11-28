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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="1ceae-103">Azure에서 PHP 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="1ceae-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="1ceae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1ceae-105">이 자습서에서는 toocreate PHP Azure에서 응용 프로그램을 구성 하 고 tooa MySQL 데이터베이스를 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="1ceae-106">완료되면 [Laravel](https://laravel.com/) 앱이 Azure App Service Web Apps에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="1ceae-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ceae-109">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="1ceae-110">PHP 응용 프로그램 tooMySQL 연결</span><span class="sxs-lookup"><span data-stu-id="1ceae-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="1ceae-111">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1ceae-112">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="1ceae-113">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="1ceae-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="1ceae-114">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="1ceae-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ceae-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1ceae-115">Prerequisites</span></span>

<span data-ttu-id="1ceae-116">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="1ceae-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="1ceae-117">Git 설치</span><span class="sxs-lookup"><span data-stu-id="1ceae-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1ceae-118">PHP 5.6.4 이상 설치</span><span class="sxs-lookup"><span data-stu-id="1ceae-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="1ceae-119">작성기 설치</span><span class="sxs-lookup"><span data-stu-id="1ceae-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="1ceae-120">PHP 확장 Laravel 요구에 따라 hello를 사용 하도록 설정: OpenSSL, PDO MySQL, Mbstring, 토크 나이저, XML</span><span class="sxs-lookup"><span data-stu-id="1ceae-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="1ceae-121">MySQL 설치 및 시작</span><span class="sxs-lookup"><span data-stu-id="1ceae-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="1ceae-122">로컬 MySQL 준비</span><span class="sxs-lookup"><span data-stu-id="1ceae-122">Prepare local MySQL</span></span>

<span data-ttu-id="1ceae-123">이 단계에서는 이 자습서에서 사용할 데이터베이스를 로컬 MySQL 서버에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="1ceae-124">Toolocal MySQL 서버 연결</span><span class="sxs-lookup"><span data-stu-id="1ceae-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="1ceae-125">터미널 창에서 tooyour 로컬 MySQL 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="1ceae-126">이 자습서에서는이 터미널 윈도우 toorun 모든 hello 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="1ceae-127">암호에 대 한 메시지가 hello에 대 한 hello 암호 입력 `root` 계정.</span><span class="sxs-lookup"><span data-stu-id="1ceae-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="1ceae-128">참조 루트 계정 암호를 기억 하지 못하는 경우 [MySQL: tooReset 루트 암호를 hello 어떻게](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="1ceae-129">명령이 성공적으로 실행되면 MySQL 서버가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="1ceae-130">그렇지 않은 경우 로컬 MySQL 서버의 다음 hello에서 시작 되었는지 확인 [MySQL 사후 설치 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="1ceae-131">로컬에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-131">Create a database locally</span></span>

<span data-ttu-id="1ceae-132">Hello에 `mysql` 요청에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="1ceae-133">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="1ceae-134">로컬에서 PHP 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-134">Create a PHP app locally</span></span>
<span data-ttu-id="1ceae-135">이 단계에서는 Laravel 샘플 응용 프로그램 가져오고, 해당 데이터베이스를 구성한 후 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="1ceae-136">복제 hello 예제</span><span class="sxs-lookup"><span data-stu-id="1ceae-136">Clone hello sample</span></span>

<span data-ttu-id="1ceae-137">Hello 터미널 창에서 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="1ceae-138">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="1ceae-139">`cd`tooyour 복제 된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="1ceae-140">Hello 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="1ceae-141">MySQL 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-141">Configure MySQL connection</span></span>

<span data-ttu-id="1ceae-142">Hello 리포지토리 루트 라는 파일을 만들어 *.env*합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="1ceae-143">Hello에 변수를 다음 복사 hello *.env* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="1ceae-144">Hello 대체  _&lt;root_password >_ 자리 표시자 hello MySQL 루트 사용자의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="1ceae-145">Laravel hello를 사용 하는 방법에 대 한 내용은 _.env_ 파일, 참조 [Laravel 환경 구성](https://laravel.com/docs/5.4/configuration#environment-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="1ceae-146">Hello 샘플을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="1ceae-146">Run hello sample locally</span></span>

<span data-ttu-id="1ceae-147">실행 [Laravel 데이터베이스 마이그레이션을](https://laravel.com/docs/5.4/migrations) toocreate hello 테이블 hello 응용 프로그램 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="1ceae-148">어떤 테이블에서에서 생성 됩니다 hello 마이그레이션에서 봐 hello toosee _데이터베이스/마이그레이션_ hello Git 리포지토리에 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="1ceae-149">새 Laravel 응용 프로그램 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="1ceae-150">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="1ceae-151">너무 이동`http://localhost:8000` 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="1ceae-152">Hello 페이지에서 몇 가지 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-152">Add a few tasks in hello page.</span></span>

![PHP tooMySQL 성공적으로 연결](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="1ceae-154">PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="1ceae-155">Azure에서 MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-155">Create MySQL in Azure</span></span>

<span data-ttu-id="1ceae-156">이 단계에서는 [MySQL용 Azure 데이터베이스(미리 보기)](/azure/mysql)에서 MySQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="1ceae-157">나중 hello PHP 응용 프로그램 tooconnect toothis 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="1ceae-158">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="1ceae-159">MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-159">Create a MySQL server</span></span>

<span data-ttu-id="1ceae-160">Hello로 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 서버 만들기 [az mysql server 만들기](/cli/azure/mysql/server#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="1ceae-161">Hello에 hello 나타나는 MySQL 서버 이름을 대체 다음 명령을,  _&lt;mysql_server_name >_ 자리 표시자 (유효한 문자는 `a-z`, `0-9`, 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="1ceae-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="1ceae-162">이 이름은의 hello MySQL 서버 호스트 이름 부분입니다 (`<mysql_server_name>.database.windows.net`), toobe 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="1ceae-163">Hello MySQL 서버를 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="1ceae-164">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-164">Configure server firewall</span></span>

<span data-ttu-id="1ceae-165">방화벽 규칙 만들기 MySQL 서버 tooallow 클라이언트에 대 한 연결 hello를 사용 하 여 [az mysql 서버 방화벽 규칙 만들기](/cli/azure/mysql/server/firewall-rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="1ceae-166">MySQL (미리 보기)에 대 한 azure 데이터베이스 연결만 tooAzure 서비스를 제한할 현재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="1ceae-167">Azure의 IP 주소를 동적으로 할당 것이 더 나은 tooenable 모든 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="1ceae-168">hello 서비스가 미리 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-168">hello service is in preview.</span></span> <span data-ttu-id="1ceae-169">데이터베이스를 보호하기 위해 더 나은 방법을 제공하도록 계획되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="1ceae-170">MySQL 서버를 로컬로 tooproduction 연결</span><span class="sxs-lookup"><span data-stu-id="1ceae-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="1ceae-171">Hello 터미널 창에서 Azure의 toohello MySQL 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="1ceae-172">에 대 한 이전에 지정 된 값이 hello를 사용 하 여  _&lt;mysql_server_name >_합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="1ceae-173">암호를 입력 하는 경우 사용 _tr0ngPa $$ w0rd!_, hello 데이터베이스를 만들 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="1ceae-174">프로덕션 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-174">Create a production database</span></span>

<span data-ttu-id="1ceae-175">Hello에 `mysql` 요청에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="1ceae-176">사용 권한이 있는 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-176">Create a user with permissions</span></span>

<span data-ttu-id="1ceae-177">라는 데이터베이스 사용자 만들기 _phpappuser_ hello에서 모든 권한을 지정 `sampledb` 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="1ceae-178">입력 하 여 hello 서버 연결을 종료 `quit`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="1ceae-179">응용 프로그램 tooAzure MySQL 연결</span><span class="sxs-lookup"><span data-stu-id="1ceae-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="1ceae-180">이 단계에서는 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 만든 hello PHP 응용 프로그램 toohello MySQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="1ceae-181">Hello 데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-181">Configure hello database connection</span></span>

<span data-ttu-id="1ceae-182">Hello 리포지토리 루트에서 만듭니다는 _. env.production_ 파일과 복사본 hello에 변수를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="1ceae-183">Hello 자리 표시자 대체  _&lt;mysql_server_name >_합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="1ceae-184">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="1ceae-185">MySQL 연결 정보를이 파일 hello Git 저장소에서 이미 제외 되었습니다. toosecure (참조 _.gitignore_ hello 리포지토리 루트에).</span><span class="sxs-lookup"><span data-stu-id="1ceae-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="1ceae-186">이상에서는 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 데이터베이스 응용 프로그램 서비스 tooconnect tooyour에서 환경 변수 tooconfigure 방법 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="1ceae-187">환경 변수를 사용 하면 hello을 필요가 없습니다 *.env* 앱 서비스에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="1ceae-188">SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-188">Configure SSL certificate</span></span>

<span data-ttu-id="1ceae-189">기본적으로 MySQL용 Azure 데이터베이스에는 클라이언트로부터의 SSL 연결이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="1ceae-190">사용 해야 tooconnect tooyour Azure의 MySQL 데이터베이스를 한 _.pem_ SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="1ceae-191">열기 _config/database.php_ hello 추가 _sslmode_ 및 _옵션_ 매개 변수가 너무`connections.mysql`hello 코드 다음에 나온 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="1ceae-192">toolearn 어떻게 toogenerate이 _certificate.pem_, 참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](../mysql/howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="1ceae-193">hello 경로 _/ssl/certificate.pem_ tooan 기존 가리키는 _certificate.pem_ hello Git 리포지토리에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="1ceae-194">이 파일은 이 자습서의 편의를 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="1ceae-195">최상의 방법으로 _.pem_ 인증서를 원본 제어에 커밋하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="1ceae-196">로컬로 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="1ceae-196">Test hello application locally</span></span>

<span data-ttu-id="1ceae-197">데이터베이스 마이그레이션에 Laravel 실행 _. env.production_ MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 MySQL 데이터베이스의 환경 파일 toocreate hello 테이블 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="1ceae-198">에 유의 해야 _. env.production_ Azure의 hello 연결 정보 tooyour MySQL 데이터베이스 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="1ceae-199">_.env.production_에는 아직 유효한 응용 프로그램 키가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="1ceae-200">Hello 터미널에 것에 대 한 새를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="1ceae-201">Hello 샘플 응용 프로그램을 실행 _. env.production_ hello 환경 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="1ceae-202">너무 이동`http://localhost:8000`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="1ceae-203">오류 없이 hello 페이지가 로드 되 면 hello PHP 응용 프로그램이 Azure에서 MySQL 데이터베이스 사용 toohello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="1ceae-204">Hello 페이지에서 몇 가지 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-204">Add a few tasks in hello page.</span></span>

![PHP 성공적으로 연결 tooAzure 데이터베이스 MySQL (미리 보기)에 대 한](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="1ceae-206">PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="1ceae-207">변경 내용을 커밋합니다</span><span class="sxs-lookup"><span data-stu-id="1ceae-207">Commit your changes</span></span>

<span data-ttu-id="1ceae-208">변경 내용을 Git 명령을 toocommit 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="1ceae-209">앱 배포 준비 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="1ceae-210">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-210">Deploy tooAzure</span></span>

<span data-ttu-id="1ceae-211">이 단계에서는 hello PHP MySQL에 연결 된 응용 프로그램 tooAzure 앱 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="1ceae-212">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="1ceae-213">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="1ceae-214">Set hello PHP 버전</span><span class="sxs-lookup"><span data-stu-id="1ceae-214">Set hello PHP version</span></span>

<span data-ttu-id="1ceae-215">응용 프로그램 hello set hello PHP 버전 hello를 사용 하 여 필요한 [az webapp 구성 집합](/cli/azure/webapp/config#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="1ceae-216">hello 다음 명령은 설정 hello PHP 버전 too_7.0_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="1ceae-217">데이터베이스 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-217">Configure database settings</span></span>

<span data-ttu-id="1ceae-218">이전에 지적으로 환경 변수를 사용 하 여 앱 서비스에서 tooyour Azure의 MySQL 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="1ceae-219">앱 서비스 환경 변수를 설정 _앱 설정_ hello를 사용 하 여 [az webapp 구성 appsettings 세트](/cli/azure/webapp/config/appsettings#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="1ceae-220">hello 다음 명령을 hello 응용 프로그램 설정을 구성 `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, 및 `DB_PASSWORD`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="1ceae-221">Hello 자리 표시자를 대체  _&lt;응용 프로그램 이름 >_ 및  _&lt;mysql_server_name >_합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="1ceae-222">Hello PHP를 사용할 수 있습니다 [getenv](http://www.php.net/manual/function.getenv.php) 메서드 tooaccess hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="1ceae-223">사용 하 여 hello Laravel 코드는 [env](https://laravel.com/docs/5.4/helpers#method-env) hello PHP 통해 래퍼 `getenv`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="1ceae-224">에 MySQL 구성 예를 들어 hello _config/database.php_ 코드 다음 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="1ceae-225">Laravel 환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="1ceae-226">Laravel에는 App Service의 응용 프로그램 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="1ceae-227">앱 설정을 사용하여 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-227">You can configure it with app settings.</span></span>

<span data-ttu-id="1ceae-228">사용 하 여 `php artisan` toogenerate too_.env_ 저장 하지 않고 새 응용 프로그램 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="1ceae-229">Hello 응용 프로그램 키에에서 설정 hello 앱 서비스 웹 앱 hello를 사용 하 여 [az webapp 구성 appsettings 세트](/cli/azure/webapp/config/appsettings#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="1ceae-230">Hello 자리 표시자를 대체  _&lt;응용 프로그램 이름 >_ 및  _&lt;outputofphpartisankey: 생성 >_합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="1ceae-231">`APP_DEBUG="true"`지시 Laravel tooreturn 디버깅 정보 hello 웹 앱을 배포할 때 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="1ceae-232">프로덕션 응용 프로그램을 실행할 때 설정 너무`false`, 변수인 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="1ceae-233">Hello 가상 응용 프로그램 경로 설정 합니다</span><span class="sxs-lookup"><span data-stu-id="1ceae-233">Set hello virtual application path</span></span>

<span data-ttu-id="1ceae-234">Hello 웹 앱에 대 한 hello 가상 응용 프로그램 경로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="1ceae-235">이 단계는 필요 하기 때문에 hello [Laravel 응용 프로그램 수명 주기](https://laravel.com/docs/5.4/lifecycle) hello에서 시작 _공용_ hello 응용 프로그램의 루트 디렉터리가 아닌 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="1ceae-236">Hello 루트 디렉터리에서 해당 수명 주기를 시작 하는 다른 PHP 프레임 워크는 hello 가상 응용 프로그램 경로 수동으로 구성 하지 않고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="1ceae-237">Hello를 사용 하 여 hello 가상 응용 프로그램 경로 설정 [az 리소스 업데이트](/cli/azure/resource#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="1ceae-238">Hello 대체  _&lt;응용 프로그램 이름 >_ 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="1ceae-239">기본적으로 Azure 앱 서비스는 hello 루트 가상 응용 프로그램 경로 가리키는 (_/_) hello의 toohello 루트 디렉터리는 응용 프로그램 파일 배포 (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="1ceae-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="1ceae-240">배포 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="1ceae-241">로컬 Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="1ceae-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="1ceae-242">Git에서 tooAzure 푸시</span><span class="sxs-lookup"><span data-stu-id="1ceae-242">Push tooAzure from Git</span></span>

<span data-ttu-id="1ceae-243">Azure 원격 tooyour 로컬 Git 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="1ceae-244">Toohello Azure 원격 toodeploy hello PHP 응용 프로그램을 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ceae-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="1ceae-245">이전 hello 배포 사용자의 hello 만들기의 일부로 제공한 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="1ceae-246">배포하는 동안 Azure App Service는 진행 상황을 Git에 전합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

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
> <span data-ttu-id="1ceae-247">Hello 배포 프로세스를 설치 한다는 것을 알 수 있습니다 [작성기](https://getcomposer.org/) hello 끝에 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="1ceae-248">앱 서비스 기본 배포 하는 동안 이러한 자동화가 실행 되지 않으면, 하므로이 샘플 리포지토리에는 3 개의 추가 파일의 루트 디렉터리 tooenable에서:</span><span class="sxs-lookup"><span data-stu-id="1ceae-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="1ceae-249">`.deployment`-이 파일을 통해 앱 서비스 toorun 알 `bash deploy.sh` hello 사용자 지정 배포 스크립트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="1ceae-250">`deploy.sh`-사용자 지정 배포 스크립트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="1ceae-251">Hello 파일을 검토 하는 경우 실행 되는지 표시 됩니다 `php composer.phar install` 후 `npm install`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="1ceae-252">`composer.phar`-hello 작성기 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="1ceae-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="1ceae-253">이 접근 방식을 tooadd 모든 단계 tooyour Git 기반 배포 tooApp 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="1ceae-254">자세한 내용은 [사용자 지정 배포 스크립트](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ceae-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="1ceae-255">Toohello Azure 웹 앱을 찾아보기</span><span class="sxs-lookup"><span data-stu-id="1ceae-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="1ceae-256">너무 찾아보기`http://<app_name>.azurewebsites.net` 몇 가지 작업 toohello 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="1ceae-258">축하합니다! Azure App Service에서 데이터 기반 PHP 앱을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="1ceae-259">로컬에서 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-259">Update model locally and redeploy</span></span>

<span data-ttu-id="1ceae-260">이 단계에서는 간단 하 게 변경 toohello 잘못 수행 `task` 데이터 모델 및 hello webapp, 한 다음 업데이트 tooAzure hello를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="1ceae-261">Hello 작업 시나리오에 대 한 작업을 완료로 표시할 수 있도록 hello 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="1ceae-262">열 추가</span><span class="sxs-lookup"><span data-stu-id="1ceae-262">Add a column</span></span>

<span data-ttu-id="1ceae-263">Hello 터미널, toohello 루트 hello Git 리포지토리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="1ceae-264">Hello에 대 한 새 데이터베이스 마이그레이션을 생성 `tasks` 테이블:</span><span class="sxs-lookup"><span data-stu-id="1ceae-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="1ceae-265">이 명령은 생성 되는 hello 마이그레이션 파일의 이름을 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="1ceae-266">_database/migrations_에서 이 파일을 찾아서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="1ceae-267">Hello 대체 `up` 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="1ceae-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="1ceae-268">hello 이전 부울 열에에서 추가 hello `tasks` 라는 테이블 `complete`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="1ceae-269">Hello 대체 `down` hello 롤백 작업에 대 한 코드 다음 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="1ceae-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="1ceae-270">Hello 터미널, Laravel 데이터베이스 마이그레이션을 toomake hello 변경 hello 로컬 데이터베이스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="1ceae-271">Hello에 따라 [Laravel ô ä ¢](https://laravel.com/docs/5.4/eloquent#defining-models), hello 모델 `Task` (참조 _app/Task.php_) toohello 매핑합니다 `tasks` 기본적으로 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="1ceae-272">응용 프로그램 논리 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ceae-272">Update application logic</span></span>

<span data-ttu-id="1ceae-273">열기 hello *routes/web.php* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="1ceae-274">hello 응용 프로그램의 경로 및 여기에 비즈니스 논리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="1ceae-275">Hello 파일의 hello 끝 코드 다음 hello로 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="1ceae-276">hello 위의 코드는 간단한 업데이트 toohello 데이터 모델의 hello 값을 토글하 여 `complete`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="1ceae-277">Hello 뷰 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ceae-277">Update hello view</span></span>

<span data-ttu-id="1ceae-278">열기 hello *resources/views/tasks.blade.php* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="1ceae-279">Hello `<tr>` 여는 태그과 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="1ceae-280">코드 변경 내용을 hello 행 색 hello 작업이 완료 되었는지 여부에 따라 앞에 오는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="1ceae-281">Hello 다음 줄에 다음 코드는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="1ceae-282">코드 다음 hello hello 줄을 전체를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="1ceae-283">hello 앞의 코드에서는 앞에서 정의한 hello 경로 참조 하는 hello 전송 단추</span><span class="sxs-lookup"><span data-stu-id="1ceae-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="1ceae-284">Hello 변경 내용을 로컬 테스트</span><span class="sxs-lookup"><span data-stu-id="1ceae-284">Test hello changes locally</span></span>

<span data-ttu-id="1ceae-285">Hello Git 리포지토리의 루트 디렉터리 hello hello 개발 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="1ceae-286">toosee hello 작업을 상태 변경, 탐색 너무`http://localhost:8000` 및 선택 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![추가 된 확인란 tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="1ceae-288">PHP toostop 입력 `Ctrl + C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="1ceae-289">변경 내용을 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="1ceae-289">Publish changes tooAzure</span></span>

<span data-ttu-id="1ceae-290">Hello 터미널, hello Azure 데이터베이스 hello 프로덕션 연결 문자열 toomake hello 변경 Laravel 데이터베이스 마이그레이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="1ceae-291">Git에서 모든 hello 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="1ceae-292">한 번 hello `git push` 를 마치면 toohello Azure 웹 앱과 테스트 hello 새로운 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![모델 및 데이터베이스 변경 내용이 게시 tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="1ceae-294">모든 작업을 추가한 hello 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="1ceae-295">업데이트 toohello 데이터 스키마 기존 데이터는 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="1ceae-296">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="1ceae-296">Stream diagnostic logs</span></span>

<span data-ttu-id="1ceae-297">PHP 응용 프로그램 hello Azure 앱 서비스에서 실행 되는 동안 hello 콘솔 로그 파이프 된 tooyour 터미널 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="1ceae-298">이런 방식으로 가져올 수 있습니다 hello 같은 진단 메시지 toohelp 응용 프로그램 오류를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="1ceae-299">스트리밍을 사용 하 여 hello toostart 로그 [az webapp 비상 로그](/cli/azure/webapp/log#tail) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="1ceae-300">스트리밍 로그 시작 된 후 일부 웹 트래픽을 hello 브라우저 tooget의 hello Azure 웹 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="1ceae-301">이제 콘솔 로그 파이프 된 toohello 터미널을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="1ceae-302">콘솔 로그가 즉시 표시되지 않으면 30초 후에 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="1ceae-303">언제 든 지에서 스트리밍을 toostop 로그 형식 `Ctrl` + `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="1ceae-304">PHP 응용 프로그램 hello 표준 צ ְ ײ [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="1ceae-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="1ceae-305">hello 샘플 응용 프로그램에서이 접근 방식을 사용 하 여 _app/Http/routes.php_합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="1ceae-306">웹 프레임 워크로 [Laravel Monolog 사용 하 여](https://laravel.com/docs/5.4/errors) hello 로깅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="1ceae-307">toosee tooget Monolog toooutput toohello 콘솔 메시지는 방법 참조 [PHP: 어떻게 toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="1ceae-308">Hello Azure 웹 앱 관리</span><span class="sxs-lookup"><span data-stu-id="1ceae-308">Manage hello Azure web app</span></span>

<span data-ttu-id="1ceae-309">Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toomanage hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="1ceae-310">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="1ceae-312">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-312">You see your web app's Overview page.</span></span> <span data-ttu-id="1ceae-313">여기서 중지, 시작, 다시 시작, 찾아보기 및 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="1ceae-314">왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-314">hello left menu provides pages for configuring your app.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="1ceae-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ceae-316">Next steps</span></span>

<span data-ttu-id="1ceae-317">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ceae-318">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ceae-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="1ceae-319">PHP 응용 프로그램 tooMySQL 연결</span><span class="sxs-lookup"><span data-stu-id="1ceae-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="1ceae-320">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1ceae-321">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="1ceae-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="1ceae-322">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="1ceae-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="1ceae-323">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="1ceae-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="1ceae-324">다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap tooa 웹 앱의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ceae-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ceae-325">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1ceae-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
