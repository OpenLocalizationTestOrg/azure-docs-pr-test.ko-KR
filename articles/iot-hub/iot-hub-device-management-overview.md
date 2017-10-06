---
title: "Azure IoT Hub와 aaaDevice 관리 | Microsoft Docs"
description: "Azure IoT Hub의 장치 관리에 대한 개요: 엔터프라이즈 장치 수명 주기 및 재부팅, 공장 재설정, 펌웨어 업데이트, 구성, 장치 배, 쿼리, 작업과 같은 장치 관리 패턴."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a><span data-ttu-id="fba32-103">IoT Hub를 사용한 장치 관리 개요</span><span class="sxs-lookup"><span data-stu-id="fba32-103">Overview of device management with IoT Hub</span></span>
## <a name="introduction"></a><span data-ttu-id="fba32-104">소개</span><span class="sxs-lookup"><span data-stu-id="fba32-104">Introduction</span></span>
<span data-ttu-id="fba32-105">Azure IoT Hub hello 기능과 장치 및 백 엔드 개발자 toobuild 강력한 장치 관리 솔루션을 사용 하도록 설정 하는 확장성 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-105">Azure IoT Hub provides hello features and an extensibility model that enable device and back-end developers toobuild robust device management solutions.</span></span> <span data-ttu-id="fba32-106">제한 된 센서 및 단일 용도 마이크로프로세서, 장치 그룹에 대 한 통신을 라우팅하는 toopowerful 게이트웨이에에서 장치 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-106">Devices range from constrained sensors and single purpose microcontrollers, toopowerful gateways that route communications for groups of devices.</span></span>  <span data-ttu-id="fba32-107">또한 hello 사용 사례 및 IoT 연산자에 대 한 요구 사항을 크게 다를 산업 분야입니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-107">In addition, hello use cases and requirements for IoT operators vary significantly across industries.</span></span>  <span data-ttu-id="fba32-108">이 변형을 불구 하 고 hello 기능, 패턴 및 코드 라이브러리 toocater tooa 다양 한 장치 및 최종 사용자에 게 IoT 허브를 사용 하 여 장치 관리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-108">Despite this variation, device management with IoT Hub provides hello capabilities, patterns, and code libraries toocater tooa diverse set of devices and end users.</span></span>

<span data-ttu-id="fba32-109">성공적인 전사적 IoT 솔루션을 만드는의 중요 한 부분 tooprovide 연산자 hello 지속적인 관리 장치 컬렉션을 처리 하는 방법을 대 한 전략은 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-109">A crucial part of creating a successful enterprise IoT solution is tooprovide a strategy for how operators handle hello ongoing management of their collection of devices.</span></span> <span data-ttu-id="fba32-110">IoT 연산자는 간단 하 고 신뢰할 수 있는 도구 및 응용 프로그램을 사용할 수 있도록 toofocus hello에 해당 작업의 더 많은 전략적 요소에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-110">IoT operators require simple and reliable tools and applications that enable them toofocus on hello more strategic aspects of their jobs.</span></span> <span data-ttu-id="fba32-111">이 문서는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-111">This article provides:</span></span>

* <span data-ttu-id="fba32-112">Azure IoT Hub 접근 방식 toodevice 관리에 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-112">A brief overview of Azure IoT Hub approach toodevice management.</span></span>
* <span data-ttu-id="fba32-113">일반적인 장치 관리 원칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="fba32-113">A description of common device management principles.</span></span>
* <span data-ttu-id="fba32-114">장치 수명 주기 hello에 대 한 설명</span><span class="sxs-lookup"><span data-stu-id="fba32-114">A description of hello device lifecycle.</span></span>
* <span data-ttu-id="fba32-115">일반적인 장치 관리 패턴의 개요</span><span class="sxs-lookup"><span data-stu-id="fba32-115">An overview of common device management patterns.</span></span>

## <a name="device-management-principles"></a><span data-ttu-id="fba32-116">장치 관리 원칙</span><span class="sxs-lookup"><span data-stu-id="fba32-116">Device management principles</span></span>
<span data-ttu-id="fba32-117">IoT 수 있도록 도와주는 고유한 부담감이 상당한 일련의 장치 관리 하 고 모든 엔터프라이즈 수준의 솔루션 hello 원칙에 따라 해결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-117">IoT brings with it a unique set of device management challenges and every enterprise-class solution must address hello following principles:</span></span>

