---
title: "Visual Studio에서 연결 된 서비스를 사용 하 여 Azure 저장소 aaaAdd | Microsoft Docs"
description: "Hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 Azure 저장소 tooyour 앱 추가"
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
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="0dae8-103">Visual Studio 연결 서비스를 사용하여 Azure 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="0dae8-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="0dae8-104">Visual Studio와 함께 hello tooAzure 저장소 hello를 사용 하 여 다음 중 하나 연결할 수 있습니다 **연결 된 서비스 추가** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="0dae8-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="0dae8-105">C# 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="0dae8-105">C# cloud service</span></span>
- <span data-ttu-id="0dae8-106">.NET 백 엔드 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="0dae8-106">.NET backend mobile service</span></span>
- <span data-ttu-id="0dae8-107">ASP.NET 웹 사이트 또는 서비스</span><span class="sxs-lookup"><span data-stu-id="0dae8-107">ASP.NET website or service</span></span>
- <span data-ttu-id="0dae8-108">ASP.NET Core 서비스</span><span class="sxs-lookup"><span data-stu-id="0dae8-108">ASP.NET Core service</span></span>
- <span data-ttu-id="0dae8-109">Azure WebJob 서비스</span><span class="sxs-lookup"><span data-stu-id="0dae8-109">Azure WebJob service</span></span> 

<span data-ttu-id="0dae8-110">hello 연결된 서비스 기능 모든 필요한 hello 참조와 연결 코드 tooyour 프로젝트를 추가 및 구성 파일을 적절 하 게 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="0dae8-111">작업이 완료 되 면 hello **연결 된 서비스 추가** 설명서 hello 단계 필요한 toostart blob 저장소, 큐 및 테이블 사용을 자세히 보여 주는 대화 상자에 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="0dae8-112">TooAzure hello 연결 된 서비스를 사용 하 여 저장소 연결 대화 상자</span><span class="sxs-lookup"><span data-stu-id="0dae8-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="0dae8-113">Visual Studio에서 프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="0dae8-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="0dae8-114">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **연결 된 서비스** 노드를 선택 하 고 hello 상황에 맞는 메뉴에서 **연결 된 서비스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Azure 연결된 서비스 추가](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="0dae8-116">Hello에 **연결 된 서비스** 페이지에서 **Azure 저장소와 클라우드 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure Storage 추가](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="0dae8-118">Hello에 **Azure 저장소** 대화 상자, 기존 저장소 계정 선택 및 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="0dae8-119">저장소 계정 toocreate 해야 할 경우 toohello 다음 단계로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="0dae8-120">그렇지 않은 경우 6 toostep를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-120">Otherwise, skip toostep 6.</span></span>
    
    ![기존 저장소 계정 tooproject 추가](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="0dae8-122">toocreate 저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="0dae8-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="0dae8-123">선택 **새 저장소 계정 만들기** hello hello 대화 상자 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="0dae8-124">Hello 채울 **저장소 계정 만들기** 대화 상자를 닫고 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![새 Azure Storage 계정](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="0dae8-126">Hello 때 **Azure 저장소** 대화 상자가 표시 됩니다, 새 저장소 계정 hello hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="0dae8-127">Hello 목록의 hello 새 저장소 계정을 선택 하 고 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="0dae8-128">저장소 연결된 서비스 hello 아래에 나타납니다. hello **서비스 참조** 프로젝트의 노드.</span><span class="sxs-lookup"><span data-stu-id="0dae8-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="0dae8-129">프로젝트를 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="0dae8-129">How your project is modified</span></span>
<span data-ttu-id="0dae8-130">Hello 대화를 완료 하면 Visual Studio는 참조를 추가 하 고 특정 구성 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="0dae8-131">그러면 특정 변경 내용이 hello hello 프로젝트 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0dae8-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="0dae8-132">ASP.NET 프로젝트 - [변경된 내용 – ASP.NET 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="0dae8-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="0dae8-133">ASP.NET Core 프로젝트 - [변경된 내용 – ASP.NET 5 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="0dae8-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="0dae8-134">클라우드 서비스 프로젝트(웹 역할 및 작업자 역할) - [변경된 내용 – 클라우드 서비스 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="0dae8-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="0dae8-135">WebJob 프로젝트 - [변경된 내용 -WebJob 프로젝트](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="0dae8-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dae8-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0dae8-136">Next steps</span></span>
- [<span data-ttu-id="0dae8-137">MSDN 포럼: Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="0dae8-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="0dae8-138">Microsoft Azure Storage 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="0dae8-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="0dae8-139">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="0dae8-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
