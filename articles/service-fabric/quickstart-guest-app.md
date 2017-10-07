---
title: "aaaQuickly 기존 앱 tooan Azure 서비스 패브릭 클러스터를 배포 합니다."
description: "Visual Studio와 함께 Azure 서비스 패브릭 클러스터 toohost 기존 Node.js 응용 프로그램을 사용 합니다."
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
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="8356f-103">Azure Service Fabric에서 Node.js 응용 프로그램 호스트</span><span class="sxs-lookup"><span data-stu-id="8356f-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="8356f-104">이 퀵 스타트를 사용 하면 Azure에서 실행 하는 기존 응용 프로그램 (이 예제의 Node.js) tooa 서비스 패브릭 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8356f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8356f-105">Prerequisites</span></span>

<span data-ttu-id="8356f-106">시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="8356f-107">포함 된 hello 서비스 패브릭 SDK 및 Visual Studio 2017 또는 2015를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="8356f-108">또한 toohave 기존 Node.js 응용 프로그램 배포에 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="8356f-109">이 빠른 시작은 [여기][download-sample]에서 다운로드할 수 있는 간단한 Node.js 웹 사이트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="8356f-110">이 파일 tooyour 추출 `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello 다음 단계에서 hello 프로젝트를 만든 후 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="8356f-111">Azure 구독이 아직 없는 경우 [체험 계정][create-account]을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="8356f-112">Hello 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="8356f-112">Create hello service</span></span>

<span data-ttu-id="8356f-113">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="8356f-114">`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8356f-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="8356f-115">Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="8356f-116">Hello 응용 프로그램 이름을 **MyGuestApp** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8356f-117">Node.js는 hello 260 자까지 가능 windows에는 경로에 때 쉽게 중단 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="8356f-118">와 같은 hello 프로젝트 자체에 대 한 짧은 경로 사용 **c:\code\svc1**합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Visual Studio의 새 프로젝트 대화 상자][new-project]

<span data-ttu-id="8356f-120">Hello 다음 대화 상자에서 모든 유형의 서비스 패브릭 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="8356f-121">이 빠른 시작에서 **게스트 실행 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="8356f-122">Hello 서비스 이름을 **MyGuestService** hello 오른쪽 toohello에서 hello 옵션 설정에 따라 값:</span><span class="sxs-lookup"><span data-stu-id="8356f-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="8356f-123">설정</span><span class="sxs-lookup"><span data-stu-id="8356f-123">Setting</span></span>                   | <span data-ttu-id="8356f-124">값</span><span class="sxs-lookup"><span data-stu-id="8356f-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="8356f-125">코드 패키지 폴더</span><span class="sxs-lookup"><span data-stu-id="8356f-125">Code Package Folder</span></span>       | <span data-ttu-id="8356f-126">_&lt;Node.js 응용 프로그램과 함께 hello 폴더&gt;_</span><span class="sxs-lookup"><span data-stu-id="8356f-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="8356f-127">코드 패키지 동작</span><span class="sxs-lookup"><span data-stu-id="8356f-127">Code Package Behavior</span></span>     | <span data-ttu-id="8356f-128">폴더 내용을 tooproject 복사</span><span class="sxs-lookup"><span data-stu-id="8356f-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="8356f-129">프로그램</span><span class="sxs-lookup"><span data-stu-id="8356f-129">Program</span></span>                   | <span data-ttu-id="8356f-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="8356f-130">node.exe</span></span> |
| <span data-ttu-id="8356f-131">인수</span><span class="sxs-lookup"><span data-stu-id="8356f-131">Arguments</span></span>                 | <span data-ttu-id="8356f-132">server.js</span><span class="sxs-lookup"><span data-stu-id="8356f-132">server.js</span></span> |
| <span data-ttu-id="8356f-133">작업 폴더</span><span class="sxs-lookup"><span data-stu-id="8356f-133">Working Folder</span></span>            | <span data-ttu-id="8356f-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="8356f-134">CodePackage</span></span> |

<span data-ttu-id="8356f-135">**확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-135">Press **OK**.</span></span>

![Visual Studio의 새 서비스 대화 상자][new-service]

