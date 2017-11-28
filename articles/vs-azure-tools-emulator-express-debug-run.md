---
title: "Emulator Express를 사용하여 Azure 클라우드 서비스를 로컬 컴퓨터에서 실행 및 디버그 | Microsoft Docs"
description: "Emulator Express를 사용하여 클라우드 서비스를 로컬 컴퓨터에서 실행 및 디버그"
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
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="e6ef3-103">Emulator Express를 사용하여 로컬 컴퓨터에서 Azure 클라우드 서비스 실행 및 디버그</span><span class="sxs-lookup"><span data-stu-id="e6ef3-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="e6ef3-104">Emulator Express를 사용하여 관리자로 Visual Studio를 실행하지 않고 클라우드 서비스를 테스트 및 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="e6ef3-105">클라우드 서비스의 요구 사항에 따라 Emulator Express 또는 전체 에뮬레이터를 사용하도록 프로젝트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="e6ef3-106">전체 에뮬레이터에 대한 자세한 내용은 [계산 에뮬레이터에서 Azure 응용 프로그램 실행](storage/common/storage-use-emulator.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="e6ef3-107">Visual Studio에서 Emulator Express 사용</span><span class="sxs-lookup"><span data-stu-id="e6ef3-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="e6ef3-108">Azure SDK 2.3 이상에서 Azure 프로젝트를 만들 때 Emulator Express가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="e6ef3-109">이전 버전의 Azure SDK를 사용하여 만든 기존 프로젝트의 경우 다음 단계에 따라 Emulator Express를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="e6ef3-110">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e6ef3-111">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="e6ef3-112">프로젝트 속성 페이지에서 **웹** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Azure 클라우드 서비스 프로젝트의 속성](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="e6ef3-114">**로컬 개발 서버** 아래에서 **IIS Express 사용 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="e6ef3-115">**에뮬레이터** 아래에서 **Emulator Express 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="e6ef3-116">Emulator Express를 시작하려면 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="e6ef3-117">Emulator Express 제한 사항</span><span class="sxs-lookup"><span data-stu-id="e6ef3-117">Emulator Express limitations</span></span>
<span data-ttu-id="e6ef3-118">다음 문제는 Emulator Express의 알려진 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="e6ef3-119">Emulator Express는 IIS 웹 서버와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="e6ef3-120">클라우드 서비스는 여러 역할을 포함할 수 있지만 각 역할은 하나의 인스턴스로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="e6ef3-121">1000 아래의 포트 번호에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="e6ef3-122">일반적으로 1000 아래의 포트를 사용하는 인증 공급자를 사용하는 경우 1000 위의 포트 번호로 이 값을 변경해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="e6ef3-123">Azure 계산 에뮬레이터에 적용되는 모든 제한 사항은 Emulator Express에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="e6ef3-124">예를 들어 배포당 50개 이상의 역할 인스턴스를 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="e6ef3-125">Azure 계산 에뮬레이터에 대한 자세한 내용은 [계산 에뮬레이터에서 Azure 응용 프로그램 실행](http://go.microsoft.com/fwlink/p/?LinkId=623050)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6ef3-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6ef3-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6ef3-126">Next steps</span></span>
[<span data-ttu-id="e6ef3-127">Azure Cloud Services 디버그</span><span class="sxs-lookup"><span data-stu-id="e6ef3-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
