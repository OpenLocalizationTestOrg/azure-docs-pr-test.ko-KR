---
title: "Azure에서 Java 및 MySQL 웹앱 빌드"
description: "Azure MySQL 데이터베이스 서비스에 연결되는 Java 앱이 Azure App Service에서 작동되도록 하는 방법을 알아봅니다."
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="e507e-103">Azure에서 Java 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="e507e-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="e507e-104">이 자습서에서는 Azure에서 Java 웹앱을 만들고 MySQL 데이터베이스에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="e507e-105">작업이 완료되면 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)에서 실행되는 [MySQL용 Azure 데이터베이스](https://docs.microsoft.com/azure/mysql/overview)에 [Spring Boot](https://projects.spring.io/spring-boot/) 응용 프로그램 저장 데이터가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="e507e-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e507e-108">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e507e-109">데이터베이스에 샘플 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e507e-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="e507e-110">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e507e-111">앱 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="e507e-112">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e507e-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e507e-113">Azure Portal에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="e507e-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e507e-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e507e-114">Prerequisites</span></span>

1. [<span data-ttu-id="e507e-115">Git 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="e507e-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="e507e-116">JDK Java 7 이상 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="e507e-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="e507e-117">MySQL 다운로드, 설치 및 시작</span><span class="sxs-lookup"><span data-stu-id="e507e-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e507e-118">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e507e-119">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="e507e-120">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e507e-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="e507e-121">로컬 MySQL 준비</span><span class="sxs-lookup"><span data-stu-id="e507e-121">Prepare local MySQL</span></span> 

<span data-ttu-id="e507e-122">이 단계에서는 컴퓨터에서 로컬로 앱을 테스트하는 데 사용할 데이터베이스를 로컬 MySQL 서버에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="e507e-123">MySQL 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="e507e-123">Connect to MySQL server</span></span>

<span data-ttu-id="e507e-124">터미널 창에서 로컬 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="e507e-125">이 터미널 창을 사용하여 이 자습서의 모든 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e507e-126">암호를 묻는 메시지가 표시되면 `root` 계정에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="e507e-127">루트 계정 암호를 기억하지 못하는 경우 [MySQL: 루트 암호를 재설정하는 방법](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e507e-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="e507e-128">명령이 성공적으로 실행되면 MySQL 서버가 이미 실행되고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="e507e-129">그렇지 않은 경우 [MySQL 설치 후 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)에 따라 로컬 MySQL 서버가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="e507e-130">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-130">Create a database</span></span> 

<span data-ttu-id="e507e-131">`mysql` 프롬프트에서 할 일 항목에 대한 데이터베이스 및 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="e507e-132">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="e507e-133">샘플 앱 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="e507e-133">Create and run the sample app</span></span> 

<span data-ttu-id="e507e-134">이 단계에서는 샘플 Spring 부팅 앱을 복제하고 로컬 MySQL 데이터베이스를 사용하도록 구성한 다음 컴퓨터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="e507e-135">샘플 복제</span><span class="sxs-lookup"><span data-stu-id="e507e-135">Clone the sample</span></span>

<span data-ttu-id="e507e-136">터미널 창에서 작업 디렉터리로 이동하고 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="e507e-137">MySQL 데이터베이스를 사용하도록 앱 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="e507e-138">MySQL 프롬프트를 여는 데 사용한 것과 동일한 루트 암호로 *spring-boot-mysql-todo/src/main/resources/application.properties*의 `spring.datasource.password` 및 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="e507e-139">샘플 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="e507e-139">Build and run the sample</span></span>

<span data-ttu-id="e507e-140">리포지토리에 포함된 Maven 래퍼를 사용하여 샘플을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="e507e-141">브라우저를 열어 http://localhost:8080 에 접속하여 작업의 샘플에서 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="e507e-142">목록에 작업을 추가하여 MySQL 프롬프트에서 다음 SQL 명령을 사용하여 MySQL에 저장된 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="e507e-143">터미널에서 `Ctrl`+`C`를 입력하여 응용 프로그램을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="e507e-144">Azure MySQL 데이트베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="e507e-145">이 단계에서는 [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)를 사용하여 [MySQL용 Azure 데이터베이스 ](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="e507e-146">이 자습서의 후반부에서 샘플 응용 프로그램을 구성하여 이 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="e507e-147">터미널 창에서 Azure CLI 2.0을 사용하여 Azure App Service에서 Java 응용 프로그램을 호스트하는 데 필요한 리소스를 만들 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="e507e-148">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="e507e-149">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-149">Create a resource group</span></span>

<span data-ttu-id="e507e-150">[az group create](/cli/azure/group#create) 명령을 사용하여 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e507e-151">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정 등의 관련 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="e507e-152">다음 예wp에서는 북유럽 지역의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="e507e-153">`--location`에 사용할 수 있는 가능한 값을 보려면 [az appservice list-locations](/cli/azure/appservice#list-locations) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="e507e-154">MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-154">Create a MySQL server</span></span>

<span data-ttu-id="e507e-155">[az mysql server create](/cli/azure/mysql/server#create) 명령을 사용하여 MySQL용 Azure 데이터베이스의 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="e507e-156">`<mysql_server_name>` 자리 표시자를 고유한 MySQL 서버 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="e507e-157">이 이름은 MySQL 서버의 호스트 이름인 `<mysql_server_name>.mysql.database.azure.com`에 속하므로 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="e507e-158">또한 `<admin_user>` 및 `<admin_password>`를 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="e507e-159">MySQL 서버를 만들면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="e507e-160">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-160">Configure server firewall</span></span>

<span data-ttu-id="e507e-161">[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) 명령을 사용하여 클라이언트 연결을 허용하도록 MySQL 서버에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="e507e-162">MySQL용 Azure 데이터베이스(미리 보기)는 현재 Azure 서비스에서 자동으로 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="e507e-163">Azure의 IP 주소는 동적으로 할당되므로 지금은 모든 IP 주소를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="e507e-164">서비스가 미리 보기를 계속 제공하고 있으며, 데이터베이스를 보호하기 위한 더 나은 방법이 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="e507e-165">Azure MySQL 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="e507e-166">컴퓨터의 터미널 창에서 Azure의 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="e507e-167">`<admin_user>` 및 `<mysql_server_name>`에 대해 이전에 지정한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="e507e-168">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-168">Create a database</span></span> 

<span data-ttu-id="e507e-169">`mysql` 프롬프트에서 할 일 항목에 대한 데이터베이스 및 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="e507e-170">사용 권한이 있는 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-170">Create a user with permissions</span></span>

<span data-ttu-id="e507e-171">데이터베이스 사용자를 만들고 `tododb` 데이터베이스에서 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="e507e-172">자리 표시자 `<Javaapp_user>` 및 `<Javaapp_password>`를 고유한 응용 프로그램 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="e507e-173">`quit`을 입력하여 서버 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="e507e-174">Azure App Service에 샘플 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="e507e-175">[az appservice plan create](/cli/azure/appservice/plan#create) CLI 명령을 사용하여 **무료** 가격 책정 계층과 함께 Azure App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="e507e-176">App Service 계획은 앱을 호스트하는 데 사용되는 실제 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="e507e-177">App Service 계획에 할당된 모든 응용 프로그램은 이들 리소스를 공유하므로 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="e507e-178">계획이 준비되면 Azure CLI는 다음 예와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="e507e-179">Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-179">Create an Azure Web app</span></span>

 <span data-ttu-id="e507e-180">[az webapp create](/cli/azure/appservice/web#create) CLI 명령을 사용하여 `myAppServicePlan` App Service 계획에서 웹앱 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="e507e-181">웹앱 정의는 응용 프로그램에 액세스하는 URL을 제공하고 Azure에 코드를 배포하는 몇 가지 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="e507e-182">`<app_name>` 자리 표시자를 고유한 앱 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="e507e-183">이 고유한 이름은 웹앱에 대한 기본 도메인 이름의 일부이므로 이름은 Azure에 있는 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="e507e-184">사용자에게 노출하기 전에 웹앱에 사용자 지정 도메인 이름 항목을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="e507e-185">웹앱 정의가 준비되면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="e507e-186">Java 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-186">Configure Java</span></span> 

<span data-ttu-id="e507e-187">[az appservice web config update](/cli/azure/appservice/web/config#update) 명령으로 앱에 필요한 Java 런타임 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="e507e-188">다음 명령은 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0에서 실행되도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="e507e-189">Azure SQL Database를 사용하도록 앱 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="e507e-190">샘플 앱을 실행하기 전에 Azure에서 만든 Azure MySQL 데이터베이스를 사용하기 위해 웹앱에서 응용 프로그램 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="e507e-191">이러한 속성은 환경 변수로서 웹 응용 프로그램에 노출되며 패키지된 웹앱 내부의 application.properties에 설정된 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="e507e-192">CLI에서 [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings)를 사용하여 응용 프로그램 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="e507e-193">FTP 배포 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="e507e-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="e507e-194">FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 BitBucket과 같은 다양한 방법으로 응용 프로그램을 Azure App Service에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="e507e-195">이 예에서는 로컬 컴퓨터에 이전에 빌드된 .WAR 파일을 Azure App Service에 배포하는 FTP입니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="e507e-196">ftp 명령에서 웹앱으로 전달할 자격 증명을 결정하려면 [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="e507e-197">FTP를 사용하여 앱 업로드</span><span class="sxs-lookup"><span data-stu-id="e507e-197">Upload the app using FTP</span></span>

<span data-ttu-id="e507e-198">선호하는 FTP 도구를 사용하여 이전 명령의 `URL` 필드에서 가져온 서버 주소에 있는 */site/wwwroot/webapps* 폴더에 .WAR 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="e507e-199">기존 기본(루트) 응용 프로그램 디렉터리를 제거하고 기존 ROOT.war를 자습서의 앞부분에서 빌드한 .WAR 파일로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="e507e-200">웹앱 테스트</span><span class="sxs-lookup"><span data-stu-id="e507e-200">Test the web app</span></span>

<span data-ttu-id="e507e-201">`http://<app_name>.azurewebsites.net/`으로 이동한 후 목록에 몇 가지 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="e507e-203">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="e507e-203">**Congratulations!**</span></span> <span data-ttu-id="e507e-204">Azure App Service에서 데이터 기반 Java 앱이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="e507e-205">앱 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-205">Update the app and redeploy</span></span>

<span data-ttu-id="e507e-206">항목을 만든 날에 대한 할일 목록에 추가 열을 포함하도록 응용 프로그램을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="e507e-207">기존 데이터베이스 레코드를 변경하지 않고 데이터 모델이 변경되면 Spring Boot는 사용자에 대한 데이터베이스 스키마 업데이트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="e507e-208">로컬 시스템에서 *src/main/java/com/example/fabrikam/TodoItem.java*를 열고 다음 가져오기를 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="e507e-209">`String` 속성 `timeCreated`를 *src/main/java/com/example/fabrikam/TodoItem.java*에 추가하여 개체 생성 시 timestamp으로 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="e507e-210">이 파일을 편집하는 동안 새 `timeCreated` 속성에 대해 getter/setter를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="e507e-211">*src/main/java/com/example/fabrikam/TodoDemoController.java*를 `updateTodo` 메서드의 라인으로 업데이트하여 timestamp를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="e507e-212">Thymeleaf 템플릿에서 새 필드에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="e507e-213">*src/main/resources/templates/index.html*를 timestamp에 대한 새 테이블 머리글, 그리고 각 테이블의 데이터 행의 timestamp의 값을 표시하는 새 필드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="e507e-214">응용 프로그램을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="e507e-215">FTP는 이전과 같은 업데이트된 .WAR이며, 기존 *site/wwwroot/webapps/ROOT* 디렉터리와 *ROOT.war*를 제거한 다음, 업데이트된 .WAR 파일을 ROOT.war로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="e507e-216">앱을 새로 고치면 **만든 시간** 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="e507e-217">새 작업을 추가하면 앱은 자동으로 timestamp를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="e507e-218">기본 데이터 모델이 변경되더라도 기존 작업은 변경되지 않고 앱와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![새 열로 업데이트된 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="e507e-220">진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e507e-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="e507e-221">Java 응용 프로그램을 Azure App Service에서 실행하는 동안 콘솔 로그를 바로 터미널에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="e507e-222">이 방법으로 응용 프로그램 오류를 디버깅하는 데 도움이 되는 진단 메시지를 동일하게 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="e507e-223">로그 스트리밍을 시작하려면 [az webapp log tail](/cli/azure/appservice/web/log#tail) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e507e-224">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="e507e-224">Manage your Azure web app</span></span>

<span data-ttu-id="e507e-225">만든 웹앱을 보려면 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="e507e-226">이 작업을 수행하려면 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="e507e-227">왼쪽 메뉴에서 **App Service**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="e507e-229">기본적으로 웹앱의 블레이드는 **개요** 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="e507e-230">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e507e-231">여기에서 중지, 시작, 다시 시작, 삭제와 같은 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="e507e-232">블레이드의 왼쪽에 있는 탭에서는 열 수 있는 다른 구성 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Azure Portal의 App Service 블레이드](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="e507e-234">블레이드의 이러한 탭은 웹앱에 추가할 수 있는 유용한 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="e507e-235">다음은 몇 가지 가능성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="e507e-236">사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="e507e-236">Map a custom DNS name</span></span>
* <span data-ttu-id="e507e-237">사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="e507e-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="e507e-238">지속적 배포 구성</span><span class="sxs-lookup"><span data-stu-id="e507e-238">Configure continuous deployment</span></span>
* <span data-ttu-id="e507e-239">수평 및 수직 확장</span><span class="sxs-lookup"><span data-stu-id="e507e-239">Scale up and out</span></span>
* <span data-ttu-id="e507e-240">사용자 인증 추가</span><span class="sxs-lookup"><span data-stu-id="e507e-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e507e-241">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="e507e-241">Clean up resources</span></span>

<span data-ttu-id="e507e-242">다른 자습서에서 이러한 리소스가 필요하지 않으면([다음 단계](#next) 참조) 다음 명령을 실행하여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e507e-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e507e-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e507e-244">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e507e-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e507e-245">MySQL에 샘플 Java 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e507e-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="e507e-246">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e507e-247">앱 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e507e-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="e507e-248">Azure에서 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="e507e-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e507e-249">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="e507e-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="e507e-250">사용자 지정 DNS 이름을 앱에 매핑하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e507e-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="e507e-251">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="e507e-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)