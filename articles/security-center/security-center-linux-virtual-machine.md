---
title: "aaaAzure 보안 센터와 Azure 가상 컴퓨터와 Linux | Microsoft Docs"
description: "이 문서를 사용 하면 toounderstand 어떻게 Azure 보안 센터 수 보호 하면 Azure 가상 컴퓨터."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: yurid
ms.openlocfilehash: d7aa9e54032272839dabfefa30c4c614d5e5610a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines-with-linux"></a>Linux에 설치된 Azure Security Center 및 Azure Virtual Machines
[Azure 보안 센터](https://azure.microsoft.com/services/security-center/) 하면 방지, 검색 및 toothreats 응답 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

이 문서에서는 Security Center가 Linux 운영 체제에서 실행되는 Azure VM(Virtual Machines)을 보호하는 데 어떻게 도움이 되는지 보여 줍니다.

## <a name="why-use-security-center"></a>보안 센터를 사용해야 하는 이유
Security Center를 사용하면 가상 컴퓨터의 보안 설정에 가시성을 제공하고 위협을 모니터링하여 Azure에서 가상 컴퓨터의 데이터를 보호할 수 있습니다. Security Center는 다음의 목적으로 가상 컴퓨터를 모니터링할 수 있습니다. 

* 권장 구성 규칙 hello로 운영 체제 (OS) 보안 설정
* 시스템 보안 및 누락된 중요 업데이트
* 끝점 보호 권장 사항
* 디스크 암호화 유효성 검사
* 네트워크 기반 공격([표준 버전](https://azure.microsoft.com/en-us/pricing/details/security-center/)에서만 사용할 수 있음)

또한 toohelping Azure Vm을 보호, 보안 센터도 보안 모니터링 및 클라우드 서비스, 응용 프로그램 서비스, 가상 네트워크 등에 대 한 관리를 제공 합니다. 

> [!NOTE]
> 참조 [소개 tooAzure 보안 센터](security-center-intro.md) toolearn Azure 보안 센터에 대 한 자세한 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
Azure 보안 센터를 시작 하는 tooget tooknow 필요 하 고 hello 다음 사항을 고려 합니다.

* 구독 tooMicrosoft Azure 있어야 합니다. 보안 센터의 무료 및 표준 계층에 대한 자세한 내용은 [보안 센터 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요.
* 참조, 보안 센터 채택 계획 [Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) toolearn 계획 및 작업 고려 사항에 대 한 자세한 합니다.
* 운영 체제 지원 가능성에 대한 정보는 [Azure Security Center FAQ(질문과 대답)](security-center-faq.md)를 참조하세요. 

## <a name="set-security-policy"></a>보안 정책 설정
해당 Azure 보안 센터 tooprovide 권장 사항 및 생성 된 경고를 필요한 hello 정보를 수집할 수 있도록 사용 데이터 컬렉션 요구 toobe hello 보안 정책을 기반으로 구성 합니다. Hello 아래 그림을 볼 수 있습니다는 **데이터 수집** 설정 되어 있으면 **에**합니다.

보안 정책 hello 지정된 구독 또는 리소스 그룹 내의 리소스에 대 한 권장 되는 제어 hello 집합을 정의 합니다. 보안 정책을 활성화 하기 전에 데이터 수집을 사용 하도록 설정 되어 있어야, tooassess 자신의 보안 상태는 보안 권장 사항을 제공 하 고 toothreats를 경고를 정렬 하는 보안 센터에서 가상 컴퓨터에서 데이터를 수집 합니다. 보안 센터를 Azure 구독 또는 tooyour 회사의 보안 요구 사항과 hello 응용 프로그램 종류 또는 hello 데이터 각 구독에서의 민감도 따라 리소스 그룹에 대 한 정책을 정의 합니다. 

![보안 정책](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig1.png)

> [!NOTE]
> 각각에 대 한 자세한 toolearn **방지 정책** 참조를 사용할 수 [보안 정책 설정](security-center-policies.md) 문서.
> 

## <a name="manage-security-recommendations"></a>보안 권장 사항 관리
보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다. 보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다. hello 권장 사항이 필요한 hello 컨트롤 구성의 hello 프로세스를 안내 합니다.

보안 정책으로 설정한 후 보안 센터 리소스 tooidentify 잠재적인 취약점의 hello 보안 상태를 분석 합니다. hello 권장 여기서 각 줄은 한 가지 특정 권장 하는 테이블 형식으로 표시 됩니다. hello 아래 표에서 Azure Vm에 대 한 권장 구성의 예로 Linux 운영 체제와 각은 적용 하는 경우 수행할 작업을 실행 합니다. 권장 구성을 선택 하면 tooimplement 보안 센터의 권장 조치를 hello 하는 방법을 보여 주는 정보가 제공 됩니다.

| 권장 사항 | 설명 |
| --- | --- |
| [구독에 대해 데이터 수집 활성화](security-center-enable-data-collection.md) |구독에서 각 구독 하 고 모든 가상 컴퓨터 (Vm)에 대 한 hello 보안 정책에서 데이터 컬렉션 켜기 하는 것이 좋습니다. |
| [OS 취약성 해결](security-center-remediate-os-vulnerabilities.md) |예를 들어 권장 구성 규칙 hello로 운영 체제 구성을 정렬 하는 권장 저장 암호 toobe를 허용 하지 않습니다. |
| [시스템 업데이트 적용](security-center-apply-system-updates.md) |누락 된 시스템 보안 및 중요 업데이트 tooVMs를 배포 하는 것이 좋습니다. |
| [시스템 업데이트 후 다시 부팅](security-center-apply-system-updates.md#reboot-after-system-updates) |시스템 업데이트를 적용 한 VM toocomplete hello 프로세스를 다시 부팅 하는 것이 좋습니다. |
| [VM 에이전트 사용](security-center-enable-vm-agent.md) |하면 toosee Vm 해야 하는 hello VM 에이전트를 사용 합니다. VM 에이전트 hello 순서 tooprovision 패치 검사, 검색 기준 및 맬웨어 방지 프로그램에서에서 Vm에 설치 되어야 합니다. hello Azure Marketplace에서에서 배포 되는 Vm에 대 한 hello VM 에이전트는 기본적으로 설치 됩니다. hello 문서 [VM 에이전트 및 확장-2 부](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) tooinstall VM 에이전트를 hello 하는 방법에 대해 설명 합니다. |
| [디스크 암호화 적용](security-center-apply-disk-encryption.md) |Azure 디스크 암호화(Windows 및 Linux VM)를 사용하여 VM 디스크를 암호화하는 것이 좋습니다. Hello OS와 VM에 데이터 볼륨에 대 한 암호화를 사용 하는 것이 좋습니다. |


> [!NOTE]
> 권장 사항에 대해 자세히 toolearn 참조 [보안 권장 사항 관리](security-center-recommendations.md) 문서.
> 

## <a name="monitor-security-health"></a>보안 상태 모니터링
사용 하도록 설정한 후 [보안 정책](security-center-policies.md) 구독의 리소스에 대 한 보안 센터 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다.  Hello에서 모든 문제와 함께 리소스 hello 보안 상태를 볼 수 **리소스 보안 상태** 블레이드입니다. 클릭할 때 **가상 컴퓨터** hello에 **리소스 보안** 상태 타일, hello **가상 컴퓨터** Vm에 대 한 권장 사항과 블레이드가 열립니다. 

![보안 상태](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>관리 및 toosecurity 경고에 응답
보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션 (예: 방화벽 및 endpoint protection 솔루션)에서 로그 데이터를 통합 toodetect 실제 위협 하 고 거짓 긍정을 줄입니다. 다양 한 집계를 활용 하 여 [검색 기능이](security-center-detection-capabilities.md), 보안 센터는 우선 순위가 지정 된 수 toogenerate 보안 경고를 신속 하 게 hello 문제를 조사 하 고 방법에 대 한 권장 사항을 제공 toohelp tooremediate 가능한 공격입니다.

![보안 경고](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

보안 경고 toolearn 선택 tootake tooremediate 공격 hello 캡처할 이벤트를 발생 시킨 hello 알림과 부분, any, 과정을 설명 하는 경우에 대 한 자세한 필요 합니다. 보안 경고는 [형식](security-center-alerts-type.md) 및 날짜별로 그룹화됩니다.

## <a name="monitor-security-health"></a>보안 상태 모니터링
사용 하도록 설정한 후 [보안 정책](security-center-policies.md) 구독의 리소스에 대 한 보안 센터 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다.  Hello에서 모든 문제와 함께 리소스 hello 보안 상태를 볼 수 **리소스 보안 상태** 블레이드입니다. 클릭할 때 **가상 컴퓨터** hello에 **리소스 보안** 상태 타일, hello **가상 컴퓨터** Vm에 대 한 권장 사항과 블레이드가 열립니다. 

![보안 상태](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig4.png)

이어야 하는 hello 특정 작업에 대 한 자세한 내용은이 권장 사항을 클릭 하면 나타납니다 tooaddress 문제 별로 수행 합니다. hello 세부 정보에에서 표시 됩니다 hello hello 블레이드 맨 아래에서 **권장 사항을**합니다. 

![보안 상태 2](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig5.png)


## <a name="see-also"></a>참고 항목
보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.

