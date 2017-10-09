---
title: "Azure Site Recovery를 사용 하 여 SAN 사용 하 여 VMM의 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooreplicate Hyper-v 가상 컴퓨터 SAN 복제를 사용 하 여 Azure Site Recovery와 두 사이트 사이입니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>SAN을 사용 하 여 Azure Site Recovery와 VMM 클라우드에 tooa 보조 사이트의 Hyper-v Vm 복제


Toodeploy 하려는 경우에이 문서를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) (System Center Virtual Machine Manager 클라우드에 관리 됨) Hyper-v Vm tooa 보조 VMM 사이트의 hello 클래식 포털에서 Azure Site Recovery를 사용 하 여 toomanage 복제 합니다. 이 시나리오는 hello 새 Azure 포털에서 사용할 수 없습니다.



이 문서의 끝 hello에 대 한 설명을 게시 합니다. Hello에 tootechnical 질문 답변을 얻을 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="why-replicate-with-san-and-site-recovery"></a>SAN 및 Site Recovery를 사용하여 복제하는 이유는 무엇입니까?

* SAN은 SAN 통해 Hyper-v를 포함 하는 주 사이트 san Lun tooa 보조 사이트를 복제할 수 있도록 엔터프라이즈 수준의 확장 가능한 복제 솔루션을 제공 합니다. 저장소는 VMM에서 관리되며 복제 및 장애 조치(Failover)는 Site Recovery를 통해 오케스트레이션됩니다.
* 사이트 복구는 몇 가지와 협력 하 [SAN 저장소 파트너](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) 파이버 채널과 iSCSI 저장소를 통한 tooprovide 복제 합니다.  
* 기존 SAN 인프라 tooprotect 업무용 앱 사용 Hyper-v 클러스터에 배포 합니다. N계층 앱이 지속적으로 장애 조치(Failover)되도록 VM을 그룹으로 복제할 수 있습니다.
* SAN 복제는 저장소 배열 기능에 따라 낮은 RTO 및 RPO에 대해 동기화된 복제와 뛰어난 유연성을 위해 비동기화된 복제를 사용하여 다양한 응용 프로그램 계층 간의 복제 일관성을 보장합니다.  
* Hello VMM 패브릭에서에서 SAN 저장소를 관리할 수 있고-> Smi-s를 사용 하 여 VMM toodiscover 기존 저장소에 있습니다.  

다음 사항에 유의하세요.
- SAN 통해 사이트 간 복제 hello Azure 포털에서에서 사용할 수 없습니다. Hello 클래식 포털에서 제공 됩니다. Hello 클래식 포털에서 새 자격 증명 모음을 만들 수 없습니다. 기존 자격 증명 모음은 유지 관리될 수 있습니다.
- SAN tooAzure에서 복제가 지원 되지 않습니다.
- 공유 Vhdx를 복제할 수 없습니다 또는 논리 단위 (Lun)에 직접 tooVMs iSCSI 또는 파이버 채널을 통해 연결 합니다. 게스트 클러스터는 복제될 수 있습니다.


## <a name="architecture"></a>아키텍처

