---
title: "Visual Studio용 Data Lake 도구 및 Hortonworks 샌드박스 - Azure HDInsight | Microsoft Docs"
description: "Hortonworks Sandbox(로컬 VM에서 실행됨)와 Azure Data Lake tools for Visual Studio를 사용하는 방법을 알아봅니다. 이러한 도구로 샌드박스에 대한 Hive 및 Pig 작업을 만들고 실행하며 작업 출력 및 기록을 볼 수 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="e6281-104">Hortonworks Sandbox와 Azure Data Lake tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="e6281-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="e6281-105">Azure Data Lake는 제네릭 Hadoop 클러스터를 사용하기 위한 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="e6281-106">이 문서에서는 로컬 가상 컴퓨터에서 실행되는 Hortonworks Sandbox와 Data Lake 도구를 사용하는 데 필요한 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="e6281-107">Hortonworks Sandbox를 사용하여 개발 환경에서 로컬로 Hadoop를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="e6281-108">솔루션을 개발하여 대규모로 배포했으므로 HDInsight 클러스터를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6281-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e6281-109">Prerequisites</span></span>

* <span data-ttu-id="e6281-110">개발 환경의 가상 컴퓨터에서 실행되는 Hortonworks Sandbox입니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="e6281-111">이 문서는 Oracle VirtualBox에서 실행 중인 샌드박스로 작성 및 테스트되었으며,</span><span class="sxs-lookup"><span data-stu-id="e6281-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="e6281-112">샌드박스 설정에 대한 자세한 내용은 [Hortonworks 샌드박스 시작](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e6281-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="e6281-113">문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6281-113">document.</span></span>

