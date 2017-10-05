---
title: "Power BI에서 Apache Storm 사용 - Azure HDInsight | Microsoft Docs"
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="9e78d-103">Power BI를 사용하여 Apache Storm 토폴로지에서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="9e78d-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="9e78d-104">Power BI를 사용하면 데이터를 보고서로 시각적으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="9e78d-105">이 문서는 HDInsight의 Apache Storm을 사용하여 Power BI에 대한 데이터를 생성하는 방법의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="9e78d-106">이 문서의 단계는 Visual Studio가 있는 Windows 개발 환경에서 진행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="9e78d-107">컴파일된 프로젝트는 Linux 기반 HDInsight 클러스터로 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9e78d-108">2016년 10월 28일 이후 생성된 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="9e78d-109">Linux 기반 클러스터에 C# 토폴로지를 사용하려면 프로젝트에 사용되는 Microsoft.SCP.Net.SDK NuGet 패키지를 0.10.0.6 버전 이상으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="9e78d-110">패키지 버전은 HDInsight에 설치된 Storm의 주 버전과도 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="9e78d-111">예를 들어 HDInsight에서 Storm 버전 3.3 및 3.4는 Storm 버전 0.10.x를 사용하는 반면, HDInsight 3.5는 Storm 1.0.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="9e78d-112">Linux 기반 클러스터의 C# 토폴로지는 .NET 4.5를 사용해야 하며 Mono를 사용하여 HDInsight 클러스터에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="9e78d-113">대부분의 항목이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-113">Most things work.</span></span> <span data-ttu-id="9e78d-114">하지만 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 문서에서 잠재적인 비호환성이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="9e78d-115">Linux 기반 또는 Windows 기반 HDInsight로 작동하는 이 프로젝트의 Java 버전에 대해서는 [HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e78d-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e78d-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9e78d-116">Prerequisites</span></span>

