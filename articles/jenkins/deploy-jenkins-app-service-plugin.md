---
title: "aaaDeploy tooAzure Jenkins 플러그인과 앱 서비스 | Microsoft Docs"
description: "어떻게 toouse Azure 앱 서비스 Jenkins 플러그 인 toodeploy Java 웹 응용 프로그램 tooAzure Jenkins에 알아봅니다."
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Jenkins 플러그인과 tooAzure 앱 서비스 배포 
Java 웹 응용 프로그램 tooAzure toodeploy Azure CLI에 사용할 수 있습니다 [Jenkins 파이프라인](/azure/jenkins/execute-cli-jenkins-pipeline) 되도록 할 수 있습니다 hello 활용 [Azure 앱 서비스 Jenkins 플러그 인](https://plugins.jenkins.io/azure-app-service)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Jenkins toodeploy tooAzure FTP 통해 응용 프로그램 서비스 구성 
> * Docker 통해 Linux에서 Jenkins toodeploy tooAzure 앱 서비스를 구성 합니다. 

## <a name="create-and-configure-jenkins-instance"></a>Jenkins 인스턴스 만들기 및 구성
Hello로 시작 하는 Jenkins 마스터 아직 없는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), JDK8 및 필요한 플러그 인을 다음 hello 포함:

