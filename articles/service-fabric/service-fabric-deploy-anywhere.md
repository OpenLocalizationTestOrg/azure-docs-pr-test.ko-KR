---
title: "Windows Server 및 Linux에서 aaaCreate Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "서비스 패브릭 클러스터에서 Windows Server 및 있음을 나타내는 Linux에서 실행 됩니다 수 toodeploy 서비스 패브릭 응용 프로그램 및 호스트 원하는 위치에 Windows Server 또는 Linux를 실행할 수 있습니다."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Windows Server 또는 Linux에서 Service Fabric 클러스터 만들기
Azure Serivce Fabric 클러스터는 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다. 클러스터의 일부인 컴퓨터나 VM을 클러스터 노드라고 합니다. 클러스터 노드의 toothousands를 확장할 수 있습니다. 새 노드 toohello 클러스터를 추가 하는 경우 서비스 패브릭 서비스 파티션 복제본 hello 및 인스턴스 노드 수가 증가 하는 hello 간에 변경 합니다. 전체 응용 프로그램의 성능을 개선 하 고 액세스 toomemory에 대 한 경합이 감소 합니다. Hello 클러스터의 노드 hello 효율적으로 사용 되지 않는, hello hello 클러스터의 노드 수를 줄일 수 있습니다. 서비스 패브릭 hello 파티션 복제를 다시 변경 하 고 노드 toomake 수가 감소 하는 hello에서 인스턴스 좋은 hello 하드웨어 각 노드에서 사용 하 여 키를 누릅니다.

서비스 패브릭 hello 모든 Vm 또는 Windows Server 또는 Linux를 실행 하는 컴퓨터에 서비스 패브릭 클러스터 만들기를 허용 합니다. 즉, toodeploy 수 있고 상호 연결 되는 Windows Server 또는 Linux 컴퓨터 집합에 있는 모든 환경에서 서비스 패브릭 응용 프로그램 실행, 온-프레미스, Microsoft Azure 수 또는 모든 클라우드 공급자와 합니다.

## <a name="create-service-fabric-clusters-on-azure"></a>Azure에서 Service Fabric 클러스터 만들기
Azure에서 클러스터 만들기 리소스 모델 템플릿 또는 hello Azure 포털을 통해 수행 됩니다. 읽기 [리소스 관리자 템플릿을 사용 하 여 서비스 패브릭 클러스터를 만들](service-fabric-cluster-creation-via-arm.md) 또는 [hello Azure 포털에서에서 서비스 패브릭 클러스터를 만드는](service-fabric-cluster-creation-via-portal.md) 자세한 정보에 대 한 합니다.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Azure에서 클러스터에 지원되는 운영 체제
사용자는 이러한 운영 체제를 실행 하는 Vm의 수 toocreate 클러스터:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04(공개 미리 보기 상태) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>온-프레미스에서 또는 클라우드 공급자를 사용하여 Service Fabric 독립 실행형 클러스터 만들기
서비스 패브릭 설치 패키지를 제공 하면 toocreate 독립 실행형 서비스 패브릭 클러스터에 온-프레미스 또는 모든 클라우드 공급자

