---
title: "aaaSecure 프로그램 인터넷 IoT (사물) Azure에서 | Microsoft Docs"
description: " Azure IoT(사물 인터넷) 서비스는 광범위한 기능을 제공합니다. 이 문서에서는 이해 하는 데 어떻게 toosecure azure에서 IoT 솔루션입니다. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="f9f14-104">사물 인터넷 보안 개요</span><span class="sxs-lookup"><span data-stu-id="f9f14-104">Internet of Things security overview</span></span>
<span data-ttu-id="f9f14-105">Azure IoT(사물 인터넷) 서비스는 광범위한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="f9f14-106">이러한 엔터프라이즈급 서비스를 사용하면 다음과 같은 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="f9f14-107">장치에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="f9f14-107">Collect data from devices</span></span>
* <span data-ttu-id="f9f14-108">동작 내 데이터 스트림 분석</span><span class="sxs-lookup"><span data-stu-id="f9f14-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="f9f14-109">큰 데이터 집합 저장 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="f9f14-109">Store and query large data sets</span></span>
* <span data-ttu-id="f9f14-110">실시간 및 기록 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="f9f14-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="f9f14-111">백 오피스 시스템과 통합</span><span class="sxs-lookup"><span data-stu-id="f9f14-111">Integrate with back-office systems</span></span>

<span data-ttu-id="f9f14-112">이러한 기능, Azure IoT Suite 함께 패키지 toodeliver 여러 Azure 서비스 사용자 지정 확장 프로그램으로 미리 구성 된 솔루션으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="f9f14-113">이러한 미리 구성 된 솔루션은 tooreduce hello 시간 IoT 솔루션 toodeliver 수행 하는 데 도움이 되는 일반적인 IoT 솔루션 패턴의 기본 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="f9f14-114">Hello IoT 소프트웨어 개발 키트를 사용 하 여 사용자 지정할 수 있으며 이러한 솔루션 toomeet 사용자의 요구 사항을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="f9f14-115">또한 새로운 IoT 솔루션을 개발할 때 이러한 솔루션을 예제 또는 템플릿으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="f9f14-116">hello Azure IoT suite는 IoT 요구 사항에 대 한 강력한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="f9f14-117">그러나, 것이 가장 중요 하면 IoT 솔루션에서 hello 시작 보안 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="f9f14-118">Hello 수가 너무 많아 IoT 장치, 때문에 보안 문제 중요 한 결과 사용 하 여 광범위 한 이벤트를 신속 하 게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="f9f14-119">알아야 toohelp 어떻게 toosecure 하면 IoT 솔루션 했으므로 다음 정보는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="f9f14-120">보안 아키텍처</span><span class="sxs-lookup"><span data-stu-id="f9f14-120">Security architecture</span></span>
<span data-ttu-id="f9f14-121">시스템을 디자인할 때 중요 한 toounderstand hello 잠재적 위협 toothat 시스템 이며 hello 시스템을 디자인 하 고 설계 하는 대로 적절 한 방어를 적절 하 게 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="f9f14-122">Toodesign 적절 한 완화 hello 처음부터 현재 위치에 있는지 확인 하는 사용 하면 공격자는 시스템 수 toocompromise 수 있습니다 어떻게 이해 하기 때문에 보안을 염두 hello 시작에서 제품을 hello 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="f9f14-123">[사물 인터넷 보안 아키텍처](../iot-suite/iot-security-architecture.md)를 읽어 IoT 보안 아키텍처에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="f9f14-124">이 문서에서는 다음 항목 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="f9f14-125">보안은 위협 모델에서 출발</span><span class="sxs-lookup"><span data-stu-id="f9f14-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="f9f14-126">IoT의 보안</span><span class="sxs-lookup"><span data-stu-id="f9f14-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="f9f14-127">위협 모델링 hello Azure IoT 참조 아키텍처</span><span class="sxs-lookup"><span data-stu-id="f9f14-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="f9f14-128">Hello 접지에서 보안</span><span class="sxs-lookup"><span data-stu-id="f9f14-128">Security from hello ground up</span></span>
<span data-ttu-id="f9f14-129">hello IoT 헤드로 고유한 보안, 개인 정보 보호 및 규정 준수 문제 toobusinesses 전 세계 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="f9f14-130">여기서 이러한 문제를 중심으로 소프트웨어 및 구현 하는 전통적인 사이버 기술, 달리 IoT hello 사이버 및 hello 실제 세계 수렴 하는 경우와 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="f9f14-131">IoT 솔루션 보호 장치, 이러한 장치 및 hello 클라우드 및 처리 및 저장 시 hello 클라우드에서 데이터의 보안 보호 간의 보안 연결의 보안 프로 비전 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="f9f14-132">그러나 이러한 기능에 대한 작업에는 리소스가 제한된 장치, 배포의 지리적 분산 및 솔루션 내 많은 수의 장치에 대한 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="f9f14-133">학습할 수 있는 방법을 읽어 이러한 영역에서 toohandle 보안 [hello 접지에서 사물 인터넷 보안](../iot-suite/securing-iot-ground-up.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="f9f14-134">hello 문서에서는 다음 항목 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="f9f14-135">Hello 접지에서 안전한 인프라</span><span class="sxs-lookup"><span data-stu-id="f9f14-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="f9f14-136">Microsoft Azure - 비즈니스를 위한 보안 IoT 인프라</span><span class="sxs-lookup"><span data-stu-id="f9f14-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="f9f14-137">모범 사례</span><span class="sxs-lookup"><span data-stu-id="f9f14-137">Best Practices</span></span>
<span data-ttu-id="f9f14-138">IoT 인프라를 보호하려면 엄격한 보안 심층 전략이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="f9f14-139">보안에서 공용 인터넷을 toosecurely 프로 비전 장치, 각 계층에서 보안을 보증 큰 빌드 hello 통해 전송 되에서는 동안 데이터 무결성을 보호 하는 hello 클라우드에서 데이터 hello 전체 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="f9f14-140">[사물 인터넷 보안 모범 사례](../iot-suite/iot-security-best-practices.md)를 읽어 사물 인터넷 보안 모범 사례에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="f9f14-141">hello 문서에서는 다음 항목 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f14-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="f9f14-142">IoT 하드웨어 제조업체/통합업체</span><span class="sxs-lookup"><span data-stu-id="f9f14-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="f9f14-143">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="f9f14-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="f9f14-144">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="f9f14-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="f9f14-145">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="f9f14-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
