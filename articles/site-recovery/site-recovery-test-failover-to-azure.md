---
title: "사이트 복구에서 장애 조치 tooAzure aaaTest | Microsoft Docs"
description: "온-프레미스 tooAzure에서 테스트 장애 조치를 실행 하는 방법에 대 한 자세한 내용은"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>사이트 복구에서 장애 조치 tooAzure 테스트



테스트 장애 조치 또는 가상 컴퓨터와 물리적 서버와 DR 드릴을 수행 하기 위한 지침은 Azure hello 복구 사이트로 사용 하 여 Site Recovery로 보호 된 및이 문서 정보를 제공 합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

테스트 장애 조치는 toovalidate 복제 전략을 실행 하거나 데이터 손실 또는 가동 중지 시간 없이 재해 복구 훈련과 수행 합니다. 테스트 장애 조치를 수행 하 프로덕션 환경 또는 hello 진행 중인 복제에 영향을 받지가지고 하지 않습니다. 가상 컴퓨터 또는 [복구 계획](site-recovery-create-recovery-plans.md)에서 테스트 장애 조치(failover)를 수행할 수 있습니다. 테스트 장애 조치를 트리거하는 경우 toospecify hello 네트워크 toowhich 테스트 가상 컴퓨터에 연결 해야 합니다. 테스트 장애 조치 트리거된 hello에서 진행률을 추적할 수 있습니다 **작업** 페이지.  


## <a name="supported-scenarios"></a>지원되는 시나리오
테스트 장애 조치 이외의 다른 모든 배포 시나리오에서 지원 됩니다 [레거시 VMware 사이트 tooAzure](site-recovery-vmware-to-azure-classic-legacy.md)합니다. 테스트 장애 조치도 지원 되지 않습니다 tooAzure을 통해 가상 컴퓨터에 실패 한 경우.  


## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
이 절차에서는 설명 어떻게 toorun 복구에 대 한 테스트 장애 조치 계획 합니다. 또는 hello에 적절 한 옵션을 사용 하 여 단일 컴퓨터에 대 한 테스트 장애 조치를 실행할 수도 있습니다.

