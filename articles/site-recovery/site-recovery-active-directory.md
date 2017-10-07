---
title: "aaaProtect Active Directory 및 DNS를 Azure Site Recovery와 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooimplement Azure Site Recovery를 사용 하 여 Active Directory에 대 한 재해 복구 솔루션입니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Azure Site Recovery로 Active Directory 및 DNS 보호
SharePoint, Dynamics AX 및 SAP와 같은 엔터프라이즈 응용 프로그램 올바르게 Active Directory 및 DNS 인프라 toofunction에 따라 다릅니다. 응용 프로그램에 대 한 재해 복구 솔루션을 만들 때 필요한 tooprotect hello 하기 전에 Active Directory 및 DNS를 복구 하는 중요 한 tooremember tooensure 재해가 발생 하는 경우 작업이 제대로 작동 하는, 다른 응용 프로그램 구성 요소입니다.

Site Recovery는 가상 컴퓨터 복제, 장애 조치(failover) 및 복구를 오케스트레이션하여 재해 복구 기능을 제공하는 Azure 서비스입니다. 사이트 복구는 다양 한 tooconsistently 보호 하는 복제 시나리오와 원활 하 게 장애 조치 가상 컴퓨터 및 응용 프로그램 tooprivate, public 또는 호스팅 서비스 공급자 클라우드를 지원 합니다.

Site Recovery를 사용하여 Active Directory에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다. 컴퓨터가 중단되는 경우 어디서나 몇 초 만에 장애 조치(failover)를 시작하고 몇 분 안에 Active Directory를 가동 및 실행할 수 있습니다. 기본 사이트에 여러 SharePoint 및 SAP 응용 프로그램에 대 한 Active Directory 배포 되었으며 toofail hello 완전 한 사이트를 통해 하려는 경우 Active Directory 먼저 사용 조치할 수 사이트 복구 및 장애 조치 후 hello 다른 응용 프로그램 응용 프로그램별 복구 계획을 사용합니다.

이 문서에서는 toocreate Active Directory에 대 한 재해 복구 솔루션, 어떻게 tooperform 계획 하 고, 계획 되지 않은 및 테스트 장애 조치는 한 번의 클릭 복구 계획을 사용 하 여 지원 되는 구성 및 필수 구성 요소 hello 하는 방법을 설명 합니다.  시작하기 전에 Active Directory와 Azure Site Recovery에 대해 잘 알고 있어야 합니다.

## <a name="replicating-domain-controller"></a>도메인 컨트롤러 복제

