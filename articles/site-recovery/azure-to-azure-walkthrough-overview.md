---
title: "Azure 지역 간에 Azure Vm aaaReplicate | Microsoft Docs"
description: "Hello 단계 필요한 tooreplicate를 Azure Vm hello Azure 포털에서에서 hello Azure Site Recovery 서비스와 Azure 지역 간 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Azure Site Recovery를 사용하여 지역 간 Azure VM 복제

>이 문서에서는 Azure 지역 tooAzure 다른 지역에 Vm에서에서 Azure 가상 컴퓨터 (Vm) hello 단계 필요한 tooreplicate의 개요를 제공 합니다. 

>[!NOTE]
>
> Azure VM 복제는 현재 미리 보기로 제공됩니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="step-1-review-architecture"></a>1단계: 아키텍처 검토

배포를 시작 하기 전에 hello 시나리오 아키텍처 및 toodeploy 필요한 hello 구성 요소를 검토 합니다.

너무 이동[1 단계: hello 아키텍처 검토](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2단계: 필수 구성 요소 검토

구독, 가상 네트워크, 저장소 계정 및 VM 요구 사항을 비롯 한 위치에서 필수 구성 요소를 Azure에 hello가 있는지 확인 하십시오.

너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>3단계: 네트워킹 계획

아웃 바운드 연결 tooreplicate, 온-프레미스에서 연결 설정 하 고 원하는 Azure Vm에 설치 되어 있는지 확인 합니다.

너무 이동[4 단계: 네트워킹 계획](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>4단계: 자격 증명 모음 만들기 

복제를 관리 하며 hello 소스 지역을 지정 복구 서비스 자격 증명 모음 tooorchestrate tooset 필요 합니다.

너무 이동[4 단계: 자격 증명 모음 만들기](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>5단계: 복제 사용


tooenable 복제 대상 위치 설정을 구성 하 고 복제 정책을 설정한 tooreplicate 원하는 hello Azure Vm을 선택 합니다. 를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.

너무 이동[5 단계: 복제 사용](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>6단계: 테스트 장애 조치 실행

초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.

너무 이동[6 단계: 테스트 장애 조치 실행](azure-to-azure-walkthrough-test-failover.md)


