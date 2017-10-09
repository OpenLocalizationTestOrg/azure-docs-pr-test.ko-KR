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
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="002fd-103">TooAzure Jenkins 서비스 응용 프로그램을 배포 하 고 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="002fd-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="002fd-104">Java 웹 응용 프로그램 tooAzure toodeploy Azure CLI에 사용할 수 있습니다 [Jenkins 파이프라인](https://jenkins.io/doc/book/pipeline/)합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="002fd-105">이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="002fd-106">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="002fd-107">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="002fd-107">Configure Jenkins</span></span>
> * <span data-ttu-id="002fd-108">Azure에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="002fd-109">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="002fd-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="002fd-110">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="002fd-111">Hello 파이프라인을 실행 하 고 hello 웹 응용 프로그램을 확인</span><span class="sxs-lookup"><span data-stu-id="002fd-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="002fd-112">이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상.</span><span class="sxs-lookup"><span data-stu-id="002fd-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="002fd-113">toofind hello 버전을 실행 `az --version`합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="002fd-114">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="002fd-115">Jenkins 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="002fd-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="002fd-116">Hello로 시작 하는 Jenkins 마스터 아직 없는 경우 [솔루션 템플릿을](install-jenkins-solution-template.md), 필요한 hello를 포함 하는 [Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) 기본적으로 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="002fd-117">hello Azure 자격 증명 플러그 인 Jenkins에 toostore Microsoft Azure 서비스 사용자 자격 증명을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="002fd-118">버전 1.2에서에서 지원이 추가 되었습니다 hello Jenkins 파이프라인 hello Azure 자격 증명을 가져올 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="002fd-119">버전 1.2 이상이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="002fd-120">Hello Jenkins 대시보드 내에서 클릭 **Jenkins 관리 플러그 인 관리자->->** 검색 한 **Azure 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="002fd-121">Hello 버전 1.2 보다 이전 이면 hello 플러그 인을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="002fd-122">Java JDK 및 Maven hello Jenkins 마스터에도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="002fd-123">tooinstall, SSH를 사용 하 여 tooJenkins 마스터에 로그인 하 고 hello 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="002fd-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="002fd-124">Azure 서비스 주체 tooJenkins 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="002fd-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="002fd-125">Azure 자격 증명은 필요한 tooexecute Azure CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="002fd-126">Hello Jenkins 대시보드 내에서 클릭 **자격 증명-> 시스템->**합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="002fd-127">**전역 자격 증명(제한 없음)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="002fd-128">클릭 **추가 자격 증명** tooadd는 [Microsoft Azure 서비스 사용자](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점 hello 입력 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="002fd-129">이후 단계에서 사용할 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-129">Provide an ID for use in subsequent step.</span></span>

![자격 증명 추가](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="002fd-131">Hello Java 웹 응용 프로그램을 배포 하기 위한 Azure 앱 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="002fd-132">Hello로 Azure 앱 서비스 계획 만들기 **무료** 가격 책정 계층 hello를 사용 하 여 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="002fd-133">앱 서비스 계획 hello hello 사용 하는 물리적 리소스 toohost 앱을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="002fd-134">Tooan 앱 서비스 계획을 할당 하는 모든 응용 프로그램에 있도록 toosave 비용 여러 앱을 호스트 하는 경우 이러한 리소스를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="002fd-135">Hello 계획 준비 되 면 Azure CLI 표시 비슷한 hello toohello 다음 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="002fd-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="002fd-136">Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-136">Create an Azure Web app</span></span>

 <span data-ttu-id="002fd-137">사용 하 여 hello [az webapp 만들](/cli/azure/appservice/web#create) CLI 명령 toocreate hello에 있는 웹 응용 프로그램 정의 `myAppServicePlan` 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="002fd-138">URL tooaccess 응용 프로그램에 제공 하 고 몇 가지 옵션 toodeploy 코드 tooAzure를 구성 하는 hello 웹 응용 프로그램 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="002fd-139">대체 hello `<app_name>` 자신의 고유한 응용 프로그램 이름 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="002fd-140">이 고유 이름이 hello 웹 앱에 대 한 기본 도메인 이름 hello의 일부 이므로 hello 이름 필요한 toobe 고유 Azure에서 모든 앱에서.</span><span class="sxs-lookup"><span data-stu-id="002fd-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="002fd-141">Tooyour 사용자 노출 먼저 사용자 지정 도메인 이름 항목 toohello 웹 응용 프로그램을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="002fd-142">Hello 웹 응용 프로그램 정의 준비 되 면 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="002fd-143">Java 구성</span><span class="sxs-lookup"><span data-stu-id="002fd-143">Configure Java</span></span> 

<span data-ttu-id="002fd-144">Hello로 앱 필요한 hello Java 런타임 구성을 설정 [az 앱 서비스 웹 구성 업데이트](/cli/azure/appservice/web/config#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="002fd-145">hello 다음 명령을 hello 웹 앱 toorun에서 구성 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="002fd-146">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="002fd-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="002fd-147">열기 hello [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) 리 포 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="002fd-148">toofork hello 리포지토리 tooyour GitHub 계정이 소유한, hello 클릭 **포크** hello 오른쪽 위 모퉁이의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="002fd-149">GitHub 웹 UI에서 **Jenkinsfile** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="002fd-150">Hello 연필 아이콘 tooedit이 파일 tooupdate hello 리소스 그룹 및 선 20 및 21 웹 응용 프로그램의 이름을 각각 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="002fd-151">Jenkins 인스턴스의 줄 23 tooupdate 자격 증명 ID를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="002fd-152">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="002fd-153">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="002fd-154">Hello 작업에 대 한 이름을 지정 하 고 선택 **파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="002fd-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-155">Click **OK**.</span></span>
* <span data-ttu-id="002fd-156">Hello 클릭 **파이프라인** 다음 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="002fd-157">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="002fd-158">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="002fd-159">분기 리 포에 대 한 hello GitHub URL 입력: https:\<분기 리 포\>.git</span><span class="sxs-lookup"><span data-stu-id="002fd-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="002fd-160">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="002fd-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="002fd-161">파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="002fd-161">Test your pipeline</span></span>
* <span data-ttu-id="002fd-162">만든 toohello 파이프라인 이동 **이제 빌드**</span><span class="sxs-lookup"><span data-stu-id="002fd-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="002fd-163">빌드는 몇 초 후에 성공적으로 및 toohello 빌드를 이동 하 고 클릭 **콘솔 출력** toosee hello 세부 정보</span><span class="sxs-lookup"><span data-stu-id="002fd-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="002fd-164">웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="002fd-164">Verify your web app</span></span>
<span data-ttu-id="002fd-165">tooverify hello WAR 파일을 정상적으로 배포 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="002fd-166">웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-166">Open a web browser:</span></span>

* <span data-ttu-id="002fd-167">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="002fd-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="002fd-168">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="002fd-169">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y</span><span class="sxs-lookup"><span data-stu-id="002fd-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="002fd-171">TooAzure Linux에서 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="002fd-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="002fd-172">Toouse Azure CLI 프로그램 Jenkins에 파이프라인 하는 방법을 파악 했으므로 hello 스크립트 toodeploy tooan Linux에서 Azure 웹 앱을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="002fd-173">웹 응용 프로그램에 액세스 Linux Docker toouse은 다른 방식으로 toodo hello 배포를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="002fd-174">toodeploy, tooprovide Docker 이미지를 서비스 런타임 사용 하 여 웹 앱을 패키지 하는 Dockerfile 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="002fd-175">hello 플러그 인 다음 hello 이미지, tooa Docker 레지스트리 푸시 빌드하고 hello 이미지 tooyour 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="002fd-176">Hello 단계에 따라 [여기](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux에서 실행 하는 Azure 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="002fd-177">Docker을 Jenkins 인스턴스에서 hello 지침에 따라 설치 [문서](https://docs.docker.com/engine/installation/linux/ubuntu/)합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="002fd-178">Hello 단계를 사용 하 여 컨테이너 레지스트리 hello Azure 포털에서에서 만들 [여기](/azure/container-registry/container-registry-get-started-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="002fd-179">동일한 hello [Azure에 대 한 간단한 Java 웹 응용 프로그램](https://github.com/azure-devops/javawebappsample) 리포지토리를 분기 하면 편집 hello **Jenkinsfile2** 파일:</span><span class="sxs-lookup"><span data-stu-id="002fd-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="002fd-180">18-21 줄, 각각 리소스 그룹, 웹 앱과 ACR의 toohello 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="002fd-181">줄 24, 업데이트 \<azsrvprincipal\> tooyour 자격 증명 ID</span><span class="sxs-lookup"><span data-stu-id="002fd-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="002fd-182">Windows에서는이 경우에만 사용 하 여 tooAzure 웹 앱을 배포할 때와 마찬가지로 새 Jenkins 파이프라인을 만들고 **Jenkinsfile2** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="002fd-183">새 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-183">Run your new job.</span></span>
* <span data-ttu-id="002fd-184">tooverify, Azure CLI에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="002fd-185">결과 다음 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="002fd-186">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="002fd-187">Hello 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="002fd-188">Toohttp 이동: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (대체 &lt;x > 및 &lt;y > 모든 번호로) tooget hello 총 x 및 y</span><span class="sxs-lookup"><span data-stu-id="002fd-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="002fd-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="002fd-189">Next steps</span></span>
<span data-ttu-id="002fd-190">이 자습서에서는 GitHub 리포지토리에 있는 hello 소스 코드를 확인 하는 Jenkins 파이프라인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="002fd-191">Maven toobuild war 파일을 실행 하 고 Azure CLI toodeploy tooAzure 앱 서비스를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="002fd-192">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="002fd-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="002fd-193">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="002fd-194">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="002fd-194">Configure Jenkins</span></span>
> * <span data-ttu-id="002fd-195">Azure에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="002fd-196">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="002fd-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="002fd-197">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="002fd-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="002fd-198">Hello 파이프라인을 실행 하 고 hello 웹 응용 프로그램을 확인</span><span class="sxs-lookup"><span data-stu-id="002fd-198">Run hello pipeline and verify hello web app</span></span>
