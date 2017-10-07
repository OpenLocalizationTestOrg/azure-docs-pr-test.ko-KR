---
title: "Azure 자동화 데이터 aaaManaging | Microsoft Docs"
description: "이 문서는 Azure 자동화 환경 관리에 대한 여러 항목을 포함합니다.  현재 Azure 자동화에 데이터 보존 및 Azure 자동화 재해 복구 백업이 포함되어 있습니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Azure 자동화 데이터 관리
이 문서는 Azure 자동화 환경 관리에 대한 여러 항목을 포함합니다.

## <a name="data-retention"></a>데이터 보존
Azure 자동화에서 리소스를 삭제할 경우 영구적으로 제거하기 전에 감사를 위해 90일간 보존됩니다.  참조 하거나이 시간 동안 hello 리소스를 사용할 수 없습니다.  이 정책에는 삭제 된 tooan 자동화 계정에 속하는 tooresources도 적용 됩니다.

Azure 자동화는 90일이 넘은 작업을 자동으로 삭제하고 영구적으로 제거합니다.

다음 표에 hello 다른 리소스에 대 한 hello 보존 정책이 요약 되어 있습니다.

| Data | 정책 |
|:--- |:--- |
| 계정 |사용자가 hello 계정을 삭제 한 후 90 일을 영구적으로 제거 합니다. |
| 자산 |Hello asset 사용자가 삭제 되거나 계정이 hello 자산을 보유 하는 사용자가 삭제 hello 후 90 일 후 90 일을 영구적으로 제거 합니다. |
| 모듈 |Hello 모듈 사용자가 삭제 되거나 계정이 hello 모듈을 포함 하는 사용자가 삭제 hello 후 90 일 후 90 일이 지나면 영구적으로 제거 됩니다. |
| Runbook |Hello 리소스는 사용자가 삭제 되거나 계정이 hello 리소스를 보유 하는 사용자가 삭제 hello 후 90 일 후 90 일이 지나면 영구적으로 제거 됩니다. |
| 작업 |마지막으로 수정한지 90일이 지나면 삭제 및 영구 제거됩니다. Hello 작업 완료를 중지 또는 일시 중단 한 후 확인할 수 있습니다. |
| 노드 구성/MOF 파일 |이전 노드 구성은 새 노드 구성이 생성된 후 90일이 지나면 영구적으로 제거됩니다. |
| DSC 노드 |Hello 노드 Azure 포털 또는 hello를 사용 하 여 자동화 계정에서 등록 되지 않은 후 90 일이 지나면 영구적으로 제거 [등록 취소 AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) Windows powershell에서 cmdlet. 노드는 hello 노드는 사용자가 삭제를 보유 하는 hello 계정의 후 90 일도 영구적으로 제거 합니다. |
| 노드 보고서 |해당 노드에 대한 새 보고서가 생성된 후 90일이 지나면 영구적으로 제거됩니다. |

hello 보존 정책을 tooall 사용자가 적용 하 고 현재 사용자 지정할 수 없습니다.

그러나 더 긴 시간 동안 tooretain 데이터 해야 할 경우 runbook 작업 로그 tooLog 분석을 전달할 수 있습니다.  보다 자세한 정보를 검토 [Azure 자동화 작업 데이터 tooOMS 로그 분석 전달](automation-manage-send-joblogs-log-analytics.md)합니다.   

## <a name="backing-up-azure-automation"></a>Azure 자동화 백업
Microsoft Azure에서 자동화 계정을 삭제 하면 runbook, 모듈, 구성, 설정, 작업 및 자산을 포함 하 여 hello 계정에 개체를 모두 삭제 됩니다. hello 개체 hello 계정 삭제 된 후 복구할 수 없습니다.  Hello 자동화 계정 정보 toobackup hello 내용을 삭제 하기 전에 다음을 사용할 수 있습니다. 

### <a name="runbooks"></a>Runbook
Hello Azure 관리 포털 또는 hello를 사용 하 여 runbook tooscript 파일을 내보낼 수 [Get-azureautomationrunbookdefinition](https://msdn.microsoft.com/library/dn690269.aspx) Windows powershell에서 cmdlet.  [Runbook 만들기 또는 가져오기](https://msdn.microsoft.com/library/dn643637.aspx)에 설명된 것처럼 다른 자동화 계정으로 이러한 스크립트 파일을 가져올 수 있습니다.

### <a name="integration-modules"></a>통합 모듈
Azure 자동화에서는 통합 모듈을 내보낼 수 없습니다.  Hello 자동화 계정 외부에서 사용할 수 있는지 확인 해야 합니다.

### <a name="assets"></a>자산
Azure 자동화에서는 [자산](https://msdn.microsoft.com/library/dn939988.aspx) 을 내보낼 수 없습니다.  Hello Azure 관리 포털을 사용 하 여, 변수, 자격 증명, 인증서, 연결 및 일정의 hello 세부 정보 기록해 두어야 합니다.  그런 다음 다른 자동화로 가져온 Runbook에서 사용하는 자산을 수동으로 만들어야 합니다.

사용할 수 있습니다 [Azure cmdlet](https://msdn.microsoft.com/library/dn690262.aspx) 미래에 대 한 자산 암호화 되지 않은 한 저장의 tooretrieve 세부 정보를 참조 하거나 다른 자동화 계정에 해당 자산을 만듭니다.

암호화 된 변수 또는 cmdlet을 사용 하는 자격 증명의 hello 암호 필드에 대 한 hello 값을 검색할 수 없습니다.  이러한 값을 알 수 없는 경우 hello를 사용 하 여 runbook에서 검색할 수 있습니다 [Get-automationvariable](https://msdn.microsoft.com/library/dn940012.aspx) 및 [Get-automationpscredential](https://msdn.microsoft.com/library/dn940015.aspx) 활동입니다.

Azure 자동화에서는 인증서를 내보낼 수 없습니다.  Azure 외부에서 인증서를 사용할 수 있는지 확인해야 합니다.

### <a name="dsc-configurations"></a>DSC 구성
Hello Azure 관리 포털 또는 hello를 사용 하 여 구성을 tooscript 파일을 내보낼 수 [내보내기 AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) Windows powershell에서 cmdlet. 이러한 구성은 다른 자동화 계정에서 가져오고 사용할 수 있습니다.

## <a name="geo-replication-in-azure-automation"></a>Azure 자동화의 지역에서 복제
지리적 복제를 Azure 자동화 계정에는 표준 계정 데이터 tooa 다른 지리적 지역 중복 백업합니다. 사용자 계정을 설정할 때 기본 지역을 선택할 수 있습니다 및 다음 보조 지역 tooit 자동으로 할당 됩니다. 데이터 손실 된 경우에 hello 기본 지역에서 복사 하는 hello 보조 데이터를 지속적으로 새로 고쳐집니다.  

다음 표에서 hello hello 사용 가능한 기본 및 보조 지역 쌍을 보여 줍니다.

| 보조 | 주 |
| --- | --- |
| 미국 중남부 |미국 중북부 |
| 미국 동부 2 |미국 중부 |
| 서유럽 |북유럽 |
| 동남아시아 |동아시아 |
| 일본 동부 |일본 서부 |

Hello 흔하지 기본 지역 데이터 손실 된다는, Microsoft 시도 toorecover 것입니다. Hello 주 데이터를 복구할 수 없는 경우 지리적 장애 조치를 수행 하 고 hello 영향을 받는 고객 통해 알림을 받습니다이 대 한 구독.