![테스트 장애 조치(Failover)](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. **복구 계획** > *recoveryplan_name*을 선택합니다. **테스트 장애 조치(failover)**를 클릭합니다.
1. 선택 된 **복구 지점** toofailover 하 합니다. Hello 다음 옵션 중 하나를 사용할 수 있습니다.
    1.  **최신 처리**: hello 복구 계획 toohello 최근 복구 지점 Site Recovery 서비스에서 이미 처리 된 모든 가상 컴퓨터를 통해이 옵션에 실패 합니다. 가상 컴퓨터의 테스트 장애 조치를 수행 하는 타임 스탬프 hello 최근 처리 된 복구 지점 표시 됩니다. 복구 계획의 장애 조치를 수행 하는 경우 tooindividual 가상 컴퓨터를 이동 하 고 확인 수 **최신 복구 지점을** tooget이이 정보를 바둑판식으로 합니다. 시간이 없는 tooprocess hello 처리 되지 않은 데이터,이 옵션은 낮은 RTO (복구 시간 목표) 장애 조치 옵션을 제공 합니다.
    1.  **최신 응용 프로그램에 일관 된**:이 옵션의 hello 복구 계획 toohello 최신 응용 프로그램 일치 복구 지점 Site Recovery 서비스에서 이미 처리 된 모든 가상 컴퓨터를 통해 실패 합니다. 가상 컴퓨터의 테스트 장애 조치를 수행 하는 hello 최신 응용 프로그램 일치 복구 지점의 타임 스탬프 표시 됩니다. 복구 계획의 장애 조치를 수행 하는 경우 tooindividual 가상 컴퓨터를 이동 하 고 확인 수 **최신 복구 지점을** tooget이이 정보를 바둑판식으로 합니다.
    1.  **최신**:이 옵션은 먼저 tooit을 통해이 중지 하기 전에 보낸된 tooSite 복구 서비스 toocreate 각 가상 컴퓨터에 대 한 복구 지점이 된 모든 hello 데이터를 처리 합니다. 이 옵션은 hello 제공 hello 가상 컴퓨터로 장애 조치에는 모든 hello 데이터 갖습니다 후 생성 된 가장 낮은 RPO (Recovery Point Objective)는 hello 장애 조치 트리거된 경우 tooSite 복구 서비스를 복제 합니다.
    1.  **최신 다중 VM 처리**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다. 가상 컴퓨터는 복제 그룹 장애 조치 toohello 최신 일반적인 다중 VM 일관성 복구의 일부인 가리킵니다. 다른 가상 컴퓨터 장애 조치 tootheir 최신 처리 된 복구 지점입니다.  
    1.  **최신 다중 VM 앱 일치**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다. 복제의 일부인 가상 컴퓨터 장애 조치 toohello 최신 일반적인 다중 VM 응용 프로그램 일치 복구 지점을 그룹화 합니다. 다른 가상 컴퓨터 장애 조치 tootheir 최신 응용 프로그램 일치 복구 지점입니다. 
    1.  **사용자 지정**: 가상 컴퓨터의 테스트 장애 조치를 수행 하는 경우이 옵션 toofailover tooa 특정 복구 지점을 사용할 수 있습니다.
1. 선택 된 **Azure 가상 네트워크**: hello 테스트 가상 컴퓨터를 만들 수는 있는 Azure 가상 네트워크를 제공 합니다. 사이트 복구는 동일한 이름의 서브넷의 toocreate 테스트 가상 컴퓨터를 시도 하 고에 제공 된 것과 동일한 IP hello를 사용 하 여 **계산 및 네트워크** hello 가상 컴퓨터의 설정 합니다. 동일한 이름의 서브넷 없는 경우 hello 테스트 장애 조치에 대해 제공 된 Azure 가상 네트워크에서에서 사용할 수 있는 경우 테스트 가상 컴퓨터 hello 첫 번째 서브넷에 사전순으로 생성 합니다. 동일한 IP hello 서브넷에 사용할 수 없는 경우 가상 컴퓨터는 hello 서브넷에서 사용 가능한 다른 IP 주소를 가져옵니다. [자세한 내용](#creating-a-network-for-test-failover)은 이 섹션을 참조하세요.
1. TooAzure로는 장애 조치 하는 경우 및 데이터 암호화를 사용 하면에 **암호화 키** 선택 hello 발급 된 인증서를 데이터 공급자 설치 중에 암호화를 사용 하는 경우. Hello 가상 컴퓨터에 대 한 암호화를 설정 하지 않은 경우이 단계를 무시할 수 있습니다.
1. Hello에서 장애 조치 진행률 추적 **작업** 탭 합니다. 수 toosee hello 테스트 복제본 컴퓨터 hello Azure 포털에에서 있어야 합니다.
1. hello 가상 컴퓨터에 대 한 RDP 연결 tooinitiate 해야 너무[공용 ip 추가](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) hello에 네트워크 인터페이스의 hello 가상 컴퓨터를 통해 실패 합니다. Tooa 클래식 가상 컴퓨터를 통해 실패 하는 경우 필요한 너무[끝점 추가](../virtual-machines/windows/classic/setup-endpoints.md) 포트 3389에서
1. 완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. **노트** 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.


> [!TIP]
> 사이트 복구는 동일한 이름의 서브넷의 toocreate 테스트 가상 컴퓨터를 시도 하 고에 제공 된 것과 동일한 IP hello를 사용 하 여 **계산 및 네트워크** hello 가상 컴퓨터의 설정 합니다. 동일한 이름의 서브넷 없는 경우 hello 테스트 장애 조치에 대해 제공 된 Azure 가상 네트워크에서에서 사용할 수 있는 경우 테스트 가상 컴퓨터 hello 첫 번째 서브넷에 사전순으로 생성 합니다. Hello 대상 IP 서브넷을 선택 하는 hello의 일부 이면 사이트 복구는 hello 대상 IP를 사용 하 여 toocreate hello 테스트 장애 조치 가상 컴퓨터를 시도 합니다. Hello 대상 IP 서브넷을 선택 하는 hello의 일부가 아닙니다. 사용 가능한 임의의 IP를 사용 하 여 서브넷을 선택 하는 hello에 테스트 장애 조치 가상 컴퓨터 생성을 가져옵니다.
>
>

## <a name="test-failover-job"></a>테스트 장애 조치 작업

![테스트 장애 조치(Failover)](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

장애 조치가 트리거되면 다음 단계를 수행합니다.

1. 필수 조건 확인: 장애 조치에 필요한 모든 조건이 충족되는지 확인합니다.
1. 장애 조치:이 단계 hello 데이터를 처리 하 고 옵트아웃 Azure 가상 컴퓨터를 만들 수 있도록 준비 만듭니다. 선택한 경우 **최신** 복구 지점을이 단계는 toohello 서비스 보낸 hello 데이터에서 복구 지점의 만듭니다.
1. 시작:이 단계는 hello 이전 단계에서 처리 하는 hello 데이터를 사용 하 여 Azure 가상 컴퓨터를 만듭니다.

## <a name="time-taken-for-failover"></a>장애 조치(Failover)에 걸리는 시간

경우에 따라 가상 컴퓨터의 장애 조치 일반적으로 약 8 too10 분 toocomplete 받아들이는 중간 단계를 수행 해야 합니다. 여기에 해당하는 경우는 다음과 같습니다.

* Hello 9.8 보다 오래 된 모바일 서비스의 버전을 사용 하 여 VMware 가상 컴퓨터
* 물리적 서버
* VMware Linux 가상 컴퓨터
* 물리적 서버로 보호되는 Hyper-V 가상 컴퓨터
* 다음 드라이버가 부팅 드라이버로 제공되지 않는 VMware 가상 컴퓨터
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* DHCP 또는 고정 IP 주소 사용 여부와 관계없이 DHCP 서비스를 사용할 수 없는 VMware 가상 컴퓨터

모든 hello에 다른 경우가 중간 단계 필요 하지 않으며 hello 장애 조치에 걸리는 hello 훨씬 낮습니다.


## <a name="creating-a-network-for-test-failover"></a>테스트 장애 조치(Failover)를 위한 네트워크 만들기
테스트 장애 조치를 수행 하는 경우 사용자가 제공한 실제 복구 사이트 네트워크와에서 격리 된 네트워크를 선택 하는 것이 좋습니다 **계산 및 네트워크** hello 가상 컴퓨터에 대 한 설정입니다. 사용자가 만드는 Azure 가상 네트워크는 기본적으로 다른 네트워크와 격리됩니다. 이 네트워크는 프로덕션 네트워크와 비슷해야 합니다.

1. 테스트 네트워크는 프로덕션 네트워크의 hello 서브넷의 이름이 hello와 프로덕션 네트워크에 서브넷의 수가 같아야 합니다.
1. 테스트 네트워크를 사용할지는 프로덕션 네트워크와 동일한 IP 범위 hello 합니다.
1. 업데이트 hello hello hello IP에서 hello DNS 가상 컴퓨터에 대 한 IP를 대상으로 지정한 대로 테스트 네트워크의 DNS **계산 및 네트워크** 설정 합니다. 자세한 내용은 [Active Directory의 테스트 장애 조치(failover) 시 고려 사항](site-recovery-active-directory.md#test-failover-considerations) 섹션을 살펴보세요.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>복구 사이트에서 테스트 장애 조치 tooa 프로덕션 네트워크
테스트 장애 조치를 수행 하는 경우 선택 하는 네트워크에서 제공한 실제 복구 사이트 네트워크와에서 다른 것이 좋습니다. **계산 및 네트워크** hello 가상 컴퓨터에 대 한 설정입니다. 원하는 toovalidate 끝 tooend 네트워크 연결에 실패 한 경우 가상 컴퓨터를 통해 hello 지점 다음에 유의 합니다.

1. Hello 테스트 장애 조치를 수행 하는 경우 해당 hello 주 가상 컴퓨터는 종료 있는지 확인 합니다. 이렇게 하지 않는 경우 있을 hello로 두 개의 가상 컴퓨터가 hello에서 실행 되는 동일한 id 동일한 네트워크 hello에 동시 및 있는 tooundesired 결과 발생할 수 있습니다.
1. Hello 테스트 장애 조치 가상 컴퓨터에 수행한 모든 변경 내용이 손실 됩니다 때 정리 hello 테스트 장애 조치 가상 컴퓨터가 있습니다. 이러한 변경 내용은 주 가상 컴퓨터 복제 백 toohello 되지 않습니다.
1. 이러한 방법으로 테스트를 수행 하는 프로덕션 응용 프로그램의 가동 중지 시간을 tooa 이어집니다. Hello 응용 프로그램의 사용자가 해야 묻는 메시지가 toonot hello DR 드릴의 사용 하 여 hello 응용 프로그램 진행 중입니다.  



## <a name="prepare-active-directory-and-dns"></a>Active Directory 및 DNS 준비
응용 프로그램 테스트에 대 한 테스트 장애 조치 toorun 테스트 환경에서 hello 프로덕션 Active Directory 환경의 복사본이 필요 합니다. 자세한 내용은 [Active Directory의 테스트 장애 조치(failover) 시 고려 사항](site-recovery-active-directory.md#test-failover-considerations) 섹션을 살펴보세요.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>장애 조치 후 tooconnect tooAzure Vm을 준비 합니다.

Tooconnect tooAzure Vm을 원하는 경우 RDP를 사용 하 여 장애 조치 후 hello 표에서 요약 설명한 동작 hello 수행 되었는지 확인 합니다.

**장애 조치(Failover)** | **위치**: | **actions**
--- | --- | ---
**Windows를 실행하는 Azure VM** | 장애 조치(failover) 전에 온-프레미스 컴퓨터에서 | tooaccess를 통해 Azure VM hello 인터넷 hello, RDP를 활성화, 확인 되었는지 TCP 및 UDP 규칙이 hello에 대 한 추가 됩니다 **공용**, RDP에 허용 되 고 **Windows 방화벽** > **허용 됨 앱**, 모든 프로필에 대 한 합니다.<br/><br/> 사이트 간 연결을 통해 tooaccess hello 컴퓨터에서 RDP를 활성화 하 고 hello에 RDP를 사용할 수 있는지 확인 하십시오. **Windows 방화벽** -> **허용 되는 앱 및 기능** 에 대 한  **도메인 및 개인** 네트워크입니다.<br/><br/>  Hello 운영 체제의 SAN 정책 너무 설정 되어 있는지 확인**OnlineAll**합니다. [자세히 알아봅니다](https://support.microsoft.com/kb/3031135).<br/><br/> 장애 조치를 트리거하 때 기다리는 Windows 업데이트가 hello 가상 컴퓨터에가 있는지 확인 합니다. Windows 업데이트는 장애 조치 하 고 됩니다 toohello 가상 컴퓨터 수 toologin hello 업데이트가 완료 될 때까지 때 시작 될 수 있습니다. <br/><br/>
**Windows를 실행하는 Azure VM** | 장애 조치(failover) 후 Azure VM에서 | 클래식 가상 컴퓨터에 대 한 [공용 끝점을 추가](../virtual-machines/windows/classic/setup-endpoints.md) hello RDP 포트 3389 프로토콜에 대 한<br/><br/>  Resource Manager 가상 컴퓨터의 경우 [공용 IP를 추가](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine)합니다.<br/><br/> 장애 조치 VM을 hello에 대 한 네트워크 보안 그룹 규칙 hello 및 hello, 연결 된 Azure 서브넷 toowhich tooallow 들어오는 연결 toohello RDP 포트가 필요 합니다.<br/><br/> 리소스 관리자 가상 컴퓨터에 대해 확인할 수 있습니다 **진단 부팅** toolook에 hello 가상 컴퓨터의 스크린 샷<br/><br/> 연결할 수 없는 경우 VM에서 실행 되 고 해당 hello를 확인 한 다음 확인 이러한 [문제 해결 팁](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)합니다.<br/><br/>
**Linux를 실행하는 Azure VM** | 장애 조치(failover) 전에 온-프레미스 컴퓨터에서 | 해당 hello hello Azure VM에서 보안 셸 서비스 toostart 자동으로 설정 된 시스템 부팅 시 확인 합니다.<br/><br/> 방화벽 규칙 SSH 연결 tooit 허용 하는지 확인 합니다.
**Linux를 실행하는 Azure VM** | 장애 조치(failover) 후 Azure VM | 장애 조치 VM을 hello에 대 한 네트워크 보안 그룹 규칙 hello 및 hello, 연결 된 Azure 서브넷 toowhich tooallow 들어오는 연결 toohello SSH 포트가 필요 합니다.<br/><br/> 클래식 가상 컴퓨터에 대 한 [공용 끝점을 추가](../virtual-machines/windows/classic/setup-endpoints.md) 만들 tooallow hello SSH 포트 (TCP 포트 22 기본적으로)에서 들어오는 연결 합니다.<br/><br/> Resource Manager 가상 컴퓨터의 경우 [공용 IP를 추가](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine)합니다.<br/><br/> 리소스 관리자 가상 컴퓨터에 대해 확인할 수 있습니다 **진단 부팅** toolook에 hello 가상 컴퓨터의 스크린 샷<br/><br/>



## <a name="next-steps"></a>다음 단계
테스트 장애 조치(failover)를 성공적으로 수행한 후에는 [장애 조치](site-recovery-failover.md)(failover)를 수행해도 됩니다.
