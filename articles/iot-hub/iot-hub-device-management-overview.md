---
title: "Azure IoT Hub 장치 관리 | Microsoft Docs"
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
ms.openlocfilehash: 6d667d42bfef2ec61b055009210d5621f51c17df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a><span data-ttu-id="6b601-103">IoT Hub를 사용한 장치 관리 개요</span><span class="sxs-lookup"><span data-stu-id="6b601-103">Overview of device management with IoT Hub</span></span>
## <a name="introduction"></a><span data-ttu-id="6b601-104">소개</span><span class="sxs-lookup"><span data-stu-id="6b601-104">Introduction</span></span>
<span data-ttu-id="6b601-105">Azure IoT Hub는 장치 및 백 엔드 개발자가 강력한 장치 관리 솔루션을 빌드할 수 있도록 하는 기능 및 확장성 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-105">Azure IoT Hub provides the features and an extensibility model that enable device and back-end developers to build robust device management solutions.</span></span> <span data-ttu-id="6b601-106">장치의 범위는 제한된 센서 및 단일 목적 마이크로컨트롤러에서 다수의 장치에 대한 통신을 라우팅하는 강력한 게이트웨이까지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-106">Devices range from constrained sensors and single purpose microcontrollers, to powerful gateways that route communications for groups of devices.</span></span>  <span data-ttu-id="6b601-107">또한 IoT 운영자의 사용 사례 및 요구 사항은 여러 산업에 따라 크게 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-107">In addition, the use cases and requirements for IoT operators vary significantly across industries.</span></span>  <span data-ttu-id="6b601-108">이 변형에도 불구하고 IoT Hub 장치 관리는 기능, 패턴 및 코드 라이브러리를 다양한 장치 및 최종 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-108">Despite this variation, device management with IoT Hub provides the capabilities, patterns, and code libraries to cater to a diverse set of devices and end users.</span></span>

<span data-ttu-id="6b601-109">성공적인 기업 IoT 솔루션을 만드는 데 있어 중요한 부분은 운영자가 다수의 장치를 지속적으로 관리하는 방법에 대한 전략을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-109">A crucial part of creating a successful enterprise IoT solution is to provide a strategy for how operators handle the ongoing management of their collection of devices.</span></span> <span data-ttu-id="6b601-110">IoT 운영자는 업무 중 보다 전략적인 측면에 중점을 둘 수 있는 간단하고 안정적인 도구와 응용 프로그램을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-110">IoT operators require simple and reliable tools and applications that enable them to focus on the more strategic aspects of their jobs.</span></span> <span data-ttu-id="6b601-111">이 문서는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-111">This article provides:</span></span>

* <span data-ttu-id="6b601-112">장치 관리에 대한 Azure IoT Hub 접근 방식의 간략한 개요</span><span class="sxs-lookup"><span data-stu-id="6b601-112">A brief overview of Azure IoT Hub approach to device management.</span></span>
* <span data-ttu-id="6b601-113">일반적인 장치 관리 원칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="6b601-113">A description of common device management principles.</span></span>
* <span data-ttu-id="6b601-114">장치 수명 주기에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="6b601-114">A description of the device lifecycle.</span></span>
* <span data-ttu-id="6b601-115">일반적인 장치 관리 패턴의 개요</span><span class="sxs-lookup"><span data-stu-id="6b601-115">An overview of common device management patterns.</span></span>

## <a name="device-management-principles"></a><span data-ttu-id="6b601-116">장치 관리 원칙</span><span class="sxs-lookup"><span data-stu-id="6b601-116">Device management principles</span></span>
<span data-ttu-id="6b601-117">IoT는 특유의 장치 관리 과제를 수반하며 모든 기업 수준의 솔루션은 다음과 같은 원칙을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-117">IoT brings with it a unique set of device management challenges and every enterprise-class solution must address the following principles:</span></span>

![장치 관리 원칙 그래픽][img-dm_principles]