![장치 관리 원칙 그래픽][img-dm_principles]

* <span data-ttu-id="fba32-119">**크기 조정 및 자동화**: IoT 솔루션 일상적인 작업을 자동화 하 고 상대적으로 작은 작업을 활성화 수 있는 간단한 도구 직원의 장치 수백만 toomanage가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-119">**Scale and automation**: IoT solutions require simple tools that can automate routine tasks and enable a relatively small operations staff toomanage millions of devices.</span></span> <span data-ttu-id="fba32-120">일상적인, 연산자 예상 toohandle 장치 작업 원격으로 대량에서 tooonly 직접 주의 기울여야 하는 문제가 발생 하면 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-120">Day-to-day, operators expect toohandle device operations remotely, in bulk, and tooonly be alerted when issues arise that require their direct attention.</span></span>
* <span data-ttu-id="fba32-121">**개방성 및 호환성**: hello 장치 에코 시스템은 매우 다양 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-121">**Openness and compatibility**: hello device ecosystem is extraordinarily diverse.</span></span> <span data-ttu-id="fba32-122">관리 도구에는 다양 한 장치 클래스, 플랫폼 및 프로토콜 맞춤형된 tooaccommodate 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-122">Management tools must be tailored tooaccommodate a multitude of device classes, platforms, and protocols.</span></span> <span data-ttu-id="fba32-123">연산자 수 있어야 toosupport 다양 한 유형의 장치 hello에서 가장 제한 된 포함 단일 프로세스 칩, toopowerful 및 컴퓨터를 완벽 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-123">Operators must be able toosupport many types of devices, from hello most constrained embedded single-process chips, toopowerful and fully functional computers.</span></span>
* <span data-ttu-id="fba32-124">**컨텍스트 인식**: IoT 환경은 동적이며 변화무쌍합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-124">**Context awareness**: IoT environments are dynamic and ever-changing.</span></span> <span data-ttu-id="fba32-125">서비스 안정성이 다른 무엇보다 가장 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-125">Service reliability is paramount.</span></span> <span data-ttu-id="fba32-126">장치 관리 작업 해당 유지 관리 계정 hello 요소 tooensure 다음을 고려해 야 합니다 가동 중지 시간이 중요 한 비즈니스 운영에 영향을 또는 위험한 조건을 만들 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-126">Device management operations must take into account hello following factors tooensure that maintenance downtime doesn't affect critical business operations or create dangerous conditions:</span></span>
    * <span data-ttu-id="fba32-127">SLA 유지 관리 기간</span><span class="sxs-lookup"><span data-stu-id="fba32-127">SLA maintenance windows</span></span>
    * <span data-ttu-id="fba32-128">네트워크 및 전력 상태</span><span class="sxs-lookup"><span data-stu-id="fba32-128">Network and power states</span></span>
    * <span data-ttu-id="fba32-129">사용 중인 조건</span><span class="sxs-lookup"><span data-stu-id="fba32-129">In-use conditions</span></span>
    * <span data-ttu-id="fba32-130">장치의 지리적 위치</span><span class="sxs-lookup"><span data-stu-id="fba32-130">Device geolocation</span></span>
* <span data-ttu-id="fba32-131">**여러 역할 서비스**: hello 고유 워크플로 및 프로세스의 IoT 작업 역할에 대 한 지원이 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-131">**Service many roles**: Support for hello unique workflows and processes of IoT operations roles is crucial.</span></span> <span data-ttu-id="fba32-132">hello 운영 담당자는 내부 IT 부서의 제약 조건이 지정 된 hello로 harmoniously 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-132">hello operations staff must work harmoniously with hello given constraints of internal IT departments.</span></span>  <span data-ttu-id="fba32-133">또한 유지 가능한 방법으로 toosurface 실시간 장치 작업 정보 toosupervisors 및 기타 비즈니스 관리 역할 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-133">They must also find sustainable ways toosurface realtime device operations information toosupervisors and other business managerial roles.</span></span>

