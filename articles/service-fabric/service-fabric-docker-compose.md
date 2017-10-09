---
title: "aaaAzure 서비스 패브릭 Docker 작성 미리 보기"
description: "Azure 서비스 패브릭 형식 toomake Docker Compose를 허용 하기 서비스 패브릭을 사용 하 여 보다 쉽게 tooorchestrate 기존 컨테이너입니다. 이 지원은 현재 미리 보기로 제공되고 있습니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Azure Service Fabric의 Docker Compose 응용 프로그램 지원(미리 보기)

Docker hello를 사용 하 여 [docker compose.yml](https://docs.docker.com/compose) 다중 컨테이너 응용 프로그램 정의 파일입니다. toomake 것 Docker tooorchestrate 기존 컨테이너에서 응용 프로그램과 함께 Azure Service Fabric 친숙 한 고객을 쉽게의 포함 되어 있습니다 Docker Compose에 대 한 미리 보기 지원 고유 하 게 hello 플랫폼입니다. Service Fabric은 `docker-compose.yml` 파일의 버전 3 이상을 수락할 수 있습니다. 

이 지원은 미리 보기로 제공되므로 Compose 지시문의 하위 집합만 지원됩니다. 예를 들어 응용 프로그램 업그레이드는 지원되지 않습니다. 그러나 응용 프로그램을 업그레이드하는 대신 항상 제거한 후 배포할 수 있습니다.

toouse 미리이 hello SDK에 해당 하는 hello와 함께 Azure 포털을 통해 서비스 패브릭 런타임을 hello 5.7 이상 버전으로 클러스터를 만듭니다. 

> [!NOTE]
> 이 기능은 미리 보기로 제공되며 프로덕션에서 지원되지 않습니다.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Service Fabric에서 Docker Compose 파일 배포

hello 다음 명령은 서비스 패브릭 응용 프로그램을 만듭니다 (라는 `fabric:/TestContainerApp` hello 예에서는 앞에서)를 모니터링 하 고 다른 서비스 패브릭 응용 프로그램 처럼 관리할 수 있는 합니다. 상태 쿼리 수에 대 한 hello 지정 된 응용 프로그램 이름을 사용할 수 있습니다.

### <a name="use-powershell"></a>PowerShell 사용

Hello 다음 powershell에서 명령을 실행 하 여 docker compose.yml 파일에서 서비스 패브릭 구성 응용 프로그램을 만듭니다.

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`및 `RegistryPassword` toohello 컨테이너 레지스트리 사용자 이름 및 암호를 참조 하십시오. Hello 응용 프로그램을 완료 한 후 다음 명령을 hello를 사용 하 여 해당 상태를 확인할 수 있습니다.

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete hello PowerShell에서 다음 명령을 사용 하 여 hello 통해 응용 프로그램 작성.

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Azure Service Fabric CLI(sfctl) 사용

또는 다음 서비스 패브릭 CLI 명령을 hello를 사용할 수 있습니다.

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Hello 응용 프로그램을 만든 후 다음 명령을 hello를 사용 하 여 해당 상태를 확인할 수 있습니다.

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

toodelete hello 작성할 응용 프로그램에는 hello 다음 명령을 사용 합니다.

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>지원되는 Compose 지시문

이 미리 보기 hello Compose 3 버전 형식에 기본 형식 다음 hello를 포함 하 여 hello 구성 옵션의 하위 집합을 지원 합니다.

* 서비스 > 배포 > 복제본
* 서비스 > 배포 > 배치 > 제약 조건
* 서비스 > 배포 > 리소스 > 제한
    * -cpu-shares
    * -memory
    * -memory-swap
* 서비스 > 명령
* 서비스 > 환경
* 서비스 > 포트
* 서비스 > 이미지
* 서비스 > 격리(Windows에만 해당)
* 서비스 > 로깅 > 드라이버
* 서비스 > 로깅 > 드라이버 > 옵션
* 볼륨 및 배포 > 볼륨

에 설명 된 대로 리소스 제한을 적용 하는 것에 대 한 hello 클러스터를 설정 [서비스 패브릭 리소스 관리](service-fabric-resource-governance.md)합니다. 다른 모든 Docker Compose 지시문은 이 미리 보기에서 지원되지 않습니다.

## <a name="servicednsname-computation"></a>ServiceDnsName 계산

구성 파일에서 지정 하는 hello 서비스 이름을 정규화 된 도메인 이름인 경우 (즉, 포함 된 점 [.]) 서비스 패브릭에서 등록 하는 hello DNS 이름이 `<ServiceName>` (hello 점 포함). 그렇지 않은 경우 각 경로 세그먼트 hello 응용 프로그램 이름에 hello hello 최상위 도메인 레이블 되는 첫 번째 경로 세그먼트와 hello 서비스 DNS 이름에는 도메인 레이블이 됩니다.

예를 들어 hello 응용 프로그램 이름 지정은 `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` hello 등록 된 DNS 이름을 것입니다.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Compose(인스턴스 정의) 및 Service Fabric 응용 프로그램 모델(형식 정의) 간 차이

docker-compose.yml 파일은 해당 속성 및 구성을 포함하는 컨테이너의 배포 가능 집합을 설명합니다.
예를 들어 hello 파일 환경 변수 및 포트를 포함할 수 있습니다. Hello docker compose.yml 파일에서 DNS 이름, 배치 제약 조건 및 리소스 제한 등 배포 매개 변수를 지정할 수도 있습니다.

hello [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md) 사용 하 여 서비스 유형 및 응용 프로그램 유형, 응용 프로그램 인스턴스 수를 사용할 수 있는 hello 같은 형식입니다. 예를 들어 고객이 각자 하나의 응용 프로그램 인스턴스를 사용할 수 있습니다. 이 형식 기반 모델에서는 여러 버전의 hello hello 런타임과 함께 등록 되어 있는 동일한 응용 프로그램 종류입니다.

예를 들어 고객 A, AppTypeA 유형의 1.0 사용 하 여 인스턴스화되고 응용 프로그램을 가질 수 있습니다 및 B 고객에 게 다른 응용 프로그램 hello를 사용 하 여 인스턴스화되고 동일한 유형 및 버전입니다. Hello 응용 프로그램 매니페스트의 hello 응용 프로그램 종류를 정의 하 고 hello 응용 프로그램을 만들 때 hello 응용 프로그램 이름 및 배포 매개 변수를 지정 합니다.

유연성을 제공 하는이 모델을 있지만 예정 toosupport hello 매니페스트 파일에서 형식을 암시적는 간단 하 고 인스턴스 기반 배포 모델입니다. 이 모델에서 각 응용 프로그램은 자체의 독립적인 매니페스트를 갖게 됩니다. 인스턴스 기반 배포 형식인 docker-compose.yml에 대한 지원을 추가하여 이러한 방식을 미리 검토하고 있습니다.

## <a name="next-steps"></a>다음 단계

* Hello에 대 [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md)
* [Service Fabric CLI 시작](service-fabric-cli.md)
