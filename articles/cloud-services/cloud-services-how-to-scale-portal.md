---
title: "aaaAuto hello 포털에서 클라우드 서비스의 크기를 조정 | Microsoft Docs"
description: "어떻게 toouse hello는 클라우드 서비스 웹 역할 또는 작업자 역할에서 Azure에 대 한 포털 tooconfigure 자동 크기 조정 규칙에 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="3c48b-103">Tooconfigure 자동 hello 포털에서 클라우드 서비스에 대 한 크기 조정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c48b-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c48b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3c48b-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="3c48b-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="3c48b-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="3c48b-106">규모 감축 또는 규모 확장 작업을 트리거하는 클라우드 서비스 작업자 역할에 대해 조건을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="3c48b-107">hello 역할에 대 한 hello 조건은 hello CPU, 디스크 또는 hello 역할의 네트워크 부하를 기반으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="3c48b-108">구독과 관련 된 일부 다른 Azure 리소스로의 메시지 큐 또는 hello 메트릭을 기반 조건을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3c48b-109">이 문서에서는 클라우드 서비스 웹 및 작업자 역할에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="3c48b-110">가상 컴퓨터(클래식)를 직접 만든 경우 이 가상 컴퓨터는 클라우드 서비스에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="3c48b-111">표준 가상 컴퓨터를 [가용성 집합](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에 연결하여 규모를 조정하고 수동으로 켜거나 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="3c48b-112">고려 사항</span><span class="sxs-lookup"><span data-stu-id="3c48b-112">Considerations</span></span>
<span data-ttu-id="3c48b-113">Hello 응용 프로그램에 대해 크기 조정을 구성 하기 전에 다음 정보를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="3c48b-114">크기 조정은 코어 사용량의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="3c48b-115">역할 인스턴스가 클수록 더 많은 코어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-115">Larger role instances use more cores.</span></span> <span data-ttu-id="3c48b-116">구독에 대 한 hello 코어 한도 내 에서만 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="3c48b-117">예를 들어 구독의 코어 제한이 20이라고 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="3c48b-118">두 개의 중간 규모의 클라우드 서비스 (총 4 코어)와 응용 프로그램을 실행 하는 경우만 여 확장할 수 있습니다 다른 클라우드 서비스 배포를 구독에서 hello 나머지 코어 16 개.</span><span class="sxs-lookup"><span data-stu-id="3c48b-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="3c48b-119">크기에 대한 자세한 내용은 [클라우드 서비스 크기](cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c48b-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="3c48b-120">큐 메시지 임계값에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="3c48b-121">방법에 대 한 자세한 내용은 toouse 큐 참조 [어떻게 toouse hello 큐 저장소 서비스](../storage/queues/storage-dotnet-how-to-use-queues.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="3c48b-122">구독에 연결된 다른 리소스의 크기도 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="3c48b-123">응용 프로그램의 고가용성을 tooenable을 확인 해야 두 개 이상의 역할 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="3c48b-124">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c48b-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="3c48b-125">크기 조정 기능이 제공되는 위치</span><span class="sxs-lookup"><span data-stu-id="3c48b-125">Where scale is located</span></span>
<span data-ttu-id="3c48b-126">클라우드 서비스를 선택한 후에 hello 클라우드 서비스 블레이드 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="3c48b-127">Hello, hello 클라우드 서비스 블레이드의 **역할 및 인스턴스** 타일, 선택 hello hello 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="3c48b-128">**중요 한**: 있는지 tooclick hello 클라우드 서비스 역할, 하지 hello 역할 아래에 있는 역할 인스턴스를 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="3c48b-129">선택 hello **배율** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="3c48b-130">자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="3c48b-130">Automatic scale</span></span>
<span data-ttu-id="3c48b-131">**수동** 또는 **자동**의 두 가지 모드 중 하나를 사용하여 역할에 대한 크기 조정 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="3c48b-132">설명서가 예상 대로 인스턴스의 hello 절대 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="3c48b-133">그러나 자동은 규칙을 제어 하는 방법과 방법 훨씬 있습니다 조정 해야 tooset을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="3c48b-134">집합 hello **하 여 확장할** 옵션**일정 및 성능 규칙이**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![프로필 및 규칙을 사용하는 클라우드 서비스 크기 조정 설정](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="3c48b-136">기존 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-136">An existing profile.</span></span>
2. <span data-ttu-id="3c48b-137">Hello 부모 프로필에 대 한 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="3c48b-138">다른 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-138">Add another profile.</span></span>

<span data-ttu-id="3c48b-139">**프로필 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-139">Select **Add Profile**.</span></span> <span data-ttu-id="3c48b-140">hello 프로필에 따라 결정 하는 모드 toouse hello 눈금에 대 한 원하는: **항상**, **되풀이**, **고정 날짜**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="3c48b-141">Hello 프로필 및 규칙을 구성 하 고 나면 선택 hello **저장** hello 위쪽에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="3c48b-142">프로필</span><span class="sxs-lookup"><span data-stu-id="3c48b-142">Profile</span></span>
<span data-ttu-id="3c48b-143">hello 프로 파일 집합이 최소 및 최대 인스턴스 수 hello에 대 한 크기 조정와이 눈금 범위 활성화 된도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="3c48b-144">**항상**</span><span class="sxs-lookup"><span data-stu-id="3c48b-144">**Always**</span></span>

    <span data-ttu-id="3c48b-145">항상은 이 범위의 인스턴스를 항상 사용 가능하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-145">Always keep this range of instances available.</span></span>  

    ![항상 크기를 조정하는 클라우드 서비스](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="3c48b-147">**되풀이**</span><span class="sxs-lookup"><span data-stu-id="3c48b-147">**Recurrence**</span></span>

    <span data-ttu-id="3c48b-148">Hello 주 tooscale의 일 집합을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-148">Choose a set of days of hello week tooscale.</span></span>

    ![되풀이 일정을 사용하는 클라우드 서비스 크기 조정](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="3c48b-150">**고정 날짜**</span><span class="sxs-lookup"><span data-stu-id="3c48b-150">**Fixed Date**</span></span>

    <span data-ttu-id="3c48b-151">고정된 날짜 범위 tooscale hello 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-151">A fixed date range tooscale hello role.</span></span>

    ![고정 날짜를 사용하는 클라우드 서비스 크기 조정](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="3c48b-153">Hello 프로필을 구성 하 고 나면 선택 hello **확인** hello hello 프로필 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="3c48b-154">규칙</span><span class="sxs-lookup"><span data-stu-id="3c48b-154">Rule</span></span>
<span data-ttu-id="3c48b-155">Tooa 프로필을 추가 하는 규칙과 hello 눈금을 트리거하는 조건을 나타내는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="3c48b-156">hello 규칙 트리거는 hello 클라우드 서비스 (CPU 사용량, 디스크 작업 또는 네트워크 활동)의 메트릭을 기반 toowhich 조건 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="3c48b-157">또한 구독에 연결 된 일부 다른 Azure 리소스로의 메시지 큐 또는 hello 메트릭을 기반 hello 트리거를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="3c48b-158">Hello 규칙을 구성 하 고 나면 선택 hello **확인** hello hello 규칙 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="3c48b-159">뒤로 toomanual 배율</span><span class="sxs-lookup"><span data-stu-id="3c48b-159">Back toomanual scale</span></span>
<span data-ttu-id="3c48b-160">Toohello 이동 [배율 설정을](#where-scale-is-located) 및 집합 hello **하 여 확장할** 옵션**수동으로 입력 한 인스턴스 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![프로필 및 규칙을 사용하는 클라우드 서비스 크기 조정 설정](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="3c48b-162">이 설정은 hello 역할에서 자동화 된 확장을 제거 하 고 다시 hello 인스턴스 수를 직접 설정할 수 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="3c48b-163">hello (수동 또는 자동) 크기 조정 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="3c48b-164">역할 인스턴스 슬라이더 tooset hello를 tooscale를 인스턴스에입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="3c48b-165">hello 역할 tooscale의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="3c48b-166">Hello 크기 조정 설정을 구성한 경우 선택 hello **저장** hello 위쪽에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3c48b-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
