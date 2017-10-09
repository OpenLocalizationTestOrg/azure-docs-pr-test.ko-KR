---
title: "aaaReplicate VMware Vm 또는 실제 서버 tooanother 사이트 (Azure 클래식 포털) | Microsoft Docs"
description: "Azure Site Recovery와이 문서 tooreplicate VMware Vm 이나 Windows/Linux 물리적 서버의 tooa 보조 사이트를 사용 합니다."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>온-프레미스 VMware 가상 컴퓨터 또는 실제 서버 tooa hello 클래식 Azure 포털에서 보조 사이트를 복제 합니다.

## <a name="overview"></a>개요
Azure Site Recovery의 InMage Scout는 온-프레미스 VMWare 사이트 간의 실시간 복제 기능을 제공합니다. InMage Scout는 Azure Site Recovery 서비스 구독에 포함되어 있습니다. 

## <a name="prerequisites"></a>필수 조건
**Azure 계정**: [Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/) .

## <a name="step-1-create-a-vault"></a>1단계: 자격 증명 모음 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 새로 만들기 > 관리 > 백업 및 사이트 복구(OMS)를 클릭합니다. 또는 찾아보기 > Recovery Services 자격 증명 모음 > 추가를 클릭합니다.
3. **이름** 이름 tooidentify hello 자격 증명 모음을 지정 합니다. 구독이 두 개 이상인 경우 그 중에서 하나를 선택합니다.
4. **리소스 그룹**에서 새 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다. Azure 지역 toocomplete 필수 필드를 지정 합니다.
5. **위치**, 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 되는 toocheck 지역 참조 [Azure 사이트 복구 가격](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
6. 원하는 경우에 tooquickly 액세스 hello 자격 증명 모음 대시보드 hello에서 Pin toodashboard를 클릭 한 다음 만들기를 클릭 합니다.
7. hello 새 자격 증명 모음 대시보드 hello에 나타납니다. > 모든 리소스를 hello에 기본 복구 서비스 자격 증명 모음 고 블레이드 합니다.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>2 단계: hello 자격 증명 모음 구성 및 InMage Scout 구성 요소 다운로드
1. Hello 복구 서비스 자격 증명 모음 블레이드에서 자격 증명 모음을 선택 하 고 설정을 클릭 합니다.
2. **설정** > **시작**에서 **Site Recovery** > 1단계: **인프라 준비** > **보호 목표**를 클릭합니다.
3. **보호 목표** toorecovery 사이트를 선택 하 고 VMware vsphere 하이퍼바이저 예를 선택 합니다. 그런 후 확인을 클릭합니다.
4. **Scout 설치**, InMage Scout 8.0.1 GA toodownload 소프트웨어 및 등록 키 다운로드를 클릭 합니다. 모든 hello에 대 한 설치 파일 hello hello 다운로드 한.zip 파일에 구성 요소가 필요 합니다.

## <a name="step-3-install-component-updates"></a>3단계: 구성 요소 업데이트를 설치합니다.
Hello에 대 한 최근 읽기 [업데이트](#updates)합니다. 순서에 따라 hello에 hello 업데이트 파일 서버에 설치 합니다.

1. 하나인 경우 RX 서버
2. 서버 구성
3. 프로세스 서버
4. 마스터 대상 서버
5. vContinuum 서버.
6. 원본 서버(Windows 및 Linux 서버)

다음과 같이 hello 업데이트를 설치 합니다.

1. Hello 다운로드 [업데이트](https://aka.ms/asr-scout-update5) .zip 파일입니다. 이.zip 파일 hello를 다음 파일이 포함 되어 있습니다.

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA update4 bits for RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Hello.zip 파일을 추출 합니다.<br>
3. **RX 서버 hello에 대 한**: 복사 **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello RX 서버 압축을 풉니다. Hello를 실행 하는 폴더를 추출한 **/설치**합니다.<br>
4. **구성 서버/프로세스 서버 hello에 대 한**: 복사 **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello 구성 서버와 프로세스 서버입니다. Toorun 두 번 클릭 하 고 있습니다.<br>
5. **Hello Windows 마스터 대상 서버에 대 한**: tooupdate hello 에이전트, 복사 통합 **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello 마스터 대상 서버입니다. 두 번 클릭 toorun 것입니다. 통합 된 에이전트 hello는 소스 Update4까지 업데이트 되지 않은 경우 적용 가능한 toohello 원본 서버 이기도 합니다. 이 목록 뒷부분의 설명 했 듯이 hello 원본 서버와에를 설치 해야 있습니다.<br>
6. **Hello vContinuum 서버에 대 한**: 복사 **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum 서버입니다.  Hello vContinuum 마법사를 닫은 있는지 확인 합니다. 두 번 클릭 hello 파일 toorun 것입니다.<br>
7. **Hello Linux 마스터 대상 서버에 대 한**: tooupdate hello 에이전트, 복사 통합 **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello 마스터 대상 서버 하 고 압축을 풉니다. Hello를 실행 하는 폴더를 추출한 **/설치**합니다.<br>
8. **Windows 원본 서버 hello에 대 한**: 원본 update4에 이미 있으면 원본에 대해 tooinstall 업데이트 5 에이전트가 필요 하지 않습니다. 그럴 경우 update4 보다 작은 hello 업데이트 5 에이전트를 적용 됩니다.
tooupdate hello 에이전트, 복사 통합 **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello 소스 서버입니다. 두 번 클릭 toorun 것입니다. <br>
9. **Hello Linux 원본 서버에 대 한**: tooupdate 통합된 에이전트 hello UA 파일 toohello Linux 서버의 해당 버전을 복사 하 고 압축을 풉니다. Hello를 실행 하는 폴더를 추출한 **/설치**합니다.  예: RHEL 6.7 64 비트 서버에 대 한 복사 **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello 서버 압축을 풉니다. Hello를 실행 하는 폴더를 추출한 **/설치**합니다.

## <a name="step-4-set-up-replication"></a>4단계: 복제 설정
1. 사이트 hello 소스 및 대상 VMware 간의 복제를 설정 합니다.
2. 지침을 보려면 hello InMage Scout 설명서 다운로드 된 hello 제품과 함께 사용 합니다. 또는 다음과 같이 hello 설명서에 액세스할 수 있습니다.

   * [릴리스 정보](https://aka.ms/asr-scout-release-notes)
   * [호환성 매트릭스](https://aka.ms/asr-scout-cm)
   * [사용자 가이드](https://aka.ms/asr-scout-user-guide)
   * [RX 사용자 가이드](https://aka.ms/asr-scout-rx-user-guide)
   * [빠른 설치 가이드](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>업데이트
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 업데이트 5
Scout 업데이트 5는 누적 업데이트입니다. 까지 update4 및 새로운 버그 수정 및 향상 된 기능을 다음과 같은 업데이트 1의 hello 수정 사항이 모두가지고 있습니다.
수정 ASR Scout update4 tooupdate5에서 추가 되는 특정 tooMaster 대상 및 vContinuum 구성 요소입니다. 필요한 모든 원본 서버를 마스터 대상, 구성 서버, 프로세스 서버 및 RX이 아직 ASR Scout update4 다음 있습니다 tooapply 업데이트 5 마스터 대상 서버에만 합니다. 

**새 플랫폼 지원**
* SUSE Linux Enterprise Server 11 SP4(서비스 팩 4)

> [!NOTE]
> SLES 11 SP4 64비트 **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz**는 기본 Scout GA 패키지 **InMage_Scout_Standard_8.0.1 GA.zip**과 함께 패키지되어 있습니다. [1단계](#step-1-create-a-vault)에 설명된 대로 Scout GA 패키지를 다운로드합니다.
>

**버그 수정 및 향상된 기능**

* Windows 클러스터 지원 안정성 향상
    * 일부 hello P2V MSCS 클러스터 될 디스크를 고정 어느 시킵니다 RAW 복구 후
    * Toodisk 순서가 일치 하지 않습니다. 인해 실패할 자릿수 P2V MSCS 클러스터 복구
    * 수정됨 - 디스크 크기 불일치로 인해 MSCS 클러스터에서 디스크 작업 추가 실패
    * 수정됨 - 크기 확인에서 RDM LUN을 사용한 원본 MSCS 클러스터 매핑 준비 확인 실패
    * TooSCSI 불일치 문제가 인해 실패할 자릿수 단일 노드 클러스터 보호 
    * 대상 클러스터 디스크를 사용할 수 있는 경우 실패 자릿수 hello P2V Windows 클러스터 서버의 다시 보호 합니다. 
    
* 장애 복구 보호 하는 동안 선택한 MT에 없으면 hello 동일한 ESXi 서버 vContinuum 장애 복구 하는 동안 잘못 된 MT hello 선택 하 고 복구 작업이 실패 하면 이후에 (정방향 보호의 경우) 하는 동안 원본 컴퓨터를 보호 hello의 합니다.

> [!NOTE]
> 
> * P2V 클러스터 수정 위에 ASR Scout update5 새로 보호 된 해당 물리적 MSCS 클러스터 tooonly 적용할 수는 있습니다. tooavail hello 클러스터 수정 hello에 이미 이전 업데이트를 사용 하는 P2V MSCS 클러스터를 보호, 12 hello 섹션에 언급 된 toofollow hello 업그레이드 단계 필요, 업그레이드 보호 P2V MSCS의 클러스터 tooScout Update5 [ASR Scout 릴리스 메모](https://aka.ms/asr-scout-release-notes)합니다.
> 
> * 실제 MSCS 클러스터의 다시 보호 하는 경우 시에만 hello의 다시 보호 노드 때 처음으로 보호 하는 hello 클러스터의 각 디스크의 동일한 집합 상태인 hello 기존 대상 디스크 다시 사용할 수 있습니다. 그렇지 않은 다음 수동 단계가 경우 12의 섹션에서 설명 했 듯이 [ASR Scout 릴리스 정보](https://aka.ms/asr-scout-release-notes) 너무 hello 대상 쪽 디스크 toohello 올바른 데이터 저장소 경로 toore 사용 가능한 이동 다시 보호 하는 동안 해당 합니다. 업그레이드 단계를 수행 하지 않고 P2V 모드로 hello MSCS 클러스터를 다시 보호 하는 경우 hello 대상 ESXi 서버에 새 디스크를 만들 됩니다 것입니다. Toomanually delete hello hello 데이터 저장소에서 이전 디스크가 필요 합니다.
> 
> * 때마다 SLES11를 원본 또는 서비스 팩 서버 SLES11를 제대로 다시 부팅 한 hello로 수동으로 표시 해야 하나 **루트** CX UI에서 알림을 받지 것입니다 대로 다시 동기화에 대 한 복제 쌍 디스크. 이렇게 하지 않으면 ' 표시 hello 루트 디스크를 다시 동기화에 대 한 데이터 무결성 (DI) 문제를 표시 될 수 있습니다.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery 서비스 Scout 8.0.1 업데이트 4
Scout 업데이트 4는 누적 업데이트입니다. 까지 update3 및 새로운 버그 수정 및 향상 된 기능을 다음과 같은 업데이트 1의 hello 수정 사항이 모두가지고 있습니다.

**새 플랫폼 지원**

* vCenter/vSphere 6.0, 6.1 및 6.2에 대한 지원이 추가되었습니다.
* 다음 Linux 운영 체제에 대한 지원이 추가되었습니다.
  * Red Hat Enterprise Linux(RHEL)7.0, 7.1 및 7.2
  * CentOS 7.0, 7.1 및 7.2
  * Red Hat Enterprise Linux(RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64비트 **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz**가 기본 Scout GA 패키지 **InMage_Scout_Standard_8.0.1 GA.zip**에 패키지되어 있습니다. [1단계](#step-1-create-a-vault)에 설명된 대로 Scout GA 패키지를 다운로드합니다.
>
>

**버그 수정 및 향상된 기능**

* 향상된 된 종료 다음 Linux Os와 복제본 tooprevent 원치 않는 다시 동기화 문제를 처리 합니다.
  * Red Hat Enterprise Linux(RHEL) 6.x
  * Oracle Linux(OL) 6.x
* Linux 용 통합된 에이전트 설치 디렉터리의 사용 권한은 이제 전체 폴더 액세스 toohello 로컬 사용자만을 제한 합니다.
* Windows에서 SQL 및 SharePoint 클러스터와 같은 과도한 부하의 분산 응용 프로그램에서 일반적인 분산된 일관성 북마크가 발생하는 동안의 시간 초과 문제가 해결되었습니다.
* CX 기본 설치 관리자에 로그 관련 수정 프로그램이 추가되었습니다.
* VMware vCLI 6.0 다운로드 링크 tooWindows 마스터 대상의 기본 설치 관리자 추가 됩니다.
* 장애 조치 및 DR 드릴 중 네트워크 구성 변경에 대한 추가 확인 및 로그가 추가되었습니다.
* 어느 보존 정보가 보고 toohello CX 않습니다.  
* 실제 클러스터의 경우 원본 볼륨 축소가 발생했을 때 vContinuum 마법사를 통해 볼륨 크기 조정 작업이 실패합니다.
* 클러스터 보호 실패 했습니다 오류 "Failed toofind hello 디스크 서명" 클러스터 디스크가 PRDM 디스크인 경우.
* 범위 이탈 예외로 인해 cxps 전송 서버 작동이 중단됩니다.
* vContinuum 마법사의 푸시 설치 페이지에서 서버 이름 및 IP 열의 크기를 조정할 수 있습니다.
* RX API 향상 기능
  * 사용 가능한 5개의 최신 공통된 일관성 지점을 제공합니다(보장됨 태그만).
  * 모든 용량 및 사용 가능한 공간 세부 정보는 보호 장치 hello를 제공 합니다.
  * 원본 서버에서 Scout 드라이버 상태를 제공합니다.

> [!NOTE]
> * 이제 **InMage_Scout_Standard_8.0.1_GA.zip** 기본 패키지에서 CX 기본 설치 관리자 **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** 및 Windows 마스터 대상 기본 설치 관리자 **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**가 업데이트되었습니다. 모든 신규 설치에 새 CX 및 Windows 마스터 대상 GA 비트가 사용됩니다.
> * 업데이트 4를 8.0.1 GA에 직접 적용할 수 있습니다.
> * hello 구성 서버 및 RX 업데이트 hello 시스템에 적용 한 후에 다시 롤백할 수 없습니다.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery 서비스 Scout 8.0.1 업데이트 3
업데이트 3에 hello 다음과 같은 버그 수정 및 향상 된 기능:

* hello 구성 서버 및 RX tooregister toohello 사이트 복구 자격 증명 모음 hello 프록시 뒤에 있을 때 실패 합니다.
* hello 시간 hello 복구 지점 목표 (RPO)을 충족 되지 않으면 hello 상태 보고서의 업데이트 되지 않습니다.
* hello 구성 서버는 hello ESX 하드웨어 세부 정보 또는 네트워크 정보 u t F-8에 있는 문자를 사용할 때 하지 RX와 동기화 됩니다.
* Windows Server 2008 R2 도메인 컨트롤러는 복구 후 tooboot을 실패합니다.
* 오프라인 동기화는 예상대로 작동하지 않습니다.
* 가상 컴퓨터 (VM) 장애 조치 후 오랜 시간 동안 복제 쌍 삭제 hello CX UI에에서 걸릴 및 사용자가 다시 시작 작업 또는 hello 장애 복구를 완료할 수 없습니다.
* Hello 일관성 작업에 의해 수행 되는 스냅숏 작업 최적화 전반적인 toohelp 줄일 응용 프로그램 SQL 클라이언트와 같은 연결을 끊습니다.
* Windows에서 스냅숏을 만드는 데 필요한 hello 메모리 사용량을 줄여 hello 일관성 도구의 (VACP.exe) hello 성능이 향상 되었습니다.
* hello 푸시 hello 암호는 16 자를 초과할 경우 서비스 충돌을 설치 합니다.
* vContinuum 검사 및 hello 자격 증명을 변경할 때 새 vCenter 자격 증명을 묻는 메시지가 표시 되지 않는 합니다.
* Linux에서 하지 hello 마스터 대상 캐시 관리자 (cachemgr) 복제 쌍 제한으로 인해 hello 프로세스 서버에서 파일을 다운로드 됩니다.
* Hello 물리적 장애 조치 클러스터 (MSCS) 디스크 순서 이면 하지 모든 hello 노드에서 hello 동일 hello 클러스터 볼륨 중 일부에 대해 복제가 설정 되지 않았습니다.
  <br/>해당 hello 클러스터 필요한 toobe 참고 tootake 이점은이 수정 프로그램의 다시 보호 합니다.  
* SMTP 기능 RX가 Scout 7.1 tooScout 8.0.1에서에서 업그레이드 된 후 예상 대로 작동 하지 않습니다.
* 기타 통계 toocomplete 걸렸습니다 hello 롤백 작업 tootrack hello 시간에 대 한 hello 로그에 추가 된 것입니다.
* Hello 원본 서버에서 Linux 운영 체제에 대 한 지원이 추가 되었습니다.
  * RHEL(Red Hat Enterprise Linux) 6 업데이트 7
  * CentOS 6 업데이트 7
* hello CX 및 RX UI에 비트맵 모드로 전환 되는 hello 쌍에 대 한 hello 알림을 표시 수 있습니다.
* hello 다음 보안 수정에에서 추가 되었음 RX:

| **문제 설명** | **구현 절차** |
| --- | --- |
| 매개 변수 변조를 통해 권한 부여 바이패스 |제한 된 액세스 toonon 적용 가능한 사용자입니다. |
| 교차 사이트 요청 위조 |모든 페이지에 대해 임의로 생성 하는 구현 된 hello 페이지 토큰 개념입니다. <br/>이를 통해 다음을 확인할 수 있습니다. <li> 만 단일 로그인 인스턴스는 hello에 대 한 동일한 사용자입니다.</li><li>페이지 새로 작동 하지 않습니다.-toohello 대시보드 리디렉션됩니다.</li> |
| 악성 파일 업로드 |제한 된 파일 toocertain 확장입니다. 허용된 확장자: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml, and zip. |
| 영구 사이트 간 스크립팅 |추가된 입력 유효성 검사 |

> [!NOTE]
> * 모든 사이트 복구 업데이트는 누적됩니다. 업데이트 3의 업데이트 1 및 업데이트 2의 모든 hello 수정 합니다. 업데이트3은 8.0.1 GA에 직접 적용할 수 있습니다.
> * hello 구성 서버 및 RX 업데이트 hello 시스템에 적용 한 후에 다시 롤백할 수 없습니다.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery 서비스 Scout 8.0.1 업데이트 2(2015년 12월 3일 업데이트)
업데이트 2에서 수정 사항은 다음과 같습니다.

* **구성 서버**: 예상 대로 hello 구성 서버 Site Recovery에 등록 되었습니다. hello 31 일 무료 계량 기능 작동에서 되지 않는 문제에 대 한 수정 합니다.
* **통합 된 에이전트**: hello 업데이트 설치 되 고 있지 hello 마스터 대상 서버에 버전 8.0 too8.0.1에서 업그레이드 된 경우에 발생 하는 업데이트 1에서 문제에 대 한 수정 합니다.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery 서비스 Scout 8.0.1 업데이트 1
업데이트 1에 hello 다음과 같은 버그 픽스와 새로운 기능:

* 서버 인스턴스 당 31일간 무료 보호됩니다. 이렇게 하면 tootest 기능 또는--개념 증명을 설정 합니다.
  * 장애 조치 및 장애 복구를 포함 하 여 hello 서버에 대 한 모든 작업 사용할 수 있는 hello에 대 한 첫 번째 31 일 하는 서버를 먼저 사이트 복구 Scout 암호로 hello 시간에서 시작 합니다.
  * Hello에서 32 날부터, 각 보호 된 서버 청구 됩니다 Azure Site Recovery 보호 tooa 고객 소유의 사이트에 대 한 hello 표준 인스턴스 비율입니다.
  * 언제 든 지 현재 청구 하는 보호 된 서버의 hello 수는 hello Azure Site Recovery 자격 증명 모음의 hello 대시보드 페이지에서 사용할 수 있습니다.
* vSphere 명령줄 인터페이스 (vCLI) 5.5 업데이트 2에 대한 지원이 추가됩니다.
* Hello 원본 서버에서 Linux 운영 체제에 대 한 추가 지원:
  * RHEL 6 업데이트 6
  * RHEL 5 업데이트 11
  * CentOS 6 업데이트 6
  * CentOS 5 업데이트 11
* 버그 수정 tooaddress hello 될:
  * RX 서버나 hello 구성 서버에 대 한 자격 증명 모음 등록 실패합니다.
  * 다시 시작할 때 가상 컴퓨터가 다시 보호되면 클러스터 볼륨이 예상대로 표시되지 않습니다.
  * 장애 복구 hello 마스터 대상 서버 hello 온-프레미스 프로덕션 가상 컴퓨터에서 다른 ESXi 서버에서 호스트 되 면 실패 합니다.
  * 보호 및 작업에 영향을 주는 too8.0.1를 업그레이드 하는 경우 구성 파일 사용 권한은 변경 됩니다.
  * hello 다시 동기화 임계값 보장 되지 않습니다 예상 대로 tooinconsistent 복제 동작을 유발입니다.
  * hello 구성 서버 인터페이스에 hello RPO 설정을 제대로 나타나지 않습니다. hello 압축 되지 않은 데이터 값 hello 압축 값을 올바르게 표시 합니다.
  * hello vContinuum 마법사에서 예상 대로 hello 제거 작업이 삭제 되지 않습니다 및 복제 hello 구성 서버 인터페이스에서 삭제 되지 않습니다.
  * Hello vContinuum 마법사에서 hello 디스크 선택 하지 않으면 자동으로 클릭 하면 **세부 정보** MSCS 가상 컴퓨터의 보호 하는 동안 hello 디스크 뷰에서 합니다.
  * Hello 물리적 컴퓨터 가상 (P2V) 시나리오 중 CIMnotify 등 CqMgHost, 필요한 HP 서비스에 가상 컴퓨터 복구에서 이동된 toomanual 되지 않습니다. 이 때문에 부팅 시간이 늘어납니다.
  * Linux 가상 컴퓨터 보호 hello 마스터 대상 서버에 26 개 이상의 디스크 있을 경우 실패 합니다.

## <a name="next-steps"></a>다음 단계
Hello에 있는 모든 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.
