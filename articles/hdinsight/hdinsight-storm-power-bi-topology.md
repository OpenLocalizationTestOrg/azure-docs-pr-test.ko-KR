---
title: "Power bi-Azure HDInsight의 Apache Storm aaaUse | Microsoft Docs"
description: "HDInsight의 Apache Storm 클러스터에서 실행 중인 C# 토폴로지로부터 데이터를 사용하여 Power BI 보고서를 만듭니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="d4feb-103">Apache Storm 토폴로지에서 Power BI toovisualize 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="d4feb-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="d4feb-104">Power BI 보고서로 데이터를 표시 하는 toovisually를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="d4feb-105">이 문서는 방법의 예에서는 Power BI에 대 한 HDInsight toogenerate 데이터에서 Apache Storm toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="d4feb-106">hello이 문서의 단계에 의존 Visual Studio와 함께 Windows 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="d4feb-107">hello 컴파일된 프로젝트 제출 된 tooa Linux 기반 HDInsight 클러스터 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d4feb-108">2016년 10월 28일 이후 생성된 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="d4feb-109">Linux 기반 클러스터에서 업데이트 hello 프로젝트 tooversion 0.10.0.6 프로그램에서 사용 되는 또는 더 높은 Microsoft.SCP.Net.SDK NuGet 패키지는 C# 토폴로지 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="d4feb-110">또한 hello 버전의 hello 패키지 hello HDInsight에 설치 된 Storm의 주 버전을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="d4feb-111">예를 들어 HDInsight에서 Storm 버전 3.3 및 3.4는 Storm 버전 0.10.x를 사용하는 반면, HDInsight 3.5는 Storm 1.0.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="d4feb-112">Linux 기반 클러스터에서 C# 토폴로지는.NET 4.5를 사용 하 고 모노 toorun hello HDInsight 클러스터에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="d4feb-113">대부분의 항목이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-113">Most things work.</span></span> <span data-ttu-id="d4feb-114">하지만 Hello를 확인 해야 [모노 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 잠재적인 호환성 문제에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="d4feb-115">Linux 기반 또는 Windows 기반 HDInsight로 작동하는 이 프로젝트의 Java 버전에 대해서는 [HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4feb-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4feb-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4feb-116">Prerequisites</span></span>

* <span data-ttu-id="d4feb-117">[Power BI](https://powerbi.com) 액세스 권한이 있는 Azure Active Directory 사용자</span><span class="sxs-lookup"><span data-stu-id="d4feb-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="d4feb-118">HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="d4feb-118">An HDInsight cluster.</span></span> <span data-ttu-id="d4feb-119">자세한 내용은 [HDInsight에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4feb-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d4feb-120">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4feb-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4feb-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d4feb-122">Visual Studio (hello 버전을 다음 중 하나)</span><span class="sxs-lookup"><span data-stu-id="d4feb-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="d4feb-123">Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d4feb-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="d4feb-124">Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d4feb-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="d4feb-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d4feb-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="d4feb-126">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="d4feb-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="d4feb-127">Visual Studio 용 HDInsight 도구 hello: 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 설치 정보에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d4feb-128">작동 방법</span><span class="sxs-lookup"><span data-stu-id="d4feb-128">How it works</span></span>

<span data-ttu-id="d4feb-129">이 예제에서는 IIS(인터넷 정보 서비스) 로그 데이터를 무작위로 생성하는 C# Storm 토폴로지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="d4feb-130">이 데이터 tooa SQL 데이터베이스에 기록 되며 여기에서 Power BI에서 사용 되는 toogenerate 보고서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="d4feb-131">이 예의 파일 구현 hello 주요 기능을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="d4feb-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="d4feb-132">**SqlAzureBolt.cs**: hello 스톰 토폴로지 tooSQL 데이터베이스에서에서 생성 한 정보를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="d4feb-133">**IISLogsTable.sql**: hello 데이터에 저장 되어 있는 hello Transact SQL 문 사용 toogenerate hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="d4feb-134">SQL 데이터베이스에서 HDInsight 클러스터에서 hello 토폴로지를 시작 하기 전에 hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="d4feb-135">Hello 예제를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-135">Download hello example</span></span>

<span data-ttu-id="d4feb-136">Hello 다운로드 [HDInsight C# 스톰 Power BI 예제](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="d4feb-137">toodownload, 하거나 포크/복제를 사용 하 여 [git](http://git-scm.com/), 하거나 hello를 사용 하 여 **다운로드** 링크 toodownload hello 보관의.zip 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="d4feb-138">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d4feb-138">Create a database</span></span>

1. <span data-ttu-id="d4feb-139">데이터베이스 toocreate hello 단계를 사용 하 여 hello에 [SQL 데이터베이스 자습서](../sql-database/sql-database-get-started.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="d4feb-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="d4feb-140">Hello에서 단계를 다음 hello 하 여 연결 toohello 데이터베이스 [Visual Studio를 사용 하 여 tooa SQL 데이터베이스 연결](../sql-database/sql-database-connect-query.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="d4feb-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="d4feb-141">개체 탐색기에서 hello 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="d4feb-142">Hello의 hello 내용 붙여넣기 **IISLogsTable.sql** hello에 포함 된 파일 hello 쿼리 창에 프로젝트를 다운로드 한 다음 Ctrl + Shift + E tooexecute hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="d4feb-143">Hello 명령을 성공적으로 완료 하는 메시지를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="d4feb-144">Hello 샘플 구성</span><span class="sxs-lookup"><span data-stu-id="d4feb-144">Configure hello sample</span></span>

1. <span data-ttu-id="d4feb-145">Hello에서 [Azure 포털](https://portal.azure.com), SQL 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="d4feb-146">Hello에서 **Essentials** hello SQL 데이터베이스 블레이드, 선택의 섹션 **데이터베이스 연결 문자열 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="d4feb-147">Hello 목록이 표시 되 면 복사 hello **ADO.NET (SQL 인증)** 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="d4feb-148">Visual Studio에서 hello 샘플을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="d4feb-149">**솔루션 탐색기**개방형 hello **App.config** 파일을 선택한 다음 hello 다음 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="d4feb-150">Hello 대체 **# # TOBEFILLED # #** hello 이전 단계에서 복사한 값 hello 데이터베이스 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="d4feb-151">대체 **{프로그램\_사용자 이름}** 및 **{프로그램\_암호}** hello 이름과 hello 데이터베이스에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="d4feb-152">저장 하 고 hello 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="d4feb-153">Hello 예제 배포</span><span class="sxs-lookup"><span data-stu-id="d4feb-153">Deploy hello sample</span></span>

1. <span data-ttu-id="d4feb-154">**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **StormToSQL** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d4feb-155">Hello에서 HDInsight 클러스터를 선택 hello **Storm 클러스터** 드롭다운 대화입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4feb-156">Hello에 대 한 몇 초 정도 **Storm 클러스터** 드롭다운 toopopulate 서버 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="d4feb-157">메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="d4feb-158">구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d4feb-159">Hello 토폴로지가 제출 될 때 hello __토폴로지 뷰어__ 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="d4feb-160">tooview이 토폴로지, hello 목록에서 선택 hello SqlAzureWriterTopology 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![선택한 hello 토폴로지 hello 토폴로지](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="d4feb-162">이 보기 toosee 정보를 사용 하 여 hello 토폴로지에서 하거나 hello 토폴로지는 항목 (예: hello SqlAzureBolt) toosee 정보 특정 tooa 구성 요소를 두 번 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="d4feb-163">Hello 후 토폴로지 실행 몇 분 동안 반환 toohello SQL 쿼리 창 toocreate hello 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="d4feb-164">다음 쿼리에서 hello hello 기존 문을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="d4feb-165">Ctrl + Shift를 사용 하 여 + E tooexecute hello 쿼리의 결과 유사한 toohello 같은 데이터가 수신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="d4feb-166">이 데이터 hello 스톰 토폴로지에서 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="d4feb-167">보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="d4feb-167">Create a report</span></span>

1. <span data-ttu-id="d4feb-168">Toohello 연결 [Azure SQL 데이터베이스 커넥터](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="d4feb-169">**데이터베이스** 내에서 **가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="d4feb-170">**Azure SQL Database**를 선택한 다음 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4feb-171">Toodownload hello Power BI Desktop toocontinue를 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="d4feb-172">이 경우 다음 단계 tooconnect hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="d4feb-173">Power BI Desktop을 열고 __Get Data__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="d4feb-174">2  __Azure__를 선택한 다음 __Azure SQL Database__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="d4feb-175">Hello 정보 tooconnect tooyour Azure SQL 데이터베이스를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="d4feb-176">Hello를 방문 하 여이 정보를 찾을 수 [Azure 포털](https://portal.azure.com) SQL 데이터베이스를 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4feb-177">사용 하 여 사용자 지정 필터 및 hello 새로 고침 간격을 설정할 수도 있습니다 **고급 옵션을 사용 하도록 설정** hello에서 대화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="d4feb-178">를 연결한 후 새 데이터 집합 이름과 같은 이름을 hello 데이터베이스에 연결 하는 hello로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="d4feb-179">Hello dataset toobegin 보고서 디자인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="d4feb-180">**필드**, hello 확장 **IISLOGS** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="d4feb-181">hello 확인란을 선택 하는 보고서 목록 hello URI는 형태소 분석 toocreate **URISTEM**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![보고서 만들기](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="d4feb-183">다음으로 끌어 **메서드** toohello 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="d4feb-184">hello 보고서 업데이트 toolist hello 생기고 hello 해당 HTTP 메서드 hello HTTP 요청에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![hello 메서드 데이터를 추가합니다.](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="d4feb-186">Hello에서 **시각화** 열, 선택 hello **필드** 아이콘을 선택한 후 hello 아래쪽 화살표 옆 너무**메서드** hello에 **값**섹션.</span><span class="sxs-lookup"><span data-stu-id="d4feb-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="d4feb-187">URI에 몇 번의 개수에 액세스 하는 toodisplay 선택 **Count**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![메서드의 tooa 수 변경](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="d4feb-189">Hello를 다음으로, 선택 **누적 세로 막대형 차트** toochange 어떻게 hello 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![변경 tooa 누적된 차트](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="d4feb-191">선택 toosave hello 보고서 **저장** hello 보고서에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d4feb-192">Hello 토폴로지를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-192">Stop hello topology</span></span>

<span data-ttu-id="d4feb-193">hello 토폴로지는 중지 하거나 hello 스톰 HDInsight 클러스터에서 삭제 될 때까지 toorun를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="d4feb-194">toostop은 토폴로지 hello에 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="d4feb-195">Visual Studio에서 toohello 토폴로지 뷰어를 반환 하 고 hello 토폴로지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="d4feb-196">선택 hello **Kill** 단추 toostop hello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill hello 토폴로지 요약에서 단추](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="d4feb-198">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="d4feb-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d4feb-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4feb-199">Next steps</span></span>

<span data-ttu-id="d4feb-200">이 문서에서 배운 어떻게 스톰 토폴로지 tooSQL 데이터베이스에서에서 toosend 데이터를 시각화 하 여 Power BI를 사용 하 여 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d4feb-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="d4feb-201">방법에 대 한 HDInsight에서 Storm를 사용 하 여 다른 Azure 기술로 toowork hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d4feb-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="d4feb-202">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="d4feb-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
