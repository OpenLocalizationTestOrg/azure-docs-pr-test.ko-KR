---
title: "Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 aaaLicensing"
description: "Toolicensing Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="a18cd-103">Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스</span><span class="sxs-lookup"><span data-stu-id="a18cd-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="a18cd-104">개요</span><span class="sxs-lookup"><span data-stu-id="a18cd-104">Overview</span></span>
<span data-ttu-id="a18cd-105">Microsoft 부드러운 스트리밍 클라이언트 이식 키트 (**SSPK** 줄여서)는 포함 된 최적화 된 toohelp 장치 제조업체, 케이블 및 모바일 사업자, 콘텐츠 서비스 공급자, 송수화기는 부드러운 스트리밍 클라이언트 구현 제조업체, 독립 소프트웨어 공급 업체 (Isv) 및 솔루션 공급자 toocreate 제품 및 서비스 부드러운 스트리밍 형식의 적응 스트리밍 콘텐츠를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="a18cd-106">SSPK는 정식 사용자 tooany 장치 hello 및 플랫폼으로 이식 될 수 있는 부드러운 스트리밍 클라이언트의 장치 및 플랫폼 독립적 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="a18cd-107">아래에 포함 된 높은 수준의 아키텍처 이며 IIS 부드러운 스트리밍 이식 키트 상자는 Microsoft에서 제공 하는 hello 부드러운 스트리밍 클라이언트 구현 하며 부드러운 스트리밍 콘텐츠를 재생 하기 위한 모든 hello 핵심 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="a18cd-108">그런 다음 파트너는 적절한 인터페이스를 구현하며 특정 장치 또는 플랫폼에 맞게 이식합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="a18cd-110">설명</span><span class="sxs-lookup"><span data-stu-id="a18cd-110">Description</span></span>
<span data-ttu-id="a18cd-111">SSPK는 뛰어난 비즈니스 가치를 제공하는 조건으로 사용 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="a18cd-112">SSPK 라이선스와 hello 업계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="a18cd-113">C++의 부드러운 스트리밍 이식 키트 소스</span><span class="sxs-lookup"><span data-stu-id="a18cd-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="a18cd-114">부드러운 스트리밍 클라이언트 기능 구현</span><span class="sxs-lookup"><span data-stu-id="a18cd-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="a18cd-115">형식 구문 분석, 추론, 버퍼링 논리 등 추가</span><span class="sxs-lookup"><span data-stu-id="a18cd-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="a18cd-116">플레이어 응용 프로그램 API</span><span class="sxs-lookup"><span data-stu-id="a18cd-116">Player application APIs</span></span> 
  * <span data-ttu-id="a18cd-117">미디어 플레이어 응용 프로그램과 상호 작용을 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="a18cd-118">PAL(플랫폼 추상화 계층) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="a18cd-119">hello 운영 체제 (스레드, 소켓)와 상호 작용에 대 한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="a18cd-120">HAL(하드웨어 추상화 계층) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="a18cd-121">하드웨어 A/V 디코더(디코딩, 렌더링)와 상호 작용을 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="a18cd-122">DRM(디지털 권한 관리) 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="a18cd-123">DRM hello DRM DAL (추상화 계층)을 통해 처리 하기 위한 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="a18cd-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="a18cd-124">Microsoft PlayReady 이식 키트는 별도로 제공되지만 이 인터페이스를 통해 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="a18cd-125">Microsoft PlayReady 장치 라이선스에 대한 자세한 내용을 보려면 [여기](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="a18cd-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="a18cd-126">구현 샘플</span><span class="sxs-lookup"><span data-stu-id="a18cd-126">Implementation samples</span></span> 
  * <span data-ttu-id="a18cd-127">Linux용 샘플 PAL 구현</span><span class="sxs-lookup"><span data-stu-id="a18cd-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="a18cd-128">GStreamer용 샘플 HAL 구현</span><span class="sxs-lookup"><span data-stu-id="a18cd-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="a18cd-129">라이선스 옵션</span><span class="sxs-lookup"><span data-stu-id="a18cd-129">Licensing Options</span></span>
