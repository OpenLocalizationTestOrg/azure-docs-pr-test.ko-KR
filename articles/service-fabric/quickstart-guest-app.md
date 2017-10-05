---
title: "Azure Service Fabric 클러스터에 기존 앱을 신속하게 배포"
description: "Azure Service Fabric 클러스터를 사용하여 Visual Studio에서 기존 Node.js 응용 프로그램을 호스트합니다."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="d2d63-103">Azure Service Fabric에서 Node.js 응용 프로그램 호스트</span><span class="sxs-lookup"><span data-stu-id="d2d63-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="d2d63-104">이 빠른 시작을 통해 Azure에서 실행되는 Service Fabric 클러스터에 기존 응용 프로그램(이 예제에서는 Node.js)을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-104">This quickstart helps you deploy an existing application (Node.js in this example) to a Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2d63-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2d63-105">Prerequisites</span></span>

<span data-ttu-id="d2d63-106">시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="d2d63-107">Service Fabric SDK 및 Visual Studio 2017 또는 2015 설치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-107">Which includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="d2d63-108">또한 배포하기 위해 기존 Node.js 응용 프로그램이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-108">You also need to have an existing Node.js application for deployment.</span></span> <span data-ttu-id="d2d63-109">이 빠른 시작은 [여기][download-sample]에서 다운로드할 수 있는 간단한 Node.js 웹 사이트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="d2d63-110">다음 단계에서 프로젝트를 만든 후 `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` 폴더에 이 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-110">Extract this file to your `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create the project in the next step.</span></span>

<span data-ttu-id="d2d63-111">Azure 구독이 아직 없는 경우 [체험 계정][create-account]을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-the-service"></a><span data-ttu-id="d2d63-112">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="d2d63-112">Create the service</span></span>

