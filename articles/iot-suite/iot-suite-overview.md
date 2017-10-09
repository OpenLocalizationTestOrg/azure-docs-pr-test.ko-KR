---
title: "aaaMicrosoft Azure IoT Suite 개요 | Microsoft Docs"
description: "Azure IoT Suite 가지 미리 구성 된 솔루션 toocollect의 인터넷을 배달 하는 방법의 개요를 분석 및 데이터를 저장, 시각화를 제공 및 다른 시스템과 통합 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="89739-103">Azure IoT Suite의 개요</span><span class="sxs-lookup"><span data-stu-id="89739-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="89739-104">hello Azure 인터넷 IoT (사물) 서비스의 다양 한 범위의 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="89739-105">이러한 엔터프라이즈급 서비스를 사용하면 다음과 같은 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89739-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="89739-106">장치에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="89739-106">Collect data from devices</span></span>
* <span data-ttu-id="89739-107">동작 내 데이터 스트림 분석</span><span class="sxs-lookup"><span data-stu-id="89739-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="89739-108">큰 데이터 집합 저장 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="89739-108">Store and query large data sets</span></span>
* <span data-ttu-id="89739-109">실시간 및 기록 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="89739-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="89739-110">백 오피스 시스템과 통합</span><span class="sxs-lookup"><span data-stu-id="89739-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="89739-111">장치 관리</span><span class="sxs-lookup"><span data-stu-id="89739-111">Manage your devices</span></span>

<span data-ttu-id="89739-112">toodeliver 이러한 기능, Azure IoT Suite 패키지으로 사용자 지정 확장을 사용 하 여 여러 Azure 서비스 함께 *솔루션 미리 구성 된*합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="89739-113">이러한 미리 구성 된 솔루션은 tooreduce hello 시간 IoT 솔루션 toodeliver 수행 하는 데 도움이 되는 일반적인 IoT 솔루션 패턴의 기본 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="89739-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="89739-114">Hello를 사용 하 여 [IoT 소프트웨어 개발 키트][lnk-sdks]를 사용자 지정할 수 있으며 이러한 솔루션 toomeet 사용자의 요구 사항을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89739-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="89739-115">또한 새로운 IoT 솔루션을 개발할 때 이러한 솔루션을 예제 또는 템플릿으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89739-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="89739-116">hello 다음 비디오에서는 소개 tooAzure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="89739-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="89739-117">Azure IoT Suite에서 Azure IoT 서비스</span><span class="sxs-lookup"><span data-stu-id="89739-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="89739-118">미리 구성 하는 hello 솔루션은 일반적으로 서비스를 수행 하는 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="89739-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="89739-119">코어 tooAzure IoT Suite는 hello [Azure IoT Hub] [ lnk-iot-hub] 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="89739-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="89739-120">이 서비스는 hello 장치-클라우드 및 클라우드 다른 키 IoT Suite 서비스 hello 메시징 기능을 클라우드-장치 및 게이트웨이 toohello hello 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="89739-121">hello 서비스 tooreceive 메시지 배율 사용할 때 장치를 사용 하면 및 tooyour 장치 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89739-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="89739-122">hello 서비스 하면 수도 너무[장치를 관리 하][lnk-device-management]합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="89739-123">예를 들어, 구성 컴퓨터를 다시 부팅 하거나 하나 이상의 장치 연결 된 toohello 허브에서 공장 재설정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89739-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="89739-124">[Azure Stream Analytics][lnk-asa]는 모션 내 데이터 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="89739-125">서비스 tooprocess 들어오는 원격 분석을 사용 하 여 IoT Suite, 집계를 수행 하 고 이벤트 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="89739-126">또한 미리 구성 하는 hello 솔루션 스트림 분석 tooprocess 정보 메시지 장치에서 메타 데이터 또는 명령 응답 등의 데이터를 포함 하는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="89739-127">hello 솔루션 사용 하 여 장치에서 스트림 분석 tooprocess hello 메시지 및 tooother 서비스 해당 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="89739-128">[Azure 저장소] [ lnk-azure-storage] 및 [Azure Cosmos DB] [ lnk-document-db] hello 데이터 저장소 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="89739-129">hello 미리 구성 된 솔루션을 사용 하 고 toomake blob 저장소 toostore 원격 분석에 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="89739-130">hello Cosmos DB toostore 장치 메타 데이터를 사용 하 여 솔루션과 hello 솔루션의 hello 장치 관리 기능을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="89739-131">[Azure 웹 앱] [ lnk-web-apps] 및 [Microsoft Power BI] [ lnk-power-bi] hello 데이터 시각화 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="89739-132">Power BI의 hello 유연성을 사용 하면 tooquickly IoT Suite 데이터를 사용 하는 사용자 고유의 대화형 대시보드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="89739-133">일반적인 IoT 솔루션의 hello 아키텍처의 개요를 참조 하십시오. [Microsoft Azure 및 인터넷 IoT (사물) hello][iot-suite-what-is-azure-iot]합니다.</span><span class="sxs-lookup"><span data-stu-id="89739-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="89739-134">미리 구성된 솔루션</span><span class="sxs-lookup"><span data-stu-id="89739-134">Preconfigured solutions</span></span>

<span data-ttu-id="89739-135">IoT Suite 미리 구성 된 솔루션에 포함 된 해당 있습니다 tooquickly 시작 설정 및 일반적인 IoT 시나리오와 같은 hello tooexplore:</span><span class="sxs-lookup"><span data-stu-id="89739-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="89739-136">원격 모니터링</span><span class="sxs-lookup"><span data-stu-id="89739-136">Remote monitoring</span></span>
* <span data-ttu-id="89739-137">예측 유지 관리</span><span class="sxs-lookup"><span data-stu-id="89739-137">Predictive maintenance</span></span>
* <span data-ttu-id="89739-138">연결된 공장</span><span class="sxs-lookup"><span data-stu-id="89739-138">Connected factory</span></span>

<span data-ttu-id="89739-139">이러한 솔루션 tooyour Azure 구독을 배포 하 고 완전 한 종단 간 IoT 시나리오를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89739-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89739-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89739-140">Next steps</span></span>

<span data-ttu-id="89739-141">IoT Suite 수행할 수 있는 란 무엇 이며 해당 기본 구성 요소에 대 한 개요를가지고 학습할 수 있는 미리 구성 하는 hello 솔루션 IoT Suite에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="89739-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="89739-142">자세한 내용은 참조 [솔루션 미리 구성 된 Azure IoT hello 무엇 인가요?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="89739-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
