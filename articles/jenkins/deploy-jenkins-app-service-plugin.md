---
title: "Jenkins 플러그 인을 사용해 Azure App Service에 배포 | Microsoft Docs"
description: "Azure App Service Jenkins 플러그 인을 사용하여 Jenkins에서 Azure에 Java 웹앱을 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="559e2-103">Jenkins 플러그 인으로 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="559e2-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="559e2-104">Azure에 Java 웹앱을 배포하려면 [Jenkins 파이프라인](/azure/jenkins/execute-cli-jenkins-pipeline)의 Azure CLI를 사용하거나 [Azure App Service Jenkins 플러그 인](https://plugins.jenkins.io/azure-app-service)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="559e2-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="559e2-106">FTP를 통해 Azure App Service에 배포하도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="559e2-107">Docker를 통해 Linux의 Azure App Service에 배포하도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="559e2-108">Jenkins 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="559e2-109">Jenkins 마스터가 아직 없는 경우 [솔루션 템플릿](install-jenkins-solution-template.md)으로 시작합니다. 이 템플릿에는 JDK8 및 다음 필수 플러그 인이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="559e2-110">[Jenkins Git 클라이언트 플러그 인](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="559e2-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="559e2-111">[Docker Commons 플러그 인](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="559e2-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="559e2-112">[Azure 자격 증명](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="559e2-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="559e2-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="559e2-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="559e2-114">App Service 플러그 인을 사용하여 Azure App Service에서 지원되는 모든 언어(예: C#, PHP, Java 및 node.js 등)로 웹앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="559e2-115">이 자습서에서는 샘플 Java 앱인 [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="559e2-116">사용자 고유의 GitHub 계정에 리포지토리를 분기하려면 오른쪽 위 모서리에 있는 **분기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="559e2-117">Java 프로젝트 빌드를 위해 Java JDK 및 Maven이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="559e2-118">지속적인 통합을 위해 사용하는 경우 Jenkins 마스터 또는 VM 에이전트에 구성 요소를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="559e2-119">설치하려면 SSH를 사용하여 Jenkins 인스턴스에 로그인하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="559e2-120">Linux에 App Service를 배포하는 경우 빌드에 사용되는 VM 에이전트 또는 Jenkins 마스터에도 Docker를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="559e2-121">도커를 설치하려면 다음 문서를 참조하십시오. https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="559e2-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="559e2-122">Jenkins 자격 증명에 Azure 서비스 주체 추가</span><span class="sxs-lookup"><span data-stu-id="559e2-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="559e2-123">Azure에 배포하려면 Azure 서비스 주체가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="559e2-124">[Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 또는 [Azure Portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal)을 사용하여 Azure 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="559e2-125">Jenkins 대시보드 내에서 **자격 증명->시스템->**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="559e2-126">**전역 자격 증명(제한 없음)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="559e2-127">**자격 증명 추가**를 클릭한 다음 구독 ID, 클라이언트 ID, 클라이언트 암호 및 OAuth 2.0 토큰 끝점을 입력하여 Microsoft Azure 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="559e2-128">이후 단계에서 사용할 ID **mySp**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="559e2-129">Azure App Service 플러그 인</span><span class="sxs-lookup"><span data-stu-id="559e2-129">Azure App Service plugin</span></span>

<span data-ttu-id="559e2-130">Azure App Service 플러그 인 v1.0은 다음을 통해 Azure 웹앱으로의 지속적인 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="559e2-131">Git 및 FTP</span><span class="sxs-lookup"><span data-stu-id="559e2-131">Git and FTP</span></span>
* <span data-ttu-id="559e2-132">Linux의 웹앱용 Docker</span><span class="sxs-lookup"><span data-stu-id="559e2-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="559e2-133">Jenkins 대시보드를 사용하여 FTP를 통해 웹앱을 배포하도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="559e2-134">Azure 웹앱에 프로젝트를 배포하려면 Git 또는 FTP를 사용하여 빌드 아티팩트(예:.Java의 .war 파일)를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="559e2-135">Jenkins에서 작업을 설정하기 전에 Azure App Service 계획과 Java 앱에서 실행하기 위한 웹앱이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="559e2-136">[az appservice plan create](/cli/azure/appservice/plan#create) CLI 명령을 사용하여 **무료** 가격 책정 계층과 함께 Azure App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="559e2-137">App Service 계획은 앱을 호스트하는 데 사용되는 실제 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="559e2-138">App Service 계획에 할당된 모든 응용 프로그램은 이들 리소스를 공유하므로 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="559e2-139">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-139">Create a Web App.</span></span> <span data-ttu-id="559e2-140">[Azure Portal](/azure/app-service-web/web-sites-configure)을 사용하거나 다음 Az CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="559e2-141">앱에 필요한 Java 런타임 구성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="559e2-142">다음 Azure CLI 명령은 최근 Java 8 JDK 및 [Apache Tomcat](http://tomcat.apache.org/) 8.0에서 실행되도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="559e2-143">Jenkins 작업 설정</span><span class="sxs-lookup"><span data-stu-id="559e2-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="559e2-144">Jenkins 대시보드에 새 **프리스타일** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="559e2-145">**리포지토리 URL**을 제공하여 [Azure용 간단한 Java 웹앱](https://github.com/azure-devops/javawebappsample)의 로컬 분기를 사용하도록 **소스 코드 관리**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="559e2-146">예: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="559e2-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="559e2-147">빌드 단계를 추가하여 Maven을 사용하여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="559e2-148">이를 위해 **셸 실행**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="559e2-149">이 예제의 경우 대상 폴더의 *.war 파일 이름을 ROOT.war로 바꾸기 위한 추가 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="559e2-150">**Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="559e2-151">이전 단계에서 저장한 Azure 서비스 주체 "mySp"를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="559e2-152">**앱 구성** 섹션에서 구독의 리소스 그룹 및 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="559e2-153">플러그 인은 웹앱이 Windows 기반인지 또는 Linux 기반인지를 자동으로 탐지합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="559e2-154">Windows 기반 웹앱의 경우 "파일 게시" 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="559e2-155">배포할 파일을 입력합니다(예: Java를 사용 중인 경우 war 패키지). 소스 디렉터리와 대상 디렉터리는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="559e2-156">파일을 업로드할 때 매개 변수를 사용하여 소스 및 대상 폴더를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="559e2-157">Azure의 Java 웹앱은 Tomcat 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="559e2-158">따라서 webapps 폴더에 war 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="559e2-159">이 예제에서는 **소스 디렉터리**를 "target"으로 설정하고 **대상 디렉터리**에 "webapps"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="559e2-160">프로덕션 이외의 슬롯에 배포하려는 경우 **슬롯** 이름도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="559e2-161">프로젝트를 저장하고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-161">Save the project and build it.</span></span> <span data-ttu-id="559e2-162">빌드가 완료되면 웹앱이 Azure에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="559e2-163">Jenkins 파이프라인을 사용하여 FTP를 통해 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="559e2-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="559e2-164">플러그 인에서 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="559e2-165">GitHub 리포지토리의 샘플을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="559e2-166">GitHub 웹 UI에서 **Jenkinsfile_ftp_plugin** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="559e2-167">연필 아이콘을 클릭하여 이 파일을 편집하고 줄 11과 12에서 각각 웹앱의 리소스 그룹 및 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="559e2-168">줄 14를 변경하여 Jenkins 인스턴스의 자격 증명 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="559e2-169">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="559e2-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="559e2-170">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="559e2-171">작업 이름을 제공하고 **파이프라인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="559e2-172">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-172">Click **OK**.</span></span>
3. <span data-ttu-id="559e2-173">**파이프라인** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="559e2-174">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="559e2-175">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="559e2-176">분기 리포지토리의 GitHub URL을 입력합니다(https:&lt;분기 리포지토리>.git).</span><span class="sxs-lookup"><span data-stu-id="559e2-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="559e2-177">**스크립트 경로**를 "Jenkinsfile_ftp_plugin"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="559e2-178">**저장**을 클릭하고 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="559e2-179">Jenkins를 구성하여 Docker를 통해 Linux에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="559e2-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="559e2-180">Git/FTP 외에 Linux의 웹앱은 Docker를 사용한 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="559e2-181">Docker를 사용하여 배포하려면 서비스 런타임에 웹앱을 Docker 이미지로 패키지화하는 Dockerfile을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="559e2-182">그러면 플러그 인이 이미지를 빌드하고 Docker 레지스트리에 푸시하고 이미지를 웹앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="559e2-183">Linux의 웹앱은 Git 및 FTP와 같은 일반적인 방법도 지원하지만 기본 제공되는 언어에 한합니다(.NET Core, Node.js, PHP 및 Ruby).</span><span class="sxs-lookup"><span data-stu-id="559e2-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="559e2-184">다른 언어의 경우 응용 프로그램 코드와 서비스 런타임을 함께 Docker 이미지로 패키징하고 Docker를 사용하여 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="559e2-185">Jenkins에서 작업을 설정하기 전에 Linux에 Azure App Service가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="559e2-186">개인 Docker 컨테이너 이미지를 저장하고 관리하기 위해 컨테이너 레지스트리도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="559e2-187">DockerHub를 사용할 수 있습니다. 이 예제에서는 Azure Container Registry를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="559e2-188">[여기](/azure/app-service-web/app-service-linux-how-to-create-web-app)에 나온 단계에 따라 Linux에서 웹앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="559e2-189">Azure Container Registry는 오픈 소스 Docker Registry 2.0에 기반한 관리되는 [Docker 레지스트리](https://docs.docker.com/registry/) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="559e2-190">방법에 대한 추가 지침이 필요한 경우 [여기](/azure/container-registry/container-registry-get-started-azure-cli)에 나온 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="559e2-191">DockerHub를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="559e2-192">Docker를 사용하여 배포하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-192">To deploy using docker:</span></span>

1. <span data-ttu-id="559e2-193">Jenkins 대시보드에 새 프리스타일 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="559e2-194">**리포지토리 URL**을 제공하여 [Azure용 간단한 Java 웹앱](https://github.com/azure-devops/javawebappsample)의 로컬 분기를 사용하도록 **소스 코드 관리**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="559e2-195">예: http://github.com/&lt;yourid>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="559e2-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="559e2-196">빌드 단계를 추가하여 Maven을 사용하여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="559e2-197">이를 위해 **셸 실행**을 추가하고 **명령**에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="559e2-198">**Azure 웹앱 게시**를 선택하여 빌드 후 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="559e2-199">이전 단계에서 저장한 Azure 서비스 주체 **mySp**를 Azure 자격 증명으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="559e2-200">**앱 구성** 섹션에서 구독의 리소스 그룹 및 Linux 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="559e2-201">Docker를 통해 게시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="559e2-202">**Dockerfile** 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="559e2-203">기본값 "/Dockerfile"을 유지할 수 있습니다. Azure Container Registry를 사용하는 경우 **Docker 레지스트리 URL**에 https://&lt;myRegistry>.azurecr.io 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="559e2-204">DockerHub를 사용하는 경우 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="559e2-205">**레지스트리 자격 증명**에는 Azure Container Registry에 대한 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="559e2-206">Azure CLI에서 다음 명령을 실행하여 사용자 ID와 암호를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="559e2-207">첫 번째 명령은 관리자 계정을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="559e2-208">**고급** 탭의 Docker 이미지 이름 및 태그는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="559e2-209">기본적으로 이미지 이름은 Azure Portal에서(Docker 컨테이너 설정에) 구성한 이미지 이름에서 가져옵니다. 태그는 $BUILD_NUMBER에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="559e2-210">Azure Portal에 이미지 이름을 지정하거나 **고급** 탭의 **Docker 이미지**에 대한 값을 제공해야 합니다. 이 예제의 경우 **Docker 이미지**에 "&lt;yourRegistry>.azurecr.io/calculator"를 입력하고 **Docker 이미지 태그**는 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="559e2-211">기본 제공 Docker 이미지 설정을 사용할 경우 배포가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="559e2-212">Azure Portal의 Docker 컨테이너 설정에서 사용자 지정 이미지를 사용하도록 Docker 구성을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="559e2-213">기본 제공 이미지의 경우 파일 업로드 방법을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="559e2-214">파일 업로드 방법과 비슷한 방법으로, 프로덕션 이외의 다른 슬롯을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="559e2-215">프로젝트를 만들고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-215">Save and build the project.</span></span> <span data-ttu-id="559e2-216">컨테이너 이미지가 레지스트리로 푸시되고 웹앱이 배포되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="559e2-217">Jenkins 파이프라인을 사용하여 Docker를 통해 Linux에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="559e2-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="559e2-218">GitHub 웹 UI에서 **Jenkinsfile_container_plugin** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="559e2-219">연필 아이콘을 클릭하여 이 파일을 편집하고 줄 11과 12에서 각각 웹앱의 리소스 그룹 및 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="559e2-220">줄 13을 컨테이너 레지스트리 서버로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="559e2-221">줄 16을 변경하여 Jenkins 인스턴스의 자격 증명 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="559e2-222">Jenkins 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="559e2-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="559e2-223">웹 브라우저에서 Jenkins를 열고 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="559e2-224">작업 이름을 제공하고 **파이프라인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="559e2-225">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-225">Click **OK**.</span></span>
3. <span data-ttu-id="559e2-226">**파이프라인** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="559e2-227">**정의**에서 **SCM의 파이프라인 스크립트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="559e2-228">**SCM**에서 **Git**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="559e2-229">분기 리포지토리의 GitHub URL을 입력합니다(https:&lt;분기 리포지토리>.git).</span><span class="sxs-lookup"><span data-stu-id="559e2-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="559e2-230">7, **스크립트 경로**를 "Jenkinsfile_container_plugin"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="559e2-231">**저장**을 클릭하고 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="559e2-232">웹앱 확인</span><span class="sxs-lookup"><span data-stu-id="559e2-232">Verify your web app</span></span>

1. <span data-ttu-id="559e2-233">WAR 파일이 웹앱에 성공적으로 배포되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="559e2-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="559e2-234">웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-234">Open a web browser.</span></span>
2. <span data-ttu-id="559e2-235">http://&lt;app_name>.azurewebsites.net/api/calculator/ping으로 이동하면 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="559e2-236">Java 웹앱 시작!!!</span><span class="sxs-lookup"><span data-stu-id="559e2-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="559e2-237">업데이트되었습니다!</span><span class="sxs-lookup"><span data-stu-id="559e2-237">This is updated!</span></span>
   <span data-ttu-id="559e2-238">2017년 6월 17일 일요일 16:39:10 UTC</span><span class="sxs-lookup"><span data-stu-id="559e2-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="559e2-239">http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>(&lt;x> 및 &lt;y>를 임의의 숫자로 대체)로 이동하여 x와 y의 합계를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![계산기: 추가](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="559e2-241">Linux의 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="559e2-241">For App service on Linux</span></span>

* <span data-ttu-id="559e2-242">확인하려면 Azure CLI에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="559e2-243">다음 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="559e2-244">http://&lt;app_name>.azurewebsites.net/api/calculator/ping으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="559e2-245">메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="559e2-246">http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>(&lt;x> 및 &lt;y>를 임의의 숫자로 대체)로 이동하여 x와 y의 합계를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="559e2-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="559e2-247">Next steps</span></span>

<span data-ttu-id="559e2-248">이 자습서에서는 Azure App Service 플러그 인을 사용하여 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="559e2-249">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="559e2-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="559e2-250">FTP를 통해 Azure App Service를 배포하도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="559e2-251">Docker를 통해 Linux의 Azure App Service에 배포하도록 Jenkins 구성</span><span class="sxs-lookup"><span data-stu-id="559e2-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 