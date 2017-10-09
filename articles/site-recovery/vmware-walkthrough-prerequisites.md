---
title: "Azure Site Recovery를 사용 하 여 VMware tooAzure 복제에 대 한 aaaPrerequisites | Microsoft Docs"
description: "VMware Vm tooAzure, hello Azure Site Recovery 서비스를 사용 하 여에서 실행 되는 작업을 복제 하기 위한 필수 구성 요소를 hello 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>2 단계: VMware tooAzure 복제에 대 한 hello 필수 구성 요소를 검토 합니다.

다음 표에 hello에 요약 되어 hello 필수 구성 요소를 읽습니다.

**필수 요소** | **세부 정보**
--- | ---
**Azure** | [Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.
**온-프레미스 구성 서버** | Windows Server 2012 R2 이상을 실행하는 VMware VM이 필요합니다. Site Recovery를 배포하는 동안 이 서버를 설정합니다.<br/><br/> 기본 hello 프로세스에 의해 서버 및 마스터 대상 서버 에서도이 VM에 설치 됩니다. 수직 확장, 별도 프로세스 서버를 할 수 있고 hello 갖고 hello 구성 서버와 동일한 요구 사항이 있습니다.<br/><br/> [여기](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)에서 이러한 구성 요소에 대해 자세히 알아보기
**온-프레미스 VMware 서버** | 최신 업데이트가 포함된 6.5, 6.0, 5.5, 5.1을 실행하는 하나 이상의 VMware vSphere 서버. 서버 hello hello 구성 서버 (또는 별도 프로세스 서버)와 동일한 네트워크에 있어야 합니다.<br/><br/> VCenter 서버 hello 최신 업데이트로 6.5, 6.0 또는 5.5를 실행 하는 toomanage 호스트를 좋습니다.
**온-프레미스 VM** | Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다. VM에서 VMware 도구가 실행되어야 합니다.
**URL** | 구성 서버 hello toothese Url에 액세스 해야 합니다.<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.<br/></br> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.<br/></br> West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.<br/><br/> 이 URL hello MySQL 다운로드에 대 한 허용: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi 합니다.
**모바일 서비스** | 모든 복제된 VM에 설치




## <a name="limitations"></a>제한 사항

배포 하기 전에 hello 표에 요약 된 hello 제한 이해 하 고 있는지 확인 합니다.

**제한 사항** | **세부 정보**
--- | ---
**Azure** | 저장소 및 네트워크 계정은 hello에 있어야 hello 자격 증명 모음과 동일한 지역<br/><br/> 프리미엄 저장소 계정을 사용 하는 경우 또한 해야 표준 계정 toostore 복제 로그를 저장 합니다.<br/><br/> Toopremium 계정 중앙 및 남 인도에 복제할 수 없습니다.
**온-프레미스 구성 서버** | VMware VM 어댑터 유형은 VMXNET3이어야 합니다. 그렇지 않은 경우 [이 업데이트를 설치하세요.](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere PowerCLI 6.0을 설치해야 합니다.<br/><br> hello 컴퓨터는 도메인 컨트롤러일 하지 않아야 합니다. hello 컴퓨터에 고정 IP 주소를 해야 합니다.<br/><br/> hello 호스트 이름은 15 자 여야 합니다, 운영 체제 영어에 있어야 합니다.
**VMware** | Site Recovery에서는 교차 vCenter vMotion, 가상 볼륨 및 저장소 DRS와 같은 새로운 vCenter 및 vSphere 6.5 및 6.0 기능을 지원하지 않습니다.
**VM** | [Azure VM 제한 사항](site-recovery-prereq.md#azure-requirements) 확인<br/><br/> 암호화된 디스크를 사용하는 VM 또는 UEFI/EFI 부팅을 사용하는 VM은 복제할 수 없습니다.<br/><br> 공유 디스크 클러스터는 지원되지 않습니다. Hello 소스가 VM에서 NIC 팀을 가진 경우 변환 tooa 장애 조치 후 NIC를 단일 합니다.<br/><br/> Vm에 iSCSI 디스크 있으면 사이트 복구 변환 tooa VHD 파일 장애 조치 후 합니다. Hello Azure VM으로 hello iSCSI 대상에 연결할 수 경우 tooit를 연결 하 고 괄호와 hello VHD에 게 표시 합니다. 이 경우 hello iSCSI 대상 연결을 끊습니다.<br/><br/> 동일한 작업 toobe 복구 hello를 실행 하는 Vm 수 있는 tooenable 다중 VM 일관성을 원하는 함께 tooa 일관 된 데이터를 가리키고 20004 hello VM에서 포트를 열어야 합니다.<br/><br/> Windows는 hello C 드라이브에 설치 되어야 합니다. 기본 및 동적 아님 hello OS 디스크 여야 합니다. 데이터 디스크 hello 동적일 수 있습니다.<br/><br/> Vm에서 Linux /etc/hosts 파일에는 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목이 없어야 합니다. 호스트 이름, 탑재 지점, 장치 이름, 시스템 경로 및 파일 이름 hello (/ 등; /usr)만 영어에 있어야 합니다.<br/><br/> 특정 유형의 [Linux 저장소](site-recovery-support-matrix-to-azure.md#support-for-storage)가 지원됩니다.<br/><br/>만들거나 설정 **disk.enableUUID=true** hello VM 설정에서 합니다. 올바르게를 탑재 하 고만 델타 변경 내용을 전체 복제 하지 않고 장애 복구 하는 동안 전송된 백 tooon 온-프레미스 있도록 일관 된 UUID toohello VMDK를 제공 합니다.


## <a name="next-steps"></a>다음 단계

- 전체 배포를 수행 하는 경우 너무 이동[3 단계: 용량 계획](vmware-walkthrough-capacity.md)
- 간단한 테스트 배포를 수행 하는 경우 너무 이동[4 단계: 네트워킹 계획](vmware-walkthrough-network.md)합니다.
