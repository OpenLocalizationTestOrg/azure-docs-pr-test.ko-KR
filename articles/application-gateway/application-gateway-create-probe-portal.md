---
title: "aaaCreate 사용자 지정 프로브-Azure 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 프로브 응용 프로그램 게이트웨이에 대 한 hello 포털을 사용 하 여 알아봅니다"
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
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a><span data-ttu-id="38cd8-103">Hello 포털을 사용 하 여 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브를 만들기</span><span class="sxs-lookup"><span data-stu-id="38cd8-103">Create a custom probe for Application Gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38cd8-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="38cd8-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="38cd8-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="38cd8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="38cd8-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="38cd8-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="38cd8-107">이 문서에서는 hello Azure 포털을 통해 사용자 지정 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-107">In this article, you add a custom probe tooan existing application gateway through hello Azure portal.</span></span> <span data-ttu-id="38cd8-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용 하는 응용 프로그램 또는 hello 기본 웹 응용 프로그램에 대 한 성공적인 응답을 제공 하지 않는 응용 프로그램에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="38cd8-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="38cd8-109">Before you begin</span></span>

<span data-ttu-id="38cd8-110">응용 프로그램 게이트웨이 아직 없는 경우 방문 [응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md) toocreate 응용 프로그램 게이트웨이 toowork 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-110">If you do not already have an application gateway, visit [Create an Application Gateway](application-gateway-create-gateway-portal.md) toocreate an application gateway toowork with.</span></span>

## <span data-ttu-id="38cd8-111"><a name="createprobe"></a>Hello 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="38cd8-111"><a name="createprobe"></a>Create hello probe</span></span>

<span data-ttu-id="38cd8-112">프로브는 hello 포털을 통해는 두 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-112">Probes are configured in a two-step process through hello portal.</span></span> <span data-ttu-id="38cd8-113">hello 첫 번째 단계는 toocreate hello 프로브입니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-113">hello first step is toocreate hello probe.</span></span> <span data-ttu-id="38cd8-114">Hello 두 번째 단계에서는 hello 프로브 toohello 백 엔드 http 설정의 hello 응용 프로그램 게이트웨이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-114">In hello second step, you add hello probe toohello backend http settings of hello application gateway.</span></span>

1. <span data-ttu-id="38cd8-115">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-115">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="38cd8-116">아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-116">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>

1. <span data-ttu-id="38cd8-117">Azure 포털 즐겨찾기 창 hello에서 모든 리소스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-117">In hello Azure portal Favorites pane, click All resources.</span></span> <span data-ttu-id="38cd8-118">Hello 응용 프로그램 게이트웨이 hello에서 모든 리소스 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-118">Click hello application gateway in hello All resources blade.</span></span> <span data-ttu-id="38cd8-119">이미 선택한 hello 구독에 있는 여러 가지 리소스가, 경우에 이름으로 hello 필터에에서 partners.contoso.net를 입력할 수 있습니다...</span><span class="sxs-lookup"><span data-stu-id="38cd8-119">If hello subscription you selected already has several resources in it, you can enter partners.contoso.net in hello Filter by name…</span></span> <span data-ttu-id="38cd8-120">상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-120">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="38cd8-121">클릭 **프로브** hello 클릭 **추가** 단추 tooadd 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-121">Click **Probes** and click hello **Add** button tooadd a probe.</span></span>

  ![정보가 입력된 프로브 추가 블레이드][1]

