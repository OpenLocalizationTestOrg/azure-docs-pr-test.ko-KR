---
title: "Azure의 IoT(사물 인터넷) 보안 | Microsoft Docs"
description: " Azure IoT(사물 인터넷) 서비스는 광범위한 기능을 제공합니다. 이 문서에서는 Azure에서 IoT 솔루션을 보호하는 방법을 이해하도록 도움을 줍니다. "
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
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="92f79-104">사물 인터넷 보안 개요</span><span class="sxs-lookup"><span data-stu-id="92f79-104">Internet of Things security overview</span></span>
<span data-ttu-id="92f79-105">Azure IoT(사물 인터넷) 서비스는 광범위한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="92f79-106">이러한 엔터프라이즈급 서비스를 사용하면 다음과 같은 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="92f79-107">장치에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="92f79-107">Collect data from devices</span></span>
* <span data-ttu-id="92f79-108">동작 내 데이터 스트림 분석</span><span class="sxs-lookup"><span data-stu-id="92f79-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="92f79-109">큰 데이터 집합 저장 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="92f79-109">Store and query large data sets</span></span>
* <span data-ttu-id="92f79-110">실시간 및 기록 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="92f79-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="92f79-111">백 오피스 시스템과 통합</span><span class="sxs-lookup"><span data-stu-id="92f79-111">Integrate with back-office systems</span></span>

<span data-ttu-id="92f79-112">이러한 기능을 제공하기 위해 Azure IoT Suite는 사용자 지정 확장이 포함된 여러 Azure 서비스를 미리 구성된 솔루션으로 패키지화했습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="92f79-113">이러한 미리 구성된 솔루션은 IoT 솔루션을 제공하는 데 걸릴 시간을 줄이는 데 도움이 되는 일반적인 IoT 솔루션 패턴의 기본 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="92f79-114">IoT 소프트웨어 개발자 키트를 통해 이러한 솔루션을 사용자 지정 및 확장하여 사용자의 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="92f79-115">또한 새로운 IoT 솔루션을 개발할 때 이러한 솔루션을 예제 또는 템플릿으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="92f79-116">Azure IoT Suite는 IoT 요구 사항에 대한 강력한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="92f79-117">그러나 IoT 솔루션은 처음부터 보안을 염두에 두고 설계되었다는 점이 가장 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="92f79-118">수많은 IoT 장치로 인해 보안 문제는 심각한 결과로 빠르게 광범위한 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="92f79-119">IoT 솔루션을 보호하는 방법을 이해할 수 있도록 다음과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="92f79-120">보안 아키텍처</span><span class="sxs-lookup"><span data-stu-id="92f79-120">Security architecture</span></span>
<span data-ttu-id="92f79-121">시스템을 디자인하고 아키텍처를 설계할 때 해당 시스템에 대한 잠재적 위협을 파악하고, 그에 따라 적절한 방어 수단을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="92f79-122">처음부터 보안을 염두에 두고 제품을 설계하는 것이 매우 중요합니다. 공격자가 시스템을 손상시킬 수 있는 방법을 파악하면 처음부터 적절한 위협 완화 조치를 수행할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="92f79-123">[사물 인터넷 보안 아키텍처](../iot-suite/iot-security-architecture.md)를 읽어 IoT 보안 아키텍처에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="92f79-124">이 문서는 다음 항목을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="92f79-125">보안은 위협 모델에서 출발</span><span class="sxs-lookup"><span data-stu-id="92f79-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="92f79-126">IoT의 보안</span><span class="sxs-lookup"><span data-stu-id="92f79-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="92f79-127">Azure IoT 참조 아키텍처 위협 모델링</span><span class="sxs-lookup"><span data-stu-id="92f79-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="92f79-128">처음부터 보안을 고려</span><span class="sxs-lookup"><span data-stu-id="92f79-128">Security from the ground up</span></span>
<span data-ttu-id="92f79-129">IoT는 전 세계 기업에 고유한 보안, 개인 정보 및 규정 준수 문제를 제기합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="92f79-130">문제가 소프트웨어와 구현 방식을 중심으로 발생하는 기존의 사이버 기술과는 달리 IoT는 사이버 세계와 실제 세계가 만날 때 일어나는 일과 관련하여 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="92f79-131">IoT 솔루션을 보호하기 위해서는 장치의 안전한 프로비전, 이러한 장치 및 클라우드 간의 보안 연결, 처리 및 저장 중에 클라우드에서 데이터 보호 설정이 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="92f79-132">그러나 이러한 기능에 대한 작업에는 리소스가 제한된 장치, 배포의 지리적 분산 및 솔루션 내 많은 수의 장치에 대한 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="92f79-133">[처음부터 사물 인터넷 보안](../iot-suite/securing-iot-ground-up.md)을 읽어 이러한 영역에서 보안을 처리하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="92f79-134">이 문서는 다음 항목을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="92f79-135">처음부터 보안 인프라</span><span class="sxs-lookup"><span data-stu-id="92f79-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="92f79-136">Microsoft Azure - 비즈니스를 위한 보안 IoT 인프라</span><span class="sxs-lookup"><span data-stu-id="92f79-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="92f79-137">모범 사례</span><span class="sxs-lookup"><span data-stu-id="92f79-137">Best Practices</span></span>
<span data-ttu-id="92f79-138">IoT 인프라를 보호하려면 엄격한 보안 심층 전략이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="92f79-139">클라우드의 데이터 보안부터 공용 인터넷을 통해 전송 중인 데이터 무결성을 보호하고 장치를 안전하게 프로비전하는 기능까지, 각 계층이 전체 인프라에서 우수한 보안을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="92f79-140">[사물 인터넷 보안 모범 사례](../iot-suite/iot-security-best-practices.md)를 읽어 사물 인터넷 보안 모범 사례에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="92f79-141">이 문서는 다음 항목을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92f79-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="92f79-142">IoT 하드웨어 제조업체/통합업체</span><span class="sxs-lookup"><span data-stu-id="92f79-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="92f79-143">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="92f79-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="92f79-144">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="92f79-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="92f79-145">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="92f79-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
