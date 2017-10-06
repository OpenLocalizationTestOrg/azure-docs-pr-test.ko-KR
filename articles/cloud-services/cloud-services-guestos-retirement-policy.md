---
title: "Azure 게스트 OS에 대 한 aaaSupportability 및 사용 중지 정책 가이드 | Microsoft Docs"
description: "Microsoft는 클라우드 서비스에서 사용 하는 Azure 게스트 OS toohello 관련 지원에 대 한 정보를 제공 합니다."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Azure 게스트 OS 지원 가능성 및 사용 중지 정책
이 페이지의 hello 정보 관련 toohello Azure 게스트 운영 체제 ([게스트 OS](cloud-services-guestos-update-matrix.md)) 클라우드 서비스 작업자 및 웹 역할 (PaaS)에 대 한 합니다. TooVirtual 컴퓨터 (IaaS)은 적용 되지 않습니다.

Microsoft는 게시 된 [hello 게스트 OS에 대 한 지원 정책](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq)합니다. 이제이 읽고 있는 hello 페이지 hello 정책을 구현 하는 방법을 설명 합니다.

hello 정책

1. Microsoft는 지원 **이상 hello 게스트 OS의 두 가지 최신 제품군 hello**합니다. 제품군이 사용 중지 하는 경우 고객 hello 공식 사용 중지 날짜 tooupdate tooa 새 지원 되는 게스트 OS 제품군 로부터 12 개월 동안 해야 합니다.
2. Microsoft는 지원 **hello 지원 게스트 OS 제품군의 최신 두 버전 이상 hello**합니다.
3. Microsoft는 지원 **최소한 최근 2 가지 버전의 Azure SDK hello hello**합니다. 하면 한 버전의 SDK를 사용 중지 하는 hello 고객 hello 공식 사용 중지 날짜 tooupdate tooa 최신 버전부터 12 개월을 갖게 됩니다.

세 개 이상의 제품군 또는 릴리스가 지원되는 경우도 있습니다. 공식 게스트 OS 지원 정보가 hello에 나타납니다. [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](cloud-services-guestos-update-matrix.md)합니다.

## <a name="when-a-guest-os-family-or-version-is-retired"></a>게스트 OS 제품군 또는 버전 사용 중지된 경우
새 게스트 OS **제품군** hello hello Windows Server 운영 체제의 새 공식 버전이 출시 후 얼마 동안 도입 되었습니다. 새 게스트 OS 제품군이 제공 될 때마다 Microsoft hello 가장 오래 된 게스트 OS 제품군 사용 중지 됩니다.

새 게스트 OS **버전** 모든 달 tooincorporate hello 최신 MSRC 업데이트에 대 한 소개 합니다. Hello 정기적으로 매월 업데이트는 게스트 OS 버전 이므로는 출시 후 60 일이 지나면 일반적으로 비활성화 합니다. 사용할 수 있는 각 제품군에 대해 최소 두 버전의 게스트 OS를 유지합니다.

### <a name="process-during-a-guest-os-family-retirement"></a>게스트 OS 제품군 사용 중지 시 프로세스
Hello 사용 중지가 발표 된 후 고객은 서비스에서 hello 이전 제품군이 공식적으로 제거 하기 전에 12 개월 "전환" 기간을 갖습니다. 이 전환 기간은 Microsoft의 hello 판단에 따라 확장할 수 있습니다. 업데이트가 hello에 게시 될 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](cloud-services-guestos-update-matrix.md)합니다.

단계적 사용 중지 프로세스는 6 (6) 개월 hello 전환 기간으로 시작 됩니다. 이 기간 동안:

1. Microsoft은 hello 사용 중지의 고객을 게 알립니다.
2. hello hello Azure SDK의 최신 버전 사용 중지 하는 hello 게스트 OS 제품군을 지원 하지 않습니다.
3. 새로운 배포 및 클라우드 서비스의 재배포가 허용 되지 않습니다 hello 사용 중지 된 제품군에서

Microsoft는 toointroduce hello hello "만료 날짜" 라고 hello 전환 기간의 마지막 날까지 최신 MSRC 업데이트 hello를 통합 하는 새 게스트 OS 버전을 계속 합니다. Hello 만료 날짜에 실행 중인 클라우드 서비스는 hello Azure SLA 따라 지원 되지 것입니다. Microsoft는 hello 신중 하 게 tooforce 업그레이드, 삭제 또는 해당 날짜 이후에 해당 서비스를 중지 합니다.

