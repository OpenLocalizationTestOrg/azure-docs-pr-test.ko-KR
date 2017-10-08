---
title: "aaaDebug Eclipse에서 Azure 서비스 패브릭 응용 프로그램 | Microsoft Docs"
description: "개발 하 고 로컬 개발 클러스터에 Eclipse에서 디버깅 하 여 서비스의 hello 안정성 및 성능을 개선 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="81ccf-103">Eclipse를 사용하여 Java Service Fabric 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="81ccf-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81ccf-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="81ccf-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="81ccf-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="81ccf-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="81ccf-106">로컬 개발 클러스터에 hello 단계에 따라 시작 [서비스 패브릭 개발 환경 설정](service-fabric-get-started-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="81ccf-107">EntryPoint.sh 업데이트 hello 서비스의 원하는 toodebug, 원격 디버그 매개 변수가 있는 hello java 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="81ccf-108">Hello 수정할 수 있는 위치에서이 파일을 찾을 수 있습니다: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="81ccf-109">이 예제에서 포트 8001은 디버깅을 위해 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="81ccf-110">Hello 인스턴스 수를 설정 하 여 hello 응용 프로그램 매니페스트를 업데이트 하거나 hello 되는 hello 서비스에 대 한 복제본 수 디버깅 too1 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="81ccf-111">이 설정은 디버깅에 사용 되는 hello 포트에 대 한 충돌을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="81ccf-112">예를 들어 상태 비저장 서비스에 대 한 설정 ``InstanceCount="1"`` 상태 저장 서비스에 대 한 hello 대상 및 최소 복제본 집합 크기 too1와 같이 설정 하 고: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="81ccf-113">Hello 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-113">Deploy hello application.</span></span>

5. <span data-ttu-id="81ccf-114">Hello Eclipse IDE에서에서 선택 **실행 디버그 구성-> 원격 Java 응용 프로그램-> 연결 속성을 입력 하 고** hello 속성을 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="81ccf-115">원하는 시점에 중단점을 설정 하 고 hello 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="81ccf-116">Hello 응용 프로그램 충돌 tooenable coredumps를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="81ccf-117">셸에서 ``ulimit -c``를 실행했을 때 0이 반환될 경우 coredump가 사용하지 않도록 설정된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="81ccf-118">tooenable 무제한 coredumps hello 다음 명령을 실행: ``ulimit -c unlimited``합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="81ccf-119">Hello 명령을 사용 하 여 hello 상태를 확인할 수도 있습니다 ``ulimit -a``합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="81ccf-120">Tooupdate hello coredump 생성 경로가 필요한 경우 실행 ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``합니다.</span><span class="sxs-lookup"><span data-stu-id="81ccf-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="81ccf-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81ccf-121">Next steps</span></span>

* <span data-ttu-id="81ccf-122">[Linux Azure 진단을 사용하여 로그 수집](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="81ccf-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="81ccf-123">[로컬로 서비스 모니터링 및 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="81ccf-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
