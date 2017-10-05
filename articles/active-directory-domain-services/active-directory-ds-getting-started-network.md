---
title: "Azure Active Directory Domain Services: 시작 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화(미리 보기)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="b1b01-103">Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="b1b01-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="b1b01-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b1b01-104">Before you begin</span></span>
<span data-ttu-id="b1b01-105">[Azure Active Directory Domain Services의 네트워킹 고려 사항](active-directory-ds-networking.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b01-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="b1b01-106">작업 2: 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b1b01-106">Task 2: configure network settings</span></span>
<span data-ttu-id="b1b01-107">다음 구성 작업은 Azure 가상 네트워크를 만들고 그 안에 전용 서브넷을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="b1b01-108">가상 네트워크 내의 이 서브넷에서 Azure Active Directory Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="b1b01-109">기존 가상 네트워크를 선택하고 그 안에 전용 서브넷을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="b1b01-110">**가상 네트워크**를 클릭하여 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="b1b01-111">**가상 네트워크 선택** 블레이드에서 기존 가상 네트워크를 모두 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="b1b01-112">리소스 그룹에 속한 가상 네트워크 및 **기본 사항** 마법사 페이지에서 선택한 Azure 위치만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="b1b01-113">Azure AD Domain Services를 사용하도록 설정해야 하는 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="b1b01-114">새 가상 네트워크를 만들려는 경우 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="b1b01-115">Azure AD Domain Services에 전용 서브넷을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b1b01-116">기존 가상 네트워크를 선택하면 [가상 네트워크 확장을 사용하여 전용 서브넷을 만든](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 다음 해당 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![가상 네트워크 선택](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="b1b01-118">**서브넷**을 클릭하여 이 가상 네트워크에서 새 관리되는 도메인을 사용하도록 설정할 전용 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="b1b01-119">**서브넷 만들기** 블레이드에서 서브넷 이름을 지정하고 완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="b1b01-120">예를 들어 이름이 'DomainServices'인 서브넷을 만들어 다른 관리자가 서브넷에 배포된 항목을 이해하기 쉽게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![가상 네트워크 내에서 서브넷 선택](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="b1b01-122">**서브넷 선택 지침**</span><span class="sxs-lookup"><span data-stu-id="b1b01-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="b1b01-123">Azure AD Domain Services에 전용 서브넷을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="b1b01-124">이 서브넷에 다른 가상 컴퓨터를 배포하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="b1b01-125">이 구성을 사용하면 관리되는 도메인을 방해하지 않고 워크로드/가상 컴퓨터에 대해 NSG(네트워크 보안 그룹)을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="b1b01-126">자세한 내용은 [Azure Active Directory Domain Services의 네트워킹 고려 사항](active-directory-ds-networking.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b01-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="b1b01-127">Azure AD Domain Services 배포를 위해 게이트웨이 서브넷을 선택하지 마세요. 이 서브넷에는 지원되는 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="b1b01-128">선택한 서브넷에 사용 가능한 주소 공간이 충분한지 확인합니다(3-5개 이상의 사용 가능한 IP 주소).</span><span class="sxs-lookup"><span data-stu-id="b1b01-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="b1b01-129">완료되면 **확인**을 클릭하여 마법사의 **관리자 그룹** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b01-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="b1b01-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1b01-130">Next step</span></span>
[<span data-ttu-id="b1b01-131">작업 3: 관리 그룹 구성 및 Azure AD Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="b1b01-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
