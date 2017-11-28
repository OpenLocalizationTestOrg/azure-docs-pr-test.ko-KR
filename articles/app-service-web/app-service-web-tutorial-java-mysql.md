---
title: "aaaBuild Azure에서 Java 및 MySQL 웹 응용 프로그램"
description: "자세한 내용은 tooget Java 응용 프로그램 하는 연결 하는 방법을 toohello Azure 앱 서비스에서 작업 하는 Azure의 MySQL 데이터베이스 서비스입니다."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="aee37-103">Azure에서 Java 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="aee37-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="aee37-104">이 자습서에는 toocreate Java 웹 앱에 Azure 하 고 tooa MySQL 데이터베이스를 연결 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="aee37-105">작업이 완료되면 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)에서 실행되는 [MySQL용 Azure 데이터베이스](https://docs.microsoft.com/azure/mysql/overview)에 [Spring Boot](https://projects.spring.io/spring-boot/) 응용 프로그램 저장 데이터가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="aee37-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aee37-108">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="aee37-109">샘플 응용 프로그램 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="aee37-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="aee37-110">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="aee37-111">업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="aee37-112">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="aee37-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="aee37-113">Hello Azure 포털에서에서 hello 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="aee37-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="aee37-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aee37-114">Prerequisites</span></span>