* <span data-ttu-id="6b601-119">**규모 및 자동화**: IoT 솔루션은 일상적인 작업을 자동화할 수 있는 간단한 도구를 필요로 하며 비교적 적은 수의 운영 담당자가 수백만 대의 장치를 관리할 수 있도록 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-119">**Scale and automation**: IoT solutions require simple tools that can automate routine tasks and enable a relatively small operations staff to manage millions of devices.</span></span> <span data-ttu-id="6b601-120">운영자는 매일 원격에서 일괄적으로 장치 작업을 처리하고 운영자가 주의를 기울여야 하는 문제가 발생할 때만 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-120">Day-to-day, operators expect to handle device operations remotely, in bulk, and to only be alerted when issues arise that require their direct attention.</span></span>
* <span data-ttu-id="6b601-121">**개방성 및 호환성**: 장치 생태계는 매우 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-121">**Openness and compatibility**: The device ecosystem is extraordinarily diverse.</span></span> <span data-ttu-id="6b601-122">관리 도구는 다수의 장치 클래스, 플랫폼 및 프로토콜을 수용하도록 조정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-122">Management tools must be tailored to accommodate a multitude of device classes, platforms, and protocols.</span></span> <span data-ttu-id="6b601-123">운영자는 가장 제한된 내장형 단일 프로세스 칩에서 강력하고 완벽하게 작동하는 컴퓨터에 이르는 많은 종류의 장치를 지원할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-123">Operators must be able to support many types of devices, from the most constrained embedded single-process chips, to powerful and fully functional computers.</span></span>
* <span data-ttu-id="6b601-124">**컨텍스트 인식**: IoT 환경은 동적이며 변화무쌍합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-124">**Context awareness**: IoT environments are dynamic and ever-changing.</span></span> <span data-ttu-id="6b601-125">서비스 안정성이 다른 무엇보다 가장 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-125">Service reliability is paramount.</span></span> <span data-ttu-id="6b601-126">장치 관리 작업은 유지 관리 중단 시간이 중대한 비즈니스 작업에 영향을 미치거나 위험한 상황을 만들지 않도록 다음 요소를 감안해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-126">Device management operations must take into account the following factors to ensure that maintenance downtime doesn't affect critical business operations or create dangerous conditions:</span></span>
    * <span data-ttu-id="6b601-127">SLA 유지 관리 기간</span><span class="sxs-lookup"><span data-stu-id="6b601-127">SLA maintenance windows</span></span>
    * <span data-ttu-id="6b601-128">네트워크 및 전력 상태</span><span class="sxs-lookup"><span data-stu-id="6b601-128">Network and power states</span></span>
    * <span data-ttu-id="6b601-129">사용 중인 조건</span><span class="sxs-lookup"><span data-stu-id="6b601-129">In-use conditions</span></span>
    * <span data-ttu-id="6b601-130">장치의 지리적 위치</span><span class="sxs-lookup"><span data-stu-id="6b601-130">Device geolocation</span></span>
* <span data-ttu-id="6b601-131">**많은 역할 서비스**: IoT 운영 역할 특유의 워크플로와 프로세스에 대한 지원이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-131">**Service many roles**: Support for the unique workflows and processes of IoT operations roles is crucial.</span></span> <span data-ttu-id="6b601-132">운영 담당자는 내부 IT 부서에 주어진 제약 조건에 맞도록 작업을 진행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-132">The operations staff must work harmoniously with the given constraints of internal IT departments.</span></span>  <span data-ttu-id="6b601-133">또한 실시간 장치 운영 정보를 감독자 및 기타 관리 역할 담당자에게 표면화시키는 지속 가능한 방법을 찾아내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-133">They must also find sustainable ways to surface realtime device operations information to supervisors and other business managerial roles.</span></span>

