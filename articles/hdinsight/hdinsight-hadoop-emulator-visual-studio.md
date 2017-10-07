---
title: "Hortonworks 샌드박스-Azure HDInsight와 Visual Studio 용 aaaData 호수 도구 | Microsoft Docs"
description: "어떻게 toouse hello Azure 데이터 레이크 tools for Visual Studio 로컬 VM에서 실행 하는 hello Hortonworks 샌드박스를 알아봅니다. 이러한 도구를 통해 만들 하 고 hello 샌드박스 및 작업 출력 보기 및 기록에 Hive 및 Pig 작업을 실행할 수 있습니다."
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
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="93a7c-104">Visual Studio에 대 한 hello Azure 데이터 레이크 도구를 사용 하 여 hello Hortonworks 샌드박스로</span><span class="sxs-lookup"><span data-stu-id="93a7c-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="93a7c-105">Azure Data Lake는 제네릭 Hadoop 클러스터를 사용하기 위한 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="93a7c-106">이 문서 필요한 toouse hello 데이터 레이크 도구와 hello 로컬 가상 컴퓨터에서 실행 중인 Hortonworks 샌드박스 hello 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="93a7c-107">Hello Hortonworks 샌드박스를 사용 하 여 로컬 개발 환경에서 Hadoop으로 toowork가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="93a7c-108">원하는 toodeploy를 솔루션을 개발한 후 그 tooan HDInsight 클러스터를 옮길 수 배율을 사용할 때.</span><span class="sxs-lookup"><span data-stu-id="93a7c-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93a7c-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93a7c-109">Prerequisites</span></span>

