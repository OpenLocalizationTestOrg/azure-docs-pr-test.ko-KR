---
title: "Hadoop aaaRun Azure Cosmos DB 및 HDInsight를 사용 하 여 작업 | Microsoft Docs"
description: "Cosmos DB Azure 및 Azure HDInsight toorun 간단한 Hive, Pig 및 MapReduce 작업 하는 방법에 대해 알아봅니다."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="f4194-103"><a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB 및 HDInsight를 사용하여 Apache Hive, Pig 또는 Hadoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4194-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="f4194-104">이 자습서에서는 어떻게 toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], 및 [Apache Hadoop] [ apache-hadoop] Cosmos DB Hadoop 커넥터와 함께 Azure HDInsight의 MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="f4194-105">Cosmos DB의 Hadoop 커넥터는 소스 및 Hive, Pig 및 MapReduce 작업에 대 한 싱크 Cosmos DB tooact을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="f4194-106">이 자습서는 Hadoop 작업에 대 한 hello 데이터 원본 및 대상으로 Cosmos DB를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="f4194-107">이 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="f4194-108">Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에서 데이터를 로드하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="f4194-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="f4194-109">Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에 데이터를 저장하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="f4194-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="f4194-110">다음 비디오에서는 Cosmos DB 및 HDInsight를 사용 하 여 하이브 작업을 통해 실행 위치 hello를 시청 하 여 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="f4194-111">에서 반환 toothis 문서 hello Cosmos DB 데이터에 분석 작업을 실행 하는 방법을 대 한 전체 세부 정보를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="f4194-112">이 자습서에서는 사용자가 이전에 Apache Hadoop, Hive 및/또는 Pig를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="f4194-113">새 tooApache Hadoop, Hive, 및 Pig 인 경우 hello 방문 하는 것이 좋습니다 [Apache Hadoop 설명서][apache-hadoop-doc]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="f4194-114">또한 이 자습서에서는 이전에 Cosmos DB를 사용한 경험이 있으며 Cosmos DB 계정이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="f4194-115">새 tooCosmos DB 인지는 Cosmos DB 계정이 없는 경우 확인 하세요 우리의 [시작] [ getting-started] 페이지.</span><span class="sxs-lookup"><span data-stu-id="f4194-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="f4194-116">자습서 hello 및 Hive, Pig 및 MapReduce tooget hello 전체 샘플 PowerShell 스크립트를 원하는 시간 toocomplete 없습니까?</span><span class="sxs-lookup"><span data-stu-id="f4194-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="f4194-117">[여기][hdinsight-samples]에서 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="f4194-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="f4194-118">hello 다운로드에는 이러한 예제에 대 한 hello hql로 변환, pig 및 java 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="f4194-119"><a name="NewestVersion"></a>최신 버전</span><span class="sxs-lookup"><span data-stu-id="f4194-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="f4194-120">Hadoop 커넥터 버전</span><span class="sxs-lookup"><span data-stu-id="f4194-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="f4194-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="f4194-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="f4194-122">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="f4194-122">Script Uri</span></span></th>
        <td><span data-ttu-id="f4194-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="f4194-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="f4194-124">수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="f4194-124">Date Modified</span></span></th>
        <td><span data-ttu-id="f4194-125">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="f4194-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="f4194-126">지원되는 HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="f4194-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="f4194-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="f4194-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="f4194-128">변경 로그</span><span class="sxs-lookup"><span data-stu-id="f4194-128">Change Log</span></span></th>
        <td><span data-ttu-id="f4194-129">Azure DB Cosmos Java SDK too1.6.0 업데이트</span><span class="sxs-lookup"><span data-stu-id="f4194-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="f4194-130">원본 및 싱크로 분할된 컬렉션에 대한 추가 지원</span><span class="sxs-lookup"><span data-stu-id="f4194-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="f4194-131"><a name="Prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4194-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f4194-132">이 자습서에서는 hello 지침을 수행 하기 전에 hello 다음 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="f4194-133">Cosmos DB 계정, 데이터베이스 및 내부 문서가 포함된 컬렉션.</span><span class="sxs-lookup"><span data-stu-id="f4194-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="f4194-134">자세한 내용은 [Cosmos DB 시작하기][getting-started]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4194-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="f4194-135">Hello Cosmos DB 계정에 샘플 데이터를 가져올 [Cosmos DB 가져오기 도구][import-data]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="f4194-136">처리량.</span><span class="sxs-lookup"><span data-stu-id="f4194-136">Throughput.</span></span> <span data-ttu-id="f4194-137">HDInsight에서의 읽기 및 쓰기는 해당 컬렉션에 할당된 요청 단위로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="f4194-138">각 출력 컬렉션 내의 추가 저장 프로시저 용량.</span><span class="sxs-lookup"><span data-stu-id="f4194-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="f4194-139">hello 저장 프로시저 결과 문서를 전송 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="f4194-140">Hello Hive, Pig, 또는 MapReduce 작업의 결과 문서 hello에 대 한 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="f4194-141">[*선택 사항*] 추가 컬렉션의 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="f4194-142">순서 tooavoid hello hello 작업 동안 새 컬렉션을 만드는에 hello 결과 toostdout 인쇄, hello 출력 tooyour WASB 컨테이너에 저장 하거나 이미 기존 컬렉션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="f4194-143">기존 컬렉션을 지정 하는 hello 경우, 새 문서 hello 컬렉션 내 만들어지고 이미 기존 문서에서 충돌 하는 경우에 적용 될 *id*합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="f4194-144">**hello 커넥터 id 충돌이 있는 기존 문서를 자동으로 덮어쓰기 때문**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="f4194-145">Hello upsert 옵션 toofalse를 설정 하 여이 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="f4194-146">Upsert가 false이 고 hello Hadoop 작업이 실패 합니다; 충돌이 발생 하는 경우 id 충돌 오류를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="f4194-147"><a name="ProvisionHDInsight"></a>1단계: 새 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f4194-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="f4194-148">이 자습서에서는 스크립트 작업 hello Azure 포털 toocustomize에서 HDInsight 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="f4194-149">이 자습서에서는 hello Azure 포털 toocreate HDInsight 클러스터에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="f4194-150">Toouse PowerShell cmdlet 또는 hello HDInsight.NET SDK 확인 하는 방법에 대 한 지침은 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터] [ hdinsight-custom-provision] 문서.</span><span class="sxs-lookup"><span data-stu-id="f4194-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="f4194-151">Toohello 로그인 [Azure 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="f4194-152">클릭 **+ 새로 만들기** hello 맨 왼쪽 탐색 hello에서 검색 한 **HDInsight** hello 새 블레이드의 hello 검색 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="f4194-153">**HDInsight** 공개한 **Microsoft** hello hello 결과 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="f4194-154">클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="f4194-155">Hello 새 HDInsight 클러스터에 만드는 블레이드를 입력 하면 **클러스터 이름** 선택 hello 및 **구독** tooprovision 아래에서이 리소스를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="f4194-156">클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="f4194-156">Cluster name</span></span></td><td><span data-ttu-id="f4194-157">Hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="f4194-158">DNS 이름은 영숫자 문자로 시작 및 끝나야 하고 대시를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="f4194-159">hello 필드는 3 ~ 63 자 사이의 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="f4194-160">구독 이름</span><span class="sxs-lookup"><span data-stu-id="f4194-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="f4194-161">둘 이상의 Azure 구독을 보유 하는 경우 HDInsight 클러스터를 호스팅하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="f4194-162">
