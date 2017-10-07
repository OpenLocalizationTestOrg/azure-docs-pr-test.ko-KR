---
title: "Azure 백업에서 파일 및 폴더의 aaaTroubleshoot 느린 백업을 | Microsoft Docs"
description: "제공 Azure 백업 성능 문제의 원인 hello 진단 지침 toohelp 문제 해결"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Azure 백업에서 파일 및 폴더의 느린 백업 문제 해결
이 문서에서는 문제 해결 지침을 제공 toohelp Azure 백업을 사용 하는 파일 및 폴더에 대 한 백업 성능 저하의 hello 원인을 진단 합니다. 파일을 Azure 백업 에이전트 tooback hello를 사용 하는 경우에 백업 프로세스 hello 예상 보다 오래 걸릴 수 있습니다. 이 지연 hello 다음 중 하나 이상을 원인일 수 있습니다.

* [성능 병목 상태를 백업 하는 hello 컴퓨터에 있습니다.](#cause1)
* [다른 프로세스 또는 바이러스 백신 소프트웨어가 hello Azure 백업 프로세스에 방해가 됩니다.](#cause2)
* [hello 백업 에이전트는 Azure 가상 컴퓨터 (VM)에서 실행 됩니다.](#cause3)  
* [많은 수(수백만 개)의 파일을 백업하는 경우](#cause4)

다운로드 하 고 hello를 설치 하는 권장 문제 해결을 시작 하기 전에 [최신 Azure 백업 에이전트](http://aka.ms/azurebackup_agent)합니다. 에서는 자주 업데이트 toohello 백업 에이전트 toofix 다양 한 문제를 확인, 기능을 추가 및 성능을 향상 합니다.

또한 좋습니다 hello를 검토 하는 [Azure 백업 서비스 FAQ](backup-azure-backup-faq.md) toomake hello 일반적인 구성 문제가 발생 하지 하면 있는지 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Hello 컴퓨터에 성능 병목 현상을 원인:
병목 상태를 백업 하는 hello 컴퓨터에 지연이 발생할 수 있습니다. 예를 들어 컴퓨터의 능력 tooread 또는 쓰기 toodisk hello 또는 hello 네트워크를 통해 사용 가능한 대역폭 toosend 데이터 병목 현상이 발생할 수 있습니다.

Windows에서 호출 되는 기본 제공 도구가 제공 [성능 모니터](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect 이러한 병목 상태입니다.

다음은 최적의 백업을 위해 병목 현상을 진단하는 데 도움이 될 수 있는 몇 가지 성능 카운터 및 범위입니다.

| 카운터 | 가동 상태 |
| --- | --- |
| Logical Disk(Physical Disk)--%idle |• 100% 유휴 too50% 유휴 = 정상</br>• 49% 유휴 too20% 유휴 = 경고 또는 모니터</br>• 19% 유휴 too0% 유휴 = 위험 또는 부재 중 사양 |
| 논리 디스크(실제 디스크)--%평균 Disk Sec Read or Write |• 0.001 ms too0.015 ms = 정상</br>• 0.015 ms too0.025 ms = 경고 또는 모니터</br>• 0.026ms 이상 = 위험 또는 사양을 벗어남 |
| 논리 디스크(실제 디스크)--현재 디스크 큐 길이(모든 인스턴스) |6분이 넘는 시간 동안 80개 요청 |
| Memory--Pool Non Paged Bytes |• 사용된 풀의 60% 미만 = 정상<br>사용 된 풀의 • 61% too80% = 경고 또는 모니터</br>• 사용된 풀의 80% 초과 = 위험 또는 사양을 벗어남 |
| Memory--Pool Paged Bytes |• 사용된 풀의 60% 미만 = 정상</br>사용 된 풀의 • 61% too80% = 경고 또는 모니터</br>• 사용된 풀의 80% 초과 = 위험 또는 사양을 벗어남 |
| Memory--Available Megabytes |• 사용 가능한 여유 메모리의 50% 이상 = 정상</br>• 사용 가능한 여유 메모리의 25% = 모니터링</br>• 사용 가능한 여유 메모리의 10% = 경고</br>• 사용 가능한 여유 메모리의 100MB 또는 5% 미만 = 위험 또는 사양을 벗어남 |
| Processor--\%%Processor Time(모든 인스턴스) |• 60% 미만 사용 = 정상</br>• 61% too90% 사용 모니터 또는 주의 =</br>• 91% too100% 소모 위험 = |

> [!NOTE]
> 확인 되 면 hello 인프라는 hello 원인을 권장 하는 정기적으로 성능 향상을 위해 hello 디스크 조각 모음 합니다.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>원인: 다른 프로세스 또는 바이러스 백신 소프트웨어가 Azure 백업을 방해함
Hello Windows 시스템의에서 다른 프로세스는 hello Azure 백업 에이전트 프로세스의 성능을 저하 하는 여러 인스턴스를 살펴보았습니다. 예를 들어 hello Azure Backup agent와 다른 프로그램 tooback 등 데이터를 사용 하 여 또는 바이러스 백신 소프트웨어가 실행 되 고 toobe 파일에 대 한 잠금을를 백업 하는 경우 환영 파일에 여러 잠금 경합이 발생할 수 있습니다. 이 경우 hello 백업이 실패할 수 있습니다 또는 hello 작업이 예상 보다 오래 걸릴 수 있습니다.

이 시나리오에서 최적의 권장 구성을 hello hello 오프 tooturn 다른 백업 프로그램 toosee hello hello Azure 백업 에이전트에 대 한 백업 시간 변경 여부는 합니다. 일반적으로 여러 개의 백업 작업이 실행 되지 않는 있도록 hello 동시는 충분 한 tooprevent 서로 영향을 주는.

바이러스 백신 프로그램에 대 한 것이 좋습니다 hello 다음을 제외 하는 파일 및 위치:

* C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe를 프로세스로 제외합니다.
* C:\Program Files\Microsoft Azure Recovery Services Agent\ 폴더를 제외합니다.
* (Hello 표준 위치를 사용 하지 않는) 하는 경우 위치를 스크래치

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>원인: 백업 에이전트가 Azure 가상 컴퓨터에서 실행되고 있음
VM에서 hello 백업 에이전트를 실행 하는, 성능은에서 실행 하면 해당 실제 컴퓨터 보다 느립니다 것입니다. 세대와 함께 tooIOPS 제한 사항 때문입니다.  그러나 tooAzure 프리미엄 저장소 백업 되 고 hello 데이터 드라이브를 전환 하 여 hello 성능을 최적화할 수 있습니다. 이 문제를 수정한 다음 작업 하 고 hello 수정 프로그램은 이후 릴리스에서 사용할 수 있습니다.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>원인: 많은 수(수백만 개)의 파일 백업
이동하는 데이터의 양이 많을수록 시간이 더 오래 걸립니다. 경우에 따라 백업 시간 관련 toonot hello 데이터 뿐만 아니라 hello 수의 파일 또는 폴더의 크기를 hello만 합니다. 특히 경우 수많은 작은 파일 (몇 바이트 tooa 몇 킬로바이트) 백업 되 고 있습니다.

Azure 파일을 동시에 카탈로그는 hello 데이터를 백업 하 고 tooAzure 이동 하는 동안이 문제가 발생 합니다. 일부 드문 시나리오에서는 hello 카탈로그 작업이 예상 보다 오래 걸릴 수 있습니다.

표시기를 수행 하는 hello hello 병목 상태를 이해 하 고 hello 다음 단계를 적절 하 게 작업할 수 있습니다.

* **UI는 hello 데이터 전송에 대 한 진행률을 보여 주는**합니다. hello 데이터 여전히 전송 중입니다. 네트워크 대역폭을 hello 또는 데이터의 hello 크기는 지연을 초래할 수 있습니다.
* **UI hello 데이터 전송에 대 한 진행률을 표시 되지 않는**합니다. 열기 hello 로그 C:\Microsoft Azure 복구 서비스 Agent\Temp에 있으며 hello 로그에 항목이 FileProvider::EndData hello에 대 한 다음 확인 합니다. 이 항목 hello 데이터 전송이 완료 및 발생 하는 hello 카탈로그 작업을 나타냅니다. Hello 백업 작업을 취소 하지 마십시오. 대신 카탈로그 작업 toofinish hello에 대 한 조금 더 기다립니다. Hello 문제가 계속 되 면 문의 [Azure 지원](https://portal.azure.com/#create/Microsoft.Support)합니다.
