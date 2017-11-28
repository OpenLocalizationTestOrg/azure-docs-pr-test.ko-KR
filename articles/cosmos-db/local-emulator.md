---
title: "hello Azure Cosmos DB 에뮬레이터를 사용 하 여 로컬로 aaaDevelop | Microsoft Docs"
description: "Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 개발 하 고 Azure 구독을 만들지 않고 비어 있거나 응용 프로그램을 로컬로 테스트할 수 있습니다."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 에뮬레이터"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="5d476-104">Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 로컬 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5d476-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="5d476-105"><strong>이진 파일</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="5d476-106">MSI 다운로드</span><span class="sxs-lookup"><span data-stu-id="5d476-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="5d476-108">Docker 허브</span><span class="sxs-lookup"><span data-stu-id="5d476-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-109"><strong>Docker 원본</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="5d476-110">Github</span><span class="sxs-lookup"><span data-stu-id="5d476-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="5d476-111">hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스를 개발 목적으로 에뮬레이트하는 로컬 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="5d476-112">Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 개발 하 고 Azure 구독을 만들거나 모든 비용이 발생 하지 않고 응용 프로그램을 로컬로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="5d476-113">Hello Azure Cosmos DB 에뮬레이터에서에서 응용 프로그램 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure Cosmos DB 계정을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="5d476-114">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5d476-115">Hello 에뮬레이터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="5d476-116">Windows 용 Docker에 hello 에뮬레이터 실행</span><span class="sxs-lookup"><span data-stu-id="5d476-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="5d476-117">요청 인증</span><span class="sxs-lookup"><span data-stu-id="5d476-117">Authenticating requests</span></span>
> * <span data-ttu-id="5d476-118">Hello 에뮬레이터의에서 hello 데이터 탐색기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5d476-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="5d476-119">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d476-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="5d476-120">에뮬레이터의 hello hello 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="5d476-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="5d476-121">추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="5d476-121">Collecting trace files</span></span>

<span data-ttu-id="5d476-122">다음 비디오에서는 Kirill Gavrylyuk tooget Azure Cosmos DB 에뮬레이터 hello로 시작 하는 방법을 보여 줍니다 hello를 시청 하 여 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d476-123">Hello 비디오를 눌러 이후 Azure Cosmos DB 에뮬레이터 hello 하는 hello 비디오에서는 DocumentDB 에뮬레이터 hello 라고 toohello 에뮬레이터 되지만 hello 도구 자체 이름이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="5d476-124">비디오 hello에서 모든 정보는 hello Azure Cosmos DB 에뮬레이터에 대 한 정확 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="5d476-125">Hello 에뮬레이터의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="5d476-125">How hello Emulator works</span></span>
<span data-ttu-id="5d476-126">hello Azure Cosmos DB 에뮬레이터의 hello Azure Cosmos DB 서비스의 충실도 높은 재현 에뮬레이션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="5d476-127">JSON 문서 만들기 및 쿼리, 컬렉션 프로비전 및 확장, 저장 프로시저 및 트리거 실행을 비롯하여 Azure Cosmos DB으로 동일한 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="5d476-128">개발 및 hello Azure Cosmos DB 에뮬레이터를 사용 하 여 응용 프로그램을 테스트 하 고 방금 단일 구성을 Azure Cosmos DB에 대 한 toohello 연결 끝점을 변경 하 여 세계적인 규모에 tooAzure 배포 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="5d476-129">Hello 실제 Azure Cosmos DB 서비스의 충실도 높은 재현 로컬 에뮬레이션 만들었습니다 동안 hello Azure Cosmos DB 에뮬레이터의 hello 구현 hello 서비스의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="5d476-130">예를 들어 hello Azure Cosmos DB 에뮬레이터는 지 속성 및 연결에 대 한 HTTPS 프로토콜 스택에 hello 로컬 파일 시스템 등 표준 OS 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="5d476-131">즉, 글로벌 복제, 읽기/쓰기 및 튜닝할 수 있는 일관성 수준에 대 한 대기 시간이 단일 자리 숫자 밀리초를 hello Azure Cosmos DB 에뮬레이터를 통해 사용할 수 없는 경우와 같은 Azure 인프라를 사용 하는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="5d476-132">Hello에이 시간 hello 데이터 탐색기에서 에뮬레이터는 DocumentDB API 컬렉션과 MongoDB 컬렉션 hello 만들기만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="5d476-133">hello 에뮬레이터의 hello 데이터 탐색기 현재 테이블 및 그래프의 hello 생성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="5d476-134">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5d476-134">System requirements</span></span>
<span data-ttu-id="5d476-135">hello Azure Cosmos DB 에뮬레이터의 hello 하드웨어 및 소프트웨어 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="5d476-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="5d476-136">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5d476-136">Software requirements</span></span>
  * <span data-ttu-id="5d476-137">Windows Server 2012 R2, Windows Server 2016 또는 Windows 10</span><span class="sxs-lookup"><span data-stu-id="5d476-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="5d476-138">최소 하드웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5d476-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="5d476-139">2GB RAM</span><span class="sxs-lookup"><span data-stu-id="5d476-139">2 GB RAM</span></span>
  * <span data-ttu-id="5d476-140">10GB의 하드 디스크 여유 공간</span><span class="sxs-lookup"><span data-stu-id="5d476-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="5d476-141">설치</span><span class="sxs-lookup"><span data-stu-id="5d476-141">Installation</span></span>
