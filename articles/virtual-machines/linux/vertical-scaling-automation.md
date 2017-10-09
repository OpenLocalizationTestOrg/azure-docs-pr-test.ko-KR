---
title: "aaaVertically 배율 Azure 자동화 인 Azure 가상 컴퓨터 | Microsoft Docs"
description: "Toovertically 응답 toomonitoring 알림 Azure 자동화에서 Linux 가상 컴퓨터를을 조절 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>Azure Automation을 사용하여 Azure Linux 가상 컴퓨터를 수직으로 확장
세로 배율는 증가 또는 감소 응답 toohello 작업에서 컴퓨터의 hello 리소스의 hello 프로세스입니다. Azure의 hello 가상 컴퓨터의 hello 크기를 변경 하 여 수행할 수 있습니다. 이 hello 다음 시나리오에에서 도움이 될 수 있습니다.

* 가상 컴퓨터 hello 자주 사용 하지 않으면, 조정할 수 있습니다 더 작은 크기 tooreduce tooa 아래로 월별 비용
* 수 hello 가상 컴퓨터는 최대 부하를 보고 하는 경우 크기가 조정 된 tooa 더 큰 크기 tooincrease 용량과 수

이 목록은 hello 단계 tooaccomplish에 대 한 hello 개요 아래

1. Azure 자동화 tooaccess 가상 컴퓨터 설정
2. 구독에 hello Azure 자동화 세로 배율 runbook 가져오기
3. Webhook tooyour runbook 추가
4. 경고는 tooyour 가상 컴퓨터를 추가 합니다.

> [!NOTE]
> Hello hello 크기 때문에 첫 번째 가상 컴퓨터를 확장할 수 있습니다 hello 크기 제한 될 수 있습니다 hello의 가용성을 toohello 인해 hello 클러스터에 다른 크기 현재 가상 컴퓨터 배포에 합니다. Hello이이 경우 처리 하 고 VM 크기 쌍 아래 hello 내로 확장할이 문서에서 사용 하는 자동화 runbook을 게시 합니다. 이 있음을 의미 Standard_D1v2 가상 컴퓨터는 하지 갑자기 수 tooStandard_G5 수직 확장 tooBasic_A0 축소 합니다.
> 
> | VM 크기 조정 쌍 |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Azure 자동화 tooaccess 가상 컴퓨터 설정
hello가 가장 먼저 해야 toodo hello 사용 되는 runbook tooscale hello VM 크기 집합 인스턴스를 호스팅하는 Azure 자동화 계정 만들기. 최근에 hello 자동화 서비스는 hello 서비스 사용자 설치를 위해 자동으로 실행 중인 hello runbook hello 사용자 대신 매우 쉽게 hello "계정으로 실행" 기능을 소개 했습니다. 자세한 내용은 아래 hello 기술 자료 문서에서이 내용을:

* [Azure 실행 계정으로 Runbook 인증](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>구독에 hello Azure 자동화 세로 배율 runbook 가져오기
가상 컴퓨터에 이미 게시 되어 수직 확장에 필요한 hello runbook hello Azure 자동화 Runbook 갤러리입니다. Tooimport 해야 구독에 해당 합니다. 다음 문서를 읽음으로써 tooimport runbook hello 하는 방법을 배울 수 있습니다.

* [Azure 자동화용 Runbook 및 모듈 갤러리](../../automation/automation-runbook-gallery.md)

가져온 toobe 해야 하는 hello runbook hello 이미지 아래에 표시 됩니다.

![Runbook 가져오기](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Webhook tooyour runbook 추가
Hello runbook을 가져온 후 가상 컴퓨터에서 발생 한 경고에 의해 트리거될 수 있으므로 tooadd webhook toohello runbook 야 합니다. Runbook에 대 한는 webhook를 만드는 hello 세부 정보는 여기에 읽을 수합니다 있습니다.

* [Azure 자동화 Webhook](../../automation/automation-webhooks.md)

Hello 다음 섹션에서이 필요 하므로 hello webhook 대화 상자를 닫기 전에 hello webhook을 복사 하 고 있는지 확인 합니다.

## <a name="add-an-alert-tooyour-virtual-machine"></a>경고는 tooyour 가상 컴퓨터를 추가 합니다.
1. 가상 컴퓨터 설정 선택
2. "경고 규칙" 선택
3. "경고 추가" 선택
4. 메트릭 toofire hello 경고를 선택 합니다.
5. 조건을 선택할 수 있는 경우에 수행 됩니다 hello 경고 toofire 발생
6. 5 단계에서에서 hello 조건에 대 한 임계값을 선택 합니다. fulfilled toobe
7. 5 단계 및 6에서 hello 조건 및 임계값에 대 한 어떤 hello를 통해 모니터링 서비스는 확인 기간을 선택 합니다.
8. Hello 이전 섹션에서 복사한 hello webhook에 붙여 넣습니다.

![경고 tooVirtual 컴퓨터 1 추가](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![경고 tooVirtual 컴퓨터 2 추가](./media/vertical-scaling-automation/add-alert-webhook-2.png)

