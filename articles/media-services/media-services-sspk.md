---
title: "Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스"
description: "Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스를 얻는 방법에 대해 알아보세요."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="2cbf2-103">Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="2cbf2-104">개요</span><span class="sxs-lookup"><span data-stu-id="2cbf2-104">Overview</span></span>
<span data-ttu-id="2cbf2-105">Microsoft 부드러운 스트리밍 클라이언트 이식 키트(줄여서**SSPK**)는 임베디드 장치 제조업체, 케이블 및 모바일 운영자, 콘텐츠 서비스 공급자, 송수화기 제조업체, ISV(독립 소프트웨어 공급업체) 및 솔루션 공급자가 가변 스트리밍 콘텐츠를 부드러운 스트리밍 형식으로 스트리밍하는 제품 및 서비스를 만들 수 있도록 최적화된 부드러운 스트리밍 클라이언트 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="2cbf2-106">SSPK는 정식 사용자가 어떠한 장치 및 플랫폼에도 이식할 수 있는 부드러운 스트리밍 클라이언트의 장치 및 플랫폼 독립적인 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="2cbf2-107">아래 내용은 상위 수준의 아키텍처를 보여주며 IIS 부드러운 스트리밍 이식 키트 상자는 Microsoft에서 제공하는 부드러운 스트리밍 클라이언트 구현으로, 부드러운 스트리밍 콘텐츠 재생을 위한 모든 핵심 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="2cbf2-108">그런 다음 파트너는 적절한 인터페이스를 구현하며 특정 장치 또는 플랫폼에 맞게 이식합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="2cbf2-110">설명</span><span class="sxs-lookup"><span data-stu-id="2cbf2-110">Description</span></span>
<span data-ttu-id="2cbf2-111">SSPK는 뛰어난 비즈니스 가치를 제공하는 조건으로 사용 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="2cbf2-112">SSPK 라이선스는 업계에 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="2cbf2-113">C++의 부드러운 스트리밍 이식 키트 소스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="2cbf2-114">부드러운 스트리밍 클라이언트 기능 구현</span><span class="sxs-lookup"><span data-stu-id="2cbf2-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="2cbf2-115">형식 구문 분석, 추론, 버퍼링 논리 등 추가</span><span class="sxs-lookup"><span data-stu-id="2cbf2-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="2cbf2-116">플레이어 응용 프로그램 API</span><span class="sxs-lookup"><span data-stu-id="2cbf2-116">Player application APIs</span></span> 
  * <span data-ttu-id="2cbf2-117">미디어 플레이어 응용 프로그램과 상호 작용을 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="2cbf2-118">PAL(플랫폼 추상화 계층) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="2cbf2-119">운영 체제(스레드, 소켓)와 상호 작용을 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="2cbf2-120">HAL(하드웨어 추상화 계층) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="2cbf2-121">하드웨어 A/V 디코더(디코딩, 렌더링)와 상호 작용을 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="2cbf2-122">DRM(디지털 권한 관리) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="2cbf2-123">DAL(DRM 추상화 계층)을 통해 DRM을 처리하기 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="2cbf2-124">Microsoft PlayReady 이식 키트는 별도로 제공되지만 이 인터페이스를 통해 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="2cbf2-125">Microsoft PlayReady 장치 라이선스에 대한 자세한 내용을 보려면 [여기](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="2cbf2-126">구현 샘플</span><span class="sxs-lookup"><span data-stu-id="2cbf2-126">Implementation samples</span></span> 
  * <span data-ttu-id="2cbf2-127">Linux용 샘플 PAL 구현</span><span class="sxs-lookup"><span data-stu-id="2cbf2-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="2cbf2-128">GStreamer용 샘플 HAL 구현</span><span class="sxs-lookup"><span data-stu-id="2cbf2-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="2cbf2-129">라이선스 옵션</span><span class="sxs-lookup"><span data-stu-id="2cbf2-129">Licensing Options</span></span>
<span data-ttu-id="2cbf2-130">Microsoft 부드러운 스트리밍 클라이언트 이식 키트는 두 가지의 고유한 라이선스 계약에 따라 정식 사용자에게 제공됩니다. 하나는 부드러운 스트리밍 클라이언트 중간 제품 개발을 위한 라이선스에고 다른 하나는 부드러운 스트리밍 클라이언트 최종 제품을 최종 사용자에게 배포하기 위한 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="2cbf2-131">칩셋 제조업체, 시스템 통합 업체 또는 중간 제품 개발을 위해 소스 코드 이식 키트가 필요한 ISV(독립 소프트웨어 공급업체)는 Microsoft 부드러운 스트리밍 클라이언트 이식 키트 **중간 제품 라이선스**를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="2cbf2-132">부드러운 스트리밍 클라이언트 최종 제품을 최종 사용자에게 배포하는 권한이 필요한 장치 제조업체 또는 ISV는 Microsoft 부드러운 스트리밍 클라이언트 이식 키트 **최종 제품 라이선스**를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="2cbf2-133">Microsoft 부드러운 스트리밍 클라이언트 이식 키트 중간 제품 라이선스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="2cbf2-134">이 라이선스에 따라, Microsoft는 부드러운 스트리밍 클라이언트 이식 키트 및 필요한 지적 재산권을 제공하여 부드러운 스트리밍 클라이언트 중간 제품을 개발하고 다른 부드러운 스트리밍 클라이언트 이식 키트 장치 정식 사용자에게 배포하며 정식 사용자가 부드러운 스트리밍 클라이언트 최종 제품을 배포할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="2cbf2-135">요금 구조</span><span class="sxs-lookup"><span data-stu-id="2cbf2-135">Fee structure</span></span>
<span data-ttu-id="2cbf2-136">한 번의 미국 50,000달러 라이선스 비용으로 부드러운 스트리밍 클라이언트 이식 키트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="2cbf2-137">Microsoft 부드러운 스트리밍 클라이언트 이식 키트 최종 제품 라이선스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="2cbf2-138">이 라이선스에 따라, Microsoft는 다른 부드러운 스트리밍 클라이언트 이식 키트 정식 사용자로부터 부드러운 스트리밍 클라이언트 중간 제품을 받고 회사 브랜드 부드러운 스트리밍 클라이언트 최종 제품을 최종 사용자에게 배포하는 데 필요한 모든 지적 재산권을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="2cbf2-139">요금 구조</span><span class="sxs-lookup"><span data-stu-id="2cbf2-139">Fee structure</span></span>
<span data-ttu-id="2cbf2-140">부드러운 스트리밍 클라이언트 최종 제품은 아래 사용료 모델에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="2cbf2-141">제공된 장치 구현당 0.10달러</span><span class="sxs-lookup"><span data-stu-id="2cbf2-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="2cbf2-142">사용료는 각 연도에 50,000달러로 제한됨</span><span class="sxs-lookup"><span data-stu-id="2cbf2-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="2cbf2-143">각 연도의 최초 10,000대의 장치 구현에 대해서는 사용료 없음</span><span class="sxs-lookup"><span data-stu-id="2cbf2-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="2cbf2-144">라이선스 절차 및 SSPK 액세스</span><span class="sxs-lookup"><span data-stu-id="2cbf2-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="2cbf2-145">모든 라이선스 관련 문의는 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 로 문의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="2cbf2-146">[SSPK 배포 포털](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) 은 등록된 중간 정식 사용자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="2cbf2-147">중간 및 최종 SSPK 정식 사용자는 [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="2cbf2-148">Microsoft 부드러운 스트리밍 클라이언트 중간 제품 계약 정식 사용자</span><span class="sxs-lookup"><span data-stu-id="2cbf2-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="2cbf2-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="2cbf2-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="2cbf2-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="2cbf2-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="2cbf2-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="2cbf2-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="2cbf2-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-153">Alticast Corporation</span></span>
* <span data-ttu-id="2cbf2-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="2cbf2-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="2cbf2-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-157">Cavium, Inc.</span></span>
* <span data-ttu-id="2cbf2-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="2cbf2-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-159">Enseo, Inc.</span></span>
* <span data-ttu-id="2cbf2-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-160">Fluendo S.A.</span></span>
* <span data-ttu-id="2cbf2-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="2cbf2-162">Infomir GMBH</span></span>
* <span data-ttu-id="2cbf2-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="2cbf2-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="2cbf2-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="2cbf2-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="2cbf2-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-166">MediaTek Inc.</span></span>
* <span data-ttu-id="2cbf2-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="2cbf2-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="2cbf2-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="2cbf2-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="2cbf2-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="2cbf2-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="2cbf2-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="2cbf2-172">SoftAtHome</span></span>
* <span data-ttu-id="2cbf2-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-173">Sony Corporation</span></span>
* <span data-ttu-id="2cbf2-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="2cbf2-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="2cbf2-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="2cbf2-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="2cbf2-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="2cbf2-180">Microsoft 부드러운 스트리밍 클라이언트 최종 제품 계약 정식 사용자</span><span class="sxs-lookup"><span data-stu-id="2cbf2-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="2cbf2-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="2cbf2-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="2cbf2-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="2cbf2-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="2cbf2-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="2cbf2-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="2cbf2-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="2cbf2-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="2cbf2-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-189">VE TİC.</span></span> <span data-ttu-id="2cbf2-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="2cbf2-190">A.Ş</span></span>
* <span data-ttu-id="2cbf2-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="2cbf2-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="2cbf2-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="2cbf2-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="2cbf2-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="2cbf2-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="2cbf2-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-196">Enseo, Inc.</span></span>
* <span data-ttu-id="2cbf2-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="2cbf2-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-198">Fluendo S.A.</span></span>
* <span data-ttu-id="2cbf2-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="2cbf2-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="2cbf2-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="2cbf2-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="2cbf2-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="2cbf2-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="2cbf2-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="2cbf2-205">Infomir GMBH</span></span>
* <span data-ttu-id="2cbf2-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-207">KDDI Corporation</span></span>
* <span data-ttu-id="2cbf2-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="2cbf2-209">Orange SA</span></span>
* <span data-ttu-id="2cbf2-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="2cbf2-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="2cbf2-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="2cbf2-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="2cbf2-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="2cbf2-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="2cbf2-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="2cbf2-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="2cbf2-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="2cbf2-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="2cbf2-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="2cbf2-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="2cbf2-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="2cbf2-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="2cbf2-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="2cbf2-219">SoftAtHome</span></span>
* <span data-ttu-id="2cbf2-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-220">Sony Corporation</span></span>
* <span data-ttu-id="2cbf2-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="2cbf2-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="2cbf2-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="2cbf2-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="2cbf2-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="2cbf2-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="2cbf2-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="2cbf2-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="2cbf2-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="2cbf2-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-228">Wistron Corporation</span></span>
* <span data-ttu-id="2cbf2-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="2cbf2-230">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2cbf2-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2cbf2-231">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2cbf2-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

