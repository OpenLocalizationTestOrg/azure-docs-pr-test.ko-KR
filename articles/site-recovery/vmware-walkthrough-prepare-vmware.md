---
title: "aaaPrepare 온-프레미스 VMware 리소스에 대 한 Azure Site Recovery와 복제 tooAzure | Microsoft Docs"
description: "VMware Vm tooAzure 저장소에서 실행 되는 작업을 복제 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>6 단계: 온-프레미스 VMware 복제 tooAzure 준비

Hello 지침을 사용 하 여 Azure Site Recovery와이 문서 tooprepare 온-프레미스 VMware 서버 toointeract에 및 VMWare Vm hello 모바일 서비스의 설치를 준비 합니다. hello 모바일 서비스 에이전트가 tooreplicate tooAzure 원하는 모든 온-프레미스 Vm에 설치 되어야 합니다.

## <a name="prepare-for-automatic-discovery"></a>자동 검색 준비

Site Recovery는 vSphere ESXi 호스트에서 실행 중인 VM을 자동으로 검색합니다(vCenter 서버 포함 또는 제외). 자동 검색, 사이트 복구 요구 계정 tooaccess 호스트 및 서버:

1. 전용된 계정 toouse (hello 테이블 아래에서 설명 하는 hello 사용 권한이 사용의 hello vCenter 수준에서 역할 만들기 이름을 **Azure_Site_Recovery**와 같이 지정합니다.
2. 그런 다음 hello vSphere 호스트/vCenter 서버에 사용자를 만들고 hello 역할 toohello 사용자를 할당 합니다. Site Recovery를 배포하는 동안 이 사용자 계정을 지정합니다.


### <a name="vmware-account-permissions"></a>VMware 계정 권한

사이트 복구 및 장애 조치 및 Vm의 장애 복구에 hello 프로세스 서버 tooautomatically 검색 Vm에 대 한 액세스 tooVMware 필요 합니다.

- **마이그레이션**: 읽기 전용 역할을 갖는 VMware 계정 적이 다시 실패 하지 않고 toomigrate VMware Vm tooAzure만 하려는 경우 사용할 수 있습니다. 이러한 역할은 장애 조치(failover)를 실행할 수 있지만 보호된 원본 컴퓨터를 종료할 수는 없습니다. 마이그레이션에서는 필요하지 않습니다.
- **Replicate/복구**: Vm 등의 전원을 켜는 toodeploy 전체 복제 (복제, 장애 조치, 장애 복구) hello 계정이 생성 및 디스크를 제거 하는 등의 작업 수 toorun 이어야 합니다.
- **자동 검색**: 최소한 읽기 전용 계정이 필요합니다.


**Task** | **필요한 계정/역할** | **권한** | **세부 정보**
--- | --- | --- | ---
**프로세스 서버가 VMware VM을 자동으로 검색** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체, toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).
**장애 조치(Failover)** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체 toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).<br/><br/> 전체 복제, 장애 조치, 장애 복구가 아닌 마이그레이션에 유용합니다.
**장애 조치 및 장애 복구** | Hello 필요한 사용 권한이 있는 역할 (Azure_Site_Recovery)을 만들고 다음 hello 역할 tooa VMware 사용자 또는 그룹을 할당 것이 좋습니다. | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 Azure_Site_Recovery =<br/><br/> 데이터 저장소 -> 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트<br/><br/> 네트워크 -> 네트워크 할당<br/><br/> 리소스 할당 VM tooresource 풀->, 마이그레이션 전원이 꺼진 VM, VM의 전원이 마이그레이션<br/><br/> 태스크 -> 만들기 태스크, 업데이트 태스크<br/><br/> 가상 컴퓨터 -> 구성<br/><br/> 가상 컴퓨터 -> 상호 작용 -> 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치<br/><br/> 가상 컴퓨터 -> 인벤토리 -> 만들기, 등록, 등록 취소<br/><br/> 가상 컴퓨터 -> 프로비전 -> 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용<br/><br/> 가상 컴퓨터 -> 스냅숏 -> 스냅숏 제거 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체, toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Hello 모바일 서비스의 강제 설치에 대 한 준비

hello 모바일 서비스를 설치 해야 tooreplicate 원하는 모든 vm입니다. 수동 설치 hello 사이트 복구 프로세스 서버에서 강제 설치와 System Center Configuration Manager와 같은 메서드를 사용 하 여 설치를 포함 하 여 같은 방법으로 tooinstall hello 서비스의 여러 가지가 있습니다.

Toouse 강제 설치를 수행 하는 경우 사이트 복구 tooaccess hello VM을 사용할 수 있는 계정을 tooprepare를 해야 합니다.

- 도메인 또는 로컬 계정을 사용할 수 있습니다.
- Windows 도메인 계정을 사용 하지 않는 경우 필요 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 합니다. 이 hello에 등록할 toodo **찾아**, hello DWORD 항목을 추가 **LocalAccountTokenFilterPolicy**, 값이 1 인 합니다.
- Windows에서 CLI tooadd hello 레지스트리 항목을 하려는 경우 다음을 입력 합니다.``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Linux 용 hello 계정은 hello 원본 Linux 서버에 루트 이어야 합니다.



## <a name="next-steps"></a>다음 단계

너무 이동[7 단계: 자격 증명 모음 만들기](vmware-walkthrough-create-vault.md)
