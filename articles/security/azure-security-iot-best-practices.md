---
title: "작업 보안 모범 사례 aaaInternet | Microsoft Docs"
description: "hello 문서에는 작업 보안에 대 한 유용한 정보 및 일반적인 권장 사항은 Microsoft 인터넷의 큐 레이트 목록을 제공 합니다."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="76b2f-103">사물 인터넷 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="76b2f-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="76b2f-104">고정 hello 인터넷 IoT (사물) 인프라는 IoT 솔루션과 관련 된 모든 사용자에 대 한 중요 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="76b2f-105">포함 된 장치 수 hello 및 hello 때문에 이러한 장치는 보안 이벤트 hello 영향의 분산된 특성 관련 toocompromise IoT 장치 수많은의 특수 이며 광범위 한 영향을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="76b2f-106">이런 이유로 IoT 보안은 심층적인 보안 접근 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="76b2f-107">데이터 요구 toobe 보안 hello 클라우드 및으로 개인 및 공용 네트워크를 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="76b2f-108">메서드는 toobe 위치 toosecurely 프로 비전 hello IoT 장치 자체에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="76b2f-109">장치, toonetwork, toocloud 백 엔드에서 각 계층 강력한 보안 보증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="76b2f-110">다음 방식으로 hello에서 IoT에 대 한 유용한 정보를 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="76b2f-111">IoT 하드웨어 제조업체 또는 통합업체</span><span class="sxs-lookup"><span data-stu-id="76b2f-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="76b2f-112">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="76b2f-112">IoT solution developer</span></span>
* <span data-ttu-id="76b2f-113">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="76b2f-113">IoT solution deployer</span></span>
* <span data-ttu-id="76b2f-114">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="76b2f-114">IoT solution operator</span></span>

<span data-ttu-id="76b2f-115">이 문서는 [사물 인터넷 보안 모범 사례](../iot-suite/iot-security-best-practices.md)를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="76b2f-116">자세한 내용을 보려면 toothat 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="76b2f-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="76b2f-117">IoT 하드웨어 제조업체 또는 통합업체</span><span class="sxs-lookup"><span data-stu-id="76b2f-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="76b2f-118">IoT 하드웨어 제조업체 또는 하드웨어 integrator 인 경우 아래 hello 모범 사례를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="76b2f-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="76b2f-119">**하드웨어 toominimum 요구 범위**: hello 하드웨어 설계 hello 하드웨어 하며 그 이상의의 작동에 필요한 최소 기능을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="76b2f-120">**하드웨어 변조할**: 메커니즘 toodetect 물리적 변조 hello 장치 등의 일부를 hello 장치 덮개 열기 등의 하드웨어에서 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="76b2f-121">**보안 하드웨어를 중심으로 구축**: [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) 가 허용된다면 안전하게 암호화되는 저장소 및 TPM(신뢰할 수 있는 플랫폼 모듈) 기반 부팅 기능 같은 보안 기능을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="76b2f-122">**업그레이드를 안전 하 게**: hello 장치의 수명 동안 펌웨어 업그레이드는 불가피 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="76b2f-123">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="76b2f-123">IoT solution developer</span></span>
<span data-ttu-id="76b2f-124">IoT 솔루션 개발자의 경우 아래 hello 모범 사례를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="76b2f-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="76b2f-125">**보안 소프트웨어 개발 방법에 따라**: 명확 하 게 접속 모든 hello 방식으로 tooits 구현, 테스트 및 배포 hello 끌려 hello 프로젝트의 보안을 고려할 필요 안전한 소프트웨어를 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="76b2f-126">**오픈 소스 소프트웨어를 주의 해 서 선택**: 기회를 제공 하는 오픈 소스 소프트웨어 tooquickly 솔루션을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="76b2f-127">**주의 하 여 통합**: 다양 한 소프트웨어 보안 결함 hello 라이브러리 및 Api의 hello 경계에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="76b2f-128">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="76b2f-128">IoT solution deployer</span></span>
<span data-ttu-id="76b2f-129">IoT 솔루션 배포자의 경우 아래 hello 모범 사례를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="76b2f-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="76b2f-130">**하드웨어를 안전 하 게 배포**: IoT 배포와 같이 공용 공간 또는 자율된 로캘 보안 되지 않은 위치에 배포 된 하드웨어 toobe 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="76b2f-131">**인증 키를 안전 하 게 유지**: 배포 하는 동안 각 장치 장치 Id를 요구 하 고 hello 클라우드 서비스에 의해 생성 된 인증 키를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="76b2f-132">Hello 배포 후에 이러한 키를 물리적으로 안전 하 게 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="76b2f-133">기존 장치로 악의적인 장치 toomasquerade에서 손상 된 모든 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="76b2f-134">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="76b2f-134">IoT solution operator</span></span>
<span data-ttu-id="76b2f-135">IoT 솔루션 운영자 인 경우 아래 hello 모범 사례를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="76b2f-136">**시스템이 toodate 최신 유지**: 장치 운영 체제 및 모든 장치 드라이버는 업데이트 된 toohello 최신 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="76b2f-137">**악의적인 활동 으로부터 보호**: hello 운영 체제 허용 하는 경우 각 장치 운영 체제에 hello 최신 바이러스 백신 및 맬웨어 방지 기능을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="76b2f-138">**자주 감사**: 보안 관련 문제는 toosecurity 인시던트 응답 하는 경우 키에 대 한 IoT 인프라를 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="76b2f-139">**Hello IoT 인프라를 물리적으로 보호**: hello 최악의 IoT 인프라에 대 한 보안 공격 toodevices 물리적으로 액세스를 사용 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="76b2f-140">**클라우드 자격 증명을 보호**: 구성 및 작동 IoT 배포에 사용 되는 클라우드 인증 자격 증명 하는 가장 쉬운 방법은 toogain 액세스 hello 및 IoT 시스템을 손상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76b2f-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

