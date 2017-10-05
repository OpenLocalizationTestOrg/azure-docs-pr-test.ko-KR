---
title: "Azure Active Directory Domain Services: 가상 네트워크 만들기 또는 선택 | Microsoft Docs"
description: "Azure 클래식 포털을 사용하여 Azure Active Directory Domain Services 활성화"
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
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="f9149-103">Azure Active Directory Domain Services의 가상 네트워크 만들기 또는 선택</span><span class="sxs-lookup"><span data-stu-id="f9149-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="f9149-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f9149-104">Before you begin</span></span>
<span data-ttu-id="f9149-105">[Azure Active Directory Domain Services의 네트워킹 고려 사항](active-directory-ds-networking.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9149-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="f9149-106">작업 2: Azure 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f9149-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="f9149-107">다음 구성 작업은 Azure Virtual Network를 만들고 그 안에 서브넷을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="f9149-108">가상 네트워크 내의 이 서브넷에서 Azure Active Directory Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="f9149-109">기존 가상 네트워크를 사용하려는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="f9149-110">Azure Active Directory Domain Services와 함께 사용하도록 만들거나 선택하는 Azure 가상 네트워크가 Azure Active Directory Domain Services에서 지원하는 Azure 지역에 속하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f9149-111">Azure Active Directory Domain Services를 사용할 수 있는 Azure 지역을 확인하려면 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9149-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="f9149-112">후속 구성 단계에서 Azure Active Directory Domain Services를 사용하도록 설정할 때 올바른 가상 네트워크를 선택할 수 있도록 가상 네트워크의 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="f9149-113">Azure Active Directory Domain Services를 사용하려는 Azure 가상 네트워크를 만들려면 다음 구성 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="f9149-114">[Azure 클래식 포털](https://manage.windowsazure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f9149-115">왼쪽 창에서 **Networks**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="f9149-116">![Networks 노드](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="f9149-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="f9149-117">**Virtual Networks** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="f9149-118">페이지 아래쪽의 작업 창에서 **새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Virtual Networks 창](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="f9149-120">**Network Services**를 클릭한 다음 **Virtual Network**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![가상 네트워크 - 빠른 생성](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="f9149-122">가상 네트워크를 만들려면 **빨리 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="f9149-123">가상 네트워크에 대해 **이름**을 지정하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="f9149-124">이 네트워크에 대해 **주소 공간** 또는 **최대 VM 수**를 구성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="f9149-125">지금은 **DNS 서버** 설정을 **없음**으로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="f9149-126">DNS 서버 설정은 Azure Active Directory Domain Services를 사용하도록 설정한 후에 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="f9149-127">**위치** 드롭다운에서 지원되는 Azure 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="f9149-128">Azure Active Directory Domain Services를 사용할 수 있는 Azure 지역을 확인하려면 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9149-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="f9149-129">가상 네트워크를 만들려면 **Virtual Network 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Azure Active Directory Domain Services의 가상 네트워크 만들기](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="f9149-131">가상 네트워크를 만든 후 가상 네트워크의 이름을 선택한 다음 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="f9149-133">**가상 네트워크 주소 공간**에서 **서브넷 추가**를 클릭한 다음 **AaddsSubnet**이라는 이름으로 서브넷을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Azure Active Directory Domain Services의 서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="f9149-135">서브넷을 만들려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9149-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="f9149-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9149-136">Next step</span></span>
[<span data-ttu-id="f9149-137">작업 3: Azure Active Directory Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="f9149-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