<span data-ttu-id="8356f-137">Visual Studio hello 응용 프로그램 프로젝트 만들고 hello 행위자 서비스 프로젝트 및 솔루션 탐색기에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="8356f-138">hello 응용 프로그램 프로젝트 (**MyGuestApp**) 코드는 직접 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="8356f-139">대신 서비스 프로젝트의 집합을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="8356f-140">추가로 3가지 다른 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="8356f-141">**게시 프로필**</span><span class="sxs-lookup"><span data-stu-id="8356f-141">**Publish profiles**</span></span>  
<span data-ttu-id="8356f-142">다양한 환경에 대한 도구 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="8356f-143">**스크립트**</span><span class="sxs-lookup"><span data-stu-id="8356f-143">**Scripts**</span></span>  
<span data-ttu-id="8356f-144">응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="8356f-145">**응용 프로그램 정의**</span><span class="sxs-lookup"><span data-stu-id="8356f-145">**Application definition**</span></span>  
<span data-ttu-id="8356f-146">응용 프로그램 매니페스트 hello 포함 *ApplicationPackageRoot*합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="8356f-147">연결 된 응용 프로그램 매개 변수 파일이 *ApplicationParameters*, hello 응용 프로그램을 정의 하 고 tooconfigure를 사용 하는 지정된 된 환경에 대해 구체적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="8356f-148">Hello 서비스 프로젝트의 hello 내용에 대 한 개요를 참조 하십시오. [신뢰할 수 있는 서비스 시작](service-fabric-reliable-services-quick-start.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="8356f-149">네트워킹 설정</span><span class="sxs-lookup"><span data-stu-id="8356f-149">Set up networking</span></span>

<span data-ttu-id="8356f-150">Node.js 응용 프로그램에서는 배포 하는 포트를 사용 하는 hello 예제 **80** tootell 해당 포트 표시 해야 하는 서비스 패브릭 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="8356f-151">열기 hello **ServiceManifest.xml** hello 프로젝트 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="8356f-152">Hello 매니페스트의 hello 맨 아래에는 한 `<Resources> \ <Endpoints>` 이미 정의 된 항목이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="8356f-153">해당 항목 tooadd 수정 `Port`, `Protocol`, 및 `Type`합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="8356f-154">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="8356f-154">Deploy tooAzure</span></span>

<span data-ttu-id="8356f-155">키를 누르면 **F5** 배포 toohello 로컬 클러스터는 hello 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="8356f-156">그러나 tooAzure를 대신 배포 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="8356f-157">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시...**  대화 toopublish tooAzure 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![게시 서비스 패브릭 서비스에 대 한 tooazure 대화 상자][publish]

<span data-ttu-id="8356f-159">선택 hello **PublishProfiles\Cloud.xml** 프로필 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="8356f-160">이전에 하지 않은 경우에 Azure 계정 toodeploy를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="8356f-161">아직 없는 경우 [하나에 등록][create-account]합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="8356f-162">아래 **연결 끝점**를 선택 하려면 서비스 패브릭 클러스터 toodeploy hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="8356f-163">선택 하지 않은 경우 하나를  **&lt;새 클러스터 만들기... &gt;**  웹 브라우저 창 toohello Azure 포털을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="8356f-164">자세한 내용은 참조 [hello 포털에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="8356f-165">Hello 서비스 패브릭 클러스터를 만들 때 확인 되었는지 tooset hello **사용자 지정 끝점** 너무 설정**80**합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![사용자 지정 끝점이 있는 Service Fabric 노드 형식 구성][custom-endpoint]

<span data-ttu-id="8356f-167">새 서비스 패브릭 클러스터를 만드는 데 몇 시간 toocomplete 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="8356f-168">생성 된, 이동 백 toohello 게시 대화 상자 및 선택 경과 했는데도 문제가 있다면 되 면  **&lt;새로 고침&gt;**합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="8356f-169">새 클러스터 hello hello 드롭다운 목록 상자에 나열 됩니다. 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="8356f-170">키를 눌러 **게시** hello 배포 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="8356f-171">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-171">This may take a few minutes.</span></span> <span data-ttu-id="8356f-172">완료 되 면 hello 응용 프로그램 toobe 완벽 하 게 사용할 수에 대 일 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="8356f-173">테스트 hello 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="8356f-173">Test hello website</span></span>

<span data-ttu-id="8356f-174">서비스가 게시된 후에 웹 브라우저에서 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="8356f-175">서비스 패브릭 서비스를 찾을 hello Azure 포털을 열고 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="8356f-176">Hello 개요 블레이드에 hello 서비스 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="8356f-177">Hello에서 사용 하 여 hello 도메인 이름 _클라이언트 연결 끝점_ 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="8356f-178">예: `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8356f-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![서비스 패브릭 개요 블레이드에 hello Azure 포털에서][overview]

<span data-ttu-id="8356f-180">Hello 나타납니다 toothis 주소 이동 `HELLO WORLD` 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="8356f-181">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8356f-181">Delete hello cluster</span></span>

<span data-ttu-id="8356f-182">이러한 리소스에 대 한 요금이 청구 됩니다 때이 퀵 스타트를 만든 후 hello 리소스를 모두 toodelete를 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8356f-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8356f-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8356f-183">Next steps</span></span>
<span data-ttu-id="8356f-184">[게스트 실행 파일](service-fabric-deploy-existing-app.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8356f-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F