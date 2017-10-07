---
title: "Microsoft Azure 가상 컴퓨터, 클라우드 서비스 및 웹 앱의 자동 크기 조정의 aaaOverview | Microsoft Docs"
description: "Microsoft Azure의 자동 크기 조정의 개요입니다. TooVirtual 컴퓨터, 클라우드 서비스 및 웹 앱에 적용 됩니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Microsoft Azure Microsoft Azure Virtual Machines, Cloud Services 및 Web Apps에서 자동 크기 조정 개요
이 문서에서는 어떤 Microsoft Azure 자동 크기 조정의 장점 이며, 사용 하 여 tooget을 시작 하는 방법을 설명 합니다.  

Azure 모니터의 자동 크기 조정 적용만 너무[가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다.

> [!NOTE]
> Azure에는 두 개의 자동 크기 조정 메서드가 있습니다. 이전 버전의 자동 크기 조정 tooVirtual 컴퓨터 (가용성 집합)를 적용합니다. 이 기능은 제한적으로 지원 하 고 보다 빠르고 안정적 자동 크기 조정 지원에 대 한 마이그레이션 toovirtual 컴퓨터 크기를 설정 하는 것이 좋습니다. Toouse 이전 기술을 hello 하는 방법에 대 한 링크는이 문서에 포함 됩니다.  
>
>

## <a name="what-is-autoscale"></a>자동 크기 조정이란?
자동 크기 조정 응용 프로그램에서 toohandle hello 부하를 실행 중인 리소스의 toohave hello 올바른 용량이 있습니다. Tooadd 리소스를 toohandle 증가에 로드 하 고 유휴 상태는 리소스를 제거 하 여 비용을 절감할 수도 있습니다. 인스턴스 toorun 최소 및 최대 수를 지정 하 고 추가 하거나 Vm 규칙의 집합에 따라 자동으로 제거 합니다. 최소값을 설정하면 응용 프로그램이 항상 부하가 적은 상태에서 실행될 수 있습니다. 최대값을 설정하면 가능한 총 시간 비용이 제한됩니다. 만든 규칙을 사용하여 이러한 두 극한값 사이를 자동으로 조정합니다.

 ![자동 크기 조정이 설명되었습니다. VM 추가 및 제거](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

규칙 조건이 충족되면 하나 이상의 자동 크기 조정 동작이 트리거됩니다. VM을 추가 및 제거하거나 다른 작업을 수행할 수 있습니다. hello 다음 개념적 다이어그램에서는이 프로세스  

 ![자동 크기 조정 흐름 다이어그램](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

hello 아래 설명 적용 toohello 가지 hello 이전 다이어그램입니다.   

## <a name="resource-metrics"></a>리소스 메트릭
리소스에서 메트릭을 내보내며, 이러한 메트릭은 나중에 규칙에 따라 처리됩니다. 메트릭은 다른 메서드를 통해 제공됩니다.
가상 컴퓨터 크기 집합 웹 앱 및 클라우드 서비스에 대 한 원격 분석 hello Azure 인프라에서 직접 가져온 반면 Azure 진단 에이전트에서 원격 분석 데이터를 사용 합니다. 일부 자주 사용되는 통계는 CPU 사용량, 메모리 사용량, 스레드 수, 큐 길이 및 디스크 사용량을 포함합니다. 사용할 수 있는 원격 분석 데이터 목록은 [자동 크기 조정 공통 메트릭](insights-autoscale-common-metrics.md)을 참조하세요.

## <a name="custom-metrics"></a>사용자 지정 메트릭
응용 프로그램에서 내보낼 수 있는 사용자 지정 메트릭을 활용할 수도 있습니다. 응용 프로그램 toosend 메트릭 tooApplication 여부에 이러한 메트릭 toomake 결정을 활용할 수 있는 통찰력을 구성한 경우 tooscale 여부입니다. 

## <a name="time"></a>Time
일정 기반 규칙은 UTC 기준으로 합니다. 규칙을 설정할 때 표준 시간대를 올바르게 설정해야 합니다.  

## <a name="rules"></a>규칙
hello 다이어그램 하나만 자동 크기 조정 규칙을 보여주지만 여러 개 있을 수 있습니다. 상황에 필요한 대로 겹치는 복잡한 규칙을 만들 수 있습니다.  규칙 형식은 다음을 포함합니다.  

* **메트릭 기반** - 예를 들어 CPU 사용률이 50%보다 높으면 이 작업을 수행합니다.
* **시간 기반** - 예를 들어 지정된 표준 시간대에 토요일 오전 8시마다 웹후크를 트리거합니다.

메트릭 기반의 규칙은 응용 프로그램 부하를 측정하고 해당 부하를 기반으로 VM을 추가 또는 제거합니다. 일정에 기반 규칙을 사용 하면 tooscale 부하에서 시간 패턴을 파악 하 고 사용할 수 있는 부하 증가 하기 전에 tooscale 또는 감소 발생 하는 경우.  

## <a name="actions-and-automation"></a>작업 및 자동화
규칙은 하나 이상의 형식을 가진 작업을 트리거할 수 있습니다.

* **크기 조정** - VM을 감축 또는 확장합니다.
* **전자 메일** -toosubscription 관리자 전자 메일, 공동 관리자 및/또는 추가 전자 메일 주소를 지정 하면 보내기
* **Webhook 통해 자동화** - Azure의 내부 또는 외부에서 여러 복잡한 작업을 트리거할 수 있는 웹후크를 호출합니다. Azure에서 Azure Automation runbook, Azure Function 또는 Azure Logic App을 시작할 수 있습니다. Azure 외부의 타사 URL 예제는 Slack 및 Twilio와 같은 서비스를 포함합니다.

## <a name="autoscale-settings"></a>자동 크기 조정 설정
자동 크기 조정 hello 다음 이름을 사용해 서 용어와 구조입니다.

- **자동 크기 조정 설정** 여부 hello 자동 크기 조정 엔진 toodetermine 읽은 tooscale 위나 아래로 이동 합니다. 하나 자세한 프로필, hello 대상 리소스 및 알림 설정에 대 한 정보를 포함합니다.

    - **자동 크기 조정 프로필**은 다음 항목의 조합입니다.

        - **용량 설정**, hello 최소, 최대, 나타냅니다 및 기본 인스턴스 수에 대 한 값입니다.
        - **일련의 집합**은 각 트리거(시간 또는 미터법) 및 크기 조정 작업(위쪽 또는 아래쪽)을 포함합니다.
        - **되풀이**는 자동 크기 조정에서 이 프로필을 적용할 시기를 지정합니다.

        겹치는 서로 다른 요구 사항 care of tootake 수 있게 해 주는 여러 프로필을 가질 수 있습니다. 다른 자동 크기 조정 프로필 하루 또는 한 hello 주 중 일 서로 다른 시간에 대 한 예를 들어 있을 수 있습니다.

    - A **알림 설정** hello 기준을 hello 자동 크기 조정 설정의 프로필 중 하나를 만족에 따라 자동 크기 조정 이벤트 발생 시 알림을 수행할지 정의 합니다. 자동 크기 조정 하나 이상의 전자 메일 주소 또는 호출 tooone 또는 자세한 webhook 수 있습니다.


![Azure 자동 크기 조정 설정, 프로필 및 규칙 구조](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

hello 구성 가능한 필드 및 설명의 전체 목록은 영어로 hello [자동 크기 조정 REST API](https://msdn.microsoft.com/library/dn931928.aspx)합니다.

코드 예제는 다음을 참조하세요.

* [Resource Manager 템플릿을 사용하여 VM 확장 집합에 대한 고급 자동 크기 조정 구성](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [자동 크기 조정 REST API](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>수평 및 수직적 크기 조정
자동 크기 조정만 확장할 수 수평으로 ("out") 증가 또는 감소 ("")는 hello VM 인스턴스 수에 있습니다.  가로 toohandle 부하 Vm의 잠재적으로 수천 toorun 수 있으므로 클라우드 상황에서 더 유연 합니다.

반대로 수직적 규모 조정은 다릅니다. 이 유지 hello 동일한 Vm 수 있지만 hello ("업") 다소간 ("아래쪽") 강력한 Vm입니다. 전원은 메모리, CPU 속도, 디스크 공간 등에서 측정됩니다.  수직적 크기 조정에 더 많은 제한이 있습니다. 더 큰 하드웨어를 신속 하 게 상한값에 도달 하 고 지역에 따라 다 수의 hello 가용성에 따라 달라 집니다. 또한 일반적으로 크기 조정을 세로 VM toostop 차지 하며 다시 시작 합니다.

자세한 내용은 [Azure Automation을 사용하여 Azure 가상 컴퓨터를 수직으로 확장](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.

## <a name="methods-of-access"></a>액세스 방법
자동 크기 조정은 다음을 통해 설정할 수 있습니다.

* [Azure 포털](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [플랫폼 간 CLI(명령줄 인터페이스)](insights-cli-samples.md#autoscale)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>자동 크기 조정이 지원되는 서비스
| 부여 | 스키마 및 문서 |
| --- | --- |
| 웹앱 |[웹앱 크기 조정](insights-how-to-scale.md) |
| 클라우드 서비스 |[클라우드 서비스 자동 크기 조정](../cloud-services/cloud-services-how-to-scale.md) |
| Virtual Machines: 클래식 |[클래식 가상 컴퓨터 가용성 집합 크기 조정](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Virtual Machines: Windows 확장 집합 |[Windows에서 가상 컴퓨터 확장 집합 크기 조정](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Virtual Machines: Linux 확장 집합 |[Linux에서 가상 컴퓨터 확장 집합 크기 조정](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Virtual Machines: Windows 예제 |[Resource Manager 템플릿을 사용하여 VM 확장 집합에 대한 고급 자동 크기 조정 구성](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>다음 단계
toolearn 자동 크기 조정에 대 한 자세한 자동 크기 조정 연습 앞에 나열 된 hello를 사용 하거나, toohello 다음 리소스를 참조 하십시오.

* [Azure Monitor 자동 크기 조정 공용 메트릭](insights-autoscale-common-metrics.md)
* [Azure Monitor 자동 크기 조정에 대한 모범 사례](insights-autoscale-best-practices.md)
* [자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용](insights-autoscale-to-webhook-email.md)
* [자동 크기 조정 REST API](https://msdn.microsoft.com/library/dn931953.aspx)
* [가상 컴퓨터 규모 집합 자동 크기 조정 문제 해결](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