<span data-ttu-id="d2d63-113">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="d2d63-114">`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d2d63-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="d2d63-115">**새 프로젝트** 대화 상자에서 **클라우드 > Service Fabric 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-115">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="d2d63-116">응용 프로그램의 이름을 **MyGuestApp**으로 지정하고 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-116">Name the application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d2d63-117">Node.js는 Windows에 있는 경로에 대한 260자 제한을 쉽게 초과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-117">Node.js can easily break the 260 character limit for paths that windows has.</span></span> <span data-ttu-id="d2d63-118">**c:\code\svc1**과 같은 프로젝트 자체에 짧은 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-118">Use a short path for the project itself such as **c:\code\svc1**.</span></span>
   
![Visual Studio의 새 프로젝트 대화 상자][new-project]

<span data-ttu-id="d2d63-120">다음 대화 상자에서 모든 형식의 Service Fabric 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-120">You can create any type of Service Fabric service from the next dialog.</span></span> <span data-ttu-id="d2d63-121">이 빠른 시작에서 **게스트 실행 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="d2d63-122">서비스 이름을 **MyGuestService**로 지정하고 다음과 같은 값으로 오른쪽에 있는 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-122">Name the service **MyGuestService** and set the options on the right to the following values:</span></span>

| <span data-ttu-id="d2d63-123">설정</span><span class="sxs-lookup"><span data-stu-id="d2d63-123">Setting</span></span>                   | <span data-ttu-id="d2d63-124">값</span><span class="sxs-lookup"><span data-stu-id="d2d63-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="d2d63-125">코드 패키지 폴더</span><span class="sxs-lookup"><span data-stu-id="d2d63-125">Code Package Folder</span></span>       | <span data-ttu-id="d2d63-126">_&lt;Node.js 앱을 포함한 폴더&gt;_</span><span class="sxs-lookup"><span data-stu-id="d2d63-126">_&lt;the folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="d2d63-127">코드 패키지 동작</span><span class="sxs-lookup"><span data-stu-id="d2d63-127">Code Package Behavior</span></span>     | <span data-ttu-id="d2d63-128">프로젝트에 폴더 내용 복사</span><span class="sxs-lookup"><span data-stu-id="d2d63-128">Copy folder contents to project</span></span> |
| <span data-ttu-id="d2d63-129">프로그램</span><span class="sxs-lookup"><span data-stu-id="d2d63-129">Program</span></span>                   | <span data-ttu-id="d2d63-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="d2d63-130">node.exe</span></span> |
| <span data-ttu-id="d2d63-131">인수</span><span class="sxs-lookup"><span data-stu-id="d2d63-131">Arguments</span></span>                 | <span data-ttu-id="d2d63-132">server.js</span><span class="sxs-lookup"><span data-stu-id="d2d63-132">server.js</span></span> |
| <span data-ttu-id="d2d63-133">작업 폴더</span><span class="sxs-lookup"><span data-stu-id="d2d63-133">Working Folder</span></span>            | <span data-ttu-id="d2d63-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="d2d63-134">CodePackage</span></span> |

<span data-ttu-id="d2d63-135">**확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-135">Press **OK**.</span></span>

![Visual Studio의 새 서비스 대화 상자][new-service]

<span data-ttu-id="d2d63-137">Visual Studio는 응용 프로그램 프로젝트 및 작업자 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-137">Visual Studio creates the application project and the actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="d2d63-138">응용 프로그램 프로젝트(**MyGuestApp**)는 코드를 직접 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-138">The application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="d2d63-139">대신 서비스 프로젝트의 집합을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="d2d63-140">추가로 3가지 다른 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="d2d63-141">**게시 프로필**</span><span class="sxs-lookup"><span data-stu-id="d2d63-141">**Publish profiles**</span></span>  
<span data-ttu-id="d2d63-142">다양한 환경에 대한 도구 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="d2d63-143">**스크립트**</span><span class="sxs-lookup"><span data-stu-id="d2d63-143">**Scripts**</span></span>  
<span data-ttu-id="d2d63-144">응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="d2d63-145">**응용 프로그램 정의**</span><span class="sxs-lookup"><span data-stu-id="d2d63-145">**Application definition**</span></span>  
<span data-ttu-id="d2d63-146">*ApplicationPackageRoot*에서 응용 프로그램 매니페스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-146">Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="d2d63-147">관련된 응용 프로그램 매개 변수 파일은 *ApplicationParameters*에 있으며 응용 프로그램을 정의하고 지정된 환경에 대해 해당 응용 프로그램을 구체적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-147">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
    
<span data-ttu-id="d2d63-148">서비스 프로젝트의 내용에 대한 개요는 [Reliable Services 시작](service-fabric-reliable-services-quick-start.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d63-148">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="d2d63-149">네트워킹 설정</span><span class="sxs-lookup"><span data-stu-id="d2d63-149">Set up networking</span></span>

<span data-ttu-id="d2d63-150">배포하는 예제 Node.js 앱은 포트 **80**을 사용하므로 Service Fabric에 해당 포트를 노출하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-150">The example Node.js app we're deploying uses port **80** and we need to tell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="d2d63-151">프로젝트에서 **ServiceManifest.xml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-151">Open the **ServiceManifest.xml** file in the project.</span></span> <span data-ttu-id="d2d63-152">매니페스트의 맨 아래에는 이미 정의된 항목이 포함된 `<Resources> \ <Endpoints>`이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-152">At the bottom of the manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="d2d63-153">해당 항목을 수정하여 `Port`, `Protocol` 및 `Type`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-153">Modify that entry to add `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a><span data-ttu-id="d2d63-154">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="d2d63-154">Deploy to Azure</span></span>

<span data-ttu-id="d2d63-155">**F5** 키를 누르고 프로젝트를 실행하면 로컬 클러스터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-155">If you press **F5** and run the project, it is deployed to the local cluster.</span></span> <span data-ttu-id="d2d63-156">하지만 대신 Azure에 배포해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-156">However, let's deploy to Azure instead.</span></span>

<span data-ttu-id="d2d63-157">프로젝트를 마우스 오른쪽 단추로 클릭하고 대화 상자를 여는 **게시...**를 선택하여 Azure에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-157">Right-click on the project and choose **Publish...** which opens a dialog to publish to Azure.</span></span>