### <a name="process-during-a-guest-os-version-retirement"></a>게스트 OS 버전 사용 중지 시 프로세스
고객이 자신의 게스트 OS tooautomatically 업데이트를 설정 하지 있는데 tooworry 처리 게스트 OS 버전에 대 한 항상 사용할 hello 최신 게스트 OS 버전입니다.

게스트 OS 버전은 매달 출시됩니다. Hello 정기적인 릴리스 속도로 인해 각 버전이 마다 고정된 수명이 있습니다.

Hello 수명 60 일,는 버전은 "*비활성화*"입니다. "비활성화" 의미 hello 포털에서 해당 hello 버전을 제거 합니다. hello 버전 hello CSCFG 구성 파일에서 더 이상 설정할 수 없습니다. 기존 배포는 계속 실행됩니다. 하지만 새 배포 및 코드 및 구성 업데이트 tooexisting 배포 허용 되지 않습니다.

잠시 후 되 고 "비활성화" hello 게스트 OS 버전 "*만료*" 되며 해당 버전을 실행 중인 모든 설치가 강제로 업그레이드 이후 hello에 tooautomatically 업데이트 hello 게스트 OS를 설정 합니다. 만료는 hello 기간 동안 사용할 수 없는 상태 tooexpiration에서 달라질 수 있으므로 일괄 처리로 수행 됩니다.

이러한 기간 연장 될 수 있습니다에 Microsoft의 재량에 따라 tooease 고객 전환 합니다. Hello에서 변경 내용을 알려 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](cloud-services-guestos-update-matrix.md)합니다.

### <a name="notifications-during-retirement"></a>사용 중지 시 알림
* **제품군 사용 중지** <br>Microsoft는 블로그 게시물 및 포털 알림을 사용합니다. 사용 중지 된 게스트 OS 제품군을 여전히 사용 되는 고객 (전자 메일, 포털 메시지, 전화 통화) 직접 통신 tooassigned 서비스 관리자를 통해 알림을 받게 됩니다. Toothis 페이지와 hello RSS 피드가이 페이지의 hello 시작 부분에 나열 된 모든 변경 내용은 게시 됩니다.
* **버전 사용 중지** <br>모든 변경 내용 및 발생 하는 hello 날짜 toothis 페이지와 hello RSS 피드 릴리스, 사용 안 함, 및 만료를 포함 하 여이 페이지의 hello 시작 부분에 나열 된 게시 됩니다. 서비스 관리자는 비활성화된 게스트 OS 버전 또는 제품군에서 실행 되는 배포가 있는 경우 전자 메일을 받게 됩니다. 이러한 전자 메일의 hello 타이밍 달라질 수 있습니다. 일반적으로 비활성화되기 최소 1개월 전이지만 이 시기는 공식 SLA는 없습니다.

## <a name="frequently-asked-questions"></a>질문과 대답
**마이그레이션의 hello 영향을 줄일 수는 방법**

Cloud Services를 디자인하기 위한 최신 게스트 OS 제품군을 사용하는 것이 좋습니다.

1. 마이그레이션 tooa 최신 제품군을 초기 계획을 시작 합니다.
2. Hello 새 제품군에서 실행 중인 클라우드 서비스 배포 tootest 임시 테스트를 설정 합니다.
3. 게스트 OS 버전을 너무 설정**자동** (osVersion = * hello에 [.cscfg](cloud-services-model-and-package.md#cscfg) 파일) 하므로 hello 마이그레이션 toonew 게스트 OS 버전을 자동으로 발생 합니다.

**경우에 어떻게 웹 응용 프로그램 내 사용 hello OS와 밀접 하 게 통합을 필요 합니다.**

Hello 운영 체제의 기본 기능에 종속 되는 웹 응용 프로그램 아키텍처를 사용 하 여 플랫폼 지원 기능 등 [시작 작업](cloud-services-startup-tasks.md) 또는 다른 확장성 메커니즘입니다. 또는 사용할 수도 있습니다 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS (서비스), 중인 운영 체제 기본 hello를 유지 관리 해야 합니다.

## <a name="next-steps"></a>다음 단계
검토 hello 최신 [게스트 OS 릴리스와](cloud-services-guestos-update-matrix.md)합니다.