![SAN 아키텍처](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: hello Azure 포털에서에서 사이트 복구 자격 증명 모음을 설정 합니다.
- **SAN 저장소**: SAN 저장소 hello VMM 패브릭에서에서 관리 됩니다. Hello 저장소 공급자를 추가, 저장소 분류를 만들고 저장소 풀을 설정 합니다.
- **VMM 및 Hyper-V**: 각 사이트에 VMM 서버를 사용하는 것이 좋습니다. VMM 사설 클라우드를 설정하고 클라우드에 Hyper-V 클러스터를 배치합니다. 배포 하는 동안 hello Azure 사이트 복구 공급자가 각 VMM 서버에 설치 및 hello 서버 hello 자격 증명 모음에 등록 됩니다. hello 공급자 hello Site Recovery 서비스 toomanage 복제, 장애 조치 및 장애 복구와 통신합니다.
- **복제**: hello 기본 및 보조 SAN 저장소 간에 복제가 발생 한 후 VMM에서 저장소를 설정 하 고 사이트 복구에서 복제를 구성 합니다. 복제 데이터를 보내지 않은 tooSite 복구 합니다.
- **장애 조치**: hello Site Recovery 포털에서 장애 조치할 수 있도록 합니다. 복제가 동기 상태이기 때문에 장애 조치(failover) 중에 데이터가 손실되지 않습니다.
- **장애 복구**: toofail 다시 역방향 복제 tootransfer 델타 변경 내용을 hello 보조 사이트 toohello 기본 사이트에서 사용 하도록 설정 합니다. 역방향 복제가 완료 된 후에 보조 tooprimary에서 계획된 된 장애 조치를 실행 합니다. 이 계획 된 장애 조치 hello 보조 사이트에서 hello 복제본 Vm을 중지 하 고 hello 기본 사이트에서 시작 합니다.


## <a name="before-you-start"></a>시작하기 전에


**필수 구성 요소** | **세부 정보**
--- | ---
**Azure** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. Site Recovery 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/). Azure Site Recovery 자격 증명 모음 tooconfigure 만들고 복제 및 장애 조치를 관리 합니다.
**VMM** | 단일 VMM 서버를 사용 하 고 서로 다른 클라우드 간에 복제할 수 있지만 hello 기본 사이트에 하나의 VMM과 hello 보조 사이트에 하나는 것이 좋습니다. VMM을 물리적 또는 가상 독립 실행형 서버나 클러스터로 배포할 수 있습니다. <br/><br/>VMM 서버 hello System Center 2012 r 2를 실행 해야 hello 최신 누적 업데이트가 설치 된 이상.<br/><br/> 구성 된 클라우드가 하나 이상 필요 hello tooprotect 원하는 hello 보조 VMM 서버에 구성 된 클라우드가 하나는 기본 VMM 서버에 장애 조치에 대 한 toouse 원하는 합니다.<br/><br/> hello 원본 클라우드는 하나 이상의 VMM 호스트 그룹을 포함 해야 합니다.<br/><br/> 모든 VMM 클라우드의 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다.<br/><br/> VMM 클라우드 설정에 대한 자세한 내용은 [개인 VM 클라우드 배포](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview)를 참조하세요.
**Hyper-V** | 기본 및 보조 VMM 클라우드에 있는 하나 이상의 Hyper-V 클러스터가 있어야 합니다.<br/><br/> hello 원본 Hyper-v 클러스터는 하나 이상의 가상 컴퓨터를 포함 해야 합니다.<br/><br/> VMM 호스트 그룹 hello 기본 및 보조 사이트에서 hello hello Hyper-v 클러스터가 하나 이상 포함 해야 합니다.<br/><br/>hello 호스트 및 대상 Hyper-v 서버에 Windows Server 2012를 실행 해야 하거나 hello Hyper-v 역할 및 hello 최신 업데이트로 이상 설치 합니다.<br/><br/> 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 broker가 자동으로 만들어지지 않습니다. 수동으로 구성해야 합니다. 자세한 내용은 [Hyper-V 복제본에 사용할 호스트 클러스터 준비](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters)를 참조하세요.
**SAN 저장소** | iSCSI 또는 채널 저장소나 공유 가상 하드 디스크(vhdx)를 사용하여 게스트 클러스터형 가상 컴퓨터를 복제할 수 있습니다.<br/><br/> 두 개의 SAN 배열이 필요: hello 기본 사이트 및 보조 사이트 하나에 hello에 각각 하나씩 있습니다.<br/><br/> Hello 배열 간에 네트워크 인프라를 설정 해야 합니다. 피어링 및 복제를 구성해야 합니다. 복제 라이선스 hello 저장소 배열 요구 사항에 따라 설정 해야 합니다.<br/><br/>호스트가 iSCSI 또는 파이버 채널을 사용 하 여 저장소 Lun와 통신할 수 있도록 hello Hyper-v 호스트 서버와 hello 저장소 배열 간에 네트워킹을 설정 합니다.<br/><br/> [지원되는 저장소 배열](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx)을 확인합니다.<br/><br/> 저장소 배열 제조업체에서 SMI-S 공급자를 설치 해야 하 고 hello 공급자가 관리 해야 하는 hello SAN 배열입니다. Toomanufacturer 지침에 따라 hello 공급자를 설정 합니다.<br/><br/>해당 hello 배열-> Smi-s 공급자가 서버에 해당 hello VMM 해야 서버에서 IP 주소 또는 FQDN을 사용 하 여 hello 네트워크를 통해 액세스할 수 있습니다.<br/><br/> 각 SAN 배열에 사용할 수 있는 저장소 풀이 하나 이상 있어야 합니다.<br/><br/> 기본 VMM 서버 hello hello 기본 배열을 관리 해야 하 고 보조 VMM 서버 hello hello 보조 배열을 관리 해야 합니다.
**네트워크 매핑** | 장애 조치 후 보조 Hyper-v 호스트 서버에 복제 된 가상 컴퓨터가 최적으로 배치 되도록 하 고 연결 된 tooappropriate VM 네트워크는 네트워크 매핑을 설정 합니다. 네트워크 매핑을 구성 하지 않으면, 복제본 Vm 장애 조치 후 연결 된 tooany 네트워크 수 없습니다.<br/><br/> Site Recovery 배포 중에 네트워크 매핑을 설정할 수 있도록 VMM 네트워크가 제대로 구성되었는지 확인합니다. VMM에서 Vm hello hello 원본 Hyper-v 호스트에 연결 된 tooa VMM VM 네트워크 여야 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.<br/><br/> hello 대상 클라우드는 해당 VM 네트워크가 있어야 하며 차례로 연결 된 tooa 해당 논리 네트워크를 hello 대상 클라우드와 연결 된 해야 합니다.<br/><br/>에서도 확인할 수 있습니다.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>1 단계: hello VMM 인프라 준비
tooprepare VMM 인프라를 해야 합니다.

