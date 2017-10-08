---
title: "aaaMonitor 및 가상 컴퓨터 및 물리적 서버에 대 한 보호 문제 해결 | Microsoft Docs"
description: "Azure Site Recovery hello 복제, 장애 조치 및 온-프레미스 서버 tooAzure 또는 보조 데이터 센터에 있는 가상 컴퓨터의 복구를 조정 합니다. 이 문서 toomonitor를 사용 하 고 Virtual Machine Manager 또는 Hyper-v 사이트 보호를 해결 합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>가상 컴퓨터 및 물리적 서버를 위한 보호 모니터링 및 문제 해결
이 모니터링 및 배웁니다이 가이드에서는 문제 해결 방법을 tootrack 복제 상태 및 Azure 사이트 복구에 대 한 기술 문제를 해결 합니다.

## <a name="understand-hello-components"></a>Hello 구성 요소 이해
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>온-프레미스와 Azure 간 복제를 위한 VMware 가상 컴퓨터 또는 물리적 서버 사이트 배포
온-프레미스 VMware 가상 컴퓨터 또는 물리적 서버와 Azure 간 데이터베이스 복구를 tooset, tooset hello 구성 서버, 마스터 대상 서버 및 가상 컴퓨터 또는 서버에 프로세스 서버 구성 요소를 필요합니다. Hello 원본 서버에 대 한 보호를 사용 하도록 설정 하면 Azure Site Recovery는 Microsoft Azure 앱 서비스의 hello 모바일 앱 기능을 설치 합니다. 온-프레미스 중단 후 및 hello 원본 서버에 오류가 발생 tooAzure 통해 이후 고객 tooset Azure에 프로세스 서버와 온-프레미스에서 온 프레미스 toorebuild hello 원본 서버에서 마스터 대상 서버를 해야합니다.

