---
title: "Azure Site Recovery와 DR aaaAutomate StorSimple fileshare | Microsoft Docs"
description: "Hello 단계와 Microsoft Azure StorSimple 저장소에서 호스팅되는 파일 공유에 대 한 재해 복구 솔루션을 만들기 위한 모범 사례를 설명 합니다."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>StorSimple에서 호스트되는 파일 공유에 Azure Site Recovery를 사용하는 자동화된 재해 복구 솔루션
## <a name="overview"></a>개요
Microsoft Azure StorSimple 주소 hello 일반적으로 파일 공유와 관련 된 구조화 되지 않은 데이터의 복잡성을 하는 하이브리드 클라우드 저장소 솔루션입니다. StorSimple의 hello 확장 온-프레미스 솔루션 및 온-프레미스 저장소와 클라우드 저장소에서 데이터를 자동으로 눈금으로 클라우드 저장소를 사용 합니다. 데이터 보호와 통합 된 로컬 및 클라우드 스냅숏, 대 한 저장소 인프라에 대 한 hello 필요성을 제거 합니다.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) 는 가상 컴퓨터의 복제, 장애 조치(failover) 및 복구를 오케스트레이션하여 DR(재해 복구) 기능을 제공하는 Azure 기반 서비스입니다. Azure Site Recovery에는 다양 한 복제 기술 tooconsistently replicate 지원, 보호, 및 원활 하 게 가상 컴퓨터 및 응용 프로그램 tooprivate/공개 또는 호스 티 드 클라우드에 장애 조치할 합니다.

Azure 사이트 복구, 가상 컴퓨터 복제 및 StorSimple 클라우드 스냅숏 기능을 사용 하 여, 전체 파일 서버 환경 hello를 보호할 수 있습니다. 중단의 hello 이벤트를 한 번의 클릭 toobring 파일에는 몇 분만에 Azure에서 온라인 공유를 사용할 수 있습니다.

이 문서에서는 StorSimple 저장소에서 호스트되는 파일 공유를 위한 재해 복구 솔루션을 만들고 원클릭 복구 계획을 사용하여 계획된 장애 조치(failover), 계획되지 않은 장애 조치(failover) 및 테스트 장애 조치(failover)를 수행하는 방법을 자세히 설명합니다. 기본적으로 재해 시나리오 중 Azure 사이트 복구 자격 증명 모음 tooenable StorSimple 장애에서에서 복구 계획 hello를 수정 하는 방법을 보여 줍니다. 또한 지원되는 구성 및 필수 조건을 설명합니다. 이 문서에서는 Azure Site Recovery 및 StorSimple 아키텍처의 hello 기본 사항을 잘 알고 있다면를 가정 합니다.

## <a name="supported-azure-site-recovery-deployment-options"></a>지원되는 Azure Site Recovery 배포 옵션
고객은 파일 서버를 Hyper-V 또는 VMware에서 실행되는 물리적 서버 또는 VM(가상 컴퓨터)으로 배포한 다음 StorSimple 저장소의 잘라낸 볼륨에서 파일 공유를 만들 수 있습니다. Azure Site Recovery는 보조 사이트나 tooAzure 두 물리적 및 가상 배포 tooeither를 보호할 수 있습니다. 이 문서에서는 StorSimple 저장소에서 파일 공유 및 Hyper-v에서 VM을 호스팅할 파일 서버에 대 한 hello 복구 사이트와 Azure DR 솔루션의 세부 정보를 다룹니다. 마찬가지로 VMware VM 또는 물리적 컴퓨터에는 hello 파일 서버 VM이 다른 시나리오를 구현할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
StorSimple 저장소에서 호스팅되는 파일 공유에 대 한 Azure Site Recovery를 사용 하는 한 번의 클릭 재해 복구 솔루션 구현 hello 다음 필수 구성 요소에 있습니다.

* Hyper-V 또는 VMware나 물리적 컴퓨터에서 호스트되는 온-프레미스 Windows Server 2012 R2 파일 서버 VM
* Azure StorSimple Manager에 등록된 온-프레미스 StorSimple 저장소 장치
* (이에 보관할 수 종료 상태) hello Azure StorSimple manager에서 만든 StorSimple 클라우드 어플라이언스
* Hello StorSimple 저장소 장치에 구성 된 hello 볼륨에서 호스팅되는 파일 공유
* [Azure Site Recovery 서비스 자격 증명 모음](../site-recovery/site-recovery-vmm-to-vmm.md) 

