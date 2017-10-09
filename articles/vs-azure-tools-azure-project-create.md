---
title: "Visual Studio에서 Azure 클라우드 서비스 프로젝트 aaaCreating | Microsoft Docs"
description: "이제 toocreate Visual Studio에서 Azure 클라우드 서비스 프로젝트에 알아봅니다"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="45fbb-103">Visual Studio에서 Azure 클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="45fbb-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="45fbb-104">Azure Tools for Visual Studio hello Azure 클라우드 서비스를 만들 수 있는 프로젝트 템플릿을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="45fbb-105">Visual Studio tooconfigure hello 프로젝트를 만든 후 하면, 디버깅 및 hello 클라우드 서비스 tooAzure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="45fbb-106">단계 toocreate Visual Studio에서 Azure 클라우드 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="45fbb-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="45fbb-107">이 섹션에서는 하나 이상의 웹 역할을 사용하여 Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="45fbb-108">관리자 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="45fbb-109">Hello 주 메뉴에서 선택 **파일** > **새로** > **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="45fbb-110">선택 **클라우드** hello Visual C# 또는 Visual Basic에서 프로젝트 템플릿 노드에서 선택한 **Azure 클라우드 서비스** hello 템플릿 목록에서.</span><span class="sxs-lookup"><span data-stu-id="45fbb-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![새 Azure 클라우드 서비스](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="45fbb-112">Hello toouse toodevelop 프로젝트를 원하는.NET Framework의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="45fbb-113">이름 및 프로젝트에 대 한 위치와 hello 솔루션에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="45fbb-114">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-114">Select **OK**.</span></span>

1. <span data-ttu-id="45fbb-115">Hello에 **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 선택 hello 역할 tooadd, 원하고 hello 오른쪽 화살표 단추 tooadd 선택으로 tooyour 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![새 Azure 클라우드 서비스 역할 선택](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="45fbb-117">hover hello hello 역할에서 역할을 추가한 toorename **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 hello 상황에 맞는 메뉴에서 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="45fbb-118">솔루션 내에서 역할 이름을 변경할 수 있습니다 (hello에 **솔루션 탐색기**)에 추가 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Azure 클라우드 서비스 역할 이름 바꾸기](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="45fbb-120">Visual Studio Azure 프로젝트 hello hello 솔루션에 연결 toohello 역할 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="45fbb-121">hello 프로젝트도 hello *서비스 정의 파일* 및 *서비스 구성 파일*:</span><span class="sxs-lookup"><span data-stu-id="45fbb-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="45fbb-122">**서비스 정의 파일** -은 필요한 역할을 포함 하는 응용 프로그램, 끝점 및 가상 컴퓨터 크기에 대 한 hello 런타임 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="45fbb-123">**서비스 구성 파일** -역할의 인스턴스 개수 실행 되 고 hello 역할에 대해 정의 된 hello 설정의 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="45fbb-124">이러한 파일에 대 한 자세한 내용은 참조 [Visual Studio에서 Azure 클라우드 서비스에 대 한 hello 역할 구성](vs-azure-tools-configure-roles-for-cloud-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45fbb-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45fbb-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45fbb-125">Next steps</span></span>
- [<span data-ttu-id="45fbb-126">Visual Studio에서 Azure 클라우드 서비스 프로젝트의 역할 관리</span><span class="sxs-lookup"><span data-stu-id="45fbb-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
