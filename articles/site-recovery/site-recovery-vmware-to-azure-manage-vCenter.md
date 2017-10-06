---
title: " Azure Site Recovery에서 VMware vCenter 서버 관리 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에서 VMware vCenter를 추가 및 관리하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Azure Site Recovery에서 VMware vCenter 서버 관리
이 문서에서는 hello VMware vCenter에 수행할 수 있는 다양 한 사이트 복구 작업입니다.

## <a name="prerequisites"></a>필수 조건

**VMware vCenter 및 VMware vSphere ESX 호스트 지원** | **세부 정보** |
|--- | --- |
|**온-프레미스 VMware 서버** | 최신 업데이트가 포함된 6.0, 5.5, 5.1을 실행하는 하나 이상의 VMware vSphere 서버. 서버 hello hello 구성 서버 (또는 별도 프로세스 서버)와 동일한 네트워크에 있어야 합니다.<br/><br/> VCenter 서버 toomanage 실행 하는 호스트를, 6.0 또는 5.5 hello 최신 업데이트로 좋습니다. 버전 6.0을 배포하는 경우 5.5에서 사용할 수 있는 기능만 지원됩니다.|

## <a name="prepare-an-account-for-automatic-discovery"></a>자동 검색용 계정 준비
사이트 복구 및 장애 조치 및 가상 컴퓨터의 장애 복구에 가상 컴퓨터를 검색 하는 hello 프로세스 서버 tooautomatically 대 한 액세스 tooVMware 필요 합니다.

* **마이그레이션**: 읽기 전용 역할을 갖는 VMware 계정 적이 다시 실패 하지 않고 toomigrate VMware 가상 컴퓨터 tooAzure만 하려는 경우 사용할 수 있습니다. 이러한 역할은 장애 조치(failover)를 실행할 수 있지만 보호된 원본 컴퓨터를 종료할 수는 없습니다. 마이그레이션에서는 필요하지 않습니다.
* **Replicate/복구**: 가상 컴퓨터의 전원을 켜는 toodeploy 전체 복제 (복제, 장애 조치, 장애 복구) hello 계정이 생성 및 디스크를 제거 하는 등의 작업 수 toorun 이어야 합니다.
* **자동 검색**: 최소한 읽기 전용 계정이 필요합니다.


|**작업** | **필요한 계정/역할** | **권한** | **세부 정보**|
|--- | --- | --- | ---|
|**프로세스 서버가 VMware 가상 컴퓨터를 자동으로 검색** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** toohello 자식 개체 (vSphere 호스트, 데이터 저장소, 가상 컴퓨터 및 네트워크) 개체입니다.|
|**장애 조치(Failover)** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체 toohello 자식 개체 (vSphere 호스트, 데이터 저장소, 가상 컴퓨터 및 네트워크).<br/><br/> 전체 복제, 장애 조치, 장애 복구가 아닌 마이그레이션에 유용합니다.|
|**장애 조치 및 장애 복구** | Hello 필요한 사용 권한이 있는 역할 (AzureSiteRecoveryRole)을 만들고 다음 hello 역할 tooa VMware 사용자 또는 그룹을 할당 것이 좋습니다. | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 AzureSiteRecoveryRole =<br/><br/> 데이터 저장소 -> 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트<br/><br/> 네트워크 -> 네트워크 할당<br/><br/> 리소스 할당 VM tooresource 풀->, 마이그레이션 전원이 꺼진 VM, VM의 전원이 마이그레이션<br/><br/> 태스크 -> 만들기 태스크, 업데이트 태스크<br/><br/> 가상 컴퓨터 -> 구성<br/><br/> 가상 컴퓨터 -> 상호 작용 -> 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치<br/><br/> 가상 컴퓨터 -> 인벤토리 -> 만들기, 등록, 등록 취소<br/><br/> 가상 컴퓨터 -> 프로비전 -> 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용<br/><br/> 가상 컴퓨터 -> 스냅숏 -> 스냅숏 제거 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** toohello 자식 개체 (vSphere 호스트, 데이터 저장소, 가상 컴퓨터 및 네트워크) 개체입니다.|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>계정 tooconnect tooVMware vCenter 서버 만들기 / VMware vSphere EXSi 호스트
1. Hello 구성 서버와 시작 hello cspsconfigtool.exe hello 바탕 화면에 배치 하는 hello 바로 가기를 사용 하 여에 로그인 합니다.
2. 클릭 **계정 추가** hello에 **계정 관리** 탭 합니다.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Hello 계정 세부 정보를 제공 하 고 확인 tooadd hello 계정을 클릭 합니다. hello 계정은 hello에 나열 된 hello 권한이 있어야 [자동 검색에 대 한 계정을 준비](#prepare-an-account-for-automatic-discovery) 섹션.

  >[!NOTE]
  Hello 계정 정보 toobe hello Site Recovery 서비스와 동기화 될 때까지 약 15 분 걸립니다.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>VMware vCenter/VMware vSphere ESX 호스트 연결(vCenter 추가)
* Azure 포털 hello, 너무 찾아보기*YourRecoveryServicesVault* > **사이트 복구 인프라** > **구성 서버**  >  *ConfigurationServer*
* Hello 구성 서버 세부 정보 페이지에서 클릭 안녕하세요 + vCenter 단추입니다.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>사용 된 자격 증명 tooconnect toohello vCenter 서버 수정 / vSphere ESXi 호스트

1. Hello 구성 서버와 시작 hello cspsconfigtool.exe에 로그인
2. 클릭 **계정 추가** hello에 **계정 관리** 탭 합니다.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Hello 새 계정 정보를 제공 하 고 확인 tooadd hello 계정을 클릭 합니다. hello 계정은 hello에 나열 된 hello 권한이 있어야 [자동 검색에 대 한 계정을 준비](#prepare-an-account-for-automatic-discovery) 섹션.
4. Azure 포털 hello, 너무 찾아보기*YourRecoveryServicesVault* > **사이트 복구 인프라** > **구성 서버**  >  *ConfigurationServer*
5. Hello 구성 서버 세부 정보 페이지에서 클릭 hello **서버 새로 고침** 단추입니다.
6. Hello 새로 고침 서버 작업이 완료 되 면 hello vCenter Server tooopen hello vCenter 요약 페이지를 선택 합니다.
7. 선택 hello 새로 추가 된 계정에 hello **vCenter 서버/vSphere 호스트 계정** 필드를 클릭 hello **저장** 단추입니다.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Azure Site Recovery에서 vCenter 삭제
1. Azure 포털 hello, 너무 찾아보기*YourRecoveryServicesVault* > **사이트 복구 인프라** > **구성 서버**  >  *ConfigurationServer*
2. Hello 구성 서버 세부 정보 페이지 hello vCenter Server tooopen hello vCenter 요약 페이지를 선택 합니다.
3. Hello 클릭 **삭제** toodelete hello vCenter 단추

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
필요한 경우 toomodify hello Vcenter FQDN/IP 주소, 포트 세부 정보 toodelete hello vCenter 서버에 필요 하 고 다시 추가 합니다.
