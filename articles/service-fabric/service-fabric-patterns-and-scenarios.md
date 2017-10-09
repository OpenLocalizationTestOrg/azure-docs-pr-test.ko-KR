---
title: "서비스 패브릭 aaaAzure 패턴 및 시나리오 | Microsoft Docs"
description: "모범 사례 알아보고 개발 및 작동 프로그램 microservices 서비스 패브릭에서 재사용 가능한 패턴 toodesign이 입증 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a>Service Fabric 패턴 및 시나리오
Azure Service Fabric을 사용 하 여 대규모 microservices 구축에 찾고 있는 경우 hello 전문가 설계 및 서비스 (PaaS)이이 플랫폼을 구축 하 게 알아봅니다. 적절 한 아키텍처를 시작 하 고 그 다음에 설명 방법을 응용 프로그램에 대 한 toooptimize 리소스입니다. hello [서비스 패브릭 Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) 과정 서비스 패브릭 시나리오 및 응용 프로그램 영역에 대 한 실제 고객이 가장 자주 요청 하는 hello 질문에 답변 합니다.
 
Toodesign, 개발 및 모범 사례 및 검증 된 하 고 재사용 가능한 패턴을 사용 하 여 서비스 패브릭에서 프로그램 microservices 작동 방법을 확인 합니다. Service Fabric의 개요를 살펴본 다음 클러스터 최적화 및 보안, 마이그레이션 레거시 앱, 대규모 IoT, 호스팅 게임 엔진 등을 다루는 항목에 대해 자세히 알아봅니다. 다양 한 작업에 대 한 지속적인 업데이트 살펴보고도 Linux 지원 및 컨테이너에서 hello 세부 정보를 가져옵니다. 

## <a name="introduction"></a>소개
모범 사례를 탐색하고 IaaS(서비스 제공 인프라)를 통한 PaaS(Platform as a Service) over 선택에 대해 알아봅니다. 다음과 같은 입증 된 응용 프로그램 디자인 원칙에 hello 세부 정보를 가져옵니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">소개 tooService 패브릭</a></td></tr>
</table>

## <a name="cluster-planning-and-management"></a>클러스터 계획 및 관리
Azure Service Fabric에 있어서 용량 계획, 클러스터 최적화 및 클러스터 보안에 대해 알아봅니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">클러스터 계획 및 관리</a></td></tr>
</table>

## <a name="hyper-scale-web"></a>초대형 웹
가용성과 안정성, 초대형 및 상태 관리를 비롯한 초대형 웹 관련 개념을 검토합니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">하이퍼스케일(hyper-scale) 웹</a></td></tr>
</table>

## <a name="iot"></a>IoT
Azure 서비스 패브릭에서 배율로 hello Azure IoT 파이프라인, 다중 테 넌 트 IoT 등의 hello 컨텍스트에서 hello 인터넷 IoT (사물)을 탐색 합니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></td></tr>
</table>

## <a name="gaming"></a>게임
턴 기반 게임, 대화형 게임 및 기존 게임 엔진 호스팅에 대해 살펴봅니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">게임</a></td></tr>
</table>

## <a name="continuous-delivery"></a>지속적인 업데이트
Visual Studio Team Services를 통한 지속적인 통합/지속적인 업데이트, 워크플로 빌드/패키지/게시, 다중 환경 설치 및 서비스 패키지/공유를 포함한 개념을 살펴봅니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">지속적인 업데이트</a></td></tr>
</table>

## <a name="migration"></a>마이그레이션
또한 레거시 응용 프로그램의 toomigration 클라우드 서비스에서 마이그레이션에 대해 알아봅니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">마이그레이션</a></td></tr>
</table>

## <a name="containers-and-linux-support"></a>컨테이너 및 Linux Support
Hello toohello 질문 응답을 가져올 "이유 컨테이너?" Windows 컨테이너, Linux 지원 하 고 Linux 컨테이너 오케스트레이션 용 hello 미리 보기에 알아봅니다. 또한 방법을 보려면 toomigrate.NET Core 앱 tooLinux 합니다.

<table><tr><th>비디오</th><th>PowerPoint 데크</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">컨테이너 및 Linux 지원</a></td></tr>
</table>

## <a name="next-steps"></a>다음 단계
서비스 패브릭 패턴 및 시나리오에 대 한 알아보았습니다 했으므로 대해 자세히 알아보세요 너무 어떻게[만들기 및 관리 클러스터](service-fabric-deploy-anywhere.md), [클라우드 서비스 앱 tooService 패브릭 마이그레이션할](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [설정 지속적인 업데이트](service-fabric-set-up-continuous-integration.md), 및 [컨테이너 배포](service-fabric-containers-overview.md)합니다.
