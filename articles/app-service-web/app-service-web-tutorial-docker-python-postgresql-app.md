---
title: "Azure에서 Docker Python 및 PostgreSQL 웹앱 빌드 | Microsoft Docs"
description: "PostgreSQL 데이터베이스에 연결하여 Azure에서 Docker Python 앱이 작동하도록 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="78332-103">Azure에서 Docker Python 및 PostgreSQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="78332-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="78332-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="78332-105">이 자습서에서는 Azure에서 기본 Docker Python 웹앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78332-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="78332-106">또한 이 앱을 PostgreSQL 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="78332-107">완료되면 [App Service Web Apps](app-service-web-overview.md)의 Docker 컨테이너 내에서 Python Flask 응용 프로그램을 실행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Azure App Service의 Docker Python Flask 앱](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="78332-109">macOS에서 다음 단계를 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="78332-110">Linux와 Windows의 지침은 대부분 동일하지만, 차이점은 이 자습서에서 자세히 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="78332-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78332-111">Prerequisites</span></span>

<span data-ttu-id="78332-112">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="78332-113">Git 설치</span><span class="sxs-lookup"><span data-stu-id="78332-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="78332-114">Python 설치</span><span class="sxs-lookup"><span data-stu-id="78332-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="78332-115">PostgreSQL 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="78332-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="78332-116">Docker Community Edition 설치</span><span class="sxs-lookup"><span data-stu-id="78332-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="78332-117">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="78332-118">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="78332-119">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78332-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="78332-120">로컬 PostgreSQL 설치 테스트 및 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="78332-121">터미널 창을 열고 `psql postgres`를 실행하여 로컬 PostgreSQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="78332-122">연결이 성공하면 PostgreSQL 데이터베이스가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="78332-123">연결이 실패하면 [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/)의 단계를 수행하여 로컬 PostgresQL 데이터베이스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="78332-124">*eventregistration*라는 데이터베이스를 만들고, 암호가 *supersecretpass*인 *manager*라는 별도의 데이터베이스 사용자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="78332-125">*\q*를 입력하여 PostgreSQL 클라이언트를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="78332-126">로컬 Python Flask 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-126">Create local Python Flask application</span></span>

<span data-ttu-id="78332-127">이 단계에서는 로컬 ASP.NET 프로젝트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="78332-128">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="78332-128">Clone the sample application</span></span>