## <a name="device-lifecycle"></a><span data-ttu-id="fba32-134">장치 수명 주기</span><span class="sxs-lookup"><span data-stu-id="fba32-134">Device lifecycle</span></span>
<span data-ttu-id="fba32-135">일련의 일반적인 tooall 엔터프라이즈 IoT 프로젝트는 일반 장치 관리 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-135">There is a set of general device management stages that are common tooall enterprise IoT projects.</span></span> <span data-ttu-id="fba32-136">Azure IoT는 hello 장치 수명 주기 내에서 5 단계:</span><span class="sxs-lookup"><span data-stu-id="fba32-136">In Azure IoT, there are five stages within hello device lifecycle:</span></span>

![hello 5 Azure IoT 장치 수명 주기 단계: 계획, 프로 비전, 구성, 모니터링, 사용 중지][img-device_lifecycle]

<span data-ttu-id="fba32-138">내 각 5 단계에서 fulfilled tooprovide 완벽 한 솔루션 이어야 하는 몇 가지 장치 연산자 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-138">Within each of these five stages, there are several device operator requirements that should be fulfilled tooprovide a complete solution:</span></span>

* <span data-ttu-id="fba32-139">**계획**: 연산자 toocreate tooeasily 정확 하 고에 대 한 쿼리 수 있게 해 주는 장치 메타 데이터 스키마를 사용 하도록 설정 하 고 대량 관리 작업에 대 한 장치 그룹을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-139">**Plan**: Enable operators toocreate a device metadata scheme that enables them tooeasily and accurately query for, and target a group of devices for bulk management operations.</span></span> <span data-ttu-id="fba32-140">이 장치 메타 데이터 태그 및 속성의 hello 형태로 hello 장치로 이중 toostore를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-140">You can use hello device twin toostore this device metadata in hello form of tags and properties.</span></span>
  
    <span data-ttu-id="fba32-141">*추가 정보*: [장치 트윈스 시작][lnk-twins-getstarted], [장치 트윈스 이해][lnk-twins-devguide], [방법 toouse 장치로 이중 속성][lnk-twin-properties]합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-141">*Further reading*: [Get started with device twins][lnk-twins-getstarted], [Understand device twins][lnk-twins-devguide], [How toouse device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="fba32-142">**프로 비전**: 안전 하 게 프로 비전 할 새 장치 tooIoT 허브를 사용 하도록 설정한 연산자 tooimmediately 장치 기능을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-142">**Provision**: Securely provision new devices tooIoT Hub and enable operators tooimmediately discover device capabilities.</span></span>  <span data-ttu-id="fba32-143">Hello IoT Hub identity 레지스트리 toocreate 유연한 장치 id 및 자격 증명을 수행 하이 작업을 대량 작업을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="fba32-143">Use hello IoT Hub identity registry toocreate flexible device identities and credentials, and perform this operation in bulk by using a job.</span></span> <span data-ttu-id="fba32-144">기능과 조건 hello 장치로 이중에서 장치 속성을 통해 장치 tooreport를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="fba32-144">Build devices tooreport their capabilities and conditions through device properties in hello device twin.</span></span>
  
    <span data-ttu-id="fba32-145">*추가 정보*: [장치 id를 관리][lnk-identity-registry], [관리 장치 id의 대량][lnk-bulk-identity], [어떻게 toouse 장치로 이중 속성][lnk-twin-properties]합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-145">*Further reading*: [Manage device identities][lnk-identity-registry], [Bulk management of device identities][lnk-bulk-identity], [How toouse device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="fba32-146">**구성**: 대량을 용이 하 게 구성 변경 및 펌웨어 toodevices 상태 및 보안을 모두 유지 하면서 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-146">**Configure**: Facilitate bulk configuration changes and firmware updates toodevices while maintaining both health and security.</span></span> <span data-ttu-id="fba32-147">원하는 속성 또는 직접 메서드와 브로드캐스트 작업을 사용하여 대량으로 이러한 장치 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-147">Perform these device management operations in bulk by using desired properties or with direct methods and broadcast jobs.</span></span>
  
    <span data-ttu-id="fba32-148">*추가 정보*: [직접 메서드를 사용 하 여][lnk-c2d-methods], [장치에서 직접 메서드를 호출][lnk-methods-devguide], [방법 toouse 장치로 이중 속성][lnk-twin-properties], [일정 및 브로드캐스트 작업][lnk-jobs], [여러장치에서작업을예약] [lnk-jobs-devguide].</span><span class="sxs-lookup"><span data-stu-id="fba32-148">*Further reading*:  [Use direct methods][lnk-c2d-methods], [Invoke a direct method on a device][lnk-methods-devguide], [How toouse device twin properties][lnk-twin-properties], [Schedule and broadcast jobs][lnk-jobs], [Schedule jobs on multiple devices][lnk-jobs-devguide].</span></span>
