---
title: "aaaSubscription Azure에서 Linux Vm에 대 한 계정 및 | Microsoft Docs"
description: "Hello 주요 디자인 및 구현에 대 한 지침이 구독 및 Azure에서 계정에 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Linux VM에 대한 Azure 구독 및 계정 지침

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

이 문서는 사용자 환경 및 사용자 기반으로 구독 및 계정 관리와 tooapproach 증가 하는 방법을 이해에 중점을 둡니다.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>구독 및 계정에 대한 구현 지침
의사 결정:

* 집합의 구독 및 계정 필요 한가요 toohost IT 작업 또는 인프라?
* 어떻게 hello 계층 toofit 아래로 toobreak 조직?

작업:

* Toomanage 원하는 만큼 논리적 구성이 계층 정의 구독 수준에서 합니다.
* toomatch이 논리적 계층 구조 필요한 hello 계정 및 각 계정 아래에서 구독을 정의 합니다.
* Hello 집합을 구독 및 명명 규칙을 사용 하 여 계정을 만듭니다.

## <a name="subscriptions-and-accounts"></a>구독 및 계정
Azure와 toowork, 하나 이상의 Azure 구독이 필요합니다. VM(가상 컴퓨터) 또는 가상 네트워크와 같은 리소스는 해당 구독에 존재합니다.

* 일반적으로 기업 고객은 hello 계층의 최상위 리소스 hello 되었고 관련된 tooone 또는 계정을 더는 기업 등록 계약을 가집니다.
* 소비자 및 기업 등록 없는 고객에 대 한 최상위 리소스 hello hello 계정입니다.
* 구독은 연결된 tooaccounts 있으며 계정당 구독을 하나 이상 있을 수 있습니다. Azure 레코드 hello 구독 수준에서 정보를 청구 합니다.

Hello 계정/구독 관계에 있는 두 명의 계층 수준의 toohello 제한을 인해 계정 및 구독 toohello 요구 청구의 중요 한 tooalign hello 명명 규칙은 것입니다. 예를 들어, 글로벌 기업에서 Azure를 사용 하는 경우 있습니다 수 toohave 하나 계정 / 지역당, 선택한 구독에서 관리 지역 수준을 hello:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

예를 들어, 다음 구조 hello를 사용할 수 있습니다.

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Hello ô ä ¢ 방법을 tooencode를 통합 해야 영역 toohave 둘 이상의 구독을 하나 관련된 tooa 특정 그룹을 경우 hello hello 계정 또는 hello 구독 이름에 추가 데이터입니다. 이 조직에 청구 보고서 중 청구 데이터 toogenerate hello 새 계층의 수준 massaging 허용 됩니다.

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

hello 조직 다음 예제는 hello와 같을 수 있습니다.

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

기업 계약의 단일 계정 또는 모든 계정에 대해 다운로드한 파일을 통해 자세한 청구를 제공합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

