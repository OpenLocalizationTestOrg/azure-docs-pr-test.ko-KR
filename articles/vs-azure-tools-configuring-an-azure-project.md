---
title: "Visual Studio에서 Azure 클라우드 서비스 프로젝트 aaaConfigure | Microsoft Docs"
description: "어떻게 tooconfigure Azure 클라우드 해당 프로젝트에 대 한 요구 사항에 따라 Visual Studio에서 서비스 프로젝트에 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="42f40-103">Visual Studio에서 Azure 클라우드 서비스 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="42f40-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="42f40-104">프로젝트 요구 사항에 따라 Azure 클라우드 서비스 프로젝트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="42f40-105">다음 범주 hello에 대 한 hello 프로젝트에 대 한 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="42f40-106">**클라우드 서비스 tooAzure 게시** -기존 클라우드 서비스 배포 tooAzure 실수로 삭제 되지 않도록 하는 속성 toomake를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="42f40-107">**Hello 로컬 컴퓨터에서 클라우드 서비스 실행 또는 디버그할** -서비스 구성 toouse를 선택할 수 있으며 toostart hello Azure 저장소 에뮬레이터를 표시할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="42f40-108">**만들 때 클라우드 서비스 패키지의 유효성을 검사** -아무 문제 없이 배포 해당 hello 클라우드 서비스 패키지를 확인할 수 있도록 모든 경고를 오류로 tootreat를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="42f40-109">단계 tooconfigure Azure 클라우드 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="42f40-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="42f40-110">Visual Studio에서 클라우드 서비스 프로젝트 열기 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="42f40-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="42f40-111">**솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="42f40-112">Hello 프로젝트의 속성 페이지에서 선택 hello **개발** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![프로젝트 속성 메뉴](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="42f40-114">설정 **기존 배포를 삭제 하기 전에 확인** 너무**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="42f40-115">이 설정을 통해 Azure의 기존 배포가 실수로 삭제 하지 않으면 tooensure</span><span class="sxs-lookup"><span data-stu-id="42f40-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="42f40-116">원하는 선택 hello **서비스 구성** tooindicate 서비스 구성을 원하는 toouse 실행 하거나 클라우드 서비스를 로컬로 디버깅할 때.</span><span class="sxs-lookup"><span data-stu-id="42f40-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="42f40-117">방법에 대 한 자세한 내용은 toomodify는 역할에 대 한 서비스 구성을 참조 [어떻게 Azure에 대 한 tooconfigure hello 역할 클라우드 Visual Studio와 함께 서비스](./vs-azure-tools-configure-roles-for-cloud-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="42f40-118">설정 **Azure 저장소 에뮬레이터 시작** 너무**True** toostart hello Azure 저장소 에뮬레이터를 실행 하거나 클라우드 서비스를 로컬로 디버깅할 때.</span><span class="sxs-lookup"><span data-stu-id="42f40-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="42f40-119">설정 **경고를 오류로 처리** 너무**True** toomake 있는지 패키지 유효성 검사 오류가 있는 경우 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="42f40-120">설정 **웹 프로젝트 포트 사용** 너무**True** IIS Express에서 로컬로 시작할 때마다 웹 역할이 동일한 포트 각각 hello를 사용 하는지 toomake 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="42f40-121">Visual Studio 도구 모음 hello **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="42f40-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f40-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42f40-122">Next steps</span></span>
- [<span data-ttu-id="42f40-123">여러 서비스 구성을 사용하여 Azure 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="42f40-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

