---
title: "aaaExecute hello Jenkins와 Azure CLI | Microsoft Docs"
description: "어떻게 toouse Azure CLI toodeploy Java 웹 응용 프로그램 tooAzure Jenkins 파이프라인에 알아봅니다."
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>TooAzure Jenkins 서비스 응용 프로그램을 배포 하 고 Azure CLI hello
Java 웹 응용 프로그램 tooAzure toodeploy Azure CLI에 사용할 수 있습니다 [Jenkins 파이프라인](https://jenkins.io/doc/book/pipeline/)합니다. 이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.

> [!div class="checklist"]
> * Jenkins VM 만들기
> * Jenkins 구성
> * Azure에서 웹앱 만들기
> * GitHub 리포지토리 준비
> * Jenkins 파이프라인 만들기
> * Hello 파이프라인을 실행 하 고 hello 웹 응용 프로그램을 확인

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. toofind hello 버전을 실행 `az --version`합니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Jenkins 인스턴스 만들기 및 구성
Hello로 시작 하는 Jenkins 마스터 아직 없는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), 필요한 hello를 포함 하는 [Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) 기본적으로 플러그 인 합니다. 

hello Azure 자격 증명 플러그 인 Jenkins에 toostore Microsoft Azure 서비스 사용자 자격 증명을 허용합니다. 버전 1.2에서에서 지원이 추가 되었습니다 hello Jenkins 파이프라인 hello Azure 자격 증명을 가져올 수 있도록 합니다. 

버전 1.2 이상이 있는지 확인합니다.
* Hello Jenkins 대시보드 내에서 클릭 **Jenkins 관리 플러그 인 관리자->->** 검색 한 **Azure 자격 증명**합니다. 
* Hello 버전 1.2 보다 이전 이면 hello 플러그 인을 업데이트 합니다.

Java JDK 및 Maven hello Jenkins 마스터에도 필요 합니다. tooinstall, SSH를 사용 하 여 tooJenkins 마스터에 로그인 하 고 hello 다음 명령을 실행:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure 서비스 주체 tooJenkins 자격 증명 추가

Azure 자격 증명은 필요한 tooexecute Azure CLI입니다.

* Hello Jenkins 대시보드 내에서 클릭 **자격 증명-> 시스템->**합니다. **전역 자격 증명(제한 없음)**을 클릭합니다.
* 클릭 **추가 자격 증명** tooadd는 [Microsoft Azure 서비스 사용자](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점 hello 입력 하 여 합니다. 이후 단계에서 사용할 ID를 제공합니다.

![자격 증명 추가](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Hello Java 웹 응용 프로그램을 배포 하기 위한 Azure 앱 서비스 만들기

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

## <a name="prepare-a-github-repository"></a>GitHub 리포지토리 준비
열기 hello [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) 리 포 합니다. toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.

* GitHub 웹 UI에서 **Jenkinsfile** 파일을 엽니다. Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 선 20 및 21 웹 응용 프로그램의 이름을 각각 클릭 합니다.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Jenkins 인스턴스의 줄 23 tooupdate 자격 증명 ID를 변경 합니다.

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Jenkins 파이프라인 만들기
웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다. 

* Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다. **확인**을 클릭합니다.
* Hello 클릭 **파이프라인** 다음 탭 합니다. 
* **정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.
* **SCM**에서 **Git**을 선택합니다.
* 분기 리 포에 대 한 hello GitHub URL 입력: https:\<분기 리 포\>.git
* 페이지 맨 아래에 있는 **저장**

## <a name="test-your-pipeline"></a>파이프라인 테스트
* 만든 toohello 파이프라인 이동 **이제 빌드**
* 빌드는 몇 초 후에 성공적으로 및 toohello 빌드를 이동 하 고 클릭 **콘솔 출력** toosee hello 세부 정보

## <a name="verify-your-web-app"></a>웹앱 확인
tooverify hello WAR 파일을 정상적으로 배포 tooyour 웹 앱입니다. 웹 브라우저를 엽니다.

* Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping  
다음이 표시됩니다.

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y

![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>TooAzure Linux에서 웹 응용 프로그램 배포
Toouse Azure CLI 프로그램 Jenkins에 파이프라인 하는 방법을 파악 했으므로 hello 스크립트 toodeploy tooan Linux에서 Azure 웹 앱을 수정할 수 있습니다.

웹 응용 프로그램에 액세스 Linux Docker toouse은 다른 방식으로 toodo hello 배포를 지원 합니다. toodeploy, tooprovide Docker 이미지를 서비스 런타임 사용 하 여 웹 앱을 패키지 하는 Dockerfile 필요 합니다. hello 플러그 인 다음 hello 이미지, tooa Docker 레지스트리 푸시 빌드하고 hello 이미지 tooyour 웹 앱을 배포 합니다.

* Hello 단계에 따라 [여기](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux에서 실행 하는 Azure 웹 응용 프로그램입니다.
* Docker을 Jenkins 인스턴스에서 hello 지침에 따라 설치 [문서](https://docs.docker.com/engine/installation/linux/ubuntu/)합니다.
* Hello 단계를 사용 하 여 컨테이너 레지스트리 hello Azure 포털에서에서 만들 [여기](/azure/container-registry/container-registry-get-started-azure-cli)합니다.
* 동일한 hello [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) 리포지토리를 분기 하면 편집 hello **Jenkinsfile2** 파일:
    * 18-21 줄, 각각 리소스 그룹, 웹 앱과 ACR의 toohello 이름을 업데이트 합니다. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * 줄 24, 업데이트 \<azsrvprincipal\> tooyour 자격 증명 ID
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Windows에서는이 경우에만 사용 하 여 tooAzure 웹 앱을 배포할 때와 마찬가지로 새 Jenkins 파이프라인을 만들고 **Jenkinsfile2** 대신 합니다.
* 새 작업을 실행합니다.
* tooverify, Azure CLI에서 실행 합니다.

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    결과 다음 hello를 발생할 수 있습니다.
    
    ```
    [
    "calculator"
    ]
    ```
    
    Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 합니다. Hello 메시지가 표시 됩니다. 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y
    
## <a name="next-steps"></a>다음 단계
이 자습서에서는 GitHub 리포지토리에 있는 hello 소스 코드를 확인 하는 Jenkins 파이프라인을 구성 합니다. Maven toobuild war 파일을 실행 하 고 Azure CLI toodeploy tooAzure 앱 서비스를 사용 하 여 키를 누릅니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Jenkins VM 만들기
> * Jenkins 구성
> * Azure에서 웹앱 만들기
> * GitHub 리포지토리 준비
> * Jenkins 파이프라인 만들기
> * Hello 파이프라인을 실행 하 고 hello 웹 응용 프로그램을 확인