1. VMM 클라우드를 확인합니다.
2. VMM에 SAN 저장소를 통합하고 분류합니다.
3. LUN을 만들고 저장소를 할당합니다.
4. 복제 그룹을 만듭니다.
5. VM 네트워크를 설정합니다.

### <a name="verify-vmm-clouds"></a>VMM 클라우드 확인

Site Recovery 배포를 시작하기 전에 VMM 클라우드가 올바르게 설정되었는지 확인합니다.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>통합 및 hello VMM 패브릭에서에서 SAN 저장소를 분류 합니다.

1. Hello VMM 콘솔에서 이동 너무**패브릭** > **저장소** > **리소스 추가** > **저장장치**.
2. Hello에 **저장 장치 추가** 선택 마법사 **저장소 공급자 유형 선택** 선택 **검색 하 고 Smi-s 공급자가 관리 하는 SAN 및 NAS 장치**합니다.

    ![공급자 유형](./media/site-recovery-vmm-san/provider-type.png)

3. Hello에 **프로토콜 및 hello 저장소 Smi-s 공급자의 주소 지정** 페이지에서 **Smi-s CIMXML** toohello 공급자 연결에 대 한 hello 설정을 지정 합니다.
4. **공급자 IP 주소 또는 FQDN** 및 **TCP/IP 포트**, toohello 공급자 연결에 대 한 hello 설정을 지정 합니다. SMI-S CIMXML에 대해서만 SSL 연결을 사용할 수 있습니다.

    ![공급자 연결](./media/site-recovery-vmm-san/connect-settings.png)
5. **계정으로 실행**, hello 공급자에 액세스 하거나 계정을 만들 수 있는 VMM 계정으로 실행 계정을 지정 합니다.
6. Hello에 **정보 수집** 페이지에서 VMM toodiscover 및 가져오기 hello 저장소 장치 정보를 자동으로 시도 합니다. tooretry 검색 클릭 **스캔 공급자**합니다. Hello 검색 프로세스가 성공 하면 경우에 hello 검색 저장소 배열, 저장소 풀, 제조업체, 모델 및 용량 hello 페이지에 표시 됩니다.

    ![저장소 검색](./media/site-recovery-vmm-san/discover.png)