1. <span data-ttu-id="38cd8-123">Hello에 **추가 상태 프로브** 블레이드에서 hello 프로브에 대 한 hello 필요한 정보를 입력 하 고 클릭 하 여 완료 된 경우 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-123">On hello **Add health probe** blade, fill out hello required information for hello probe, and when complete click **OK**.</span></span>

  |<span data-ttu-id="38cd8-124">**설정**</span><span class="sxs-lookup"><span data-stu-id="38cd8-124">**Setting**</span></span> | <span data-ttu-id="38cd8-125">**값**</span><span class="sxs-lookup"><span data-stu-id="38cd8-125">**Value**</span></span> | <span data-ttu-id="38cd8-126">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="38cd8-126">**Details**</span></span>|
  |---|---|---|
  |<span data-ttu-id="38cd8-127">**Name**</span><span class="sxs-lookup"><span data-stu-id="38cd8-127">**Name**</span></span>|<span data-ttu-id="38cd8-128">customProbe</span><span class="sxs-lookup"><span data-stu-id="38cd8-128">customProbe</span></span>|<span data-ttu-id="38cd8-129">이 값은 hello 포털에 액세스 하는 이름 toohello 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-129">This value is a friendly name toohello probe that is accessible in hello portal.</span></span>|
  |<span data-ttu-id="38cd8-130">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="38cd8-130">**Protocol**</span></span>|<span data-ttu-id="38cd8-131">HTTP 또는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="38cd8-131">HTTP or HTTPS</span></span> | <span data-ttu-id="38cd8-132">상태 프로브 hello hello 프로토콜 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-132">hello protocol that hello health probe uses.</span></span>|
  |<span data-ttu-id="38cd8-133">**호스트**</span><span class="sxs-lookup"><span data-stu-id="38cd8-133">**Host**</span></span>|<span data-ttu-id="38cd8-134">예:</span><span class="sxs-lookup"><span data-stu-id="38cd8-134">i.e</span></span> <span data-ttu-id="38cd8-135">contoso.com</span><span class="sxs-lookup"><span data-stu-id="38cd8-135">contoso.com</span></span>|<span data-ttu-id="38cd8-136">이 값은 hello 프로브에 사용 되는 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-136">This value is hello host name that is used for hello probe.</span></span> <span data-ttu-id="38cd8-137">다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-137">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="38cd8-138">이 값은 hello VM 호스트 이름이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-138">This value is different from hello VM host name.</span></span>|
  |<span data-ttu-id="38cd8-139">**Path**</span><span class="sxs-lookup"><span data-stu-id="38cd8-139">**Path**</span></span>|<span data-ttu-id="38cd8-140">/ 또는 다른 경로</span><span class="sxs-lookup"><span data-stu-id="38cd8-140">/ or another path</span></span>|<span data-ttu-id="38cd8-141">사용자 지정 프로브 hello에 대 한 전체 url hello의 hello 나머지입니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-141">hello remainder of hello full url for hello custom probe.</span></span> <span data-ttu-id="38cd8-142">유효한 경로는 '/'로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-142">A valid path starts with '/'.</span></span> <span data-ttu-id="38cd8-143">사용 하 여 정당한 http://contoso.com의 기본 경로 hello에 대 한 '/'</span><span class="sxs-lookup"><span data-stu-id="38cd8-143">For hello default path of http://contoso.com just use '/'</span></span> |
  |<span data-ttu-id="38cd8-144">**간격(초)**</span><span class="sxs-lookup"><span data-stu-id="38cd8-144">**Interval (secs)**</span></span>|<span data-ttu-id="38cd8-145">30</span><span class="sxs-lookup"><span data-stu-id="38cd8-145">30</span></span>|<span data-ttu-id="38cd8-146">얼마나 자주 hello 프로브는 실행 상태에 대 한 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-146">How often hello probe is run toocheck for health.</span></span> <span data-ttu-id="38cd8-147">30 초 보다 낮은 tooset hello는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-147">It is not recommended tooset hello lower than 30 seconds.</span></span>|
  |<span data-ttu-id="38cd8-148">**시간 제한(초)**</span><span class="sxs-lookup"><span data-stu-id="38cd8-148">**Timeout (secs)**</span></span>|<span data-ttu-id="38cd8-149">30</span><span class="sxs-lookup"><span data-stu-id="38cd8-149">30</span></span>|<span data-ttu-id="38cd8-150">hello 양의 시간 hello 검색 시간 초과 전까지 대기합니다. hello 시간 제한 간격 요구 toobe tooensure hello 백 엔드 상태 페이지는 http 호출을 할 수는 충분히 높은 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="38cd8-150">hello amount of time hello probe waits before timing out. hello timeout interval needs toobe high enough that an http call can be made tooensure hello backend health page is available.</span></span>|
  |<span data-ttu-id="38cd8-151">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="38cd8-151">**Unhealthy threshold**</span></span>|<span data-ttu-id="38cd8-152">3</span><span class="sxs-lookup"><span data-stu-id="38cd8-152">3</span></span>|<span data-ttu-id="38cd8-153">비정상으로 간주 하는 시도 toobe를 실패 하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-153">Number of failed attempts toobe considered unhealthy.</span></span> <span data-ttu-id="38cd8-154">임계값이 상태 검사에 실패 하는 경우 백 엔드 hello 0 이면 즉시 비정상 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-154">A threshold of 0 means that if a health check fails hello back-end is determined unhealthy immediately.</span></span>|

  > [!IMPORTANT]
  > <span data-ttu-id="38cd8-155">hello 호스트 이름이 서버 이름과 달라 서는 안녕 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-155">hello host name is not hello same as server name.</span></span> <span data-ttu-id="38cd8-156">이 값은 hello 이름 hello hello 응용 프로그램 서버에서 실행 되는 가상 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-156">This value is hello name of hello virtual host running on hello application server.</span></span> <span data-ttu-id="38cd8-157">hello 프로브 toohttp 보내집니다: / /(host name):(port from httpsetting)/urlPath</span><span class="sxs-lookup"><span data-stu-id="38cd8-157">hello probe is sent toohttp://(host name):(port from httpsetting)/urlPath</span></span>

