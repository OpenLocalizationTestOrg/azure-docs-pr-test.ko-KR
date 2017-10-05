---
title: "사용자 지정 프로브 만들기 - Azure Application Gateway - Azure Portal | Microsoft Docs"
description: "포털을 사용하여 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브를 만드는 방법을 알아봅니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 65e9bba4ce9ac41ae2a9a8c3fa7f661165fc1403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-the-portal"></a><span data-ttu-id="7ef2a-103">포털을 사용하여 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="7ef2a-103">Create a custom probe for Application Gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ef2a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7ef2a-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="7ef2a-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ef2a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="7ef2a-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ef2a-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="7ef2a-107">이 문서에서는 Azure Portal을 통해 기존 응용 프로그램 게이트웨이에 사용자 지정 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-107">In this article, you add a custom probe to an existing application gateway through the Azure portal.</span></span> <span data-ttu-id="7ef2a-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용하는 응용 프로그램이나 기본 웹 응용 프로그램에서 성공적으로 응답을 제공하지 않는 응용 프로그램에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7ef2a-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7ef2a-109">Before you begin</span></span>

<span data-ttu-id="7ef2a-110">응용 프로그램 게이트웨이 아직 없는 경우 방문 [응용 프로그램 게이트웨이 만들기](application-gateway-create-gateway-portal.md)를 참조하여 사용할 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-110">If you do not already have an application gateway, visit [Create an Application Gateway](application-gateway-create-gateway-portal.md) to create an application gateway to work with.</span></span>

## <span data-ttu-id="7ef2a-111"><a name="createprobe"></a>프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="7ef2a-111"><a name="createprobe"></a>Create the probe</span></span>

<span data-ttu-id="7ef2a-112">프로브는 포털을 통해 두 단계 프로세스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-112">Probes are configured in a two-step process through the portal.</span></span> <span data-ttu-id="7ef2a-113">첫 번째 단계는 프로브를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-113">The first step is to create the probe.</span></span> <span data-ttu-id="7ef2a-114">두 번째 단계로 응용 프로그램 게이트웨이의 백 엔드 http 설정에 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-114">In the second step, you add the probe to the backend http settings of the application gateway.</span></span>

1. <span data-ttu-id="7ef2a-115">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-115">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7ef2a-116">아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-116">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>

1. <span data-ttu-id="7ef2a-117">Azure Portal의 [즐겨찾기] 창에서 [모든 리소스]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-117">In the Azure portal Favorites pane, click All resources.</span></span> <span data-ttu-id="7ef2a-118">[모든 리소스] 블레이드에서 응용 프로그램 게이트웨이를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-118">Click the application gateway in the All resources blade.</span></span> <span data-ttu-id="7ef2a-119">선택한 구독에 이미 여러 리소스가 있는 경우 [이름으로 필터링...]에서 partners.contoso.net을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-119">If the subscription you selected already has several resources in it, you can enter partners.contoso.net in the Filter by name…</span></span> <span data-ttu-id="7ef2a-120">응용 프로그램 게이트웨이에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-120">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="7ef2a-121">**프로브**를 클릭한 다음 **추가** 단추를 클릭하여 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-121">Click **Probes** and click the **Add** button to add a probe.</span></span>

  ![정보가 입력된 프로브 추가 블레이드][1]