* <span data-ttu-id="93a7c-110">hello Hortonworks 샌드박스, 개발 환경에서 가상 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="93a7c-111">이 문서 작성 하 고 Oracle VirtualBox에서 실행 되는 hello 샌드박스를 사용 하 여 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="93a7c-112">Hello 샌드박스를 설정에 대 한 자세한 내용은 참조 hello [hello Hortonworks 샌드박스 시작 합니다.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="93a7c-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="93a7c-113">문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93a7c-113">document.</span></span>

* <span data-ttu-id="93a7c-114">Visual Studio 2013, Visual Studio 2015 또는 Visual Studio 2017(모든 에디션)</span><span class="sxs-lookup"><span data-stu-id="93a7c-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="93a7c-115">hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/) 2.7.1 이상.</span><span class="sxs-lookup"><span data-stu-id="93a7c-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="93a7c-116">hello [Azure 데이터 레이크 l Visual Studio 용 도구](https://www.microsoft.com/download/details.aspx?id=49504)합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="93a7c-117">Hello 샌드박스에 대 한 암호 구성</span><span class="sxs-lookup"><span data-stu-id="93a7c-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="93a7c-118">해당 hello Hortonworks 샌드박스 실행 되 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93a7c-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="93a7c-119">Hello에서 hello 단계를 수행 [hello Hortonworks 샌드박스에서](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) 문서.</span><span class="sxs-lookup"><span data-stu-id="93a7c-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="93a7c-120">이러한 단계는 hello SSH에 대 한 hello 암호 구성 `root` 계정을 한 Ambari hello `admin` 계정.</span><span class="sxs-lookup"><span data-stu-id="93a7c-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="93a7c-121">이 암호는 Visual Studio에서 toohello 샌드박스를 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="93a7c-122">Hello 도구 toohello 샌드박스 연결</span><span class="sxs-lookup"><span data-stu-id="93a7c-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="93a7c-123">Visual Studio를 열고 **보기** 및 **서버 탐색기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="93a7c-124">**서버 탐색기**, 마우스 오른쪽 단추로 클릭 hello **HDInsight** 항목을 선택한 후 **tooHDInsight 에뮬레이터 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![스크린샷의 서버 탐색기와 연결 tooHDInsight 강조 표시 하는 에뮬레이터](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="93a7c-126">Hello에서 **tooHDInsight 에뮬레이터 연결** 대화 상자 Ambari를 위해 구성 된 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="93a7c-128">선택 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="93a7c-129">사용 하 여 hello **암호** hello에 대 한 구성 필드 tooenter hello 암호 `root` 계정.</span><span class="sxs-lookup"><span data-stu-id="93a7c-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="93a7c-130">Hello hello 기본값에 다른 필드를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-130">Leave hello other fields at hello default value.</span></span>

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="93a7c-132">선택 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="93a7c-133">Hello 서비스 toofinish의 유효성 검사 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="93a7c-134">경우에 따라 유효성 검사 실패 하 고 tooupdate hello 구성 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="93a7c-135">유효성 검사에 실패할 경우 선택 **업데이트**, hello 구성 및 서비스 toofinish hello에 대 한 확인을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![업데이트 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="93a7c-137">hello 업데이트 프로세스 Ambari toomodify hello Hortonworks 샌드박스 구성 toowhat에서 예상 하는 hello 데이터 레이크 tools for Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="93a7c-138">유효성 검사 완료 되 면 선택 **마침** toocomplete 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="93a7c-139">![마침 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="93a7c-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="93a7c-140">개발 환경 및 hello toohello 가상 컴퓨터를 할당 된 메모리 크기의 hello 속도 따라 수 몇 분 tooconfigure 수행 하 고 hello 서비스의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="93a7c-141">다음이 단계를 따른 후 해야는 **HDInsight 로컬 클러스터** hello에서 서버 탐색기의 항목 **HDInsight** 섹션.</span><span class="sxs-lookup"><span data-stu-id="93a7c-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="93a7c-142">Hive 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="93a7c-142">Write a Hive query</span></span>

<span data-ttu-id="93a7c-143">Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="93a7c-144">사용 하 여 hello 다음 toolearn hello 로컬 클러스터에 대 한 주문형 toorun 쿼리 하는 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="93a7c-145">**서버 탐색기**를 이전에 추가한 hello 로컬 클러스터에 대 한 hello 항목을 마우스 오른쪽 단추로 클릭 한 다음 선택 **는 하이브 쿼리를 작성할**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Hive 쿼리 작성이 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="93a7c-147">새 쿼리 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-147">A new query window appears.</span></span> <span data-ttu-id="93a7c-148">신속 하 게 수 여기 쓰고 쿼리 toohello 로컬 클러스터에 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="93a7c-149">새 쿼리 창 hello hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="93a7c-150">toorun hello 쿼리의 **전송** hello 창의 위쪽에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="93a7c-151">Hello 다른 값을 둡니다 (**일괄 처리** 서버 이름과) hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Hello 전송 단추가 강조 표시 된 쿼리 창의 스크린 샷](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="93a7c-153">또한도 사용할 수 있습니다 hello 드롭 다운 메뉴 다음**전송** tooselect **고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="93a7c-154">고급 옵션을 사용 하면 추가 옵션 tooprovide hello 작업을 제출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="93a7c-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="93a7c-156">Hello 쿼리를 제출 하면 hello 작업 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="93a7c-157">hello 작업 상태는 hadoop 처리는 hello 작업에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="93a7c-158">**작업 상태** hello hello 작업 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="93a7c-159">hello 상태 새로 고침 아이콘 toorefresh hello를 수동으로 진행할 수 있습니다 또는 hello 상태는 주기적으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![작업 상태가 강조 표시된 작업 보기 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="93a7c-161">Hello 후 **작업 상태** 쪽 변경**마침**, 전달 된 비순환 그래프 (DAG) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="93a7c-162">이 다이어그램에서는 hello 하이브 쿼리를 처리할 때 Tez에 의해 결정 된 hello 실행 경로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="93a7c-163">Tez는 hello 로컬 클러스터에 Hive 위한 되는 hello 기본 실행 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93a7c-164">Tez는 Linux 기반 HDInsight 클러스터를 사용 하는 경우 hello 기본값 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="93a7c-165">Windows 기반 HDInsight의 hello 기본 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="93a7c-166">toouse 것 hello 줄을 추가 해야 하는, `set hive.execution.engine = tez;` 하이브 쿼리 toohello 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="93a7c-167">사용 하 여 hello **작업 출력** tooview hello 출력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="93a7c-168">이 경우,이 823 hello hello sample_08 테이블의 행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="93a7c-169">Hello를 사용 하 여 hello 작업에 대 한 진단 정보를 볼 수 **작업 로그** 및 **YARN 로그 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="93a7c-170">Hello를 변경 하 여 하이브 작업을 대화형으로 실행할 수도 있습니다 **일괄 처리** 너무 필드**Interactive'**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="93a7c-171">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-171">Then select **Execute**.</span></span>

    ![대화형 및 실행 단추가 강조 표시된 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="93a7c-173">스트림을 hello toohello 처리 중에 생성 된 출력 로그는 대화형 쿼리 **HiveServer2 출력** 창.</span><span class="sxs-lookup"><span data-stu-id="93a7c-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93a7c-174">hello 정보는 hello hello에서 사용할 수 있는 동일한 **작업 로그** 작업이 완료 된 후 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![출력 로그의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="93a7c-176">Hive 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="93a7c-176">Create a Hive project</span></span>

<span data-ttu-id="93a7c-177">또한 여러 Hive 스크립트를 포함하는 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="93a7c-178">스크립트와 관련 된 또는 버전 제어 시스템에 toostore 스크립트를 원하는 경우 프로젝트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="93a7c-179">Visual Studio에서 **파일**, **새로 만들기** 및 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="93a7c-180">프로젝트의 hello 목록에서 확장 **템플릿**, 확장 **Azure 데이터 레이크**를 선택한 후 **하이브 (HDInsight)**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="93a7c-181">Hello 템플릿 목록에서 선택 **하이브 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="93a7c-182">이름과 위치를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-182">Enter a name and location, and then select **OK**.</span></span>

    ![Azure Data Lake, HIVE, Hive 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="93a7c-184">hello **하이브 샘플** 프로젝트에 두 개의 스크립트 **WebLogAnalysis.hql** 및 **SensorDataAnalysis.hql**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="93a7c-185">이러한 스크립트를 사용 하 여 hello 동일 제출할 수 **전송** hello hello 창 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="93a7c-186">Pig 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="93a7c-186">Create a Pig project</span></span>

<span data-ttu-id="93a7c-187">Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공하지만 Pig는 데이터에 대한 변환을 수행하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="93a7c-188">Pig 변환의 파이프라인 toodevelop를 허용 하는 언어 (Pig 라틴 문자)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="93a7c-189">toouse Pig hello 로컬 클러스터와 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="93a7c-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="93a7c-190">Visual Studio를 열고 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="93a7c-191">프로젝트의 hello 목록에서 확장 **템플릿**, 확장 **Azure 데이터 레이크**를 선택한 후 **Pig (HDInsight)**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="93a7c-192">Hello 템플릿 목록에서 선택 **Pig 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="93a7c-193">이름과 위치를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-193">Enter a name, location, and then select **OK**.</span></span>

    ![Azure Data Lake, Pig, Pig 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="93a7c-195">콘텐츠로 사용 hello hello 텍스트를 다음 hello 입력 **script.pig** 이 프로젝트를 사용 하 여 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="93a7c-196">다른 언어를 사용 하 여 하이브 보다 Pig, hello 작업을 실행 하는 방법에 일관성이 hello 통해 두 언어 간 **전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="93a7c-197">선택 hello 옆에 있는 드롭 다운 **전송** Pig에 대 한 고급 전송 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="93a7c-199">hello 작업 상태 및 출력도 표시 됩니다, 그리고 Hive 쿼리도 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![완료된 Pig 작업의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="93a7c-201">작업 보기</span><span class="sxs-lookup"><span data-stu-id="93a7c-201">View jobs</span></span>

<span data-ttu-id="93a7c-202">데이터 레이크 도구 tooeasily Hadoop에서 실행 된 작업에 대 한 정보 보기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="93a7c-203">Hello 로컬 클러스터에서 실행 하는 단계 toosee hello 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="93a7c-204">**서버 탐색기**를 hello 로컬 클러스터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **작업 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="93a7c-205">제출 된 toohello 클러스터 된 작업 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![작업 보기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="93a7c-207">작업의 hello 목록에서 하나를 선택 tooview hello에 대 한 작업 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="93a7c-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![스크린샷의 작업을 사용 하 여 브라우저 강조 표시 하는 hello 작업 중 하나](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="93a7c-209">비슷한 toowhat 링크 tooview hello 출력 및 로그 정보를 포함 하 여 하이브 또는 Pig 쿼리를 실행 한 후 참조에 hello 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="93a7c-210">또한 수정할 수 있으며 여기에서 hello 작업을 다시 제출 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93a7c-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="93a7c-211">Hive 데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="93a7c-211">View Hive databases</span></span>

1. <span data-ttu-id="93a7c-212">**서버 탐색기**, hello 확장 **HDInsight 로컬 클러스터** 항목을 확장 한 후 **하이브 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="93a7c-213">hello **기본** 및 **xademo** 데이터베이스 hello 로컬 클러스터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="93a7c-214">데이터베이스를 확장할 hello 데이터베이스 내에서 hello 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-214">Expanding a database shows hello tables within hello database.</span></span>

    ![데이터베이스가 확장된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="93a7c-216">테이블을 확장에 해당 테이블에 대 한 hello 열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="93a7c-217">tooquickly 뷰 hello 데이터 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **보기 Top 100 Rows**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![테이블이 확장되고 상위 100개 행 보기가 선택된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="93a7c-219">데이터베이스 및 테이블 속성</span><span class="sxs-lookup"><span data-stu-id="93a7c-219">Database and table properties</span></span>

<span data-ttu-id="93a7c-220">데이터베이스 또는 테이블의 hello 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="93a7c-221">선택 하면 **속성** hello 속성 창에서 선택한 hello 항목에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="93a7c-222">예를 들어 hello 스크린 샷 뒤에 표시 된 hello 정보 참조:</span><span class="sxs-lookup"><span data-stu-id="93a7c-222">For example, see hello information shown in hello following screenshot:</span></span>

![속성 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="93a7c-224">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="93a7c-224">Create a table</span></span>

<span data-ttu-id="93a7c-225">toocreate 테이블을 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Create Table**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![테이블 만들기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="93a7c-227">그런 다음 폼을 사용 하는 hello 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-227">You can then create hello table using a form.</span></span> <span data-ttu-id="93a7c-228">다음 스크린 샷 hello의 hello 맨 아래에 볼 수 있습니다는 사용 되는 toocreate hello 테이블 원시 HiveQL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a7c-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Toocreate 테이블을 사용 하는 hello 폼의 스크린 샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="93a7c-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93a7c-230">Next steps</span></span>

* [<span data-ttu-id="93a7c-231">Hello Hortonworks 샌드박스의 hello ropes 학습</span><span class="sxs-lookup"><span data-stu-id="93a7c-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="93a7c-232">Hadoop 자습서 - HDP 시작</span><span class="sxs-lookup"><span data-stu-id="93a7c-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