## <a name="add-probe-toohello-gateway"></a><span data-ttu-id="38cd8-158">프로브 toohello 게이트웨이 추가</span><span class="sxs-lookup"><span data-stu-id="38cd8-158">Add probe toohello gateway</span></span>

<span data-ttu-id="38cd8-159">이제 hello 프로브를 만든입니다 시간 tooadd 것 toohello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-159">Now that hello probe has been created, it is time tooadd it toohello gateway.</span></span> <span data-ttu-id="38cd8-160">프로브 hello hello 응용 프로그램 게이트웨이 백 엔드 http 설정에 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-160">Probe settings are set on hello backend http settings of hello application gateway.</span></span>

1. <span data-ttu-id="38cd8-161">클릭 **HTTP 설정** hello 응용 프로그램 게이트웨이 hello 현재 백 엔드 http 설정 hello 창에 나열 된 toobring hello 구성 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-161">Click **HTTP settings** on hello application gateway, toobring up hello configuration blade click hello current backend http settings listed in hello window.</span></span>

  ![https 설정 창][2]

1. <span data-ttu-id="38cd8-163">Hello에 **appGatewayBackEndHttpSettings** 설정 블레이드에서, 검사 hello **사용 하 여 사용자 지정 프로브** 확인란 hello에서 만든 hello 프로브 선택 [만들기 hello 프로브](#createprobe) 섹션 hello에 **사용자 지정 프로브** 드롭 다운...</span><span class="sxs-lookup"><span data-stu-id="38cd8-163">On hello **appGatewayBackEndHttpSettings** settings blade, check hello **Use custom probe** checkbox and choose hello probe created in hello [Create hello probe](#createprobe) section on hello **Custom probe** drop-down..</span></span>
<span data-ttu-id="38cd8-164">완료 되 면 **저장** hello 설정이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-164">When complete, click **Save** and hello settings are applied.</span></span>

<span data-ttu-id="38cd8-165">hello 기본 프로브 hello 기본 액세스 toohello 웹 응용 프로그램을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-165">hello default probe checks hello default access toohello web application.</span></span> <span data-ttu-id="38cd8-166">사용자 지정 프로브를 만든 후, hello 응용 프로그램 게이트웨이 백 엔드 서버 hello에 대 한 hello 정의 된 사용자 지정 경로 toomonitor 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-166">Now that a custom probe has been created, hello application gateway uses hello custom path defined toomonitor health for hello backend servers.</span></span> <span data-ttu-id="38cd8-167">정의 된 hello 기준에 따라, 응용 프로그램 게이트웨이 hello hello 프로브에 지정 된 hello 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-167">Based on hello criteria that was defined, hello application gateway checks hello path specified in hello probe.</span></span> <span data-ttu-id="38cd8-168">Hello 호출 toohost:Port / 경로 HTTP 200 399 상태 응답 반환 하지 않는, 경우 hello 비정상 임계값에 도달 하면 hello 서버 순환 순서에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-168">If hello call toohost:Port/path does not return an HTTP 200-399 status response, hello server is taken out of rotation after hello unhealthy threshold is reached.</span></span> <span data-ttu-id="38cd8-169">다시 정상 있게 되 면 hello 비정상 인스턴스 toodetermine에서 계속 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-169">Probing continues on hello unhealthy instance toodetermine when it becomes healthy again.</span></span> <span data-ttu-id="38cd8-170">트래픽이 흐르는 tooit 다시 및 검색 toohello 시작 hello 인스턴스 백 toohealthy 서버 풀에 추가 되 면 인스턴스는 일반적인 방법으로 사용자 지정된 간격으로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cd8-170">Once hello instance is added back toohealthy server pool, traffic begins flowing tooit again and probing toohello instance continues at user specified interval as normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38cd8-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38cd8-171">Next steps</span></span>

<span data-ttu-id="38cd8-172">Azure 응용 프로그램 게이트웨이 통해 SSL 오프 로딩 tooconfigure 참조 toolearn [SSL 오프 로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="38cd8-172">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

