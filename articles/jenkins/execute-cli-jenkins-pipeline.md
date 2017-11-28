---
title: "Jenkins로 Azure CLI 실행 | Microsoft Docs"
description: "Azure CLI를 사용하여 Jenkins 파이프라인을 통해 Azure에 Java 웹앱을 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="2588c-103">Jenkins 및 Azure CLI를 사용해 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="2588c-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="2588c-104">Azure에 Java 웹앱을 배포하기 위해 [Jenkins 파이프라인](https://jenkins.io/doc/book/pipeline/)에서 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="2588c-105">이 자습서에서는 Azure VM에서 CI/CD 파이프라인을 만들며 다음 방법이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2588c-106">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="2588c-107">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="2588c-107">Configure Jenkins</span></span>
> * <span data-ttu-id="2588c-108">Azure에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="2588c-109">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="2588c-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="2588c-110">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="2588c-111">파이프라인 실행 및 웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="2588c-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="2588c-112">이 자습서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2588c-113">버전을 확인하려면 `az --version`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="2588c-114">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2588c-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="2588c-115">Jenkins 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2588c-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="2588c-116">Jenkins 마스터가 아직 없는 경우 [솔루션 템플릿](install-jenkins-solution-template.md)으로 시작합니다. 이 템플릿에는 필수 [Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) 플러그 인이 기본적으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="2588c-117">Azure 자격 증명 플러그 인을 사용하면 Microsoft Azure 서비스 주체 자격 증명을 Jenkins에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="2588c-118">버전 1.2에서는 Jenkins 파이프라인이 Azure 자격 증명을 얻을 수 있도록 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="2588c-119">버전 1.2 이상이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="2588c-120">Jenkins 대시보드 내에서 **Jenkins 관리->플러그 인 관리자->**를 클릭하고 **Azure 자격 증명**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="2588c-121">버전이 1.2보다 이전이면 플러그 인을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="2588c-122">Java JDK 및 Maven도 Jenkins 마스터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="2588c-123">설치하려면 SSH를 사용하여 Jenkins 마스터에 로그인하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="2588c-124">Jenkins 자격 증명에 Azure 서비스 주체 추가</span><span class="sxs-lookup"><span data-stu-id="2588c-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="2588c-125">Azure CLI를 실행하려면 Azure 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="2588c-126">Jenkins 대시보드 내에서 **자격 증명->시스템->**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="2588c-127">**전역 자격 증명(제한 없음)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="2588c-128">**자격 증명 추가**를 클릭한 다음 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점을 입력하여 [Microsoft Azure 서비스 주체](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="2588c-129">이후 단계에서 사용할 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-129">Provide an ID for use in subsequent step.</span></span>

![자격 증명 추가](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="2588c-131">Java 웹앱을 배포하기 위한 Azure App Service 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="2588c-132">[az appservice plan create](/cli/azure/appservice/plan#create) CLI 명령을 사용하여 **무료** 가격 책정 계층과 함께 Azure App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="2588c-133">App Service 계획은 앱을 호스트하는 데 사용되는 실제 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="2588c-134">App Service 계획에 할당된 모든 응용 프로그램은 이들 리소스를 공유하므로 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="2588c-135">계획이 준비되면 Azure CLI는 다음 예와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="2588c-136">Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-136">Create an Azure Web app</span></span>

 <span data-ttu-id="2588c-137">[az webapp create](/cli/azure/appservice/web#create) CLI 명령을 사용하여 `myAppServicePlan` App Service 계획에서 웹앱 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="2588c-138">웹앱 정의는 응용 프로그램에 액세스하는 URL을 제공하고 Azure에 코드를 배포하는 몇 가지 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="2588c-139">`<app_name>` 자리 표시자를 고유한 앱 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="2588c-140">이 고유한 이름은 웹앱에 대한 기본 도메인 이름의 일부이므로 이름은 Azure에 있는 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="2588c-141">사용자에게 노출하기 전에 웹앱에 사용자 지정 도메인 이름 항목을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="2588c-142">웹앱 정의가 준비되면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="2588c-143">Java 구성</span><span class="sxs-lookup"><span data-stu-id="2588c-143">Configure Java</span></span> 

<span data-ttu-id="2588c-144">[az appservice web config update](/cli/azure/appservice/web/config#update) 명령으로 앱에 필요한 Java 런타임 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="2588c-145">다음 명령은 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0에서 실행되도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="2588c-146">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="2588c-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="2588c-147">[Azure용 간단한 Java 웹앱](https://github.com/azure-devops/javawebappsample) 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="2588c-148">사용자 고유의 GitHub 계정에 리포지토리를 분기하려면 오른쪽 위 모서리에 있는 **분기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="2588c-149">GitHub 웹 UI에서 **Jenkinsfile** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="2588c-150">연필 아이콘을 클릭하여 이 파일을 편집하고 줄 20과 21에서 각각 웹앱의 리소스 그룹 및 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="2588c-151">줄 23을 변경하여 Jenkins 인스턴스의 자격 증명 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="2588c-152">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="2588c-153">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="2588c-154">작업 이름을 제공하고 **파이프라인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="2588c-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-155">Click **OK**.</span></span>
* <span data-ttu-id="2588c-156">**파이프라인** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="2588c-157">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="2588c-158">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="2588c-159">분기 리포지토리의 GitHub URL을 입력합니다(https:\<분기 리포지토리\>.git).</span><span class="sxs-lookup"><span data-stu-id="2588c-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="2588c-160">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="2588c-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="2588c-161">파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="2588c-161">Test your pipeline</span></span>
* <span data-ttu-id="2588c-162">만든 파이프라인으로 이동한 다음 **지금 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="2588c-163">몇 초 후에 빌드에 성공하고, 빌드로 이동한 다음 **콘솔 출력**을 클릭하여 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="2588c-164">웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="2588c-164">Verify your web app</span></span>
<span data-ttu-id="2588c-165">WAR 파일이 웹앱에 성공적으로 배포되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="2588c-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="2588c-166">웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-166">Open a web browser:</span></span>

* <span data-ttu-id="2588c-167">http://&lt;app_name>.azurewebsites.net/api/calculator/ping으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="2588c-168">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="2588c-169">http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>(&lt;x> 및 &lt;y>를 임의의 숫자로 대체)로 이동하여 x와 y의 합계를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="2588c-171">Linux에서 Azure Web App에 배포</span><span class="sxs-lookup"><span data-stu-id="2588c-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="2588c-172">이제 Jenkins 파이프라인에서 Azure CLI를 사용하는 방법을 배웠으므로 Linux에서 Azure Web App에 배포하도록 스크립트를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="2588c-173">Linux에서 Web App은 Docker를 사용하여 배포를 수행하는 다양한 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="2588c-174">배포하려면 서비스 런타임에 웹앱을 Docker 이미지로 패키지화 하는 Dockerfile을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="2588c-175">그러면 플러그 인이 이미지를 빌드하고 Docker 레지스트리에 푸시하고 이미지를 웹앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="2588c-176">Linux에서 실행되는 Azure Web App을 만들려면 [이 단계](/azure/app-service-web/app-service-linux-how-to-create-web-app)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2588c-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="2588c-177">이 [문서](https://docs.docker.com/engine/installation/linux/ubuntu/)의 지침에 따라 Jenkins 인스턴스에 Docker를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="2588c-178">[이 단계](/azure/container-registry/container-registry-get-started-azure-cli)에 따라 Azure Portal에 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="2588c-179">분기한 동일한 [Azure용 간단한 Java 웹앱](https://github.com/azure-devops/javawebappsample) 리포지토리에서 **Jenkinsfile2** 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="2588c-180">18-21줄에서 리소스 그룹, 웹앱 및 ACR의 이름으로 각각 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="2588c-181">24줄에서 \<azsrvprincipal\>을 자격 증명 ID로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="2588c-182">Windows에서 Azure 웹앱에 배포할 때 수행했던 것처럼 새 Jenkins 파이프라인을 만듭니다. 이번에만 대신 **Jenkinsfile2**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="2588c-183">새 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-183">Run your new job.</span></span>
* <span data-ttu-id="2588c-184">확인하려면 Azure CLI에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="2588c-185">다음 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="2588c-186">http://&lt;app_name>.azurewebsites.net/api/calculator/ping으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="2588c-187">메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="2588c-188">http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>(&lt;x> 및 &lt;y>를 임의의 숫자로 대체)로 이동하여 x와 y의 합계를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="2588c-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2588c-189">Next steps</span></span>
<span data-ttu-id="2588c-190">이 자습서에서는 GitHub 리포지토리에 있는 소스 코드를 확인하는 Jenkins 파이프라인을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="2588c-191">Maven을 실행하여 war 파일을 작성한 다음 Azure CLI를 사용하여 Azure App Service를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="2588c-192">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2588c-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2588c-193">Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="2588c-194">Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="2588c-194">Configure Jenkins</span></span>
> * <span data-ttu-id="2588c-195">Azure에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="2588c-196">GitHub 리포지토리 준비</span><span class="sxs-lookup"><span data-stu-id="2588c-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="2588c-197">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="2588c-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="2588c-198">파이프라인 실행 및 웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="2588c-198">Run the pipeline and verify the web app</span></span>