5.클릭 **클러스터 유형 선택** 집합 hello 속성 toohello 다음 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="f4194-163">클러스터 유형</span><span class="sxs-lookup"><span data-stu-id="f4194-163">Cluster type</span></span></td><td><span data-ttu-id="f4194-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="f4194-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f4194-165">클러스터 계층</span><span class="sxs-lookup"><span data-stu-id="f4194-165">Cluster tier</span></span></td><td><span data-ttu-id="f4194-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="f4194-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f4194-167">운영 체제</span><span class="sxs-lookup"><span data-stu-id="f4194-167">Operating System</span></span></td><td><span data-ttu-id="f4194-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="f4194-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f4194-169">버전</span><span class="sxs-lookup"><span data-stu-id="f4194-169">Version</span></span></td><td><span data-ttu-id="f4194-170">최신 버전</span><span class="sxs-lookup"><span data-stu-id="f4194-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="f4194-171">이제 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-171">Now, click **SELECT**.</span></span>

    ![Hadoop HDInsight 초기 클러스터 세부 정보 제공][image-customprovision-page1]
6. <span data-ttu-id="f4194-173">클릭 **자격 증명** tooset 로그인 및 원격 액세스 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="f4194-174">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="f4194-175">클러스터에 tooremote 하려는 경우 선택 *예* hello hello 블레이드 맨 아래에 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="f4194-176">클릭 **데이터 원본** tooset 데이터에 대 한 기본 위치에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="f4194-177">Hello 선택 **선택 방법을** 하 고 이미 기존 저장소 계정을 지정 하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="f4194-178">동일한 블레이드 hello, 지정 된 **기본 컨테이너** 및 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="f4194-179">그리고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4194-180">위치 닫기 tooyour 성능 향상을 위해 Cosmos DB 계정 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="f4194-181">클릭 **가격 책정** tooselect hello의 노드 수와 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="f4194-182">Hello 기본 구성 및 크기 조정 hello 작업자 노드 수를 나중에 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="f4194-183">클릭 **옵션 구성**, 다음 **스크립트 동작** 선택적 구성 블레이드 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="f4194-184">스크립트 동작에서 다음 정보 toocustomize hello HDInsight 클러스터에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="f4194-185">속성</span><span class="sxs-lookup"><span data-stu-id="f4194-185">Property</span></span></th><th><span data-ttu-id="f4194-186">값</span><span class="sxs-lookup"><span data-stu-id="f4194-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="f4194-187">이름</span><span class="sxs-lookup"><span data-stu-id="f4194-187">Name</span></span></td>
             <td><span data-ttu-id="f4194-188">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="f4194-189">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="f4194-189">Script URI</span></span></td>
             <td><span data-ttu-id="f4194-190">가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="f4194-191">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-191">Please enter:</span></span> </br> <span data-ttu-id="f4194-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="f4194-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f4194-193">헤드</span><span class="sxs-lookup"><span data-stu-id="f4194-193">Head</span></span></td>
             <td><span data-ttu-id="f4194-194">Hello 확인란 toorun hello hello 헤드 노드에 대 한 PowerShell 스크립트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="f4194-195">
             <strong>이 확인란을 선택합니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="f4194-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f4194-196">작업자</span><span class="sxs-lookup"><span data-stu-id="f4194-196">Worker</span></span></td>
             <td><span data-ttu-id="f4194-197">Hello 작업자 노드에 hello 확인란 toorun hello PowerShell 스크립트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="f4194-198">
             <strong>이 확인란을 선택합니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="f4194-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f4194-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="f4194-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="f4194-200">Hello 사육에 hello 확인란 toorun hello PowerShell 스크립트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="f4194-201">
             <strong>필요하지 않습니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="f4194-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="f4194-202">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f4194-202">Parameters</span></span></td>
             <td><span data-ttu-id="f4194-203">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="f4194-204">
             <strong>필요한 매개 변수가 없습니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="f4194-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="f4194-205">
