---
title: "Azure의 Docker Python 및 PostgreSQL 웹 앱 aaaBuild | Microsoft Docs"
description: "자세한 방법을 tooget Docker Python 응용 프로그램 데이터베이스 연결 tooa PostgreSQL와 Azure에서 작동 합니다."
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="9a0b4-103">Azure에서 Docker Python 및 PostgreSQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="9a0b4-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="9a0b4-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9a0b4-105">이 자습서에서는 기본 Docker Python toocreate Azure에서 응용 프로그램 웹 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="9a0b4-106">이 응용 프로그램 tooa PostgreSQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="9a0b4-107">완료되면 [App Service Web Apps](app-service-web-overview.md)의 Docker 컨테이너 내에서 Python Flask 응용 프로그램을 실행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Azure App Service의 Docker Python Flask 앱](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="9a0b4-109">MacOS에서 아래 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="9a0b4-110">Linux 및 Windows 지침은 대부분의 경우에서 hello 동일 하지만 hello 차이점이이 자습서에서 자세히 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="9a0b4-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a0b4-111">Prerequisites</span></span>

<span data-ttu-id="9a0b4-112">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="9a0b4-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="9a0b4-113">Git 설치</span><span class="sxs-lookup"><span data-stu-id="9a0b4-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="9a0b4-114">Python 설치</span><span class="sxs-lookup"><span data-stu-id="9a0b4-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="9a0b4-115">PostgreSQL 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="9a0b4-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="9a0b4-116">Docker Community Edition 설치</span><span class="sxs-lookup"><span data-stu-id="9a0b4-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9a0b4-117">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9a0b4-118">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9a0b4-119">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="9a0b4-120">로컬 PostgreSQL 설치 테스트 및 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="9a0b4-121">Hello 터미널 윈도우를 열고 실행 `psql postgres` tooconnect tooyour 로컬 PostgreSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="9a0b4-122">연결이 성공하면 PostgreSQL 데이터베이스가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="9a0b4-123">그렇지 않은 경우 로컬 PostgresQL 데이터베이스 hello 단계를 수행 하 여 시작 되었는지 확인 [다운로드-PostgreSQL 코어 배포](https://www.postgresql.org/download/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="9a0b4-124">*eventregistration*라는 데이터베이스를 만들고, 암호가 *supersecretpass*인 *manager*라는 별도의 데이터베이스 사용자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="9a0b4-125">형식 *\q* tooexit hello PostgreSQL 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="9a0b4-126">로컬 Python Flask 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-126">Create local Python Flask application</span></span>

<span data-ttu-id="9a0b4-127">이 단계에서는 hello 로컬 Python 플라스 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="9a0b4-128">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="9a0b4-128">Clone hello sample application</span></span>

<span data-ttu-id="9a0b4-129">터미널 창을 열고 hello 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="9a0b4-130">실행된 hello 다음 명령을 tooclone hello 샘플 리포지토리 및 go toohello *0.1 initialapp* 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="9a0b4-131">이 샘플 리포지토리에는 [Flask](http://flask.pocoo.org/) 응용 프로그램이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="9a0b4-132">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9a0b4-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="9a0b4-133">이후 단계에서 hello 프로덕션 데이터베이스와 Docker 컨테이너 toouse를 구축 하 여이 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="9a0b4-134">Hello 필요한 패키지를 설치 하 고 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="9a0b4-135">Hello 앱은 완전히 로드, 메시지의 뒤에, 다음과 유사한 toohello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="9a0b4-136">브라우저에서 toohttp://127.0.0.1:5000을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="9a0b4-137">**Register!**를 클릭하고</span><span class="sxs-lookup"><span data-stu-id="9a0b4-137">Click **Register!**</span></span> <span data-ttu-id="9a0b4-138">테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-138">and create a test user.</span></span>

![로컬로 Python Flask 응용 프로그램 실행](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="9a0b4-140">hello 플라스 샘플 응용 프로그램 hello 데이터베이스에 사용자 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="9a0b4-141">사용자 등록에 성공 하면 앱은 데이터 toohello 로컬 PostgreSQL 데이터베이스를 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="9a0b4-142">언제 든 지, toostop hello 플라스 서버 hello 터미널에 Ctrl + C를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="9a0b4-143">프로덕션 PostgreSQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="9a0b4-144">이 단계에서는 Azure에 PostgreSQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="9a0b4-145">앱 배포 tooAzure 이면이 클라우드 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="9a0b4-146">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="9a0b4-146">Log in tooAzure</span></span>

<span data-ttu-id="9a0b4-147">진행 중인 toouse hello Azure CLI 2.0 toocreate hello 리소스가 필요 toohost Azure 앱 서비스에서 Python 응용 프로그램 이제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="9a0b4-148">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="9a0b4-149">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-149">Create a resource group</span></span>

<span data-ttu-id="9a0b4-150">만들기는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello로 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="9a0b4-151">hello 다음 예제에서는 리소스 그룹을 만듭니다 hello 미국 서 부 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="9a0b4-152">사용 하 여 hello [위치 나열 az appservice](/cli/azure/appservice#list-locations) Azure CLI 명령을 toolist 사용 가능한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="9a0b4-153">PostgreSQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="9a0b4-154">PostgreSQL 서버 hello 만들 [az postgres 서버 만들](/cli/azure/documentdb#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="9a0b4-155">Hello hello에 대 한 고유한 서버 이름을 대체 다음 명령을,  *\<postgresql_name >* 자리 표시자 및 hello에 대 한 사용자 이름을  *\<admin_username >* 자리 표시자 .</span><span class="sxs-lookup"><span data-stu-id="9a0b4-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="9a0b4-156">hello 서버 이름이 PostgreSQL 끝점의 일부로 사용 됩니다 (`https://<postgresql_name>.postgres.database.azure.com`) hello 이름 해야 toobe 고유 Azure의 모든 서버에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="9a0b4-157">hello 초기 데이터베이스 관리자 사용자 계정에 대 한 hello 사용자 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="9a0b4-158">이 사용자의 암호를 입력 정보 요청된 toopick 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="9a0b4-159">PostgreSQL 서버에 대 한 hello Azure 데이터베이스를 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="9a0b4-160">PostgreSQL 서버에 대 한 hello Azure 데이터베이스에 대 한 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="9a0b4-161">Hello Azure CLI 명령을 tooallow access toohello 데이터베이스 모든 IP 주소에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="9a0b4-162">hello Azure CLI 출력 유사한 toohello 다음 예제와 hello 방화벽 규칙 만들기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="9a0b4-163">응용 프로그램 Python 플라스 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="9a0b4-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="9a0b4-164">이 단계에서는 프로그램 Python 플라스 샘플 응용 프로그램 toohello Azure 데이터베이스 PostgreSQL 사용자가 만든 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="9a0b4-165">빈 데이터베이스 만들기 및 새 데이터베이스 응용 프로그램 사용자 설정</span><span class="sxs-lookup"><span data-stu-id="9a0b4-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="9a0b4-166">Access tooa 단일 데이터베이스에만 있는 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="9a0b4-167">이러한 자격 증명 tooavoid 제공 hello 응용 프로그램 전체 액세스 toohello 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="9a0b4-168">(메시지가 나타나면 관리자 암호) toohello 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="9a0b4-169">PostgreSQL CLI hello에서 hello 데이터베이스와 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="9a0b4-170">형식 *\q* tooexit hello PostgreSQL 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="9a0b4-171">Hello Azure PostgreSQL 데이터베이스에 대해 로컬로 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="9a0b4-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="9a0b4-172">이제 toohello를 다시 살펴보자면 *앱* hello의 폴더 Github 리포지토리를 복제, hello 데이터베이스 환경 변수를 업데이트 하 여 hello Python 플라스 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="9a0b4-173">Hello 앱은 완전히 로드, 메시지의 뒤에, 다음과 유사한 toohello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="9a0b4-174">브라우저에서 toohttp://127.0.0.1:5000을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="9a0b4-175">**Register!**를 클릭하고</span><span class="sxs-lookup"><span data-stu-id="9a0b4-175">Click **Register!**</span></span> <span data-ttu-id="9a0b4-176">테스트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-176">and create a test registration.</span></span> <span data-ttu-id="9a0b4-177">이제 Azure에서 데이터 toohello 데이터베이스를 작성 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-177">You are now writing data toohello database in Azure.</span></span>

![로컬로 Python Flask 응용 프로그램 실행](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="9a0b4-179">Docker 컨테이너에서 hello 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="9a0b4-180">Hello Docker 컨테이너 이미지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="9a0b4-181">Docker는 해당 it 만들었습니다 hello 컨테이너 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="9a0b4-182">데이터베이스 환경 변수 tooan 환경 변수 파일 추가 *db.env*합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="9a0b4-183">hello 앱은 Azure에서 toohello PostgreSQL 프로덕션 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="9a0b4-184">Hello Docker 컨테이너 내에서 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="9a0b4-185">hello 다음 명령은 hello 환경 변수 파일을 지정 하 고 hello 기본 플라스 포트 5000 toolocal port 5000을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="9a0b4-186">hello 출력은 유사한 toowhat 했 듯이입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="9a0b4-187">그러나 hello 초기 데이터베이스 마이그레이션 더 이상 필요 없는 toobe 수행 하며 따라서를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="9a0b4-188">hello 데이터베이스에는 이전에 만든 hello 등록 이미 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-188">hello database already contains hello registration you created previously.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="9a0b4-190">Hello Docker 컨테이너 tooa 컨테이너 레지스트리 업로드</span><span class="sxs-lookup"><span data-stu-id="9a0b4-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="9a0b4-191">이 단계에서는 hello Docker 컨테이너 tooa 컨테이너 레지스트리를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="9a0b4-192">Azure Container Registry를 사용하지만 Docker 허브와 같이 인기 있는 다른 레지스트리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="9a0b4-193">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="9a0b4-194">다음 명령 toocreate 컨테이너 레지스트리 hello에서 대체  *\<registry_name >* 원하는 고유한 Azure 컨테이너 레지스트리 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="9a0b4-195">출력</span><span class="sxs-lookup"><span data-stu-id="9a0b4-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="9a0b4-196">밀어넣기 및 Docker 이미지를 끌어오려면의 hello 레지스트리 자격 증명을 검색</span><span class="sxs-lookup"><span data-stu-id="9a0b4-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="9a0b4-197">tooshow 레지스트리 자격 증명 관리자 모드를 먼저 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="9a0b4-198">두 개의 암호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-198">You see two passwords.</span></span> <span data-ttu-id="9a0b4-199">Hello 사용자 이름 및 hello 첫 번째 암호의 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="9a0b4-200">Docker 컨테이너 tooAzure 컨테이너 레지스트리 업로드</span><span class="sxs-lookup"><span data-stu-id="9a0b4-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="9a0b4-201">Hello, 응용 프로그램 tooAzure Docker Python 플라스 배포</span><span class="sxs-lookup"><span data-stu-id="9a0b4-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="9a0b4-202">이 단계에서는 프로그램 Docker 컨테이너 기반 Python 플라스 응용 프로그램 tooAzure 앱 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="9a0b4-203">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-203">Create an App Service plan</span></span>

<span data-ttu-id="9a0b4-204">Hello로 앱 서비스 계획 만들기 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="9a0b4-205">hello 다음 예제에서는 Linux 기반 앱 서비스 계획을 만듭니다 라는 *myAppServicePlan* hello S1 가격 책정 계층을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9a0b4-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="9a0b4-206">Hello 앱 서비스 계획을 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="9a0b4-207">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-207">Create a web app</span></span>

<span data-ttu-id="9a0b4-208">Hello에 웹 앱 만들기 *myAppServicePlan* hello로 앱 서비스 계획 [az webapp 만들](/cli/azure/webapp#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="9a0b4-209">응용 프로그램을 배포 하는 hello 웹 응용 프로그램을 제공 된 호스팅 toodeploy 코드 공간 tooview hello 있습니다에 대 한 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="9a0b4-210">Toocreate hello 웹 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="9a0b4-211">Hello hello 바꿉니다 다음 명령을,  *\<app_name >* 고유한 응용 프로그램 이름 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="9a0b4-212">이 이름은 hello 이름 해야 toobe 고유 Azure 앱 서비스의 모든 앱 간에 hello 웹 앱에 대 한 hello 기본 URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="9a0b4-213">Hello 웹 응용 프로그램을 만들면 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="9a0b4-214">Hello 데이터베이스 환경 변수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-214">Configure hello database environment variables</span></span>

<span data-ttu-id="9a0b4-215">Hello 자습서의 앞부분에서 환경 변수 tooconnect tooyour PostgreSQL 데이터베이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="9a0b4-216">앱 서비스 환경 변수를 설정 _앱 설정_ hello를 사용 하 여 [az webapp 구성 appsettings 세트](/cli/azure/webapp/config#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="9a0b4-217">hello 다음 예제에서는 hello 데이터베이스에 대 한 연결 세부 정보로 지정 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="9a0b4-218">또한 hello 사용 *포트* 포트 80에서 Docker 컨테이너 tooreceive HTTP 트래픽에서 변수 toomap PORT 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="9a0b4-219">Docker 컨테이너 배포 구성</span><span class="sxs-lookup"><span data-stu-id="9a0b4-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="9a0b4-220">AppService는 Docker 컨테이너를 자동으로 다운로드하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="9a0b4-221">Hello Docker 컨테이너를 업데이트 하거나 hello 설정을 변경할 때마다 hello 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="9a0b4-222">다시 시작 하면 모든 설정이 적용 됩니다 hello 최신 컨테이너는 hello 레지스트리에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="9a0b4-223">Toohello Azure 웹 앱을 찾아보기</span><span class="sxs-lookup"><span data-stu-id="9a0b4-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="9a0b4-224">찾아보기 toohello 웹 브라우저를 사용 하 여 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="9a0b4-225">hello 웹 앱 hello 컨테이너에 다운로드 하 고 hello 컨테이너 구성이 변경 된 후 시작 toobe 때문에 더 긴 tooload를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="9a0b4-226">Hello 이전 단계에서 toohello Azure 프로덕션 데이터베이스에 저장 된 이전에 등록 된 게스트 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="9a0b4-228">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a0b4-228">**Congratulations!**</span></span> <span data-ttu-id="9a0b4-229">Azure App Service에서 Docker 컨테이너 기반 Python Flask 앱을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="9a0b4-230">데이터 모델 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="9a0b4-230">Update data model and redeploy</span></span>

<span data-ttu-id="9a0b4-231">이 단계에서는 hello 게스트 모델을 업데이트 하 여 hello 참석자 tooeach 이벤트 등록 수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="9a0b4-232">체크 아웃 hello *0.2 마이그레이션* 다음 git 명령을 hello로 버전:</span><span class="sxs-lookup"><span data-stu-id="9a0b4-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="9a0b4-233">이 릴리스는 이미 필요한 변경 tooviews, 컨트롤러 및 모델 hello 적용.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="9a0b4-234">또한 *alembic*(`flask db migrate`)를 통해 생성된 데이터베이스 마이그레이션도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="9a0b4-235">Hello 다음 git 명령을 통해 수행 된 모든 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="9a0b4-236">변경 내용을 로컬에서 테스트</span><span class="sxs-lookup"><span data-stu-id="9a0b4-236">Test your changes locally</span></span>

<span data-ttu-id="9a0b4-237">다음 명령을 tootest hello 변경 내용을 로컬로 실행 hello 플라스 서버를 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="9a0b4-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="9a0b4-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="9a0b4-239">Toohttp://127.0.0.1:5000 브라우저 tooview hello 변경 내용을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="9a0b4-240">테스트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-240">Create a test registration.</span></span>

![로컬로 실행되는 Docker 컨테이너 기반 Python Flask 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="9a0b4-242">변경 내용을 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="9a0b4-242">Publish changes tooAzure</span></span>

<span data-ttu-id="9a0b4-243">Hello 새 docker 이미지를 빌드하고 toohello 컨테이너 레지스트리 푸시 hello 앱을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="9a0b4-244">Azure 웹 앱 tooyour 이동한 hello 새 기능을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="9a0b4-245">다른 이벤트 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Azure App Service의 Docker Python Flask 앱](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="9a0b4-247">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="9a0b4-247">Manage your Azure web app</span></span>

<span data-ttu-id="9a0b4-248">Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toosee hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="9a0b4-249">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="9a0b4-251">기본적으로 hello 포털은 웹 앱의 표시 **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="9a0b4-252">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="9a0b4-253">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="9a0b4-254">hello hello 페이지의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="9a0b4-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a0b4-256">Next steps</span></span>

<span data-ttu-id="9a0b4-257">다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap tooyour 웹 앱의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0b4-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9a0b4-258">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9a0b4-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
