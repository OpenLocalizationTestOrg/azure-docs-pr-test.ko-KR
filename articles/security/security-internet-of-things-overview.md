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
# <a name="internet-of-things-security-overview"></a>사물 인터넷 보안 개요
Azure IoT(사물 인터넷) 서비스는 광범위한 기능을 제공합니다. 이러한 엔터프라이즈급 서비스를 사용하면 다음과 같은 작업을 할 수 있습니다.

* 장치에서 데이터 수집
* 동작 내 데이터 스트림 분석
* 큰 데이터 집합 저장 및 쿼리
* 실시간 및 기록 데이터 시각화
* 백 오피스 시스템과 통합

이러한 기능, Azure IoT Suite 함께 패키지 toodeliver 여러 Azure 서비스 사용자 지정 확장 프로그램으로 미리 구성 된 솔루션으로 합니다. 이러한 미리 구성 된 솔루션은 tooreduce hello 시간 IoT 솔루션 toodeliver 수행 하는 데 도움이 되는 일반적인 IoT 솔루션 패턴의 기본 구현입니다. Hello IoT 소프트웨어 개발 키트를 사용 하 여 사용자 지정할 수 있으며 이러한 솔루션 toomeet 사용자의 요구 사항을 확장할 수도 있습니다. 또한 새로운 IoT 솔루션을 개발할 때 이러한 솔루션을 예제 또는 템플릿으로 사용할 수도 있습니다.

hello Azure IoT suite는 IoT 요구 사항에 대 한 강력한 솔루션입니다. 그러나, 것이 가장 중요 하면 IoT 솔루션에서 hello 시작 보안 설계 되었습니다. Hello 수가 너무 많아 IoT 장치, 때문에 보안 문제 중요 한 결과 사용 하 여 광범위 한 이벤트를 신속 하 게 될 수 있습니다.

알아야 toohelp 어떻게 toosecure 하면 IoT 솔루션 했으므로 다음 정보는 hello 합니다.

## <a name="security-architecture"></a>보안 아키텍처
시스템을 디자인할 때 중요 한 toounderstand hello 잠재적 위협 toothat 시스템 이며 hello 시스템을 디자인 하 고 설계 하는 대로 적절 한 방어를 적절 하 게 추가 합니다. Toodesign 적절 한 완화 hello 처음부터 현재 위치에 있는지 확인 하는 사용 하면 공격자는 시스템 수 toocompromise 수 있습니다 어떻게 이해 하기 때문에 보안을 염두 hello 시작에서 제품을 hello 유용 합니다.

[사물 인터넷 보안 아키텍처](../iot-suite/iot-security-architecture.md)를 읽어 IoT 보안 아키텍처에 대해 알아볼 수 있습니다.

이 문서에서는 다음 항목 hello를 설명 합니다.

* [보안은 위협 모델에서 출발](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [IoT의 보안](../iot-suite/iot-security-architecture.md#security-in-iot)
* [위협 모델링 hello Azure IoT 참조 아키텍처](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Hello 접지에서 보안
hello IoT 헤드로 고유한 보안, 개인 정보 보호 및 규정 준수 문제 toobusinesses 전 세계 있습니다. 여기서 이러한 문제를 중심으로 소프트웨어 및 구현 하는 전통적인 사이버 기술, 달리 IoT hello 사이버 및 hello 실제 세계 수렴 하는 경우와 관련 됩니다. IoT 솔루션 보호 장치, 이러한 장치 및 hello 클라우드 및 처리 및 저장 시 hello 클라우드에서 데이터의 보안 보호 간의 보안 연결의 보안 프로 비전 되었는지 확인 해야 합니다. 그러나 이러한 기능에 대한 작업에는 리소스가 제한된 장치, 배포의 지리적 분산 및 솔루션 내 많은 수의 장치에 대한 작업이 포함됩니다.

학습할 수 있는 방법을 읽어 이러한 영역에서 toohandle 보안 [hello 접지에서 사물 인터넷 보안](../iot-suite/securing-iot-ground-up.md)합니다.

hello 문서에서는 다음 항목 hello를 설명 합니다.

* [Hello 접지에서 안전한 인프라](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure - 비즈니스를 위한 보안 IoT 인프라](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>모범 사례
IoT 인프라를 보호하려면 엄격한 보안 심층 전략이 필요합니다. 보안에서 공용 인터넷을 toosecurely 프로 비전 장치, 각 계층에서 보안을 보증 큰 빌드 hello 통해 전송 되에서는 동안 데이터 무결성을 보호 하는 hello 클라우드에서 데이터 hello 전체 인프라입니다.

[사물 인터넷 보안 모범 사례](../iot-suite/iot-security-best-practices.md)를 읽어 사물 인터넷 보안 모범 사례에 대해 알아볼 수 있습니다.

hello 문서에서는 다음 항목 hello를 설명 합니다.

* [IoT 하드웨어 제조업체/통합업체](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [IoT 솔루션 개발자](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [IoT 솔루션 배포자](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [IoT 솔루션 운영자](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