![Service Fabric 서비스의 Azure 대화 상자에 게시][publish]

<span data-ttu-id="d2d63-159">**PublishProfiles\Cloud.xml** 대상 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-159">Select the **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="d2d63-160">이전에 수행하지 않은 경우 배포할 Azure 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-160">If you haven't previously, choose an Azure account to deploy to.</span></span> <span data-ttu-id="d2d63-161">아직 없는 경우 [하나에 등록][create-account]합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="d2d63-162">**연결 끝점**에서 배포할 Service Fabric 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-162">Under **Connection Endpoint**, select the Service Fabric cluster to deploy to.</span></span> <span data-ttu-id="d2d63-163">없는 경우 Azure Portal에 웹 브라우저 창을 여는 **&lt;새 클러스터 만들기...&gt;**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window to the Azure portal.</span></span> <span data-ttu-id="d2d63-164">자세한 내용은 [포털에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d63-164">For more information, see [create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="d2d63-165">Service Fabric 클러스터를 만들 때 **사용자 지정 끝점** 설정을 **80**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-165">When you create the Service Fabric cluster, make sure to set the **Custom endpoints** setting to **80**.</span></span>

![사용자 지정 끝점이 있는 Service Fabric 노드 형식 구성][custom-endpoint]

<span data-ttu-id="d2d63-167">새 Service Fabric 클러스터 만들기를 완료하려면 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-167">Creating a new Service Fabric cluster takes some time to complete.</span></span> <span data-ttu-id="d2d63-168">Service Fabric 클러스터를 만들면 게시 대화 상자로 다시 이동하고 **&lt;새로 고침&gt;**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-168">Once it has been created, go back to the publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="d2d63-169">새 클러스터가 드롭다운 상자에 나열되면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-169">The new cluster is listed in the drop-down box; select it.</span></span>

<span data-ttu-id="d2d63-170">**게시**를 눌러서 배포가 끝나기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-170">Press **Publish** and wait for the deployment to finish.</span></span>

<span data-ttu-id="d2d63-171">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-171">This may take a few minutes.</span></span> <span data-ttu-id="d2d63-172">배포가 완료된 후에 완벽하게 응용 프로그램을 사용할 수 있는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-172">After it completes, it may take a few more minutes for the application to be fully available.</span></span>

## <a name="test-the-website"></a><span data-ttu-id="d2d63-173">웹 사이트 테스트</span><span class="sxs-lookup"><span data-stu-id="d2d63-173">Test the website</span></span>

<span data-ttu-id="d2d63-174">서비스가 게시된 후에 웹 브라우저에서 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="d2d63-175">먼저 Azure Portal을 열고 Service Fabric 서비스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-175">First, open the Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="d2d63-176">서비스 주소의 개요 블레이드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-176">Check the overview blade of the service address.</span></span> <span data-ttu-id="d2d63-177">_클라이언트 연결 끝점_ 속성의 도메인 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-177">Use the domain name from the _Client connection endpoint_ property.</span></span> <span data-ttu-id="d2d63-178">예: `http://mysvcfab1.westus2.cloudapp.azure.com`</span><span class="sxs-lookup"><span data-stu-id="d2d63-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Azure Portal에서 Service Fabric 개요 블레이드][overview]

<span data-ttu-id="d2d63-180">`HELLO WORLD` 응답이 표시되는 이 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-180">Navigate to this address where you will see the `HELLO WORLD` response.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="d2d63-181">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="d2d63-181">Delete the cluster</span></span>

<span data-ttu-id="d2d63-182">해당 리소스에 대한 요금이 청구되므로 이 빠른 시작에서 만든 리소스를 모두 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d63-182">Do not forget to delete all of the resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d63-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2d63-183">Next steps</span></span>
<span data-ttu-id="d2d63-184">[게스트 실행 파일](service-fabric-deploy-existing-app.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d2d63-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F