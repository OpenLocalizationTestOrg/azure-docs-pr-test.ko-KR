---
title: "Azure Active Directory Domain Services: 시작 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정"
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
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="9f783-103">Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9f783-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="9f783-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9f783-104">Before you begin</span></span>
<span data-ttu-id="9f783-105">너무 참조[Azure Active Directory 도메인 서비스에 대 한 네트워킹 고려 사항](active-directory-ds-networking.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="9f783-106">작업 2: 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="9f783-106">Task 2: configure network settings</span></span>
<span data-ttu-id="9f783-107">다음 구성 작업 hello는 Azure 가상 네트워크 및 그 안에 전용된 서브넷이 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="9f783-108">가상 네트워크 내의 이 서브넷에서 Azure Active Directory Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="9f783-109">기존 가상 네트워크를 선택 및 그 안에 hello 전용 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="9f783-110">클릭 **가상 네트워크** tooselect 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="9f783-111">Hello에 **가상 네트워크 선택** 블레이드에서 모든 기존 가상 네트워크를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9f783-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="9f783-112">Hello 가상 네트워크만 toohello 리소스 그룹 및 Azure 위치 hello에서 선택한 속하는 참조 **기본 사항** 마법사 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="9f783-113">Azure AD 도메인 서비스를 활성화 해야 하는 hello 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="9f783-114">클릭 **새로 만들기**toocreate 새 가상 네트워크를 선호 하는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="9f783-115">Azure AD Domain Services에 전용 서브넷을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="9f783-116">기존 가상 네트워크를 선택 하면 [hello 가상 네트워크 확장을 사용 하는 전용된 서브넷을 만든](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 한 다음 해당 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![가상 네트워크 선택](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="9f783-118">클릭 **서브넷** toopick hello 어떤 tooenable 내에서 새 관리 되는 도메인을이 가상 네트워크에 전용된 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="9f783-119">Hello에 **서브넷을 만든** 블레이드에서 hello 서브넷에 대 한 이름을 지정 하 고 클릭 **확인** 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="9f783-120">예를 들어 hello 이름의 쉽게 다른 관리자가 toounderstand는 배포 된 hello 서브넷 내에서 ' DomainServices' 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Hello 가상 네트워크 내에서 서브넷을 선택 합니다.](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="9f783-122">**서브넷 선택 지침**</span><span class="sxs-lookup"><span data-stu-id="9f783-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="9f783-123">Azure AD Domain Services에 전용 서브넷을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="9f783-124">가상 컴퓨터의 toothis 서브넷을 배포 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9f783-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="9f783-125">이 구성을 사용 하면 (Nsg) tooconfigure 네트워크 보안 그룹 작업/가상 컴퓨터에 대해 관리 되는 도메인을 방해 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="9f783-126">자세한 내용은 [Azure Active Directory Domain Services의 네트워킹 고려 사항](active-directory-ds-networking.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f783-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="9f783-127">지원 되는 구성 없기 때문에 Azure AD 도메인 서비스 배포를 위한 hello 게이트웨이 서브넷을 선택 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9f783-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="9f783-128">선택한 hello 서브넷에 충분 한 사용 가능한 주소 공간이-3-5 이상 사용 가능한 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="9f783-129">완료 되 면 클릭 **확인** toohello에 toomove **관리자 그룹** hello 마법사의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9f783-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="9f783-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f783-130">Next step</span></span>
[<span data-ttu-id="9f783-131">작업 3: 관리 그룹 구성 및 Azure AD Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="9f783-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
