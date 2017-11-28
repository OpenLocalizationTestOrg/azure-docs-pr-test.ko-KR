---
title: "Windows PowerShell에서 Azure 클라우드 서비스 aaaScale | Microsoft Docs"
description: "(클래식) 자세한 내용은 방법 toouse PowerShell tooscale 웹 역할 또는 작업자 역할에서 또는 Azure에서 축소 합니다."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="6d4ac-103">PowerShell에서 tooscale는 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6d4ac-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="6d4ac-104">추가 하거나 제거 하 여 웹 역할 또는 작업자 역할 또는 Windows PowerShell tooscale를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="6d4ac-105">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="6d4ac-105">Log in tooAzure</span></span>

<span data-ttu-id="6d4ac-106">PowerShell을 통해 구독에 대한 작업을 수행하려면 먼저 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="6d4ac-107">구독이 여러 개인 사용자 계정과 연결 된 클라우드 서비스가 있는 위치에 따라 toochange hello 현재 구독을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="6d4ac-108">실행 toocheck hello 현재 구독:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="6d4ac-109">Toochange hello 현재 구독 해야 할 경우 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="6d4ac-110">사용자 역할에 대 한 hello 현재 인스턴스 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="6d4ac-111">사용자 역할의 toocheck hello 현재 상태를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="6d4ac-112">현재 OS 버전 및 인스턴스 수를 포함 하는 hello 역할에 대 한 정보 되돌려야.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="6d4ac-113">이 경우 hello 역할에 인스턴스가 하나일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-113">In this case, hello role has a single instance.</span></span>

![Hello 역할에 대 한 정보](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="6d4ac-115">더 많은 인스턴스를 추가 하 여 hello 역할 확장</span><span class="sxs-lookup"><span data-stu-id="6d4ac-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="6d4ac-116">사용자의 역할 아웃 tooscale, 패스 hello hello로 인스턴스 수를 원하는 대로 **Count** 매개 변수 toohello **집합 AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="6d4ac-117">hello cmdlet 블록 hello 새 인스턴스는 동안 일시적으로 프로 비전 하 고 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="6d4ac-118">새 PowerShell 창 및 호출을 여는 경우이 시간 동안 **Get-azurerole** hello 새 대상 인스턴스 개수에서 설명한 것 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="6d4ac-119">고 hello 새 인스턴스를 시작 hello 포털에서 hello 역할 상태를 검사 하는 경우 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![포털에서 시작 중인 VM 인스턴스](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="6d4ac-121">Hello 새 인스턴스를 시작 되 면 hello cmdlet이 성공적으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![역할 인스턴스 증가 성공](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="6d4ac-123">인스턴스를 제거 하 여 hello 역할의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6d4ac-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="6d4ac-124">Hello에 인스턴스를 제거 하 여 역할에 확장할 수 같은 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="6d4ac-125">집합 hello **개수** 매개 변수와 **집합 AzureRole** toohello 수 인스턴스의 원하는 toohave hello 크기 조정 작업에서 완료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d4ac-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d4ac-126">Next steps</span></span>

<span data-ttu-id="6d4ac-127">PowerShell에서 클라우드 서비스에 대 한 가능한 tooconfigure 자동 단위는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="6d4ac-128">참조 하는 toodo [tooauto 클라우드 서비스를 확장 하는 방법을](cloud-services-how-to-scale-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