또한 Azure는 복구 사이트를 실행 hello [Azure 가상 컴퓨터 준비 평가 도구](http://azure.microsoft.com/downloads/vm-readiness-assessment/) Azure Vm 및 Azure 사이트 복구와 호환 되는 Vm tooensure에 서비스입니다.

(비용이 더 많이 발생 시킬 수) 있는 tooavoid 대기 시간 문제 StorSimple 클라우드 어플라이언스, 자동화 계정 만들기 및 저장소 계정에서 hello 동일한 지역에 있는지 확인 합니다.

## <a name="enable-dr-for-storsimple-file-shares"></a>StorSimple 파일 공유에 DR 사용
Hello의 각 구성 요소 온-프레미스 환경에 필요한 보호 toobe tooenable 복제 및 복구 합니다. 이 섹션에서는 다음 방법을 설명합니다.

* Active Directory 및 DNS 복제 설정(선택 사항)
* Hello 파일 서버 VM의 Azure Site Recovery tooenable 보호를 사용 하 여
* StorSimple 볼륨의 보호 사용
* Hello 네트워크 구성

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Active Directory 및 DNS 복제 설정(선택 사항)
원하는 경우 tooprotect hello tooexplicitly 해야 hello DR 사이트에서 사용할 수 있도록 Active Directory 및 DNS를 실행 하는 컴퓨터를 보호 합니다 (있도록 hello 파일 서버 인증에 대 한 장애 조치 후에 액세스할 수 있는). Hello 복잡 한 hello 고객의 온-프레미스 환경에 따라 두 가지 권장된 옵션이 있습니다.

#### <a name="option-1"></a>옵션 1
Hello 고객이 응용 프로그램 수가 적은 경우 hello 전체에 대 한 단일 도메인 컨트롤러 온-프레미스 사이트와 Azure 사이트 복구 복제 tooreplicate hello 도메인 컨트롤러 컴퓨터를 사용 하는 것이 좋습니다 hello 전체 사이트를 통해 실패 tooa 보조 사이트 (사이트 간 및 Azure 사이트에 둘 다에 적용 됩니다).

#### <a name="option-2"></a>옵션 2
Hello 고객 응용 프로그램의 많은 수 없는 Active Directory 포리스트에 실행 하 고 한 번에 몇 가지 응용 프로그램에 비해 실패할 수 다음 hello DR 사이트에서 추가 도메인 컨트롤러 설정 것이 좋습니다 (보조 사이트 또는 Azure).

너무를 참조 하십시오[Active Directory 및 DNS를 Azure Site Recovery를 사용 하 여 자동화 된 DR 솔루션](../site-recovery/site-recovery-active-directory.md) hello DR 사이트에서 도메인 컨트롤러를 사용할 수 있도록 하는 경우의 지침에 대 한 합니다. 이 문서의 나머지 hello에 대 한 hello DR 사이트에서 도메인 컨트롤러를 사용할 수 있는 가정 합니다.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Hello 파일 서버 VM의 Azure Site Recovery tooenable 보호를 사용 하 여
이 단계는 hello 온-프레미스 파일 서버 환경을 준비, 만들기 및는 Azure Site Recovery 자격 증명 모음을 준비 하는 hello VM의 파일 보호를 사용 하도록 설정 해야 합니다.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>tooprepare hello 온-프레미스 파일 서버 환경
1. 집합 hello **사용자 계정 컨트롤** 너무**Never Notify**합니다. 키를 Azure 사이트 복구는 실패 한 후 Azure 자동화 스크립트 tooconnect hello iSCSI 대상을 사용할 수 있도록 이것이 필요 합니다.

   1. Hello Windows 키 + Q를 누르고 검색 **UAC**합니다.
   2. **사용자 계정 컨트롤 설정 변경**을 선택합니다.
   3. 막대 toohello 아래쪽으로 끌어서 hello **Never Notify**합니다.
   4. **확인**을 클릭한 다음 메시지가 표시되면 **예**를 선택합니다.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. 각 hello 파일 서버 Vm hello VM 에이전트를 설치 합니다. Hello 장애 조치 Vm에 Azure 자동화 스크립트를 실행할 수 있도록 이것이 필요 합니다.

   1. [Hello 에이전트 다운로드](http://aka.ms/vmagentwin) 너무`C:\\Users\\<username>\\Downloads`합니다.
   2. 관리자 모드 (관리자 권한으로 실행)에서 Windows PowerShell을 열고 고 hello 수정할 수 있는 명령 toonavigate toohello 다운로드 위치를 입력 하십시오.

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > hello 파일 이름은 hello 버전에 따라 변경 될 수 있습니다.
      >
      >
3. **다음**을 누릅니다.
4. Hello 수락 **계약 조건** 클릭 하 고 **다음**합니다.
5. **마침**을 클릭합니다.
6. StorSimple 저장소의 잘라낸 볼륨을 사용하여 파일 공유를 만듭니다. 자세한 내용은 참조 [hello StorSimple 관리자 서비스 toomanage 볼륨을 사용 하 여](storsimple-manage-volumes.md)합니다.

   1. 온-프레미스 Vm에 hello Windows 키 + Q 키를 누릅니다 하 고 검색할 **iSCSI**합니다.
   2. **iSCSI 초기자**를 선택합니다.
   3. 선택 hello **구성** 탭 및 복사 hello 초기자 이름입니다.
   4. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
   5. 선택 hello **StorSimple** 탭 한 다음 선택 hello hello 물리적 장치를 포함 하는 StorSimple Manager 서비스입니다.
   6. 볼륨 컨테이너를 만든 다음 볼륨을 만듭니다. (이러한 볼륨은 hello 파일 서버 Vm에 hello 파일 공유에 대 한)입니다. Hello 초기자 이름 복사한 hello 볼륨을 만들 때 액세스 제어 레코드 hello에 대 한 적절 한 이름을 제공 합니다.
   7. 선택 hello **구성** 탭 및 hello 장치의 hello IP 주소를 적어 둡니다.
   8. 온-프레미스 Vm에서 이동 toohello **iSCSI 초기자** 다시 hello 빠른 연결 섹션에에서 hello IP를 입력 합니다. 클릭 **빠른 연결** (hello 장치가 이제 연결).
   9. Azure 포털 열기 hello 및 선택 hello **볼륨 및 장치** 탭 합니다. **자동 구성**을 클릭합니다. 방금 만든 hello 볼륨 표시 되어야 합니다.
   10. Hello 포털에서 선택 hello **장치** 탭을 선택한 다음 **새 가상 장치 만들기.** 를 선택합니다. 새로운이 가상 장치가 오프 라인 상태로 tooavoid에 보관할 수 추가 비용입니다. tootake hello 가상 장치 오프 라인, 이동 toohello **가상 컴퓨터** hello 포털 섹션 및 절차에 따라 종료 합니다.
   11. Toohello 온-프레미스 Vm 돌아가서 디스크 관리를 엽니다 (hello Windows 키 + X를 눌러 **디스크 관리**).
   12. 몇 가지 추가 디스크 (수에 따라 hello 만든 볼륨)를 확인할 수 있습니다. 마우스 오른쪽 단추로 클릭 첫 번째 hello, 선택 **디스크 초기화**를 선택 하 고 **확인**합니다. 마우스 오른쪽 단추로 클릭 hello **할당 되지 않은** 섹션에서 **새 단순 볼륨**, 드라이브 문자를 할당 및 hello 마법사를 완료 합니다.
   13. 모든 hello 디스크 l 단계를 반복 합니다. 모든 hello 디스크에서 볼 수 있습니다 **이 PC** hello Windows 탐색기에서에서 합니다.
   14. 이 볼륨에 hello 파일 및 저장소 서비스 역할 toocreate 파일 공유를 사용 합니다.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate는 Azure Site Recovery 자격 증명 모음을 준비 하 고
Toohello 참조 [Azure Site Recovery 설명서](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget hello 파일 서버 VM을 보호 하기 전에 Azure 사이트 복구를 시작 합니다.

#### <a name="tooenable-protection"></a>tooenable 보호
1. Hello iSCSI 연결 끊기 hello에서 별로 온-프레미스 tooprotect Azure Site Recovery를 통해 원하는 Vm:

   1. Windows 키+Q를 누르고 **iSCSI**를 검색합니다.
   2. **iSCSI 초기자 설정**을 선택합니다.
   3. 이전에 연결 된 hello StorSimple 장치 연결을 끊습니다. 또는 끌 수 있습니다 hello 파일 서버를 몇 분간 보호를 사용 하도록 설정할 때.

   > [!NOTE]
   > 이렇게 하면 hello 파일 공유 toobe 일시적으로 사용할 수 없습니다.
   >
   >
2. [가상 컴퓨터 보호 사용](../site-recovery/site-recovery-hyper-v-site-to-azure.md) hello hello Azure Site Recovery 포털에서 파일 서버 VM의 합니다.
3. Hello 초기 동기화가 시작 되 면 hello 대상을 다시 다시 연결할 수 있습니다. ISCSI 초기자 toohello hello StorSimple 장치를 선택한 클릭 **연결**합니다.
4. Hello 동기화가 완료 되 고 면 hello VM의 hello 상태 **Protected**hello VM을 선택 hello **구성** 탭 하 고 hello VM의 hello 네트워크에 따라 업데이트 (이 hello 네트워크 장애 조치 VM(s) 해당 hello가 됩니다의 일부). Hello 네트워크 나타나지 hello 동기화 여전히 진행 되는 것입니다.

### <a name="enable-protection-of-storsimple-volumes"></a>StorSimple 볼륨의 보호 사용
Hello를 선택 하지 않은 경우 **이 볼륨에 대 한 기본 백업 사용** hello StorSimple 볼륨에 대 한 옵션을 너무 이동**백업 정책** hello StorSimple Manager 서비스와 적합 한 백업 만들기 모든 hello 볼륨에 대 한 정책입니다. 백업 toohello 복구 지점 목표 (RPO)이 싶다는 의사를 toosee hello 응용 프로그램에 대 한 hello 빈도 설정 하는 것이 좋습니다.

### <a name="configure-hello-network"></a>Hello 네트워크 구성
Hello 파일 서버 VM에 대 한는 hello VM 네트워크가 연결 된 toohello 올바른 DR 네트워크 장애 조치 후 Azure 사이트 복구에서 네트워크 설정을 구성 합니다.

Hello에 hello VM을 선택할 수 있습니다 **복제 항목** hello 다음 그림에에서 나와 있는 것 처럼 tooconfigure hello 네트워크 설정을 탭 합니다.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>복구 계획 만들기
ASR tooautomate hello 장애 조치 프로세스의 hello 파일 공유에서 복구 계획을 만들 수 있습니다. 통신이 중단 되는 경우 한 번의 클릭으로 몇 분 안에 hello 파일 공유 가져올 수 있습니다. tooenable이이 자동화는 Azure 자동화 계정이 필요 합니다.

#### <a name="toocreate-an-automation-account"></a>toocreate 자동화 계정
1. Azure 포털 toohello 이동 &gt; **자동화** 섹션.
2. **+ 추가** 단추를 클릭하면 아래에 블레이드가 열립니다.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * 이름 - 새 Automation 계정을 입력합니다.
   * 구독 - 구독을 선택합니다.
   * 리소스 그룹 - 새 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.
   * 위치-위치 선택, hello에 보관는 hello StorSimple 클라우드 어플라이언스 및 저장소 계정을 만든 동일한 지역/지역입니다.
   * Azure 실행 계정 만들기 - **예** 옵션을 선택합니다.

3. Toohello 자동화 계정 이동 **Runbook** &gt; **찾아보기 갤러리** hello 모든 tooimport hello 자동화 계정으로 runbook를 필요 합니다.
4. Runbook을 검색 하 여 다음 hello 추가 **재해 복구** hello 갤러리에는 태그:

   * TFO(테스트 장애 조치(failover)) 후 StorSimple 볼륨 정리
   * StorSimple 볼륨 컨테이너 장애 조치(failover)
   * 장애 조치(failover) 후 StorSimple 장치에서 볼륨 탑재
   * Azure VM에서 사용자 지정 스크립트 확장 제거
   * StorSimple 가상 어플라이언스 시작

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Hello 자동화 계정에서 hello runbook을 선택 하 여 모든 hello 스크립트를 게시 하 고 클릭 **편집** &gt; **게시** 차례로 **예** toohello 확인 메시지. 이 단계를 hello **Runbook** 탭이 다음과 같이 표시 됩니다.

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Hello 자동화 계정에서 선택 hello **자산** 탭 &gt; 클릭 **변수** &gt; **변수 추가** hello 다음 변수를 추가 합니다. 이러한 자산 tooencrypt를 선택할 수 있습니다. 이러한 변수는 복구 계획과 관련됩니다. 복구 계획 (있음 hello 다음 단계에서 만들) 이름은 TestPlan, 다음 TestPlan StorSimRegKey, TestPlan-AzureSubscriptionName 등에 프로그램 변수 여야 합니다.

   * *RecoveryPlanName***-StorSimRegKey**: hello StorSimple Manager 서비스에 대 한 hello 등록 키입니다.
   * *RecoveryPlanName***-AzureSubscriptionName**: hello 이름 hello Azure 구독입니다.
   * *RecoveryPlanName***-ResourceName**: hello 이름 hello hello StorSimple 장치에 있는 StorSimple 리소스입니다.
   * *RecoveryPlanName***-DeviceName**: hello 장치 toobe 장애 조치를 합니다.
   * *RecoveryPlanName***-VolumeContainers**: volcon1, volcon2, volcon3 toobe, 예를 들어 실패 해야 하는 hello 장치에 볼륨 컨테이너의 쉼표로 구분 된 문자열을 제공 합니다.
   * *RecoveryPlanName***-TargetDeviceName**: hello StorSimple 클라우드 어플라이언스에 있는 hello에 컨테이너는 toobe 장애 조치 합니다.
   * *RecoveryPlanName***-TargetDeviceDnsName**: hello 대상 장치의 hello 서비스 이름 (이 hello에서 찾을 수 있습니다 **가상 컴퓨터** 섹션: hello 서비스 이름이 동일 hello로 hello은 DNS 이름)입니다.
   * *RecoveryPlanName***-StorageAccountName**: hello script에서 hello 저장소 계정 이름 (있는 toorun hello에 장애 조치를 취한 VM) 저장 됩니다. 이 인해 약간의 공간 toostore hello 스크립트를 일시적으로 포함 된 저장소 계정 수 있습니다.
   * *RecoveryPlanName***-StorageAccountKey**: 저장소 계정 위에 hello에 대 한 hello 선택 키입니다.
   * *RecoveryPlanName***-ScriptContainer**: hello 컨테이너에서 어떤 hello 스크립트를 저장할 hello 클라우드에서 hello 이름입니다. Hello 컨테이너가 존재 하지 않는 경우 생성 됩니다.
   * *RecoveryPlanName***-VMGUIDS**: VM을 보호 하는 경우, 시 Azure Site Recovery 할당 모든 VM의 장애 조치 VM hello hello 세부 정보를 제공 하는 고유 ID입니다. tooobtain hello VMGUID, 선택 hello **복구 서비스** 탭을 클릭 **보호 항목** &gt; **보호 그룹** &gt; **컴퓨터** &gt; **속성**합니다. 여러 Vm이 있는 경우 쉼표로 구분 된 문자열로 hello Guid를 추가 합니다.
   * *RecoveryPlanName***-AutomationAccountName** – hello를 추가한 hello runbook과 자산 hello hello 자동화 계정의 이름입니다.

  예를 들어 hello hello 복구 계획의 이름인 fileServerpredayRP, 않다면 **자격 증명** & **변수** 탭 hello 자산을 모두 추가한 후 다음과 같이 표시 됩니다.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Toohello 이동 **복구 서비스** 섹션 및 이전에 만든 선택 hello Azure Site Recovery 자격 증명 모음입니다.
8. 선택 hello **복구 계획 (사이트 복구)** 옵션에서 **관리** 그룹화 하 고 다음과 같이 복구 계획을 새로 만듭니다.

   a.  **+ 복구 계획** 단추를 클릭하여 아래의 블레이드를 엽니다.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  복구 계획 이름을 입력하고 원본, 대상 및 배포 모델 값을 선택합니다.

   c.  Hello 복구 계획에서 tooinclude 되도록 hello 보호 그룹에서 선택한 hello Vm **확인** 단추입니다.

   d.  앞에서 만든 복구 계획 선택를 클릭 **사용자 지정** tooopen hello 복구 계획 사용자 지정 보기 단추입니다.

   e.  마우스 오른쪽 단추로 **모든 그룹 종료**를 클릭하고 **사전 작업 추가**를 클릭합니다.

   f.  엽니다 동작 블레이드를 삽입, 이름을 입력 하 고, 선택 **기본 측** toorun 옵션을 (를 추가한 hello runbook) 자동화 계정 선택 하 고 다음 hello를 선택 하는 위치에서 옵션  **StorSimple 볼륨 컨테이너가 장애 조치** runbook입니다.

   g.  마우스 오른쪽 단추로 클릭 **그룹 1: 시작** 클릭 **보호 된 항목 추가** 옵션 다음 hello Vm을 toobe hello 복구 계획에서 보호를 선택 **확인** 단추입니다. 이미 선택된 VM인 경우 선택 사항입니다.

   h.  마우스 오른쪽 단추로 클릭 **그룹 1: 시작** 클릭 **후 작업** 옵션 후 다음 스크립트 hello 모든 추가:

   * Start-StorSimple-Virtual-Appliance Runbook
   * Fail over-StorSimple-volume-containers Runbook
   * Mount-volumes-after-failover Runbook
   * Uninstall-custom-script-extension Runbook

   i.  동일한 hello에서 위의 4 hello 스크립트 후 수동 작업을 추가할 **그룹 1: 사후 단계** 섹션. 이 동작은을 확인할 수 있습니다 모든 기능이 올바르게 작동 하는 hello 지점에 설명 합니다. 이 작업이 필요 toobe 테스트 장애 조치의 일부로 추가 (만 선택 hello **테스트 장애 조치** 확인란).

   j.  Hello 수동 작업 후 추가 hello **정리** 스크립트를 사용 하 여 hello에 사용한 동일한 절차 hello 다른 runbook입니다. **저장** hello 복구 계획 합니다.

    > [!NOTE]
    > 테스트 장애 조치를 실행할 때는 hello 대상 장치에 복제 된 했습니다 hello StorSimple 볼륨 hello 수동 작업이 완료 된 후 hello 정리의 일부로 삭제 되므로 hello 수동 작업 단계에서 모든 항목 확인 해야 합니다.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>테스트 장애 조치(failover) 수행
Toohello 참조 [Active Directory DR 솔루션](../site-recovery/site-recovery-active-directory.md) 고려 사항 특정 tooActive 디렉터리 hello 테스트 장애 조치 중에 대 한 부록 가이드입니다. hello 온-프레미스 설정도 hello 테스트 장애 조치 발생 시 전혀 추가 되지 됩니다. 연결 된 StorSimple 볼륨 hello toohello 온-프레미스 VM 복제 toohello Azure에서 클라우드 어플라이언스에 StorSimple 됩니다. Azure에서 테스트 목적 VM 상태가 및 hello 복제 된 볼륨이 연결된 toohello VM 합니다.

#### <a name="tooperform-hello-test-failover"></a>tooperform hello에 대 한 테스트 장애 조치
1. Hello Azure 포털에서에서 사이트 복구 자격 증명 모음을 선택 합니다.
2. Hello 파일 서버 VM에 대해 만든 hello 복구 계획을 클릭 합니다.
3. **테스트 장애 조치(failover)**를 클릭합니다.
4. Hello Azure 가상 네트워크 toowhich 장애 조치가 발생 한 후 연결 될 Azure Vm을 선택 합니다.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. 클릭 **확인** toobegin hello 장애 조치 합니다. Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치 작업** 자격 증명 모음 이름에 &gt; **작업** &gt; **사이트복구작업**.
6. Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 &gt; **가상 컴퓨터**합니다. 유효성 검사를 수행할 수 있습니다.
7. Hello 유효성 검사가 완료 된 후 클릭 **유효성 검사 완료**합니다. 가 정리 hello StorSimple 볼륨 및 종료 hello StorSimple 클라우드 어플라이언스에이 있습니다.
8. 완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. 테스트 장애 조치 메모 레코드에서 및 hello와 관련 된 모든 관찰 저장 합니다. 테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.

## <a name="perform-a-planned-failover"></a>계획된 장애 조치(failover) 수행
   계획된 된 장애 조치 하는 동안 hello 온-프레미스 파일 서버 VM을 정상적으로 종료 및 hello 볼륨 StorSimple 장치에 대 한 백업 스냅숏을 생성 하는 클라우드입니다. hello StorSimple 볼륨은 toohello 가상 장치를 Azure에서 VM 상태가 복제본 조치할 및 hello 볼륨이 연결된 toohello VM 합니다.

#### <a name="tooperform-a-planned-failover"></a>계획된 된 장애 조치 tooperform
1. Hello Azure 포털에서에서 선택 **복구 서비스** 자격 증명 모음 &gt; **복구 계획 (사이트 복구)** &gt; **recoveryplan_name** 에 대해 생성 hello 파일 서버 VM입니다.
2. Hello 복구 계획 블레이드에서 클릭 **자세한** &gt; **계획 된 장애 조치**합니다.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Hello에 **확인 계획 된 장애 조치** 블레이드에서 hello 소스 및 대상 위치 선택 대상 네트워크를 선택 하 고 hello 검사 아이콘 ✓ toostart hello 장애 조치 프로세스를 클릭 합니다.
4. 복제본 가상 컴퓨터가 만들어진 후에는 커밋 대기중 상태입니다. 클릭 **커밋** toocommit hello 장애 조치 합니다.
5. 복제가 완료 된 후 hello 보조 위치에서 hello 가상 컴퓨터 시작 합니다.

## <a name="perform-a-failover"></a>장애 조치 수행
계획 되지 않은 경우 장애 조치 하는 동안 hello StorSimple 볼륨은 toohello 가상 장치를 Azure에서 VM을 주어 복제본 조치할 및 hello 볼륨이 연결된 toohello VM 합니다.

#### <a name="tooperform-a-failover"></a>tooperform 장애 조치
1. Hello Azure 포털에서에서 선택 **복구 서비스** 자격 증명 모음 &gt; **복구 계획 (사이트 복구)** &gt; **recoveryplan_name** 에 대해 생성 hello 파일 서버 VM입니다.
2. Hello 복구 계획 블레이드에서 클릭 **자세한** &gt; **장애 조치**합니다.  
3. Hello에 **확인 장애 조치** 블레이드에서 hello 원본을 선택 하 고 대상 위치입니다.
4. 선택 **가상 컴퓨터를 종료 하 고 hello 최신 데이터를 동기화** toospecify Site Recovery를 통해 가상 컴퓨터를 보호 하는 hello tooshut를 시도 하 고 hello hello 데이터의 최신 버전이 될 수 있도록 hello 데이터를 동기화 해야 장애 조치 합니다.
5. Hello 장애 조치 후 hello 가상 컴퓨터가 커밋 대기 중 상태인에에서 있습니다. 클릭 **커밋** toocommit hello 장애 조치 합니다.


## <a name="perform-a-failback"></a>장애 복구(failback) 수행
장애 복구 하는 동안 StorSimple 볼륨 컨테이너가 장애 조치 됩니다 백 toohello 물리적 장치 백업을 수행한 후.

#### <a name="tooperform-a-failback"></a>tooperform는 장애 복구
1. Hello Azure 포털에서에서 선택 **복구 서비스** 자격 증명 모음 &gt; **복구 계획 (사이트 복구)** &gt; **recoveryplan_name** 에 대해 생성 hello 파일 서버 VM입니다.
2. Hello 복구 계획 블레이드에서 클릭 **자세한** &gt; **계획 된 장애 조치**합니다.  
3. Hello 원본 및 대상 위치, 적절 한 데이터 동기화 선택 hello 및 VM 만들기 옵션을 선택 합니다.
4. 클릭 **확인** toostart hello 장애 복구 프로세스 단추입니다.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>모범 사례
### <a name="capacity-planning-and-readiness-assessment"></a>용량 계획 및 준비 평가
#### <a name="hyper-v-site"></a>Hyper-V 사이트
사용 하 여 hello [사용자 용량 계획 도구](http://www.microsoft.com/download/details.aspx?id=39057) toodesign hello 서버, 저장소 및 Hyper-v 복제 환경에 대 한 네트워크 인프라입니다.

#### <a name="azure"></a>Azure
Hello를 실행할 수 있습니다 [Azure 가상 컴퓨터 준비 평가 도구](http://azure.microsoft.com/downloads/vm-readiness-assessment/) Azure Vm 및 Azure 사이트 복구 서비스와 호환 되는지 Vm tooensure에 있습니다. VM 구성을 확인 하 고 구성을 Azure와 호환 되지 않는 경우 경고를 표시 하는 hello 준비 평가 도구입니다. 예를 들어 C: 드라이브가 127GB 보다 큰 경우 경고가 발생합니다.

용량 계획은 다음과 같은 두 개 이상의 중요 프로세스로 구성됩니다.

* 매핑 온-프레미스 Hyper-v Vm tooAzure VM 크기 (예: A6, A7, A8 및 A9).
* 인터넷 대역폭이 필요 hello를 결정 합니다.

## <a name="limitations"></a>제한 사항
* 현재 StorSimple 장치 1만 장애 조치 될 수 (tooa StorSimple 클라우드 장비를 단일). 여러 개의 StorSimple 장치에 걸쳐 있는 파일 서버의 hello 시나리오 아직 지원 되지 않습니다.
* VM에 대 한 보호를 활성화 하는 동안 오류가 발생 하면 hello iSCSI 대상을 분리 했습니다 있는지 확인 합니다.
* 볼륨 컨테이너를 포괄 하는 백업 정책 때문에 함께 그룹화 된 모든 hello 볼륨 컨테이너는 장애 조치 될 함께 합니다.
* 선택한 hello 볼륨 컨테이너에 모든 hello 볼륨을 장애 조치 됩니다.
* 64TB 없습니다 장애 조치 단일 StorSimple 클라우드 어플라이언스에 hello 최대 용량은 64TB 이므로 보다 toomore 구성 하는 볼륨을 선택 합니다.
* Hello 계획/계획 되지 않은 장애 조치가 실패할 경우 hello Vm은 Azure에서 만든 다음 작업을 정리 하지 hello Vm입니다. 대신 장애 복구(failback)를 수행하세요. Hello Vm을 삭제 하는 경우 다음 hello 온-프레미스 Vm 다시 설정할 수 없습니다.
* 장애 조치 후 수 없는 경우 toosee hello 볼륨 toohello Vm 이동 디스크 관리, hello 디스크 다시 검사를 열고 온라인 상태로 전환할 합니다.
* 경우에 따라 hello DR 사이트에서 드라이브 문자 hello hello 문자 온-프레미스 보다 달라질 수 있습니다. 이 경우 hello 장애 조치가 완료 된 후 toomanually 올바른 hello 문제를 해야 합니다.
* Azure 자격 증명 자산으로 hello 자동화 계정에 입력 된 hello에 대 한 다단계 인증을 해제 되어야 합니다. 이 인증 되지 않으면 스크립트 허용 되지 않습니다 toorun 자동으로 한 hello 복구 계획이 실패 합니다.
* 장애 조치 작업 시간 초과: hello StorSimple 스크립트 hello 볼륨 컨테이너를 장애 조치 (현재 120 분) 스크립트 당 hello Azure Site Recovery 제한 보다 더 많은 시간이 걸리는 경우 시간 초과 됩니다.
* 백업 작업 시간 제한: 볼륨의 백업을 hello 스크립트 (현재 120 분) 마다 hello Azure Site Recovery 제한 보다 더 많은 시간이 걸리는 경우 hello StorSimple 스크립트 시간이 초과 합니다.

  > [!IMPORTANT]
  > Hello Azure 포털에서에서 수동으로 hello 백업을 실행 하 고 hello 복구 계획을 다시 실행 하십시오.

* 복제 작업 시간 초과: 스크립트 (현재 120 분) 마다 hello Azure Site Recovery 제한 보다 더 많은 시간이 걸리는 hello 복제 볼륨의 경우 hello StorSimple 스크립트 시간이 초과 합니다.
* 시간 동기화 오류: hello StorSimple 스크립트 hello 백업 되지에 성공 했음을 hello 백업 hello 포털에서 성공 하더라도 말하는 오류가 발생 합니다. 해당 hello StorSimple 어플라이언스 시간이 수도 hello와 동기화 hello 표준 시간대의 현재 시간이 원인일 수 있습니다.

  > [!IMPORTANT]
  > 동기화 hello 어플라이언스 시간 hello로 hello 표준 시간대의 현재 시간입니다.

* 어플라이언스 장애 조치 오류: hello StorSimple 스크립트 때 hello 복구 계획 실행 중인 경우 어플라이언스 장애 조치 하는 경우 실패할 수 있습니다.

  > [!IMPORTANT]
  > Hello 기기 장애 조치를 완료 한 후 hello 복구 계획을 다시 실행 합니다.


## <a name="summary"></a>요약
Azure Site Recovery를 사용하여 StorSimple 저장소에 호스트된 파일 공유가 있는 파일 서버 VM에 대한 전체 자동화된 재해 복구 계획을 만들 수 있습니다. 어디에서 나 몇 초 이내 hello 장애 조치를 시작할 수 있습니다에 이벤트를 더 이상의 hello 및 hello 응용 프로그램 실행를 가져오고 잠시 후에 있습니다.
