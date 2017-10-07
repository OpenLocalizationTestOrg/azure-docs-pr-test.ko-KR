---
title: "사물 인터넷 (IoT Suite)에 대 한 aaaAzure 솔루션 | Microsoft Docs"
description: "샘플 솔루션 아키텍처 및 tooAzure IoT Suite 및 미리 구성 하는 hello 솔루션 관계를 포함 하 여 Azure에서 IoT의 개요입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: e527ca3f7541c84fbd6abc99ee38792468f88644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a>Azure IoT Suite
Microsoft Azure IoT Suite hello에 tooget 확장할 수 있는 미리 구성 된 솔루션의 집합을 통해 빠르게 시작할 수 있는 엔터프라이즈 수준의 솔루션입니다. 이러한 솔루션은 [원격 모니터링][lnk-preconfigured-solutions], [예측 유지 관리][lnk-predictive-maintenance] 및 [연결된 공장][lnk-connected-factory] 같은 일반적인 IoT 시나리오를 처리합니다. 이러한 솔루션은 hello이이 문서에 설명 된 IoT 솔루션 아키텍처의 구현입니다.

hello 미리 구성 된 솔루션이 완료 되 면 작업을 포함 하는 종단 간 솔루션:

- 시작한 장치 tooget을 시뮬레이션 합니다.
- 미리 구성된 Azure 서비스(예: [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning] 및 [Azure Storage][Azure storage])
- 솔루션 특정 관리 콘솔 

미리 구성 하는 hello 솔루션 검증 된, 프로덕션에 사용 가능한 코드에서 사용자 지정할 수 있으며 특정 사용자 고유의 IoT 시나리오 tooimplement 확장 포함 됩니다.

Hello에 관심이 있을 수 [Azure IoT Hub] [ Azure IoT Hub] hello 미리 구성 된 솔루션의 대부분을 사용 하는 서비스입니다. [Azure IoT Hub] [ Azure IoT Hub] 장치 및 미리 구성 하는 hello 솔루션 아키텍처에서 사용 하는 hello 클라우드 간의 hello 안전 하 고 신뢰할 수 있는 양방향 통신을 제공 합니다.

## <a name="next-steps"></a>다음 단계
이러한 리소스 toocontinue IoT Suite에 대 한 학습을 탐색 하 고 미리 구성 된 솔루션을 hello:

* [Azure IoT Suite란?][lnk-whatissuite]
* [Hello 미리 구성 된 Azure IoT Suite 솔루션은 무엇입니까?][lnk-whatarepreconfigured]

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md