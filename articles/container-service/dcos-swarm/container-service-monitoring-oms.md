---
title: "aaaMonitor Azure DC/OS 클러스터 운영 관리 | Microsoft Docs"
description: "Microsoft Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터를 모니터링합니다."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터 모니터링

OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. 컨테이너에서 hello 컨테이너 인벤토리 보기, 성능 및 단일 위치에 있는 로그를 사용 하면 OMS 로그 분석 솔루션을 합니다. 감사, 중앙된 위치에 hello 로그를 확인 하 여 컨테이너 문제 해결 및 사용 과다 컨테이너 호스트에 잡음이 있는 확인할 수 있습니다.

![](media/container-service-monitoring-oms/image1.png)

컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Hello DC/OS universe에서 OMS를 설정합니다.


이 문서에서는 DC/OS를 설정 하 고 간단한 웹 컨테이너 응용 프로그램에서는 hello 클러스터에 배포 하는 가정 합니다.

### <a name="pre-requisite"></a>필수 구성 요소
- [Microsoft Azure 구독](https://azure.microsoft.com/free/) - 무료로 다운로드할 수 있습니다.  
- Microsoft OMS 작업 영역 설치 - 아래 "3단계" 참조
- [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) 설치

1. Hello DC/OS 대시보드에서 Universe 및 아래와 같이 'OMS'에 대 한 검색을 클릭 합니다.

![](media/container-service-monitoring-oms/image2.png)

2. **Install**을 클릭합니다. Pop를 hello OMS 버전 정보와 함께 표시 됩니다는 및 **패키지 설치** 또는 **고급 설치** 단추입니다. 클릭할 때 **고급 설치**, toohello 안내는 **OMS 어댑터별 구성 속성** 페이지.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. 여기에서는 묻는 tooenter hello `wsid` (hello OMS 작업 영역 ID) 및 `wskey` (hello OMS 기본 키 hello 작업 영역 id에 대 한). 두 tooget `wsid` 및 `wskey` toocreate OMS 계정에 필요한 <https://mms.microsoft.com>합니다. Hello 단계 toocreate 계정을 수행 하십시오. Tooobtain hello 계정 만들기를 완료 해야 사용자 `wsid` 및 `wskey` 클릭 하 여 **설정**, 다음 **연결 된 원본**, 차례로 **Linux 서버** 다음과 같이 합니다.

 ![](media/container-service-monitoring-oms/image5.png)

4. 인스턴스를 선택 hello 숫자 하면 OMS 고 hello '검토 하 고 설치' 단추를 클릭 합니다. 일반적으로 toohave hello 수가 VM 에이전트 클러스터에 있는 수가 인스턴스 같은 toohello OMS 해야 합니다. Linux 용 OMS 에이전트 toocollect 모니터링 정보와 로깅 정보 브로드캐스트하며 각 VM에서 개별 컨테이너로 설치 됩니다.

## <a name="setting-up-a-simple-oms-dashboard"></a>간단한 OMS 대시보드 설정

Hello Vm에 Linux 용 OMS 에이전트 hello를 설치한 후 다음 단계를 OMS 대시보드에 hello tooset입니다. 두 가지 방법으로 toodo이: OMS 포털 또는 Azure 포털입니다.

### <a name="oms-portal"></a>OMS 포털 

Toohello OMS 포털에 로그인 (<https://mms.microsoft.com>) toohello 이동 **솔루션 갤러리**합니다.

![](media/container-service-monitoring-oms/image6.png)

Hello에 있는 경우 **솔루션 갤러리**선택, **컨테이너**합니다.

![](media/container-service-monitoring-oms/image7.png)

Hello 컨테이너 솔루션을 선택한 후 hello 타일 hello OMS 개요 대시보드 페이지에 표시 됩니다. 수집 된 hello 컨테이너 데이터는 인덱싱된 나타납니다 hello 타일 솔루션 보기 타일에 대 한 정보로 채워집니다.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure 포털 

TooAzure 포털에 로그인 <https://portal.microsoft.com/>합니다. **마켓플레이스**로 이동하고 **모니터링 + 관리**를 선택한 다음 **모두 표시**를 클릭합니다. 그런 다음 검색 상자에서 `containers`를 입력합니다. "컨테이너" hello 검색 결과에 표시 됩니다. **컨테이너**를 선택하고 **만들기**를 클릭합니다.

![](media/container-service-monitoring-oms/image9.png)

**만들기**를 클릭하면 작업 영역을 묻습니다. 작업 영역을 선택하거나 작업 영역이 없는 경우 새 작업 영역을 만듭니다.

![](media/container-service-monitoring-oms/image10.PNG)

작업 영역을 선택했으면 **만들기**를 클릭합니다.

![](media/container-service-monitoring-oms/image11.png)

Hello OMS 컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>어떻게 tooscale OMS 에이전트와 ACS DC/OS 

Hello 실제 노드 수 부족 toohave 설치 된 OMS 에이전트 필요 하거나 더 많은 VM을 추가 하 여 VMSS를 크기 조정, 후 그렇게 hello를 확장 하 여 `msoms` 서비스입니다.

TooMarathon 또는 hello DC/o S I c e s 탭으로 이동 수 있으며 노드 수를 확장할 수도 있습니다.

![](media/container-service-monitoring-oms/image12.PNG)

Hello OMS 에이전트를 아직 배포 하지 않은 tooother 노드인을 배포 합니다.

## <a name="uninstall-ms-oms"></a>MS OMS 제거

MS OMS toouninstall hello 다음 명령을 입력 합니다.

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>알려주세요!!!
무슨 일입니까? 무엇이 필요합니까? 다른 작업 필요 한가요이 toobe에 대 한 유용한 드립니다? <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>에 알려주세요.

## <a name="next-steps"></a>다음 단계

 설정한 후 OMS toomonitor 컨테이너, 했으므로[컨테이너 대시보드](../../log-analytics/log-analytics-containers.md)합니다.