* <span data-ttu-id="fba32-149">**모니터**: 전반적인 장치 컬렉션 상태, 진행 중인 작업 및 경고 연산자 tooissues 주의 해야 할 수도 있는 hello 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-149">**Monitor**: Monitor overall device collection health, hello status of ongoing operations, and alert operators tooissues that might require their attention.</span></span>  <span data-ttu-id="fba32-150">Hello 장치로 이중 tooallow 장치 tooreport 실시간 작동 조건 및 업데이트 작업의 상태를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-150">Apply hello device twin tooallow devices tooreport realtime operating conditions and status of update operations.</span></span> <span data-ttu-id="fba32-151">빌드 강력한 대시보드 장치로 이중 쿼리를 사용 하 여 해당 표면 hello 대부분의 즉각적인 문제를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-151">Build powerful dashboard reports that surface hello most immediate issues by using device twin queries.</span></span>
  
    <span data-ttu-id="fba32-152">*추가 정보*: [어떻게 toouse 장치로 이중 속성][lnk-twin-properties], [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query-language].</span><span class="sxs-lookup"><span data-stu-id="fba32-152">*Further reading*: [How toouse device twin properties][lnk-twin-properties], [IoT Hub query language for device twins, jobs, and message routing][lnk-query-language].</span></span>
* <span data-ttu-id="fba32-153">**사용 중지**: 대체 또는 오류가 발생 한 후 장치를 서비스 해제, 주기, 업그레이드 또는 hello hello 서비스 수명이 끝날 때.</span><span class="sxs-lookup"><span data-stu-id="fba32-153">**Retire**:  Replace or decommission devices after a failure, upgrade cycle, or at hello end of hello service lifetime.</span></span>  <span data-ttu-id="fba32-154">물리적 장치 hello 되 고 있으면 hello 장치로 이중 toomaintain 장치 정보를 사용 하 여 교체 되거나 사용이 중지 될 경우에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-154">Use hello device twin toomaintain device info if hello physical device is being replaced, or archived if being retired.</span></span> <span data-ttu-id="fba32-155">장치 id 및 자격 증명을 안전 하 게 취소에 대 한 IoT Hub id 레지스트리에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-155">Use hello IoT Hub identity registry for securely revoking device identities and credentials.</span></span>
  
    <span data-ttu-id="fba32-156">*추가 정보*: [어떻게 toouse 장치로 이중 속성][lnk-twin-properties], [장치 id를 관리][lnk-identity-registry]합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-156">*Further reading*: [How toouse device twin properties][lnk-twin-properties], [Manage device identities][lnk-identity-registry].</span></span>

## <a name="device-management-patterns"></a><span data-ttu-id="fba32-157">장치 관리 패턴</span><span class="sxs-lookup"><span data-stu-id="fba32-157">Device management patterns</span></span>
<span data-ttu-id="fba32-158">IoT Hub에 장치 관리 패턴의 집합을 추적 하는 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-158">IoT Hub enables hello following set of device management patterns.</span></span>  <span data-ttu-id="fba32-159">hello [장치 관리 자습서] [ lnk-get-started] 방법을 더 자세하게에서 설명 tooextend 이러한 패턴 toofit 정확한 시나리오 및 이러한 이벤트에 대해 toodesign 새 패턴을 따라 하는 방법 핵심 템플릿.</span><span class="sxs-lookup"><span data-stu-id="fba32-159">hello [device management tutorials][lnk-get-started] show you in more detail how tooextend these patterns toofit your exact scenario and how toodesign new patterns based on these core templates.</span></span>

