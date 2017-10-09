---
title: "Emulator Express toorun aaaUsing 및 디버그 Azure 클라우드 서비스는 로컬 컴퓨터에서 | Microsoft Docs"
description: "Emulator Express toorun 및 디버그 하는 클라우드 서비스를 사용 하 여 로컬 컴퓨터에서"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="46e15-103">Emulator Express를 사용 하 여 toorun 및 디버그 Azure 클라우드 서비스는 로컬 컴퓨터에서</span><span class="sxs-lookup"><span data-stu-id="46e15-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="46e15-104">Emulator Express를 사용하여 관리자로 Visual Studio를 실행하지 않고 클라우드 서비스를 테스트 및 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="46e15-105">Emulator Express 중 하나가 프로젝트 설정을 toouse 설정 하거나 클라우드 서비스의 hello 요구 사항에 따라 전체 에뮬레이터 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="46e15-106">Hello 전체 에뮬레이터에 대 한 자세한 내용은 참조 [hello 계산 에뮬레이터에서에서 Azure 응용 프로그램 실행](storage/common/storage-use-emulator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="46e15-107">Visual Studio에서 Emulator Express 사용</span><span class="sxs-lookup"><span data-stu-id="46e15-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="46e15-108">Azure SDK 2.3 이상에서 Azure 프로젝트를 만들 때 Emulator Express가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="46e15-109">이전 버전의 hello Azure SDK를 사용 하 여 만든 기존 프로젝트에 대 한 hello 다음 단계 tooselect Emulator Express를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="46e15-110">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="46e15-111">**솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="46e15-112">Hello 프로젝트 속성 페이지에서 선택 hello **웹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Azure 클라우드 서비스 프로젝트의 속성](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="46e15-114">**로컬 개발 서버** 아래에서 **IIS Express 사용 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="46e15-115">**에뮬레이터** 아래에서 **Emulator Express 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="46e15-116">toolaunch hello Emulator Express hello 다음 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="46e15-117">Emulator Express 제한 사항</span><span class="sxs-lookup"><span data-stu-id="46e15-117">Emulator Express limitations</span></span>
<span data-ttu-id="46e15-118">hello 될은 알려진 Emulator Express의 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="46e15-119">Emulator Express는 IIS 웹 서버와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="46e15-120">클라우드 서비스에는 여러 역할을 포함할 수 있지만 각 역할은 제한 된 tooone 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="46e15-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="46e15-121">1000 아래의 포트 번호에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="46e15-122">일반적으로 1000 아래의 포트를 사용 하는 인증 공급자를 사용 하는 경우이 값 tooa이 포트 번호를 1000 이상 toochange를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="46e15-123">Azure 계산 에뮬레이터 toohello 적용 되는 모든 제한 사항을 tooEmulator Express도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="46e15-124">예를 들어 배포당 50개 이상의 역할 인스턴스를 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="46e15-125">Azure 계산 에뮬레이터의 hello에 대 한 자세한 내용은 참조 [hello 계산 에뮬레이터에서에서 Azure 응용 프로그램 실행](http://go.microsoft.com/fwlink/p/?LinkId=623050)합니다.</span><span class="sxs-lookup"><span data-stu-id="46e15-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46e15-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46e15-126">Next steps</span></span>
[<span data-ttu-id="46e15-127">Azure Cloud Services 디버그</span><span class="sxs-lookup"><span data-stu-id="46e15-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
