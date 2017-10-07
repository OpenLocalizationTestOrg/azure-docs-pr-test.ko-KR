---
title: "aaaManage Azure DC/OS 마라톤 UI를 사용한 클러스터 | Microsoft Docs"
description: "Hello 마라톤 웹 UI를 사용 하 여 컨테이너 tooan Azure 컨테이너 서비스 클러스터 서비스를 배포 합니다."
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
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Hello 마라톤 웹 UI 사용 하는 Azure 컨테이너 서비스 DC/OS 클러스터 관리
DC/OS를 배포 및 hello 기본 하드웨어를 추상화 하는 동안 클러스터 된 작업 확장에 대 한 환경을 제공 합니다. DC/OS의 상단에 계산 워크로드의 예약 및 실행을 관리하는 프레임워크가 있습니다.

프레임 워크는 다양 한 인기 있는 작업에 사용할 수 있는,이 문서에서는 tooget 시작 마라톤을 사용 하 여 컨테이너를 배포 하는 방법을 설명 합니다. 


## <a name="prerequisites"></a>필수 조건
이러한 예제를 통해 작업하기 전에 Azure 컨테이너 서비스에 구성된 DC/OS 클러스터가 필요합니다. Toohave 원격 연결 toothis 클러스터도 필요 합니다. 이러한 항목에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [Azure 컨테이너 서비스 클러스터 배포](container-service-deployment.md)
* [Tooan Azure 컨테이너 서비스 클러스터에 연결](../container-service-connect.md)

> [!NOTE]
> 이 문서에서는 toohello DC/OS 클러스터 로컬 포트 80 통해 터널링 할 가정 합니다.
>

## <a name="explore-hello-dcos-ui"></a>DC/OS UI hello 탐색
SSH (보안 셸) 터널와 [설정](../container-service-connect.md), toohttp://localhost/ 찾아보기 합니다. 이 hello DC/OS 웹 UI를 로드 하 고 사용 되는 리소스, 활성 에이전트를 실행 중인 서비스와 같은 hello 클러스터에 대 한 정보를 보여 줍니다.

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Hello 마라톤 UI 탐색
toosee hello 마라톤 UI toohttp://localhost/marathon를 찾습니다. 이 화면에서 hello Azure 컨테이너 서비스 DC/OS 클러스터에서 새 컨테이너 또는 다른 응용 프로그램을 시작할 수 있습니다. 컨테이너 및 응용 프로그램을 실행하는 방법에 대한 정보를 볼 수 있습니다.  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Docker로 포맷된 컨테이너 배포
toodeploy 마라톤을 사용 하 여 새 컨테이너를 클릭 하 여 **응용 프로그램 만들기**, hello hello 양식 탭에 다음 정보를 입력 합니다.

| 필드 | 값 |
| --- | --- |
| ID |nginx |
| 메모리 | 32 |
| 이미지 |nginx |
| 네트워크 |Bridged |
| 호스트 포트 |80 |
| 프로토콜 |TCP |

![새 응용 프로그램 UI--일반](./media/container-service-mesos-marathon-ui/dcos4.png)

![새 응용 프로그램 UI--Docker 컨테이너](./media/container-service-mesos-marathon-ui/dcos5.png)

![새 응용 프로그램 UI--포트 및 서비스 검색](./media/container-service-mesos-marathon-ui/dcos6.png)

Toostatically hello 컨테이너 포트 tooa 포트 매핑 hello 에이전트에서 원하는 경우 toouse JSON 모드 해야 합니다. toodo 따라서 전환 hello 새 응용 프로그램 마법사 너무**JSON 모드** hello 설정/해제를 사용 하 여 합니다. Hello hello에서 설정은 다음에 enter `portMappings` hello 응용 프로그램 정의의 섹션입니다. 이 예에서는 hello DC/OS 에이전트의 hello 컨테이너 tooport 80의 포트 80을 바인딩합니다. 이렇게 변경한 후에 이 마법사를 JSON 모드에서 해제할 수 있습니다.

```none
"hostPort": 80,
```

![새 응용 프로그램 UI--포트 80 예제](./media/container-service-mesos-marathon-ui/dcos13.png)

Tooenable 상태 검사를 하려는 경우 hello에 경로 설정 **상태 검사** 탭 합니다.

![새 응용 프로그램 UI--상태 검사](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

hello DC/OS 클러스터는 개인 및 공용 에이전트 집합을 함께 배포 됩니다. Hello 클러스터 toobe 수 tooaccess 응용 프로그램에서 인터넷 hello toodeploy hello 응용 프로그램 tooa 공용 에이전트가 필요합니다. toodo hello를 따라서 선택 **옵션** hello 새 응용 프로그램 마법사의 탭 하 고 입력 **slave_public** hello에 대 한 **리소스 역할 수락**합니다.

그런 다음 **응용 프로그램 만들기**를 클릭합니다.

![새 응용 프로그램 UI--공용 에이전트 설정](./media/container-service-mesos-marathon-ui/dcos14.png)

Hello 마라톤 기본 페이지에서 다시 hello 컨테이너에 대 한 hello 배포 상태를 볼 수 있습니다. 처음에는 **배포 중** 상태가 표시됩니다. 배포 된 후 상태를 변경할 수을 너무 hello**실행**합니다.

![Marathon 기본 페이지 UI--컨테이너 배포 상태](./media/container-service-mesos-marathon-ui/dcos7.png)

뒤로 toohello DC/OS 웹 UI http://localhost/ 전환 하면 hello DC/OS 클러스터에서 작업 (이 경우 Docker로 포맷 된 컨테이너)에 실행 되 고 있는지 볼 수 있습니다.

![DC/OS 웹 UI-hello 클러스터에서 실행 중인 작업](./media/container-service-mesos-marathon-ui/dcos8.png)

실행 되 고 작업을 hello toosee hello 클러스터 노드를 hello 클릭 **노드** 탭 합니다.

![DC/OS 웹 UI--작업 클러스터 노드](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Hello 컨테이너에 도달

이 예제에서는 공용 에이전트 노드에서 hello 응용 프로그램 실행 중입니다. Hello에서 hello 응용 프로그램에 도달 하면 toohello hello 클러스터의 에이전트를 검색 하 여 인터넷: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, 여기서:

* **DNSPREFIX** hello 클러스터를 배포할 때 제공 하는 hello DNS 접두사입니다.
* **지역** 리소스 그룹의 위치를 가리키는 hello 영역입니다.

    ![인터넷의 Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>다음 단계
* [DC/OS를 사용 하 고 hello 마라톤 API](container-service-mesos-marathon-rest.md)

* Azure 컨테이너 서비스 Mesos hello에 대 한 고찰

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
