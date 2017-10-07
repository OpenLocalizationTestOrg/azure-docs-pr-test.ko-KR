---
title: "(VMware tooAzure) hello 소스 환경 설정 | Microsoft Docs"
description: "이 문서에서는 VMware 가상 복제 하 여 온-프레미스 환경 toostart tooset tooAzure 컴퓨터 하는 방법을 설명 합니다."
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
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Hello 소스 환경 (VMware tooAzure) 설정
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [물리적 tooAzure](./site-recovery-set-up-physical-to-azure.md)

이 문서에서는 tooset 가상 복제 하 여 온-프레미스 환경 toostart 컴퓨터의 실행 방법을 설명 VMware tooAzure에 있습니다.

## <a name="prerequisites"></a>필수 조건

hello 문서에서는 이미 만들었다고 가정 합니다.
- Hello에 복구 서비스 자격 증명 모음 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.
- [자동 검색](./site-recovery-vmware-to-azure.md)에 사용할 수 있는 VMware vCenter의 전용 계정
- Tooinstall hello 구성 서버에서 가상 컴퓨터.

## <a name="configuration-server-minimum-requirements"></a>구성 서버 최소 요구 사항
hello 구성 서버 소프트웨어는 항상 사용 가능한 VMware 가상 컴퓨터에 배포 되어야 합니다. 다음 표에서 hello hello 최소 하드웨어, 소프트웨어 및 구성 서버에 대 한 네트워크 요구 사항을 나열 합니다.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS 기반 프록시 서버 hello 구성 서버에서 지원 되지 않습니다.

## <a name="choose-your-protection-goals"></a>보호 목표 선택

1. Hello Azure 포털에서에서 toohello 이동 **복구 서비스** 블레이드를 자격 증명 모음 및 자격 증명 모음을 선택 합니다.
2. Hello 자격 증명 모음의 hello 리소스 메뉴에서 이동 너무**시작** > **사이트 복구** > **1 단계: 인프라 준비**  >  **보호 목표**합니다.

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. **보호 목표**선택, **tooAzure**, 선택 **VMware vSphere 하이퍼바이저와 예,**합니다. 그런 후 **OK**를 클릭합니다.

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정
Hello 소스 환경 설정 두 가지 주요 작업이 포함 됩니다.

- Site Recovery를 사용하여 구성 서버를 설치 및 등록합니다.
- 사이트 복구 tooyour 온-프레미스 VMware vCenter 또는 vSphere EXSi 호스트를 연결 하 여 온-프레미스 가상 컴퓨터를 검색 합니다.

### <a name="step-1-install-and-register-a-configuration-server"></a>1단계: 구성 서버 설치 및 등록

1. **1단계: 인프라 준비** > **원본**을 클릭합니다. **준비 소스**클릭 하 여 구성 서버, 없는 경우, **구성 서버 +** tooadd 하나입니다.

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Hello에 **서버 추가** 블레이드를 확인 하는 **구성 서버** 에 표시 **서버 유형**합니다.
4. Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.
5. Hello 자격 증명 모음 등록 키를 다운로드 합니다. 통합 설치를 실행할 때 hello 등록 키가 필요 합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Hello 구성 서버를 사용 하는 hello 컴퓨터에서 실행 **Azure Site Recovery 통합 설치** tooinstall hello 구성 서버, 프로세스 서버 hello 및 hello 마스터 대상 서버입니다.

#### <a name="run-azure-site-recovery-unified-setup"></a>Azure Site Recovery 통합 설치 프로그램 실행

> [!TIP]
> 컴퓨터의 시스템 시계에 hello 시간이 현지 시간에서 5 분 이상 차이가 날 구성 서버 등록에 실패 합니다. 시스템 시계와 동기화 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello 설치를 시작 하기 전에.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 명령줄을 통해 hello 구성 서버를 설치할 수 있습니다. 자세한 내용은 참조 [명령줄 도구를 사용 하 여 설치 hello 구성 서버](http://aka.ms/installconfigsrv)합니다.

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>자동 검색에 대 한 hello VMware 계정 추가

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>2단계: vCenter 추가
tooallow Azure Site Recovery toodiscover 가상 컴퓨터 사용자의 온-프레미스 환경에서 실행 해야 tooconnect VMware vCenter Server 또는 사이트 복구와 vSphere ESXi 호스트 합니다.

선택 **+ vCenter** toostart VMware vCenter server 또는 VMware vSphere ESXi 호스트를 연결 합니다.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>일반적인 문제
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>다음 단계
Azure에서 [대상 환경 설정](./site-recovery-prepare-target-vmware-to-azure.md).
