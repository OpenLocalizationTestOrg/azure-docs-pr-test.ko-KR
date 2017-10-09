---
title: "aaaMonitor Azure DC/OS 클러스터 Dynatrace | Microsoft Docs"
description: "Dynatrace를 사용하여 Azure Container Service DC/OS 클러스터를 모니터링합니다. Hello DC/OS 대시보드를 사용 하 여 hello Dynatrace OneAgent를 배포 합니다."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed를 사용하여 Azure Container Service DC/OS 클러스터 모니터링
이 문서에서는 보여줍니다 어떻게 toodeploy hello [Dynatrace](https://www.dynatrace.com/) 모든 OneAgent toomonitor hello Azure 컨테이너 서비스 클러스터의 에이전트 노드. 이러한 구성을 위해서는 Dynatrace SaaS/Managed 계정이 필요합니다. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed
Dynatrace는 매우 동적인 컨테이너 및 클러스터 환경을 위한 클라우드 네이티브 모니터링 솔루션입니다. 있습니다 toobetter 실시간 사용 현황 데이터를 사용 하 여 컨테이너 배포 및 메모리 할당을 최적화 합니다. 자동화된 기준 지정, 문제 상관 관계 및 근본 원인 검색을 제공하여 응용 프로그램 및 인프라 문제를 자동으로 파악할 수 있습니다.

hello 다음 그림에서는 hello Dynatrace UI 수 있습니다.

![Dynatrace UI](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>필수 조건 
[배포](container-service-deployment.md) 및 [연결](./../container-service-connect.md) tooa 클러스터 Azure 컨테이너 서비스에서 구성 합니다. Hello 탐색 [마라톤 UI](container-service-mesos-marathon-ui.md)합니다. 너무 이동[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS 계정.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Marathon으로 Dynatrace 배포 구성
이러한 단계 tooconfigure Dynatrace 마라톤을 사용 하는 응용 프로그램 tooyour 클러스터를 배포 합니다.

1. [http://localhost:80/](http://localhost:80/)을 통해 DC/OS UI에 액세스합니다. 한 번 hello DC/OS UI, toohello 이동 **Universe** 탭 한 다음 검색 **Dynatrace**합니다.

    ![DC/OS Universe의 Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. toocomplete hello 구성 Dynatrace SaaS 계정 또는 무료 평가판 계정을 해야합니다. Hello Dynatrace 대시보드에 로그인 선택 **배포 Dynatrace**합니다.

    ![Dynatrace PaaS 통합 설정](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Hello 페이지에서 선택 **PaaS 통합 설정**합니다. 

    ![Dynatrace API 토큰](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Hello Dynatrace OneAgent 구성 hello DC/OS Universe 내에 API 토큰을 입력 합니다. 

    ![DC/OS Universe hello에 Dynatrace OneAgent 구성](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Hello 인스턴스 toohello 수를 설정 하려는 toorun 노드. 설정 값이 클수록도 작동 하지만 DC/OS 계속 시도 합니다 toofind 새 인스턴스가 실제로 해당 수에 도달할 때까지 합니다. 원하는 경우 1000000 같은이 tooa 값을 설정할 수도 있습니다. 이 경우 새 노드 toohello 클러스터를 추가할 때마다 Dynatrace는 에이전트 toothat 새 노드를 지속적으로 toodeploy 추가 인스턴스를 시도 DC/OS의 hello 가격으로 자동으로 배포 합니다.

    ![DC/OS Universe-인스턴스 hello에 Dynatrace 구성](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>다음 단계

Hello 패키지를 설치한 다음 백 toohello Dynatrace 대시보드를 탐색 합니다. Hello 컨테이너에 대 한 다른 사용 메트릭을 hello 클러스터 내에서 탐색할 수 있습니다. 