<span data-ttu-id="a18cd-130">Microsoft 부드러운 스트리밍 클라이언트 이식 키트는 두 개의 고유 사용권 계약에서 사용 가능한 toolicensees 이루어집니다: 부드러운 스트리밍 클라이언트 중간 제품 및 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 tooend 사용자 배포 관리를 위한 개발에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="a18cd-131">칩셋 제조업체, 시스템 통합 업체가 또는 독립 소프트웨어 공급 업체 (Isv 소스 코드 포팅 해야 하 는) 키트는 Microsoft 부드러운 스트리밍 클라이언트 이식 키트 toodevelop 중간 제품 **중간 제품 라이선스** 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="a18cd-132">장치 제조업체 또는 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 tooend 사용자에 대 한 배포 권한이 필요로 하는 Isv hello Microsoft 부드러운 스트리밍 클라이언트 이식 키트에 대 한 **최종 제품 라이선스** 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="a18cd-133">Microsoft 부드러운 스트리밍 클라이언트 이식 키트 중간 제품 라이선스</span><span class="sxs-lookup"><span data-stu-id="a18cd-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="a18cd-134">이 라이선스에 따라 Microsoft는 부드러운 스트리밍 클라이언트 이식 키트 제공 필요한 지적 재산권 권한 toodevelop hello 및 부드러운 스트리밍 클라이언트 중간 제품 tooother 부드러운 스트리밍 클라이언트 이식 키트 장치 라이선스 실시 권 자 배포 하는 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a18cd-135">요금 구조</span><span class="sxs-lookup"><span data-stu-id="a18cd-135">Fee structure</span></span>
<span data-ttu-id="a18cd-136">미국 $ 50, 000 번 라이센스 요금은 액세스 toohello 부드러운 스트리밍 클라이언트 이식 키트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="a18cd-137">Microsoft 부드러운 스트리밍 클라이언트 이식 키트 최종 제품 라이선스</span><span class="sxs-lookup"><span data-stu-id="a18cd-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="a18cd-138">이 라이선스에 따라 Microsoft는 다른 부드러운 스트리밍 클라이언트 이식 키트용 라이선스 실시 권 자 및 회사 브랜드 부드러운 스트리밍 클라이언트 최종 toodistribute에서 필요한 모든 지적 재산권 권한 tooreceive 부드러운 스트리밍 클라이언트 중간 제품을 제공 제품 tooend 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a18cd-139">요금 구조</span><span class="sxs-lookup"><span data-stu-id="a18cd-139">Fee structure</span></span>
<span data-ttu-id="a18cd-140">여기에서는 스트리밍 되지 않은 부드러운 클라이언트 최종 제품 hello 아래으로 사용료 모델에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="a18cd-141">제공된 장치 구현당 0.10달러</span><span class="sxs-lookup"><span data-stu-id="a18cd-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="a18cd-142">각 연도 50, 000 달러에 hello 사용료는 제한</span><span class="sxs-lookup"><span data-stu-id="a18cd-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="a18cd-143">각 연도의 최초 10,000대의 장치 구현에 대해서는 사용료 없음</span><span class="sxs-lookup"><span data-stu-id="a18cd-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="a18cd-144">라이선스 절차 및 SSPK 액세스</span><span class="sxs-lookup"><span data-stu-id="a18cd-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="a18cd-145">모든 라이선스 관련 문의는 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 로 문의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="a18cd-146">hello [SSPK 배포 포털](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) 는 액세스할 수 있는 tooregistered 중간 라이선스 실시 권 자입니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="a18cd-147">중간 및 마지막 SSPK 라이선스 실시 권 자 기술 관련 질문에 너무 제출할 수[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a18cd-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="a18cd-148">Microsoft 부드러운 스트리밍 클라이언트 중간 제품 계약 정식 사용자</span><span class="sxs-lookup"><span data-stu-id="a18cd-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="a18cd-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="a18cd-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="a18cd-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a18cd-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a18cd-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a18cd-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a18cd-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a18cd-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-153">Alticast Corporation</span></span>
* <span data-ttu-id="a18cd-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a18cd-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a18cd-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-157">Cavium, Inc.</span></span>
* <span data-ttu-id="a18cd-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a18cd-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-159">Enseo, Inc.</span></span>
* <span data-ttu-id="a18cd-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a18cd-160">Fluendo S.A.</span></span>
* <span data-ttu-id="a18cd-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a18cd-162">Infomir GMBH</span></span>
* <span data-ttu-id="a18cd-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="a18cd-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="a18cd-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="a18cd-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="a18cd-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="a18cd-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-166">MediaTek Inc.</span></span>
* <span data-ttu-id="a18cd-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="a18cd-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="a18cd-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="a18cd-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="a18cd-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a18cd-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="a18cd-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a18cd-172">SoftAtHome</span></span>
* <span data-ttu-id="a18cd-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-173">Sony Corporation</span></span>
* <span data-ttu-id="a18cd-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="a18cd-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a18cd-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a18cd-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="a18cd-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="a18cd-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="a18cd-180">Microsoft 부드러운 스트리밍 클라이언트 최종 제품 계약 정식 사용자</span><span class="sxs-lookup"><span data-stu-id="a18cd-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="a18cd-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a18cd-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a18cd-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a18cd-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a18cd-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a18cd-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a18cd-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="a18cd-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a18cd-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="a18cd-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="a18cd-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="a18cd-189">VE TİC.</span></span> <span data-ttu-id="a18cd-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="a18cd-190">A.Ş</span></span>
* <span data-ttu-id="a18cd-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="a18cd-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="a18cd-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="a18cd-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="a18cd-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="a18cd-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a18cd-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-196">Enseo, Inc.</span></span>
* <span data-ttu-id="a18cd-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="a18cd-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a18cd-198">Fluendo S.A.</span></span>
* <span data-ttu-id="a18cd-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="a18cd-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="a18cd-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="a18cd-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="a18cd-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a18cd-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="a18cd-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a18cd-205">Infomir GMBH</span></span>
* <span data-ttu-id="a18cd-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-207">KDDI Corporation</span></span>
* <span data-ttu-id="a18cd-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="a18cd-209">Orange SA</span></span>
* <span data-ttu-id="a18cd-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="a18cd-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="a18cd-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="a18cd-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="a18cd-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="a18cd-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a18cd-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="a18cd-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a18cd-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="a18cd-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="a18cd-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="a18cd-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="a18cd-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="a18cd-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="a18cd-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="a18cd-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="a18cd-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a18cd-219">SoftAtHome</span></span>
* <span data-ttu-id="a18cd-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-220">Sony Corporation</span></span>
* <span data-ttu-id="a18cd-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="a18cd-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="a18cd-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="a18cd-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="a18cd-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="a18cd-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a18cd-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a18cd-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="a18cd-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="a18cd-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="a18cd-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="a18cd-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="a18cd-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-228">Wistron Corporation</span></span>
* <span data-ttu-id="a18cd-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a18cd-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="a18cd-230">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a18cd-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a18cd-231">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a18cd-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

