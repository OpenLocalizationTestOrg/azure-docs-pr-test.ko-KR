---
title: "Azure 서비스 끝점"
description: "Eclipse용 Azure 도구 키트에서 Azure 서비스 끝점 설정을 설명합니다."
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
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="fbede-103">Azure 서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="fbede-103">Azure Service Endpoints</span></span>
<span data-ttu-id="fbede-104">Azure 서비스 끝점은 응용 프로그램이 글로벌 Azure 플랫폼에서 배포되고 관리되는지, 중국의 21Vianet에서 운영하는 Azure인지, 개인 Azure 플랫폼인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="fbede-105">**서비스 끝점** 대화 상자를 통해 사용하려는 서비스 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="fbede-106">**서비스 끝점** 대화 상자를 열려면 Eclipse 내에서 **창**, **기본 설정**을 차례로 클릭하고 **Azure**를 확장한 다음 **서비스 끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="fbede-107">**Active Set** (활성 설정) 필드를 설정하여 Azure 서비스 끝점을 현재 작업 영역에서 Azure 프로젝트에 사용할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="fbede-108">다음은 **서비스 끝점** 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="fbede-109">서비스 끝점을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="fbede-109">To set the service endpoints</span></span>
<span data-ttu-id="fbede-110">**서비스 끝점** 대화 상자에서 다음 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="fbede-111">글로벌 Azure 플랫폼을 사용하려는 경우 **활성 설정** 드롭다운 목록에서 **windowsazure.com**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="fbede-112">중국의 21Vianet에서 운영하는 Azure를 사용하려는 경우 **Active Set**(활성 설정) 드롭다운 목록에서 **windowsazure.cn(중국)**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="fbede-113">개인 Azure 플랫폼을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="fbede-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="fbede-114">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="fbede-115">대화 상자가 열리면서 **서비스 끝점** 대화 상자가 닫히고 기본 설정 집합 파일이 열린다고 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="fbede-116">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-116">Click **OK**.</span></span>

  3. <span data-ttu-id="fbede-117">Preferencesets.xml 파일에 새 `preferenceset` 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="fbede-118">이 새 요소에 대해 `name`, `blob`, `management`, `portalURL` 및 `publishsettings` 특성을 만들고 개인 Azure 플랫폼에 해당하는 특성 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="fbede-119">기존 `preferenceset` 요소에 대해 제공되는 값을 템플릿으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="fbede-120">**참고**: `blob` 특성에 사용되는 값에는 URL에 "blob" 텍스트가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="fbede-121">preferencesets.xml을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="fbede-122">**서비스 끝점** 대화 상자를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="fbede-123">**활성 설정** 드롭다운 목록에서 만들어진 활성 설정을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="fbede-124">개인 Azure 플랫폼 `preferenceset` 요소를 만들면 **서비스 끝점** 대화 상자의 **편집** 단추를 클릭하여 요소에 할당된 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="fbede-125">또한 원하는 경우 여러 개인 Azure 플랫폼 `preferenceset` 요소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbede-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="fbede-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fbede-126">See Also</span></span>
<span data-ttu-id="fbede-127">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fbede-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="fbede-128">[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fbede-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="fbede-129">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fbede-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="fbede-130">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbede-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