Windows Server에서 독립 실행형 Service Fabric 클러스터 설치에 자세한 내용은 [Windows Server용 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>클라우드 배포와 온-프레미스 배포 비교
온-프레미스 서비스 패브릭 클러스터를 만들기 위한 hello 프로세스는 유사 toohello 프로세스 Vm 집합이 있는 사용자가 선택한 모든 클라우드에 대 한 클러스터를 만드는입니다. hello 초기 단계 tooprovision hello Vm 클라우드 공급자 hello 또는 사용 하는 온-프레미스 환경에서 관리 됩니다. 으로 Vm의 집합을 설정한 후, 사이 사용할 네트워크 연결 다음 hello 서비스 패브릭 패키지를 단계 tooset hello, hello 클러스터 설정을 편집 hello 클러스터 만들기를 실행 및 관리 스크립트는 동일 합니다. 이렇게 하면 지식 및 운영 하 고 서비스 패브릭 클러스터 관리 환경을 양도할 수 tootarget 새 호스팅 환경을 선택 합니다.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>독립 실행형 서비스 패브릭 클러스터를 만들 경우의 이점
* 무료 toochoose는 모든 클라우드 공급자 toohost 클러스터입니다.
* 서비스 패브릭 응용 프로그램을 작성 한 번 toono 최소한의 변경 내용으로 여러 호스팅 환경에서 실행할 수 있습니다.
* 서비스 패브릭 응용 프로그램 구축 기술 한 호스팅 환경 tooanother에서를 통해 전달 합니다.
* 운영 경험을 실행 하 고 서비스 패브릭 관리를 통해 환경 tooanother에서 수행을 클러스터링 합니다.
* 호스팅 환경 제약을 받지 않아 고객 도달 범위가 넓습니다.
* 안정성 및 광범위 한 가동 중단 으로부터 보호 하는 추가적인 hello 서비스 하는 경우 데이터 센터 tooanother 배포 환경 위로 이동 하면 또는 클라우드 공급자에 게는 중단 때문에 존재 합니다.

## <a name="supported-operating-systems-for-standalone-clusters"></a>독립 실행형 클러스터에 지원되는 운영 체제
사용자는 이러한 운영 체제를 실행 하는 컴퓨터 또는 Vm에 수 toocreate 클러스터:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux(서비스 예정)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>온-프레미스에서 만든 독립 실행형 서비스 패브릭 클러스터와 비교한 Azure 서비스 패브릭 클러스터의 장점
Azure에서 서비스 패브릭 클러스터를 실행 hello 온-프레미스 옵션에 비해 이점을 제공 하므로 클러스터를 실행 하는 위치에 대 한 특정 요구를 설정 하지 않은 경우 권장 되는 사항은 Azure에서 실행 하 합니다. Azure에서 다른 Azure 기능 및 쉽고 안정적 작업 및 hello 클러스터의 관리를 서비스와 통합을 제공 합니다.

* **Azure 포털:** Azure 포털에서 쉽게 toocreate를 사용 하면 및 클러스터를 관리 합니다.
* **Azure 리소스 관리자:** 단위로 hello 클러스터에서 사용 하는 모든 리소스를 쉽게 관리할 수 있게 하 고 비용 추적 및 요금 청구를 간소화 하는 Azure 리소스 관리자를 사용 합니다.
* **Azure 리소스로서의 서비스 패브릭 클러스터** 서비스 패브릭 클러스터는 ARM 리소스이므로 Azure의 다른 ARM 리소스와 같이 모델링할 수 있습니다.
* **Azure 인프라와의 통합** 서비스 패브릭 원본 운영 체제, 네트워크 및 기타 업그레이드 tooimprove 가용성 및 응용 프로그램의 안정성에 대 한 Azure 인프라를 사용 하는 hello와 동등 합니다.  
* **진단:** Azure에서는 Azure 진단과 Log Analytics가 통합됩니다.
* **자동 크기 조정:** tooVirtual 컴퓨터 크기 집합 인해 자동 크기 조정 기능을 기본적으로 클러스터의 경우 Azure에서 제공 합니다. 온-프레미스 및 다른 클라우드 환경에서은 toobuild 고유한 자동 크기 조정 기능 또는 배율 수동으로 hello 서비스 패브릭 노출 하는 Api를 사용 하 여 클러스터 크기를 조정 합니다.

## <a name="next-steps"></a>다음 단계

* Windows Server를 실행하는 VM 또는 컴퓨터에서 클러스터 만들기: [Windows Server용 서비스 패브릭 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md)
* Linux를 실행하는 VM 또는 컴퓨터에서 클러스터 만들기: [Linux의 서비스 패브릭](service-fabric-linux-overview.md)
* [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기