1. <span data-ttu-id="7ef2a-123">**상태 프로브 추가** 블레이드에서 프로브에 필요한 정보를 입력하고, 완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-123">On the **Add health probe** blade, fill out the required information for the probe, and when complete click **OK**.</span></span>

  |<span data-ttu-id="7ef2a-124">**설정**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-124">**Setting**</span></span> | <span data-ttu-id="7ef2a-125">**값**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-125">**Value**</span></span> | <span data-ttu-id="7ef2a-126">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-126">**Details**</span></span>|
  |---|---|---|
  |<span data-ttu-id="7ef2a-127">**Name**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-127">**Name**</span></span>|<span data-ttu-id="7ef2a-128">customProbe</span><span class="sxs-lookup"><span data-stu-id="7ef2a-128">customProbe</span></span>|<span data-ttu-id="7ef2a-129">포털에서 액세스할 수 있는 프로브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-129">This value is a friendly name to the probe that is accessible in the portal.</span></span>|
  |<span data-ttu-id="7ef2a-130">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-130">**Protocol**</span></span>|<span data-ttu-id="7ef2a-131">HTTP 또는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="7ef2a-131">HTTP or HTTPS</span></span> | <span data-ttu-id="7ef2a-132">상태 프로브에서 사용하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-132">The protocol that the health probe uses.</span></span>|
  |<span data-ttu-id="7ef2a-133">**호스트**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-133">**Host**</span></span>|<span data-ttu-id="7ef2a-134">예:</span><span class="sxs-lookup"><span data-stu-id="7ef2a-134">i.e</span></span> <span data-ttu-id="7ef2a-135">contoso.com</span><span class="sxs-lookup"><span data-stu-id="7ef2a-135">contoso.com</span></span>|<span data-ttu-id="7ef2a-136">프로브에 사용되는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-136">This value is the host name that is used for the probe.</span></span> <span data-ttu-id="7ef2a-137">다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-137">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="7ef2a-138">이 값은 VM 호스트 이름과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-138">This value is different from the VM host name.</span></span>|
  |<span data-ttu-id="7ef2a-139">**Path**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-139">**Path**</span></span>|<span data-ttu-id="7ef2a-140">/ 또는 다른 경로</span><span class="sxs-lookup"><span data-stu-id="7ef2a-140">/ or another path</span></span>|<span data-ttu-id="7ef2a-141">사용자 지정 프로브의 전체 url 중 나머지 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-141">The remainder of the full url for the custom probe.</span></span> <span data-ttu-id="7ef2a-142">유효한 경로는 '/'로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-142">A valid path starts with '/'.</span></span> <span data-ttu-id="7ef2a-143">http://contoso.com의 기본 경로로 '/'만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-143">For the default path of http://contoso.com just use '/'</span></span> |
  |<span data-ttu-id="7ef2a-144">**간격(초)**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-144">**Interval (secs)**</span></span>|<span data-ttu-id="7ef2a-145">30</span><span class="sxs-lookup"><span data-stu-id="7ef2a-145">30</span></span>|<span data-ttu-id="7ef2a-146">상태를 확인하기 위해 프로브가 실행되는 주기입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-146">How often the probe is run to check for health.</span></span> <span data-ttu-id="7ef2a-147">30초 이하 값을 설정하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-147">It is not recommended to set the lower than 30 seconds.</span></span>|
  |<span data-ttu-id="7ef2a-148">**시간 제한(초)**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-148">**Timeout (secs)**</span></span>|<span data-ttu-id="7ef2a-149">30</span><span class="sxs-lookup"><span data-stu-id="7ef2a-149">30</span></span>|<span data-ttu-id="7ef2a-150">프로브에서 시간 초과되기 전에 대기하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-150">The amount of time the probe waits before timing out.</span></span> <span data-ttu-id="7ef2a-151">시간 제한 간격은 http 호출이 백 엔드 상태 페이지를 사용하도록 설정할 수 있을만큼 충분히 높아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-151">The timeout interval needs to be high enough that an http call can be made to ensure the backend health page is available.</span></span>|
  |<span data-ttu-id="7ef2a-152">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="7ef2a-152">**Unhealthy threshold**</span></span>|<span data-ttu-id="7ef2a-153">3</span><span class="sxs-lookup"><span data-stu-id="7ef2a-153">3</span></span>|<span data-ttu-id="7ef2a-154">비정상으로 간주되는 실패한 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-154">Number of failed attempts to be considered unhealthy.</span></span> <span data-ttu-id="7ef2a-155">임계값이 0이면 상태 확인에 실패한 경우 백 엔드는 즉시 비정상인 것으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-155">A threshold of 0 means that if a health check fails the back-end is determined unhealthy immediately.</span></span>|

  > [!IMPORTANT]
  > <span data-ttu-id="7ef2a-156">호스트 이름은 서버 이름과 같지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-156">The host name is not the same as server name.</span></span> <span data-ttu-id="7ef2a-157">이 값은 응용 프로그램 서버에서 실행 중인 가상 호스트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-157">This value is the name of the virtual host running on the application server.</span></span> <span data-ttu-id="7ef2a-158">프로브는 http://(host name):(port from httpsetting)/urlPath로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-158">The probe is sent to http://(host name):(port from httpsetting)/urlPath</span></span>