* [Jenkins Git 클라이언트 플러그 인](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons 플러그 인](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

Hello (예를 들어, C#, PHP, Java 및 node.js 등) 지 원하는 모든 언어 Azure 앱 서비스에서에서 플러그인 toodeploy 앱 서비스 웹 앱을 사용할 수 있습니다. 이 자습서에서 사용 하 여 hello 샘플 Java 응용 프로그램을 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample)합니다. toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.  

Java JDK 및 Maven는 hello Java 프로젝트를 빌드하기 위해 필요 합니다. 연속 통합을 위한 사용 하는 경우 hello Jenkins master 또는 hello VM 에이전트에서 hello 구성 요소를 설치 해야 합니다. 

tooinstall, SSH를 사용 하 여 toohello Jenkins 인스턴스에 로그인을 명령을 수행 하는 hello를 실행 합니다.

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

TooApp linux 서비스를 배포 하기 위한 tooinstall Docker 빌드에 사용 된 hello VM 에이전트 hello Jenkins 마스터에 필요 합니다. Toothis 문서 tooinstall Docker 참조: https://docs.docker.com/engine/installation/linux/ubuntu/ 합니다.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure 서비스 주체 tooJenkins 자격 증명 추가

Azure 서비스 사용자는 필요한 toodeploy tooAzure입니다. 

<ol>
<li>사용 하 여 [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 또는 [Azure 포털](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate Azure 서비스 사용자</li>
<li>Hello Jenkins 대시보드 내에서 클릭 **자격 증명-> 시스템->**합니다. **전역 자격 증명(제한 없음)**을 클릭합니다.</li>
<li>클릭 **추가 자격 증명** tooadd 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점 hello 입력 하 여 Microsoft Azure 서비스 사용자입니다. 이후 단계에서 사용할 ID **mySp**를 제공합니다.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure App Service 플러그 인

Azure 앱 서비스에 대 한 플러그 인 v 1.0 지원 연속 배포 tooAzure 웹 응용 프로그램을 통해:

* Git 및 FTP
* Linux의 웹앱용 Docker

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Jenkins toodeploy hello Jenkins 대시보드를 사용 하 여 FTP 통해 웹 응용 프로그램 구성

toodeploy 프로그램 프로젝트 tooAzure 웹 앱에 빌드 아티팩트 (예를 들어 java에서.war 파일)을 업로드할 수 Git 또는 FTP를 사용 하 여 합니다.

Jenkins에서 hello 작업을 설정 하기 전에 Azure 앱 서비스 계획 및 웹 응용 프로그램에 필요한 실행 중인 hello Java 응용 프로그램.


1. Hello로 Azure 앱 서비스 계획 만들기 **무료** 가격 책정 계층 hello를 사용 하 여 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) CLI 명령입니다. 앱 서비스 계획 hello hello 사용 하는 물리적 리소스 toohost 앱을 정의합니다. Tooan 앱 서비스 계획을 할당 하는 모든 응용 프로그램에 있도록 toosave 비용 여러 앱을 호스트 하는 경우 이러한 리소스를 공유 합니다.
2. 웹앱을 만듭니다. 중 하나 사용 하 여 hello 수 [Azure 포털](/azure/app-service-web/web-sites-configure) 다음 Az CLI 명령을 사용 하 여 hello 또는:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. 앱에서 필요한 hello Java 런타임 구성을 설정할 수 있는지 확인 합니다. 다음 Azure CLI 명령을 hello 최근 JDK Java 8에서 웹 앱 toorun hello 구성 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0 합니다.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Hello Jenkins 작업 설정


1. Jenkins 대시보드에 새 **프리스타일** 프로젝트를 만듭니다.
2. 구성 **소스 코드 관리** toouse의 로컬 포크 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) hello를 제공 하 여 **리포지토리 URL**합니다. 예: http://github.com/&lt;yourID>/javawebappsample.
3. Maven을 사용 하 여 빌드 단계 toobuild hello 프로젝트를 추가 합니다. 이를 위해 **셸 실행**을 추가합니다. 이 예는 추가 단계 toorename hello *.war 파일 대상 폴더 tooROOT.war에 필요합니다.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. **Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.
5. 공급 장치, "mySp", 이전 단계에서 저장 된 hello Azure 서비스 사용자입니다.
6. **앱 구성** 섹션에서 구독에 hello 리소스 그룹 및 웹 응용 프로그램을 선택 합니다. hello 플러그 인 Windows hello 웹 응용 프로그램 인지 자동으로 검색 또는 Linux 기반 합니다. Windows 기반 웹 앱에 대 한 "게시할 파일" hello 옵션 표시 됩니다.
7. 채우기 hello 파일에서 원하는 toodeploy (예를 들어 war 패키지 Java를 사용 하 여.) 소스 디렉터리와 대상 디렉터리는 선택 사항입니다. hello 매개 변수를 사용 하면 toospecify 소스 및 대상 폴더 파일을 업로드 하는 경우. Azure의 Java 웹앱은 Tomcat 서버에서 실행됩니다. 따라서 webapps 폴더에 war 패키지를 업로드합니다. 이 예제에서는 설정 **소스 디렉터리** 너무 "대상" 및 "webapps" 제공할 **대상 디렉터리**합니다.
8. 프로덕션 이외의 toodeploy tooa 슬롯을 하려는 경우 설정할 수도 있습니다 **슬롯** 이름입니다.
9. Hello 프로젝트를 저장 하 고 빌드하십시오. 웹 앱 배포 tooAzure 때 작성이 완료 합니다.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Jenkins 파이프라인을 사용하여 FTP를 통해 웹앱 배포

hello 플러그 인은 파이프라인 준비 합니다. Hello GitHub 리포지토리에 있는 tooa 예제를 참조할 수 있습니다.

1. GitHub 웹 UI에서 **Jenkinsfile_ftp_plugin** 파일을 엽니다. Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 11 및 12 줄에 웹 응용 프로그램의 이름을 각각 클릭 합니다.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Jenkins 인스턴스의 줄 14 tooupdate 자격 증명 ID를 변경 합니다.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Jenkins 파이프라인 만들기

1. 웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.
2. Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다. **확인**을 클릭합니다.
3. Hello 클릭 **파이프라인** 다음 탭 합니다.
4. **정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.
5. **SCM**에서 **Git**을 선택합니다. 분기 리 포에 대 한 hello GitHub URL 입력: https:&lt;분기 리 포 >.git
6. 업데이트 **스크립트 경로** 너무 "Jenkinsfile_ftp_plugin"
7. 클릭 **저장** 및 실행된 hello 작업 합니다.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Docker 통해 Linux에서 Jenkins toodeploy 웹 응용 프로그램 구성

Git/FTP 외에 Linux의 웹앱은 Docker를 사용한 배포를 지원합니다. Docker를 사용 하 여 toodeploy tooprovide docker 이미지를 서비스 런타임 사용 하 여 웹 앱을 패키지 하는 Dockerfile을 사용 해야 합니다. 그런 다음 hello 플러그 인 hello 이미지 tooa docker 레지스트리 밀어 넣고 hello 이미지 tooyour 웹 앱을 배포 합니다.

Linux의 웹앱은 Git 및 FTP와 같은 일반적인 방법도 지원하지만 기본 제공되는 언어에 한합니다(.NET Core, Node.js, PHP 및 Ruby). 다른 언어에 대 한 필요한 toopackage 응용 프로그램 코드와 서비스 런타임을 함께 docker 이미지에 및 docker toodeploy 사용 합니다.

Jenkins에서 hello 작업을 설정 하기 전에 Linux에서 Azure 응용 프로그램 서비스를 해야 합니다. 컨테이너 레지스트리 필요한 toostore 이기도 하 고 사용자 개인 Docker 컨테이너 이미지를 관리 합니다. DockerHub를 사용할 수 있습니다. 이 예제에서는 Azure Container Registry를 사용합니다.

* Hello 단계를 따르면 [여기](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux에서 웹 응용 프로그램 
* Azure 컨테이너 레지스트리는 관리 되는 [Docker 레지스트리] (https://docs.docker.com/registry/) 서비스에 따라 hello Docker 레지스트리 2.0 오픈 소스입니다. [여기] hello 단계에 따라 (/ azure/container-registry/container-registry-get-started-azure-cli)는 방법에 대 한 자세한 지침에 대 한 toodo 하도록 합니다. DockerHub를 사용할 수도 있습니다.

### <a name="toodeploy-using-docker"></a>docker를 사용 하 여 toodeploy:

1. Jenkins 대시보드에 새 프리스타일 프로젝트를 만듭니다.
2. 구성 **소스 코드 관리** toouse의 로컬 포크 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) hello를 제공 하 여 **리포지토리 URL**합니다. 예: http://github.com/&lt;yourid>/javawebappsample.
Maven을 사용 하 여 빌드 단계 toobuild hello 프로젝트를 추가 합니다. 추가 하 여 이렇게는 **셸 실행** hello 다음에 줄을 추가 하 고 **명령**:    
```bash
mvn clean package
```

3. **Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.
4. 를 제공 **mySp**, Azure 자격 증명으로 이전 단계에서 저장 된 hello Azure 서비스 사용자입니다.
5. **앱 구성** 섹션에서 구독에 hello 리소스 그룹 및 Linux 웹 응용 프로그램을 선택 합니다.
6. Docker를 통해 게시를 선택합니다.
7. **Dockerfile** 경로를 입력합니다. Hello 기본 상태로 유지할 수 있습니다 "/ Dockerfile"에 대 한 **Docker 레지스트리 URL**https://의 hello 형식에서 지정&lt;myRegistry >. azurecr.io Azure 컨테이너 레지스트리를 사용 하는 경우. DockerHub를 사용하는 경우 비워 둡니다.
8. 에 대 한 **레지스트리 자격 증명**, Azure 컨테이너 레지스트리 hello에 대 한 hello 자격 증명을 추가 합니다. Hello 뒤의 Azure CLI 명령을 실행 하 여 hello 사용자 id와 암호를 가져올 수 있습니다. hello 첫 번째 명령은 hello 관리자 계정을 사용 하도록 설정 합니다.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. docker 이미지 이름 및 태그에 hello **고급** 탭은 선택 사항입니다. 기본적으로 이미지 이름은 가져옵니다 hello 이미지에서 Azure 포털 (에서 Docker 컨테이너 설정입니다.) hello 태그에 구성 된 이름 $BUILD_NUMBER에서 생성 됩니다. 있는지 확인 하거나 Azure 포털에 hello 이미지 이름을 지정 하거나 값을 제공 **Docker 이미지** 에 **고급** 탭 합니다. 이 예제의 경우 **Docker 이미지**에 "&lt;yourRegistry>.azurecr.io/calculator"를 입력하고 **Docker 이미지 태그**는 비워 둡니다.
10. 기본 제공 Docker 이미지 설정을 사용할 경우 배포가 실패합니다. Azure 포털의 Docker 컨테이너에에서 docker 구성 toouse 사용자 지정 이미지를 변경 해야 합니다. 기본 제공 이미지에 대 한 파일 업로드 방법은 toodeploy를 사용 합니다.
11. 유사한 toofile 업로드 방법을 프로덕션 이외의 다른 슬롯을 선택할 수 있습니다.
12. 저장 하 고 hello 프로젝트를 빌드하십시오. 컨테이너 이미지 tooyour 레지스트리 푸시됩니다 및 웹 응용 프로그램이 배포 되었는지 표시 됩니다.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>TooWeb Jenkins 파이프라인을 사용 하 여 Docker 통해 Linux에서 앱 배포

1. GitHub 웹 UI에서 **Jenkinsfile_container_plugin** 파일을 엽니다. Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 11 및 12 줄에 웹 응용 프로그램의 이름을 각각 클릭 합니다.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. 줄 13 tooyour 컨테이너 레지스트리 서버 변경    
```java
def registryServer = '<registryURL>'
```    

3. Jenkins 인스턴스의 줄 16 tooupdate 자격 증명 ID를 변경 합니다.    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Jenkins 파이프라인 만들기    

1. 웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.
2. Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다. **확인**을 클릭합니다.
3. Hello 클릭 **파이프라인** 다음 탭 합니다.
4. **정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.
5. **SCM**에서 **Git**을 선택합니다.
6. 분기 리 포에 대 한 hello GitHub URL 입력: https:&lt;분기 리 포 >.git</li>
업데이트 7, **스크립트 경로** 너무 "Jenkinsfile_container_plugin"
8. 클릭 **저장** 및 실행된 hello 작업 합니다.

## <a name="verify-your-web-app"></a>웹앱 확인

1. tooverify hello WAR 파일을 정상적으로 배포 tooyour 웹 앱입니다. 웹 브라우저를 엽니다.
2. Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 표시:    
     웹 앱 tooJava를 시작! 업데이트되었습니다!
   2017년 6월 17일 일요일 16:39:10 UTC
3. Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y        
    ![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Linux의 앱 서비스

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

이 자습서에서는 Azure 앱 서비스 플러그 인 toodeploy tooAzure hello를 사용합니다.

다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Jenkins toodeploy FTP 통해 Azure 앱 서비스를 구성 합니다. 
> * Docker 통해 Linux에서 Jenkins toodeploy tooAzure 앱 서비스를 구성 합니다. 
