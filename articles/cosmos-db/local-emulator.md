---
title: "Azure Cosmos DB 에뮬레이터를 사용하여 로컬로 개발 | Microsoft Docs"
description: "Azure Cosmos DB 에뮬레이터를 사용하여 Azure 구독을 구입하지 않고도 무료로 로컬에서 응용 프로그램을 개발하고 테스트할 수 있습니다."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="e5a74-104">로컬 개발 및 테스트에 Azure Cosmos DB 에뮬레이터 사용</span><span class="sxs-lookup"><span data-stu-id="e5a74-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="e5a74-105"><strong>이진 파일</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="e5a74-106">MSI 다운로드</span><span class="sxs-lookup"><span data-stu-id="e5a74-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="e5a74-108">Docker 허브</span><span class="sxs-lookup"><span data-stu-id="e5a74-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-109"><strong>Docker 원본</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="e5a74-110">Github</span><span class="sxs-lookup"><span data-stu-id="e5a74-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="e5a74-111">Azure Cosmos DB 에뮬레이터는 개발 목적으로 Azure Cosmos DB 서비스를 에뮬레이트하는 로컬 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="e5a74-112">Azure Cosmos DB 에뮬레이터를 사용하면 Azure 구독을 구입하거나 비용을 발생시키지 않고도 로컬에서 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="e5a74-113">Azure Cosmos DB 에뮬레이터에서 응용 프로그램이 작동하는 방식에 만족하는 경우 Azure Cosmos DB 계정을 클라우드에서 사용하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="e5a74-114">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e5a74-115">에뮬레이터 설치</span><span class="sxs-lookup"><span data-stu-id="e5a74-115">Installing the Emulator</span></span>
> * <span data-ttu-id="e5a74-116">Windows용 Docker에서 에뮬레이터 실행</span><span class="sxs-lookup"><span data-stu-id="e5a74-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="e5a74-117">요청 인증</span><span class="sxs-lookup"><span data-stu-id="e5a74-117">Authenticating requests</span></span>
> * <span data-ttu-id="e5a74-118">에뮬레이터에서 데이터 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="e5a74-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="e5a74-119">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5a74-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="e5a74-120">명령줄에서 에뮬레이터 호출</span><span class="sxs-lookup"><span data-stu-id="e5a74-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="e5a74-121">추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="e5a74-121">Collecting trace files</span></span>

<span data-ttu-id="e5a74-122">Kirill Gavrylyuk가 Azure Cosmos DB 에뮬레이터를 시작하는 방법을 보여 주는 다음 비디오를 시청하는 것으로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e5a74-123">이 비디오는 DocumentDB 에뮬레이터를 참조하지만 비디오를 탭한 후에는 도구 자체의 이름이 Azure Cosmos DB 에뮬레이터로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="e5a74-124">비디오의 모든 정보는 Azure Cosmos DB 에뮬레이터에 대해 정확합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="e5a74-125">에뮬레이터의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="e5a74-125">How the Emulator works</span></span>
<span data-ttu-id="e5a74-126">Azure Cosmos DB 에뮬레이터는 신뢰도 있는 Azure Cosmos DB 서비스의 에뮬레이션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="e5a74-127">JSON 문서 만들기 및 쿼리, 컬렉션 프로비전 및 확장, 저장 프로시저 및 트리거 실행을 비롯하여 Azure Cosmos DB으로 동일한 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="e5a74-128">Azure Cosmos DB 에뮬레이터를 사용하여 응용 프로그램을 개발 및 테스트하고 Azure Cosmos DB에 대한 연결 끝점에 대한 단일 구성을 변경하여 글로벌 규모로 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="e5a74-129">실제 Azure Cosmos DB 서비스의 충실도 높은 로컬 에뮬레이션을 만들었지만 Azure Cosmos DB 에뮬레이터의 구현은 서비스의 구현과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="e5a74-130">예를 들어 Azure Cosmos DB 에뮬레이터는 로컬 파일 시스템(지속성) 및 HTTPS 프로토콜 스택(연결성)과 같은 표준 OS 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="e5a74-131">따라서 전역 복제, 한 자리 밀리초 읽기/쓰기 대기 시간, 튜닝 가능한 일관성 수준 등 Azure 인프라를 기반으로 하는 일부 기능은 Azure Cosmos DB 에뮬레이터를 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="e5a74-132">현재 에뮬레이터의 데이터 탐색기는 DocumentDB API 컬렉션 및 MongoDB 컬렉션 만들기만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="e5a74-133">에뮬레이터의 데이터 탐색기는 현재 테이블 및 그래프 만들기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="e5a74-134">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="e5a74-134">System requirements</span></span>
<span data-ttu-id="e5a74-135">Azure Cosmos DB 에뮬레이터에는 다음과 같은 하드웨어 및 소프트웨어 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="e5a74-136">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="e5a74-136">Software requirements</span></span>
  * <span data-ttu-id="e5a74-137">Windows Server 2012 R2, Windows Server 2016 또는 Windows 10</span><span class="sxs-lookup"><span data-stu-id="e5a74-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="e5a74-138">최소 하드웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="e5a74-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="e5a74-139">2GB RAM</span><span class="sxs-lookup"><span data-stu-id="e5a74-139">2 GB RAM</span></span>
  * <span data-ttu-id="e5a74-140">10GB의 하드 디스크 여유 공간</span><span class="sxs-lookup"><span data-stu-id="e5a74-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="e5a74-141">설치</span><span class="sxs-lookup"><span data-stu-id="e5a74-141">Installation</span></span>
