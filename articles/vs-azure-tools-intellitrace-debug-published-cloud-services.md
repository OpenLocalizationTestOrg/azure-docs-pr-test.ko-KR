---
title: "Azure에서 게시 된 aaaDebugging 클라우드 Visual Studio 및 IntelliTrace와 서비스 | Microsoft Docs"
description: "Visual Studio 및 IntelliTrace와 toodebug 하는 클라우드 서비스 하는 방법에 대해 알아봅니다"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="12e6d-103">Visual Studio 및 IntelliTrace를 사용하여 게시된 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="12e6d-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="12e6d-104">IntelliTrace를 사용하여 Azure에서 실행할 때 역할 인스턴스에 대한 광범위한 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="12e6d-105">IntelliTrace 로그 toostep hello Azure에서 실행 중인 경우에 따라 toofind hello 원인을 해야 할 경우 Visual Studio에서 코드를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="12e6d-106">실제로 IntelliTrace 키 코드 실행 및 환경 데이터를 기록 Azure 응용 프로그램은 Azure에서 클라우드 서비스로 실행 되 고 수 있습니다는 Visual Studio에서 hello 기록 데이터를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="12e6d-107">Visual Studio Enterprise가 설치되어 있으며 Azure 응용 프로그램 대상 .NET Framework 4 이상 버전이 있는 경우 IntelliTrace를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="12e6d-108">IntelliTrace는 Azure 역할에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="12e6d-109">이러한 역할에 대 한 hello 가상 컴퓨터는 항상 64 비트 운영 체제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="12e6d-110">사용할 수 있습니다 [원격 디버깅](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach 직접 tooa 클라우드 서비스가 Azure에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12e6d-111">IntelliTrace는 디버그 시나리오 전용이며 프로덕션 배포용으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="12e6d-112">IntelliTrace에 대한 Azure 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="12e6d-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="12e6d-113">tooenable IntelliTrace는 Azure 응용 프로그램에 대 한 만들고 해야 Visual Studio Azure 프로젝트에서 hello 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="12e6d-114">TooAzure 게시 하기 전에 Azure 응용 프로그램에 대 한 IntelliTrace를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="12e6d-115">IntelliTrace를 구성 하지 않고 응용 프로그램을 게시 하는 경우 toorepublish hello 프로젝트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="12e6d-116">자세한 내용은 [Visual Studio를 사용하여 Azure Cloud Services 게시](http://go.microsoft.com/fwlink/p/?LinkId=623012)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12e6d-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="12e6d-117">중이면 toodeploy Azure 응용 프로그램을 준비에서 프로젝트 빌드 대상이 너무 설정 되어 있는지 확인**디버그**합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="12e6d-118">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="12e6d-119">Hello에 **Azure 응용 프로그램 게시** 대화 상자, 선택 hello Azure 구독 및 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="12e6d-120">Hello에 **설정** 페이지, 선택 hello **고급 설정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="12e6d-121">Hello 켜기 **IntelliTrace 사용** hello 클라우드에 게시할 때 응용 프로그램에 대 한 IntelliTrace 로그 toocollect 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="12e6d-122">toocustomize hello 기본 IntelliTrace 구성을 선택 **설정** 다음 너무**IntelliTrace 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![IntelliTrace 설정 링크](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="12e6d-124">Hello에 **IntelliTrace 설정** 대화 상자에서 어떤 이벤트 toolog, toocollect 호출 정보 여부, 모듈 및 프로세스 toocollect 어떤에 대 한 로그 및 얼마나 많은 공간이 tooallocate toohello 기록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="12e6d-125">IntelliTrace에 대한 자세한 내용은 [IntelliTrace로 디버깅](http://go.microsoft.com/fwlink/?LinkId=214468)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12e6d-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace 설정](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="12e6d-127">hello IntelliTrace 로그는 (hello 기본 크기는 250MB) hello IntelliTrace 설정에 지정 된 hello 최대 크기의 순환 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="12e6d-128">IntelliTrace 로그는 hello 가상 컴퓨터의 hello 파일 시스템에서 수집 된 tooa 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="12e6d-129">Hello 로그를 요청할 스냅숏으로 시간 해당 시점에 수행 하 고 tooyour 로컬 컴퓨터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="12e6d-130">Hello Azure 클라우드 서비스에 대 한 게시 된 tooAzure를 수행한 후 Azure hello에서 IntelliTrace가 설정 되었는지 확인할 수 있습니다에 노드 **서버 탐색기**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="12e6d-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![서버 탐색기 - IntelliTrace 사용](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="12e6d-132">역할 인스턴스에 대한 IntelliTrace 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="12e6d-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="12e6d-133">Visual Studio를 사용하여 다음 단계를 통해 역할 인스턴스에 대한 IntelliTrace 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="12e6d-134">**서버 탐색기**, hello 확장 **클라우드 서비스** 노드를 해당 로그를 toodownload 역할 인스턴스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="12e6d-135">Hello 역할 인스턴스를 마우스 오른쪽 단추로 클릭 하 고 hello s 상황에 맞는 메뉴에서 선택 **IntelliTrace 로그 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![IntelliTrace 로그 보기 메뉴 옵션](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="12e6d-137">hello IntelliTrace 로그는 로컬 컴퓨터의 디렉터리에 다운로드 한 tooa 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="12e6d-138">Hello IntelliTrace 로그를 요청할 때마다 새 스냅숏이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="12e6d-139">Visual Studio hello에 hello 연산의 hello 진행률을 표시 hello 로그를 다운로드 하는 동안 **Azure 활동 로그** 창.</span><span class="sxs-lookup"><span data-stu-id="12e6d-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="12e6d-140">Hello 다음 그림에에서 나와 있는 것 처럼 hello 작업 toosee hello 행 항목을 자세히를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="12e6d-142">Hello IntelliTrace 로그를 다운로드 하는 동안 Visual Studio에서 toowork를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="12e6d-143">Hello 로그 다운로드 완료 되 면 Visual Studio에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="12e6d-144">hello IntelliTrace 로그 포함 될 수 있습니다 예외 hello framework를 생성 하 고 나중에 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="12e6d-145">내부 프레임워크 코드는 안전하게 무시할 수 있도록 역할을 시작할 때의 일반적인 한 부분으로 이러한 예외를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="12e6d-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="12e6d-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12e6d-146">Next steps</span></span>
- [<span data-ttu-id="12e6d-147">Azure Cloud Services 디버깅 옵션</span><span class="sxs-lookup"><span data-stu-id="12e6d-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="12e6d-148">Visual Studio를 사용하여 클라우드 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="12e6d-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)