7. **관리 저장소 풀 tooplace를 선택 하 고 분류 할당**, hello 저장소 풀이 VMM 관리 되며 할당 한 분류를 선택 합니다. Hello 저장소 풀에서 LUN 정보를 가져올 수 있습니다. Lun 기반 만들기 hello 응용 프로그램에 필요한 tooprotect, 용량 요구 사항 및 요구 사항을 함께 tooreplicate는 사항에 대 한 합니다.

    ![저장소 분류](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>LUN을 만들고 저장소 할당

Lun 기반 만들기 hello 응용 프로그램에 필요한 tooprotect, 용량 요구 사항 및 요구 사항을 함께 tooreplicate는 사항에 대 한 합니다.

1. Hello 저장소 VMM 패브릭 hello에 나타나면 다음을 할 수 있습니다 [Lun을 프로 비전](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm)합니다.

     > [!NOTE]
     > VM 지 원하는 복제 tooLUNs hello에 대 한 Vhd를 추가 하지 마십시오. LUN이 Site Recovery 복제 그룹에 없으면 Site Recovery에서 찾을 수 없습니다.
     >

2. VMM에서 가상 컴퓨터 데이터를 프로 비전 toohello 저장소를 배포할 수 있도록 저장소 용량 toohello Hyper-v 호스트 클러스터를 할당 합니다.

   * Tooallocate toohello 클러스터 저장소를 할당 하기 전에 해야 것 toohello VMM 호스트 그룹을 클러스터는 hello에 상주 합니다. 자세한 내용은 참조 [tooallocate 저장소 논리 단위 tooa VMM에서 그룹을 호스트 하는 방법을](https://technet.microsoft.com/library/gg610686.aspx) 및 [tooallocate 저장소 풀을 VMM의 호스트 그룹 tooa 어떻게](https://technet.microsoft.com/library/gg610635.aspx)합니다.
   * 에 설명 된 대로 저장소 용량 toohello 클러스터 할당 [tooconfigure 저장소 Hyper-v 호스트를 VMM에서 클러스터를 어떻게](https://technet.microsoft.com/library/gg610692.aspx)합니다.

    ![공급자 유형](./media/site-recovery-vmm-san/provider-type.png)
3. **프로토콜 및 hello 저장소 Smi-s 공급자의 주소 지정**선택, **Smi-s CIMXML**합니다. Toohello 공급자를 연결 하기 위한 hello 설정을 지정 합니다. SSL 연결은 SMI-S CIMXML에만 사용할 수 있습니다.

    ![공급자 연결](./media/site-recovery-vmm-san/connect-settings.png)
4. **계정으로 실행**, hello 공급자에 액세스 하거나 계정을 만들 수 있는 VMM 계정으로 실행 계정을 지정 합니다.
5. **정보 수집**, VMM toodiscover 및 가져오기 hello 저장소 장치 정보를 자동으로 시도 합니다. Tooretry 필요 하면 클릭 **스캔 공급자**합니다. Hello 검색 프로세스에 성공 하면 hello 저장소 배열, 저장소 풀, 제조업체, 모델 및 용량 hello 페이지에 표시 됩니다.

    ![저장소 검색](./media/site-recovery-vmm-san/discover.png)
7. **관리 저장소 풀 tooplace를 선택 하 고 분류 할당**, 선택 hello 저장소 풀이 VMM 관리 하 고 분류를 할당 합니다. Hello 저장소 풀에서 LUN 정보를 가져올 수 있습니다.

    ![저장소 분류](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>복제 그룹 만들기

가 함께 tooreplicate 필요로 하는 모든 hello Lun을 포함 하는 복제 그룹을 만듭니다.

1. Hello VMM 콘솔을 열고 hello **복제 그룹** hello 저장소 배열 속성을 한 후 탭 **새로**합니다.
2. Hello 복제 그룹을 만듭니다.

    ![SAN 복제 그룹](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>네트워크 설정

네트워크 매핑을 tooconfigure 하려는 경우 다음 hello지 않습니다.

1. Site Recovery 네트워크 매핑을 살펴봅니다.
2. VMM에서 VM 네트워크를 준비합니다.

   * [논리 네트워크를 설정합니다](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [VM 네트워크를 설정합니다](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>2단계: 자격 증명 모음 만들기

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) tooregister hello 자격 증명 모음에 VMM 서버 hello에서에서 원하는 합니다.
2. **Data Services** > **Recovery Services**를 확장하고 **Site Recovery 자격 증명 모음**을 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.
5. **지역**, 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 되는 toocheck 지역 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
6. **자격 증명 모음 만들기**를 클릭합니다.

    ![새 자격 증명 모음](./media/site-recovery-vmm-san/create-vault.png)

자격 증명 모음 hello hello 상태 표시줄 tooconfirm 올바르게 만들어졌는지 확인 합니다. hello 자격 증명 모음으로 나열 됩니다 **활성** 주 hello에 **복구 서비스** 페이지.

### <a name="register-hello-vmm-servers"></a>Hello VMM 서버 등록

1. 열기 hello **빠른 시작** hello에서 페이지 **복구 서비스** 페이지. 빠른 시작 언제 든 지 hello 아이콘을 선택 하 여 열 수도 있습니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Hello 드롭다운 목록 상자에서 선택 **하이퍼-V 사이의 온-프레미스 배열 복제를 사용 하 여 사이트**합니다.

    ![등록 키](./media/site-recovery-vmm-san/select-san.png)
3. **준비 VMM 서버**, hello hello Azure Site Recovery Provider 설치 파일의 최신 버전을 다운로드 합니다.
4. Hello 원본 VMM 서버에서이 파일을 실행 합니다. VMM이 클러스터에 배포 된 hello에 대 한 공급자 hello 처음으로 설치 하는 경우 액티브 노드에서 hello 공급자를 설치 하 고 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다. 그런 다음 hello 공급자에 설치 hello 다른 노드가 있습니다. Hello 공급자를 업그레이드 하는 경우에 동일한 공급자 버전이 hello가 모든 노드에서 tooupgrade 필요.
5. hello 설치 관리자는 요구 사항 및 요청 권한 toostop hello VMM 서비스 toobegin Provider 설치를 확인 합니다. 자동으로 설치가 완료 되 면 hello 서비스를 다시 시작 됩니다. VMM 클러스터에서 증명된 toostop hello 클러스터 역할 수 있습니다.
6. **Microsoft Update**, 업데이트,에 선택할 수 있습니다 및 tooyour Microsoft Update 정책에 따라 공급자 업데이트가 설치 됩니다.

    ![Microsoft 업데이트](./media/site-recovery-vmm-san/ms-update.png)

7. 기본적으로 공급자 hello에 대 한 hello 설치 위치는 <SystemDrive>files\microsoft System Center 2012 R2\Virtual Machine Manager\bin 합니다. 클릭 **설치** toobegin 합니다.

    ![설치 위치](./media/site-recovery-vmm-san/install-location.png)

8. Hello 공급자를 설치한 후 클릭 **등록** hello 자격 증명 모음에 tooregister hello VMM 서버입니다.

    ![설치 완료](./media/site-recovery-vmm-san/install-complete.png)

9. **인터넷 연결**, hello 공급자 toohello 인터넷 연결 하는 방법을 지정 합니다. 선택 **기본 시스템 프록시 설정 사용** hello 서버의 toouse hello 기본 인터넷 연결 설정을 선택 합니다.

    ![인터넷 설정](./media/site-recovery-vmm-san/proxy-details.png)

   * 사용자 지정 프록시 toouse 하려는 경우 설정 hello 공급자를 설치 하기 전에. 사용자 지정 프록시 설정을 구성할 때 테스트 toocheck hello 프록시 연결을 실행 합니다.
   * 사용자 지정 프록시를 사용 하 여 수행 하거나 기본 프록시에 인증이 필요한 경우 hello 주소와 포트를 포함 하 여 hello 프록시 세부 정보를 입력 해야 합니다.
   * hello 필요 Url hello VMM 서버에서 액세스할 수 있어야 합니다.
   * 지정 된 hello를 사용 하 여 VMM 실행 계정 (DRAProxyAccount) 자동으로 생성 사용자 지정 프록시를 사용 하는 경우 프록시 자격 증명입니다. 이 계정을 인증할 수 있도록 hello 프록시 서버를 구성 합니다. Hello VMM 콘솔에서 hello 계정으로 실행 계정 설정을 수정할 수 있습니다 (**설정** > **보안** > **실행 계정**  >  **DRAProxyAccount**). Tootake 효과 변경 하는 hello에 대 한 hello VMM 서비스를 다시 시작 해야 합니다.
10. **등록 키**선택, hello 포털 형식과 복사 toohello VMM 서버에서 다운로드 한 hello 키입니다.
11. **자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다.

    ![서버 등록](./media/site-recovery-vmm-san/vault-creds.png)
12. hello 암호화 설정은 VMM tooAzure 복제에만 사용 됩니다. 무시해도 됩니다.

    ![서버 등록](./media/site-recovery-vmm-san/encrypt.png)
13. **서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다. 클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.
14. **초기 클라우드 메타 데이터 동기화**hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용할지 선택 합니다. 이 작업은 toohappen 각 서버에서 한 번만 필요합니다. Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.

    ![서버 등록](./media/site-recovery-vmm-san/friendly-name.png)

15. 클릭 **다음** toocomplete hello 프로세스입니다. 등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버에 표시 되 **서버** > **VMM 서버** hello 자격 증명 모음에 있습니다.

### <a name="command-line-installation"></a>명령줄 설치

다음 명령줄 hello를 사용 하 여 hello Azure Site Recovery Provider를 설치할 수도 있습니다. 이 메서드는 Server Core에 대 한 Windows Server 2012 r 2에서 사용 되는 tooinstall hello 공급자 수 있습니다.

1. Hello 공급자 설치 파일과 등록 키 tooa 폴더를 다운로드 합니다. 예: C:\ASR.
2. Hello VMM 서비스를 중지 합니다.
3. Hello 공급자 설치 관리자를 추출 합니다. 관리자 권한으로 다음 명령을 실행합니다.

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Hello 공급자를 설치 합니다.

        C:\ASR> setupdr.exe /i
5. Hello 공급자를 등록 합니다.

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

매개 변수

* **/ 자격 증명**: 필수 매개 변수는 hello 등록 키 파일의 위치를 가리키는 hello 위치입니다.  
* **/ FriendlyName**: hello Azure Site Recovery 포털에 표시 되는 hello Hyper-v 호스트 서버 hello 이름에 대 한 필수 매개 변수입니다.
* **/ EncryptionEnabled**: tooAzure VMM에서에서 복제 하는 경우에 사용 하는 선택적 매개 변수입니다.
* **/proxyAddress**: hello hello 프록시 서버의 주소를 지정 하는 선택적 매개 변수입니다.
* **/proxyport**: hello hello 프록시 서버의 포트를 지정 하는 선택적 매개 변수입니다.
* **/proxyUsername**: (hello 프록시에 인증이 필요) 하는 경우 hello 프록시 사용자 이름을 지정 하는 선택적 매개 변수입니다.
* **/proxyPassword**: (hello 프록시에 인증이 필요) 하는 경우 프록시 서버 hello에 인증 하기 위해 hello 암호를 지정 하는 선택적 매개 변수입니다.

## <a name="step-3-map-storage-arrays-and-pools"></a>3단계: 저장소 배열과 풀 매핑

기본 및 보조 배열 toospecify를 hello 기본 풀에서 복제 데이터를 수신 하는 보조 저장소 풀을 매핑하십시오. 매핑할 저장소 복제를 구성 하기 전에 복제 그룹에 대 한 보호를 사용 하도록 설정 하면 hello 매핑 정보가 사용 됩니다.

시작 하기 전에 hello 자격 증명 모음에 VMM 클라우드에 표시 되는지 확인 합니다. 공급자 설치 중 모든 클라우드를 동기화 할 때 또는 hello VMM 콘솔에서 특정 클라우드를 동기화 하면 클라우드가 검색 됩니다.

1. **리소스** > **서버 저장소** > **원본 및 대상 배열 매핑**을 클릭합니다.
    ![서버 등록](./media/site-recovery-vmm-san/storage-map.png)

2. Hello 저장소 배열에 hello 기본 사이트를 선택 하 고 hello 보조 사이트에 toostorage 배열에 매핑하십시오. **저장소 풀**원본을 선택 하 고 저장소 풀 toomap 대상으로 합니다.

    ![서버 등록](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>4단계: 복제 설정 구성

VMM 서버가 등록된 후에는 클라우드 보호 설정을 구성합니다.

1. Hello에 **빠른 시작** 페이지 **VMM 클라우드에 대 한 보호 설정**합니다.
2. Hello에 **보호 된 항목** 탭을 선택 hello 클라우드 **구성**합니다.
3. **대상**에서 **VMM**을 선택합니다.
4. **대상 위치**선택, toouse 복구에 대 한 원하는 hello 클라우드를 관리 하는 hello VMM 서버입니다.
5. **대상 클라우드**, toouse VM 장애 조치에 대해 원하는 hello 대상 클라우드를 선택 합니다.
   * Hello 가상 컴퓨터 보호에 대 한 복구 요구 사항을 충족 하는 대상 클라우드를 선택 하는 것이 좋습니다.
   * 클라우드는 tooa 단일 클라우드 쌍은 주 가상 컴퓨터 또는 대상 클라우드로만 속할 수 있습니다.
6. 사이트 복구 클라우드 액세스 tooSAN 저장소 및 해당 hello 저장소 배열에 매핑되는 했는지 확인 합니다.
7. 확인에 성공하면 **복제 유형**에서 **SAN**을 선택합니다.

Hello 설정을 저장 한 후 ְ  있는 hello에서 모니터링할 수 **작업** 탭 합니다. Hello에 설정을 수정할 수 있는 **구성** 탭 합니다. Toomodify hello 대상 위치 또는 대상 클라우드를 원하는 경우 hello 클라우드 구성을 제거한 후 hello 클라우드를 다시 구성 해야 합니다.

## <a name="step-5-enable-network-mapping"></a>5단계: 네트워크 매핑 사용

1. Hello에 **빠른 시작** 페이지 **네트워크 매핑**합니다.
2. Hello 원본 VMM 서버를 선택한 다음 네트워크가 매핑될 hello 대상 VMM 서버 toowhich hello를 선택 합니다. 원본 네트워크 및 연결 된 대상 네트워크의 hello 목록이 표시 됩니다. 매핑되지 않은 네트워크에 대해서는 빈 값이 표시됩니다. Hello 정보 아이콘 다음 toohello 소스 및 대상 네트워크 이름 tooview hello에 대 한 서브넷 각 네트워크를 클릭 합니다.
3. **원본 네트워크**에서 네트워크를 선택하고 **매핑**을 클릭합니다. hello 서비스는 hello hello 대상 서버의 VM 네트워크를 검색 하 고 표시 합니다.

    ![SAN 아키텍처](./media/site-recovery-vmm-san/network-map1.png)
4. Hello 대상 VMM 서버에서 hello VM 네트워크 중 하나를 선택 합니다.

    ![SAN 아키텍처](./media/site-recovery-vmm-san/network-map2.png)

5. 대상 네트워크를 선택 하면 hello hello 원본 네트워크를 사용 하는 보호 된 클라우드가 표시 됩니다. 사용 가능한 대상 네트워크도 표시됩니다. 복제에 사용할 사용 가능한 tooall hello 클라우드에 있는 대상 네트워크를 선택 하는 것이 좋습니다.
6. Hello 확인 표시가 toocomplete hello 매핑 프로세스를 클릭 합니다. 진행 상황을 추적하는 작업이 시작됩니다. Hello에서 볼 수 있습니다 **작업** 탭 합니다.

## <a name="step-6-enable-replication-for-replication-groups"></a>6단계: 복제 그룹에 대해 복제 사용

가상 컴퓨터에 대 한 보호를 활성화 하려면 먼저 tooenable 복제 저장소 복제 그룹에 대 한 합니다.

1. Hello에 **속성** hello open hello hello 사이트 복구 포털의 기본 클라우드 페이지 **가상 컴퓨터** 탭을 클릭 **복제 그룹 추가**합니다.
2. 하나 이상의 VMM 복제 그룹 선택 hello 클라우드와 연결 된 hello 소스 및 대상 배열을 확인 하 고 hello 복제 빈도 지정 합니다.

사이트 복구, VMM 및 hello Smi-s 공급자 hello 대상 사이트 저장소 Lun을 프로 비전 하 고 저장소 복제를 사용 하도록 설정 합니다. Hello 복제 그룹이 이미 복제 된 경우 사이트 복구 hello 기존 복제 관계를 다시 사용 및 업데이트 hello 정보입니다.

## <a name="step-7-enable-protection-for-virtual-machines"></a>7단계: 가상 컴퓨터의 보호 활성화


저장소 그룹을 복제할 때 hello 메서드를 다음 중 하나가 지정 된 hello VMM 콘솔에서 Vm에 대 한 보호 사용:

* **새 가상 컴퓨터**: 복제를 활성화 하 고 VM hello와 hello 복제 그룹에 연결 하는 VM을 만들 때.
  이 옵션을 VMM에서 hello 복제 그룹의 hello Lun에 지능형 배치 toooptimally 위치 hello VM 저장소를 사용합니다. 사이트 복구는 hello 그림자 hello 보조 사이트의 VM 만들기를 조정 하 고 장애 조치 후 복제 Vm을 시작할 수 있도록 용량을 할당 합니다.
* **기존 가상 컴퓨터**: 가상 컴퓨터는 VMM에서 이미 배포한 경우에 복제 사용을 저장소 마이그레이션 tooa 복제 그룹을 수행할 수 있습니다. 완료 되 면 VMM 및 사이트 복구에서 검색 한 후 새 VM hello 및 사이트 복구에서 관리를 시작 합니다. 그림자 VM hello 보조 사이트에 만들어지면 및 장애 조치 된 후 해당 hello 복제본 VM을 시작할 수 있도록 용량이 할당 됩니다.

![보호 사용](./media/site-recovery-vmm-san/enable-protect.png)

Vm 복제를 활성화 한 후 hello Site Recovery 콘솔에 나타납니다. VM 속성을 보고, 상태를 추적하고, 여러 VM이 포함된 복제 그룹 장애 조치(Failover)를 추적할 수 있습니다. SAN 복제에서 복제 그룹과 연결된 모든 VM은 함께 장애 조치(Failover)되어야 합니다. 장애 조치 hello 저장소 계층에서 먼저 발생 때문입니다. 것이 중요 한 toogroup 복제 올바르게 그룹화 하 고 연결된 하는 Vm만 함께 배치 합니다.

> [!NOTE]
> VM에 대 한 복제를 설정한 후 사이트 복구 복제 그룹에 있는 경우를 제외 해당 Vhd tooLUNs를 추가 하지 마십시오. VHD가 Site Recovery 복제 그룹에 있어야만 Site Recovery에서 찾을 수 있습니다.
>
>

Hello에 hello 초기 복제를 포함 하 여 진행률을 추적할 수 있습니다 **작업** 탭 합니다. Hello 보호 완료 작업이 실행 된 후에 hello 가상 컴퓨터는 장애 조치에 대 한 준비.

![가상 컴퓨터 보호 작업](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>8 단계: hello 배포를 테스트 합니다.

프로그램 배포 toomake Vm 넘는 예상 대로 실패를 테스트 합니다. toodo이 복구 계획을 만들고 테스트 장애 조치를 실행 합니다.

1. Hello에 **복구 계획** 탭을 클릭 **복구 계획 만들기**합니다.
2. Hello 복구 계획에 대 한 이름을 지정 하 고 원본 및 대상 VMM 서버를 선택 합니다. hello 원본 서버에 장애 조치 및 복구에 사용할 수 있는 Vm 있어야 합니다. 선택 **SAN** tooview만 클라우드에 SAN 복제에 대해 구성 된 합니다.

    ![복구 계획 만들기](./media/site-recovery-vmm-san/r-plan.png)

3. **가상 컴퓨터 선택**에서 복제 그룹을 선택합니다. Hello 그룹과 연결 된 모든 Vm toohello 복구 계획에 추가 됩니다. 이러한 Vm toohello 복구 계획 기본 그룹 (그룹 1)에 추가 됩니다. 필요한 경우 그룹을 더 추가할 수 있습니다. Vm 복제 후 toohello hello 복구 계획 그룹 순서에 따라 번호는 합니다.

    ![가상 컴퓨터 선택](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Hello에 hello 목록에 나타나는 hello 복구 계획을 만든 후 **복구 계획** 탭 합니다. Hello 계획을 선택 하 고 선택 **테스트 장애 조치**합니다.
5. Hello에 **확인 테스트 장애 조치** 페이지에서 **None**합니다. 이 옵션을 사용 하면 장애 조치 복제본 Vm hello tooany 연결 된 네트워크 수 없습니다. 이 테스트 예상 대로 Vm 장애 조치 하는 hello 하지만 hello 네트워크 환경을 테스트 하지 않습니다. 기타 네트워킹 옵션에 대한 자세한 내용은 [Site Recovery 장애 조치(Failover)](site-recovery-failover.md)를 참조하세요.

    ![테스트 네트워크 선택](./media/site-recovery-vmm-san/test-fail1.png)

6. hello 테스트 VM hello hello 호스트로 VM이 있는 hello 복제본에서 동일한 호스트에 만들어집니다. hello에 복제본 VM이 있는 toohello 클라우드는 추가 되지 않습니다.
2. 복제, 후 hello 복제본 VM hello 주 가상 컴퓨터와 다른 IP 주소를 갖습니다. DHCP에서 주소를 발급하는 경우 주소가 자동으로 업데이트됩니다. DHCP를 사용 하지 않는 hello 하려는 경우 동일한 주소, toorun 몇 가지 스크립트를 사용 해야 합니다.
3. 이 스크립트 tooretrieve hello IP 주소를 실행 합니다.

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. 이 샘플 스크립트 tooupdate DNS를 실행 합니다. 검색 한 hello IP 주소를 지정 합니다.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>다음 단계

환경을 작동 하는 테스트 장애 조치 toocheck를 예상 대로 실행 했으면 후 참조 [사이트 복구 장애 조치](site-recovery-failover.md) toolearn 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 합니다.
