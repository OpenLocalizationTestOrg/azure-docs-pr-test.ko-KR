---
title: "Visual Studio에서 연결된 서비스를 사용하여 Azure 저장소 추가 | Microsoft Docs"
description: "Visual Studio 연결된 서비스 추가 대화 상자를 사용하여 Azure 저장소를 앱에 추가"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="709c1-103">Visual Studio 연결 서비스를 사용하여 Azure 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="709c1-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="709c1-104">Visual Studio를 사용하면 **연결된 서비스 추가** 대화 상자에서 Azure Storage에 다음을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="709c1-105">C# 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="709c1-105">C# cloud service</span></span>
- <span data-ttu-id="709c1-106">.NET 백 엔드 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="709c1-106">.NET backend mobile service</span></span>
- <span data-ttu-id="709c1-107">ASP.NET 웹 사이트 또는 서비스</span><span class="sxs-lookup"><span data-stu-id="709c1-107">ASP.NET website or service</span></span>
- <span data-ttu-id="709c1-108">ASP.NET Core 서비스</span><span class="sxs-lookup"><span data-stu-id="709c1-108">ASP.NET Core service</span></span>
- <span data-ttu-id="709c1-109">Azure WebJob 서비스</span><span class="sxs-lookup"><span data-stu-id="709c1-109">Azure WebJob service</span></span> 

<span data-ttu-id="709c1-110">연결된 서비스 기능은 필요한 모든 참조와 연결 코드를 프로젝트에 추가하고 구성 파일을 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="709c1-111">완료되면 **연결된 서비스 추가** 대화 상자에 Blob Storage, 큐, 테이블 작업을 시작하는 데 필요한 단계를 자세히 설명하는 설명서가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="709c1-112">연결된 서비스 대화 상자를 사용하여 Azure 저장소에 연결</span><span class="sxs-lookup"><span data-stu-id="709c1-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="709c1-113">Visual Studio에서 프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="709c1-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="709c1-114">**솔루션 탐색기**에서 **연결된 서비스** 노드를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **연결된 서비스 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Azure 연결된 서비스 추가](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="709c1-116">**연결된 서비스** 페이지에서 **Azure Storage의 클라우드 저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure Storage 추가](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="709c1-118">**Azure Storage** 대화 상자에서, 기존 저장소 계정을 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="709c1-119">저장소 계정을 만들어야 하는 경우 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="709c1-120">그렇지 않은 경우, 6단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-120">Otherwise, skip to step 6.</span></span>
    
    ![프로젝트에 기존 저장소 계정 추가](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="709c1-122">저장소 계정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="709c1-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="709c1-123">대화 상자 아래쪽에 있는 **새 저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="709c1-124">**저장소 계정 만들기** 대화 상자를 채운 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![새 Azure Storage 계정](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="709c1-126">**Azure Storage** 대화 상자가 표시되면 새 저장소 계정이 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="709c1-127">목록에서 새 저장소 계정을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="709c1-128">연결된 저장소 서비스가 프로젝트의 **서비스 참조** 노드 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="709c1-129">프로젝트를 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="709c1-129">How your project is modified</span></span>
<span data-ttu-id="709c1-130">대화 상자를 완료하면 Visual Studio는 참조를 추가하고 특정 구성 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="709c1-131">특정 변경 내용은 프로젝트 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="709c1-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="709c1-132">ASP.NET 프로젝트 - [변경된 내용 – ASP.NET 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="709c1-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="709c1-133">ASP.NET Core 프로젝트 - [변경된 내용 – ASP.NET 5 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="709c1-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="709c1-134">클라우드 서비스 프로젝트(웹 역할 및 작업자 역할) - [변경된 내용 – 클라우드 서비스 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="709c1-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="709c1-135">WebJob 프로젝트 - [변경된 내용 -WebJob 프로젝트](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="709c1-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="709c1-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="709c1-136">Next steps</span></span>
- [<span data-ttu-id="709c1-137">MSDN 포럼: Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="709c1-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="709c1-138">Microsoft Azure Storage 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="709c1-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="709c1-139">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="709c1-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
