---
title: "(실제 서버 tooAzure) hello 소스 환경 설정 | Microsoft Docs"
description: "이 문서에서는 설명 어떻게를 Azure에 Windows 또는 Linux를 실행 하는 물리적 서버를 복제 하 여 온-프레미스 환경 toostart tooset 합니다."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Hello 소스 환경 (실제 서버 tooAzure) 설정
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [물리적 tooAzure](./site-recovery-set-up-physical-to-azure.md)

이 문서에서는 설명 어떻게를 Azure에 Windows 또는 Linux를 실행 하는 물리적 서버를 복제 하 여 온-프레미스 환경 toostart tooset 합니다.

## <a name="prerequisites"></a>필수 조건

hello 문서에서는 이미 있다고 가정 합니다.
1. Hello에 복구 서비스 자격 증명 모음 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.
3. Tooinstall hello 구성 서버에서 물리적 컴퓨터입니다.

### <a name="configuration-server-minimum-requirements"></a>구성 서버 최소 요구 사항
다음 표에서 hello hello 최소 하드웨어, 소프트웨어 및 구성 서버에 대 한 네트워크 요구 사항을 나열 합니다.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS 기반 프록시 서버 hello 구성 서버에서 지원 되지 않습니다.

## <a name="choose-your-protection-goals"></a>보호 목표 선택

1. Hello Azure 포털에서에서 toohello 이동 **복구 서비스** 블레이드를 자격 증명 모음 및 자격 증명 모음을 선택 합니다.
2. Hello에 **리소스** hello 자격 증명 모음의 메뉴 클릭 **시작** > **사이트 복구** > **1 단계: 준비 인프라** > **보호 목표**합니다.

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. **보호 목표**선택, **tooAzure** 및 **하지 가상화 된/기타**, 클릭 하 고 **확인**합니다.

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

1. **준비 소스**클릭 하 여 구성 서버, 없는 경우, **구성 서버 +** tooadd 하나입니다.

  ![원본 설정](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. Hello에 **서버 추가** 블레이드에서 있는지 여부를 확인 **구성 서버** 에 표시 **서버 유형**합니다.
4. Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.
5. Hello 자격 증명 모음 등록 키를 다운로드 합니다. 통합 설치를 실행할 때 hello 등록 키가 필요 합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![원본 설정](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Hello 구성 서버를 사용 하는 hello 컴퓨터에서 실행 **Azure Site Recovery 통합 설치** tooinstall hello 구성 서버, 프로세스 서버 hello 및 hello 마스터 대상 서버입니다.

#### <a name="run-azure-site-recovery-unified-setup"></a>Azure Site Recovery 통합 설치 프로그램 실행

> [!TIP]
> 컴퓨터의 시스템 시계에 hello 시간은 현지 시간에서 5 분 넘게 구성 서버 등록 실패 합니다. 시스템 시계와 동기화 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello 설치를 시작 하기 전에.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 명령줄을 통해 hello 구성 서버를 설치할 수 있습니다. 자세한 내용은 [명령줄 도구를 사용하여 구성 서버 설치](http://aka.ms/installconfigsrv)를 참조하세요.


## <a name="common-issues"></a>일반적인 문제

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>다음 단계

다음 단계는 Azure에서 [대상 환경 설정](./site-recovery-prepare-target-physical-to-azure.md)을 포함합니다.
