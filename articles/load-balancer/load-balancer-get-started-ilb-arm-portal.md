---
title: "내부 부하 분산 장치 만들기 - Azure Portal | Microsoft Docs"
description: "Azure 포털을 사용하여 Resource Manager에서 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="604f0-103">Azure Portal에서 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="604f0-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="604f0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="604f0-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="604f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="604f0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="604f0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="604f0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="604f0-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="604f0-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="604f0-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="604f0-109">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="604f0-110">Azure 포털을 사용하여 내부 부하 분산 장치 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="604f0-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="604f0-111">Azure Portal에서 내부 부하 분산 장치를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="604f0-112">브라우저를 열고 [Azure Portal](http://portal.azure.com)로 이동하여 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="604f0-113">화면 왼쪽 상단에서 **새로 만들기** > **네트워킹** > **부하 분산 장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="604f0-114">**부하 분산 장치 만들기** 블레이드에서 부하 분산 장치의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="604f0-115">**구성표**에서 **내부**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="604f0-116">**가상 네트워크**를 클릭한 다음 부하 분산 장치를 만들 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="604f0-117">사용하려는 가상 네트워크가 보이지 않으면 부하 분산 장치에 대해 사용 중인 **위치** 를 확인하고 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="604f0-118">**서브넷**을 클릭한 다음 부하 분산 장치를 만들 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="604f0-119">**IP 주소 할당**에서 부하 분산 장치의 IP 주소를 고정으로 할 것인지 유동으로 할 것인지에 따라 **동적** 또는 **고정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="604f0-120">고정 IP 주소를 사용하도록 선택하는 경우 부하 분산 장치에 대한 주소를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="604f0-121">**리소스 그룹**에서 부하 분산 장치에 대한 새 리소스 그룹의 이름을 지정하거나 **기존 항목 선택**을 클릭하여 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="604f0-122">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="604f0-123">부하 분산 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-123">Configure load balancing rules</span></span>

<span data-ttu-id="604f0-124">부하 분산 장치를 만든 후 구성을 위해 부하 분산 장치 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="604f0-125">백 엔드 주소 풀 및 프로브를 먼저 구성한 후 부하 분산 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="604f0-126">1단계: 백 엔드 풀 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="604f0-127">Azure Portal에서 **찾아보기** > **부하 분산 장치**를 클릭한 다음 위에서 만든 부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="604f0-128">**설정** 블레이드에서 **백 엔드 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="604f0-129">**백 엔드 주소 풀** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="604f0-130">**백 엔드 풀 추가** 블레이드에서 백 엔드 풀에 대한 **이름**을 입력한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="604f0-131">2단계: 프로브 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="604f0-132">Azure Portal에서 **찾아보기** > **부하 분산 장치**를 클릭한 다음 위에서 만든 부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="604f0-133">**설정** 블레이드에서 **프로브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="604f0-134">**프로브** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="604f0-135">**프로브 추가** 블레이드에서 프로브에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="604f0-136">**프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="604f0-137">**포트**아래에서 프로브에 액세스할 때 사용할 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="604f0-138">**경로** (HTTP 프로브 전용) 아래에서 프로브로 사용할 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="604f0-139">**간격** 아래에서 응용 프로그램 검색 빈도를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="604f0-140">**비정상 임계값**에서 백 엔드 가상 컴퓨터를 비정상으로 표시하기 전에 실패하는 시도 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="604f0-141">**확인** 을 클릭하여 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="604f0-142">3단계: 부하 분산 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="604f0-143">Azure Portal에서 **찾아보기** > **부하 분산 장치**를 클릭한 다음 위에서 만든 부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="604f0-144">**설정** 블레이드에서 **부하 분산 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="604f0-145">**부하 분산 규칙** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="604f0-146">**부하 분산 규칙 추가** 블레이드에서 규칙에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="604f0-147">**프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="604f0-148">**포트**에서 클라이언트가 부하 분산 장치에 연결할 때 사용할 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="604f0-149">**백 엔드 포트**에서 백 엔드 풀에 사용할 포트를 지정합니다. 일반적으로 부하 분산 장치 포트 및 백 엔드 포트는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="604f0-150">**백 엔드 풀**아래에서 위에서 만든 백 엔드 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="604f0-151">**세션 지속성**아래에서 세션을 얼마나 지속할 것인지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="604f0-152">**유휴 시간 제한(분)**아래에서 유휴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="604f0-153">**부동 IP(Direct Server Return(DSR))**에서 **사용 안 함** 또는 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="604f0-154">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604f0-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="604f0-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="604f0-155">Next steps</span></span>

[<span data-ttu-id="604f0-156">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="604f0-157">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="604f0-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

