---
title: "도메인에 가입 된 HDInsight-Azure에서에서 aaaConfigure 하이브 정책 | Microsoft Docs"
description: "유용한 정보"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="46b02-103">도메인에 가입된 HDInsight에서 Hive 정책 구성(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="46b02-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="46b02-104">자세한 방법을 하이브에 대 한 tooconfigure Apache 레인저 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="46b02-105">이 문서에서는 두 개의 레인저 정책 toorestrict 액세스 toohello hivesampletable를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="46b02-106">hello hivesampletable HDInsight 클러스터에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="46b02-107">Hello 정책을 구성한 경우 HDInsight에서 Excel 및 ODBC 드라이버 tooconnect tooHive 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46b02-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="46b02-108">Prerequisites</span></span>
* <span data-ttu-id="46b02-109">도메인에 가입된 HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="46b02-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="46b02-110">[도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46b02-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="46b02-111">Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone 또는 Office 2010 Professional Plus를 포함한 워크스테이션</span><span class="sxs-lookup"><span data-stu-id="46b02-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="46b02-112">TooApache 레인저 관리 UI를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="46b02-113">**tooconnect tooRanger 관리 UI**</span><span class="sxs-lookup"><span data-stu-id="46b02-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="46b02-114">브라우저에서 tooRanger 관리 UI를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="46b02-115">hello URL은 https://&lt;ClusterName >.azurehdinsight.net/Ranger/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="46b02-116">Ranger는 다른 Hadoop 클러스터가 아닌 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="46b02-117">tooprevent 브라우저 캐시의 Hadoop 자격 증명을 사용 하 여 새 inprivate 브라우저 창 tooconnect toohello 레인저 관리 UI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="46b02-118">Hello 클러스터 관리자가 도메인 사용자 이름 및 암호를 사용 하 여 로그인:</span><span class="sxs-lookup"><span data-stu-id="46b02-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![HDInsight 도메인에 가입된 Ranger 홈페이지](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="46b02-120">Ranger는 현재 Yarn 및 Hive에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="46b02-121">도메인 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="46b02-121">Create Domain users</span></span>
<span data-ttu-id="46b02-122">[도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 hiveruser1 및 hiveuser2를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="46b02-123">이 자습서에서는 두 개의 사용자 계정을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="46b02-124">Ranger 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="46b02-124">Create Ranger policies</span></span>
<span data-ttu-id="46b02-125">이 섹션에서는 hivesampletable에 액세스하기 위한 두 개의 Ranger 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="46b02-126">다른 열 집합에 대한 선택 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="46b02-127">두 사용자는 모두 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="46b02-128">Hello 다음 섹션에서는 Excel에서 hello 두 정책을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="46b02-129">**toocreate 레인저 정책**</span><span class="sxs-lookup"><span data-stu-id="46b02-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="46b02-130">Ranger 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="46b02-131">참조 [tooApache 레인저 관리 UI를 연결](#connect-to-apache-ranager-admin-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="46b02-132">**Hive**에서 **&lt;ClusterName>_hive**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="46b02-133">두 개의 미리 구성 정책이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="46b02-134">클릭 **새 정책 추가**, hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="46b02-135">정책 이름: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="46b02-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="46b02-136">Hive 데이터베이스: 기본값</span><span class="sxs-lookup"><span data-stu-id="46b02-136">Hive Database: default</span></span>
   * <span data-ttu-id="46b02-137">테이블: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="46b02-137">table: hivesampletable</span></span>
   * <span data-ttu-id="46b02-138">Hive 열: *</span><span class="sxs-lookup"><span data-stu-id="46b02-138">Hive column: *</span></span>
   * <span data-ttu-id="46b02-139">사용자 선택: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="46b02-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="46b02-140">사용 권한: 선택</span><span class="sxs-lookup"><span data-stu-id="46b02-140">Permissions: select</span></span>

     ![HDInsight 도메인에 가입된 Ranger Hive 정책 구성](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="46b02-142">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="46b02-143">도메인 사용자가 사용자 선택에 채워지지 않았습니다를 AAD에 레인저 toosync 잠시 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="46b02-144">클릭 **추가** toosave hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="46b02-145">다음과 같은 속성 hello로 hello 마지막 두 단계 toocreate 다른 정책을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="46b02-146">정책 이름: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="46b02-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="46b02-147">Hive 데이터베이스: 기본값</span><span class="sxs-lookup"><span data-stu-id="46b02-147">Hive Database: default</span></span>
   * <span data-ttu-id="46b02-148">테이블: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="46b02-148">table: hivesampletable</span></span>
   * <span data-ttu-id="46b02-149">Hive 열: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="46b02-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="46b02-150">사용자 선택: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="46b02-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="46b02-151">사용 권한: 선택</span><span class="sxs-lookup"><span data-stu-id="46b02-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="46b02-152">Hive ODBC 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="46b02-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="46b02-153">hello 지침은에서 [만들기 하이브 ODBC 데이터 원본](hdinsight-connect-excel-hive-odbc-driver.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="46b02-154">속성</span><span class="sxs-lookup"><span data-stu-id="46b02-154">Property</span></span>|<span data-ttu-id="46b02-155">설명</span><span class="sxs-lookup"><span data-stu-id="46b02-155">Description</span></span>
    ---|---
    <span data-ttu-id="46b02-156">데이터 원본 이름</span><span class="sxs-lookup"><span data-stu-id="46b02-156">Data Source Name</span></span>|<span data-ttu-id="46b02-157">이름 tooyour 데이터 소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="46b02-158">호스트</span><span class="sxs-lookup"><span data-stu-id="46b02-158">Host</span></span>|<span data-ttu-id="46b02-159">&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="46b02-160">예를 들면 myHDICluster.azurehdinsight.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="46b02-161">포트</span><span class="sxs-lookup"><span data-stu-id="46b02-161">Port</span></span>|<span data-ttu-id="46b02-162"><strong>443</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="46b02-163">(이 포트를 변경 하지 563 too443에서.)</span><span class="sxs-lookup"><span data-stu-id="46b02-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="46b02-164">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="46b02-164">Database</span></span>|<span data-ttu-id="46b02-165"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="46b02-166">Hive 서버 유형</span><span class="sxs-lookup"><span data-stu-id="46b02-166">Hive Server Type</span></span>|<span data-ttu-id="46b02-167"><strong>Hive 서버 2</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="46b02-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="46b02-168">메커니즘</span><span class="sxs-lookup"><span data-stu-id="46b02-168">Mechanism</span></span>|<span data-ttu-id="46b02-169"><strong>Azure HDInsight Service</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="46b02-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="46b02-170">HTTP 경로</span><span class="sxs-lookup"><span data-stu-id="46b02-170">HTTP Path</span></span>|<span data-ttu-id="46b02-171">비워 둠</span><span class="sxs-lookup"><span data-stu-id="46b02-171">Leave it blank.</span></span>
    <span data-ttu-id="46b02-172">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="46b02-172">User Name</span></span>|<span data-ttu-id="46b02-173">hiveuser1@contoso158.onmicrosoft.com을 입력합니다. 다른 경우 hello 도메인 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="46b02-174">암호</span><span class="sxs-lookup"><span data-stu-id="46b02-174">Password</span></span>|<span data-ttu-id="46b02-175">Hiveuser1 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="46b02-176">있는지 tooclick 확인 **테스트** hello 데이터 소스를 저장 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="46b02-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="46b02-177">HDInsight에서 Excel로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="46b02-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="46b02-178">Hello 마지막 섹션에서 두 개의 정책을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="46b02-179">hiveuser1 모든 hello 열에 대 한 select 권한 hello 많고 hiveuser2 hello 두 개의 열에 대 한 select 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="46b02-180">이 섹션에서는 Excel로 hello 두 명의 사용자가 tooimport 데이터를 가장 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="46b02-181">Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="46b02-182">Hello에서 **데이터** 탭을 클릭 **기타 데이터 원본**, 클릭 하 고 **데이터 연결 마법사** toolaunch hello **데이터연결마법사**.</span><span class="sxs-lookup"><span data-stu-id="46b02-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="46b02-183">![데이터 연결 마법사 열기][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="46b02-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="46b02-184">선택 **ODBC DSN** hello 데이터 원본과 클릭으로 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="46b02-185">ODBC 데이터 원본의 선택 hello 데이터 원본 이름 hello 이전 단계에서 만든 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="46b02-186">Hello 마법사에서 hello 클러스터에 대 한 hello 암호를 다시 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="46b02-187">Hello에 대 한 대기 **데이터베이스 및 테이블 선택** 대화 tooopen 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="46b02-188">몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="46b02-189">**hivesampletable**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="46b02-190">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-190">Click **Finish**.</span></span>
8. <span data-ttu-id="46b02-191">Hello에 **데이터 가져오기** 대화 상자에서 변경 하거나 hello 쿼리를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="46b02-192">toodo 이므로, 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="46b02-193">몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="46b02-194">Hello 클릭 **정의** hello 명령 텍스트가 탭:</span><span class="sxs-lookup"><span data-stu-id="46b02-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="46b02-195">Hiveuser1는 hello 레인저 정책 정의 의해 모든 hello 열에 대해 select 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="46b02-196">따라서 이 쿼리를 hiveuser1의 자격 증명에서 사용할 수 있지만 hiveuser2의 자격 증명과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="46b02-197">![연결 속성][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="46b02-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="46b02-198">클릭 **확인** tooclose hello에 대 한 연결 속성 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="46b02-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="46b02-199">클릭 **확인** tooclose hello **데이터 가져오기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="46b02-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="46b02-200">Hiveuser1에 대 한 hello 암호를 다시 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="46b02-201">걸리는 시간은 몇 초 전에 데이터를 가져온된 tooExcel 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="46b02-202">작업이 완료되면 11개 열의 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="46b02-203">hello 마지막 섹션에서 만든 tootest hello 두 번째 정책이 (읽기 hivesampletable devicemake)</span><span class="sxs-lookup"><span data-stu-id="46b02-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="46b02-204">Excel에서 새 시트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="46b02-205">Hello 마지막 절차 tooimport hello 데이터를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="46b02-206">hello만 변경 사항이 됩니다 hiveuser1의 대신 toouse hiveuser2 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="46b02-207">Hiveuser2 permission toosee 두 열에만 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="46b02-208">다음 오류가 hello를 발생할 점에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="46b02-209">다음과 같은 hello 프로시저 tooimport 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="46b02-210">이 시간 hiveuser2의 자격 증명을 사용 하 고 또한에서 select 문을 hello를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="46b02-211">to:</span><span class="sxs-lookup"><span data-stu-id="46b02-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="46b02-212">작업이 완료되면 가져온 두 개 열의 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b02-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46b02-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46b02-213">Next steps</span></span>
* <span data-ttu-id="46b02-214">도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46b02-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="46b02-215">도메인에 가입된 HDInsight 클러스터 관리에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46b02-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="46b02-216">도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46b02-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="46b02-217">하이브 JDBC를 사용 하 여 하이브 연결에 대 한 참조 [tooHive hello 하이브 JDBC 드라이버를 사용 하 여 Azure HDInsight에 연결](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="46b02-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="46b02-218">하이브 ODBC를 사용 하 여 연결 Excel tooHadoop 참조 [Microsoft 하이브 ODBC 드라이브 hello로 Excel 연결 tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="46b02-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="46b02-219">파워 쿼리를 사용 하 여 연결 Excel tooHadoop 참조 [파워 쿼리를 사용 하 여 Excel 연결 tooHadoop](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="46b02-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
