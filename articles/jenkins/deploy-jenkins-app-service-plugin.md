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
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="fd044-103">Jenkins 플러그인과 tooAzure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="fd044-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="fd044-104">Java 웹 응용 프로그램 tooAzure toodeploy Azure CLI에 사용할 수 있습니다 [Jenkins 파이프라인](/azure/jenkins/execute-cli-jenkins-pipeline) 되도록 할 수 있습니다 hello 활용 [Azure 앱 서비스 Jenkins 플러그 인](https://plugins.jenkins.io/azure-app-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="fd044-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd044-106">Jenkins toodeploy tooAzure FTP 통해 응용 프로그램 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="fd044-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="fd044-107">Docker 통해 Linux에서 Jenkins toodeploy tooAzure 앱 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="fd044-108">Jenkins 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="fd044-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="fd044-109">Hello로 시작 하는 Jenkins 마스터 아직 없는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), JDK8 및 필요한 플러그 인을 다음 hello 포함:</span><span class="sxs-lookup"><span data-stu-id="fd044-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="fd044-110">[Jenkins Git 클라이언트 플러그 인](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="fd044-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="fd044-111">[Docker Commons 플러그 인](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="fd044-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="fd044-112">[Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="fd044-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="fd044-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="fd044-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="fd044-114">Hello (예를 들어, C#, PHP, Java 및 node.js 등) 지 원하는 모든 언어 Azure 앱 서비스에서에서 플러그인 toodeploy 앱 서비스 웹 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="fd044-115">이 자습서에서 사용 하 여 hello 샘플 Java 응용 프로그램을 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="fd044-116">toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="fd044-117">Java JDK 및 Maven는 hello Java 프로젝트를 빌드하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="fd044-118">연속 통합을 위한 사용 하는 경우 hello Jenkins master 또는 hello VM 에이전트에서 hello 구성 요소를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="fd044-119">tooinstall, SSH를 사용 하 여 toohello Jenkins 인스턴스에 로그인을 명령을 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="fd044-120">TooApp linux 서비스를 배포 하기 위한 tooinstall Docker 빌드에 사용 된 hello VM 에이전트 hello Jenkins 마스터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="fd044-121">Toothis 문서 tooinstall Docker 참조: https://docs.docker.com/engine/installation/linux/ubuntu/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="fd044-122">Azure 서비스 주체 tooJenkins 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="fd044-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="fd044-123">Azure 서비스 사용자는 필요한 toodeploy tooAzure입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="fd044-124">사용 하 여 [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 또는 [Azure 포털](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate Azure 서비스 사용자</span><span class="sxs-lookup"><span data-stu-id="fd044-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="fd044-125">Hello Jenkins 대시보드 내에서 클릭 **자격 증명-> 시스템->**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="fd044-126">**전역 자격 증명(제한 없음)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="fd044-127">클릭 **추가 자격 증명** tooadd 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점 hello 입력 하 여 Microsoft Azure 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="fd044-128">이후 단계에서 사용할 ID **mySp**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="fd044-129">Azure App Service 플러그 인</span><span class="sxs-lookup"><span data-stu-id="fd044-129">Azure App Service plugin</span></span>

<span data-ttu-id="fd044-130">Azure 앱 서비스에 대 한 플러그 인 v 1.0 지원 연속 배포 tooAzure 웹 응용 프로그램을 통해:</span><span class="sxs-lookup"><span data-stu-id="fd044-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="fd044-131">Git 및 FTP</span><span class="sxs-lookup"><span data-stu-id="fd044-131">Git and FTP</span></span>
* <span data-ttu-id="fd044-132">Linux의 웹앱용 Docker</span><span class="sxs-lookup"><span data-stu-id="fd044-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="fd044-133">Jenkins toodeploy hello Jenkins 대시보드를 사용 하 여 FTP 통해 웹 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="fd044-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="fd044-134">toodeploy 프로그램 프로젝트 tooAzure 웹 앱에 빌드 아티팩트 (예를 들어 java에서.war 파일)을 업로드할 수 Git 또는 FTP를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="fd044-135">Jenkins에서 hello 작업을 설정 하기 전에 Azure 앱 서비스 계획 및 웹 응용 프로그램에 필요한 실행 중인 hello Java 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="fd044-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="fd044-136">Hello로 Azure 앱 서비스 계획 만들기 **무료** 가격 책정 계층 hello를 사용 하 여 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="fd044-137">앱 서비스 계획 hello hello 사용 하는 물리적 리소스 toohost 앱을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="fd044-138">Tooan 앱 서비스 계획을 할당 하는 모든 응용 프로그램에 있도록 toosave 비용 여러 앱을 호스트 하는 경우 이러한 리소스를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="fd044-139">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-139">Create a Web App.</span></span> <span data-ttu-id="fd044-140">중 하나 사용 하 여 hello 수 [Azure 포털](/azure/app-service-web/web-sites-configure) 다음 Az CLI 명령을 사용 하 여 hello 또는:</span><span class="sxs-lookup"><span data-stu-id="fd044-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="fd044-141">앱에서 필요한 hello Java 런타임 구성을 설정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="fd044-142">다음 Azure CLI 명령을 hello 최근 JDK Java 8에서 웹 앱 toorun hello 구성 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="fd044-143">Hello Jenkins 작업 설정</span><span class="sxs-lookup"><span data-stu-id="fd044-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="fd044-144">Jenkins 대시보드에 새 **프리스타일** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="fd044-145">구성 **소스 코드 관리** toouse의 로컬 포크 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) hello를 제공 하 여 **리포지토리 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="fd044-146">예: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="fd044-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="fd044-147">Maven을 사용 하 여 빌드 단계 toobuild hello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="fd044-148">이를 위해 **셸 실행**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="fd044-149">이 예는 추가 단계 toorename hello *.war 파일 대상 폴더 tooROOT.war에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="fd044-150">**Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="fd044-151">공급 장치, "mySp", 이전 단계에서 저장 된 hello Azure 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="fd044-152">**앱 구성** 섹션에서 구독에 hello 리소스 그룹 및 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="fd044-153">hello 플러그 인 Windows hello 웹 응용 프로그램 인지 자동으로 검색 또는 Linux 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="fd044-154">Windows 기반 웹 앱에 대 한 "게시할 파일" hello 옵션 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="fd044-155">채우기 hello 파일에서 원하는 toodeploy (예를 들어 war 패키지 Java를 사용 하 여.) 소스 디렉터리와 대상 디렉터리는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="fd044-156">hello 매개 변수를 사용 하면 toospecify 소스 및 대상 폴더 파일을 업로드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="fd044-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="fd044-157">Azure의 Java 웹앱은 Tomcat 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="fd044-158">따라서 webapps 폴더에 war 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="fd044-159">이 예제에서는 설정 **소스 디렉터리** 너무 "대상" 및 "webapps" 제공할 **대상 디렉터리**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="fd044-160">프로덕션 이외의 toodeploy tooa 슬롯을 하려는 경우 설정할 수도 있습니다 **슬롯** 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="fd044-161">Hello 프로젝트를 저장 하 고 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd044-161">Save hello project and build it.</span></span> <span data-ttu-id="fd044-162">웹 앱 배포 tooAzure 때 작성이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="fd044-163">Jenkins 파이프라인을 사용하여 FTP를 통해 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fd044-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="fd044-164">hello 플러그 인은 파이프라인 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="fd044-165">Hello GitHub 리포지토리에 있는 tooa 예제를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="fd044-166">GitHub 웹 UI에서 **Jenkinsfile_ftp_plugin** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="fd044-167">Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 11 및 12 줄에 웹 응용 프로그램의 이름을 각각 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="fd044-168">Jenkins 인스턴스의 줄 14 tooupdate 자격 증명 ID를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="fd044-169">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="fd044-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="fd044-170">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="fd044-171">Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="fd044-172">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-172">Click **OK**.</span></span>
3. <span data-ttu-id="fd044-173">Hello 클릭 **파이프라인** 다음 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="fd044-174">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="fd044-175">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="fd044-176">분기 리 포에 대 한 hello GitHub URL 입력: https:&lt;분기 리 포 >.git</span><span class="sxs-lookup"><span data-stu-id="fd044-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="fd044-177">업데이트 **스크립트 경로** 너무 "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="fd044-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="fd044-178">클릭 **저장** 및 실행된 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="fd044-179">Docker 통해 Linux에서 Jenkins toodeploy 웹 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="fd044-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="fd044-180">Git/FTP 외에 Linux의 웹앱은 Docker를 사용한 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="fd044-181">Docker를 사용 하 여 toodeploy tooprovide docker 이미지를 서비스 런타임 사용 하 여 웹 앱을 패키지 하는 Dockerfile을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="fd044-182">그런 다음 hello 플러그 인 hello 이미지 tooa docker 레지스트리 밀어 넣고 hello 이미지 tooyour 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="fd044-183">Linux의 웹앱은 Git 및 FTP와 같은 일반적인 방법도 지원하지만 기본 제공되는 언어에 한합니다(.NET Core, Node.js, PHP 및 Ruby).</span><span class="sxs-lookup"><span data-stu-id="fd044-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="fd044-184">다른 언어에 대 한 필요한 toopackage 응용 프로그램 코드와 서비스 런타임을 함께 docker 이미지에 및 docker toodeploy 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="fd044-185">Jenkins에서 hello 작업을 설정 하기 전에 Linux에서 Azure 응용 프로그램 서비스를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="fd044-186">컨테이너 레지스트리 필요한 toostore 이기도 하 고 사용자 개인 Docker 컨테이너 이미지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="fd044-187">DockerHub를 사용할 수 있습니다. 이 예제에서는 Azure Container Registry를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="fd044-188">Hello 단계를 따르면 [여기](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux에서 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="fd044-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="fd044-189">Azure 컨테이너 레지스트리는 관리 되는 [Docker 레지스트리] (https://docs.docker.com/registry/) 서비스에 따라 hello Docker 레지스트리 2.0 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="fd044-190">[여기] hello 단계에 따라 (/ azure/container-registry/container-registry-get-started-azure-cli)는 방법에 대 한 자세한 지침에 대 한 toodo 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="fd044-191">DockerHub를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="fd044-192">docker를 사용 하 여 toodeploy:</span><span class="sxs-lookup"><span data-stu-id="fd044-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="fd044-193">Jenkins 대시보드에 새 프리스타일 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="fd044-194">구성 **소스 코드 관리** toouse의 로컬 포크 [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) hello를 제공 하 여 **리포지토리 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="fd044-195">예: http://github.com/&lt;yourid>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="fd044-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="fd044-196">Maven을 사용 하 여 빌드 단계 toobuild hello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="fd044-197">추가 하 여 이렇게는 **셸 실행** hello 다음에 줄을 추가 하 고 **명령**:</span><span class="sxs-lookup"><span data-stu-id="fd044-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="fd044-198">**Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="fd044-199">를 제공 **mySp**, Azure 자격 증명으로 이전 단계에서 저장 된 hello Azure 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="fd044-200">**앱 구성** 섹션에서 구독에 hello 리소스 그룹 및 Linux 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="fd044-201">Docker를 통해 게시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="fd044-202">**Dockerfile** 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="fd044-203">Hello 기본 상태로 유지할 수 있습니다 "/ Dockerfile"에 대 한 **Docker 레지스트리 URL**https://의 hello 형식에서 지정&lt;myRegistry >. azurecr.io Azure 컨테이너 레지스트리를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="fd044-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="fd044-204">DockerHub를 사용하는 경우 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="fd044-205">에 대 한 **레지스트리 자격 증명**, Azure 컨테이너 레지스트리 hello에 대 한 hello 자격 증명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="fd044-206">Hello 뒤의 Azure CLI 명령을 실행 하 여 hello 사용자 id와 암호를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="fd044-207">hello 첫 번째 명령은 hello 관리자 계정을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="fd044-208">docker 이미지 이름 및 태그에 hello **고급** 탭은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="fd044-209">기본적으로 이미지 이름은 가져옵니다 hello 이미지에서 Azure 포털 (에서 Docker 컨테이너 설정입니다.) hello 태그에 구성 된 이름 $BUILD_NUMBER에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="fd044-210">있는지 확인 하거나 Azure 포털에 hello 이미지 이름을 지정 하거나 값을 제공 **Docker 이미지** 에 **고급** 탭 합니다. 이 예제의 경우 **Docker 이미지**에 "&lt;yourRegistry>.azurecr.io/calculator"를 입력하고 **Docker 이미지 태그**는 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="fd044-211">기본 제공 Docker 이미지 설정을 사용할 경우 배포가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="fd044-212">Azure 포털의 Docker 컨테이너에에서 docker 구성 toouse 사용자 지정 이미지를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="fd044-213">기본 제공 이미지에 대 한 파일 업로드 방법은 toodeploy를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="fd044-214">유사한 toofile 업로드 방법을 프로덕션 이외의 다른 슬롯을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="fd044-215">저장 하 고 hello 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd044-215">Save and build hello project.</span></span> <span data-ttu-id="fd044-216">컨테이너 이미지 tooyour 레지스트리 푸시됩니다 및 웹 응용 프로그램이 배포 되었는지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="fd044-217">TooWeb Jenkins 파이프라인을 사용 하 여 Docker 통해 Linux에서 앱 배포</span><span class="sxs-lookup"><span data-stu-id="fd044-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="fd044-218">GitHub 웹 UI에서 **Jenkinsfile_container_plugin** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="fd044-219">Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 11 및 12 줄에 웹 응용 프로그램의 이름을 각각 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="fd044-220">줄 13 tooyour 컨테이너 레지스트리 서버 변경</span><span class="sxs-lookup"><span data-stu-id="fd044-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="fd044-221">Jenkins 인스턴스의 줄 16 tooupdate 자격 증명 ID를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="fd044-222">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="fd044-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="fd044-223">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="fd044-224">Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="fd044-225">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-225">Click **OK**.</span></span>
3. <span data-ttu-id="fd044-226">Hello 클릭 **파이프라인** 다음 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="fd044-227">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="fd044-228">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="fd044-229">분기 리 포에 대 한 hello GitHub URL 입력: https:&lt;분기 리 포 >.git</span><span class="sxs-lookup"><span data-stu-id="fd044-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="fd044-230">업데이트 7, **스크립트 경로** 너무 "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="fd044-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="fd044-231">클릭 **저장** 및 실행된 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="fd044-232">웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="fd044-232">Verify your web app</span></span>

1. <span data-ttu-id="fd044-233">tooverify hello WAR 파일을 정상적으로 배포 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="fd044-234">웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-234">Open a web browser.</span></span>
2. <span data-ttu-id="fd044-235">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 표시:</span><span class="sxs-lookup"><span data-stu-id="fd044-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="fd044-236">웹 앱 tooJava를 시작!</span><span class="sxs-lookup"><span data-stu-id="fd044-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="fd044-237">업데이트되었습니다!</span><span class="sxs-lookup"><span data-stu-id="fd044-237">This is updated!</span></span>
   <span data-ttu-id="fd044-238">2017년 6월 17일 일요일 16:39:10 UTC</span><span class="sxs-lookup"><span data-stu-id="fd044-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="fd044-239">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y</span><span class="sxs-lookup"><span data-stu-id="fd044-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="fd044-241">Linux의 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="fd044-241">For App service on Linux</span></span>

* <span data-ttu-id="fd044-242">tooverify, Azure CLI에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="fd044-243">결과 다음 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="fd044-244">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="fd044-245">Hello 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="fd044-246">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y</span><span class="sxs-lookup"><span data-stu-id="fd044-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="fd044-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd044-247">Next steps</span></span>

<span data-ttu-id="fd044-248">이 자습서에서는 Azure 앱 서비스 플러그 인 toodeploy tooAzure hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="fd044-249">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd044-250">Jenkins toodeploy FTP 통해 Azure 앱 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="fd044-251">Docker 통해 Linux에서 Jenkins toodeploy tooAzure 앱 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd044-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
