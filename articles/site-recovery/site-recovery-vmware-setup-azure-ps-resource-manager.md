---
title: " Azure(Resource Manager)에서 실행되는 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 Azure에서 한 장애 복구를 tooset (리소스 관리자)를 처리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Azure에서 실행되는 프로세스 서버 관리(Resource Manager)
> [!div class="op_single_selector"]
> * [리소스 관리자](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [클래식](./site-recovery-vmware-setup-azure-ps-classic.md)

장애 복구 하는 동안 좋습니다 toodeploy 프로세스 서버가 Azure의 hello Azure 가상 네트워크와 온-프레미스 네트워크 간의 대기 시간이 긴 경우. 이 문서에서는 설정, 구성 하는 방법을 hello 프로세스 서버를 Azure에서 실행 중인 관리를 설명 합니다.

> [!NOTE]
> 이 문서는 사용 하는 경우 사용 되는 toobe **리소스 관리자** hello 가상 컴퓨터 장애 조치 중에 대 한 hello 배포 모델로 합니다. 사용 하는 경우 **클래식** hello 배포 모델로 hello 단계에 따라 [어떻게 tooset 위로 및 장애 복구 (클래식) 프로세스 서버를 구성 합니다.](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>필수 조건

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Azure에 프로세스 서버 배포
1. Hello 자격 증명 모음에서에서 > **사이트 복구 인프라** (아래 hello "Manage") > **구성 서버** (아래에서 "컴퓨터에 대 한 VMware 및 물리적" 제목) hello 구성 서버를 선택 합니다.
2. 열리는 hello 구성 서버 세부 정보 페이지에서 클릭 "+ 서버 프로세스"

  ![프로세스 서버 갤러리 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Hello에 **추가 프로세스 서버** 페이지에서 다음 값에는 선택 hello

  ![프로세스 서버 갤러리 항목 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**필드 이름**|**값**|
|-|-|
|저장할 toodeploy 프로세스 서버 선택|Hello 값 선택 **Azure의 장애 복구 프로세스 서버 배포** |
|구독|Hello 장애 조치 hello 가상 컴퓨터를 Azure 구독 선택|
|리소스 그룹|기존 리소스 그룹에서 toodeploy hello 프로세스 서버를 선택 하거나 리소스 그룹 toodeploy이 프로세스 서버를 만들 수 있습니다.|
|위치|Hello Azure 데이터 센터는 hello 가상 컴퓨터를 선택으로 장애 조치 하는 경우|
|Azure 네트워크|가상 컴퓨터를 hello Azure 가상 Network(VNet) 선택 hello에 장애 조치를 합니다. 가상 컴퓨터를 여러 Azure Vnet으로 장애 조치한 경우 VNet마다 배포된 프로세스 서버가 있어야 합니다.|

4. 프로세스 서버 hello에 대 한 hello 속성 hello 나머지를 입력 합니다.

  ![프로세스 서버 요약 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**필드 이름**|**값**|
|-|-|
|서버 이름|프로세스 서버 가상 컴퓨터에 대한 표시 이름/호스트 이름|
| 사용자 이름|해당 가상 컴퓨터에서 관리자가 되는 사용자 이름|
|저장소 계정|hello hello 가상 컴퓨터의 가상 디스크의 위치는 저장소 계정 이름|
|서브넷|hello Azure VNet toowhich hello 가상 컴퓨터의 hello 서브넷 연결|
| IP 주소|싶다는 의사를 hello 프로세스 서버 tooassume 부팅 되 면 IP 주소|
5. Hello 확인 단추 toostart hello 프로세스 서버 가상 컴퓨터 배포를 클릭 합니다.

> [!NOTE]
> toobe 수 toouse이 프로세스 서버 tooregister 해야 장애 복구를 사용 하 여 hello 온-프레미스 구성 서버입니다.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Hello 프로세스 서버 (Azure에서 실행) tooa (온-프레미스로 실행) 구성 서버를 등록 하는 중

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Hello 프로세스 서버 toolatest 버전을 업그레이드 합니다.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>구성 서버 (온-프레미스로 실행)에서 (Azure에서 실행) 하는 hello 프로세스 서버를 등록 취소

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