11. Azure 구독에서 새 **리소스 그룹**을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="f4194-206">12.</span><span class="sxs-lookup"><span data-stu-id="f4194-206">12.</span></span> <span data-ttu-id="f4194-207">이제, 확인 **Pin toodashboard** tootrack 누른 배포 **만들기**!</span><span class="sxs-lookup"><span data-stu-id="f4194-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="f4194-208"><a name="InstallCmdlets"></a>2단계: Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="f4194-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="f4194-209">Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-209">Install Azure PowerShell.</span></span> <span data-ttu-id="f4194-210">자세한 내용은 [여기][powershell-install-configure]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4194-211">또는 Hive 쿼리만 해당하는 경우 HDInsight의 온라인 Hive 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="f4194-212">따라서 toohello toodo에 로그인 [Azure 포털][azure-portal], 클릭 **HDInsight** on hello 왼쪽된 창 tooview HDInsight 클러스터의 목록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="f4194-213">Hello 클러스터 toorun 하이브 쿼리를 원하는 하 고 클릭 한 다음 클릭 **쿼리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="f4194-214">Azure PowerShell 통합 스크립팅 환경 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="f4194-215">Windows 8 또는 Windows Server 2012 이상을 실행 하는 컴퓨터에서 기본 제공 hello를 사용할 수 있습니다 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="f4194-216">Hello 시작 화면에서 입력 **powershell ise** 클릭 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="f4194-217">Windows 8 또는 Windows Server 2012 이전 버전을 실행 하는 컴퓨터에서 hello 시작 메뉴를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="f4194-218">Hello 시작 메뉴에서 입력 **명령 프롬프트** hello 검색 상자에 다음 hello 결과 목록에서 클릭 **명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="f4194-219">Hello 명령 프롬프트에에서 입력 **powershell_ise** 클릭 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="f4194-220">Azure 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="f4194-221">Hello 콘솔 창에에서 입력 **Add-azureaccount** 클릭 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="f4194-222">Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="f4194-223">Azure 구독에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="f4194-224">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="f4194-225">다음 다이어그램 hello hello Azure PowerShell 스크립팅 환경을의 중요 한 부분을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Azure PowerShell에 대한 다이어그램][azure-powershell-diagram]

