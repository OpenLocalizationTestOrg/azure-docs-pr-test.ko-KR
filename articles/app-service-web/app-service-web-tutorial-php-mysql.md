---
title: "Azure에서 PHP 및 MySQL 웹앱 빌드 | Microsoft Docs"
description: "MySQL 데이터베이스에 연결하여 Azure에서 PHP 앱이 작동하도록 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="e4445-103">Azure에서 PHP 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="e4445-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="e4445-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e4445-105">이 자습서에서는 Azure에서 PHP 웹앱을 만들고 MySQL 데이터베이스에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="e4445-106">완료되면 [Laravel](https://laravel.com/) 앱이 Azure App Service Web Apps에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="e4445-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4445-109">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e4445-110">MySQL에 PHP 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e4445-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="e4445-111">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="e4445-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e4445-112">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e4445-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="e4445-113">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e4445-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e4445-114">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="e4445-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4445-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e4445-115">Prerequisites</span></span>

<span data-ttu-id="e4445-116">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="e4445-117">Git 설치</span><span class="sxs-lookup"><span data-stu-id="e4445-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="e4445-118">PHP 5.6.4 이상 설치</span><span class="sxs-lookup"><span data-stu-id="e4445-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="e4445-119">작성기 설치</span><span class="sxs-lookup"><span data-stu-id="e4445-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="e4445-120">PHP 확장 Laravel에 필요한 OpenSSL, Pdo-mysql, Mbstring, Tokenizer, XML 사용</span><span class="sxs-lookup"><span data-stu-id="e4445-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="e4445-121">MySQL 설치 및 시작</span><span class="sxs-lookup"><span data-stu-id="e4445-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="e4445-122">로컬 MySQL 준비</span><span class="sxs-lookup"><span data-stu-id="e4445-122">Prepare local MySQL</span></span>

<span data-ttu-id="e4445-123">이 단계에서는 이 자습서에서 사용할 데이터베이스를 로컬 MySQL 서버에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="e4445-124">로컬 MySQL 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="e4445-124">Connect to local MySQL server</span></span>

<span data-ttu-id="e4445-125">터미널 창에서 로컬 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="e4445-126">이 터미널 창을 사용하여 이 자습서의 모든 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e4445-127">암호를 묻는 메시지가 표시되면 `root` 계정에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="e4445-128">루트 계정 암호를 기억하지 못하는 경우 [MySQL: 루트 암호를 재설정하는 방법](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4445-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="e4445-129">명령이 성공적으로 실행되면 MySQL 서버가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="e4445-130">그렇지 않은 경우 [MySQL 설치 후 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)에 따라 로컬 MySQL 서버가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="e4445-131">로컬에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-131">Create a database locally</span></span>

<span data-ttu-id="e4445-132">`mysql` 프롬프트에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="e4445-133">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="e4445-134">로컬에서 PHP 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-134">Create a PHP app locally</span></span>
<span data-ttu-id="e4445-135">이 단계에서는 Laravel 샘플 응용 프로그램 가져오고, 해당 데이터베이스를 구성한 후 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="e4445-136">샘플 복제</span><span class="sxs-lookup"><span data-stu-id="e4445-136">Clone the sample</span></span>

<span data-ttu-id="e4445-137">터미널 창에서 `cd`를 사용하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="e4445-138">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="e4445-139">`cd`를 사용하여 복제된 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="e4445-140">필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="e4445-141">MySQL 연결 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-141">Configure MySQL connection</span></span>

<span data-ttu-id="e4445-142">리포지토리 루트에서 *.env*라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="e4445-143">다음 변수를 *.env* 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="e4445-144">_&lt;root_password>_ 자리 표시자를 MySQL 루트 사용자의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

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

<span data-ttu-id="e4445-145">Laravel에서 _.env_ 파일을 사용하는 방법에 대한 자세한 내용은 [Laravel 환경 구성](https://laravel.com/docs/5.4/configuration#environment-configuration)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4445-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="e4445-146">로컬에서 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="e4445-146">Run the sample locally</span></span>

<span data-ttu-id="e4445-147">[Laravel 데이터베이스 마이그레이션](https://laravel.com/docs/5.4/migrations)(영문)을 실행하여 응용 프로그램에 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="e4445-148">마이그레이션에서 만들어진 테이블을 보려면 Git 리포지토리의 _database/migrations_ 디렉터리를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="e4445-149">새 Laravel 응용 프로그램 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="e4445-150">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="e4445-151">브라우저에서 `http://localhost:8000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="e4445-152">해당 페이지에서 몇 가지 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-152">Add a few tasks in the page.</span></span>

![PHP가 MySQL 연결에 성공](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="e4445-154">PHP를 중지하려면 터미널에서 `Ctrl + C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="e4445-155">Azure에서 MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-155">Create MySQL in Azure</span></span>

<span data-ttu-id="e4445-156">이 단계에서는 [MySQL용 Azure 데이터베이스(미리 보기)](/azure/mysql)에서 MySQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="e4445-157">나중에 이 데이터베이스에 연결할 PHP 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="e4445-158">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="e4445-159">MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-159">Create a MySQL server</span></span>

<span data-ttu-id="e4445-160">[az mysql server create](/cli/azure/mysql/server#create) 명령을 사용하여 MySQL용 Azure 데이터베이스의 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="e4445-161">다음 명령에서 _&lt;mysql_server_name>_ 자리 표시자를 고유한 MySQL 서버 이름으로 바꿉니다(유효한 문자: `a-z`, `0-9` 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="e4445-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e4445-162">이 이름은 MySQL 서버의 호스트 이름(`<mysql_server_name>.database.windows.net`)의 일부이며, 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="e4445-163">MySQL 서버를 만들면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="e4445-164">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-164">Configure server firewall</span></span>

<span data-ttu-id="e4445-165">[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) 명령을 사용하여 클라이언트 연결을 허용하도록 MySQL 서버에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="e4445-166">MySQL용 Azure 데이터베이스(미리 보기)에서는 현재 Azure 서비스 연결만 제한하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="e4445-167">Azure의 IP 주소는 동적으로 할당되므로 모든 IP 주소를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="e4445-168">이 서비스는 미리 보기로 있으며,</span><span class="sxs-lookup"><span data-stu-id="e4445-168">The service is in preview.</span></span> <span data-ttu-id="e4445-169">데이터베이스를 보호하기 위해 더 나은 방법을 제공하도록 계획되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="e4445-170">로컬에서 프로덕션 MySQL 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="e4445-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="e4445-171">터미널 창에서 Azure의 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="e4445-172">_&lt;mysql_server_name>_에 대해 이전에 지정한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="e4445-173">암호를 묻는 메시지가 표시되면 데이터베이스를 만들 때 지정한 _$tr0ngPa$w0rd!_를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="e4445-174">프로덕션 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-174">Create a production database</span></span>

<span data-ttu-id="e4445-175">`mysql` 프롬프트에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="e4445-176">사용 권한이 있는 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-176">Create a user with permissions</span></span>

<span data-ttu-id="e4445-177">_phpappuser_라는 데이터베이스 사용자를 만들고 `sampledb` 데이터베이스의 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="e4445-178">`quit`를 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="e4445-179">Azure MySQL에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e4445-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="e4445-180">이 단계에서는 MySQL용 Azure 데이터베이스(미리 보기)에서 만든 MySQL 데이터베이스에 PHP 응용 프로그램을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="e4445-181">데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-181">Configure the database connection</span></span>

<span data-ttu-id="e4445-182">리포지토리 루트에서 _.env.production_ 파일을 만들고 다음 변수를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="e4445-183">_&lt;mysql_server_name>_ 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="e4445-184">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="e4445-185">MySQL 연결 정보를 보호하기 위해 이 파일은 이미 Git 리포지토리에서 제외됩니다(리포지토리 루트의 _.gitignore_ 참조).</span><span class="sxs-lookup"><span data-stu-id="e4445-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="e4445-186">나중에 MySQL용 Azure 데이터베이스(미리 보기)에서 데이터베이스에 연결하도록 App Service에서 환경 변수를 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="e4445-187">환경 변수를 사용하면 App Service에서 *.env* 파일이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="e4445-188">SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-188">Configure SSL certificate</span></span>

<span data-ttu-id="e4445-189">기본적으로 MySQL용 Azure 데이터베이스에는 클라이언트로부터의 SSL 연결이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="e4445-190">Azure에서 MySQL 데이터베이스에 연결하려면 _.pem_ SSL 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="e4445-191">다음 코드와 같이 _config/database.php_를 열고 _sslmode_ 및 _options_ 매개 변수를 `connections.mysql`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="e4445-192">이 _certificate.pem_을 생성하는 방법에 대한 내용은 [MySQL용 Azure 데이터베이스에 안전하게 연결하기 위한 사용자 응용 프로그램의 SSL 연결 구성](../mysql/howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4445-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="e4445-193">_/ssl/certificate.pem_ 경로는 Git 리포지토리의 기존 _certificate.pem_ 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="e4445-194">이 파일은 이 자습서의 편의를 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="e4445-195">최상의 방법으로 _.pem_ 인증서를 원본 제어에 커밋하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="e4445-196">로컬에서 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="e4445-196">Test the application locally</span></span>

<span data-ttu-id="e4445-197">_.env.production_을 환경 파일로 사용해서 Laravel 데이터베이스 마이그레이션을 실행하고 MySQL용 Azure 데이터베이스(미리 보기)에서 MySQL 데이터베이스에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="e4445-198">_.env.production_에는 Azure의 MySQL 데이터베이스에 대한 연결 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="e4445-199">_.env.production_에는 아직 유효한 응용 프로그램 키가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="e4445-200">터미널에서 새 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="e4445-201">_.env.production_을 환경 파일로 사용해서 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="e4445-202">`http://localhost:8000`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="e4445-203">오류 없이 페이지가 로드되면 PHP 응용 프로그램이 Azure의 MySQL 데이터베이스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="e4445-204">해당 페이지에서 몇 가지 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-204">Add a few tasks in the page.</span></span>

![PHP가 MySQL용 Azure 데이터베이스(미리 보기)에 데이터베이스에 성공적으로 연결됨](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="e4445-206">PHP를 중지하려면 터미널에서 `Ctrl + C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="e4445-207">변경 내용을 커밋합니다</span><span class="sxs-lookup"><span data-stu-id="e4445-207">Commit your changes</span></span>

<span data-ttu-id="e4445-208">다음 Git 명령을 실행하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="e4445-209">앱을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="e4445-210">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="e4445-210">Deploy to Azure</span></span>

<span data-ttu-id="e4445-211">이 단계에서는 MySQL에 연결된 PHP 응용 프로그램을 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e4445-212">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="e4445-213">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="e4445-214">PHP 버전 설정</span><span class="sxs-lookup"><span data-stu-id="e4445-214">Set the PHP version</span></span>

<span data-ttu-id="e4445-215">[az webapp config set](/cli/azure/webapp/config#set) 명령을 사용하여 응용 프로그램에 필요한 PHP 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="e4445-216">다음 명령은 PHP 버전을 _7.0_으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="e4445-217">데이터베이스 설정 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-217">Configure database settings</span></span>

<span data-ttu-id="e4445-218">앞서 설명한 것처럼 App Service에서 환경 변수를 사용하여 Azure MySQL 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="e4445-219">App Service에서 [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) 명령을 사용하여 환경 변수를 _앱 설정_으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="e4445-220">다음 명령에서는 `DB_HOST`, `DB_DATABASE`, `DB_USERNAME` 및 `DB_PASSWORD` 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="e4445-221">_&lt;appname>_ 및 _&lt;mysql_server_name>_ 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="e4445-222">PHP [getenv](http://www.php.net/manual/function.getenv.php) 메서드를 사용하여 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="e4445-223">Laravel 코드에서는 `getenv` PHP에 대해 [env()](https://laravel.com/docs/5.4/helpers#method-env) 래퍼를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="e4445-224">예를 들어 _config/database.php_의 MySQL 구성은 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="e4445-225">Laravel 환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="e4445-226">Laravel에는 App Service의 응용 프로그램 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="e4445-227">앱 설정을 사용하여 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-227">You can configure it with app settings.</span></span>

<span data-ttu-id="e4445-228">`php artisan`을 사용하면 _.env_로 저장하지 않고도 새 응용 프로그램 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="e4445-229">[az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) 명령을 사용하여 App Service 웹앱에서 응용 프로그램 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="e4445-230">자리 표시자 _&lt;appname>_ 및 _&lt;outputofphpartisankey:generate>_를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="e4445-231">`APP_DEBUG="true"`는 배포된 웹앱에서 오류가 발생하면 디버깅 정보를 반환하도록 Laravel에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="e4445-232">프로덕션 응용 프로그램을 실행할 때 더 안전한 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="e4445-233">가상 응용 프로그램 경로 설정</span><span class="sxs-lookup"><span data-stu-id="e4445-233">Set the virtual application path</span></span>

<span data-ttu-id="e4445-234">웹앱에 대한 가상 응용 프로그램 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="e4445-235">[Laravel 응용 프로그램 수명 주기](https://laravel.com/docs/5.4/lifecycle)(영문)가 응용 프로그램의 루트 디렉터리 대신 _public_ 디렉터리에서 시작되므로 이 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="e4445-236">해당 수명 주기가 루트 디렉터리에서 시작하는 다른 PHP 프레임워크는 가상 응용 프로그램 경로를 수동으로 구성하지 않아도 작동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="e4445-237">[az resource update](/cli/azure/resource#update) 명령을 사용하여 가상 응용 프로그램 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="e4445-238">_&lt;appname>_ 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-238">Replace the _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="e4445-239">기본적으로 Azure App Service에서는 루트 가상 응용 프로그램 경로(_/_)가 배포된 응용 프로그램 파일의 루트 디렉터리(_sites\wwwroot_)를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="e4445-240">배포 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="e4445-241">로컬 Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="e4445-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="e4445-242">Git에서 Azure에 푸시</span><span class="sxs-lookup"><span data-stu-id="e4445-242">Push to Azure from Git</span></span>

<span data-ttu-id="e4445-243">로컬 Git 리포지토리에 Azure 원격을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="e4445-244">Azure 원격 위치에 푸시하여 PHP 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="e4445-245">배포 사용자를 만드는 작업의 일부로 이전에 제공한 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="e4445-246">배포하는 동안 Azure App Service는 진행 상황을 Git에 전합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
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
> <span data-ttu-id="e4445-247">배포 프로세스를 진행하면 마지막에 [Composer](https://getcomposer.org/) 패키지가 설치되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="e4445-248">App Service는 기본 배포 중에 이러한 자동화를 실행하지 않으므로 이 샘플 리포지토리는 사용 설정에 사용되는 추가 파일 3개가 루트 디렉터리에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="e4445-249">`.deployment` - 이 파일은 App Service에서 `bash deploy.sh`를 사용자 지정 배포 스크립트로 실행하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="e4445-250">`deploy.sh` - 사용자 지정 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="e4445-251">파일을 검토하는 경우 `npm install` 다음에 `php composer.phar install`이 실행되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="e4445-252">`composer.phar` - Composer 패키지 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="e4445-253">이 방식으로 App Service에 대한 Git 기반 배포에 어떤 단계든 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="e4445-254">자세한 내용은 [사용자 지정 배포 스크립트](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4445-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="e4445-255">Azure 웹앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="e4445-255">Browse to the Azure web app</span></span>

<span data-ttu-id="e4445-256">`http://<app_name>.azurewebsites.net`으로 이동한 후 목록에 몇 가지 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![Azure App Service에서 실행 중인 PHP 앱](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="e4445-258">축하합니다! Azure App Service에서 데이터 기반 PHP 앱을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="e4445-259">로컬에서 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e4445-259">Update model locally and redeploy</span></span>

<span data-ttu-id="e4445-260">이 단계에서는 `task` 데이터 모델과 웹앱을 간단히 변경한 다음 업데이트를 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="e4445-261">작업 시나리오의 경우 작업을 완료한 것으로 표시할 수 있도록 응용 프로그램을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="e4445-262">열 추가</span><span class="sxs-lookup"><span data-stu-id="e4445-262">Add a column</span></span>

<span data-ttu-id="e4445-263">터미널에서 Git 리포지토리의 루트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="e4445-264">`tasks` 테이블에 대한 새 데이터베이스 마이그레이션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="e4445-265">이 명령은 생성되는 마이그레이션 파일의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="e4445-266">_database/migrations_에서 이 파일을 찾아서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="e4445-267">`up` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="e4445-268">앞의 코드는 `complete`라는 `tasks` 테이블에 부울 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="e4445-269">`down` 메서드를 롤백 작업에 대한 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="e4445-270">터미널에서 Laravel 데이터베이스 마이그레이션을 실행하여 로컬 데이터베이스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="e4445-271">[Laravel 명명 규칙](https://laravel.com/docs/5.4/eloquent#defining-models)에 따라 `Task`(_app/Task.php_ 참조) 모델은 기본적으로 `tasks` 테이블에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="e4445-272">응용 프로그램 논리 업데이트</span><span class="sxs-lookup"><span data-stu-id="e4445-272">Update application logic</span></span>

<span data-ttu-id="e4445-273">*routes/web.php* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="e4445-274">응용 프로그램에서 해당 경로 및 비즈니스 논리를 여기에 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="e4445-275">파일의 끝에 다음 코드를 포함하는 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-275">At the end of the file, add a route with the following code:</span></span>

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

<span data-ttu-id="e4445-276">앞의 코드는 `complete` 값을 설정/해제하여 데이터 모델을 간단히 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="e4445-277">보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="e4445-277">Update the view</span></span>

<span data-ttu-id="e4445-278">*resources/views/tasks.blade.php* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="e4445-279">`<tr>` 여는 태그를 찾아 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="e4445-280">앞의 코드는 작업이 완료되었는지 여부에 따라 행 색을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="e4445-281">다음 줄에는 다음 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="e4445-282">전체 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-282">Replace the entire line with the following code:</span></span>

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

<span data-ttu-id="e4445-283">앞의 코드는 이전에 정의한 경로를 참조하는 제출 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="e4445-284">로컬에서 변경 내용 테스트</span><span class="sxs-lookup"><span data-stu-id="e4445-284">Test the changes locally</span></span>

<span data-ttu-id="e4445-285">Git 리포지토리의 루트 디렉터리에서 개발 서버를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="e4445-286">작업 상태 변경을 확인하려면 `http://localhost:8000`으로 이동하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![작업에 확인란이 추가됨](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="e4445-288">PHP를 중지하려면 터미널에서 `Ctrl + C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="e4445-289">변경 내용을 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="e4445-289">Publish changes to Azure</span></span>

<span data-ttu-id="e4445-290">터미널에서 프로덕션 연결 문자열로 Laravel 데이터베이스 마이그레이션을 실행하여 Azure 데이터베이스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="e4445-291">Git에서 모든 변경 내용을 커밋한 다음 Azure에 코드 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="e4445-292">`git push`가 완료되면 Azure 웹앱으로 이동하여 새 기능을 테스트해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Azure에 게시된 모델 및 데이터베이스 변경 내용](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="e4445-294">모든 작업을 추가했으면 데이터베이스에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="e4445-295">데이터 스키마를 업데이트하는 경우 기존 데이터는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="e4445-296">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e4445-296">Stream diagnostic logs</span></span>

<span data-ttu-id="e4445-297">PHP 응용 프로그램이 Azure App Service에서 실행되는 동안 콘솔 로그를 터미널에 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="e4445-298">이 방법으로 응용 프로그램 오류를 디버깅하는 데 도움이 되는 진단 메시지를 동일하게 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="e4445-299">로그 스트리밍을 시작하려면 [az webapp log tail](/cli/azure/webapp/log#tail) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="e4445-300">로그 스트리밍이 시작되면 브라우저에서 Azure 웹앱을 새로 고쳐 일부 웹 트래픽을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="e4445-301">이제 터미널에 파이프된 콘솔 로그가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="e4445-302">콘솔 로그가 즉시 표시되지 않으면 30초 후에 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="e4445-303">언제든지 로그 스트리밍을 중지하려면 `Ctrl`+`C`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="e4445-304">PHP 응용 프로그램은 표준 [error_log()](http://php.net/manual/function.error-log.php)를 사용하여 콘솔에 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="e4445-305">샘플 응용 프로그램에서 _app/Http/routes.php_에서 이 접근 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="e4445-306">웹 프레임워크로서 [Laravel은 Monolog](https://laravel.com/docs/5.4/errors) 로깅 공급자로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="e4445-307">Monolog에서 콘솔에 메시지를 출력하게 하는 방법을 보려면 [PHP: monolog를 사용하여 콘솔에 로깅하는 방법(php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4445-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="e4445-308">Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="e4445-308">Manage the Azure web app</span></span>

<span data-ttu-id="e4445-309">만든 웹앱을 관리하려면 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="e4445-310">왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="e4445-312">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-312">You see your web app's Overview page.</span></span> <span data-ttu-id="e4445-313">여기서 중지, 시작, 다시 시작, 찾아보기 및 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="e4445-314">왼쪽 메뉴에서 앱을 구성하기 위한 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-314">The left menu provides pages for configuring your app.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e4445-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4445-316">Next steps</span></span>

<span data-ttu-id="e4445-317">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4445-318">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e4445-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e4445-319">MySQL에 PHP 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e4445-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="e4445-320">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="e4445-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e4445-321">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e4445-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="e4445-322">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e4445-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e4445-323">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="e4445-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="e4445-324">다음 자습서로 이동하여 사용자 지정 DNS 이름을 웹앱에 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4445-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4445-325">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="e4445-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
