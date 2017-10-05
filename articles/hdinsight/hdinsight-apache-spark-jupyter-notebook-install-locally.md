---
title: "Jupyter를 로컬로 설치하고 Azure HDInsight Spark 클러스터에 연결 | Microsoft Docs"
description: "컴퓨터에 로컬로 Jupyter 노트북을 설치하고 Azure HDInsight에서 Apache Spark 클러스터에 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="0fce6-103">컴퓨터에 Jupyter 노트북을 설치하고 HDInsight에서 Apache Spark에 연결</span><span class="sxs-lookup"><span data-stu-id="0fce6-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="0fce6-104">이 문서에서는 Spark Magic이 있는 사용자 지정 PySpark(Python용) 및 Spark(Scala용) 커널을 사용하여 Jupyter Notebook을 설치한 후 해당 노트북을 HDInsight 클러스터에 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="0fce6-105">로컬 컴퓨터에 Jupyter를 설치하는 여러 가지 이유와 몇 가지 어려운 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="0fce6-106">이에 대한 자세한 내용은 이 문서의 끝에 있는 [내 컴퓨터에 Jupyter를 설치해야 하는 이유](#why-should-i-install-jupyter-on-my-computer) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="0fce6-107">Jupyter 및 Spark Magic을 컴퓨터에 설치하는 것과 관련된 세 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="0fce6-108">Jupyter 노트북 설치</span><span class="sxs-lookup"><span data-stu-id="0fce6-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="0fce6-109">Spark Magic과 함께 PySpark 및 Spark 커널 설치</span><span class="sxs-lookup"><span data-stu-id="0fce6-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="0fce6-110">HDInsight에서 Spark 클러스터에 액세스하도록 Spark Magic 구성</span><span class="sxs-lookup"><span data-stu-id="0fce6-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="0fce6-111">HDInsight 클러스터의 Jupyter Notebook에 사용할 수 있는 사용자 지정 커널 및 Spark Magic에 대한 자세한 내용은 [HDInsight의 Apache Spark Linux 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fce6-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0fce6-112">Prerequisites</span></span>
<span data-ttu-id="0fce6-113">여기에 나열된 필수 구성 요소는 Jupyter를 설치하기 위한 것이 아니며</span><span class="sxs-lookup"><span data-stu-id="0fce6-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="0fce6-114">Jupyter 노트북이 설치되면 HDInsight 클러스터를 노트북을 연결하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="0fce6-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="0fce6-115">An Azure subscription.</span></span> <span data-ttu-id="0fce6-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0fce6-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0fce6-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="0fce6-119">컴퓨터에 Jupyter 노트북 설치</span><span class="sxs-lookup"><span data-stu-id="0fce6-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="0fce6-120">Jupyter 노트북을 설치하려면 먼저 Python을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="0fce6-121">Python 및 Jupyter 둘 다 [Anaconda 배포](https://www.continuum.io/downloads)의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="0fce6-122">Anaconda를 설치할 때 Python 배포를 설치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="0fce6-123">Anaconda를 설치한 후 적절한 명령을 실행하여 Jupyter 설치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="0fce6-124">사용하는 플랫폼용 [Anaconda 설치 관리자](https://www.continuum.io/downloads) 를 다운로드하고 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="0fce6-125">설치 마법사를 실행하는 동안 PATH 변수에 Anaconda를 추가하는 옵션을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="0fce6-126">다음 명령을 실행하여 Jupyter를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="0fce6-127">Jupyter 설치에 대한 자세한 내용은 [Anaconda를 사용하여 Jupyter 설치](http://jupyter.readthedocs.io/en/latest/install.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="0fce6-128">커널 및 Spark Magic 설치</span><span class="sxs-lookup"><span data-stu-id="0fce6-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="0fce6-129">Spark Magic, PySpark 및 Spark 커널을 설치 하는 방법에 대한 지침은 GitHub에서 [sparkmagic 설명서](https://github.com/jupyter-incubator/sparkmagic#installation)의 설치 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="0fce6-130">Spark Magic 설명서의 첫 번째 단계에서는 Spark Magic 설치를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="0fce6-131">연결하려는 HDInsight 클러스터의 버전에 따라 링크의 첫 번째 단계를 다음 명령으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="0fce6-132">그런 다음, Spark Magic 설명서의 나머지 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="0fce6-133">다른 커널을 설치하려면 Spark Magic 설치 지침 섹션에서 3단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="0fce6-134">클러스터 v3.4의 경우 `pip install sparkmagic==0.2.3`을 실행하여 sparkmagic 0.2.3을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="0fce6-135">클러스터 v3.5 및 v3.6의 경우 `pip install sparkmagic==0.11.2`를 실행하여 sparkmagic 0.11.2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="0fce6-136">HDInsight Spark 클러스터에 연결하도록 Spark Magic 구성</span><span class="sxs-lookup"><span data-stu-id="0fce6-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="0fce6-137">이 섹션에서는 이전에 설치한 Spark Magic이 Azure HDInsight에서 이미 만든 Apache Spark 클러스터에 연결되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="0fce6-138">Jupyter 구성 정보는 일반적으로 사용자 홈 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="0fce6-139">OS 플랫폼에서 홈 디렉터리를 찾으려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="0fce6-140">Python 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-140">Start the Python shell.</span></span> <span data-ttu-id="0fce6-141">명령 창에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="0fce6-142">Python 셸에서 다음 명령을 입력하여 홈 디렉터리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="0fce6-143">홈 디렉터리로 이동하고 **.sparkmagic** 폴더가 아직 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="0fce6-144">이 폴더에 **config.json** 이라는 파일을 만들고 그 안에 다음 JSON 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="0fce6-145">**{USERNAME}**, **{CLUSTERDNSNAME}** 및 **{BASE64ENCODEDPASSWORD}**를 적합한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="0fce6-146">즐겨 사용하는 프로그래밍 언어 또는 온라인의 다양한 유틸리티를 사용하여 실제 암호에 대한 base64 인코딩 암호를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="0fce6-147">`config.json`에서 올바른 하트 비트 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="0fce6-148">`kernel_python_credentials` 및 이전에 추가한 `kernel_scala_credentials` 조각과 같은 수준에서 이러한 설정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="0fce6-149">하트비트 설정을 추가하는 방법 및 추가할 위치에 대한 예제를 보려면 [샘플 config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="0fce6-150">`sparkmagic 0.2.3`(v3.4 클러스터)의 경우 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="0fce6-151">`sparkmagic 0.11.2`(v3.5 및 v3.6 클러스터)의 경우 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="0fce6-152">세션이 유출되지 않도록 하트 비트가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="0fce6-153">컴퓨터가 절전 모드로 전환되거나 종료되면, 하트비트가 전송되지 않으므로 세션이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="0fce6-154">클러스터 v3.4의 경우, 이 동작을 사용하지 않도록 설정하려면 Ambari UI에서 Livy 구성 `livy.server.interactive.heartbeat.timeout`를 `0`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="0fce6-155">클러스터 v 3.5의 경우, 위의 3.5 구성을 설정하지 않으면 세션이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="0fce6-156">Jupyter를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-156">Start Jupyter.</span></span> <span data-ttu-id="0fce6-157">명령 프롬프트에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="0fce6-158">Jupyter 노트북을 사용하여 클러스터에 연결할 수 있는지와 커널에서 사용 가능한 Spark Magic을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="0fce6-159">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-159">Perform the following steps.</span></span>

    <span data-ttu-id="0fce6-160">a.</span><span class="sxs-lookup"><span data-stu-id="0fce6-160">a.</span></span> <span data-ttu-id="0fce6-161">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-161">Create a new notebook.</span></span> <span data-ttu-id="0fce6-162">오른쪽 구석에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="0fce6-163">기본 커널 **Python2**와 설치하는 두 개의 새 커널 **PySpark** 및 **Spark**가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="0fce6-164">**PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-164">Click **PySpark**.</span></span>

    <span data-ttu-id="0fce6-165">![Jupyter 노트북의 커널](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter 노트북의 커널")</span><span class="sxs-lookup"><span data-stu-id="0fce6-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="0fce6-166">b.</span><span class="sxs-lookup"><span data-stu-id="0fce6-166">b.</span></span> <span data-ttu-id="0fce6-167">다음 코드 조각을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="0fce6-168">출력을 검색할 수 있으면 HDInsight 클러스터에 대한 연결이 테스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="0fce6-169">다른 클러스터에 연결하도록 노트북 구성을 업데이트하려는 경우 위의 3단계와 같이 새 값 집합으로 config.json을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="0fce6-170">내 컴퓨터에 Jupyter를 설치해야 해야 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0fce6-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="0fce6-171">컴퓨터에 Jupyter를 설치한 다음 HDInsight의 Spark 클러스터에 연결하는 데는 여러 가지 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="0fce6-172">Jupyter 노트북을 Azure HDInsight의 Spark 클러스터에 이미 사용할 수 있더라도 컴퓨터에 Jupyter를 설치하면 로컬에서 노트북을 만들고, 실행 중인 클러스터에 대해 응용 프로그램을 테스트한 다음 클러스터에 노트북을 업로드하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="0fce6-173">노트북에 클러스터를 업로드하려면 클러스터에서 실행되는 Jupyter 노트북을 사용하여 업로드하거나 클러스터와 연결된 저장소 계정의 /HdiNotebooks 폴더에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="0fce6-174">클러스터에 Notebook을 저장하는 방법에 대한 자세한 내용은 [Jupyter Notebook이 저장되는 위치](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fce6-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="0fce6-175">로컬에서 사용할 수 있는 Notebook을 사용하여 응용 프로그램 요구 사항에 따라 다른 Spark 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="0fce6-176">GitHub를 사용하여 원본 제어 시스템을 구현하고 Notebook에 대한 버전을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="0fce6-177">여러 사용자가 동일한 Notebook으로 작업할 수 있는 공동 작업 환경이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="0fce6-178">클러스터 없이 로컬로 Notebook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="0fce6-179">Notebook 또는 개발 환경을 수동으로 관리하기 위해서가 아니라 Notebook을 테스트하기 위해 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="0fce6-180">클러스터에서 Jupyter 설치를 구성하는 것보다 자체 로컬 개발 환경을 구성하는 것이 더 쉬울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="0fce6-181">하나 이상의 원격 클러스터를 구성하지 않고 로컬로 설치한 모든 소프트웨어를 모두 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="0fce6-182">로컬 컴퓨터에 설치된 Jupyter를 사용하면 여러 사용자가 동일한 Spark 클러스터에서 동시에 동일한 Notebook을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="0fce6-183">이러한 상황에서 여러 Livy 세션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="0fce6-184">문제가 발생하여 디버깅하려는 경우 어떤 사용자에게 어떤 Livy 세션이 속하는지를 추적하는 복잡한 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fce6-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="0fce6-185"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="0fce6-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0fce6-186">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="0fce6-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0fce6-187">시나리오</span><span class="sxs-lookup"><span data-stu-id="0fce6-187">Scenarios</span></span>
* [<span data-ttu-id="0fce6-188">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="0fce6-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0fce6-189">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="0fce6-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0fce6-190">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="0fce6-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0fce6-191">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="0fce6-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0fce6-192">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="0fce6-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0fce6-193">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="0fce6-193">Create and run applications</span></span>
* [<span data-ttu-id="0fce6-194">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0fce6-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0fce6-195">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0fce6-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0fce6-196">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="0fce6-196">Tools and extensions</span></span>
* [<span data-ttu-id="0fce6-197">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="0fce6-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0fce6-198">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="0fce6-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0fce6-199">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="0fce6-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0fce6-200">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="0fce6-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0fce6-201">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="0fce6-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="0fce6-202">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0fce6-202">Manage resources</span></span>
* [<span data-ttu-id="0fce6-203">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0fce6-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0fce6-204">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="0fce6-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
