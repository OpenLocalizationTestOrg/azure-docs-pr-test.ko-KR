---
title: "Azure Active Directory Domain Services: 가상 네트워크 만들기 또는 선택 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="8ab7d-103">Azure Active Directory Domain Services의 가상 네트워크 만들기 또는 선택</span><span class="sxs-lookup"><span data-stu-id="8ab7d-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="8ab7d-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8ab7d-104">Before you begin</span></span>
<span data-ttu-id="8ab7d-105">너무 참조[Azure Active Directory 도메인 서비스에 대 한 네트워킹 고려 사항](active-directory-ds-networking.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="8ab7d-106">작업 2: Azure 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab7d-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="8ab7d-107">다음 구성 작업 hello는 Azure 가상 네트워크 및 그 안에 서브넷이 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="8ab7d-108">가상 네트워크 내의 이 서브넷에서 Azure Active Directory Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="8ab7d-109">기존 가상 네트워크는 편이 더 toouse를 설정한 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab7d-110">Azure 가상 네트워크를 만들거나 Azure Active Directory 도메인 서비스와 toouse 속한 tooan Azure Active Directory 도메인 서비스에서 지원 되는 Azure 지역 선택 해당 hello 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="8ab7d-111">tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="8ab7d-112">후속 구성 단계에서 Azure Active Directory 도메인 서비스를 사용 하도록 설정 하면 hello 오른쪽 가상 네트워크를 선택 하면 hello 가상 네트워크 tooensure의 참고 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="8ab7d-113">toocreate tooenable Azure Active Directory 도메인 서비스를 원하는 Azure 가상 네트워크는 이러한 구성 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="8ab7d-114">Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8ab7d-115">Hello 왼쪽된 창에서 선택 **네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="8ab7d-116">![Networks 노드](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="8ab7d-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="8ab7d-117">hello **가상 네트워크** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="8ab7d-118">Hello hello hello 창 맨 아래에 작업 창에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Virtual Networks 창](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="8ab7d-120">**Network Services**를 클릭한 다음 **Virtual Network**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![가상 네트워크 - 빠른 생성](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="8ab7d-122">가상 네트워크 toocreate 클릭 **빠른 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="8ab7d-123">지정는 **이름** 가상에 대 한 네트워크, 및 hello 다음을 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="8ab7d-124">Tooconfigure를 선택할 수 있습니다 **주소 공간** 또는 **최대 VM 수** 이 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="8ab7d-125">Hello에 두면 **DNS 서버** 로 설정 **없음** 지금은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="8ab7d-126">Azure Active Directory 도메인 서비스를 사용 하도록 설정한 후 hello 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="8ab7d-127">Hello에 **위치** 드롭 다운 목록에서 지원 되는 Azure 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="8ab7d-128">tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="8ab7d-129">toocreate 가상 네트워크가 클릭 **가상 네트워크 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Azure Active Directory Domain Services의 가상 네트워크 만들기](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="8ab7d-131">가상 네트워크를 만든 후 hello 가상 네트워크의 hello 이름을 선택 하 고 클릭 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="8ab7d-133">**가상 네트워크 주소 공간**, 클릭 **서브넷을 추가**, 다음 hello 이름의 서브넷을 지정 하 고 **AaddsSubnet**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Azure Active Directory Domain Services의 서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="8ab7d-135">toocreate 서브넷 hello, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab7d-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="8ab7d-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ab7d-136">Next step</span></span>
[<span data-ttu-id="8ab7d-137">작업 3: Azure Active Directory Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="8ab7d-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