Toosetup 해야 [사이트 복구 복제](#enable-protection-using-site-recovery) 호스팅 도메인 컨트롤러 및 DNS 가상 컴퓨터를 하나 이상에 있습니다. 있는 경우 [여러 도메인 컨트롤러](#environment-with-multiple-domain-controllers) 사용자 환경에서 또한 tooreplicating hello도 tooset를 구성 해야 사이트 복구와 도메인 컨트롤러 가상 컴퓨터는 [추가도메인컨트롤러](#protect-active-directory-with-active-directory-replication) hello 대상 사이트 (Azure 또는 보조 온-프레미스 데이터 센터)에 있습니다. 

### <a name="single-domain-controller-environment"></a>단일 도메인 컨트롤러 환경
몇 가지 응용 프로그램 및 단일 도메인 컨트롤러만 있는 및 함께 toofail hello 전체 사이트를 통해 원하는 경우 사용할 수 있는 권장 사이트 복구 tooreplicate hello 도메인 컨트롤러 toohello 보조 사이트 (tooAzure로 장애 조치 하는 여부 또는 tooa 보조 사이트)입니다. hello 동일한 복제 도메인 컨트롤러/DNS 가상 컴퓨터에 사용할 수 있습니다 [테스트 장애 조치](#test-failover-considerations) 도 합니다.

### <a name="environment-with-multiple-domain-controllers"></a>도메인 컨트롤러가 여러 개 있는 환경
Hello 환경에 도메인 컨트롤러가 여러 개 또는 한 번에 몇 가지 응용 프로그램에 비해 toofail를 하려는 경우 권장는 또한 tooreplicating hello 도메인 컨트롤러 가상 및 많은 응용 프로그램이 있는 경우 컴퓨터 Site Recovery를 사용 하면 또한 설정 된 [추가 도메인 컨트롤러](#protect-active-directory-with-active-directory-replication) hello 대상 사이트 (Azure 또는 보조 온-프레미스 데이터 센터)에 있습니다. 에 대 한 [테스트 장애 조치](#test-failover-considerations), 장애 조치의 경우 hello 대상 사이트에 추가 도메인 컨트롤러 hello 및 Site Recovery에서 복제 도메인 컨트롤러를 사용 합니다. 


hello 다음 섹션에서는 어떻게 사이트 복구에서 도메인 컨트롤러에 대 한 보호 tooenable 방법과 tooset Azure에서 도메인 컨트롤러를 합니다.

## <a name="prerequisites"></a>필수 조건
* Active Directory 및 DNS 서버의 온-프레미스 배포
* Microsoft Azure 구독에서 Azure Site Recovery 서비스 자격 증명 모음
* Vm tooensure에서 hello Azure 가상 컴퓨터 준비 평가 도구를 실행 tooAzure를 복제 하는 경우 Azure Vm 및 Azure 사이트 복구 서비스와 호환 되는 합니다.

## <a name="enable-protection-using-site-recovery"></a>Site Recovery를 사용하여 보호 사용
### <a name="protect-hello-virtual-machine"></a>Hello 가상 컴퓨터 보호
사이트 복구에서 hello 도메인 컨트롤러/DNS 가상 컴퓨터의 보호를 사용 하도록 설정 합니다. Hello 가상 컴퓨터 유형 (Hyper-v 또는 VMware)에 따라 사이트 복구 설정을 구성 합니다. hello 도메인 컨트롤러를 Site Recovery를 사용 하 여 복제에 사용 되 [테스트 장애 조치](#test-failover-considerations)합니다. Hello 요구 사항에 맞는지 확인 합니다.

1. hello 도메인 컨트롤러는 글로벌 카탈로그 서버
2. hello 도메인 컨트롤러는 테스트 장애 조치 중 수행 해야 하는 역할에 대 한 hello FSMO 역할 소유자 여야 합니다 (그렇지 않으면 이러한 역할 toobe 할 [점유](http://aka.ms/ad_seize_fsmo) hello 장애 조치 후)

### <a name="configure-virtual-machine-network-settings"></a>가상 컴퓨터 네트워크 설정 구성
Hello 도메인 컨트롤러/DNS 가상 컴퓨터에 대 한 hello 가상 컴퓨터 장애 조치 후 적합 한 네트워크 연결된 toohello 수 있도록 사이트 복구에서 네트워크 설정을 구성 합니다. 

![VM 네트워크 설정](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Active Directory 복제로 Active Directory 보호
### <a name="site-to-site-protection"></a>사이트-사이트 보호
Hello 보조 사이트의 도메인 컨트롤러를 만듭니다. Hello 서버 tooa 도메인 컨트롤러 역할을 승격할 경우 hello의 hello 이름을 지정 hello 기본 사이트에서 사용 되는 동일한 도메인입니다. Hello를 사용할 수 있습니다 **Active Directory 사이트 및 서비스** 스냅인 hello 사이트 링크에서 tooconfigure 설정 개체 toowhich hello 사이트 추가 됩니다. 사이트 링크에서 설정을 구성하면 둘 이상의 사이트에서 복제가 실행되는 시기와 빈도를 관리할 수 있습니다. 자세한 내용은 [사이트 간 복제 일정 예약](https://technet.microsoft.com/library/cc731862.aspx)을 참조하세요.

### <a name="site-to-azure-protection"></a>사이트-Azure 보호
너무 hello 지침에 따라[Azure 가상 네트워크에서 도메인 컨트롤러를 만들](../active-directory/active-directory-install-replica-active-directory-domain-controller.md)합니다. Hello 서버 tooa 도메인 컨트롤러 역할을 승격할 경우 hello 지정 hello 기본 사이트에 사용 되는 동일한 도메인 이름입니다.

그런 다음 [hello 가상 네트워크에 대 한 hello DNS 서버를 다시 구성](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), Azure에서 toouse hello DNS 서버입니다.

![Azure 네트워크](./media/site-recovery-active-directory/azure-network.png)

**Azure 프로덕션 네트워크의 DNS**

## <a name="test-failover-considerations"></a>테스트 장애 조치 시 고려 사항
테스트 장애 조치(failover)는 프로덕션 워크로드에 영향을 미치지 않도록 프로덕션 네트워크에서 격리된 네트워크에서 발생합니다.

대부분의 응용 프로그램 도메인 컨트롤러 및 DNS 서버 toofunction의 hello 존재를 해야합니다. 따라서 hello 응용 프로그램 장애 조치 하기 전에 도메인 컨트롤러에 테스트 장애 조치에 사용 되는 격리 된 hello 네트워크 toobe에서 만든 toobe가 필요 합니다. 가장 쉬운 방법은 toodo hello tooreplicate Site Recovery와 도메인 컨트롤러/DNS 가상 컴퓨터입니다. 그런 다음 hello 응용 프로그램에 대 한 hello 복구 계획의 테스트 장애 조치를 실행 하기 전에 hello 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치를 실행 합니다. 그 방법은 다음과 같습니다.

1. [복제](site-recovery-replicate-vmware-to-azure.md) hello Site Recovery를 사용 하 여 도메인 컨트롤러/DNS 가상 컴퓨터.
1. 격리된 네트워크를 만듭니다. Azure에서 생성되는 모든 가상 네트워크는 기본적으로 다른 네트워크에서 격리됩니다. 이 네트워크에 대 한 hello IP 주소 범위는 프로덕션 네트워크와 동일한 것이 좋습니다. 이 네트워크에서 사이트-사이트 연결을 사용하지 마십시오.
1. Hello DNS 가상 컴퓨터 tooget 예상 하는 hello IP 주소로 만든 hello 네트워크에서 DNS IP 주소를 제공 합니다. TooAzure를 복제 하는 경우 다음 hello IP 주소를 제공 hello에 대 한 장애 조치에 사용 되는 VM에 대 한 **대상 IP** 에서 설정 **계산 및 네트워크** 설정 합니다. 

    ![대상 IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **대상 IP**

    ![Azure 테스트 네트워크](./media/site-recovery-active-directory/azure-test-network.png)

    **Azure 테스트 네트워크의 DNS**

> [!TIP]
> 사이트 복구는 동일한 이름의 서브넷의 toocreate 테스트 가상 컴퓨터를 시도 하 고에 제공 된 것과 동일한 IP hello를 사용 하 여 **계산 및 네트워크** hello 가상 컴퓨터의 설정 합니다. 동일한 이름의 서브넷 없는 경우 hello 테스트 장애 조치에 대해 제공 된 Azure 가상 네트워크에서에서 사용할 수 있는 경우 테스트 가상 컴퓨터 hello 첫 번째 서브넷에 사전순으로 생성 합니다. Hello 대상 IP 서브넷을 선택 하는 hello의 일부 이면 사이트 복구는 hello 대상 IP를 사용 하 여 toocreate hello 테스트 장애 조치 가상 컴퓨터를 시도 합니다. Hello 대상 IP 서브넷을 선택 하는 hello에 속하지 않는, 사용 가능한 임의의 IP를 사용 하 여 서브넷을 선택 하는 hello에 테스트 장애 조치 가상 컴퓨터 생성을 가져옵니다. 
>
>


1. Tooanother 온-프레미스 사이트를 복제 하는 경우 DHCP를 사용 하는 지침을 다릅니다 hello 너무[테스트 장애 조치에 대 한 DNS 및 DHCP 설정](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Hello 격리 된 네트워크에서 실행 하는 hello 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치를 수행 합니다. 사용 하 여 최신 사용 가능한 **응용 프로그램 일치** hello 도메인 컨트롤러 가상 컴퓨터 toodo hello 테스트 장애 조치의 복구 지점입니다. 
1. Hello 응용 프로그램의 가상 컴퓨터를 포함 하는 hello 복구 계획에 대 한 테스트 장애 조치를 실행 합니다. 
1. 테스트를 완료 한 후 **테스트 장애 조치 정리** hello 도메인 컨트롤러 가상 컴퓨터에 있습니다. 이 단계는 테스트 장애 조치에 대해 만들어진 hello 도메인 컨트롤러를 삭제 합니다.


### <a name="removing-reference-tooother-domain-controllers"></a>참조 tooother 도메인 컨트롤러를 제거합니다.
테스트 장애 조치를 수행 하는 경우 hello 테스트 네트워크 모든 hello 도메인 컨트롤러를 가져올 하지 않습니다. 프로덕션 환경에 존재 하는 다른 도메인 컨트롤러의 tooremove hello 참조 해야 너무[Active Directory FSMO 역할 점유](http://aka.ms/ad_seize_fsmo) 수행 [메타 데이터 정리](https://technet.microsoft.com/library/cc816907.aspx) 누락 된 도메인에 대 한 컨트롤러입니다. 



> [!IMPORTANT]
> Hello 다음 섹션에에서 설명 된 hello 구성의 일부 hello 표준/기본 도메인 컨트롤러 구성 되었습니다. 사용 되는 도메인 컨트롤러를 전용 toobe 작성 이러한 변경 내용 tooa 프로덕션 도메인 컨트롤러 합니다 toomake 하지 않으려면 사이트 복구에 대 한 장애 조치를 테스트 하 고 이러한 변경 내용을 toothat를 확인 합니다.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>가상화 세이프가드로 인한 문제 

Windows Server 2012부터 [Active Directory Domain Services에 추가 세이프가드가 기본적으로 제공됩니다](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). 이러한 보호 기능으로 hello 기본 하이퍼바이저 플랫폼이 Vm-generationid를 지 원하는 USN 롤백에 대 한 가상화 된 도메인 컨트롤러를 보호를 지원 합니다. Azure는 Windows Server 2012 또는 나중에 Azure 가상 컴퓨터를 실행 하는 도메인 컨트롤러 hello 추가 세이프 가드가 있음을 의미 있는 Vm-generationid를 지원 합니다. 


Hello VM-생성 Id를 다시 설정 hello AD DS 데이터베이스의 hello invocationID도 다시 설정, hello RID 풀이 무시 되 고 SYSVOL이 신뢰할 수 없는로 표시 됩니다. 자세한 내용은 참조 [소개 tooActive Directory 도메인 서비스 가상화](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) 및 [안전 하 게 DFSR 가상화](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

장애 조치 tooAzure VM-생성 Id의 다시 설정와 시작 하기 전에 hello 추가 세이프 가드가 Azure의 hello 도메인 컨트롤러 가상 컴퓨터가 시작 될 때. 이 될 수 있습니다는 **지연 시간이 상당한** 사용자 계정 수 toologin toohello 도메인 컨트롤러 가상 컴퓨터가 되 고 있습니다. 이 도메인 컨트롤러는 테스트 장애 조치(failover)에만 사용되므로 가상화 세이프가드가 필요 없습니다. hello 온-프레미스 도메인 컨트롤러에서 다음 DWORD too4 hello 값을 변경할 수 있습니다 hello 도메인 컨트롤러 가상 컴퓨터에 대 한 VM-생성 Id 변경 되지 않는 tooensure 합니다.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>가상화 세이프가드의 증상
 
테스트 장애 조치(failover) 후 가상화 세이프가드가 작동하는 경우 다음과 같은 증상 중 하나 이상이 나타날 수 있습니다.  

Generation ID 변경

![Generation ID 변경](./media/site-recovery-active-directory/Event2170.png)

Invocation ID 변경

![Invocation ID 변경](./media/site-recovery-active-directory/Event1109.png)

Sysvol 및 Netlogon 공유를 사용할 수 없음

![Sysvol 공유](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

모든 DFSR 데이터베이스가 삭제됨

![DFSR DB 삭제](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Hello 다음 섹션에에서 설명 된 hello 구성의 일부 hello 표준/기본 도메인 컨트롤러 구성 되었습니다. 사용 되는 도메인 컨트롤러를 전용 toobe 작성 이러한 변경 내용 tooa 프로덕션 도메인 컨트롤러 합니다 toomake 하지 않으려면 사이트 복구에 대 한 장애 조치를 테스트 하 고 이러한 변경 내용을 toothat를 확인 합니다.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>테스트 장애 조치(failover)를 수행하는 동안 도메인 컨트롤러 문제 해결


명령 프롬프트에서 SYSVOL 및 NETLOGON 폴더는 공유 여부 명령 toocheck 다음 hello를 실행 합니다.

    NET SHARE

Hello 명령 프롬프트에서 다음 도메인 컨트롤러를 hello tooensure가 제대로 작동 하는 명령을 hello를 실행 합니다.

    dcdiag /v > dcdiag.txt

Hello 출력 로그에 다음 텍스트 tooconfirm hello 도메인 컨트롤러를 찾습니다는 잘 작동 합니다. 

* "passed test Connectivity"
* "passed test Advertising"
* "passed test MachineAccount"

Hello 이전 조건이 충족 될 해당 hello 도메인 컨트롤러가 제대로 작동 합니다. 충족되지 않았으면 다음 단계를 수행합니다.


* Hello 도메인 컨트롤러의 정식 복원을 수행 합니다.
    * 없지만 [toouse FRS 복제 것은 좋지](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), 지금도 사용 되 고 다음 제공 된 hello 단계를 수행 하는 경우 [여기](https://support.microsoft.com/kb/290762) toodo 정식 복원 합니다. Hello 이전 링크에서 설명한 Burflags에 대해 자세히 알아볼 수 있습니다 [여기](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/)합니다.
    * DFSR 복제를 사용 하는 경우 다음 사용 가능한 hello 단계를 수행 [여기](https://support.microsoft.com/kb/2218556) toodo 정식 복원 합니다. 이 [링크](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/)에서 제공하는 Powershell 함수를 이 용도에 사용할 수도 있습니다. 
    
* 레지스트리 키 too0 hello 온-프레미스 도메인 컨트롤러에서 다음을 설정 하 여 초기 동기화 요구 사항을 무시 합니다. 이 DWORD가 없으면 '매개 변수' 노드에서 만들 수 있습니다. 자세한 내용은 [여기](https://support.microsoft.com/kb/2001093)서 확인할 수 있습니다.

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* 레지스트리 키 too1 hello 온-프레미스 도메인 컨트롤러에서 다음을 설정 하 여 글로벌 카탈로그 서버가 사용 가능한 toovalidate 사용자 로그온 하는지 hello 요구 사항을 사용 하지 않도록 설정 합니다. 이 DWORD가 없으면 'Lsa' 노드에서 만들 수 있습니다. 자세한 내용은 [여기](http://support.microsoft.com/kb/241789)서 확인할 수 있습니다.

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>다른 컴퓨터에서 DNS 및 도메인 컨트롤러
DNS hello에 없는 경우 동일한 가상 컴퓨터 hello 도메인 컨트롤러로 hello 테스트 장애 조치에 대 한 DNS VM toocreate 필요 합니다. 경우에 있을 경우 동일한 VM hello,이 섹션을 건너뛸 수 있습니다.

새 DNS 서버를 사용 하 고 모든 hello 필요한 영역을 만들 수 있습니다. 예를 들어 Active Directory 도메인이 contoso.com 인 경우 hello 이름 contoso.com와 DNS 영역을 만들 수 있습니다. tooActive 디렉터리에 해당 하는 hello 항목이 DNS에서 다음과 같이 업데이트 해야 합니다.

1. 이러한 설정 된 hello 복구 계획에 다른 가상 컴퓨터 상태가 되기 전에 확인 해야 합니다.
   
   * hello 포리스트 루트 이름을 hello 영역 이름을 지정 해야 합니다.
   * hello 영역 파일을 백업 해야 합니다.
   * hello 영역 보안 및 비보안 업데이트에 대해 활성화 되어야 합니다.
   * hello 도메인 컨트롤러 가상 컴퓨터의 hello 해결 프로그램은 hello DNS 가상 컴퓨터의 toohello IP 주소를 가리켜야 합니다.
2. Hello 도메인 컨트롤러 가상 컴퓨터에서 다음 명령을 실행 합니다.
   
    `nltest /dsregdns`
3. Hello DNS 서버에 영역을 추가 하 고 비보안 업데이트 허용 tooDNS 항목에 대 한 추가:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>다음 단계
읽기 [어떤 작업 부하를 보호할 수 있습니까?](site-recovery-workload.md) toolearn Azure Site Recovery와 엔터프라이즈 작업을 보호 하는 방법에 대 한 자세한 합니다.

