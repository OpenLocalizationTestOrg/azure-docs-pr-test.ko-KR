---
title: "Azure 컨테이너 서비스 aaaMonitor Sysdig 포함 하는 클러스터 | Microsoft Docs"
description: "Sysdig을 사용하여 Azure 컨테이너 서비스 클러스터를 모니터링합니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Sysdig을 사용하여 Azure 컨테이너 서비스 클러스터를 모니터링합니다.
이 문서에서는 Azure 컨테이너 서비스 클러스터의 Sysdig 에이전트 tooall hello 에이전트 노드를 배포 합니다. 이러한 구성을 위해서는 Sysdig 계정이 필요합니다. 

## <a name="prerequisites"></a>필수 조건
Azure Container Service를 통해 구성된 클러스터를 [배포](container-service-deployment.md) 및 [연결](../container-service-connect.md)합니다. Hello 탐색 [마라톤 UI](container-service-mesos-marathon-ui.md)합니다. 너무 이동[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig 클라우드 계정. 

## <a name="sysdig"></a>Sysdig
Sysdig toomonitor 수 있는 모니터링 서비스는 클러스터 내에 컨테이너입니다. Sysdig toohelp 문제 해결에 알려져 있는 하지만 CPU, 네트워킹, 메모리 및 I/O에 대 한 기본 모니터링 메트릭에서 프로그램 있습니다. Sysdig 쉽게 toosee 작업 하는 컨테이너를 사용 하면 대부분의 메모리와 CPU를 집중 또는 기본적으로 사용 하 여 hello hello 합니다. 이 보기는 hello 현재 베타 중인 "개요" 항목의에서 합니다. 

![Sysdig UI](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Marathon으로 Sysdig 배포 구성
이러한 단계는 방법을 보여 줍니다 tooconfigure Sysdig 마라톤을 사용 하는 응용 프로그램 tooyour 클러스터를 배포 합니다. 

DC/OS UI를 통해 액세스 [http://localhost:80 /](http://localhost:80/) 한 번 hello DC/OS UI에서에서 toohello "Universe" hello에 왼쪽 아래로 한 다음 "Sysdig"에 대 한 검색을 이동

![DC/OS Universe에서 Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

Sysdig 필요한 toocomplete hello 구성 이제 계정 또는 무료 평가판 계정을 클라우드입니다. Toohello Sysdig 클라우드 웹 사이트를 로그인 후 사용자 이름을 클릭 하 고 "액세스 키입니다." hello 페이지에 표시 됩니다. 

![Sysdig API 키](./media/container-service-monitoring-sysdig/sysdig2.png) 

그런 다음 hello Sysdig 구성 hello DC/OS Universe 내에 자신의 액세스 키를 입력 합니다. 

![DC/OS Universe hello에 Sysdig 구성](./media/container-service-monitoring-sysdig/sysdig3.png)

이제 hello 인스턴스 too10000000 toohello 클러스터 Sysdig 에이전트에서 자동으로 배포에 새 노드를 추가할 때마다 하므로 toothat 새 노드를 설정 합니다. 이는 중간 솔루션이 toomake Sysdig tooall hello 클러스터 내에서 새 에이전트를 배포 합니다. 

![DC/OS Universe-인스턴스 hello에 Sysdig 구성](./media/container-service-monitoring-sysdig/sysdig4.png)

Hello 패키지를 설치한 다음 백 toohello Sysdig UI 이동한 수 tooexplore hello 다른 사용 메트릭을 hello 컨테이너에 대 한 클러스터 수 있습니다. 

[새 대시보드 마법사](https://app.sysdigcloud.com/#/dashboards/new)를 통해 Mesos 및 Marathon 지정 대시보드를 설치할 수도 있습니다.