## <span data-ttu-id="f4194-227"><a name="RunHive"></a>3단계: Cosmos DB 및 HDInsight를 사용하여 Hive 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4194-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f4194-228">< >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="f4194-229">Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="f4194-230">쿼리 문자열 생성부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="f4194-231">모든 문서 시스템 생성 타임 스탬프 (_ts) 및 Azure Cosmos DB 컬렉션에서 고유 id (_rid)는 모든 문서 hello 분 단위로 계산 하 고 다음 새 Azure Cosmos DB 컬렉션에 다시 hello 결과 저장 하는 하이브 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="f4194-232">먼저 Azure Cosmos DB 컬렉션에서 Hive 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="f4194-233">다음 코드 조각 toohello PowerShell 스크립트 창 hello 추가 <strong>후</strong> # 1에서 hello 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="f4194-234">자사 문서 toojust _ts 및 _rid hello 선택적 DocumentDB.query 매개 변수 t 트림 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="f4194-235">**DocumentDB.inputCollections 이름 지정은 실수가 아니었습니다.**</span><span class="sxs-lookup"><span data-stu-id="f4194-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="f4194-236">입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="f4194-237">다음으로 hello 출력 컬렉션에 대 한 하이브 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="f4194-238">hello 출력 문서 속성 hello 월, 일, 시간, 분 및 hello 총 항목 수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4194-239">**하지만 다시 DocumentDB.outputCollections 이름 지정은 실수가 아니었습니다.**</span><span class="sxs-lookup"><span data-stu-id="f4194-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="f4194-240">출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="f4194-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB 출력 컬렉션 이름 1\>*,*\<DocumentDB 출력 컬렉션 이름 2\>*'</span><span class="sxs-lookup"><span data-stu-id="f4194-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="f4194-242">hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="f4194-243">문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="f4194-244">문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="f4194-245">마지막으로, 보겠습니다 월, 일, 시간 및 분 및 삽입 hello 결과 hello로 다시 여 집계 hello 문서 출력 Hive 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="f4194-246">Hello 스크립트 조각 toocreate 하이브 작업 정의 hello 이전 쿼리에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="f4194-247">사용할 수도 있습니다 hello-파일 전환 toospecify HDFS에 HiveQL 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="f4194-248">다음 코드 조각 toosave hello 시작 시간 hello를 추가 하 고 hello 하이브 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="f4194-249">하이브 작업 toocomplete hello에 대 한 toowait 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="f4194-250">Hello tooprint hello 표준 출력 및 hello 시작 다음을 추가 하 고 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="f4194-251">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-251">**Run** your new script!</span></span> <span data-ttu-id="f4194-252">**클릭** hello 녹색 단추를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="f4194-253">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-253">Check hello results.</span></span> <span data-ttu-id="f4194-254">Hello에 로그인 [Azure 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="f4194-255">클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="f4194-256">클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="f4194-257"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="f4194-258">다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 하이브 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="f4194-259">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="f4194-260">하이브 쿼리 hello 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-260">You will see hello results of your Hive query.</span></span>

   ![Hive 쿼리 결과][image-hive-query-results]

