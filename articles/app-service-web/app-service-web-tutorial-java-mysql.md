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
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Azure에서 Java 및 MySQL 웹앱 빌드

이 자습서에는 toocreate Java 웹 앱에 Azure 하 고 tooa MySQL 데이터베이스를 연결 하는 방법을 보여줍니다. 작업이 완료되면 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)에서 실행되는 [MySQL용 Azure 데이터베이스](https://docs.microsoft.com/azure/mysql/overview)에 [Spring Boot](https://projects.spring.io/spring-boot/) 응용 프로그램 저장 데이터가 생깁니다.

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure에서 MySQL 데이터베이스 만들기
> * 샘플 응용 프로그램 toohello 데이터베이스 연결
> * Hello 앱 tooAzure 배포
> * 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure에서 진단 로그 스트림
> * Hello Azure 포털에서에서 hello 앱 모니터링


## <a name="prerequisites"></a>필수 조건

1. [Git 다운로드 및 설치](https://git-scm.com/)
1. [다운로드 및 설치 hello JDK Java 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [MySQL 다운로드, 설치 및 시작](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="prepare-local-mysql"></a>로컬 MySQL 준비 

이 단계에서는 데이터베이스를 만들면 사용 하기 위해 로컬 MySQL 서버에서 테스트 hello 응용 프로그램에서 로컬 컴퓨터에 합니다.

### <a name="connect-toomysql-server"></a>TooMySQL 서버 연결

터미널 창에서 tooyour 로컬 MySQL 서버를 연결 합니다. 이 자습서에서는이 터미널 윈도우 toorun 모든 hello 명령을 사용할 수 있습니다.

```bash
mysql -u root -p
```

암호에 대 한 메시지가 hello에 대 한 hello 암호 입력 `root` 계정. 참조 루트 계정 암호를 기억 하지 못하는 경우 [MySQL: tooReset 루트 암호를 hello 어떻게](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)합니다.

명령이 성공적으로 실행되면 MySQL 서버가 이미 실행되고 있는 것입니다. 그렇지 않은 경우 로컬 MySQL 서버의 다음 hello에서 시작 되었는지 확인 [MySQL 사후 설치 단계](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)합니다.

### <a name="create-a-database"></a>데이터베이스 만들기 

Hello에 `mysql` 메시지를 표시, 할 일 항목 hello에 대 한 테이블 및 데이터베이스를 만듭니다.

```sql
CREATE DATABASE tododb;
```

`quit`을 입력하여 서버 연결을 종료합니다.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>만들기 및 hello 샘플 응용 프로그램 실행 

이 단계에서는 복제 샘플 스프링 부팅 응용 프로그램, toouse hello 로컬 MySQL 데이터베이스를 구성 하 고 컴퓨터에서 실행 합니다. 

### <a name="clone-hello-sample"></a>복제 hello 예제

Hello 터미널 창에서 작업 하는 디렉터리 및 복제 hello 샘플 리포지토리 tooa를 이동 합니다. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Hello app toouse hello MySQL 데이터베이스를 구성 합니다.

업데이트 hello `spring.datasource.password` 에 이름과 값 *spring-boot-mysql-todo/src/main/resources/application.properties* hello와 같은 루트 암호 tooopen hello MySQL 프롬프트를 사용 합니다.

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>빌드 및 실행 hello 샘플

빌드 및 hello 리 포에 포함 된 hello Maven 래퍼를 사용 하 여 hello 샘플을 실행 합니다.

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

작업에 대 한 hello sample에서 브라우저 toohttp://localhost:8080 toosee를 엽니다. 작업 toohello 목록을 추가한 것 처럼 hello MySQL에 저장 된 프롬프트 tooview hello 데이터 hello MySQL에서에서 다음 SQL 명령을 사용 합니다.

```SQL
use testdb;
select * from todo_item;
```

클릭 하 여 hello 응용 프로그램을 중지 `Ctrl` + `C` hello 터미널에 있습니다. 

## <a name="create-an-azure-mysql-database"></a>Azure MySQL 데이트베이스 만들기

이 단계에서는 만듭니다는 [MySQL에 대 한 Azure 데이터베이스](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) hello를 사용 하 여 인스턴스 [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다. 구성한 hello 샘플 응용 프로그램 toouse이이 데이터베이스 나중에 hello 자습서에서입니다.

터미널 창 toocreate hello 리소스에서 사용 하 여 hello Azure CLI 2.0 toohost Azure 앱 서비스에서 Java 응용 프로그램 필요합니다. Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

만들기는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello로 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정 등의 관련 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 리소스 그룹을 만듭니다 hello 북부 유럽 지역에서:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello 가능한 값에 사용할 수 있습니다 `--location`, hello를 사용 하 여 [위치 나열 az appservice](/cli/azure/appservice#list-locations) 명령입니다.

### <a name="create-a-mysql-server"></a>MySQL 서버 만들기

Hello로 MySQL (미리 보기)에 대 한 Azure 데이터베이스에서 서버 만들기 [az mysql server 만들기](/cli/azure/mysql/server#create) 명령입니다.    
Hello를 표시 하 여 고유의 고유한 MySQL 서버 이름을 대체 `<mysql_server_name>` 자리 표시자입니다. 이 이름은 MySQL 서버의 호스트 이름의 일부인 `<mysql_server_name>.mysql.database.azure.com`이므로 toobe 전역적으로 고유 해야 합니다. 또한 `<admin_user>` 및 `<admin_password>`를 고유한 값으로 바꿉니다.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Hello MySQL 서버를 만든 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.

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

### <a name="configure-server-firewall"></a>서버 방화벽 구성

방화벽 규칙 만들기 MySQL 서버 tooallow 클라이언트에 대 한 연결 hello를 사용 하 여 [az mysql 서버 방화벽 규칙 만들기](/cli/azure/mysql/server/firewall-rule#create) 명령입니다. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> MySQL용 Azure 데이터베이스(미리 보기)는 현재 Azure 서비스에서 자동으로 연결되지 않습니다. Azure의 IP 주소를 동적으로 할당 때 더 나은 tooenable 모든 IP 주소에 대 한 이제 합니다. Hello 서비스 계속의 미리 보기, 데이터베이스를 보호 하기 위한 더 나은 방식 설정 됩니다.

## <a name="configure-hello-azure-mysql-database"></a>Hello Azure의 MySQL 데이터베이스를 구성 합니다.

컴퓨터에서 터미널 창을 hello에서 Azure의 MySQL server toohello를 연결 합니다. 에 대 한 이전에 지정 된 값이 hello를 사용 하 여 `<admin_user>` 및 `<mysql_server_name>`합니다.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>데이터베이스 만들기 

Hello에 `mysql` 메시지를 표시, 할 일 항목 hello에 대 한 테이블 및 데이터베이스를 만듭니다.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>사용 권한이 있는 사용자 만들기

데이터베이스 사용자를 만들고 hello에서 모든 권한을 제공 `tododb` 데이터베이스입니다. Hello 자리 표시자를 대체 `<Javaapp_user>` 및 `<Javaapp_password>` 자신의 고유한 응용 프로그램 이름을 사용 합니다.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

`quit`을 입력하여 서버 연결을 종료합니다.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Hello 샘플 tooAzure 앱 서비스 배포

Hello로 Azure 앱 서비스 계획 만들기 **무료** 가격 책정 계층 hello를 사용 하 여 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) CLI 명령입니다. 앱 서비스 계획 hello hello 사용 하는 물리적 리소스 toohost 앱을 정의합니다. Tooan 앱 서비스 계획을 할당 하는 모든 응용 프로그램에 있도록 toosave 비용 여러 앱을 호스트 하는 경우 이러한 리소스를 공유 합니다. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Hello 계획 준비 되 면 Azure CLI 표시 비슷한 hello toohello 다음 예제 출력:

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

### <a name="create-an-azure-web-app"></a>Azure Web App 만들기

 사용 하 여 hello [az webapp 만들](/cli/azure/appservice/web#create) CLI 명령 toocreate hello에 있는 웹 응용 프로그램 정의 `myAppServicePlan` 앱 서비스 계획 합니다. URL tooaccess 응용 프로그램에 제공 하 고 몇 가지 옵션 toodeploy 코드 tooAzure를 구성 하는 hello 웹 응용 프로그램 정의 합니다. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

대체 hello `<app_name>` 자신의 고유한 응용 프로그램 이름 자리 표시자입니다. 이 고유 이름이 hello 웹 앱에 대 한 기본 도메인 이름 hello의 일부 이므로 hello 이름 필요한 toobe 고유 Azure에서 모든 앱에서. Tooyour 사용자 노출 먼저 사용자 지정 도메인 이름 항목 toohello 웹 응용 프로그램을 매핑할 수 있습니다.

Hello 웹 응용 프로그램 정의 준비 되 면 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다. 

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

### <a name="configure-java"></a>Java 구성 

Hello로 앱 필요한 hello Java 런타임 구성을 설정 [az 앱 서비스 웹 구성 업데이트](/cli/azure/appservice/web/config#update) 명령입니다.

hello 다음 명령을 hello 웹 앱 toorun에서 구성 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0 합니다.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Hello app toouse hello Azure SQL 데이터베이스를 구성 합니다.

Hello 샘플 응용 프로그램을 실행 하기 전에 Azure에서 만든 hello 웹 응용 프로그램 toouse hello Azure의 MySQL 데이터베이스에 응용 프로그램 설정을 설정 합니다. 이러한 속성은 환경 변수로 toohello 노출 된 웹 응용 프로그램 및 hello application.properties hello 패키지에 포함 된 웹 응용 프로그램 내에서 설정 하는 hello 값을 재정의 합니다. 

응용 프로그램 설정을 사용 하 여 [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI에에서:

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

### <a name="get-ftp-deployment-credentials"></a>FTP 배포 자격 증명 가져오기 
FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 BitBucket을 비롯 한 다양 한 방법으로 응용 프로그램 tooAzure appservice 프로그램을 배포할 수 있습니다. 예를 들어 FTP toodeploy hello를 선택 합니다. WAR 파일에 로컬 컴퓨터 tooAzure 앱 서비스에서 이전에 작성 합니다.

ftp 명령 toohello 웹 응용 프로그램 사용에에서 따라 toopass 자격 증명 toodetermine [az 앱 서비스 웹 배포 목록 게시-프로필](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) 명령: 

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

### <a name="upload-hello-app-using-ftp"></a>FTP를 사용 하 여 hello 앱 업로드

프로그램 즐겨 찾는 FTP 도구 toodeploy hello를 사용 합니다. WAR 파일 toohello */site/wwwroot/webapps* 폴더 hello에서 가져온 hello 서버 주소에 `URL` hello 이전 명령에서 필드입니다. Hello 기존 기본 (루트) 응용 프로그램 디렉터리를 제거 하 고 hello ROOT.war hello로 기존 바꿉니다. WAR 파일 hello 자습서의 앞부분에 나오는 hello에서 기본적으로 제공 합니다.

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

### <a name="test-hello-web-app"></a>Hello 웹 응용 프로그램 테스트

너무 찾아보기`http://<app_name>.azurewebsites.net/` 몇 가지 작업 toohello 목록을 추가 합니다. 

![Azure App Service에서 실행 중인 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**축하합니다.** Azure App Service에서 데이터 기반 Java 앱이 실행되고 있습니다.

## <a name="update-hello-app-and-redeploy"></a>Hello 앱 업데이트 및 다시 배포

Hello 응용 프로그램 tooinclude 일 hello 항목에 대해 만들어진 hello 할 일 목록에 추가 된 열을 업데이트 합니다. 기존 데이터베이스 레코드를 변경 하지 않고 hello 데이터 모델 변경 내용으로 사용자에 대 한 업데이트 hello 데이터베이스 스키마를 처리 하는 스프링 부팅 합니다.

1. 로컬 시스템에서 열고 *src/main/java/com/example/fabrikam/TodoItem.java* hello 다음 toohello 클래스를 가져오고 추가:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. 추가 `String` 속성 `timeCreated` 너무*src/main/java/com/example/fabrikam/TodoItem.java*, 개체 생성 시 타임 스탬프를 사용 하 여 초기화 합니다. 새 hello에 대 한 getter/setter 추가 `timeCreated` 이 파일을 편집 하는 동안 속성입니다.

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

3. 업데이트 *src/main/java/com/example/fabrikam/TodoDemoController.java* hello에서 선으로 `updateTodo` 메서드 tooset hello 타임 스탬프:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Hello Thymeleaf 서식 파일에 새 필드 hello에 대 한 지원을 추가 합니다. 업데이트 *src/main/resources/templates/index.html* hello 타임 스탬프 및 새 toodisplay hello의 필드 값을 각 테이블의 데이터 행의 타임 스탬프 hello에 대 한 새 테이블 헤더를 사용 합니다.

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

5. Hello 응용 프로그램을 다시 작성 하십시오.

    ```bash
    mvnw clean package 
    ```

6. FTP hello를 업데이트 합니다. Hello 기존 제거, 이전 처럼 WAR *사이트/wwwroot/webapps/ROOT* 디렉터리 및 *ROOT.war*, hello 업데이트를 업로드 합니다. ROOT.war로 WAR 파일입니다. 

Hello 앱을 새로 고칠 때는 **만든 시간** 열에 표시 됩니다. 새 작업을 추가 하면 hello 앱 hello 타임 스탬프를 자동으로 입력 됩니다. 기존 작업 유지 hello 내부 데이터 모델 변경 된 경우에 변경 되지 않은 되며 hello 앱 작동 합니다. 

![새 열로 업데이트된 Java 앱](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>진단 로그 스트림 

Azure 앱 서비스에서 Java 응용 프로그램 실행 되는 동안에 hello 콘솔을 얻을 수 있습니다 로그 tooyour 터미널 직접 파이프 됩니다. 이런 방식으로 가져올 수 있습니다 hello 같은 진단 메시지 toohelp 응용 프로그램 오류를 디버깅 합니다.

스트리밍을 사용 하 여 hello toostart 로그 [az webapp 비상 로그](/cli/azure/appservice/web/log#tail) 명령입니다.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Azure Web App 관리

만든 toohello Azure 포털 toosee hello 웹 앱을 이동 합니다.

toodo이 너무 로그인[https://portal.azure.com](https://portal.azure.com)합니다.

Hello 왼쪽된 메뉴에서 클릭 **앱 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-java-mysql/access-portal.png)

기본적으로 웹 앱 블레이드 표시 hello **개요** 페이지. 이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다. 여기에서 중지, 시작, 다시 시작, 삭제와 같은 관리 작업을 수행할 수 있습니다. hello hello 블레이드의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다.

![Azure Portal의 App Service 블레이드](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Hello 블레이드에서 이러한 탭 hello tooyour 웹 응용 프로그램을 추가할 수는 많은 유용한 기능을 보여 줍니다. hello 목록 다음 몇 가지 hello 가능성을 제공 합니다.
* 사용자 지정 DNS 이름 매핑
* 사용자 지정 SSL 인증서 바인딩
* 지속적 배포 구성
* 수평 및 수직 확장
* 사용자 인증 추가

## <a name="clean-up-resources"></a>리소스 정리

다른 자습서에 대 한 이러한 리소스를 필요 하지 않으면 (참조 [다음 단계](#next)), hello 다음 명령을 실행 하 여 삭제할 수 있습니다. 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>다음 단계

> [!div class="checklist"]
> * Azure에서 MySQL 데이터베이스 만들기
> * 샘플 Java 앱 toohello MySQL 연결
> * Hello 앱 tooAzure 배포
> * 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure에서 진단 로그 스트림
> * Hello Azure 포털에서에서 hello 응용 프로그램 관리

다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap toohello 앱의 이름을 합니다.

> [!div class="nextstepaction"] 
> [지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램](app-service-web-tutorial-custom-domain.md)
