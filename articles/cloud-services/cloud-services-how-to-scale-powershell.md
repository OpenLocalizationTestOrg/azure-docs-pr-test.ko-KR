---
title: "Windows PowerShell에서 Azure 클라우드 서비스 크기 조정 | Microsoft Docs"
description: "(클래식) PowerShell을 사용하여 Azure에서 웹 역할 또는 작업자 역할을 축소 또는 확장하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="e96e8-103">PowerShell에서 클라우드 서비스 크기를 조정하는 방법</span><span class="sxs-lookup"><span data-stu-id="e96e8-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="e96e8-104">Windows PowerShell을 사용하여 인스턴스를 추가하거나 제거함으로써 웹 역할 또는 작업자 역할을 축소하거나 확대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="e96e8-105">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="e96e8-105">Log in to Azure</span></span>

<span data-ttu-id="e96e8-106">PowerShell을 통해 구독에 대한 작업을 수행하려면 먼저 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="e96e8-107">계정에 연결된 구독이 여러 개인 경우 클라우드 서비스가 상주하는 위치에 따라 현재 구독을 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="e96e8-108">현재 구독을 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="e96e8-109">현재 구독을 변경해야 할 경우 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="e96e8-110">역할에 대한 현재 인스턴스 수 확인</span><span class="sxs-lookup"><span data-stu-id="e96e8-110">Check the current instance count for your role</span></span>

<span data-ttu-id="e96e8-111">사용자 역할의 현재 상태를 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="e96e8-112">현재 해당 OS 버전 및 인스턴스 수를 포함하여 역할에 대한 정보를 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="e96e8-113">아래의 경우 역할은 단일 인스턴스를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-113">In this case, the role has a single instance.</span></span>

![역할에 대한 정보](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="e96e8-115">인스턴스를 더 추가하여 역할 확장</span><span class="sxs-lookup"><span data-stu-id="e96e8-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="e96e8-116">역할을 확장하려면 **Set-AzureRole** cmdlet에 **Count** 매개 변수로 원하는 인스턴스 수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="e96e8-117">새 인스턴스가 프로비전되고 시작되는 동안 cmdlet은 일시적으로 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="e96e8-118">이 시간 동안 새 PowerShell 창을 열고 앞에 표시된 대로 **Get-AzureRole**을 호출하면 새 대상 인스턴스의 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="e96e8-119">그리고 포털에서 역할 상태를 검사하면 새 인스턴스가 시작 중임이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![포털에서 시작 중인 VM 인스턴스](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="e96e8-121">새 인스턴스가 시작되면 cmdlet이 다음과 같이 성공적으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![역할 인스턴스 증가 성공](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="e96e8-123">인스턴스를 제거하여 역할 축소</span><span class="sxs-lookup"><span data-stu-id="e96e8-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="e96e8-124">같은 방식으로 인스턴스를 제거하여 역할을 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="e96e8-125">**Set-AzureRole**에서 **Count** 매개 변수를 축소 작업이 완료된 후의 원하는 인스턴스 수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e96e8-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e96e8-126">Next steps</span></span>

<span data-ttu-id="e96e8-127">PowerShell에서 Cloud Services에 대한 자동 크기 조정을 구성하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e96e8-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="e96e8-128">자동 크기 조정은 [클라우드 서비스 크기를 자동으로 조정하는 방법](cloud-services-how-to-scale-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e96e8-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