1. [<span data-ttu-id="aee37-115">Git 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="aee37-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="aee37-116">다운로드 및 설치 hello JDK Java 7 이상</span><span class="sxs-lookup"><span data-stu-id="aee37-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="aee37-117">MySQL 다운로드, 설치 및 시작</span><span class="sxs-lookup"><span data-stu-id="aee37-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aee37-118">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aee37-119">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="aee37-120">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="aee37-121">로컬 MySQL 준비</span><span class="sxs-lookup"><span data-stu-id="aee37-121">Prepare local MySQL</span></span> 

<span data-ttu-id="aee37-122">이 단계에서는 데이터베이스를 만들면 사용 하기 위해 로컬 MySQL 서버에서 테스트 hello 응용 프로그램에서 로컬 컴퓨터에 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="aee37-123">TooMySQL 서버 연결</span><span class="sxs-lookup"><span data-stu-id="aee37-123">Connect tooMySQL server</span></span>

<span data-ttu-id="aee37-124">터미널 창에서 tooyour 로컬 MySQL 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="aee37-125">이 자습서에서는이 터미널 윈도우 toorun 모든 hello 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="aee37-126">암호에 대 한 메시지가 hello에 대 한 hello 암호 입력 `root` 계정.</span><span class="sxs-lookup"><span data-stu-id="aee37-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="aee37-127">참조 루트 계정 암호를 기억 하지 못하는 경우 [MySQL: tooReset 루트 암호를 hello 어떻게](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="aee37-128">명령이 성공적으로 실행되면 MySQL 서버가 이미 실행되고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="aee37-129">그렇지 않은 경우 로컬 MySQL 서버의 다음 hello에서 시작 되었는지 확인 [MySQL 사후 설치 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="aee37-130">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-130">Create a database</span></span> 

<span data-ttu-id="aee37-131">Hello에 `mysql` 메시지를 표시, 할 일 항목 hello에 대 한 테이블 및 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="aee37-132">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="aee37-133">만들기 및 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="aee37-133">Create and run hello sample app</span></span> 

<span data-ttu-id="aee37-134">이 단계에서는 복제 샘플 스프링 부팅 응용 프로그램, toouse hello 로컬 MySQL 데이터베이스를 구성 하 고 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="aee37-135">복제 hello 예제</span><span class="sxs-lookup"><span data-stu-id="aee37-135">Clone hello sample</span></span>

<span data-ttu-id="aee37-136">Hello 터미널 창에서 작업 하는 디렉터리 및 복제 hello 샘플 리포지토리 tooa를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="aee37-137">Hello app toouse hello MySQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="aee37-138">업데이트 hello `spring.datasource.password` 에 이름과 값 *spring-boot-mysql-todo/src/main/resources/application.properties* hello와 같은 루트 암호 tooopen hello MySQL 프롬프트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="aee37-139">빌드 및 실행 hello 샘플</span><span class="sxs-lookup"><span data-stu-id="aee37-139">Build and run hello sample</span></span>

<span data-ttu-id="aee37-140">빌드 및 hello 리 포에 포함 된 hello Maven 래퍼를 사용 하 여 hello 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="aee37-141">작업에 대 한 hello sample에서 브라우저 toohttp://localhost:8080 toosee를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="aee37-142">작업 toohello 목록을 추가한 것 처럼 hello MySQL에 저장 된 프롬프트 tooview hello 데이터 hello MySQL에서에서 다음 SQL 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="aee37-143">클릭 하 여 hello 응용 프로그램을 중지 `Ctrl` + `C` hello 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="aee37-144">Azure MySQL 데이트베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="aee37-145">이 단계에서는 만듭니다는 [MySQL에 대 한 Azure 데이터베이스](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) hello를 사용 하 여 인스턴스 [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="aee37-146">구성한 hello 샘플 응용 프로그램 toouse이이 데이터베이스 나중에 hello 자습서에서입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="aee37-147">터미널 창 toocreate hello 리소스에서 사용 하 여 hello Azure CLI 2.0 toohost Azure 앱 서비스에서 Java 응용 프로그램 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="aee37-148">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="aee37-149">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-149">Create a resource group</span></span>

<span data-ttu-id="aee37-150">만들기는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello로 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="aee37-151">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정 등의 관련 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="aee37-152">hello 다음 예제에서는 리소스 그룹을 만듭니다 hello 북부 유럽 지역에서:</span><span class="sxs-lookup"><span data-stu-id="aee37-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="aee37-153">toosee hello 가능한 값에 사용할 수 있습니다 `--location`, hello를 사용 하 여 [위치 나열 az appservice](/cli/azure/appservice#list-locations) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="aee37-154">MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-154">Create a MySQL server</span></span>

<span data-ttu-id="aee37-155">Hello로 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 서버 만들기 [az mysql server 만들기](/cli/azure/mysql/server#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="aee37-156">Hello를 표시 하 여 고유의 고유한 MySQL 서버 이름을 대체 `<mysql_server_name>` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="aee37-157">이 이름은 MySQL 서버의 호스트 이름의 일부인 `<mysql_server_name>.mysql.database.azure.com`이므로 toobe 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="aee37-158">또한 `<admin_user>` 및 `<admin_password>`를 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="aee37-159">Hello MySQL 서버를 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="aee37-160">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="aee37-160">Configure server firewall</span></span>

<span data-ttu-id="aee37-161">방화벽 규칙 만들기 MySQL 서버 tooallow 클라이언트에 대 한 연결 hello를 사용 하 여 [az mysql 서버 방화벽 규칙 만들기](/cli/azure/mysql/server/firewall-rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="aee37-162">MySQL용 Azure 데이터베이스(미리 보기)는 현재 Azure 서비스에서 자동으로 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="aee37-163">Azure의 IP 주소를 동적으로 할당 때 더 나은 tooenable 모든 IP 주소에 대 한 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="aee37-164">Hello 서비스 계속의 미리 보기, 데이터베이스를 보호 하기 위한 더 나은 방식 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="aee37-165">Hello Azure의 MySQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="aee37-166">컴퓨터에서 터미널 창을 hello에서 Azure의 MySQL server toohello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="aee37-167">에 대 한 이전에 지정 된 값이 hello를 사용 하 여 `<admin_user>` 및 `<mysql_server_name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="aee37-168">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-168">Create a database</span></span> 

<span data-ttu-id="aee37-169">Hello에 `mysql` 메시지를 표시, 할 일 항목 hello에 대 한 테이블 및 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="aee37-170">사용 권한이 있는 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-170">Create a user with permissions</span></span>

<span data-ttu-id="aee37-171">데이터베이스 사용자를 만들고 hello에서 모든 권한을 제공 `tododb` 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="aee37-172">Hello 자리 표시자를 대체 `<Javaapp_user>` 및 `<Javaapp_password>` 자신의 고유한 응용 프로그램 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="aee37-173">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="aee37-174">Hello 샘플 tooAzure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="aee37-175">Hello로 Azure 앱 서비스 계획 만들기 **무료** 가격 책정 계층 hello를 사용 하 여 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="aee37-176">앱 서비스 계획 hello hello 사용 하는 물리적 리소스 toohost 앱을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="aee37-177">Tooan 앱 서비스 계획을 할당 하는 모든 응용 프로그램에 있도록 toosave 비용 여러 앱을 호스트 하는 경우 이러한 리소스를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="aee37-178">Hello 계획 준비 되 면 Azure CLI 표시 비슷한 hello toohello 다음 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="aee37-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="aee37-179">Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-179">Create an Azure Web app</span></span>

 <span data-ttu-id="aee37-180">사용 하 여 hello [az webapp 만들](/cli/azure/appservice/web#create) CLI 명령 toocreate hello에 있는 웹 응용 프로그램 정의 `myAppServicePlan` 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="aee37-181">URL tooaccess 응용 프로그램에 제공 하 고 몇 가지 옵션 toodeploy 코드 tooAzure를 구성 하는 hello 웹 응용 프로그램 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="aee37-182">대체 hello `<app_name>` 자신의 고유한 응용 프로그램 이름 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="aee37-183">이 고유 이름이 hello 웹 앱에 대 한 기본 도메인 이름 hello의 일부 이므로 hello 이름 필요한 toobe 고유 Azure에서 모든 앱에서.</span><span class="sxs-lookup"><span data-stu-id="aee37-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="aee37-184">Tooyour 사용자 노출 먼저 사용자 지정 도메인 이름 항목 toohello 웹 응용 프로그램을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="aee37-185">Hello 웹 응용 프로그램 정의 준비 되 면 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="aee37-186">Java 구성</span><span class="sxs-lookup"><span data-stu-id="aee37-186">Configure Java</span></span> 

<span data-ttu-id="aee37-187">Hello로 앱 필요한 hello Java 런타임 구성을 설정 [az 앱 서비스 웹 구성 업데이트](/cli/azure/appservice/web/config#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="aee37-188">hello 다음 명령을 hello 웹 앱 toorun에서 구성 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="aee37-189">Hello app toouse hello Azure SQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="aee37-190">Hello 샘플 응용 프로그램을 실행 하기 전에 Azure에서 만든 hello 웹 응용 프로그램 toouse hello Azure의 MySQL 데이터베이스에 응용 프로그램 설정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="aee37-191">이러한 속성은 환경 변수로 toohello 노출 된 웹 응용 프로그램 및 hello application.properties hello 패키지에 포함 된 웹 응용 프로그램 내에서 설정 하는 hello 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="aee37-192">응용 프로그램 설정을 사용 하 여 [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI에에서:</span><span class="sxs-lookup"><span data-stu-id="aee37-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="aee37-193">FTP 배포 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="aee37-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="aee37-194">FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 BitBucket을 비롯 한 다양 한 방법으로 응용 프로그램 tooAzure appservice 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="aee37-195">예를 들어 FTP toodeploy hello를 선택 합니다. WAR 파일에 로컬 컴퓨터 tooAzure 앱 서비스에서 이전에 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="aee37-196">ftp 명령 toohello 웹 응용 프로그램 사용에에서 따라 toopass 자격 증명 toodetermine [az 앱 서비스 웹 배포 목록 게시-프로필](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) 명령:</span><span class="sxs-lookup"><span data-stu-id="aee37-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="aee37-197">FTP를 사용 하 여 hello 앱 업로드</span><span class="sxs-lookup"><span data-stu-id="aee37-197">Upload hello app using FTP</span></span>

<span data-ttu-id="aee37-198">프로그램 즐겨 찾는 FTP 도구 toodeploy hello를 사용 합니다. WAR 파일 toohello */site/wwwroot/webapps* 폴더 hello에서 가져온 hello 서버 주소에 `URL` hello 이전 명령에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="aee37-199">Hello 기존 기본 (루트) 응용 프로그램 디렉터리를 제거 하 고 hello ROOT.war hello로 기존 바꿉니다. WAR 파일 hello 자습서의 앞부분에 나오는 hello에서 기본적으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="aee37-200">Hello 웹 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="aee37-200">Test hello web app</span></span>

<span data-ttu-id="aee37-201">너무 찾아보기`http://<app_name>.azurewebsites.net/` 몇 가지 작업 toohello 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="aee37-203">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="aee37-203">**Congratulations!**</span></span> <span data-ttu-id="aee37-204">Azure App Service에서 데이터 기반 Java 앱이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="aee37-205">Hello 앱 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-205">Update hello app and redeploy</span></span>

<span data-ttu-id="aee37-206">Hello 응용 프로그램 tooinclude 일 hello 항목에 대해 만들어진 hello 할 일 목록에 추가 된 열을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="aee37-207">기존 데이터베이스 레코드를 변경 하지 않고 hello 데이터 모델 변경 내용으로 사용자에 대 한 업데이트 hello 데이터베이스 스키마를 처리 하는 스프링 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="aee37-208">로컬 시스템에서 열고 *src/main/java/com/example/fabrikam/TodoItem.java* hello 다음 toohello 클래스를 가져오고 추가:</span><span class="sxs-lookup"><span data-stu-id="aee37-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="aee37-209">추가 `String` 속성 `timeCreated` 너무*src/main/java/com/example/fabrikam/TodoItem.java*, 개체 생성 시 타임 스탬프를 사용 하 여 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="aee37-210">새 hello에 대 한 getter/setter 추가 `timeCreated` 이 파일을 편집 하는 동안 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="aee37-211">업데이트 *src/main/java/com/example/fabrikam/TodoDemoController.java* hello에서 선으로 `updateTodo` 메서드 tooset hello 타임 스탬프:</span><span class="sxs-lookup"><span data-stu-id="aee37-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="aee37-212">Hello Thymeleaf 서식 파일에 새 필드 hello에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="aee37-213">업데이트 *src/main/resources/templates/index.html* hello 타임 스탬프 및 새 toodisplay hello의 필드 값을 각 테이블의 데이터 행의 타임 스탬프 hello에 대 한 새 테이블 헤더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="aee37-214">Hello 응용 프로그램을 다시 작성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aee37-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="aee37-215">FTP hello를 업데이트 합니다. Hello 기존 제거, 이전 처럼 WAR *사이트/wwwroot/webapps/ROOT* 디렉터리 및 *ROOT.war*, hello 업데이트를 업로드 합니다. ROOT.war로 WAR 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="aee37-216">Hello 앱을 새로 고칠 때는 **만든 시간** 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="aee37-217">새 작업을 추가 하면 hello 앱 hello 타임 스탬프를 자동으로 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="aee37-218">기존 작업 유지 hello 내부 데이터 모델 변경 된 경우에 변경 되지 않은 되며 hello 앱 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![새 열로 업데이트된 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="aee37-220">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="aee37-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="aee37-221">Azure 앱 서비스에서 Java 응용 프로그램 실행 되는 동안에 hello 콘솔을 얻을 수 있습니다 로그 tooyour 터미널 직접 파이프 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="aee37-222">이런 방식으로 가져올 수 있습니다 hello 같은 진단 메시지 toohelp 응용 프로그램 오류를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="aee37-223">스트리밍을 사용 하 여 hello toostart 로그 [az webapp 비상 로그](/cli/azure/appservice/web/log#tail) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="aee37-224">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="aee37-224">Manage your Azure web app</span></span>

<span data-ttu-id="aee37-225">만든 toohello Azure 포털 toosee hello 웹 앱을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="aee37-226">toodo이 너무 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="aee37-227">Hello 왼쪽된 메뉴에서 클릭 **앱 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="aee37-229">기본적으로 웹 앱 블레이드 표시 hello **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="aee37-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="aee37-230">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="aee37-231">여기에서 중지, 시작, 다시 시작, 삭제와 같은 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="aee37-232">hello hello 블레이드의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Azure Portal의 App Service 블레이드](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="aee37-234">Hello 블레이드에서 이러한 탭 hello tooyour 웹 응용 프로그램을 추가할 수는 많은 유용한 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="aee37-235">hello 목록 다음 몇 가지 hello 가능성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="aee37-236">사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="aee37-236">Map a custom DNS name</span></span>
* <span data-ttu-id="aee37-237">사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="aee37-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="aee37-238">지속적 배포 구성</span><span class="sxs-lookup"><span data-stu-id="aee37-238">Configure continuous deployment</span></span>
* <span data-ttu-id="aee37-239">수평 및 수직 확장</span><span class="sxs-lookup"><span data-stu-id="aee37-239">Scale up and out</span></span>
* <span data-ttu-id="aee37-240">사용자 인증 추가</span><span class="sxs-lookup"><span data-stu-id="aee37-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="aee37-241">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="aee37-241">Clean up resources</span></span>

<span data-ttu-id="aee37-242">다른 자습서에 대 한 이러한 리소스를 필요 하지 않으면 (참조 [다음 단계](#next)), hello 다음 명령을 실행 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="aee37-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aee37-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aee37-244">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aee37-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="aee37-245">샘플 Java 앱 toohello MySQL 연결</span><span class="sxs-lookup"><span data-stu-id="aee37-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="aee37-246">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="aee37-247">업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="aee37-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="aee37-248">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="aee37-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="aee37-249">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="aee37-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="aee37-250">다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap toohello 앱의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aee37-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="aee37-251">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="aee37-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
