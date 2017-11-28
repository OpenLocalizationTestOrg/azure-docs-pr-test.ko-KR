---
title: "aaaAzure 서비스 끝점"
description: "Hello Azure 서비스 끝점 설정 hello Eclipse 용 Azure 도구 키트에에서 설명 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="a39fd-103">Azure 서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="a39fd-103">Azure Service Endpoints</span></span>
<span data-ttu-id="a39fd-104">Azure 서비스 끝점 응용 프로그램이 hello 전역 Azure 플랫폼에서 관리 하는 배포 된 tooand 인지 Azure 21Vianet에서 운영 중국 또는 개인 Azure 플랫폼을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="a39fd-105">hello **서비스 끝점** 대화 상자에서는 toospecify 서비스 toouse 원하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="a39fd-106">tooopen hello **서비스 끝점** Eclipse 내에서 대화 상자에서 클릭 **창**, 클릭 **기본 설정**, 확장 **Azure**, 클릭 하 고 **서비스 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="a39fd-107">설정 hello **활성 집합** 필드 현재 작업 영역에 있는 Azure 서비스 끝점 hello에 사용할 Azure 프로젝트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="a39fd-108">hello 다음 표시 되어 hello **서비스 끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a39fd-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="a39fd-109">tooset hello 서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="a39fd-109">tooset hello service endpoints</span></span>
<span data-ttu-id="a39fd-110">Hello에 **서비스 끝점** 대화 상자에서 hello 다음 동작 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="a39fd-111">Toouse hello 전역 Azure 플랫폼을 hello에서 원하는 **활성 집합** 드롭다운 목록에서 선택 **windowsazure.com** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="a39fd-112">Azure hello에서 중국의 21vianet이 운영 toouse 원하면 **활성 집합** 드롭다운 목록에서 선택 **windowsazure.cn (중국)** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="a39fd-113">개인 Azure 플랫폼 toouse 하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="a39fd-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="a39fd-114">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="a39fd-115">대화 상자가 열리고 해당 hello 알리는 **서비스 끝점** hello 기본 설정 집합 파일을 열 및 대화 상자가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="a39fd-116">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-116">Click **OK**.</span></span>

  3. <span data-ttu-id="a39fd-117">Hello preferencesets.xml 파일에서 만들 새 `preferenceset` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="a39fd-118">이 새 요소에 대 한 만들기 `name`, `blob`, `management`, `portalURL` 및 `publishsettings` 특성 및 tooyour 개인 Azure 플랫폼에 해당 하는 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="a39fd-119">Hello 기존 제공 hello 값을 사용 하려면 `preferenceset` 템플릿으로 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="a39fd-120">**참고**: hello에 사용 되는 값을 hello `blob` 특성 hello 텍스트 "blob" hello URL에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="a39fd-121">preferencesets.xml을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="a39fd-122">Hello를 다시 열고 **서비스 끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a39fd-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="a39fd-123">Hello에서 **활성 집합** 드롭다운 목록에서 선택 hello 활성 집합 생성 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="a39fd-124">개인 Azure 플랫폼을 만든 후 `preferenceset` 요소인 hello 할당 된 값 tooit hello를 클릭 하 여 변경할 수 있습니다 **편집** hello 단추 **서비스 끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a39fd-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="a39fd-125">또한 원하는 경우 여러 개인 Azure 플랫폼 `preferenceset` 요소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="a39fd-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a39fd-126">See Also</span></span>
<span data-ttu-id="a39fd-127">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a39fd-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a39fd-128">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a39fd-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a39fd-129">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a39fd-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a39fd-130">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