* <span data-ttu-id="fba32-160">**다시 부팅** -hello 백 엔드 응용 프로그램에 알립니다 hello 장치 직접 메서드를 통해 다시를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-160">**Reboot** - hello back-end app informs hello device through a direct method that it has initiated a reboot.</span></span>  <span data-ttu-id="fba32-161">hello 장치 사용 하 여 hello hello 장치의 속성 tooupdate hello 다시 부팅 상태를 보고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-161">hello device uses hello reported properties tooupdate hello reboot status of hello device.</span></span>
  
    ![장치 관리 다시 부팅 패턴 그래픽][img-reboot_pattern]
* <span data-ttu-id="fba32-163">**공장 재설정** -hello 백 엔드 응용 프로그램에 알립니다 hello 장치 직접 메서드를 통해 공장 재설정을 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-163">**Factory Reset** - hello back-end app informs hello device through a direct method that it has initiated a factory reset.</span></span>  <span data-ttu-id="fba32-164">hello 장치 사용 하 여 hello 속성 tooupdate hello 공장 재설정 hello 장치의 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-164">hello device uses hello reported properties tooupdate hello factory reset status of hello device.</span></span>
  
    ![장치 관리 공장 재설정 패턴 그래픽][img-facreset_pattern]
* <span data-ttu-id="fba32-166">**구성** -hello 백 엔드 응용 프로그램 hello 장치에서 실행 하는 hello 필요한 속성 tooconfigure 소프트웨어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-166">**Configuration** - hello back-end app uses hello desired properties tooconfigure software running on hello device.</span></span>  <span data-ttu-id="fba32-167">hello 장치 사용 하 여 hello hello 장치의 속성 tooupdate 구성 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-167">hello device uses hello reported properties tooupdate configuration status of hello device.</span></span>
  
    ![장치 관리 구성 패턴 그래픽][img-config_pattern]
* <span data-ttu-id="fba32-169">**펌웨어 업데이트** -hello 백 엔드 응용 프로그램에 알립니다 hello 장치 직접 메서드를 통해 펌웨어 업데이트를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-169">**Firmware Update** - hello back-end app informs hello device through a direct method that it has initiated a firmware update.</span></span>  <span data-ttu-id="fba32-170">여러 단계의 프로세스가 toodownload hello 펌웨어 이미지를 시작 하는 hello 장치 hello 펌웨어 이미지를 적용 한 toohello IoT 허브 서비스를 마지막으로 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-170">hello device initiates a multistep process toodownload hello firmware image, apply hello firmware image, and finally reconnect toohello IoT Hub service.</span></span>  <span data-ttu-id="fba32-171">Hello 다단계 프로세스 전체에서 hello 장치 사용 하 여 hello 속성 tooupdate hello 진행률과 hello 장치의 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-171">Throughout hello multistep process, hello device uses hello reported properties tooupdate hello progress and status of hello device.</span></span>
  
    ![장치 관리 펌웨어 업데이트 패턴 그래픽][img-fwupdate_pattern]
* <span data-ttu-id="fba32-173">**진행률 및 상태를 보고** -hello 솔루션 백 엔드는 장치, hello 상태에 tooreport 집합과 hello 장치에서 실행 되는 작업의 진행 상황에서 장치로 이중 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-173">**Reporting progress and status** - hello solution back end runs device twin queries, across a set of devices, tooreport on hello status and progress of actions running on hello devices.</span></span>
  
    ![장치 관리 보고 진행률 및 상태 패턴 그래픽][img-report_progress_pattern]

## <a name="next-steps"></a><span data-ttu-id="fba32-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fba32-175">Next Steps</span></span>
<span data-ttu-id="fba32-176">hello 기능, 패턴 및 장치 관리에 대 한 IoT 허브를 제공 하는 코드 라이브러리는 각 장치 수명 주기 단계 내에서 엔터프라이즈 IoT 연산자 요구 사항을 충족 하는 toocreate IoT 응용 프로그램 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-176">hello capabilities, patterns, and code libraries that IoT Hub provides for device management, enable you toocreate IoT applications that fulfill enterprise IoT operator requirements within each device lifecycle stage.</span></span>

<span data-ttu-id="fba32-177">IoT Hub에서 장치 관리 기능을 hello에 대 한 학습 toocontinue 참조 hello [장치 관리 시작] [ lnk-get-started] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="fba32-177">toocontinue learning about hello device management features in IoT Hub, see hello [Get started with device management][lnk-get-started] tutorial.</span></span>

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
