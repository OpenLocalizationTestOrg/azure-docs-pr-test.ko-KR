---
title: "aaaHow는 Azure 사이트 복구에서 수행 되는 Azure 지역 작업 간 Azure 가상 컴퓨터 복제 합니까?  | Microsoft Docs"
description: "이 문서에서는 구성 요소와 hello Azure Site Recovery 서비스를 사용 하 여 Azure 지역 간에 Azure Vm을 복제할 때 사용 되는 아키텍처의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Site Recovery에서 Azure VM 복제가 작동하는 방식


이 문서에서는 hello 구성 요소 및 프로세스를 설명 hello를 사용 하 여 tooanother 한 지역에서에서 복제 하 고 Azure 가상 컴퓨터 (Vm) 복구에 관련 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

>[!NOTE]
>Azure VM 복제 hello Site Recovery 서비스를 현재 미리 보기 중입니다.

이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="architectural-components"></a>아키텍처 구성 요소

hello 다음 다이어그램은 높은 수준의 (이 예에서는 hello 미국 동부 위치)에 특정 지역에서 Azure VM 환경 제공 합니다. Azure VM 환경은 다음과 같습니다.
- 앱은 여러 저장소 계정에 디스크가 분산되어 있는 VM에서 실행될 수 있습니다.
- hello Vm 가상 네트워크 내에서 하나 이상의 서브넷에 포함 될 수 있습니다.

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Hello 배포 필수 구성 요소 및 hello에 대 한 요구 사항을 알아봅니다 [지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)합니다.

## <a name="replication-process"></a>복제 프로세스

### <a name="step-1"></a>1단계

Hello Azure 포털에서에서 Azure VM 복제를 사용 하도록 설정 하면 hello 리소스 hello 뒤에 표시 된 다이어그램과 테이블에 자동으로 hello 대상 지역에 만들어집니다. 기본적으로 리소스는 원본 지역 설정을 기반으로 만들어집니다. 필요에 따라 hello 대상 설정을 사용자 지정할 수 있습니다. [자세히 알아봅니다](site-recovery-replicate-azure-to-azure.md).

![복제를 사용하도록 설정하는 프로세스, 1단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

**리소스** | **세부 정보**
--- | ---
**대상 리소스 그룹** | 복제 된 Vm 장애 조치 후 속한 리소스 그룹 toowhich를 hello 합니다.
**대상 가상 네트워크** | 복제 된 Vm이 있는 장애 조치 후 가상 네트워크를 hello입니다. 네트워크 매핑은 원본 및 대상 가상 네트워크 간에 만들어집니다.
**캐시 저장소 계정** | Vm이 원본에 대 한 변경 내용을 복제 toohello 대상 저장소 계정, 하기 전에 추적 되며 toohello 캐시 저장소 계정 hello 대상 위치에 전송 됩니다. 이렇게 하면 hello VM에서 실행 되는 프로덕션 응용 프로그램에 미치는 영향을 최소화 합니다.
**대상 저장소 계정**  | Hello 대상 위치 toowhich hello 데이터의 저장소 계정 복제 됩니다.
**대상 가용성 집합**  | 가용성을 복제 하는 hello Vm 있는 장애 조치 후에 설정 합니다.

### <a name="step-2"></a>2단계

복제를 사용 하는 hello 사이트 복구 확장 모바일 서비스는 hello VM에 자동으로 설치 됩니다. hello 다음 작업이 수행 됩니다.

1. hello VM Site Recovery에 등록 됩니다.

2. 연속 복제 hello VM에 대해 구성 됩니다. 데이터 디스크는 지속적으로 hello VM에서 쓰는 toohello 캐시 저장소 계정 hello 원본 위치에 전송 합니다.

   ![복제를 사용하도록 설정하는 프로세스, 2단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > 사이트 복구는 인바운드 연결 toohello VM 하지 필요합니다. hello VM 아웃 바운드 연결 tooSite 복구 서비스 Url/IP 주소, Office 365 인증 Url/IP 주소 및 캐시 저장소 계정 IP 주소가 필요합니다. 자세한 내용은 참조 hello [Azure 가상 컴퓨터 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md) 문서.

## <a name="continuous-replication-process"></a>연속 복제 프로세스

연속 복제를 작동 한 후 즉시. 쓰기는 디스크 전송 toohello 캐시 저장소 계정. 사이트 복구 hello 데이터를 처리 하 고 대상 저장소 계정과 toohello 보냅니다. Hello 데이터를 처리 한 후에 몇 분 마다으로 hello 대상 저장소 계정에서 복구 지점이 생성 됩니다.

## <a name="failover-process"></a>장애 조치(failover) 프로세스

장애 조치를 시작할 때 hello 대상 리소스 그룹, 대상 가상 네트워크, 대상 서브넷에 Vm 만들어집니다 hello 및 hello 대상 가용성 집합. 장애 조치(failover) 중에는 모든 복구 지점을 사용할 수 있습니다.

![장애 조치(failover) 프로세스](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>다음 단계

- Azure VM 복제를 위한 [네트워킹](site-recovery-azure-to-azure-networking-guidance.md)에 대해 알아보세요.
- 너무 연습에 따라[Azure Vm을 복제 합니다.](site-recovery-azure-to-azure.md)
