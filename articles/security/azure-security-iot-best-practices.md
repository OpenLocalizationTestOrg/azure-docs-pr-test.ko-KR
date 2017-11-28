---
title: "사물 인터넷 보안 모범 사례 | Microsoft Docs"
description: "이 문서는 엄선된 사물 인터넷 보안 모범 사례 및 일반 권장 사항입니다."
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
ms.openlocfilehash: 8efc0053458e338ac1afe98d9ce970c1d5cbfa81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="f4d26-103">사물 인터넷 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="f4d26-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="f4d26-104">IoT(사물 인터넷) 인프라 보안 유지는 IoT 솔루션과 관계된 사람들에게 중요한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-104">Securing the Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="f4d26-105">관련된 장치 수 및 이들 장치의 분산 특성 때문에 보안 사건으로 수백만 개의 IoT 장치가 손상되는 일이 발생 할 경우 그 영향은 심상치 않으며 광범위한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-105">Because of the number of devices involved and the distributed nature of these devices, the impact a security event related to compromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="f4d26-106">이런 이유로 IoT 보안은 심층적인 보안 접근 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="f4d26-107">데이터는 클라우드에서 그리고 개인 및 공유 네트워크로 이동할 때 안전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-107">Data needs to be secure in the cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="f4d26-108">메서드는 IoT 장치 자체를 안전하게 프로비전할 수 있게 마련되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-108">Methods need to be in place to securely provision the IoT devices themselves.</span></span> <span data-ttu-id="f4d26-109">장치에서 네트워크, 클라우드 백 엔드에 이르는 각 계층에서 강력한 보안 보장이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-109">Each layer, from device, to network, to cloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="f4d26-110">IoT 모범 사례는 다음과 같이 분류될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-110">IoT best practices can be categorized in the following way:</span></span>

* <span data-ttu-id="f4d26-111">IoT 하드웨어 제조업체 또는 통합업체</span><span class="sxs-lookup"><span data-stu-id="f4d26-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="f4d26-112">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="f4d26-112">IoT solution developer</span></span>
* <span data-ttu-id="f4d26-113">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="f4d26-113">IoT solution deployer</span></span>
* <span data-ttu-id="f4d26-114">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="f4d26-114">IoT solution operator</span></span>

<span data-ttu-id="f4d26-115">이 문서는 [사물 인터넷 보안 모범 사례](../iot-suite/iot-security-best-practices.md)를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="f4d26-116">자세한 정보는 그 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4d26-116">Please refer to that article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="f4d26-117">IoT 하드웨어 제조업체 또는 통합업체</span><span class="sxs-lookup"><span data-stu-id="f4d26-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="f4d26-118">IoT 하드웨어 제조업체 또는 하드웨어 통합업체는 아래의 모범 사례를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f4d26-118">Follow the best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="f4d26-119">**하드웨어의 최소 요구 사항 범위 설정**: 하드웨어 설계에는 하드웨어 운영에 필요한 최소한의 기능만 들어 있고 그 외에는 아무것도 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-119">**Scope hardware to minimum requirements**: the hardware design should include minimum features required for operation of the hardware, and nothing more.</span></span> 
* <span data-ttu-id="f4d26-120">**하드웨어 변조 방지**: 장치 커버를 열거나 장치 부품을 제거하는 등 하드웨어를 물리적으로 변조하는 행동을 감지하는 메커니즘을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-120">**Make hardware tamper proof**: build in mechanisms to detect physical tampering of hardware, such as opening the device cover, removing a part of the device, etc.</span></span> 
* <span data-ttu-id="f4d26-121">**보안 하드웨어를 중심으로 구축**: [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) 가 허용된다면 안전하게 암호화되는 저장소 및 TPM(신뢰할 수 있는 플랫폼 모듈) 기반 부팅 기능 같은 보안 기능을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="f4d26-122">**업그레이드 보안 강화**: 장치의 수명 동안 펌웨어 업그레이드는 피할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-122">**Make upgrades secure**: upgrading firmware during lifetime of the device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="f4d26-123">IoT 솔루션 개발자</span><span class="sxs-lookup"><span data-stu-id="f4d26-123">IoT solution developer</span></span>
<span data-ttu-id="f4d26-124">IoT 솔루션 개발자는 아래 모범 사례를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f4d26-124">Follow the best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="f4d26-125">**보안 소프트웨어 개발 방법론 준수**: 보안 소프트웨어를 개발하려면 프로젝트 시작부터 구현, 테스트 및 배포까지 처음부터 보안을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from the inception of the project all the way to its implementation, testing, and deployment.</span></span>
* <span data-ttu-id="f4d26-126">**신중하게 오픈 소스 소프트웨어 선택**: 오픈 소스 소프트웨어는 솔루션을 신속하게 개발할 수 있는 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-126">**Choose open source software with care**: open source software provides an opportunity to quickly develop solutions.</span></span>
* <span data-ttu-id="f4d26-127">**신중하게 통합**: 소프트웨어 보안 결함의 상당수가 라이브러리 및 API 경계에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-127">**Integrate with care**: many of the software security flaws exist at the boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="f4d26-128">IoT 솔루션 배포자</span><span class="sxs-lookup"><span data-stu-id="f4d26-128">IoT solution deployer</span></span>
<span data-ttu-id="f4d26-129">IoT 솔루션 배포자는 아래 모범 사례를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f4d26-129">Follow the best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="f4d26-130">**안전하게 하드웨어 배포**: IoT를 배포할 때 공공 장소나 감독되지 않는 현장처럼 안전하지 않은 위치에 하드웨어를 배포해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-130">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="f4d26-131">**인증 키를 안전하게 보관**: 배포하는 동안 각 장치에는 장치 ID 그리고 클라우드 서비스에서 생성하는 해당 ID와 연결된 인증 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="f4d26-132">배포 후에도 이러한 키를 물리적으로 안전하게 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-132">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="f4d26-133">손상된 키는 악의적인 장치에서 기존 장치로 위장하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-133">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="f4d26-134">IoT 솔루션 운영자</span><span class="sxs-lookup"><span data-stu-id="f4d26-134">IoT solution operator</span></span>
<span data-ttu-id="f4d26-135">IoT 솔루션 운영자는 아래 모범 사례를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f4d26-135">Follow the best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="f4d26-136">**시스템을 최신 상태로 유지**: 장치 운영 체제 및 모든 장치 드라이버를 최신 버전으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-136">**Keep systems up to date**: ensure device operating systems and all device drivers are updated to the latest versions.</span></span> 
* <span data-ttu-id="f4d26-137">**악의적인 활동으로부터 보호**: 운영 체제에서 허용하는 경우 각 장치 운영 체제에 최신 바이러스 백신 및 맬웨어 방지 기능을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-137">**Protect against malicious activity**: if the operating system permits, place the latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="f4d26-138">**자주 감사**: 보안 사고에 대응할 때에는 보안 관련 문제에 대한 IoT 인프라를 감사하는 것이 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding to security incidents.</span></span>
* <span data-ttu-id="f4d26-139">**IoT 인프라를 물리적으로 보호**: IoT 인프라에 대한 최악의 보안 공격은 장치에 물리적으로 액세스하여 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-139">**Physically protect the IoT infrastructure**: the worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span>
* <span data-ttu-id="f4d26-140">**클라우드 자격 증명 보호**: IoT 배포를 구성 및 운영하는 데 사용되는 클라우드 인증 자격 증명은 액세스 권한을 획득하고 IoT 시스템을 손상시킬 수 있는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d26-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> 