## <a name="add-probe-to-the-gateway"></a><span data-ttu-id="7ef2a-159">게이트웨이에 프로브 추가</span><span class="sxs-lookup"><span data-stu-id="7ef2a-159">Add probe to the gateway</span></span>

<span data-ttu-id="7ef2a-160">프로브를 만들었으므로 이제 게이트웨이에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-160">Now that the probe has been created, it is time to add it to the gateway.</span></span> <span data-ttu-id="7ef2a-161">프로브 설정은 응용 프로그램 게이트웨이의 백 엔드 http 설정에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-161">Probe settings are set on the backend http settings of the application gateway.</span></span>

1. <span data-ttu-id="7ef2a-162">응용 프로그램 게이트웨이에서 **HTTP 설정**을 클릭하여 구성 블레이드를 불러온 다음, 창에 나열된 현재 백 엔드 http 설정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-162">Click **HTTP settings** on the application gateway, to bring up the configuration blade click the current backend http settings listed in the window.</span></span>

  ![https 설정 창][2]

1. <span data-ttu-id="7ef2a-164">**appGatewayBackEndHttpSettings** 설정 블레이드에서 **사용자 지정 프로브 사용** 확인란을 선택하고, 앞서의 [프로브 만들기](#createprobe) 섹션에서 만든 프로브를 **사용자 지정 프로브** 드롭다운에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-164">On the **appGatewayBackEndHttpSettings** settings blade, check the **Use custom probe** checkbox and choose the probe created in the [Create the probe](#createprobe) section on the **Custom probe** drop-down..</span></span>
<span data-ttu-id="7ef2a-165">완료되면 **저장**을 클릭하여 해당 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-165">When complete, click **Save** and the settings are applied.</span></span>

<span data-ttu-id="7ef2a-166">기본 프로브는 웹 응용 프로그램에 대한 기본 액세스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-166">The default probe checks the default access to the web application.</span></span> <span data-ttu-id="7ef2a-167">사용자 지정 프로브를 만들었으므로 응용 프로그램 게이트웨이에서 정의된 사용자 지정 경로를 사용하여 선택된 백 엔드 서버의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-167">Now that a custom probe has been created, the application gateway uses the custom path defined to monitor health for the backend servers.</span></span> <span data-ttu-id="7ef2a-168">정의된 기준에 따라 응용 프로그램 게이트웨이에서 프로브에 지정된 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-168">Based on the criteria that was defined, the application gateway checks the path specified in the probe.</span></span> <span data-ttu-id="7ef2a-169">host:Port/path에 대한 호출에서 HTTP 200-399 상태 응답을 반환하지 않으면 비정상 임계값에 도달한 후에 서버가 회전에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-169">If the call to host:Port/path does not return an HTTP 200-399 status response, the server is taken out of rotation after the unhealthy threshold is reached.</span></span> <span data-ttu-id="7ef2a-170">비정상 인스턴스에 대해 프로빙이 계속되며 다시 정상 상태가 되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-170">Probing continues on the unhealthy instance to determine when it becomes healthy again.</span></span> <span data-ttu-id="7ef2a-171">인스턴스가 정상 서버 풀에 다시 추가되면 트래픽이 다시 흐르기 시작하고 평소처럼 사용자가 지정한 간격으로 인스턴스에 대한 프로빙이 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef2a-171">Once the instance is added back to healthy server pool, traffic begins flowing to it again and probing to the instance continues at user specified interval as normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef2a-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ef2a-172">Next steps</span></span>

<span data-ttu-id="7ef2a-173">Azure Application Gateway를 사용하여 SSL 오프로드를 구성하는 방법은 [SSL 오프로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7ef2a-173">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

