---
title: "도메인에 가입된 HDInsight에서 Hive 정책 구성 - Azure | Microsoft Docs"
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
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="31663-103">도메인에 가입된 HDInsight에서 Hive 정책 구성(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="31663-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="31663-104">Hive에 대한 Apache Ranger 정책을 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31663-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="31663-105">이 문서에서는 hivesampletable에 대한 액세스를 제한하는 두 개의 Ranger 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="31663-106">hivesampletable은 HDInsight 클러스터와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31663-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="31663-107">정책을 구성한 경우 Excel 및 ODBC 드라이버를 사용하여 HDInsight의 Hive 테이블에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31663-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31663-108">Prerequisites</span></span>
* <span data-ttu-id="31663-109">도메인에 가입된 HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="31663-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="31663-110">[도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="31663-111">Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone 또는 Office 2010 Professional Plus를 포함한 워크스테이션</span><span class="sxs-lookup"><span data-stu-id="31663-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="31663-112">Apache Ranger 관리 UI에 연결</span><span class="sxs-lookup"><span data-stu-id="31663-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="31663-113">**Ranger 관리 UI에 연결하려면**</span><span class="sxs-lookup"><span data-stu-id="31663-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="31663-114">브라우저에서 Ranger 관리 UI에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="31663-115">URL은 https://&lt;ClusterName>.azurehdinsight.net/Ranger/입니다.</span><span class="sxs-lookup"><span data-stu-id="31663-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31663-116">Ranger는 다른 Hadoop 클러스터가 아닌 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="31663-117">브라우저가 캐시된 Hadoop 자격 증명을 사용하지 않도록 방지하려면 새 inprivate 브라우저 창을 사용하여 Ranger 관리 UI에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="31663-118">클러스터 관리자 도메인 사용자 이름 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![HDInsight 도메인에 가입된 Ranger 홈페이지](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="31663-120">Ranger는 현재 Yarn 및 Hive에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="31663-121">도메인 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="31663-121">Create Domain users</span></span>
<span data-ttu-id="31663-122">[도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 hiveruser1 및 hiveuser2를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="31663-123">이 자습서에서는 두 개의 사용자 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="31663-124">Ranger 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="31663-124">Create Ranger policies</span></span>
<span data-ttu-id="31663-125">이 섹션에서는 hivesampletable에 액세스하기 위한 두 개의 Ranger 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31663-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="31663-126">다른 열 집합에 대한 선택 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="31663-127">두 사용자는 모두 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="31663-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="31663-128">다음 섹션에서는 Excel에 있는 두 개의 정책을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="31663-129">**Ranger 정책을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="31663-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="31663-130">Ranger 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31663-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="31663-131">[Apache Ranger 관리 UI에 연결](#connect-to-apache-ranager-admin-ui)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="31663-132">**Hive**에서 **&lt;ClusterName>_hive**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="31663-133">두 개의 미리 구성 정책이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="31663-134">**새 정책 추가**를 클릭하고 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="31663-135">정책 이름: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="31663-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="31663-136">Hive 데이터베이스: 기본값</span><span class="sxs-lookup"><span data-stu-id="31663-136">Hive Database: default</span></span>
   * <span data-ttu-id="31663-137">테이블: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="31663-137">table: hivesampletable</span></span>
   * <span data-ttu-id="31663-138">Hive 열: *</span><span class="sxs-lookup"><span data-stu-id="31663-138">Hive column: *</span></span>
   * <span data-ttu-id="31663-139">사용자 선택: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="31663-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="31663-140">사용 권한: 선택</span><span class="sxs-lookup"><span data-stu-id="31663-140">Permissions: select</span></span>

     ![HDInsight 도메인에 가입된 Ranger Hive 정책 구성](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="31663-142">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="31663-143">사용자 선택에서 도메인 사용자가 채워지지 않으면 Ranger가 AAD와 동기화되기를 몇 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="31663-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="31663-144">**추가** 를 클릭하여 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="31663-145">다음 속성을 가진 다른 정책을 만들려면 마지막 두 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="31663-146">정책 이름: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="31663-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="31663-147">Hive 데이터베이스: 기본값</span><span class="sxs-lookup"><span data-stu-id="31663-147">Hive Database: default</span></span>
   * <span data-ttu-id="31663-148">테이블: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="31663-148">table: hivesampletable</span></span>
   * <span data-ttu-id="31663-149">Hive 열: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="31663-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="31663-150">사용자 선택: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="31663-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="31663-151">사용 권한: 선택</span><span class="sxs-lookup"><span data-stu-id="31663-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="31663-152">Hive ODBC 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="31663-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="31663-153">[Hive ODBC 데이터 원본 만들기](hdinsight-connect-excel-hive-odbc-driver.md)에서 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="31663-154">속성</span><span class="sxs-lookup"><span data-stu-id="31663-154">Property</span></span>|<span data-ttu-id="31663-155">설명</span><span class="sxs-lookup"><span data-stu-id="31663-155">Description</span></span>
    ---|---
    <span data-ttu-id="31663-156">데이터 원본 이름</span><span class="sxs-lookup"><span data-stu-id="31663-156">Data Source Name</span></span>|<span data-ttu-id="31663-157">데이터 원본에 이름 지정</span><span class="sxs-lookup"><span data-stu-id="31663-157">Give a name to your data source</span></span>
    <span data-ttu-id="31663-158">호스트</span><span class="sxs-lookup"><span data-stu-id="31663-158">Host</span></span>|<span data-ttu-id="31663-159">&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="31663-160">예를 들면 myHDICluster.azurehdinsight.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="31663-161">포트</span><span class="sxs-lookup"><span data-stu-id="31663-161">Port</span></span>|<span data-ttu-id="31663-162"><strong>443</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="31663-163">(이 포트는 563에서 443으로 변경됨)</span><span class="sxs-lookup"><span data-stu-id="31663-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="31663-164">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="31663-164">Database</span></span>|<span data-ttu-id="31663-165"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="31663-166">Hive 서버 유형</span><span class="sxs-lookup"><span data-stu-id="31663-166">Hive Server Type</span></span>|<span data-ttu-id="31663-167"><strong>Hive 서버 2</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="31663-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="31663-168">메커니즘</span><span class="sxs-lookup"><span data-stu-id="31663-168">Mechanism</span></span>|<span data-ttu-id="31663-169"><strong>Azure HDInsight Service</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="31663-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="31663-170">HTTP 경로</span><span class="sxs-lookup"><span data-stu-id="31663-170">HTTP Path</span></span>|<span data-ttu-id="31663-171">비워 둠</span><span class="sxs-lookup"><span data-stu-id="31663-171">Leave it blank.</span></span>
    <span data-ttu-id="31663-172">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="31663-172">User Name</span></span>|<span data-ttu-id="31663-173">hiveuser1@contoso158.onmicrosoft.com을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="31663-174">사용자 이름이 다른 경우 도메인 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="31663-175">암호</span><span class="sxs-lookup"><span data-stu-id="31663-175">Password</span></span>|<span data-ttu-id="31663-176">hiveuser1의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="31663-177">데이터 원본을 저장하기 전에 **테스트**를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="31663-178">HDInsight에서 Excel로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="31663-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="31663-179">마지막 섹션에서 두 개의 정책을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="31663-180">hiveuser1에는 모든 열에 대한 선택 사용 권한이 있으며 hiveuser2에는 두 열에 대한 선택 사용 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="31663-181">이 섹션에서는 데이터를 Excel로 가져오는 두 사용자를 가장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="31663-182">Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31663-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="31663-183">**데이터** 탭에서 **다른 데이터 원본에서**를 클릭한 다음 **데이터 연결 마법사에서**를 클릭하여 **데이터 연결 마법사**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="31663-184">![데이터 연결 마법사 열기][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="31663-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="31663-185">데이터 원본으로 **ODBC DSN**을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="31663-186">ODBC 데이터 원본에서 이전 단계에서 만든 데이터 원본 이름을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="31663-187">마법사에서 클러스터의 암호를 다시 입력한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="31663-188">**데이터베이스 및 테이블 선택** 대화 상자가 열릴 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="31663-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="31663-189">몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="31663-190">**hivesampletable**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="31663-191">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-191">Click **Finish**.</span></span>
8. <span data-ttu-id="31663-192">**데이터 가져오기** 대화 상자에서 쿼리를 변경하거나 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="31663-193">이렇게 하려면 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-193">To do so, click **Properties**.</span></span> <span data-ttu-id="31663-194">몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="31663-195">**정의** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-195">Click the **Definition** tab.</span></span> <span data-ttu-id="31663-196">명령 텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="31663-197">정의한 Ranger 정책으로 hiveuser1에는 모든 열에 대한 선택 사용 권한이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="31663-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="31663-198">따라서 이 쿼리를 hiveuser1의 자격 증명에서 사용할 수 있지만 hiveuser2의 자격 증명과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="31663-199">![연결 속성][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="31663-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="31663-200">**확인** 을 클릭하여 연결 속성 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="31663-201">**확인**을 클릭하여 **데이터 가져오기** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="31663-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="31663-202">hiveuser1의 암호를 다시 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="31663-203">데이터를 Excel로 가져올 때까지 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="31663-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="31663-204">작업이 완료되면 11개 열의 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31663-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="31663-205">지난 섹션에서 만든 두 번째 정책(read-hivesampletable-devicemake)을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="31663-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="31663-206">Excel에서 새 시트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="31663-207">데이터를 가져오는 마지막 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="31663-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="31663-208">유일한 차이점은 hiveuser1의 자격 증명 대신 hiveuser2의 자격 증명을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31663-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="31663-209">hiveuser2에 두 열을 표시하는 사용 권한이 있기 때문에 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="31663-210">다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31663-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="31663-211">데이터를 가져오는 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="31663-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="31663-212">또한 이번에는 hiveuser2의 자격 증명을 사용하여 다음에서 select 문을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="31663-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="31663-213">to:</span><span class="sxs-lookup"><span data-stu-id="31663-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="31663-214">작업이 완료되면 가져온 두 개 열의 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31663-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31663-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31663-215">Next steps</span></span>
* <span data-ttu-id="31663-216">도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="31663-217">도메인에 가입된 HDInsight 클러스터 관리에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="31663-218">도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="31663-219">Hive JDBC를 사용하여 Hive를 연결하는 자세한 내용은 [Hive JDBC 드라이버를 사용하여 Azure HDInsight에서 Hive에 연결](hdinsight-connect-hive-jdbc-driver.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="31663-220">Hive ODBC를 사용하여 Hadoop에 Excel을 연결하는 자세한 내용은 [Microsoft Hive ODBC 드라이브와 함께 Hadoop에 Excel 연결](hdinsight-connect-excel-hive-odbc-driver.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="31663-221">파워 쿼리를 사용하여 Hadoop에 Excel을 연결하는 자세한 내용은 [파워 쿼리를 사용하여 Hadoop에 Excel 연결](hdinsight-connect-excel-power-query.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31663-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