## <span data-ttu-id="f4194-262"><a name="RunPig"></a>4단계: Cosmos DB 및 HDInsight를 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4194-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f4194-263">< >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="f4194-264">Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="f4194-265">쿼리 문자열 생성부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="f4194-266">모든 문서 시스템 생성 타임 스탬프 (_ts) 및 Azure Cosmos DB 컬렉션에서 고유 id (_rid)는 모든 문서 hello 분 단위로 계산 하 고 다음 새 Azure Cosmos DB 컬렉션에 다시 hello 결과 저장 하는 Pig 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="f4194-267">먼저 Cosmos DB의 문서를 HDInsight에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="f4194-268">다음 코드 조각 toohello PowerShell 스크립트 창 hello 추가 <strong>후</strong> # 1에서 hello 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="f4194-269">Tooadd는 DocumentDB 쿼리 toohello 선택적 DocumentDB 쿼리 매개 변수 tootrim 우리의 문서 toojust _ts 및 _rid 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="f4194-270">입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="f4194-271">'*\<DocumentDB 입력 컬렉션 이름 1\>*,*\<DocumentDB 입력 컬렉션 이름 2\>*'</span><span class="sxs-lookup"><span data-stu-id="f4194-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="f4194-272">hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="f4194-273">문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="f4194-274">문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="f4194-275">다음으로, 보겠습니다 hello 월, 일, 시간, 분 및 발생 빈도의 총 hello 하 여 hello 문서 수를 셉니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="f4194-276">마지막으로, 새 출력 컬렉션에 저장할 hello 결과 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4194-277">출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="f4194-278">'\<DocumentDB 출력 컬렉션 이름 1\>,\<DocumentDB 출력 컬렉션 이름 2\>'</span><span class="sxs-lookup"><span data-stu-id="f4194-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="f4194-279">hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="f4194-280">에 대해 설명 합니다 여러 컬렉션 hello 간에 분산된 라운드 로빈을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="f4194-281">문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="f4194-282">Hello 스크립트 조각 toocreate Pig 작업 정의 hello 이전 쿼리에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="f4194-283">사용할 수도 있습니다 hello-파일 전환 toospecify HDFS에서 Pig 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="f4194-284">다음 코드 조각 toosave hello 시작 시간 hello를 추가 하 고 hello Pig 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="f4194-285">Hello toowait Pig 작업 toocomplete hello에 대 한 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="f4194-286">Hello tooprint hello 표준 출력 및 hello 시작 다음을 추가 하 고 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="f4194-287">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-287">**Run** your new script!</span></span> <span data-ttu-id="f4194-288">**클릭** hello 녹색 단추를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="f4194-289">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-289">Check hello results.</span></span> <span data-ttu-id="f4194-290">Hello에 로그인 [Azure 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="f4194-291">클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="f4194-292">클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="f4194-293"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="f4194-294">다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 Pig 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="f4194-295">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="f4194-296">Hello Pig 쿼리 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-296">You will see hello results of your Pig query.</span></span>

    ![Pig 쿼리 결과][image-pig-query-results]

## <span data-ttu-id="f4194-298"><a name="RunMapReduce"></a>5단계: Azure Cosmos DB 및 HDInsight를 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4194-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="f4194-299">Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="f4194-300">Hello Azure Cosmos DB 컬렉션에서 각 문서 속성에 대해 발생 수를 계산 하는 MapReduce 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="f4194-301">이 스크립트 조각을 추가 **후** 위의 hello 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="f4194-302">TallyProperties v01.jar hello Cosmos DB Hadoop 커넥터의 사용자 지정 설치 hello 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="f4194-303">명령 toosubmit hello MapReduce 작업을 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="f4194-304">또한 toohello MapReduce 작업 정의 입력 해야 hello HDInsight 클러스터 이름을 toorun hello MapReduce 작업 및 hello 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="f4194-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="f4194-305">hello Start-azurehdinsightjob은 비동기식된 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="f4194-306">hello 작업을 사용 하 여 hello toocheck hello 완료 *Wait-azurehdinsightjob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f4194-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="f4194-307">다음 명령은 toocheck hello 실행 중인 hello MapReduce 작업을 사용 하 여 모든 오류를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="f4194-308">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-308">**Run** your new script!</span></span> <span data-ttu-id="f4194-309">**클릭** hello 녹색 단추를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="f4194-310">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-310">Check hello results.</span></span> <span data-ttu-id="f4194-311">Hello에 로그인 [Azure 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="f4194-312">클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="f4194-313">클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="f4194-314"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="f4194-315">다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="f4194-316">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="f4194-317">MapReduce 작업의 hello 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-317">You will see hello results of your MapReduce job.</span></span>

      ![MapReduce 쿼리 결과][image-mapreduce-query-results]

## <span data-ttu-id="f4194-319"><a name="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4194-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="f4194-320">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-320">Congratulations!</span></span> <span data-ttu-id="f4194-321">지금까지 Azure Cosmos DB 및 HDInsight를 사용해서 첫 번째 Hive, Pig 및 MapReduce 작업을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="f4194-322">Hadoop 커넥터는 소스가 공개되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="f4194-323">관심이 있으면 [GitHub][github]에서 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4194-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="f4194-324">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="f4194-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="f4194-325">[Documentdb로 Java 응용 프로그램 개발][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="f4194-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="f4194-326">[HDInsight의 Hadoop용 Java MapReduce 프로그램 개발][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f4194-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="f4194-327">[HDInsight tooanalyze 모바일 송수화기 사용 중인 Hadoop 하이브 사용을 시작.][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f4194-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="f4194-328">[HDInsight와 함께 MapReduce 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f4194-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="f4194-329">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f4194-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f4194-330">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f4194-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f4194-331">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="f4194-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
