---
title: "Eclipse에서 Azure Service Fabric 응용 프로그램 디버그 | Microsoft Docs"
description: "로컬 개발 클러스터의 Eclipse에서 개발하고 디버그하여 서비스의 안정성과 성능을 향상시킵니다."
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
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="dd9bb-103">Eclipse를 사용하여 Java Service Fabric 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="dd9bb-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd9bb-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="dd9bb-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="dd9bb-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="dd9bb-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="dd9bb-106">[서비스 패브릭 개발 환경 설정](service-fabric-get-started-linux.md)의 단계를 따라 로컬 개발 클러스터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="dd9bb-107">디버그하려는 서비스의 entryPoint.sh를 원격 디버그 매개 변수를 사용하여 java 프로세스를 시작하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="dd9bb-108">이 파일은 ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh`` 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="dd9bb-109">이 예제에서 포트 8001은 디버깅을 위해 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="dd9bb-110">인스턴스 수 또는 디버그하는 서비스의 복제본 수를 1로 설정하여 응용 프로그램 매니페스트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="dd9bb-111">이 설정은 디버깅에 사용되는 포트에 대한 충돌을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="dd9bb-112">예를 들어, 상태 비저장 서비스의 경우 ``InstanceCount="1"``을 설정하고 상태 저장 서비스의 경우 `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``과 같이 대상과 최소 복제본 세트 크기를 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="dd9bb-113">응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-113">Deploy the application.</span></span>

5. <span data-ttu-id="dd9bb-114">Eclipse IDE에서 **실행 -> 원격 Java 응용 프로그램 및 입력 연결 속성**을 선택하고 속성을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="dd9bb-115">원하는 지점에 중단점을 설정하고 응용 프로그램을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="dd9bb-116">응용 프로그램이 충돌하는 경우 coredump를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="dd9bb-117">셸에서 ``ulimit -c``를 실행했을 때 0이 반환될 경우 coredump가 사용하지 않도록 설정된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="dd9bb-118">무제한 coredump를 사용하도록 설정하려면 ``ulimit -c unlimited`` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="dd9bb-119">또한 ``ulimit -a`` 명령을 사용하여 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="dd9bb-120">coredump 생성 경로를 업데이트하려면 ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="dd9bb-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd9bb-121">Next steps</span></span>

* <span data-ttu-id="dd9bb-122">[Linux Azure 진단을 사용하여 로그 수집](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="dd9bb-123">[로컬로 서비스 모니터링 및 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