## <a name="device-lifecycle"></a><span data-ttu-id="6b601-134">장치 수명 주기</span><span class="sxs-lookup"><span data-stu-id="6b601-134">Device lifecycle</span></span>
<span data-ttu-id="6b601-135">모든 기업 IoT 프로젝트에 공통된 일련의 일반 장치 관리 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-135">There is a set of general device management stages that are common to all enterprise IoT projects.</span></span> <span data-ttu-id="6b601-136">Azure IoT의 장치 수명 주기 내에는 5단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-136">In Azure IoT, there are five stages within the device lifecycle:</span></span>

![5개의 Azure IoT 장치 수명 주기 단계는 계획, 구축, 구성, 모니터링, 사용 중지입니다.][img-device_lifecycle]

<span data-ttu-id="6b601-138">다섯 단계 각각에서 완벽한 솔루션을 제공하기 위해 충족해야 하는 여러 가지 장치 연산자 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-138">Within each of these five stages, there are several device operator requirements that should be fulfilled to provide a complete solution:</span></span>

* <span data-ttu-id="6b601-139">**계획**: 운영자가 대량 관리 작업을 위해 장치 그룹을 간편하고 정확하게 대상화하고 쿼리하기 위한 장치 메타데이터 구성표를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-139">**Plan**: Enable operators to create a device metadata scheme that enables them to easily and accurately query for, and target a group of devices for bulk management operations.</span></span> <span data-ttu-id="6b601-140">장치 쌍을 사용하여 이 장치 메타데이터를 태그 및 속성 형식으로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-140">You can use the device twin to store this device metadata in the form of tags and properties.</span></span>
  
    <span data-ttu-id="6b601-141">*추가 정보*: [장치 쌍 시작][lnk-twins-getstarted], [장치 쌍 이해][lnk-twins-devguide], [장치 쌍 속성 사용 방법][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="6b601-141">*Further reading*: [Get started with device twins][lnk-twins-getstarted], [Understand device twins][lnk-twins-devguide], [How to use device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="6b601-142">**프로비전**: 새 장치를 IoT Hub에 안전하게 프로비전하고 운영자가 장치의 기능을 즉시 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-142">**Provision**: Securely provision new devices to IoT Hub and enable operators to immediately discover device capabilities.</span></span>  <span data-ttu-id="6b601-143">IoT Hub ID 레지스트리를 사용하여 유연한 장치 ID 및 자격 증명을 만들고 작업을 사용하여 대량으로 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-143">Use the IoT Hub identity registry to create flexible device identities and credentials, and perform this operation in bulk by using a job.</span></span> <span data-ttu-id="6b601-144">장치 쌍에서 장치 속성을 통해 기능 및 조건을 보고하도록 장치를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-144">Build devices to report their capabilities and conditions through device properties in the device twin.</span></span>
  
    <span data-ttu-id="6b601-145">*추가 정보*: [장치 ID 관리][lnk-identity-registry], [장치 ID 대량 관리][lnk-bulk-identity], [장치 쌍 속성 사용 방법][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="6b601-145">*Further reading*: [Manage device identities][lnk-identity-registry], [Bulk management of device identities][lnk-bulk-identity], [How to use device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="6b601-146">**구성**: 정상적인 상태와 보안을 유지하면서 장치에 대한 일괄 구성 변경 및 펌웨어 업데이트를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-146">**Configure**: Facilitate bulk configuration changes and firmware updates to devices while maintaining both health and security.</span></span> <span data-ttu-id="6b601-147">원하는 속성 또는 직접 메서드와 브로드캐스트 작업을 사용하여 대량으로 이러한 장치 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-147">Perform these device management operations in bulk by using desired properties or with direct methods and broadcast jobs.</span></span>
  
    <span data-ttu-id="6b601-148">*추가 정보*:  [직접 메서드 사용][lnk-c2d-methods], [장치에서 직접 메서드 호출][lnk-methods-devguide], [장치 쌍 속성 사용 방법][lnk-twin-properties], [작업 예약 및 브로드캐스트][lnk-jobs], [여러 장치에서 작업 예약][lnk-jobs-devguide]</span><span class="sxs-lookup"><span data-stu-id="6b601-148">*Further reading*:  [Use direct methods][lnk-c2d-methods], [Invoke a direct method on a device][lnk-methods-devguide], [How to use device twin properties][lnk-twin-properties], [Schedule and broadcast jobs][lnk-jobs], [Schedule jobs on multiple devices][lnk-jobs-devguide].</span></span>
* <span data-ttu-id="6b601-149">**모니터링**: 전반적인 다수의 장치 상태와 현재 작업 상태를 모니터링하고 주의가 필요한 문제를 운영자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-149">**Monitor**: Monitor overall device collection health, the status of ongoing operations, and alert operators to issues that might require their attention.</span></span>  <span data-ttu-id="6b601-150">장치 쌍을 적용하여 장치 업데이트 작업의 상태를 실시간 운영 상태를 보고할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-150">Apply the device twin to allow devices to report realtime operating conditions and status of update operations.</span></span> <span data-ttu-id="6b601-151">장치 쌍 쿼리를 사용하여 즉각적인 문제를 노출하는 강력한 대시보드 보고서를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-151">Build powerful dashboard reports that surface the most immediate issues by using device twin queries.</span></span>
  
    <span data-ttu-id="6b601-152">*추가 정보*: [장치 쌍 속성 사용 방법][lnk-twin-properties], [장치 쌍, 작업 및 메시지 라우팅의 IoT Hub 쿼리 언어][lnk-query-language]</span><span class="sxs-lookup"><span data-stu-id="6b601-152">*Further reading*: [How to use device twin properties][lnk-twin-properties], [IoT Hub query language for device twins, jobs, and message routing][lnk-query-language].</span></span>
* <span data-ttu-id="6b601-153">**사용 중지**: 오류가 발생하거나, 업그레이드 주기 후에 또는 서비스 수명 주기가 끝나면 장치를 교체하거나 서비스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-153">**Retire**:  Replace or decommission devices after a failure, upgrade cycle, or at the end of the service lifetime.</span></span>  <span data-ttu-id="6b601-154">장치 쌍을 사용하여 물리적 장치를 바꾸는 경우 장치 정보를 유지하거나 사용이 중지될 경우 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-154">Use the device twin to maintain device info if the physical device is being replaced, or archived if being retired.</span></span> <span data-ttu-id="6b601-155">IoT Hub ID 레지스트리를 사용하여 장치 ID 및 자격 증명을 안전하게 해지합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-155">Use the IoT Hub identity registry for securely revoking device identities and credentials.</span></span>
  
    <span data-ttu-id="6b601-156">*추가 정보*: [장치 쌍 속성 사용 방법][lnk-twin-properties], [장치 ID 관리][lnk-identity-registry]</span><span class="sxs-lookup"><span data-stu-id="6b601-156">*Further reading*: [How to use device twin properties][lnk-twin-properties], [Manage device identities][lnk-identity-registry].</span></span>

## <a name="device-management-patterns"></a><span data-ttu-id="6b601-157">장치 관리 패턴</span><span class="sxs-lookup"><span data-stu-id="6b601-157">Device management patterns</span></span>
<span data-ttu-id="6b601-158">IoT Hub는 다음과 같은 장치 관리 패턴을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-158">IoT Hub enables the following set of device management patterns.</span></span>  <span data-ttu-id="6b601-159">[장치 관리 자습서][lnk-get-started]에서는 정확한 시나리오에 맞도록 이러한 패턴을 확장하는 방법 및 이러한 핵심 템플릿을 기반으로 새 패턴을 디자인하는 방법을 자세히 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-159">The [device management tutorials][lnk-get-started] show you in more detail how to extend these patterns to fit your exact scenario and how to design new patterns based on these core templates.</span></span>

* <span data-ttu-id="6b601-160">**다시 부팅** - 백 엔드 앱은 직접 메서드를 통해 다시 부팅이 시작된 것을 장치에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-160">**Reboot** - The back-end app informs the device through a direct method that it has initiated a reboot.</span></span>  <span data-ttu-id="6b601-161">장치는 보고된 속성을 사용하여 장치의 재부팅 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-161">The device uses the reported properties to update the reboot status of the device.</span></span>
  
    ![장치 관리 다시 부팅 패턴 그래픽][img-reboot_pattern]
* <span data-ttu-id="6b601-163">**공장 재설정** - 백 엔드 앱은 직접 메서드를 통해 공장 재설정이 시작된 것을 장치에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-163">**Factory Reset** - The back-end app informs the device through a direct method that it has initiated a factory reset.</span></span>  <span data-ttu-id="6b601-164">장치는 보고된 속성을 사용하여 장치의 공장 재설정 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-164">The device uses the reported properties to update the factory reset status of the device.</span></span>
  
    ![장치 관리 공장 재설정 패턴 그래픽][img-facreset_pattern]
* <span data-ttu-id="6b601-166">**구성** - 백 엔드 앱은 필요한 속성을 사용하여 장치에서 실행 중인 소프트웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-166">**Configuration** - The back-end app uses the desired properties to configure software running on the device.</span></span>  <span data-ttu-id="6b601-167">장치는 보고된 속성을 사용하여 장치의 구성 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-167">The device uses the reported properties to update configuration status of the device.</span></span>
  
    ![장치 관리 구성 패턴 그래픽][img-config_pattern]
* <span data-ttu-id="6b601-169">**펌웨어 업데이트** - 백 엔드 앱은 직접 메서드를 통해 펌웨어 업데이트를 시작한 것을 장치에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-169">**Firmware Update** - The back-end app informs the device through a direct method that it has initiated a firmware update.</span></span>  <span data-ttu-id="6b601-170">장치는 펌웨어 이미지를 다운로드하는 다단계 프로세스를 시작하고, 펌웨어 이미지를 적용하고, 마지막으로 IoT Hub 서비스에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-170">The device initiates a multistep process to download the firmware image, apply the firmware image, and finally reconnect to the IoT Hub service.</span></span>  <span data-ttu-id="6b601-171">다단계 프로세스가 진행되는 동안, 장치는 보고된 속성을 사용하여 진행률과 장치의 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-171">Throughout the multistep process, the device uses the reported properties to update the progress and status of the device.</span></span>
  
    ![장치 관리 펌웨어 업데이트 패턴 그래픽][img-fwupdate_pattern]
* <span data-ttu-id="6b601-173">**진행률 및 상태 보고** - 솔루션 백 엔드는 장치에서 실행 중인 작업의 상태와 진행률을 보고하기 위하여 일련의 장치 전반에 대해 장치 쌍 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-173">**Reporting progress and status** - The solution back end runs device twin queries, across a set of devices, to report on the status and progress of actions running on the devices.</span></span>
  
    ![장치 관리 보고 진행률 및 상태 패턴 그래픽][img-report_progress_pattern]

## <a name="next-steps"></a><span data-ttu-id="6b601-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b601-175">Next Steps</span></span>
<span data-ttu-id="6b601-176">IoT Hub에서 장치 관리를 위해 제공하는 기능, 패턴 및 코드 라이브러리를 사용하면 각 장치 수명 주기 단계에서 기업 IoT 운영자 요구 사항을 충족하는 IoT 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b601-176">The capabilities, patterns, and code libraries that IoT Hub provides for device management, enable you to create IoT applications that fulfill enterprise IoT operator requirements within each device lifecycle stage.</span></span>

<span data-ttu-id="6b601-177">IoT Hub 장치 관리 기능에 대해 계속 알아보려면 [장치 관리 시작][lnk-get-started] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b601-177">To continue learning about the device management features in IoT Hub, see the [Get started with device management][lnk-get-started] tutorial.</span></span>

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
