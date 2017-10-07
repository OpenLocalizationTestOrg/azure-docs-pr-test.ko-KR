---
title: "aaaAzure 서비스 패브릭 컨테이너 모니터링 및 진단 | Microsoft Docs"
description: "자세한 방법을 toomonitor OMS의 컨테이너 솔루션으로 Microsoft Azure 서비스 패브릭에서 조정 하는 컨테이너를 진단 하 고 있습니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>OMS를 사용하여 Windows Server 컨테이너 모니터링

## <a name="oms-containers-solution"></a>OMS 컨테이너 솔루션

hello Operations Management Suite (OMS) 팀은 컨테이너에 대 한 모니터링 및 진단에 대 한 컨테이너 솔루션에 게시 됩니다. 해당 서비스 패브릭 솔루션과 함께이 솔루션에는 서비스 패브릭에서 조정 하는 좋은 도구 toomonitor 컨테이너 배포입니다. 다음과 같은 hello 대시보드 hello 솔루션에서의 간단한 예는 다음과 같습니다.

![기본 OMS 대시보드](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

또한 다른 종류의 hello OMS 로그 분석 도구에서 쿼리할 수 있는 로그를 수집 및 메트릭 또는 생성 되 고 이벤트 사용된 toovisualize 수 있습니다. hello 로그 수집 되는 유형은 다음과 같습니다.

1. ContainerInventory: 컨테이너 위치, 이름 및 이미지에 대한 정보를 표시합니다.
2. ContainerImageInventory: ID 또는 크기를 포함하여 배포된 이미지에 대한 정보를 표시합니다.
3. ContainerLog: 특정 오류 로그, docker 로그(stdout 등) 및 기타 항목을 표시합니다.
4. ContainerServiceLog: 실행된 docker 디먼 명령을 표시합니다.
5. 성능: 성능 카운터 컨테이너를 포함 하 여 cpu, 메모리, 네트워크 소통량, 디스크 i/o 및 컴퓨터를 호스트 하는 hello에서 사용자 지정 메트릭

이 문서에서는 hello 단계 필요한 tooset 클러스터에 대 한 모니터링 하는 컨테이너를 설명 합니다. OMS의 컨테이너 솔루션에 대 한 자세한 toolearn 체크 아웃의 [설명서](../log-analytics/log-analytics-containers.md)합니다.

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Service Fabric 클러스터 설정

Hello Azure 리소스 관리자 템플릿을 사용 하 여 클러스터 만들기 [여기](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample)합니다. 고유한 OMS 작업 영역 이름을 tooadd 있는지를 확인 합니다. 이 서식 파일에는 toodeploying hello 미리 보기에 있는 클러스터 빌드 서비스 패브릭 (v255.255) 프로덕션 환경에서 사용할 수 없습니다 하며 수는 없습니다 것을 의미 하는 다른 서비스 패브릭 버전 tooa 업그레이드의 기본 설정 됩니다. 이 서식 파일에 대 한 toouse 결정 한 경우 장기 또는 프로덕션으로 hello 버전 tooa 안정적인 버전 번호를 변경 합니다.

Hello 클러스터 설정 되 고 나면 확인 hello 적절 한 인증서를 설치 하 고 수 tooconnect toohello 클러스터 되는지 확인 합니다.

머리글 toohello 하 여 리소스 그룹이 올바르게 설정 되어 확인 [Azure 포털](https://portal.azure.com/) 및 찾기 hello 배포 합니다. hello 리소스 그룹 모든 hello 서비스 패브릭 리소스를 포함 하 고도 로그 분석 솔루션 뿐 아니라 서비스 패브릭 솔루션을 포함 해야 합니다.

기존 Service Fabric 클러스터 수정:
* 진단 설정 되어 있는지 확인 (그렇지 않은 경우 활성화를 통해 [hello 가상 컴퓨터 크기 집합 업데이트](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Hello Azure 마켓플레이스를 통해 "서비스 패브릭 분석" 솔루션을 생성 하 여 OMS 작업 영역 추가
* 에 hello 클러스터 리소스 그룹이 hello에서 hello hello 서비스 패브릭 솔루션 toopick (WAD에서 설정) hello 적절 한 Azure 저장소 테이블에서 데이터를 데이터 원본 편집
* Hello 에이전트로 추가 하는 [확장 toohello 가상 컴퓨터 크기 집합](/powershell/module/azurerm.compute/add-azurermvmssextension) hello 가상 컴퓨터 크기 집합 (위와 같은 링크, toomodify hello 리소스 관리자 템플릿을) 업데이트를 통해 또는 PowerShell을 통해

## <a name="2-deploy-a-container"></a>2. 컨테이너 배포

Hello 클러스터 준비 되 고 액세스할 수 있는지 확인 한을 컨테이너 tooit를 배포 합니다. 서비스 패브릭 새 docker도 탐색할 수 hello 템플릿에 의해 세트로 toouse hello 미리 보기 버전을 선택한 경우 기능을 작성 합니다. Hello 처음으로 컨테이너 이미지를 배포 된 tooa 클러스터가, 크기에 따라 몇 분 toodownload hello 이미지를 사용 합니다.

## <a name="3-add-hello-containers-solution"></a>3. Hello 컨테이너 솔루션 추가

Hello Azure 포털에서 컨테이너 리소스를 만듭니다 (아래에서 모니터링 + 관리 hello 범주) Azure Marketplace를 통해. 

![컨테이너 솔루션 추가](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

Hello 생성 단계에서 OMS 작업 영역을 요청합니다. Hello 위의 hello 배포를 사용 하 여 만든 하나를 선택 합니다. 이 단계는 OMS 작업 영역 내에서 컨테이너 솔루션을 추가 하 고 hello 서식 파일에서 배포 된 hello OMS 에이전트에 의해 자동으로 검색 됩니다. hello 에이전트 hello 클러스터의 hello 컨테이너 프로세스에서 데이터를 수집 하 고 약 10-15 분 후에 위의 hello 대시보드의 hello 이미지와 같이 데이터로 켜 hello 솔루션 표시 되어야 합니다.

## <a name="4-next-steps"></a>4. 다음 단계

OMS 작업 영역 toomake hello의에서 다양 한 도구 더 유용 하 게 하는 경우에 제공 하면 합니다. 다음 옵션 toocustomize hello 솔루션 tooyour 요구 hello를 살펴봅니다.
- Hello로 파악 한 다음 가져올 [로그 검색 및 쿼리](../log-analytics/log-analytics-log-searches.md) 로그 분석의 일환으로 제공 하는 기능
- 특정 성능 카운터를 OMS 에이전트 toopick hello 구성 (toohello 작업 영역 홈 이동 > 설정 > 데이터 > Windows 성능 카운터)
- OMS tooset 구성할 [경고 자동](../log-analytics/log-analytics-alerts.md) 규칙 tooaid 검색 및 진단
