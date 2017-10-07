---
title: "Azure 자동화를 사용 하 여 Azure 키 자격 증명 모음 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 사용된 toomanage Azure 키 자격 증명 모음을 수 있는 방법에 대해 알아봅니다."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Azure 자동화를 사용하여 Azure 주요 자격 증명 모음 관리
이 가이드에서는 Azure 자동화 서비스 toohello 및 사용 되는 toosimplify 관리 키와 Azure 키 자격 증명 모음의 암호의 수 있는 방법을 소개 합니다.

## <a name="what-is-azure-automation"></a>Azure 자동화 정의
[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화 및 원하는 상태 구성을 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다. Azure 자동화를 사용 하 여 수동, 반복, 장기 실행 및 오류가 발생 하기 쉬운 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.

Azure 자동화 요구에 맞게 toomeet 크기가 조정 되는 매우 신뢰할 수 있으며, 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다. Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.

작동 오버 헤드를 줄이고 확보 IT DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Azure 자동화를 통해 Azure 주요 자격 증명 모음을 쉽게 관리하려면 어떻게 해야 하나요?
Hello를 사용 하 여 Azure 자동화에서 주요 자격 증명 모음을 관리할 수 있습니다 [AzureRM 키 자격 증명 모음 cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 및 [Azure 클래식 키 자격 증명 모음 cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)합니다. Azure 자동화에서 자동으로 사용할 수 없으면 기존 키 자격 증명 모음 관리 Azure 모듈 hello 및 hello를 가져올 수 있습니다 [AzureRM KeyVault 모듈](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) Azure 자동화로 다양 한 자격 증명 모음 키 관리를 수행할 수 있도록 hello 서비스 내에서 작업 합니다. 또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.

Hello Azure 키 자격 증명 모음 cmdlet과 함께 다른 규칙 으로부터 이러한 작업을 수행할 수 있습니다. 

* 주요 자격 증명 모음 만들기 및 구성
* 키 만들기 또는 가져오기
* 암호 만들기 또는 업데이트
* 키 특성 업데이트
* 키 또는 암호 가져오기
* 키 또는 암호 삭제

다음은 PowerShell toomanage 주요 자격 증명 모음을 사용 하 여 몇 가지 예입니다.  

* [Azure 주요 자격 증명 모음 - 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Azure 주요 자격 증명 모음 설정 및 구성](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>다음 단계
Azure 자동화 및 Azure 키 자격 증명 모음 사용된 toomanage 수 있는 방법의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.

* Azure 자동화 hello 참조 [초보자를 위한 자습서](../automation/automation-first-runbook-graphical.md)합니다.
* Hello 참조 [Azure 키 자격 증명 모음 PowerShell 스크립트를](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)합니다.

