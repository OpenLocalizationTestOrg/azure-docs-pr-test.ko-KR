---
title: "aaaCreate는 내부 부하 분산 장치-Azure 포털 | Microsoft Docs"
description: "어떻게 toocreate는 내부 부하 분산 장치 hello Azure 포털을 사용 하 여 리소스 관리자에 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="5c3ef-103">Hello Azure 포털에에서는 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="5c3ef-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c3ef-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5c3ef-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="5c3ef-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c3ef-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="5c3ef-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5c3ef-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="5c3ef-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="5c3ef-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5c3ef-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="5c3ef-109">사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="5c3ef-110">Azure 포털을 사용하여 내부 부하 분산 장치 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="5c3ef-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="5c3ef-111">Hello 단계 toocreate 내부 부하 분산 장치는 hello Azure 포털에서에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="5c3ef-112">브라우저를 열고 탐색 toohello [Azure 포털](http://portal.azure.com), Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="5c3ef-113">Hello hello 화면의 왼쪽 위 측면, 클릭 **새로** > **네트워킹** > **부하 분산 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="5c3ef-114">Hello에 **부하 분산 장치 만들기** 블레이드를 입력 한 **이름** 부하 분산 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="5c3ef-115">**구성표**에서 **내부**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="5c3ef-116">클릭 **가상 네트워크**을 다음 선택 hello toocreate hello에 대 한 부하 분산 장치를 원하는 가상 네트워크 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c3ef-117">Hello 가상 네트워크 toouse를 원하는 경우 확인 hello **위치** hello 부하 분산을 사용 하 고 적절 하 게 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="5c3ef-118">클릭 **서브넷**, 한 다음 toocreate hello에 대 한 부하 분산 장치를 원하는 hello 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="5c3ef-119">아래 **IP 주소 할당**, 클릭 **동적** 또는 **정적**여부 hello IP 주소에 대해 원하는 hello 부하 분산 장치 toobe 고정 (정적) 여부에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c3ef-120">Toouse 고정 IP 주소를 선택 해야 합니다 tooprovide hello 부하 분산 장치에 대 한 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="5c3ef-121">아래 **리소스 그룹** hello 부하 분산 장치에 대 한 새 리소스 그룹의 hello 이름을 지정 하거나 클릭 **기존 선택** 기존 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="5c3ef-122">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="5c3ef-123">부하 분산 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-123">Configure load balancing rules</span></span>

<span data-ttu-id="5c3ef-124">Hello 후 부하 분산 장치 만들기, 이동 toohello 부하 분산 장치 리소스 tooconfigure 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="5c3ef-125">Tooconfigure 먼저 백 엔드 주소 풀 및 필요에 검색 부하 분산 규칙을 구성 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="5c3ef-126">1단계: 백 엔드 풀 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="5c3ef-127">Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5c3ef-128">Hello에 **설정** 블레이드에서 클릭 **백 엔드 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="5c3ef-129">Hello에 **백 엔드 주소 풀** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="5c3ef-130">Hello에 **백 엔드 풀 추가** 블레이드를 입력 한 **이름** hello 백 엔드 풀 및 클릭 한 다음에 대 한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="5c3ef-131">2단계: 프로브 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="5c3ef-132">Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5c3ef-133">Hello에 **설정** 블레이드에서 클릭 **프로브**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="5c3ef-134">Hello에 **프로브** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="5c3ef-135">Hello에 **추가 프로브** 블레이드를 입력 한 **이름** hello 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="5c3ef-136">**프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="5c3ef-137">아래 **포트**, hello 프로브에 액세스할 때 hello 포트 toouse를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="5c3ef-138">아래 **경로** (프로브에 대해 HTTP만), hello 경로 toouse에 검색으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="5c3ef-139">아래 **간격** 얼마나 자주 tooprobe hello 응용 프로그램을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="5c3ef-140">아래 **비정상 임계값**, hello 백 엔드 가상 컴퓨터를 비정상으로 표시 되기 전에 개수 시도가 실패 하는지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="5c3ef-141">클릭 **확인** toocreate 프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="5c3ef-142">3단계: 부하 분산 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="5c3ef-143">Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5c3ef-144">Hello에 **설정** 블레이드에서 클릭 **부하 분산 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="5c3ef-145">Hello에 **부하 분산 규칙** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="5c3ef-146">Hello에 **추가 부하 분산 규칙** 블레이드를 입력 한 **이름** hello 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="5c3ef-147">**프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="5c3ef-148">아래 **포트**, hello 포트 클라이언트가 tooin hello에 대 한 부하 분산 장치 연결을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="5c3ef-149">아래 **백 엔드 포트가**, hello 백 엔드 풀에서 사용 하는 hello 포트 toobe 지정 (일반적으로 hello 부하 분산 장치 포트와 백 엔드 포트가 hello는 hello 동일).</span><span class="sxs-lookup"><span data-stu-id="5c3ef-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="5c3ef-150">아래 **백 엔드 풀**선택, 위에서 만든 hello 백 엔드 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="5c3ef-151">아래 **세션 지 속성**세션 toopersist 원하는 방식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="5c3ef-152">아래 **유휴 시간 제한 (분)**, hello 유휴 시간 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="5c3ef-153">**부동 IP(Direct Server Return(DSR))**에서 **사용 안 함** 또는 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="5c3ef-154">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3ef-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c3ef-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c3ef-155">Next steps</span></span>

[<span data-ttu-id="5c3ef-156">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5c3ef-157">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="5c3ef-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

