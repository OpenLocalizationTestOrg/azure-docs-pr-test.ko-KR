---
title: "이벤트 추적으로 문제 해결 | Microsoft Docs"
description: "Microsoft Azure 서비스 패브릭에 서비스를 배포하는 동안 발생하는 가장 일반적인 문제."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Azure 서비스 패브릭에서 서비스 배포 시 일반적인 문제 해결
개발자 컴퓨터에서 서비스를 실행하는 경우에는 [Visual Studio의 디버깅 도구](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)를 쉽게 사용할 수 있습니다. 원격 클러스터의 경우 [상태 보고서](service-fabric-view-entities-aggregated-health.md) 에서 시작하는 것이 좋습니다. 이러한 보고서에 액세스하는 가장 쉬운 방법은 PowerShell 또는 [SFX](service-fabric-visualizing-your-cluster.md)를 사용하는 것입니다. 이 문서는 사용자가 원격 클러스터를 디버그 중이며 이 도구 중 한 가지를 사용하는 방법에 대해 기본적인 이해력이 있다고 가정합니다.

## <a name="application-crash"></a>응용 프로그램 작동 중단
"Partition is below target replica or instance count"(파티션이 대상 복제본 또는 인스턴스 수 이하입니다) 보고서는 서비스 작동이 중단된다는 것을 알리는 표시입니다. 서비스의 어느 부분에서 작동이 중단되는지를 알아내려면 조사가 더 필요합니다. 서비스가 큰 규모로 실행되는 경우 최고의 자료는 면밀한 추적 데이터입니다.  [Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md)를 사용하여 추적을 수집하고 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)와 같은 솔루션을 사용하여 추적을 보고 검색하는 것이 좋습니다.

![SFX 파티션 상태](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>서비스 또는 행위자 초기화 과정
서비스 유형이 초기화되기 전에 예외가 발생하면 프로세스 중단이 유발됩니다. 이러한 유형의 작동 중단은, 응용 프로그램 이벤트 로그에 서비스의 오류가 표시됩니다.
서비스가 초기화되기 전에 볼 수 있는 가장 일반적인 예외는 다음과 같습니다.

***System.IO.FileNotFoundException***

이 오류는 대체로 어셈블리 종속성이 없기 때문에 발생합니다. Visual Studio에서 CopyLocal 속성을 확인하거나 노드의 전역 어셈블리 캐시를 확인하세요.

***System.Runtime.InteropServices.COMException*** *System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)에서*

 등록된 서비스 유형 이름이 서비스 매니페스트와 일치하지 않음을 나타냅니다.

[Azure 진단](service-fabric-diagnostics-how-to-setup-wad.md) 을 구성할 수 있습니다.

### <a name="runasync-or-onactivateasync"></a>RunAsync() or OnActivateAsync()
등록된 서비스 유형 또는 행위자를 초기화하거나 실행하는 중에 작동이 중단되면 Azure 서비스 패브릭이 예외를 catch합니다. 이 내용은 EventSource 공급자를 통해 볼 수 있으며 “다음 단계” 섹션에 자세히 설명되어 있습니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭에 제공되는 기존 진단에 대해 자세히 알아봅니다.

* [Reliable Actors 진단](service-fabric-reliable-actors-diagnostics.md)
* [Reliable Services 진단](service-fabric-reliable-services-diagnostics.md)