<span data-ttu-id="5d476-142">다운로드 하 여 hello에서 hello Azure Cosmos DB 에뮬레이터 설치 [Microsoft 다운로드 센터](https://aka.ms/cosmosdb-emulator)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="5d476-143">tooinstall를 구성 하 고 hello Azure Cosmos DB 에뮬레이터를 실행, hello 컴퓨터에서 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="5d476-144">Windows용 Docker에서 실행</span><span class="sxs-lookup"><span data-stu-id="5d476-144">Running on Docker for Windows</span></span>

<span data-ttu-id="5d476-145">Windows 용 Docker에 hello Azure Cosmos DB 에뮬레이터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="5d476-146">Oracle Linux에 대 한 hello 에뮬레이터 Docker에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="5d476-147">설정한 후 [Windows 용 Docker](https://www.docker.com/docker-windows) 설치 되어 끌어올 수 있습니다 hello 에뮬레이터 이미지 Docker 허브에서 hello 즐겨 찾는 셸에서 다음 명령을 실행 하 여 (cmd.exe, PowerShell 등.).</span><span class="sxs-lookup"><span data-stu-id="5d476-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="5d476-148">toostart hello 이미지를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="5d476-149">hello 응답 비슷한 toohello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="5d476-150">에뮬레이터를 시작 하는 hello 종료 hello 에뮬레이터의 컨테이너는 면 대화형 셸 hello를 종료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="5d476-151">클라이언트에서 hello 끝점과 hello 응답에서의 마스터 키를 사용 하 하며 호스트로 hello SSL 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="5d476-152">tooimport hello SSL 인증서를 관리자 명령 프롬프트에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="5d476-153">Hello 에뮬레이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-153">Start hello Emulator</span></span>

<span data-ttu-id="5d476-154">toostart hello Azure Cosmos DB 에뮬레이터 hello 시작 단추를 선택 하거나 hello Windows 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="5d476-155">입력을 시작 **Azure Cosmos DB 에뮬레이터**, 및 응용 프로그램의 hello 목록에서 선택 hello 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Hello 시작 단추를 클릭 하거나 눌러 hello Windows 키를 선택, 입력을 시작 * * Azure Cosmos DB 에뮬레이터 * *, 및 응용 프로그램의 hello 목록에서 선택 hello 에뮬레이터](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="5d476-157">Hello 에뮬레이터를 실행 하는 경우에 hello Windows 작업 표시줄 알림 영역에서에서 아이콘을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Azure Cosmos DB 로컬 에뮬레이터 작업 표시줄 알림](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="5d476-159">기본적으로 Azure Cosmos DB 에뮬레이터 hello 포트 8081에서 수신 대기 로컬 hello 컴퓨터 ("localhost")에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="5d476-160">hello Azure Cosmos DB 에뮬레이터가 설치 되어 기본 toohello로 `C:\Program Files\Azure Cosmos DB Emulator` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="5d476-161">또한 시작 하 고 hello 명령줄에서 hello 에뮬레이터를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="5d476-162">자세한 내용은 [명령줄 도구 참조](#command-line)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d476-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="5d476-163">데이터 탐색기 시작</span><span class="sxs-lookup"><span data-stu-id="5d476-163">Start Data Explorer</span></span>

<span data-ttu-id="5d476-164">Hello Azure Cosmos DB 에뮬레이터를 시작할 때 자동으로 열립니다 hello Azure Cosmos DB 데이터 탐색기 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="5d476-165">hello 주소도 나타납니다. [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="5d476-166">닫기 탐색기 hello을 하면 toore 열기 원하는 것 이상 hello URL을 브라우저에서 열 하거나 아래와 같이 hello Windows 트레이 아이콘에에서 hello Azure Cosmos DB 에뮬레이터에서에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB의 로컬 에뮬레이터 데이터 탐색기 시작 관리자](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="5d476-168">업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="5d476-168">Checking for updates</span></span>
<span data-ttu-id="5d476-169">데이터 탐색기에 다운로드할 수 있는 새 업데이트가 있는지 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="5d476-170">한 버전의 hello Azure Cosmos DB 에뮬레이터에서 만든 데이터 보장 되지 않습니다 toobe 액세스할 수 있는 다른 버전을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5d476-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="5d476-171">Hello 장기에 대 한 데이터 toopersist 경우 아닌 hello Azure Cosmos DB 에뮬레이터는 Azure Cosmos DB 계정에 해당 데이터를 저장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="5d476-172">요청 인증</span><span class="sxs-lookup"><span data-stu-id="5d476-172">Authenticating requests</span></span>
<span data-ttu-id="5d476-173">마찬가지로 hello 클라우드에서 Azure Cosmos DB와 함께 hello Azure Cosmos DB 에뮬레이터에 대해 구성 하는 모든 요청 인증 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="5d476-174">hello Azure Cosmos DB 에뮬레이터 마스터 키 인증을 위해 단일 고정 계정과 잘 알려진 인증 키를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="5d476-175">이 계정과 키는 hello Azure Cosmos DB 에뮬레이터로 사용 하기 위해 허용 hello 유일한 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="5d476-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d476-176">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="5d476-177">hello Azure Cosmos DB 에뮬레이터에서 지 원하는 hello 마스터 키 hello 에뮬레이터에만 사용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="5d476-178">Azure Cosmos DB 에뮬레이터 hello로 프로덕션 Azure Cosmos DB 계정 및 키를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="5d476-179">/Key 옵션 hello로 hello 에뮬레이터를 시작한 경우 그런 다음 대신 hello 생성 된 키 사용 "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="5d476-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="5d476-180">또한와 마찬가지로 Azure Cosmos DB 서비스를 Azure Cosmos DB 에뮬레이터 hello hello SSL 통해 안전한 통신만을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="5d476-181">로컬 네트워크 hello 에뮬레이터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="5d476-182">로컬 네트워크 hello 에뮬레이터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="5d476-183">tooenable 네트워크 액세스, hello에 hello /AllowNetworkAccess 옵션을 지정할 [명령줄](#command-line-syntax), /Key를 지정 하는 또한 합니다 key_string 또는 /KeyFile = file_name = 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="5d476-184">/GenKeyFile를 사용할 수 있습니다 = file_name toogenerate 파일 현상을 임의 키 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="5d476-185">해당 너무/키 파일을 전달할 수 = file_name 또는 /Key = contents_of_file 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="5d476-186">hello 신규 hello 사용자에 대 한 네트워크 액세스 tooenable hello 에뮬레이터를 종료 해야 하 고 hello 에뮬레이터의 데이터 디렉터리 (C:\Users\user_name\AppData\Local\CosmosDBEmulator)를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="5d476-187">Hello 에뮬레이터를 사용 하 여 개발</span><span class="sxs-lookup"><span data-stu-id="5d476-187">Developing with hello Emulator</span></span>
<span data-ttu-id="5d476-188">데스크톱에서 실행 되는 Azure DB Cosmos 에뮬레이터 hello 있는, 지원 되는 사용할 수 있습니다 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 또는 hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract 에뮬레이터 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="5d476-189">hello Azure Cosmos DB 에뮬레이터에는 모든 코드를 작성 하지 않고도 문서를 편집 하 고 hello DocumentDB MongoDB Api 및 보기에 대 한 컬렉션을 만들 수 있는 기본 제공 데이터 탐색기 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="5d476-190">사용 중인 경우 [MongoDB에 대 한 Azure Cosmos DB 프로토콜 지원](mongodb-introduction.md), 다음 연결 문자열 hello를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d476-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="5d476-191">와 같은 기존 도구를 사용할 수 있습니다 [Azure DocumentDB 스튜디오](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d476-192">Hello Azure Cosmos DB 에뮬레이터와 hello를 사용 하 여 hello Azure Cosmos DB 서비스 간에 데이터를 마이그레이션할 수도 있습니다 [Azure Cosmos DB 데이터 마이그레이션 도구](https://github.com/azure/azure-documentdb-datamigrationtool)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="5d476-193">/Key 옵션 hello로 hello 에뮬레이터를 시작한 경우 그런 다음 대신 hello 생성 된 키 사용 "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="5d476-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="5d476-194">Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 기본적으로, too25 단일 파티션 컬렉션 또는 1 분할 된 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="5d476-195">이 값을 변경 하는 방법에 대 한 자세한 내용은 참조 [hello PartitionCount 값 설정](#set-partitioncount)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="5d476-196">Hello SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d476-196">Export hello SSL certificate</span></span>

<span data-ttu-id="5d476-197">.NET 언어 및 런타임 사용 하 여 hello Windows 인증서 저장소 toosecurely toohello Azure Cosmos DB 로컬 에뮬레이터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="5d476-198">다른 언어의 경우 해당 언어만의 인증서 관리 및 사용 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="5d476-199">Java는 자체의 고유 [인증서 저장소](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)를 사용하고 Python은 [소켓 래퍼](https://docs.python.org/2/library/ssl.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="5d476-200">순서 tooobtain에서 언어 및 통합 되지 않습니다 hello Windows 인증서 저장소로 있습니다 있는 런타임과 상호 인증서 toouse 할 tooexport 인증서 관리자 Windows hello를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="5d476-201">Certlm.msc를 실행 하 여 시작 하거나 hello 단계별 지침에 따라 수 [hello Azure Cosmos DB 에뮬레이터 인증서 내보내기](./local-emulator-export-ssl-certificates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="5d476-202">Hello 인증서 관리자를 실행 하 고, 내보내기 및 열기 hello 개인 인증서 아래와 같이 hello hello 친숙 한 이름이 "DocumentDBEmulatorCertificate" 인증서 대로 E-64로 인코딩된 X.509 (.cer) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB 로컬 에뮬레이터 SSL 인증서](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="5d476-204">hello 지침에 따라 hello Java 인증서 저장소로 hello X.509 인증서를 가져올 수 [Java CA 인증서를 저장 하는 인증서 toohello 추가](https://docs.microsoft.com/azure/java-add-certificate-ca-store)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="5d476-205">가져온 hello 인증서는 hello 인증서 저장소로 MongoDB 및 Java 응용 프로그램 수 tooconnect toohello Azure Cosmos DB 에뮬레이터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="5d476-206">Python 및 Node.js Sdk에서 toohello 에뮬레이터에 연결할 때 SSL 유효성 검사 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="5d476-207"><a id="command-line"></a>명령줄 도구 참조</span><span class="sxs-lookup"><span data-stu-id="5d476-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="5d476-208">Hello 설치 위치에서 있습니다 수 명령줄 toostart hello를 사용 하 여 중지 hello 에뮬레이터, 옵션을 구성 하 고 다른 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="5d476-209">명령줄 구문</span><span class="sxs-lookup"><span data-stu-id="5d476-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="5d476-210">옵션을 형식 tooview hello 목록 `CosmosDB.Emulator.exe /?` hello 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="5d476-211"><strong>옵션</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="5d476-212"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="5d476-213"><strong>명령</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="5d476-214"><strong>인수</strong></span><span class="sxs-lookup"><span data-stu-id="5d476-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-215">[인수 없음]</span><span class="sxs-lookup"><span data-stu-id="5d476-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="5d476-216">기본 설정으로 hello Azure Cosmos DB 에뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="5d476-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="5d476-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-218">[도움말]</span><span class="sxs-lookup"><span data-stu-id="5d476-218">[Help]</span></span></td>
  <td><span data-ttu-id="5d476-219">Hello 목록을 표시 합니다. 명령줄 인수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="5d476-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="5d476-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="5d476-221">Shutdown</span></span></td>
  <td><span data-ttu-id="5d476-222">Hello Azure Cosmos DB 에뮬레이터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="5d476-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="5d476-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="5d476-224">DataPath</span></span></td>
  <td><span data-ttu-id="5d476-225">어떤 toostore 데이터 파일에 hello 경로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="5d476-226">기본값은 %LocalAppdata%\CosmosDBEmulator입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="5d476-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="5d476-228">&lt;datapath&gt;: 액세스 가능한 경로</span><span class="sxs-lookup"><span data-stu-id="5d476-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-229">포트</span><span class="sxs-lookup"><span data-stu-id="5d476-229">Port</span></span></td>
  <td><span data-ttu-id="5d476-230">Hello 에뮬레이터에 대 한 포트 번호 toouse hello를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="5d476-231">기본값은 8081입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="5d476-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="5d476-233">&lt;port&gt;: 단일 포트 번호</span><span class="sxs-lookup"><span data-stu-id="5d476-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="5d476-234">MongoPort</span></span></td>
  <td><span data-ttu-id="5d476-235">MongoDB 호환성 API에 대 한 포트 번호 toouse hello를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="5d476-236">기본값은 10255입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="5d476-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="5d476-238">&lt;mongoport&gt;: 단일 포트 번호</span><span class="sxs-lookup"><span data-stu-id="5d476-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="5d476-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="5d476-240">직접 연결에 대 한 포트 toouse hello를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="5d476-241">기본값은 10251,10252,10253,10254입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="5d476-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="5d476-243">&lt;directports&gt;: 쉼표로 구분된 4개의 포트 목록</span><span class="sxs-lookup"><span data-stu-id="5d476-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-244">키</span><span class="sxs-lookup"><span data-stu-id="5d476-244">Key</span></span></td>
  <td><span data-ttu-id="5d476-245">Hello 에뮬레이터에 대 한 권한 부여 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="5d476-246">키는 64 바이트 벡터의 hello base 64 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="5d476-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="5d476-248">&lt;키&gt;: 키 64 바이트 벡터의 hello base 64 인코딩 이어야 합니다</span><span class="sxs-lookup"><span data-stu-id="5d476-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d476-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="5d476-250">요청 속도 제한 동작을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="5d476-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d476-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d476-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="5d476-253">요청 속도 제한 동작을 사용하지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="5d476-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d476-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="5d476-255">NoUI</span></span></td>
  <td><span data-ttu-id="5d476-256">Hello 에뮬레이터 사용자 인터페이스를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="5d476-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="5d476-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="5d476-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="5d476-259">시작 시 문서 탐색기를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="5d476-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="5d476-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="5d476-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="5d476-262">Hello 분할 된 컬렉션의 최대 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="5d476-263">참조 [hello 컬렉션 수를 변경](#set-partitioncount) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="5d476-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="5d476-265">&lt;partitioncount&gt;: 허용되는 단일 파티션 컬렉션의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="5d476-266">기본값은 25입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-266">Default is 25.</span></span> <span data-ttu-id="5d476-267">허용되는 최대값은 250입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="5d476-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="5d476-269">Hello 기본 분할 된 컬렉션에 대 한 파티션 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="5d476-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="5d476-271">&lt;defaultpartitioncount&gt; 기본값은 25입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="5d476-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="5d476-273">Toohello 에뮬레이터는 네트워크를 통해 액세스 하는 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="5d476-274">/Key 전달 해야 =&lt;key_string&gt; 또는 /KeyFile =&lt;file_name&gt; tooenable 네트워크 액세스.</span><span class="sxs-lookup"><span data-stu-id="5d476-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="5d476-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="5d476-276">또는</span><span class="sxs-lookup"><span data-stu-id="5d476-276">or</span></span><br><br><span data-ttu-id="5d476-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="5d476-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="5d476-279">/AllowNetworkAccess가 사용되는 경우 방화벽 규칙을 조정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5d476-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="5d476-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="5d476-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="5d476-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="5d476-282">새 인증 키를 생성 하 고 toohello 지정된 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="5d476-283">/Key hello 또는 /KeyFile 옵션 hello 생성 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="5d476-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey 파일 경로&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-285">일관성</span><span class="sxs-lookup"><span data-stu-id="5d476-285">Consistency</span></span></td>
  <td><span data-ttu-id="5d476-286">Hello 계정에 대 한 hello 기본 일관성 수준을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="5d476-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="5d476-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="5d476-288">&lt;일관성&gt;: 값 hello 다음 중 하나 여야 합니다 [일관성 수준](consistency-levels.md): 세션, 강력한, 차례로 Eventual, 또는 BoundedStaleness 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="5d476-289">hello 기본값은 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d476-290">?</span><span class="sxs-lookup"><span data-stu-id="5d476-290">?</span></span></td>
  <td><span data-ttu-id="5d476-291">Hello 도움말 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="5d476-292">Hello Azure Cosmos DB 에뮬레이터와 Azure Cosmos DB의 차이점</span><span class="sxs-lookup"><span data-stu-id="5d476-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="5d476-293">Hello Azure Cosmos DB 에뮬레이터 로컬 개발자 워크스테이션에서 실행 되는 에뮬레이트된 환경을 제공 하기 때문에 일부 간 기능 차이 hello 에뮬레이터와 Azure Cosmos DB 계정을 hello 클라우드에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="5d476-294">hello Azure Cosmos DB 에뮬레이터만는 단일 고정 계정과 잘 알려진 마스터 키를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="5d476-295">키 다시 생성 hello Azure Cosmos DB 에뮬레이터의에서 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="5d476-296">hello Azure Cosmos DB 에뮬레이터는 확장 가능한 서비스 아니며 많은 수의 컬렉션을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="5d476-297">hello Azure Cosmos DB 에뮬레이터 시뮬레이션 하지 않습니다 다른 [Azure Cosmos DB 일관성 수준](consistency-levels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="5d476-298">hello Azure Cosmos DB 에뮬레이터 시뮬레이션 하지 않습니다 [다중 지역 복제](distribute-data-globally.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="5d476-299">hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스 (예: 문서 크기 제한, 향상 된 분할 된 컬렉션 저장소)에서 사용할 수 있는 hello 서비스 할당량 재정의 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="5d476-300">Hello Azure Cosmos DB 에뮬레이터의 사본을 수 toodate hello Azure Cosmos DB 서비스와 hello 가장 최근 변경 내용으로 구성 되지 않아, 하세요 [Azure Cosmos DB 용량 플래너](https://www.documentdb.com/capacityplanner) tooaccurately 예상 프로덕션 처리량 (RUs) 응용 프로그램의 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="5d476-301"><a id="set-partitioncount"></a>컬렉션의 hello 수 변경</span><span class="sxs-lookup"><span data-stu-id="5d476-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="5d476-302">기본적으로 too25 단일 파티션 컬렉션 또는 hello Azure Cosmos DB 에뮬레이터를 사용 하 여 1 분할 된 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d476-303">Hello를 수정 하 여 **PartitionCount** 어떠한 조합의 hello 250 단일을 초과 하지 않는 두 개의 파티션 (위치 1 분할 또는 값을 too250 단일 파티션 컬렉션 또는 10 분할 된 컬렉션을 만들 수 있습니다 컬렉션 = 25 단일 파티션 컬렉션).</span><span class="sxs-lookup"><span data-stu-id="5d476-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="5d476-304">Hello 현재 파티션 수를 초과한 후 toocreate 컬렉션을 시도 하면 hello 에뮬레이터 hello 메시지의 뒤에 있는 ServiceUnavailable 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="5d476-305">컬렉션 사용 가능한 toohello Azure Cosmos DB 에뮬레이터의 hello 수 toochange 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="5d476-306">Hello를 마우스 오른쪽 단추로 클릭 하 여 모든 로컬 Azure Cosmos DB 에뮬레이터 데이터를 삭제 **Azure Cosmos DB 에뮬레이터** hello 시스템 트레이 클릭 한 다음에 아이콘 **데이터를 다시 설정...** .</span><span class="sxs-lookup"><span data-stu-id="5d476-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="5d476-307">C:\Users\user_name\AppData\Local\CosmosDBEmulator 폴더에 있는 모든 에뮬레이터 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="5d476-308">Hello를 마우스 오른쪽 단추로 클릭 하 여 열려 있는 모든 인스턴스를 종료 **Azure Cosmos DB 에뮬레이터** hello 시스템 트레이 클릭 한 다음에 아이콘 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="5d476-309">모든 인스턴스 tooexit 1 분을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="5d476-310">최신 버전의 hello hello 설치 [Azure Cosmos DB 에뮬레이터](https://aka.ms/cosmosdb-emulator)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="5d476-311">값을 설정 하 여 hello PartitionCount 플래그로 hello 에뮬레이터를 시작 합니다. < = 250 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="5d476-312">예: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`</span><span class="sxs-lookup"><span data-stu-id="5d476-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d476-313">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5d476-313">Troubleshooting</span></span>

<span data-ttu-id="5d476-314">다음 팁 toohelp hello Azure Cosmos DB 에뮬레이터와 함께 발생할 문제를 해결 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="5d476-315">새 버전의 hello 에뮬레이터를 설치 하 여 오류를 발생 하는 경우 데이터를 다시 설정 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="5d476-316">Hello 시스템 트레이에서 hello Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 데이터를 다시 설정 클릭 하 여 데이터를 다시 설정할 수 있습니다...</span><span class="sxs-lookup"><span data-stu-id="5d476-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="5d476-317">Hello 오류를 해결 하지 않으면 제거 하 고 hello 앱을 다시 설치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="5d476-318">참조 [hello 로컬 에뮬레이터를 제거할](#uninstall) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="5d476-319">Hello Azure Cosmos DB 에뮬레이터가 충돌 하면 c:\Users\user_name\AppData\Local\CrashDumps 폴더에서 덤프 파일을 수집, 압축 및 첨부할 tooan 전자 메일 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="5d476-320">충돌 발생 하는 경우, CosmosDB.StartupEntryPoint.exe hello 관리자 명령 프롬프트에서 다음 명령을 실행 합니다.`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="5d476-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="5d476-321">연결에 문제가 발생 하는 경우 [추적 파일을 수집](#trace-files), 압축 및 첨부할 tooan 전자 메일 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="5d476-322">표시 되 면 한 **서비스를 사용할 수 없는** hello 에뮬레이터에서 실패할 수 tooinitialize hello 네트워크 스택, 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="5d476-323">검사 toosee hello 펄스 있는 경우 보안 클라이언트 또는 Juniper 네트워크 클라이언트를 설치 하 고, 해당 네트워크 필터 드라이버는 hello 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="5d476-324">Hello 문제를 해결 일반적으로 타사 네트워크 필터 드라이버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="5d476-325"><a id="trace-files"></a>추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="5d476-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="5d476-326">toocollect hello 명령 관리 명령 프롬프트에서 다음을 실행 하는 추적을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="5d476-327">`CosmosDB.Emulator.exe /shutdown`</span><span class="sxs-lookup"><span data-stu-id="5d476-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="5d476-328">조사식 hello 시스템 트레이 toomake 있는지 hello 프로그램이 종료 된, 1 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="5d476-329">클릭 해도 **종료** hello Azure Cosmos DB 에뮬레이터 사용자 인터페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="5d476-330">Hello 문제를 재현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-330">Reproduce hello problem.</span></span> <span data-ttu-id="5d476-331">데이터 탐색기 작동 하지 않는 경우만 toowait은 몇 초 toocatch hello 오류에 대 한 브라우저 tooopen hello에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="5d476-332">너무 이동`%ProgramFiles%\Azure Cosmos DB Emulator` hello docdbemulator_000001.etl 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="5d476-333">재현 단계와 함께 hello.etl 파일을 너무 보내기[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="5d476-334"><a id="uninstall"></a>제거의 로컬 에뮬레이터 hello</span><span class="sxs-lookup"><span data-stu-id="5d476-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="5d476-335">Hello의 열려 있는 모든 인스턴스를 종료 hello 시스템 트레이에서 hello Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 종료를 클릭 하 여 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="5d476-336">모든 인스턴스 tooexit 1 분을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="5d476-337">Hello Windows 검색 상자에 입력 **응용 프로그램 및 기능** hello에서을 클릭 하 고 **응용 프로그램 및 기능 (시스템 설정)** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="5d476-338">Hello 앱 목록에서 스크롤합니다 너무**Azure Cosmos DB 에뮬레이터**, 선택, 클릭 **제거**후 확인 하 고 클릭 **제거** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="5d476-339">Hello 앱을 제거할 때 이동 tooC:\Users\<사용자 > \AppData\Local\CosmosDBEmulator 및 delete hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d476-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d476-340">Next steps</span></span>

<span data-ttu-id="5d476-341">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="5d476-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d476-342">설치의 로컬 에뮬레이터 hello</span><span class="sxs-lookup"><span data-stu-id="5d476-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="5d476-343">Rand hello Windows 용 Docker에는 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="5d476-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="5d476-344">요청 인증</span><span class="sxs-lookup"><span data-stu-id="5d476-344">Authenticated requests</span></span>
> * <span data-ttu-id="5d476-345">Hello 에뮬레이터의에서 hello 데이터 탐색기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="5d476-346">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d476-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="5d476-347">에뮬레이터의 hello hello 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="5d476-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="5d476-348">추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="5d476-348">Collected trace files</span></span>

<span data-ttu-id="5d476-349">이 자습서에서는 toouse 무료 로컬 개발을 위한 로컬 에뮬레이터 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="5d476-350">이제 toohello 다음 자습서를 진행 하 고 알아볼 수 있습니다 어떻게 tooexport 에뮬레이터 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="5d476-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d476-351">Hello Azure Cosmos DB 에뮬레이터 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d476-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