<span data-ttu-id="e5a74-142">[Microsoft 다운로드 센터](https://aka.ms/cosmosdb-emulator)에서 Azure Cosmos DB 에뮬레이터를 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="e5a74-143">Azure Cosmos DB 에뮬레이터를 설치, 구성 및 실행하려면 컴퓨터에 대한 관리 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="e5a74-144">Windows용 Docker에서 실행</span><span class="sxs-lookup"><span data-stu-id="e5a74-144">Running on Docker for Windows</span></span>

<span data-ttu-id="e5a74-145">Azure Cosmos DB 에뮬레이터는 Windows용 Docker에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="e5a74-146">이 에뮬레이터는 Oracle Linux용 Docker에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="e5a74-147">[Windows용 Docker](https://www.docker.com/docker-windows)를 설치한 경우 즐겨 찾는 셸(PowerShell, cmd.exe 등)에서 다음 명령을 실행하여 Docker 허브에서 에뮬레이터 이미지를 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="e5a74-148">이미지를 시작하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="e5a74-149">응답은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="e5a74-150">에뮬레이터가 시작된 후 대화형 셸을 닫으면 에뮬레이터의 컨테이너가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="e5a74-151">클라이언트의 응답에서 끝점 및 마스터 키를 사용하고 SSL 인증서를 호스트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="e5a74-152">SSL 인증서를 가져오려면 관리자 명령 프롬프트에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="e5a74-153">에뮬레이터 시작</span><span class="sxs-lookup"><span data-stu-id="e5a74-153">Start the Emulator</span></span>

<span data-ttu-id="e5a74-154">Azure Cosmos DB 에뮬레이터를 시작하려면 시작 단추를 선택하거나 Windows 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="e5a74-155">**Azure Cosmos DB 에뮬레이터** 입력을 시작하고 응용 프로그램 목록에서 해당 에뮬레이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![시작 단추를 선택하거나 Windows 키를 누르고 **Azure Cosmos DB 에뮬레이터** 입력을 시작한 후 응용 프로그램 목록에서 해당 에뮬레이터를 선택합니다.](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="e5a74-157">에뮬레이터를 실행 하는 경우 Windows 작업 표시줄 알림 영역에 아이콘이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure Cosmos DB 로컬 에뮬레이터 작업 표시줄 알림](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="e5a74-159">기본적으로 Azure Cosmos DB 에뮬레이터는 포트 8081에서 수신 대기하는 로컬 컴퓨터("localhost")에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="e5a74-160">Azure Cosmos DB 에뮬레이터는 기본적으로 `C:\Program Files\Azure Cosmos DB Emulator` 디렉터리에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="e5a74-161">명령줄에서 에뮬레이터를 시작 및 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="e5a74-162">자세한 내용은 [명령줄 도구 참조](#command-line)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a74-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="e5a74-163">데이터 탐색기 시작</span><span class="sxs-lookup"><span data-stu-id="e5a74-163">Start Data Explorer</span></span>

<span data-ttu-id="e5a74-164">Azure Cosmos DB 에뮬레이터를 시작하면 브라우저에서 Azure Cosmos DB 데이터 탐색기가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="e5a74-165">주소는 [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="e5a74-166">탐색기를 닫고 나중에 다시 열고 싶은 경우, 브라우저에서 URL을 열거나 아래와 같이 Windows 트레이 아이콘의 Azure Cosmos DB 에뮬레이터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB의 로컬 에뮬레이터 데이터 탐색기 시작 관리자](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="e5a74-168">업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="e5a74-168">Checking for updates</span></span>
<span data-ttu-id="e5a74-169">데이터 탐색기에 다운로드할 수 있는 새 업데이트가 있는지 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="e5a74-170">Azure Cosmos DB 에뮬레이터의 특정 버전에서 만든 데이터에 다른 버전에서 액세스하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="e5a74-171">데이터를 장기간 보존하려면 Azure Cosmos DB 에뮬레이터 대신 Azure Cosmos DB 계정에 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="e5a74-172">요청 인증</span><span class="sxs-lookup"><span data-stu-id="e5a74-172">Authenticating requests</span></span>
<span data-ttu-id="e5a74-173">클라우드의 Azure Cosmos DB와 마찬가지로 Azure Cosmos DB 에뮬레이터에 대한 모든 요청을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="e5a74-174">Azure Cosmos DB 에뮬레이터는 단일 고정 계정과 마스터 키 인증에 대해 알려진 인증 키를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="e5a74-175">Azure Cosmos DB 에뮬레이터에서 사용할 수 있는 자격 증명은 이 계정과 키뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e5a74-176">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="e5a74-177">Azure Cosmos DB 에뮬레이터에서 지원하는 마스터 키는 에뮬레이터 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="e5a74-178">Azure Cosmos DB 에뮬레이터에서 프로덕션 Azure Cosmos DB 계정 및 키를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e5a74-179">/Key 옵션과 함께 에뮬레이터를 시작한 경우 “C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==” 대신 생성된 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="e5a74-180">또한 Azure Cosmos DB 서비스와 마찬가지로 Azure Cosmos DB 에뮬레이터는 SSL을 통한 보안 통신만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="e5a74-181">로컬 네트워크에서 에뮬레이터 실행</span><span class="sxs-lookup"><span data-stu-id="e5a74-181">Running the emulator on a local network</span></span>

<span data-ttu-id="e5a74-182">로컬 네트워크에서 에뮬레이터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="e5a74-183">네트워크 액세스를 활성화하려면 [명령줄](#command-line-syntax)에 /AllowNetworkAccess 옵션을 지정합니다. 또한 /Key=key_string 또는 /KeyFile=file_name/Key를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="e5a74-184">/GenKeyFile=file_name을 사용하여 미리 설정된 임의 키로 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="e5a74-185">그런 다음 /KeyFile=file_name 또는 /Key=contents_of_file로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="e5a74-186">처음에 네트워크 액세스를 사용하도록 설정하려면 사용자는 에뮬레이터를 종료하고 에뮬레이터의 데이터 디렉터리(C:\Users\user_name\AppData\Local\CosmosDBEmulator)를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="e5a74-187">에뮬레이터를 사용한 개발</span><span class="sxs-lookup"><span data-stu-id="e5a74-187">Developing with the Emulator</span></span>
<span data-ttu-id="e5a74-188">Azure Cosmos DB 에뮬레이터를 데스크톱에서 실행하는 경우 지원되는 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 또는 [Azure Cosmos DB REST API](/rest/api/documentdb/)를 사용하여 에뮬레이터와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="e5a74-189">Azure Cosmos DB 에뮬레이터에는 코드를 작성하지 않고도 DocumentDB 및 MongoDB API 컬렉션을 만들고 문서를 확인 및 편집할 수 있는 기본 제공 데이터 탐색기도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="e5a74-190">[MongoDB에 대한 Azure Cosmos DB 프로토콜 지원](mongodb-introduction.md)을 사용할 경우에는 다음 연결 문자열을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a74-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="e5a74-191">[Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio)와 같은 기존 도구를 사용하여 Azure Cosmos DB 에뮬레이터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e5a74-192">또한 [Azure Cosmos DB 데이터 마이그레이션 도구](https://github.com/azure/azure-documentdb-datamigrationtool)를 사용하여 Azure Cosmos DB 에뮬레이터와 Azure Cosmos DB 서비스 간에 데이터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="e5a74-193">/Key 옵션과 함께 에뮬레이터를 시작한 경우 “C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==” 대신 생성된 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="e5a74-194">기본적으로 Azure Cosmos DB 에뮬레이터를 사용하여 최대 25개의 단일 파티션의 컬렉션 또는 분할된 컬렉션 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="e5a74-195">이 값을 변경하는 방법에 대한 자세한 내용은 [PartitionCount 값 설정](#set-partitioncount)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a74-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="e5a74-196">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5a74-196">Export the SSL certificate</span></span>

<span data-ttu-id="e5a74-197">.NET 언어 및 런타임은 Windows 인증서 저장소를 사용하여 Azure Cosmos DB 로컬 에뮬레이터에 안전하게 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="e5a74-198">다른 언어의 경우 해당 언어만의 인증서 관리 및 사용 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="e5a74-199">Java는 자체의 고유 [인증서 저장소](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)를 사용하고 Python은 [소켓 래퍼](https://docs.python.org/2/library/ssl.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="e5a74-200">Windows 인증서 저장소와 통합되지 않는 런타임 및 언어와 함께 사용할 인증서를 가져오기 위해 Windows 인증서 관리자를 사용하여 인증서를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="e5a74-201">certlm.msc를 실행하거나 [Azure Cosmos DB 에뮬레이터 인증서 내보내기](./local-emulator-export-ssl-certificates.md)의 단계별 지침을 수행하여 이 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="e5a74-202">인증서 관리자가 실행되면 아래에 표시된 대로 개인 인증서를 열고 BASE-64 인코딩 X.509(.cer) 파일로 "DocumentDBEmulatorCertificate"라는 이름의 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB 로컬 에뮬레이터 SSL 인증서](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="e5a74-204">[Java CA 인증서 저장소에 인증서 추가](https://docs.microsoft.com/azure/java-add-certificate-ca-store)의 지침을 따라 X.509 인증서를 Java 인증서 저장소로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="e5a74-205">인증서를 인증서 저장소에 가져온 후 Java 및 MongoDB 응용 프로그램을 Azure Cosmos DB 에뮬레이터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="e5a74-206">Python 및 Node.js SDK에서 에뮬레이터에 연결하면 SSL 확인이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="e5a74-207"><a id="command-line"></a>명령줄 도구 참조</span><span class="sxs-lookup"><span data-stu-id="e5a74-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="e5a74-208">설치 위치에서 명령줄을 사용하여 에뮬레이터를 시작 및 중지하고, 옵션을 구성하고, 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="e5a74-209">명령줄 구문</span><span class="sxs-lookup"><span data-stu-id="e5a74-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="e5a74-210">옵션 목록을 보려면 명령 프롬프트에 `CosmosDB.Emulator.exe /?` 을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="e5a74-211"><strong>옵션</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="e5a74-212"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="e5a74-213"><strong>명령</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="e5a74-214"><strong>인수</strong></span><span class="sxs-lookup"><span data-stu-id="e5a74-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-215">[인수 없음]</span><span class="sxs-lookup"><span data-stu-id="e5a74-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="e5a74-216">기본 설정으로 Azure Cosmos DB 에뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="e5a74-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="e5a74-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-218">[도움말]</span><span class="sxs-lookup"><span data-stu-id="e5a74-218">[Help]</span></span></td>
  <td><span data-ttu-id="e5a74-219">지원되는 명령줄 인수 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="e5a74-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="e5a74-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="e5a74-221">Shutdown</span></span></td>
  <td><span data-ttu-id="e5a74-222">Azure Cosmos DB 에뮬레이터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="e5a74-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="e5a74-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="e5a74-224">DataPath</span></span></td>
  <td><span data-ttu-id="e5a74-225">데이터 파일을 저장할 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="e5a74-226">기본값은 %LocalAppdata%\CosmosDBEmulator입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="e5a74-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-228">&lt;datapath&gt;: 액세스 가능한 경로</span><span class="sxs-lookup"><span data-stu-id="e5a74-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-229">포트</span><span class="sxs-lookup"><span data-stu-id="e5a74-229">Port</span></span></td>
  <td><span data-ttu-id="e5a74-230">에뮬레이터에 사용할 포트 번호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="e5a74-231">기본값은 8081입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="e5a74-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-233">&lt;port&gt;: 단일 포트 번호</span><span class="sxs-lookup"><span data-stu-id="e5a74-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="e5a74-234">MongoPort</span></span></td>
  <td><span data-ttu-id="e5a74-235">MongoDB 호환성 API에 사용할 포트 번호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="e5a74-236">기본값은 10255입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="e5a74-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-238">&lt;mongoport&gt;: 단일 포트 번호</span><span class="sxs-lookup"><span data-stu-id="e5a74-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="e5a74-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="e5a74-240">직접 연결에 사용할 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="e5a74-241">기본값은 10251,10252,10253,10254입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="e5a74-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-243">&lt;directports&gt;: 쉼표로 구분된 4개의 포트 목록</span><span class="sxs-lookup"><span data-stu-id="e5a74-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-244">키</span><span class="sxs-lookup"><span data-stu-id="e5a74-244">Key</span></span></td>
  <td><span data-ttu-id="e5a74-245">에뮬레이터에 대한 권한 부여 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-245">Authorization key for the emulator.</span></span> <span data-ttu-id="e5a74-246">키는 64바이트 벡터의 base 64 인코딩이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="e5a74-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-248">&lt;key&gt;: 키는 64바이트 벡터의 base 64 인코딩이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="e5a74-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="e5a74-250">요청 속도 제한 동작을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="e5a74-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="e5a74-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="e5a74-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="e5a74-253">요청 속도 제한 동작을 사용하지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="e5a74-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="e5a74-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="e5a74-255">NoUI</span></span></td>
  <td><span data-ttu-id="e5a74-256">에뮬레이터 사용자 인터페이스를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="e5a74-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="e5a74-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="e5a74-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="e5a74-259">시작 시 문서 탐색기를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="e5a74-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="e5a74-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="e5a74-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="e5a74-262">분할된 컬렉션의 최대 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="e5a74-263">자세한 내용은 [컬렉션 수 변경](#set-partitioncount)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a74-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="e5a74-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-265">&lt;partitioncount&gt;: 허용되는 단일 파티션 컬렉션의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="e5a74-266">기본값은 25입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-266">Default is 25.</span></span> <span data-ttu-id="e5a74-267">허용되는 최대값은 250입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="e5a74-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="e5a74-269">분할된 컬렉션에 대한 기본 파티션 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="e5a74-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-271">&lt;defaultpartitioncount&gt; 기본값은 25입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="e5a74-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="e5a74-273">네트워크를 통해 에뮬레이터에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="e5a74-274">/Key=&lt;key_string&gt; 또는 /KeyFile=&lt;file_name&gt;을 전달하여 네트워크 액세스를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="e5a74-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="e5a74-276">또는</span><span class="sxs-lookup"><span data-stu-id="e5a74-276">or</span></span><br><br><span data-ttu-id="e5a74-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="e5a74-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="e5a74-279">/AllowNetworkAccess가 사용되는 경우 방화벽 규칙을 조정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e5a74-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="e5a74-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="e5a74-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="e5a74-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="e5a74-282">새 인증 키를 생성하고 지정된 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="e5a74-283">생성된 키를 /Key 또는 /KeyFile 옵션과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="e5a74-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-285">일관성</span><span class="sxs-lookup"><span data-stu-id="e5a74-285">Consistency</span></span></td>
  <td><span data-ttu-id="e5a74-286">계정의 기본 일관성 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="e5a74-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="e5a74-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="e5a74-288">&lt;일관성&gt;: 값은 Session, Strong, Eventual 또는 BoundedStaleness의 [일관성 수준](consistency-levels.md) 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="e5a74-289">기본값은 Session입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e5a74-290">?</span><span class="sxs-lookup"><span data-stu-id="e5a74-290">?</span></span></td>
  <td><span data-ttu-id="e5a74-291">도움말 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="e5a74-292">Azure Cosmos DB 에뮬레이터와 Azure Cosmos DB 간 차이점</span><span class="sxs-lookup"><span data-stu-id="e5a74-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="e5a74-293">Azure Cosmos DB 에뮬레이터는 로컬 개발자 워크스테이션에서 실행되는 에뮬레이트된 환경을 제공하기 때문에 클라우드의 Azure Cosmos DB 계정과 기능 면에서 몇 가지 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="e5a74-294">Azure Cosmos DB 에뮬레이터는 단일 고정 계정과 알려진 마스터 키만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="e5a74-295">Azure Cosmos DB 에뮬레이터에서는 키를 다시 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="e5a74-296">Azure Cosmos DB 에뮬레이터는 확장 가능한 서비스가 아니며 많은 컬렉션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="e5a74-297">Azure Cosmos DB 에뮬레이터는 여러 [Azure Cosmos DB 일관성 수준](consistency-levels.md)을 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="e5a74-298">Azure Cosmos DB 에뮬레이터는 [다중 지역 복제](distribute-data-globally.md)를 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="e5a74-299">Azure Cosmos DB 에뮬레이터는 Azure Cosmos DB 서비스에서 사용할 수 있는 서비스 할당량 재정의(예: 문서 크기 제한, 향상된 분할된 컬렉션 저장소)를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="e5a74-300">Azure Cosmos DB 에뮬레이터의 복사본은 최신 Azure Cosmos DB 서비스가 포함된 가장 최근의 변경 사항이 적용된 최신 에뮬레이터가 아닐 수 있으므로 [Azure Cosmos DB Capacity Planner](https://www.documentdb.com/capacityplanner)를 실행하여 응용 프로그램에 요구되는 프로덕션 처리량(RU)을 정확하게 예측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="e5a74-301"><a id="set-partitioncount"></a>컬렉션 수 변경</span><span class="sxs-lookup"><span data-stu-id="e5a74-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="e5a74-302">기본적으로 Azure Cosmos DB 에뮬레이터를 사용하여 최대 25개의 단일 파티션의 컬렉션 또는 분할된 컬렉션 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e5a74-303">**PartitionCount** 값을 수정하여는 최대 250개의 단일 파티션 컬렉션 또는 10개의 분할된 컬렉션을 만들거나, 합쳐서 250개의 단일 파티션을 초과하지 않는 두 컬렉션 조합을 만들 수 있습니다(분할된 컬렉션 1개 = 단일 파티션 컬렉션 25개).</span><span class="sxs-lookup"><span data-stu-id="e5a74-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="e5a74-304">현재 파티션 수가 초과된 후에 컬렉션을 만들려고 하면 에뮬레이터에서 다음 메시지와 함께 ServiceUnavailable 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="e5a74-305">Azure Cosmos DB 에뮬레이터에서 사용할 수 있는 컬렉션의 수를 변경하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="e5a74-306">시스템 트레이에서 **Azure Cosmos DB 에뮬레이터** 아이콘을 마우스 오른쪽 단추로 클릭한 다음 **데이터 다시 설정...**을 클릭하여 모든 로컬 Azure Cosmos DB 에뮬레이터 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="e5a74-307">C:\Users\user_name\AppData\Local\CosmosDBEmulator 폴더에 있는 모든 에뮬레이터 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="e5a74-308">**Azure Cosmos DB 에뮬레이터** 아이콘을 마우스 오른쪽 단추로 클릭한 다음 **마침**을 클릭하여 열려 있는 모든 인스턴스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="e5a74-309">모든 인스턴스를 종료하는 데는 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="e5a74-310">최신 버전의 [Azure Cosmos DB 에뮬레이터](https://aka.ms/cosmosdb-emulator)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="e5a74-311">250 이하의 값을 설정하여 PartitionCount 플래그로 에뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="e5a74-312">예: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`</span><span class="sxs-lookup"><span data-stu-id="e5a74-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e5a74-313">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e5a74-313">Troubleshooting</span></span>

<span data-ttu-id="e5a74-314">다음은 Azure Cosmos DB 에뮬레이터에서 발생하는 문제 해결을 도와주는 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="e5a74-315">새 버전의 에뮬레이터를 설치했는데 오류가 발생하는 경우 데이터를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="e5a74-316">시스템 트레이에서 Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭한 다음, 데이터 다시 설정...을 클릭하여 데이터를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="e5a74-317">오류가 해결되지 않으면 앱을 제거하고 다시 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="e5a74-318">지침은 [로컬 에뮬레이터 제거](#uninstall)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a74-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="e5a74-319">Azure Cosmos DB 에뮬레이터가 충돌하는 경우 c:\Users\user_name\AppData\Local\CrashDumps 폴더에서 덤프 파일을 수집하고, 압축하고, 전자 메일에 첨부하여 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="e5a74-320">CosmosDB.StartupEntryPoint.exe에서 충돌을 경험하는 경우 관리자 명령 프롬프트에서 다음 명령을 실행합니다. `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="e5a74-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="e5a74-321">연결 문제가 발생하는 경우 [추적 파일을 수집](#trace-files)하고, 압축하고, 전자 메일에 첨부하여 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="e5a74-322">**서비스를 사용할 수 없음** 메시지가 나타나는 경우 에뮬레이터에서 네트워크 스택을 초기화하지 못했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="e5a74-323">해당 네트워크 필터 드라이버로 인해 문제가 발생할 수 있으므로 Pulse 보안 클라이언트 또는 Juniper 네트워크 클라이언트를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="e5a74-324">일반적으로 타사 네트워크 필터 드라이버를 제거하면 문제가 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="e5a74-325"><a id="trace-files"></a>추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="e5a74-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="e5a74-326">디버깅 추적을 수집하려면 관리 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="e5a74-327">`CosmosDB.Emulator.exe /shutdown`</span><span class="sxs-lookup"><span data-stu-id="e5a74-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="e5a74-328">프로그램이 종료되었는지 시스템 트레이를 확인합니다. 프로그램 종료에 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="e5a74-329">Azure Cosmos DB 에뮬레이터 사용자 인터페이스에서 **종료**를 클릭해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="e5a74-330">문제를 재현합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-330">Reproduce the problem.</span></span> <span data-ttu-id="e5a74-331">데이터 탐색기가 작동하지 않는 경우 브라우저가 몇 초 간 열리고 오류를 catch할 때까지 기다리면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="e5a74-332">`%ProgramFiles%\Azure Cosmos DB Emulator`로 이동하여 docdbemulator_000001.etl 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="e5a74-333">재현 단계와 마찬가지로 디버깅을 위해 .etl 파일을 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="e5a74-334"><a id="uninstall"></a>로컬 에뮬레이터 제거</span><span class="sxs-lookup"><span data-stu-id="e5a74-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="e5a74-335">시스템 트레이에서 Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭한 다음 마침을 클릭하여 로컬 에뮬레이터의 열려 있는 모든 인스턴스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="e5a74-336">모든 인스턴스를 종료하는 데는 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="e5a74-337">Windows 검색 상자에 **앱 및 기능**을 입력하고 **앱 및 기능(시스템 설정)** 결과를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="e5a74-338">앱 목록에서 **Azure Cosmos DB 에뮬레이터**로 스크롤하여 선택하고, **제거**를 클릭한 다음, 확인하고 **제거**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="e5a74-339">앱이 제거되면 C:\Users\<user>\AppData\Local\CosmosDBEmulator로 이동하여 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5a74-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5a74-340">Next steps</span></span>

<span data-ttu-id="e5a74-341">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e5a74-342">로컬 에뮬레이터 설치</span><span class="sxs-lookup"><span data-stu-id="e5a74-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="e5a74-343">Windows용 Docker에서 에뮬레이터 실행</span><span class="sxs-lookup"><span data-stu-id="e5a74-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="e5a74-344">요청 인증</span><span class="sxs-lookup"><span data-stu-id="e5a74-344">Authenticated requests</span></span>
> * <span data-ttu-id="e5a74-345">에뮬레이터에서 데이터 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="e5a74-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="e5a74-346">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5a74-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="e5a74-347">명령줄에서 에뮬레이터 호출</span><span class="sxs-lookup"><span data-stu-id="e5a74-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="e5a74-348">추적 파일 수집</span><span class="sxs-lookup"><span data-stu-id="e5a74-348">Collected trace files</span></span>

<span data-ttu-id="e5a74-349">이 자습서에서는 무료 로컬 개발을 위해 로컬 에뮬레이터를 사용하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="e5a74-350">이제 다음 자습서로 진행하여 에뮬레이터 SSL 인증서를 내보내는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a74-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5a74-351">Azure Cosmos DB 에뮬레이터 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5a74-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