<span data-ttu-id="78332-129">터미널 창을 열고 `CD`를 사용하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="78332-130">다음 명령을 실행하여 샘플 리포지토리를 복제하고 *0.1-initialapp* 릴리스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="78332-131">이 샘플 리포지토리에는 [Flask](http://flask.pocoo.org/) 응용 프로그램이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="78332-132">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78332-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="78332-133">이후 단계에서 프로덕션 데이터베이스와 함께 사용할 Docker 컨테이너를 빌드하여 이 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="78332-134">필요한 패키지를 설치하고 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="78332-135">앱이 완전히 로드되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="78332-136">브라우저에서 http://127.0.0.1:5000 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="78332-137">**Register!**를 클릭하고</span><span class="sxs-lookup"><span data-stu-id="78332-137">Click **Register!**</span></span> <span data-ttu-id="78332-138">테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-138">and create a test user.</span></span>

![로컬로 Python Flask 응용 프로그램 실행](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="78332-140">Flask 샘플 응용 프로그램은 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="78332-141">사용자 등록에 성공하면 앱에서 로컬 PostgreSQL 데이터베이스에 데이터를 쓰고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="78332-142">언제든지 Flask 서버를 중지하려면 터미널에서 Ctrl+C를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="78332-143">프로덕션 PostgreSQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="78332-144">이 단계에서는 Azure에 PostgreSQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="78332-145">Azure에 앱을 배포하면 이 클라우드 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="78332-146">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="78332-146">Log in to Azure</span></span>

<span data-ttu-id="78332-147">이제 Azure CLI 2.0을 사용하여 Azure App Service에서 Python 응용 프로그램을 호스팅하는 데 필요한 리소스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="78332-148">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="78332-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="78332-149">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-149">Create a resource group</span></span>

<span data-ttu-id="78332-150">[az group create](/cli/azure/group#create)를 사용하여 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="78332-151">다음 예제에서는 미국 서부 지역의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="78332-152">[az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI 명령을 사용하여 사용할 수 있는 위치를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="78332-153">PostgreSQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="78332-154">[az postgres server create](/cli/azure/documentdb#create) 명령으로 PostgreSQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="78332-155">다음 명령에서 *\<postgresql_name>* 자리 표시자를 대신하여 고유한 서버 이름으로, *\<admin_username>* 자리 표시자를 대신하여 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="78332-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="78332-156">서버 이름은 PostgreSQL 끝점(`https://<postgresql_name>.postgres.database.azure.com`)의 일부로 사용되므로 이름은 Azure의 모든 서버에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="78332-157">사용자 이름은 초기 데이터베이스 관리 사용자 계정에 대한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="78332-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="78332-158">이 사용자의 암호를 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="78332-159">PostgreSQL용 Azure 데이터베이스 서버를 만들면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="78332-160">PostgreSQL 서버용 Azure 데이터베이스에 대한 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="78332-161">다음 Azure CLI 명령을 실행하여 모든 IP 주소에서 데이터베이스에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="78332-162">Azure CLI는 다음 예제와 비슷한 출력으로 방화벽 규칙 만들기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="78332-163">데이터베이스에 Python Flask 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="78332-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="78332-164">이 단계에서 Python Flask 샘플 응용 프로그램을 만든 PostgreSQL용 Azure 데이터베이스 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="78332-165">빈 데이터베이스 만들기 및 새 데이터베이스 응용 프로그램 사용자 설정</span><span class="sxs-lookup"><span data-stu-id="78332-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="78332-166">단일 데이터베이스에만 액세스할 수 있는 새 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="78332-167">서버에 대한 모든 액세스 권한을 응용 프로그램에 부여하지 않도록 하기 위해 이러한 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="78332-168">데이터베이스에 연결합니다(관리자 암호를 묻는 메시지가 표시됨).</span><span class="sxs-lookup"><span data-stu-id="78332-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="78332-169">PostgreSQL CLI에서 데이터베이스와 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="78332-170">*\q*를 입력하여 PostgreSQL 클라이언트를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="78332-171">Azure PostgreSQL 데이터베이스에 대해 로컬로 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="78332-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="78332-172">이제 복제된 Github 리포지토리의 *app* 폴더로 돌아가서 데이터베이스 환경 변수를 업데이트하여 Python Flask 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="78332-173">앱이 완전히 로드되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="78332-174">브라우저에서 http://127.0.0.1:5000 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="78332-175">**Register!**를 클릭하고</span><span class="sxs-lookup"><span data-stu-id="78332-175">Click **Register!**</span></span> <span data-ttu-id="78332-176">테스트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-176">and create a test registration.</span></span> <span data-ttu-id="78332-177">이제 Azure에서 데이터베이스에 데이터를 쓰고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-177">You are now writing data to the database in Azure.</span></span>

![로컬로 Python Flask 응용 프로그램 실행](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="78332-179">Docker 컨테이너에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78332-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="78332-180">Docker 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="78332-181">Docker는 컨테이너를 성공적으로 만들었다는 확인을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="78332-182">*db.env* 환경 변수 파일에 데이터베이스 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="78332-183">앱에서 Azure의 PostgreSQL 프로덕션 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="78332-184">Docker 컨테이너 내에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="78332-185">다음 명령은 환경 변수 파일을 지정하고 5000 기본 Flask 포트를 5000 로컬 포트에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="78332-186">출력은 이전에 표시된 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="78332-187">그러나 초기 데이터베이스 마이그레이션은 더 이상 수행할 필요가 없으므로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="78332-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="78332-188">데이터베이스에는 이미 이전에 만든 등록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-188">The database already contains the registration you created previously.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="78332-190">Docker 컨테이너를 컨테이너 레지스트리로 업로드</span><span class="sxs-lookup"><span data-stu-id="78332-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="78332-191">이 단계에서는 Docker 컨테이너를 컨테이너 레지스트리로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="78332-192">Azure Container Registry를 사용하지만 Docker 허브와 같이 인기 있는 다른 레지스트리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="78332-193">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="78332-194">컨테이너 레지스트리를 만드는 다음 명령에서 *\<registry_name>*을 선택한 Azure Container Registry의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="78332-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="78332-195">출력</span><span class="sxs-lookup"><span data-stu-id="78332-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="78332-196">Docker 이미지 밀어넣기 및 끌어오기를 위한 레지스트리 자격 증명 검색</span><span class="sxs-lookup"><span data-stu-id="78332-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="78332-197">레지스트리 자격 증명을 표시하려면 먼저 관리자 모드를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="78332-198">두 개의 암호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-198">You see two passwords.</span></span> <span data-ttu-id="78332-199">사용자 이름 및 첫 번째 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="78332-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="78332-200">Docker 컨테이너를 Azure Container Registry로 업로드</span><span class="sxs-lookup"><span data-stu-id="78332-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="78332-201">Azure에 Docker Python Flask 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="78332-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="78332-202">이 단계에서는 Docker 컨테이너 기반 Python Flask 응용 프로그램을 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="78332-203">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-203">Create an App Service plan</span></span>

<span data-ttu-id="78332-204">[az appservice plan create](/cli/azure/appservice/plan#create) 명령으로 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="78332-205">다음 예제에서는 S1 가격 책정 계층을 사용하여 *myAppServicePlan*이라는 Linux 기반 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="78332-206">App Service 계획을 만들면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="78332-207">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="78332-207">Create a web app</span></span>

<span data-ttu-id="78332-208">[az webapp create](/cli/azure/webapp#create) 명령을 사용하여 *myAppServicePlan* App Service 계획에 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="78332-209">웹앱은 코드를 배포할 호스팅 공간을 제공하고, 배포된 응용 프로그램을 확인할 수 있도록 URL도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="78332-210">웹앱을 만드는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-210">Use  to create the web app.</span></span> 

<span data-ttu-id="78332-211">다음 명령에서 *\<app_name>* 자리 표시자를 고유한 앱 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="78332-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="78332-212">이 이름은 웹앱에 대한 URL의 일부이므로 Azure App Service의 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="78332-213">웹앱을 만들었으면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="78332-214">데이터베이스 환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="78332-214">Configure the database environment variables</span></span>

<span data-ttu-id="78332-215">자습서의 앞부분에서 환경 변수를 정의하여 PostgreSQL 데이터베이스에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="78332-216">App Service에서 [az webapp config appsettings set](/cli/azure/webapp/config#set) 명령을 사용하여 환경 변수를 _앱 설정_으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="78332-217">다음 예제에서는 데이터베이스 연결 세부 정보를 앱 설정으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="78332-218">또한 *PORT* 변수를 통해 Docker 컨테이너에서 PORT 5000을 매핑하여 PORT 80에서 HTTP 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="78332-219">Docker 컨테이너 배포 구성</span><span class="sxs-lookup"><span data-stu-id="78332-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="78332-220">AppService는 Docker 컨테이너를 자동으로 다운로드하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="78332-221">Docker 컨테이너를 업데이트하거나 설정을 변경할 때마다 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="78332-222">다시 시작하면 모든 설정이 적용되고 레지스트리에서 최신 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="78332-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="78332-223">Azure 웹앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="78332-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="78332-224">웹 브라우저를 사용하여 배포된 웹앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="78332-225">컨테이너 구성을 변경한 후에 컨테이너를 다운로드하고 시작해야 하기 때문에 웹앱에서 로드하는 데 시간이 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="78332-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="78332-226">이전 단계에서 Azure 프로덕션 데이터베이스에 저장된 이전에 등록한 게스트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="78332-228">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="78332-228">**Congratulations!**</span></span> <span data-ttu-id="78332-229">Azure App Service에서 Docker 컨테이너 기반 Python Flask 앱을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="78332-230">데이터 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="78332-230">Update data model and redeploy</span></span>

<span data-ttu-id="78332-231">이 단계에서는 게스트 모델을 업데이트하여 각 이벤트 등록에 대한 참석자 수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="78332-232">다음 git 명령을 사용하여 *0.2-migration* 릴리스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="78332-233">이 릴리스에는 보기, 컨트롤러 및 모델에 필요한 변경 내용이 이미 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="78332-234">또한 *alembic*(`flask db migrate`)를 통해 생성된 데이터베이스 마이그레이션도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="78332-235">다음 git 명령을 통해 적용된 모든 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="78332-236">변경 내용을 로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="78332-236">Test your changes locally</span></span>

<span data-ttu-id="78332-237">다음 명령을 통해 Flask 서버를 로컬로 실행하여 로컬에서 변경 내용을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="78332-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="78332-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="78332-239">브라우저에서 http://127.0.0.1:5000 으로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="78332-240">테스트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-240">Create a test registration.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="78332-242">변경 내용을 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="78332-242">Publish changes to Azure</span></span>

<span data-ttu-id="78332-243">새 docker 이미지를 빌드하고 컨테이너 레지스트리에 밀어 넣은 후 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="78332-244">Azure Web App으로 이동하여 새 기능을 다시 시험해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="78332-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="78332-245">다른 이벤트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78332-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Azure App Service의 Docker Python Flask 앱](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="78332-247">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="78332-247">Manage your Azure web app</span></span>

<span data-ttu-id="78332-248">[Azure Portal](https://portal.azure.com)로 이동하여 만든 웹앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="78332-249">왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78332-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="78332-251">기본적으로 포털에는 웹앱의 **개요** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78332-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="78332-252">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78332-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="78332-253">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78332-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="78332-254">페이지의 왼쪽에 있는 탭에서는 열 수 있는 여러 구성 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78332-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="78332-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78332-256">Next steps</span></span>

<span data-ttu-id="78332-257">다음 자습서로 이동하여 사용자 지정 DNS 이름을 웹앱에 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78332-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="78332-258">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="78332-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
