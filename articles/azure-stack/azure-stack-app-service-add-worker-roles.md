---
title: "Azure 스택 앱 서비스-에 작업자 역할을 수평적 | Microsoft Docs"
description: "Azure 스택 앱 서비스를 크기 조정 하기 위한 세부 지침"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/10/2017
ms.author: anwestg
ms.openlocfilehash: 30ab325488684a26a6ef442e7c8241526a66aa4c
ms.sourcegitcommit: ccb84f6b1d445d88b9870041c84cebd64fbdbc72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2017
---
# <a name="app-service-on-azure-stack-add-more-infrastructure-or-worker-roles"></a>Azure 스택 앱 서비스: 더 많은 인프라 또는 작업자 역할 추가

이 문서에서는 Azure 스택 인프라 및 작업자 역할에서 응용 프로그램 서비스를 확장 하는 방법에 대 한 지침을 제공 합니다. 모든 규모의 응용 프로그램을 지원 하도록 추가 작업자 역할을 만들기 위한 단계를 포함 합니다.

> [!NOTE]
> Azure 스택 환경에 없는 경우 96 g B RAM 이상 문제가 용량 추가 할 수 있습니다.

기본적으로 Azure 스택 앱 서비스는 무료 및 공유 작업자 계층을 지원합니다. 다른 작업자 계층을 추가 하려면 다른 작업자 역할을 추가 해야 합니다.

Azure 스택 설치에서 기본 응용 프로그램 서비스와 함께 배포 된 내용을 확실 하지 않은 경우의 추가 정보를 검토할 수 있습니다는 [개요 Azure 스택 앱 서비스](azure-stack-app-service-overview.md)합니다.

Azure 스택 앱 서비스를 azure 가상 컴퓨터 크기 집합을 사용 하 여 모든 역할 하 고 따라서는이 작업의 크기 조정 기능 이용 합니다. 따라서 응용 프로그램 서비스 관리자를 통해 수행 됩니다 작업자 계층의 모든 크기 조정

앱 서비스 리소스 공급자 관리자 내에서 직접 추가 작업자 추가

1. 서비스 관리자로 Azure 스택 관리 포털에 로그인 합니다.

2. 찾아 **응용 프로그램 서비스**합니다.

    ![](media/azure-stack-app-service-add-worker-roles/image01.png)
  
3. **역할**을 클릭합니다. 여기에 배포 된 모든 앱 서비스 역할의 분석 결과 볼 있습니다.

4. 확장 하 고 클릭 한 다음 원하는 종류의 행을 마우스 오른쪽 단추로 클릭 **ScaleSet**합니다.

    ![](media/azure-stack-app-service-add-worker-roles/image02.png)
  
5. 클릭 **배율**, 선택, 크기를 조정 하 고 클릭 하려는 인스턴스의 수 **저장**합니다.
    
    ![](media/azure-stack-app-service-add-worker-roles/image03.png)

6. Azure 스택 앱 서비스는 이제 추가 Vm 추가, 구성, 모든 필수 소프트웨어를 설치 및이 프로세스가 완료 되 면 준비로 표시 합니다. 이 프로세스는 약 80 분 걸릴 수 있습니다.

7. 근로자에 게 확인 하 여 새 역할의 준비의 진행 상황을 모니터링할 수 있습니다는 **역할** 블레이드입니다.

이들이 완전히 하 게 배포 하 고, 작업 자가 레이어로 프로그램 작업을 배포 하는 사용자에 대해 사용할 수 있습니다. 다음 기본적으로 사용할 수 있는 여러 가격 책정 계층의 예를 보여줍니다. 특정 작업자 계층에 대 한 사용 가능한 자가 있는지, 해당 가격 책정 계층을 선택할 수 있는 옵션 ´ ù입니다.

![](media/azure-stack-app-service-add-worker-roles/image04.png)

>[!NOTE]
> 프런트 엔드 또는 게시자 역할 관리를 확장 하려면 해당 VM 크기 집합 수평 확장 해야 합니다를 추가 합니다. 이후 버전에서 응용 프로그램 서비스 관리를 통해 이러한 역할을 확장할 수 있는 기능을 추가 합니다.

관리, 프런트 엔드 또는 게시자 역할을 확장 하려면 적절 한 역할 유형을 선택한 후 동일한 단계를 따릅니다. 컨트롤러 크기 집합으로 배포 되지 않습니다 및 따라서 두 으로만 모든 프로덕션 배포에 대 한 설치 시간에 있습니다.

### <a name="next-steps"></a>다음 단계

[배포 소스 구성](azure-stack-app-service-configure-deployment-sources.md)
