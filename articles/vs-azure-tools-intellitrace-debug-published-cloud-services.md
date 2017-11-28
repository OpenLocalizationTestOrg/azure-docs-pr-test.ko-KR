---
title: "Visual Studio 및 IntelliTrace를 사용하여 게시된 Azure 클라우드 서비스 디버깅 | Microsoft Docs"
description: "Visual Studio 및 IntelliTrace를 사용하여 클라우드 서비스를 디버그하는 방법을 알아봅니다."
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
ms.openlocfilehash: 7905dfb97cbd7578a8422567fe674839d00c21ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="0539e-103">Visual Studio 및 IntelliTrace를 사용하여 게시된 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="0539e-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="0539e-104">IntelliTrace를 사용하여 Azure에서 실행할 때 역할 인스턴스에 대한 광범위한 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="0539e-105">문제의 원인을 찾아야 하는 경우 Azure에서 실행 중인 것처럼 Visual Studio에서 코드를 단계별로 거쳐 IntelliTrace 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="0539e-106">실제로 Azure에서 Azure 응용 프로그램을 클라우드 서비스로 실행 중일 때 IntelliTrace는 키 코드 실행 및 환경 데이터를 기록하여 Visual Studio에서 기록된 데이터를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span></span> 

<span data-ttu-id="0539e-107">Visual Studio Enterprise가 설치되어 있으며 Azure 응용 프로그램 대상 .NET Framework 4 이상 버전이 있는 경우 IntelliTrace를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="0539e-108">IntelliTrace는 Azure 역할에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="0539e-109">이러한 역할에 대한 가상 컴퓨터는 항상 64비트 운영 체제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-109">The virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="0539e-110">대체 방법으로 [원격 디버깅](http://go.microsoft.com/fwlink/p/?LinkId=623041)을 사용하여 Azure에서 실행 중인 클라우드 서비스로 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0539e-111">IntelliTrace는 디버그 시나리오 전용이며 프로덕션 배포용으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="0539e-112">IntelliTrace에 대한 Azure 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="0539e-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="0539e-113">Azure 응용 프로그램에 IntelliTrace를 사용하려면 Visual Studio Azure 프로젝트에서 응용 프로그램을 만들고 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span></span> <span data-ttu-id="0539e-114">Azure에 게시하기 전에 Azure 응용 프로그램에 대한 IntelliTrace를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span></span> <span data-ttu-id="0539e-115">IntelliTrace를 구성하지 않고 응용 프로그램을 게시하는 경우 프로젝트를 다시 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span></span> <span data-ttu-id="0539e-116">자세한 내용은 [Visual Studio를 사용하여 Azure Cloud Services 게시](http://go.microsoft.com/fwlink/p/?LinkId=623012)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0539e-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="0539e-117">Azure 응용 프로그램을 배포할 준비가 되면 프로젝트의 빌드 대상이 **디버그**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span></span>

1. <span data-ttu-id="0539e-118">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, 상황에 맞는 메뉴에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="0539e-119">**Azure 응용 프로그램 게시** 대화 상자에서 Azure 구독을 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="0539e-120">**설정** 페이지에서 **고급 설정** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-120">In the **Settings** page, select the **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="0539e-121">클라우드에 게시될 때 응용 프로그램에 대한 IntelliTrace 로그를 수집하려면 **IntelliTrace 사용** 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span></span>
   
1. <span data-ttu-id="0539e-122">기본 IntelliTrace 구성을 사용자 지정하려면 **IntelliTrace 사용** 옆의 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span></span>

    ![IntelliTrace 설정 링크](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="0539e-124">**IntelliTrace 설정** 대화 상자에서 기록할 이벤트, 호출 정보를 수집할지 여부, 로그를 수집할 모듈 및 프로세스, 기록에 할당할 공간의 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span></span> <span data-ttu-id="0539e-125">IntelliTrace에 대한 자세한 내용은 [IntelliTrace로 디버깅](http://go.microsoft.com/fwlink/?LinkId=214468)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0539e-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace 설정](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="0539e-127">IntelliTrace 로그는 IntelliTrace 설정에 지정된 최대 크기(기본 크기는 250MB)의 순환 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span></span> <span data-ttu-id="0539e-128">IntelliTrace 로그는 가상 컴퓨터의 파일 시스템에서 파일에 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span></span> <span data-ttu-id="0539e-129">로그를 요청하는 경우 스냅숏이 해당 시점에 수행되며 로컬 컴퓨터에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span></span>

<span data-ttu-id="0539e-130">Azure 클라우드 서비스를 Azure에 게시한 후 다음 그림에 표시된 것처럼 **서버 탐색기**의 Azure 노드에서 IntelliTrace가 활성화되었는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span></span>

![서버 탐색기 - IntelliTrace 사용](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="0539e-132">역할 인스턴스에 대한 IntelliTrace 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="0539e-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="0539e-133">Visual Studio를 사용하여 다음 단계를 통해 역할 인스턴스에 대한 IntelliTrace 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="0539e-134">**서버 탐색기**에서 **Cloud Services** 노드를 확장하고 로그를 다운로드할 역할 인스턴스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span></span> 

1. <span data-ttu-id="0539e-135">역할 인스턴스를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **IntelliTrace 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![IntelliTrace 로그 보기 메뉴 옵션](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="0539e-137">IntelliTrace 로그는 로컬 컴퓨터의 디렉터리에 있는 파일에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span></span> <span data-ttu-id="0539e-138">IntelliTrace 로그를 요청할 때마다 새 스냅숏이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="0539e-139">로그가 다운로드되는 경우 Visual Studio는 **Azure 활동 로그** 창에서 작업의 진행률을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span></span> <span data-ttu-id="0539e-140">다음 그림에 표시된 것과 같이 작업에 대한 품목을 확장하여 자세한 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="0539e-142">IntelliTrace 로그를 다운로드하는 동안 Visual Studio에서 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span></span> <span data-ttu-id="0539e-143">로그 다운로드가 완료되면 Visual Studio에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-143">When the log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="0539e-144">IntelliTrace 로그는 프레임워크가 생성되고 이후에 처리되는 예외를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span></span> <span data-ttu-id="0539e-145">내부 프레임워크 코드는 안전하게 무시할 수 있도록 역할을 시작할 때의 일반적인 한 부분으로 이러한 예외를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0539e-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0539e-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0539e-146">Next steps</span></span>
- [<span data-ttu-id="0539e-147">Azure Cloud Services 디버깅 옵션</span><span class="sxs-lookup"><span data-stu-id="0539e-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="0539e-148">Visual Studio를 사용하여 클라우드 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="0539e-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)