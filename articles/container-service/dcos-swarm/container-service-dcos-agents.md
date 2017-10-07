---
title: "Azure 컨테이너 서비스에 대 한 에이전트 풀 aaaDC/OS | Microsoft Docs"
description: "Azure 컨테이너 서비스 DC/OS 클러스터와 함께 hello 공용 및 개인 에이전트 풀을 작동 하는 방식"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Azure Container Service의 DC/OS 에이전트 풀
Azure Container Service의 DC/OS 클러스터는 2개의 풀, 즉 공용 풀과 개인 풀에 에이전트 노드를 포함합니다. 응용 프로그램을 배포할 수 있습니다 컨테이너 서비스의 컴퓨터 간에 내게 필요한 옵션에 영향을 주는 tooeither 풀입니다. hello 컴퓨터 수 있는 노출 된 toohello 인터넷 (공용) 또는 내부 (개인)을 유지 합니다. 이 문서에서는 공용 및 개인 풀이 있는 이유에 대한 간략한 개요를 제공합니다.


* **개인 에이전트**: 개인 에이전트 노드는 라우팅할 수 없는 네트워크를 통해 실행됩니다. 이 네트워크는 hello 관리 영역에서 또는 hello 공용 영역에 지 라우터를 통해에 액세스할 수 있습니다. 기본적으로 DC/OS는 사용자 에이전트 노드에서 앱을 시작합니다. 

* **공용 에이전트**: 공용 에이전트 노드는 공개적으로 액세스 가능한 네트워크를 통해 DC/OS 앱과 서비스를 실행합니다. 

DC/OS 네트워크 보안에 대 한 자세한 내용은 참조 hello [DC/OS 문서](https://dcos.io/docs/1.7/administration/securing-your-cluster/)합니다.

## <a name="deploy-agent-pools"></a>에이전트 풀 배포

hello DC/OS 에이전트 풀 Azure 컨테이너 서비스는 다음과 같이 생성 됩니다.

* hello **개인 풀** hello 시점을 지정 하는 에이전트 노드 수가 포함 되어 있습니다 [hello DC/OS 클러스터 배포](container-service-deployment.md)합니다. 

* hello **공용 풀** 처음에 미리 결정 된 에이전트 노드 수가 포함 되어 있습니다. 이 풀은 hello DC/OS 클러스터 프로 비전 될 때 자동으로 추가 됩니다.

hello 개인 풀과 hello 공용 풀은 Azure 가상 컴퓨터 크기 집합입니다. 배포 후 이러한 풀의 크기를 조정할 수 있습니다.

## <a name="use-agent-pools"></a>에이전트 풀 사용
기본적으로 **마라톤** 모든 새 응용 프로그램 toohello 배포 *개인* 에이전트 노드. 배포 응용 프로그램 toohello hello tooexplicitly 있는 *공용* 노드 hello hello 응용 프로그램을 만드는 중입니다. 선택 hello **Optional** 탭 하 고 입력 **slave_public** hello에 대 한 **리소스 역할 수락** 값입니다. 이 과정은 문서화 되어 [여기](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 및 hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) 설명서입니다.

## <a name="next-steps"></a>다음 단계
* [DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)에 대해 자세히 알아보세요.

* 너무 방법에 대해 알아봅니다[hello 방화벽을 열고](container-service-enable-public-access.md) Azure tooallow 공용 액세스 tooyour DC/OS 컨테이너에서 제공 합니다.