* <span data-ttu-id="e6281-114">Visual Studio 2013, Visual Studio 2015 또는 Visual Studio 2017(모든 에디션)</span><span class="sxs-lookup"><span data-stu-id="e6281-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="e6281-115">[Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 이상</span><span class="sxs-lookup"><span data-stu-id="e6281-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="e6281-116">[Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)</span><span class="sxs-lookup"><span data-stu-id="e6281-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="e6281-117">샌드박스의 암호 구성</span><span class="sxs-lookup"><span data-stu-id="e6281-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="e6281-118">Hortonworks Sandbox가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="e6281-119">[Hortonworks 샌드박스에서 시작](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) 문서에 나온 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="e6281-120">이러한 단계에서 SSH `root` 계정 및 Ambari `admin` 계정의 암호를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="e6281-121">Visual Studio에서 샌드박스에 연결할 때 이러한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="e6281-122">샌드박스에 도구 연결</span><span class="sxs-lookup"><span data-stu-id="e6281-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="e6281-123">Visual Studio를 열고 **보기** 및 **서버 탐색기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="e6281-124">**서버 탐색기**에서 **HDInsight** 항목을 마우스 오른쪽 단추로 클릭한 다음 **HDInsight Emulator에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![HDInsight Emulator에 연결이 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="e6281-126">**HDInsight Emulator에 연결** 대화 상자에서 Ambari에 대해 구성한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="e6281-128">**다음**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="e6281-129">**암호** 필드를 사용하여 `root` 계정에 대해 구성한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="e6281-130">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-130">Leave the other fields at the default value.</span></span>

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="e6281-132">**다음**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="e6281-133">서비스의 유효성 검사가 완료되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="e6281-134">경우에 따라 유효성 검사가 실패하고 구성을 업데이트하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="e6281-135">유효성 검사에 실패할 경우 **업데이트**를 선택하고 서비스의 구성 및 확인이 완료되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![업데이트 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="e6281-137">업데이트 프로세스는 Ambari를 사용하여 Visual Studio용 Data Lake 도구에서 예상한 Hortonworks Sandbox 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="e6281-138">유효성 검사가 완료되면 **마침**을 선택하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="e6281-139">![마침 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="e6281-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="e6281-140">개발 환경의 속도 및 가상 컴퓨터에 할당된 메모리 양에 따라 서비스를 구성하고 유효성을 검사하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="e6281-141">이러한 단계를 따르면 **HDInsight** 섹션의 서버 탐색기에서 **HDInsight 로컬 클러스터** 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="e6281-142">Hive 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="e6281-142">Write a Hive query</span></span>

<span data-ttu-id="e6281-143">Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="e6281-144">다음 단계를 사용하여 로컬 클러스터에 대해 주문형 쿼리를 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="e6281-145">**서버 탐색기**에서 이전에 추가한 로컬 클러스터에 대한 항목을 마우스 오른쪽 단추로 클릭한 다음 **Hive 쿼리 작성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Hive 쿼리 작성이 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="e6281-147">새 쿼리 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-147">A new query window appears.</span></span> <span data-ttu-id="e6281-148">쿼리를 신속하게 쓰고 로컬 클러스터에 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="e6281-149">새 쿼리 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="e6281-150">쿼리를 실행하려면 창의 위쪽에 있는 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="e6281-151">다른 값(**Batch** 및 서버 이름)을 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![제출 단추가 강조 표시된 쿼리 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="e6281-153">**제출** 옆의 드롭다운 메뉴를 사용하여 **고급**을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="e6281-154">고급 옵션을 사용하여 작업을 제출할 때 추가 옵션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="e6281-156">쿼리를 제출하면 작업 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="e6281-157">작업 상태에는 Hadoop에서 처리되는 작업에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="e6281-158">**작업 상태**는 작업의 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="e6281-159">상태는 정기적으로 업데이트됩니다. 또는 새로 고침 아이콘을 사용하여 상태를 수동으로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![작업 상태가 강조 표시된 작업 보기 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="e6281-161">**작업 상태**가 **완료됨**으로 변경되면 DAG(방향성 비순환 그래프)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="e6281-162">이 다이어그램은 Hive 쿼리 처리 시 Tez에 의해 결정된 실행 경로를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="e6281-163">Tez는 로컬 클러스터 기반 Hive의 기본 실행 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6281-164">또한 Linux 기반 HDInsight 클러스터를 사용하는 경우 Tez는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="e6281-165">Windows 기반 HDInsight에서 기본값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="e6281-166">사용하려면 Hive 쿼리의 시작 부분에 `set hive.execution.engine = tez;` 라인을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="e6281-167">출력을 보려면 **작업 출력** 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="e6281-168">이 경우 823이며, 이는 sample_08 테이블의 행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="e6281-169">**작업 로그** 및 **YARN 로그 다운로드** 링크를 사용하여 작업에 대한 진단 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="e6281-170">**Batch** 필드를 **대화형**으로 변경하여 Hive 작업을 대화형으로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="e6281-171">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-171">Then select **Execute**.</span></span>

    ![대화형 및 실행 단추가 강조 표시된 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="e6281-173">대화형 쿼리는 처리 중에 생성된 출력 로그를 **HiveServer2 출력** 창으로 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6281-174">이 정보는 작업 완료 후 **작업 로그** 링크에서 사용할 수 있는 것과 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![출력 로그의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="e6281-176">Hive 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e6281-176">Create a Hive project</span></span>

<span data-ttu-id="e6281-177">또한 여러 Hive 스크립트를 포함하는 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="e6281-178">스크립트와 관련되거나 스크립트를 버전 제어 시스템에 저장하려는 경우 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="e6281-179">Visual Studio에서 **파일**, **새로 만들기** 및 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="e6281-180">프로젝트 목록에서 **템플릿**, **Azure Data Lake**를 차례로 확장한 다음 **HIVE(HDInsight)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="e6281-181">템플릿 목록에서 **Hive 샘플**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="e6281-182">이름과 위치를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-182">Enter a name and location, and then select **OK**.</span></span>

    ![Azure Data Lake, HIVE, Hive 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="e6281-184">**Hive 샘플** 프로젝트에는 **WebLogAnalysis.hql** 및 **SensorDataAnalysis.hql**이라는 두 개의 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="e6281-185">창 위쪽의 동일한 **제출** 단추를 사용하여 이러한 스크립트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="e6281-186">Pig 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e6281-186">Create a Pig project</span></span>

<span data-ttu-id="e6281-187">Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공하지만 Pig는 데이터에 대한 변환을 수행하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="e6281-188">Pig는 변환의 파이프라인을 개발할 수 있는 언어(Pig Latin)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="e6281-189">로컬 클러스터에서 Pig를 사용하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e6281-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="e6281-190">Visual Studio를 열고 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="e6281-191">프로젝트 목록에서 **템플릿**, **Azure Data Lake**를 차례로 확장한 다음 **Pig(HDInsight)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="e6281-192">템플릿 목록에서 **Pig 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="e6281-193">이름과 위치를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-193">Enter a name, location, and then select **OK**.</span></span>

    ![Azure Data Lake, Pig, Pig 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="e6281-195">이 프로젝트로 만든 **script.pig** 파일의 콘텐츠로 다음 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="e6281-196">Pig에서 Hive와 다른 언어를 사용하는 동안 **제출** 단추를 통해 두 언어 간에 작업을 실행하는 방법은 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="e6281-197">**제출** 옆에 있는 드롭다운을 선택하면 Pig의 고급 제출 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="e6281-199">또한 작업 상태 및 출력은 Hive 쿼리와 동일하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![완료된 Pig 작업의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="e6281-201">작업 보기</span><span class="sxs-lookup"><span data-stu-id="e6281-201">View jobs</span></span>

<span data-ttu-id="e6281-202">또한 Data Lake 도구를 사용하면 Hadoop에서 실행된 작업에 대한 정보를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="e6281-203">다음 단계를 사용하여 로컬 클러스터에서 실행된 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="e6281-204">**서버 탐색기**에서 로컬 클러스터를 마우스 오른쪽 단추로 클릭한 다음 **작업 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="e6281-205">클러스터에 제출된 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![작업 보기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="e6281-207">작업 목록에서 작업 세부 정보를 볼 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-207">From the list of jobs, select one to view the job details.</span></span>

    ![작업 중 하나가 강조 표시된 작업 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="e6281-209">표시되는 정보는 출력 및 로그 정보를 보는 링크를 포함하여 Hive 또는 Pig 쿼리를 실행한 후에 표시되는 정보와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="e6281-210">또한 여기에서 작업을 수정하고 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="e6281-211">Hive 데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="e6281-211">View Hive databases</span></span>

1. <span data-ttu-id="e6281-212">**서버 탐색기**에서 **HDInsight 로컬 클러스터** 항목, **Hive 데이터베이스**를 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="e6281-213">로컬 클러스터에 있는 **Default** 및 **xademo** 데이터베이스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="e6281-214">데이터베이스 확장하면 데이터베이스 내의 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-214">Expanding a database shows the tables within the database.</span></span>

    ![데이터베이스가 확장된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="e6281-216">테이블을 확장하면 해당 테이블에 대한 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="e6281-217">데이터를 신속하게 보려면 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 100개 행 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![테이블이 확장되고 상위 100개 행 보기가 선택된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="e6281-219">데이터베이스 및 테이블 속성</span><span class="sxs-lookup"><span data-stu-id="e6281-219">Database and table properties</span></span>

<span data-ttu-id="e6281-220">데이터베이스 또는 테이블의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="e6281-221">**속성**을 선택하면 [속성] 창에서 선택한 항목에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="e6281-222">예를 들어, 다음 스크린샷에 표시된 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6281-222">For example, see the information shown in the following screenshot:</span></span>

![속성 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="e6281-224">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e6281-224">Create a table</span></span>

<span data-ttu-id="e6281-225">테이블을 만들려면 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **테이블 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![테이블 만들기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="e6281-227">그런 다음 형식을 사용하여 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-227">You can then create the table using a form.</span></span> <span data-ttu-id="e6281-228">다음 스크린샷 맨 아래에서 테이블을 만드는 데 사용할 원시 HiveQL를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6281-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![테이블을 생성하기 위해 사용한 양식의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="e6281-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6281-230">Next steps</span></span>

* [<span data-ttu-id="e6281-231">Hortonworks Sandbox의 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="e6281-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="e6281-232">Hadoop 자습서 - HDP 시작</span><span class="sxs-lookup"><span data-stu-id="e6281-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