![온-프레미스와 Azure 간 복제를 위한 VMware/물리적 사이트 배포](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>온-프레미스 사이트 간 복제를 위한 가상 컴퓨터 관리자 사이트 배포
두 데이터베이스 복구를 tooset 온-프레미스 위치, toodownload hello Azure Site Recovery 공급자에 있어야 하 고 hello Virtual Machine Manager 서버에 설치 합니다. hello 공급자가 인터넷 연결 tooensure hello Azure 포털에서에서 시작 되는 모든 hello 작업 가져오기 번역 된 tooon 온-프레미스 작업을 합니다.

![온-프레미스 사이트 간 복제를 위한 가상 컴퓨터 관리자 사이트 배포](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>온-프레미스 위치와 Azure 간 복제를 위한 가상 컴퓨터 관리자 사이트 배포
온-프레미스 위치와 Azure 간의 복구 데이터베이스를 설정 하면 toodownload hello Azure Site Recovery 공급자에 있어야 하 고 hello Virtual Machine Manager 서버에 설치 합니다. Tooinstall hello Azure 복구 서비스 에이전트는 toobe 각 Hyper-v 호스트에 설치 해야 합니다. 자세한 내용은 [자세히 알아보기](site-recovery-hyper-v-azure-architecture.md)를 참조하세요.

![온-프레미스 위치와 Azure 간 복제를 위한 가상 컴퓨터 관리자 사이트 배포](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>온-프레미스 위치와 Azure 간 복제를 위한 Hyper-V 사이트 배포
이 프로세스는 유사 tooVirtual Machine Manager 배포입니다. hello만 차이점은 hello Azure Site Recovery provider 및 Azure 복구 서비스 에이전트 자체 hello Hyper-v 호스트에 설치 된 가져오기입니다. [자세히 알아봅니다](site-recovery-hyper-v-azure-architecture.md). 등 4가지 유형의 클러스터가 제공됩니다.

## <a name="monitor-configuration-protection-and-recovery-operations"></a>구성, 보호 및 복구 작업 모니터링
Azure Site Recovery에서 모든 작업을 감사 하 고 hello에서 추적 **작업** 탭 합니다. 모든 구성, 보호 또는 복구 오류에 대 한 이동 toohello **작업** 탭 하 고 오류 찾아보십시오.

![hello 작업 탭에 있는 hello 실패 필터](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Hello에서 오류를 찾을 경우 **작업** 탭, hello 작업을 클릭 하 고 클릭 **오류 세부 정보** 해당 작업에 대 한 합니다.

![hello 오류 세부 정보 단추](media/site-recovery-monitoring-and-troubleshooting/image4.png)

hello 오류 세부 정보는 가능한 원인 및 hello 문제에 대 한 권장 사항을 식별 하는 데 도움이 됩니다.

![특정 작업에 대한 오류 세부 정보를 보여 주는 대화 상자](media/site-recovery-monitoring-and-troubleshooting/image5.png)

Hello 이전 예제에서는 다른 작업이 진행 중인 toobe hello 보호 구성 toofail를 일으키는 것 같습니다. Hello 권장 사항을 기반으로 하는 hello 문제를 해결 한 다음 클릭 **RESART** tooinitiate hello 작업을 다시 합니다.

![hello 작업 탭에서 hello 다시 시작 단추](media/site-recovery-monitoring-and-troubleshooting/image6.png)

hello **다시 시작** 옵션은 모든 작업에 대해 사용할 수 없습니다. 작업 hello에 없는 경우 **다시 시작** 옵션을 toohello 개체 뒤로 이동 하 고 작업을 다시 hello를 다시 실행 합니다. 진행 중인 모든 작업을 취소할 수 hello를 사용 하 여 **취소** 단추입니다.

![hello 취소 단추](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>가상 컴퓨터에 대한 복제 상태 모니터링
각 보호 된 hello 엔터티에 대 한 hello Azure 포털 tooremotely 모니터 Azure 사이트 복구 공급자를 사용할 수 있습니다. **보호된 항목**을 클릭한 다음 **VMM 클라우드** 또는 **보호 그룹**을 클릭합니다. hello **VMM 클라우드에** 탭은만 가상 컴퓨터 관리자에 기반 하는 배포에 사용할 수 있습니다. 다른 시나리오에 대 한 hello에서 보호 하는 hello 엔터티는 **보호 그룹** 탭 합니다.

![hello VMM 클라우드 및 보호 그룹 옵션](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Hello 해당 클라우드 또는 보호 그룹 toosee hello 아래쪽 창에 표시 된 사용 가능한 모든 작업에서 보호 되는 엔터티를 클릭 합니다.

![선택한 보호된 엔터티에 대한 사용 가능한 옵션](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Hello 이전 스크린 샷에 표시 된 것과 같이 hello 가상 컴퓨터 상태가 **위험**합니다. Hello를 클릭할 수 있는 **오류 세부 정보** 단추 hello 아래쪽 toosee hello 오류 발생 시. Hello에 따라 **원인은** 및 **권장**, hello 문제를 해결 합니다.

![hello 오류 세부 정보 단추](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![오류 및 hello 오류 세부 정보 대화 상자에서 권장 사항](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> 모든 활성 작업이 진행 중인 또는 toohello 이동 실패 한 경우 **작업** 특정 작업에 대 한 이전 tooview hello 오류에서 언급 한 보기입니다.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>온-프레미스 Hyper-V 문제 해결
Toohello 온-프레미스 Hyper-v manager 콘솔을 선택 하는 hello 가상 컴퓨터를 연결 하 고 hello 복제 상태를 확인 합니다.

![Hello Hyper-v manager 콘솔에서 옵션 tooview 복제 상태](media/site-recovery-monitoring-and-troubleshooting/image12.png)

이 경우 **복제 상태**는 **위험**입니다. Hello 가상 컴퓨터를 마우스 오른쪽 단추로 누른 **복제** > **복제 상태 보기** toosee hello 세부 정보입니다.

![특정 가상 컴퓨터에 대한 복제 상태](media/site-recovery-monitoring-and-troubleshooting/image13.png)

복제는 hello 가상 컴퓨터에 대 한 일시 중지 되 면 hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 **복제** > **복제 다시 시작**합니다.

![Hello Hyper-v manager 콘솔에서 tooresume 복제 옵션](media/site-recovery-monitoring-and-troubleshooting/image19.png)

가상 컴퓨터는 독립 실행형 컴퓨터 또는 hello 클러스터 내에 있는 새 Hyper-v 호스트를 마이그레이션하는 경우 Azure Site Recovery를 통해 hello Hyper-v 호스트를 구성한 hello 가상 컴퓨터에 대 한 복제 영향을 하지 않습니다. 해당 hello 새 Hyper-v 호스트에서 모든 hello 필수 조건을 충족 하며 Azure Site Recovery를 사용 하 여 구성 확인 합니다.

### <a name="event-log"></a>이벤트 로그
| 이벤트 원본 | 세부 정보 |
| --- |:--- |
| **응용 프로그램 및 서비스 로그/Microsoft/VirtualMachineManager/Server/Admin**(가상 컴퓨터 관리자 서버) |유용한 로깅 tootroubleshoot 많은 다른 Virtual Machine Manager 문제를 제공합니다. |
| **응용 프로그램 및 서비스 로그/MicrosoftAzureRecoveryServices/Replication**(Hyper-V 호스트) |유용한 로깅 tootroubleshoot 많은 Microsoft Azure 복구 서비스 에이전트 문제를 제공합니다. <br/> ![Hyper-V 호스트에 대한 복제 이벤트 원본 위치](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **응용 프로그램 및 서비스 로그/Microsoft/Azure Site Recovery/Provider/Operational**(Hyper-V 호스트) |유용한 로깅 tootroubleshoot 많은 Microsoft Azure Site Recovery 서비스 문제를 제공합니다. <br/> ![Hyper-V 호스트에 대한 작업 이벤트 원본 위치](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **응용 프로그램 및 서비스 로그/Microsoft/Windows/Hyper-V-VMMS/Admin**(Hyper-V 호스트) |유용한 로깅 tootroubleshoot 많은 Hyper-v 가상 컴퓨터 관리 문제를 제공합니다. <br/> ![Hyper-V 호스트에 대한 가상 컴퓨터 관리자 이벤트 원본 위치](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Hyper-V 복제 로깅 옵션
하이퍼-V-VMMS hello에 tooHyper 복제와 관련 된 모든 이벤트가 기록 됩니다\\관리 로그 응용 프로그램 및 서비스 로그 아래에 있는\\Microsoft\\Windows 합니다. 또한 Hyper-v 가상 컴퓨터 관리 서비스 hello에 대 한 분석 로그를 사용할 수 있습니다. tooenable 로그인이 먼저 분석 hello를 확인 및 디버그 로그 이벤트 뷰어 hello에서 볼 수 있습니다. 이벤트 뷰어를 연 다음 **보기** > **분석 및 디버그 로그 표시**를 클릭합니다.

![hello 분석 및 디버그 로그 표시 옵션](media/site-recovery-monitoring-and-troubleshooting/image14.png)

분석 로그가 **Hyper-V-VMMS** 아래에 표시됩니다.

![hello 분석 hello 이벤트 뷰어의 트리 로그인](media/site-recovery-monitoring-and-troubleshooting/image15.png)

Hello에 **동작** 창에서 클릭 **로그 사용**합니다. 그러면 **성능 모니터**에서 **데이터 수집기 집합**에 있는 **이벤트 추적 세션**으로 나타납니다.

![Hello 성능 모니터 트리의 이벤트 추적 세션](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello 수집 된 정보, 먼저 hello 로그를 사용 하지 않도록 설정 하 여 hello 추적 세션을 중지 합니다. Hello 로그를 저장 하 고 이벤트 뷰어의 다시 열 또는 다른 도구 tooconvert를 사용 하 여 원하는 대로 것입니다.

## <a name="reach-out-for-microsoft-support"></a>Microsoft 지원을 위한 연락
### <a name="log-collection"></a>로그 수집
가상 컴퓨터 관리자 사이트 보호에 대 한 참조 너무[지원 진단 플랫폼 (SDP) 도구를 사용 하 여 Azure 사이트 복구 로그 컬렉션](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello 로그 필요 합니다.

Hyper-v 사이트 보호에 대 한 다운로드는 [도구](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) hello Hyper-v 호스트 toocollect hello 로그에 실행 합니다.

/ 물리적 서버 시나리오에 대 한 참조 너무[VMware와 물리적 사이트 보호에 대 한 Azure 사이트 복구 로그 컬렉션](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello 로그 필요 합니다.

hello 도구 %LocalAppData%\ElevatedDiagnostics 임의로 지정 된 하위 폴더에 로컬로 hello 로그를 수집합니다.

![Hyper-V 사이트 보호에서 표시된 샘플 단계입니다.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>지원 티켓 열기
URL을 사용 하 여 Azure Site Recovery에 대 한 지원 티켓 tooraise tooAzure 지원 연락에 <http://aka.ms/getazuresupport>합니다.

## <a name="kb-articles"></a>기술 자료 문서
* [Toopreserve hello 드라이브 문자에 대 한 장애 조치 됩니다 또는 tooAzure 마이그레이션되는 가상 컴퓨터를 보호 하는 방법을](http://support.microsoft.com/kb/3031135)
* [어떻게 toomanage 온-프레미스 tooAzure 보호 네트워크 대역폭 사용](https://support.microsoft.com/kb/3056159)
* [가상 컴퓨터에 대 한 tooenable 보호 시 azure 사이트 복구: "hello 클러스터 리소스 없습니다" 오류 발생](http://support.microsoft.com/kb/3010979)
* [Hyper-V 복제 이해 및 문제 해결 가이드](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>일반적인 Azure Site Recovery 오류 및 해결 방법
다음은 일반적 오류 및 해결 방법입니다. 각 오류는 개별 wiki 페이지에 설명되어 있습니다.

### <a name="general"></a>일반
* <span style="color:green;">신규</span> [작업이 실패하고 "작업이 진행 중입니다." 오류가 표시됩니다. 오류 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">새</span> ["서버를 연결 된 toohello 인터넷 없는" 오류로 인해 실패 한 작업입니다. 오류 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>설정
* [tooan 내부 오류로 인해 hello Virtual Machine Manager 서버를 등록할 수 없습니다. Hello 오류에 대 한 자세한 내용은 hello Site Recovery 포털에서 toohello 작업 보기를 참조 하십시오. 설치 프로그램 실행 다시 tooregister hello 서버입니다.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [연결이 설정 된 toohello Hyper-v 복구 관리자 자격 증명 모음 일 수 없습니다. Hello 프록시 설정을 확인 하거나 나중에 다시 시도 하십시오.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>구성
* [보호 그룹 수 없습니다 toocreate: hello 서버 목록을 검색 하는 동안 오류가 발생 했습니다.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Hyper-v 호스트 클러스터에 고정 네트워크 어댑터가 하나 이상 없거나 연결 된 어댑터가 없습니다 구성된 toouse DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager에 없는 사용 권한을 toocomplete 동작 합니다.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [보호를 구성 하는 동안 hello 구독 내에서 hello 저장소 계정을 선택할 수 없습니다.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>보호
* <span style="color:green;">새</span> ["보호를 hello 가상 컴퓨터에 대해 구성할 수 없습니다" 오류로 인해 실패 한 보호에 사용 합니다. 오류 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">새</span> ["hello 가상 컴퓨터에 대 한 보호를 사용할 수 없습니다." 오류로 인해 실패 한 보호 사용 오류 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">새</span> [hello 가상 컴퓨터 실시간 마이그레이션 오류 23848-toobe Live 유형을 사용 하 여 진행 됩니다. 이 hello 가상 컴퓨터의 hello 복구 보호 상태를 손상 시킬 수 있습니다.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [호스트 컴퓨터에 에이전트가 설치되어 있지 않아 보호를 사용하도록 설정하지 못했습니다.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Toolow 계산 리소스 인해 hello 복제 가상 컴퓨터에 적합 한 호스트에서 찾을 수 없습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Toono 논리 네트워크에 연결 된 인해 hello 복제 가상 컴퓨터에 적합 한 호스트에서 찾을 수 없습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Toohello 복제본 호스트 컴퓨터에서 연결할 수 없는 연결을 설정할 수 없습니다.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>복구
* 가상 컴퓨터 관리자는 hello 호스트 작업을 완료할 수 없습니다.
  * [장애 조치 가상 컴퓨터에 대 한 복구 지점 선택한 toohello: 일반 액세스 거부 오류입니다.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Toohello 통해 실패 한 toofail Hyper-v 가상 컴퓨터에 대 한 복구 지점을 선택: 작업이 중단 되었습니다.  최근 복구 지점을 사용하세요. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Hello 서버와의 연결이 설정 된 (0x00002EFD) 수 없습니다.
    * [Hyper-v 가상 컴퓨터에 대 한 tooenable 역방향 복제에 실패 했습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-v 가상 컴퓨터 가상 컴퓨터에 대 한 tooenable 복제에 실패 했습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [가상 컴퓨터에 장애 조치를 커밋하지 못했습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [계획 된 장애 조치를 수행할 준비가 되지 않는 가상 컴퓨터를 포함 하는 hello 복구 계획은 합니다.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [hello 가상 컴퓨터가 계획 된 장애 조치 준비 되지 않았습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [가상 컴퓨터가 실행되고 있지 않으며 전원이 꺼져 있습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [가상 컴퓨터에 대역 외 작업이 발생하고 장애 조치(failover)를 커밋하지 못했습니다.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* 테스트 장애 조치(Failover)
  * [테스트 장애 조치(Failover)가 진행 중이므로 장애 조치(Failover)를 시작할 수 없습니다.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">새</span> 장애 조치 시간이 초과 작업과' PreFailoverWorkflow WaitForScriptExecutionTaskTimeout' hello hello 가상 컴퓨터 또는 hello 서브넷 toowhich hello 컴퓨터와 연결 된 네트워크 보안 그룹의 구성 설정을 toohello 기한 에 속해 있습니다. 너무 참조['PreFailoverWorkflow task WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) 대 한 자세한 내용은 합니다.

### <a name="configuration-server-process-server-master-target"></a>구성 서버, 프로세스 서버, 마스터 대상
* [PS/CS VM으로 호스트 되는 hello에 hello ESXi 호스트 사망의 자주색 화면 실패 합니다.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>장애 조치(Failover) 후 원격 데스크톱 문제 해결
* 많은 고객이 Azure에서 가상 컴퓨터를 조치할 문제 tooconnect toohello를 직면 한 합니다. [문서 tooRDP hello 가상 컴퓨터 문제 해결을 사용 하 여 hello](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)합니다.

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>리소스 관리자 가상 컴퓨터에 공용 IP 추가
경우 hello **연결** hello 포털에서 단추는 흐리게 표시 되 면 및 Express 경로 또는 사이트 간 VPN 연결을 통해 연결 된 tooAzure 없는, toocreate 필요 하 고 원격을 사용 하려면 먼저 가상 컴퓨터를 공용 IP 주소 할당 데스크톱/공유 셸입니다. 그런 다음 hello 가상 컴퓨터의 네트워크 인터페이스 hello에서 공용 IP를 추가할 수 있습니다.  

![가상 컴퓨터를 통해의 hello 네트워크 인터페이스에서 공용 IP를 추가 하지 못했습니다.](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
