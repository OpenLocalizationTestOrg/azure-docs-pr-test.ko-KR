---
title: "로컬로 aaaInstall Jupyter & tooan Azure HDInsight Spark 클러스터에 연결 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Jupyter 노트북 컴퓨터에 로컬로 Azure HDInsight의 Apache Spark 클러스터 tooan 연결 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="e31b1-103">Jupyter 노트북 컴퓨터에 설치 하 고 tooApache HDInsight의 Spark를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="e31b1-104">이 문서에서는 설명 어떻게 hello로 tooinstall Jupyter 노트북 (Python)에 대 한 사용자 지정 PySpark 및 매직, 멤버 및 hello 노트북 tooan HDInsight 클러스터에 연결을 사용 하는 (Scala) 용 Spark 커널을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="e31b1-105">다양 한 이유로 tooinstall Jupyter 로컬 컴퓨터에 있을 수 있으며 다른 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="e31b1-106">이 대 한 자세한에 대 한 hello 섹션을 참조 [내 컴퓨터에서에 Jupyter 설치 해야 이유](#why-should-i-install-jupyter-on-my-computer) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="e31b1-107">Jupyter 및 hello Spark 매직 컴퓨터에 설치에 관련 된 세 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="e31b1-108">Jupyter 노트북 설치</span><span class="sxs-lookup"><span data-stu-id="e31b1-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="e31b1-109">Spark 매직 hello로 PySpark hello 및 Spark 커널 설치</span><span class="sxs-lookup"><span data-stu-id="e31b1-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="e31b1-110">HDInsight의 Spark 매직 tooaccess Spark 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="e31b1-111">사용자 지정 커널 hello 및 HDInsight 클러스터와 Jupyter 노트북에 사용할 수 있는 hello Spark 매직에 대 한 자세한 내용은 참조 [HDInsight의 Apache Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 클러스터](hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e31b1-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e31b1-112">Prerequisites</span></span>
<span data-ttu-id="e31b1-113">여기에 나열 된 hello 필수 Jupyter 설치를 위한 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="e31b1-114">이들은 연결 hello Jupyter 노트북 tooan HDInsight 클러스터에 대 한 hello 노트북에 설치 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="e31b1-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e31b1-115">An Azure subscription.</span></span> <span data-ttu-id="e31b1-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e31b1-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e31b1-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e31b1-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e31b1-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="e31b1-119">컴퓨터에 Jupyter 노트북 설치</span><span class="sxs-lookup"><span data-stu-id="e31b1-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="e31b1-120">Jupyter 노트북을 설치하려면 먼저 Python을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="e31b1-121">Python 및 Jupyter 둘 다 사용할 수 있는 hello의 일부로 [Anaconda 배포](https://www.continuum.io/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="e31b1-122">Anaconda를 설치할 때 Python 배포를 설치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="e31b1-123">Anaconda가 설치 되 면 적절 한 명령을 실행 하 여 hello Jupyter 설치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="e31b1-124">Hello 다운로드 [Anaconda installer](https://www.continuum.io/downloads) 플랫폼과 실행된 hello 설치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="e31b1-125">Hello 설치 마법사를 실행 하는 동안 hello 옵션 tooadd Anaconda tooyour 경로 변수를 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="e31b1-126">다음 명령은 tooinstall Jupyter hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="e31b1-127">Jupyter 설치에 대한 자세한 내용은 [Anaconda를 사용하여 Jupyter 설치](http://jupyter.readthedocs.io/en/latest/install.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e31b1-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="e31b1-128">Hello 커널 및 Spark 매직 설치</span><span class="sxs-lookup"><span data-stu-id="e31b1-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="e31b1-129">Tooinstall hello Spark 매직, PySpark hello 및 Spark 커널 hello hello 설치 지침을 따라 방법에 대 한 지침은 [sparkmagic 설명서](https://github.com/jupyter-incubator/sparkmagic#installation) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="e31b1-130">hello 첫 번째 hello Spark 매직 설명서의 단계 tooinstall Spark 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="e31b1-131">Hello 링크의 첫 번째 단계에 명령에 연결 하는 hello HDInsight 클러스터의 hello 버전에 따라 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="e31b1-132">그 후 hello 남은 hello Spark 매직 설명서에 나와 있는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="e31b1-133">Tooinstall hello 다른 커널 원한다 면 hello Spark 매직 설치 지침 섹션에서에서 3 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="e31b1-134">클러스터 v3.4의 경우 `pip install sparkmagic==0.2.3`을 실행하여 sparkmagic 0.2.3을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="e31b1-135">클러스터 v3.5 및 v3.6의 경우 `pip install sparkmagic==0.11.2`를 실행하여 sparkmagic 0.11.2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="e31b1-136">Spark 매직 tooconnect tooHDInsight Spark 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="e31b1-137">이 섹션에서는 Azure HDInsight에서 이미 만든 해야 하는 이전 tooconnect tooan Apache Spark 클러스터를 설치 하는 hello Spark 매직을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="e31b1-138">hello Jupyter 구성 정보는 일반적으로 hello 사용자가 홈 디렉터리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="e31b1-139">toolocate 모든 OS 플랫폼의 경우 다음 형식 hello 홈 디렉터리는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="e31b1-140">Hello Python 셸을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-140">Start hello Python shell.</span></span> <span data-ttu-id="e31b1-141">명령 창에서 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="e31b1-142">Python 셸 hello hello 명령 toofind hello 홈 디렉터리를 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="e31b1-143">Toohello 홈 디렉터리를 이동 하 고 라는 폴더를 만들어 **.sparkmagic** 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e31b1-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="e31b1-144">Hello 폴더 내의 파일을 만들 **config.json** hello 다음 JSON 코드 조각은 그 안에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="e31b1-145">**{USERNAME}**, **{CLUSTERDNSNAME}** 및 **{BASE64ENCODEDPASSWORD}**를 적합한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="e31b1-146">실제 암호에 대 한 다양 한 즐겨 찾는 프로그래밍 언어 또는 온라인 toogenerate base64 인코딩된 암호에서 유틸리티를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="e31b1-147">hello 오른쪽 하트 비트 설정을 구성 `config.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="e31b1-148">이러한 설정은 hello hello로 동일한 수준에 추가 해야 `kernel_python_credentials` 및 `kernel_scala_credentials` 조각에 추가 된 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="e31b1-149">이 tooadd hello 하트 비트 설정 방법 및 위치에 대 한 예제를 보려면 [샘플 config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="e31b1-150">`sparkmagic 0.2.3`(v3.4 클러스터)의 경우 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="e31b1-151">`sparkmagic 0.11.2`(v3.5 및 v3.6 클러스터)의 경우 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="e31b1-152">하트 비트 세션 유출 되지 않습니다 tooensure를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="e31b1-153">컴퓨터 toosleep 라인 또는 종료 될 때 hello 하트 비트를 보내지 않습니다, 그리고 정리 hello 세션 중에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="e31b1-154">클러스터 v3.4 toodisable이이 동작을 원하는 경우 설정할 수 있는 hello 리비 config `livy.server.interactive.heartbeat.timeout` 너무`0` hello Ambari UI에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="e31b1-155">클러스터 v 3.5에 대 한 위의 3.5 hello 구성 설정 하지 않으면 hello 세션 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="e31b1-156">Jupyter를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-156">Start Jupyter.</span></span> <span data-ttu-id="e31b1-157">Hello hello 명령 프롬프트에서 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="e31b1-158">Hello Jupyter 노트북 및 사용할 수 있는 hello Spark 매직 hello 커널 사용할 수 있는 사용 하 여 toohello 클러스터에 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="e31b1-159">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-159">Perform hello following steps.</span></span>

    <span data-ttu-id="e31b1-160">a.</span><span class="sxs-lookup"><span data-stu-id="e31b1-160">a.</span></span> <span data-ttu-id="e31b1-161">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-161">Create a new notebook.</span></span> <span data-ttu-id="e31b1-162">Hello 오른쪽 모서리에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="e31b1-163">Hello 기본 커널 표시 되어야 **Python2** 를 설치 하는 두 개의 새 커널 hello 및 **PySpark** 및 **Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="e31b1-164">**PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-164">Click **PySpark**.</span></span>

    <span data-ttu-id="e31b1-165">![Jupyter 노트북의 커널](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter 노트북의 커널")</span><span class="sxs-lookup"><span data-stu-id="e31b1-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="e31b1-166">b.</span><span class="sxs-lookup"><span data-stu-id="e31b1-166">b.</span></span> <span data-ttu-id="e31b1-167">다음 코드 조각 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="e31b1-168">Hello 출력 성공적으로 가져오면 연결 toohello HDInsight 클러스터에이 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="e31b1-169">Tooupdate hello 노트북 구성 tooconnect tooa 다른 클러스터를 사용 하도록 하려는 경우에 위의 3 단계에서에서와 같이 hello config.json hello 새로운 집합의 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="e31b1-170">내 컴퓨터에 Jupyter를 설치해야 해야 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e31b1-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="e31b1-171">숫자일 수 HDInsight의 Spark tooa 클러스터 이유 이유 수도 tooinstall Jupyter 컴퓨터에 있으며 다음 연결 중입니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="e31b1-172">Jupyter 노트북을 이미 Azure HDInsight의 Spark 클러스터 hello에서 사용할 수 있는 경우에 로컬로 전자 필기장 옵션 toocreate hello, 실행 중인 클러스터에 대 한 응용 프로그램을 테스트 및 hello를 업로드 한 다음 제공 Jupyter 컴퓨터에 설치 노트북 toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="e31b1-173">tooupload hello 전자 필기장 toohello 클러스터 하거나 업로드 하면 클러스터를 실행 하는 hello Jupyter 노트북 또는 hello를 사용 하 여 또는 hello 클러스터와 연결 된 hello 저장소 계정에서 toohello /HdiNotebooks 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="e31b1-174">전자 필기장 hello 클러스터에 저장 되는 방법에 대 한 자세한 내용은 참조 하십시오. [Jupyter 노트북 저장 되어 있는](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="e31b1-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="e31b1-175">로컬에서 사용할 수 있는 hello 전자 필기장 응용 프로그램 요구 사항에 따라 toodifferent Spark 클러스터 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="e31b1-176">GitHub tooimplement 소스 제어 시스템을 사용할 수 있으며 hello 전자 필기장에 대 한 버전 제어.</span><span class="sxs-lookup"><span data-stu-id="e31b1-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="e31b1-177">공동 작업 환경에 여러 사용자가 작업할 수 hello 동일한 점이 전자 필기장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="e31b1-178">클러스터 없이 로컬로 Notebook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="e31b1-179">하기만 하면 클러스터 tootest 전자 필기장에 대 한, 하지 toomanually 전자 필기장 또는 개발 환경을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="e31b1-180">그 보다 쉽게 tooconfigure tooconfigure hello Jupyter 설치 hello 클러스터에서 보다 직접 로컬 개발 환경 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="e31b1-181">하나 이상의 원격 클러스터를 구성 하지 않고 로컬로 설치 된 모든 hello 소프트웨어 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="e31b1-182">로컬 컴퓨터에 설치 된 Jupyter, 여러 사용자가 hello 실행할 수 있습니다 hello hello에 동일한 Spark 클러스터에서 동일한 전자 필기장 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="e31b1-183">이러한 상황에서 여러 Livy 세션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="e31b1-184">문제를 실행 하 고 원하는 어떤 리비 세션 속한 toowhich 사용자 복잡 한 작업 tootrack 하다는 점을, toodebug 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="e31b1-185"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="e31b1-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e31b1-186">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="e31b1-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e31b1-187">시나리오</span><span class="sxs-lookup"><span data-stu-id="e31b1-187">Scenarios</span></span>
* [<span data-ttu-id="e31b1-188">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="e31b1-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e31b1-189">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="e31b1-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e31b1-190">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="e31b1-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e31b1-191">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="e31b1-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e31b1-192">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="e31b1-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e31b1-193">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="e31b1-193">Create and run applications</span></span>
* [<span data-ttu-id="e31b1-194">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e31b1-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e31b1-195">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e31b1-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e31b1-196">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="e31b1-196">Tools and extensions</span></span>
* [<span data-ttu-id="e31b1-197">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="e31b1-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e31b1-198">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="e31b1-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e31b1-199">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="e31b1-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e31b1-200">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="e31b1-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e31b1-201">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="e31b1-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="e31b1-202">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="e31b1-202">Manage resources</span></span>
* [<span data-ttu-id="e31b1-203">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31b1-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e31b1-204">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="e31b1-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