* <span data-ttu-id="9e78d-117">[Power BI](https://powerbi.com) 액세스 권한이 있는 Azure Active Directory 사용자</span><span class="sxs-lookup"><span data-stu-id="9e78d-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="9e78d-118">HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="9e78d-118">An HDInsight cluster.</span></span> <span data-ttu-id="9e78d-119">자세한 내용은 [HDInsight에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e78d-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9e78d-120">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e78d-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e78d-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9e78d-122">Visual Studio(다음 버전 중 하나)</span><span class="sxs-lookup"><span data-stu-id="9e78d-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="9e78d-123">Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="9e78d-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="9e78d-124">Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="9e78d-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="9e78d-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9e78d-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="9e78d-126">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="9e78d-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="9e78d-127">HDInsight Tools for Visual Studio: 설치 정보는 [HDInsight Tools for Visual Studio 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e78d-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9e78d-128">작동 방법</span><span class="sxs-lookup"><span data-stu-id="9e78d-128">How it works</span></span>

<span data-ttu-id="9e78d-129">이 예제에서는 IIS(인터넷 정보 서비스) 로그 데이터를 무작위로 생성하는 C# Storm 토폴로지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="9e78d-130">이 데이터는 SQL 데이터베이스에 기록되고 해당 위치에서 Power BI에 보고서를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="9e78d-131">다음 파일은 이 예제의 주요 기능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="9e78d-132">**SqlAzureBolt.cs**: SQL 데이터베이스에 대한 Storm 토폴로지에서 생성된 정보를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="9e78d-133">**IISLogsTable.sql**: 데이터가 저장되어 있는 데이터베이스를 생성하는 데 사용되는 Transact-SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="9e78d-134">HDInsight 클러스터에서 토폴로지를 시작하기 전에 SQL Database에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="9e78d-135">예제 다운로드</span><span class="sxs-lookup"><span data-stu-id="9e78d-135">Download the example</span></span>

<span data-ttu-id="9e78d-136">[HDInsight C# Storm Power BI 예제](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="9e78d-137">다운로드하려면 [git](http://git-scm.com/)를 사용하여 포크/복제하거나, **다운로드** 링크를 사용하여 .zip 보관 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="9e78d-138">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="9e78d-138">Create a database</span></span>

1. <span data-ttu-id="9e78d-139">데이터베이스를 만들려면 [SQL Database 자습서](../sql-database/sql-database-get-started.md) 문서의 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="9e78d-140">[Visual Studio와 함께 SQL Database에 연결](../sql-database/sql-database-connect-query.md) 문서의 단계를 수행하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="9e78d-141">개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="9e78d-142">다운로드한 프로젝트에 포함된 **IISLogsTable.sql** 파일의 내용을 쿼리 창에 붙여 넣은 다음 Ctrl + Shift + E를 사용하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="9e78d-143">명령이 성공적으로 완료되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="9e78d-144">샘플 구성</span><span class="sxs-lookup"><span data-stu-id="9e78d-144">Configure the sample</span></span>

1. <span data-ttu-id="9e78d-145">[Azure 포털](https://portal.azure.com)에서 SQL 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="9e78d-146">SQL 데이터베이스 블레이드의 **Essentials** 섹션에서 **데이터베이스 연결 문자열 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="9e78d-147">표시되는 목록에서 **ADO.NET(SQL 인증)** 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="9e78d-148">Visual Studio에서 샘플을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="9e78d-149">**솔루션 탐색기**에서 **App.config** 파일을 열고 다음 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="9e78d-150">**##TOBEFILLED##** 값을 이전 단계에서 복사된 데이터베이스 연결 문자열과 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="9e78d-151">**{your\_username}** 및 **{your\_password}**를 데이터베이스에 대한 사용자 이름 및 암호와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="9e78d-152">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="9e78d-153">샘플 배포</span><span class="sxs-lookup"><span data-stu-id="9e78d-153">Deploy the sample</span></span>

1. <span data-ttu-id="9e78d-154">**솔루션 탐색기**에서 **StormToSQL** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight에서 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="9e78d-155">**Storm 클러스터** 드롭다운 대화 상자에서 HDInsight 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e78d-156">**Storm 클러스터** 드롭다운을 서버 이름으로 채우는 데 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="9e78d-157">메시지가 표시되면 Azure 구독에 대한 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="9e78d-158">하나 이상의 구독이 있는 경우 HDInsight 클러스터의 Storm을 포함하는 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="9e78d-159">토폴로지가 제출되었으면 __토폴로지 뷰어__가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="9e78d-160">이 토폴로지를 보려면 목록에서 SqlAzureWriterTopology 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![토폴로지가 선택된 토폴로지](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="9e78d-162">이 보기를 사용하여 토폴로지에 대한 정보를 확인하거나 항목(예: SqlAzureBolt)을 두 번 클릭하여 토폴로지에서 구성 요소와 관련된 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="9e78d-163">몇 분 동안 토폴로지를 실행한 후에 데이터베이스를 만드는 데 사용한 SQL 쿼리 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="9e78d-164">기존 문을 다음 쿼리로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="9e78d-165">Ctrl + Shift + E를 사용하여 쿼리를 실행하면 다음 데이터와 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="9e78d-166">이 데이터는 Storm 토폴로지에서 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="9e78d-167">보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="9e78d-167">Create a report</span></span>

1. <span data-ttu-id="9e78d-168">Power BI용 [Azure SQL 데이터베이스 커넥터](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) 에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="9e78d-169">**데이터베이스** 내에서 **가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="9e78d-170">**Azure SQL Database**를 선택한 다음 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e78d-171">계속하려면 Power BI Desktop을 다운로드하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="9e78d-172">이렇게 하려면 다음 단계를 수행하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="9e78d-173">Power BI Desktop을 열고 __Get Data__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="9e78d-174">2  __Azure__를 선택한 다음 __Azure SQL Database__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="9e78d-175">정보를 입력하여 Azure SQL 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="9e78d-176">[Azure Portal](https://portal.azure.com)에 방문하고 SQL 데이터베이스를 선택하여 이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e78d-177">연결 대화 상자에서 **고급 옵션 사용** 을 사용하여 새로 고침 간격 및 사용자 지정 필터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="9e78d-178">연결한 후에 연결한 데이터베이스와 동일한 이름을 가진 새 데이터 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="9e78d-179">데이터 집합을 선택하여 보고서를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="9e78d-180">**필드**에서 **IISLOGS** 항목을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="9e78d-181">URI 스템을 나열하는 보고서를 만들려면 **URISTEM** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![보고서 만들기](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="9e78d-183">다음으로 **메서드** 보고서를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="9e78d-184">보고서는 HTTP 요청에 사용된 형태소 및 해당 HTTP 메서드를 목록에 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![메서드 데이터 추가](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="9e78d-186">**시각화** 열에서 **필드** 아이콘을 선택한 다음 **값** 섹션의 **메서드** 옆에 있는 아래쪽 화살표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="9e78d-187">URI에 액세스한 횟수를 표시하려면 **Count**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![메서드의 수 변경](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="9e78d-189">다음으로 **누적 세로 막대형 차트** 를 선택하여 정보가 표시되는 방식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![누적된 차트 변경](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="9e78d-191">보고서를 저장하려면 **저장**을 선택하고 보고서의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="9e78d-192">토폴로지 중지</span><span class="sxs-lookup"><span data-stu-id="9e78d-192">Stop the topology</span></span>

<span data-ttu-id="9e78d-193">토폴로지는 사용자가 중지하거나 HDInsight 클러스터에서 Storm을 삭제할 때까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="9e78d-194">토폴로지를 중지하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="9e78d-195">Visual Studio에서 토폴로지 뷰어로 돌아가서 토폴로지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="9e78d-196">**Kill** 단추를 선택하여 토폴로지를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-196">Select the **Kill** button to stop the topology.</span></span>

    ![토폴로지 요약의 Kill 단추](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="9e78d-198">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="9e78d-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="9e78d-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e78d-199">Next steps</span></span>

<span data-ttu-id="9e78d-200">이 문서에서는 Storm 토폴로지에서 SQL 데이터베이스로 데이터를 보낸 다음 Power BI를 사용하여 데이터를 시각화하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9e78d-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="9e78d-201">HDInsight에서 Storm을 사용하여 다른 Azure 기술을 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e78d-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="9e78d-202">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="9e78d-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
