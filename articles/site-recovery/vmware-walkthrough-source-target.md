---
title: "hello 소스 및 대상에 Azure Site Recovery와 VMware 복제 tooAzure aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 VMware Vm tooAzure 저장소의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>8 단계: hello 원본 및 복제 tooAzure VMware에 대 한 대상 설정

이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 VMware 가상 컴퓨터 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

Hello 구성 서버를 설정 하 고 hello 자격 증명 모음에 등록 한 다음 Vm을 검색 합니다.

1. **Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.
2. 구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.
3. **서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.
4. Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.
5. Hello 자격 증명 모음 등록 키를 다운로드 합니다. 통합 설치를 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

   ![원본 설정](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Hello 구성 서버 hello 자격 증명 모음 등록

수행 하기 전에 hello 다음로 시작 하 고 통합 설치 tooinstall hello 구성 서버, hello 프로세스 서버 및 마스터 대상 서버 hello 실행 합니다.
    - 간단한 동영상 개요 보기

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Hello 구성 서버 VM에서 해당 hello 시스템 시계와 동기화 되었는지 확인 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)합니다. 서로 일치해야 합니다. 15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.
    - Hello 구성 서버 VM에서 로컬 관리자로 설치 프로그램을 실행 합니다.
    - Hello VM에서 TLS 1.0을 사용할 수 있는지 확인 합니다.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> hello 구성 서버를 설치할 수도 있습니다 [hello 명령줄에서](http://aka.ms/installconfigsrv)합니다.



## <a name="connect-toovmware-servers"></a>TooVMware 서버 연결

tooallow Azure Site Recovery toodiscover 가상 컴퓨터 사용자의 온-프레미스 환경에서 실행 해야 tooconnect VMware vCenter Server 또는 사이트 복구와 vSphere ESXi 호스트 합니다. 시작 하기 전에 hello 다음 note:

- Hello 서버에서 관리자 권한이 없는 계정으로 vSphere 호스트 tooSite 복구 또는 hello vCenter 서버를 추가 하는 경우 hello 계정이 이러한 권한을 사용할 수 있어야 합니다.
    - 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터, vSphere 분산 스위치 등의 권한을 사용할 수 있도록 설정해야 합니다.
    - hello vCenter 서버에 저장소 보기 권한이 필요합니다.
- VMware 서버 tooSite 복구를 추가 하면 15 분이 걸릴 수 정도을 tooappear hello 포털에서 합니다.

### <a name="add-hello-account-for-automatic-discovery"></a>자동 검색에 대 한 hello 계정 추가

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>연결 설정

다음과 같이 tooservers 연결:

1. 선택 **+ vCenter** toostart VMware vCenter server 또는 VMware vSphere ESXi 호스트를 연결 합니다.
2. **vCenter 추가**hello vSphere 호스트 또는 vCenter 서버에 대 한 알기 쉬운 이름을 지정 하 고 다음 hello IP 주소 또는 hello 서버의 FQDN을 지정 합니다.
3. 다른 포트에서 요청에 대해 구성 된 toolisten VMware 서버 도달 하지 못할 경우 hello 포트를 443으로 그대로 둡니다. tooconnect toohello VMware vCenter 또는 vSphere ESXi 서버 hello 계정을 선택 합니다. **확인**을 클릭합니다.
4. TooVMware 서버를 연결 하는 사이트 복구 hello를 사용 하 여 설정을 지정 하 고 Vm을 검색 합니다.

> [!NOTE]
> 서버 또는 hello vCenter 또는 호스트 서버에 대 한 관리자 권한이 없는 계정으로는 호스트를 추가 하는 경우 hello 계정에 이러한 권한을 사용할 수 있는지 확인 하십시오: 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터 및 vSphere 분산 스위치입니다. 또한 hello VMware vCenter server는 권한 사용 하도록 설정 하는 hello 저장소 뷰가 필요 합니다.


## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정

Hello 대상 환경 설정 하기 전에 Azure 저장소 계정 및 가상 네트워크를 설정 했는지 확인 합니다.

1. 클릭 **준비 인프라** > **대상**, 선택 hello toouse를 원하는 Azure 구독 및 합니다.
2. 대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.
3. Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.

   ![대상](./media/vmware-walkthrough-source-target/gs-target.png)
4. 저장소 계정 또는 네트워크를 만들지 않은 경우 클릭 **저장소 계정 추가** 또는 **+ 네트워크**, 리소스 관리자 계정 또는 네트워크 인라인 toocreate 합니다.

## <a name="next-steps"></a>다음 단계

너무 이동[9 단계: 복제 정책 설정](vmware-walkthrough-replication.md)
