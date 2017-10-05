---
title: "분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용 | Microsoft Docs"
description: "분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="6de27-103">분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용</span><span class="sxs-lookup"><span data-stu-id="6de27-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="6de27-104">소개</span><span class="sxs-lookup"><span data-stu-id="6de27-104">Introduction</span></span>

<span data-ttu-id="6de27-105">심층 학습은 의료, 교통, 제조 등에 이르는 모든 분야에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="6de27-106">기업은 [이미지 분류](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [음성 인식](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), 개체 인식 및 기계 번역과 같은 어려운 문제를 해결하기 위해 심층 학습으로 전환하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="6de27-107">[Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano 등 [널리 사용되는 수많은 프레임워크](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)가 있습니다. Caffe는 가장 유명한 비기호(명령적) 신경망 프레임워크 중 하나로, 컴퓨터 비전을 비롯한 많은 영역에서 널리 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="6de27-108">또한 [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep)는 Caffe와 Apache Spark를 결합한 것으로 기존의 Hadoop 클러스터에서 Spark ETL 파이프라인과 함께 심층 학습을 쉽게 사용할 수 있어서 시스템 복잡성 및 종단 간 학습에 대한 대기 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="6de27-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/)는 유일한 완전 관리형 클라우드 Hadoop 솔루션으로, Spark, Hive, MapReduce, HBase, Storm, Kafka, R Server에 최적화된 오픈 소스 기반의 분석 클러스터를 제공하고 99.9% SLA를 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="6de27-110">이러한 각 빅 데이터 기술과 ISV 응용 프로그램은 엔터프라이즈급 보안과 모니터링으로 관리 클러스터 형태로 쉽게 배포 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="6de27-111">일부 사용자는 Microsoft의 PaaS Hadoop 제품인 HDInsight에서 심층 학습을 사용하는 방법에 대해 궁금해 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="6de27-112">향후 더 많은 내용을 공유할 예정이지만, 여기서는 HDInsight Spark에서 Caffe를 사용하는 방법에 대한 기술 블로그를 요약하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="6de27-113">이전에 Caffe를 설치했다면 이 프레임워크를 설치하는 것이 약간 어렵다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="6de27-114">이 블로그에서는 먼저 HDInsight 클러스터용 [Spark에서 Caffe](https://github.com/yahoo/CaffeOnSpark)를 설치하는 방법을 설명한 후 기본 제공 MNIST 데모를 통해 CPU에서 HDInsight Spark를 사용하여 분산 심층 학습을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="6de27-115">HDInsight에서 작업을 위해서는 4가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="6de27-116">모든 노드에 필요한 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="6de27-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="6de27-117">헤드 노드에서 HDInsight용 Spark에 Caffe 빌드</span><span class="sxs-lookup"><span data-stu-id="6de27-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="6de27-118">모든 작업자 노드에 필요한 라이브러리 배포</span><span class="sxs-lookup"><span data-stu-id="6de27-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="6de27-119">Caffe 모델 구성 및 분산 실행</span><span class="sxs-lookup"><span data-stu-id="6de27-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="6de27-120">HDInsight는 PaaS 솔루션으로, 뛰어난 플랫폼 기능을 제공하므로 일부 작업을 매우 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="6de27-121">이 블로그 게시물에서 많이 사용하는 기능 중 하나는 [스크립트 작업](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)이라고 하며 셸 명령을 실행하여 클러스터 노드(헤드 노드, 작업자 노드 또는 가장자리 노드)를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="6de27-122">1단계: 모든 노드에 필요한 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="6de27-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="6de27-123">시작하려면 필요한 종속성을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="6de27-124">Caffe 사이트 및 [CaffeOnSpark 사이트](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)는 YARN 모드(HDInsight Spark용 모드)에서 Spark에 대한 종속성을 설치하는 데 매우 유용한 몇 가지 wiki를 제공하지만 HDInsight 플랫폼에 대한 몇 가지 종속성을 더 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="6de27-125">아래와 같이 스크립트 작업을 사용하여 모든 헤드 노드 및 작업자 노드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="6de27-126">해당 종속성은 다른 패키지에도 종속되므로 이 스크립트 작업은 약 20분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="6de27-127">HDInsight 클러스터에 액세스할 수 있는 일부 위치(예: GitHub 위치 또는 기본 Blob Storage 계정)에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


<span data-ttu-id="6de27-128">위의 스크립트 작업에는 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-128">There are two steps in the script action above.</span></span> <span data-ttu-id="6de27-129">첫 번째 단계는 필요한 모든 라이브러리를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="6de27-130">이러한 라이브러리로는 Caffe를 컴파일(예: gflags, glog)하고 Caffe를 실행(예: numpy)하는 데 필요한 라이브러리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="6de27-131">CPU 최적화를 위한 libatlas를 사용 중이지만 MKL 또는 CUDA(GPU용)와 같은 다른 최적화 라이브러리를 설치하는 데는 항상 CaffeOnSpark wiki를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="6de27-132">두 번째 단계는 런타임 중에 Caffe용 protobuf 2.5.0을 다운로드, 컴파일 및 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="6de27-133">Protobuf 2.5.0이 [필요](https://github.com/yahoo/CaffeOnSpark/issues/87)하지만 이 버전은 Ubuntu 16에서 패키지로 제공되지 않으므로 소스 코드에서 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="6de27-134">[다음](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)과 같이 컴파일하는 방법에 대한 몇 가지 리소스가 인터넷에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="6de27-135">시작 과정을 간소화하기 위해서는 모든 작업자 노드 및 헤드 노드 (HDInsight 3.5용)에 대한 클러스터에 대해 이 스크립트 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="6de27-136">클러스터 실행을 위한 스크립트 동작을 실행하거나 클러스터 프로비전 시간 동안에도 스크립트 동작을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="6de27-137">스크립트 동작에 대한 자세한 내용은 [여기](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6de27-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![종속성 설치를 위한 스크립트 동작](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="6de27-139">2단계: 헤드 노드에서 HDInsight용 Spark에 Caffe 빌드</span><span class="sxs-lookup"><span data-stu-id="6de27-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="6de27-140">두 번째 단계는 헤드 노드에 Caffe를 빌드한 후 컴파일된 라이브러리를 모든 작업자 노드에 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="6de27-141">이 단계에서는 [헤드 노드에 대해 ssh](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)를 수행한 후 [CaffeOnSpark 빌드 프로세스](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn)를 따라야 합니다. 몇 가지 추가 단계로 CaffeOnSpark를 빌드하는 데 사용할 수 있는 스크립트가 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="6de27-142">CaffeOnSpark에 대한 설명서에 나와 있는 것보다 더 많은 것을 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="6de27-143">변경 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-143">The changes are:</span></span>
- <span data-ttu-id="6de27-144">CPU 전용으로 변경하고 특정 목록으로 libatlas를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="6de27-145">나중에 사용할 수 있도록 데이터 집합을 모든 작업자 노드에 액세스할 수 있는 공유 위치인 Blob Storage에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="6de27-146">컴파일된 Caffe 라이브러리를 Blob Storage에 배치하고 나중에 스크립트 동작을 사용하여 해당 라이브러리를 모든 노드에 복사하여 추가 컴파일 시간이 발생하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="6de27-147">문제 해결: Ant BuildException 발생: exec 반환됨: 2</span><span class="sxs-lookup"><span data-stu-id="6de27-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="6de27-148">CaffeOnSpark 빌드를 처음으로 시도할 때 이 메시지가 발생하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="6de27-149">"make clean"으로 코드 리포지토리를 단순히 정리한 후 "make build"를 실행하면 이 문제가 해결됩니다(단, 올바른 종속성이 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="6de27-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="6de27-150">문제 해결: Maven 리포지토리 연결 시간 초과</span><span class="sxs-lookup"><span data-stu-id="6de27-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="6de27-151">maven에서 다음과 유사한 연결 시간 초과 오류가 발생하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="6de27-152">몇 분 동안 대기한 후 코드를 다시 빌드하면 Maven에서 지정된 IP 주소로부터 트래픽을 어떤 식으로든 제한할 수 있으므로 문제가 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="6de27-153">문제 해결: Caffe 테스트 실패</span><span class="sxs-lookup"><span data-stu-id="6de27-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="6de27-154">CaffeOnSpark에 대한 최종 확인을 수행할 때 아래와 유사한 테스트 실패가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="6de27-155">UTF-8 인코딩과 관련될 수 있지만 Caffe 사용에는 영향을 주지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="6de27-156">3단계: 모든 작업자 노드에 필요한 라이브러리 배포</span><span class="sxs-lookup"><span data-stu-id="6de27-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="6de27-157">다음 단계는 모든 노드에 라이브러리(기본적으로 CaffeOnSpark/caffe-public/distribute/lib/ 및 CaffeOnSpark/caffe-distri/distribute/lib/의 라이브러리)를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="6de27-158">2단계에서는 라이브러리를 Blob Storage에 배치했으며 이 단계에서는 스크립트 동작을 사용하여 라이브러리를 모든 헤드 노드 및 작업자 노드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="6de27-159">이렇게 하려면 아래와 같이 스크립트 동작을 실행하면 됩니다(클러스터에 대한 적절한 위치를 가리켜야 함).</span><span class="sxs-lookup"><span data-stu-id="6de27-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="6de27-160">2단계에서 모든 노드에 액세스할 수 있는 Blob Storage에 배치했으므로 이 단계에서는 모든 노드에 복사하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="6de27-161">4단계: Caffe 모델 구성 및 분산 실행</span><span class="sxs-lookup"><span data-stu-id="6de27-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="6de27-162">위의 단계를 실행했으면 Caffe가 헤드노드에 이미 설치되어 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="6de27-163">다음 단계는 Caffe 모델을 작성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="6de27-164">Caffe는 "표현 아키텍처"를 사용 중이며 여기서는 모델을 구성하기 위해 대부분의 경우 코딩 없이 구성 파일을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="6de27-165">따라서 이에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-165">So let's take a look there.</span></span> 

<span data-ttu-id="6de27-166">오늘날 학습할 모델은 MNIST 학습을 위한 샘플 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="6de27-167">필기 숫자의 MNIST 데이터베이스에는 학습 집합 예제 60,000개와 테스트 집합 예제 10,000개가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="6de27-168">NIST에서 제공되는 큰 집합의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="6de27-169">이 숫자는 크기를 표준화하였고 고정 크기 이미지로 중앙에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="6de27-170">CaffeOnSpark에는 데이터 집합을 다운로드하고 적절한 형식으로 변환할 수 있는 몇 가지 스크립트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="6de27-171">CaffeOnSpark는 MNIST 학습을 위한 몇 가지 네트워크 토폴로지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="6de27-172">네트워크 아키텍처(네트워크의 토폴로지)를 분할하고 최적화하기 위한 훌륭한 설계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="6de27-173">이 경우 다음 두 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="6de27-174">"Solver" 파일(${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt)은 최적화를 감독하고 매개 변수 업데이트를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="6de27-175">예를 들어 CPU 또는 GPU를 사용할지 여부, 모멘텀, 반복 횟수 등을 정의합니다. 또한 프로그램에서 사용하는 신경망 토폴로지도 정의합니다(필요한 두 번째 파일).</span><span class="sxs-lookup"><span data-stu-id="6de27-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="6de27-176">Solver에 대한 자세한 내용은 [Caffe 설명서](http://caffe.berkeleyvision.org/tutorial/solver.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6de27-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="6de27-177">이 예제의 경우 GPU보다는 CPU를 사용하므로 마지막 줄을 다음으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe 구성](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="6de27-179">필요에 따라 다른 줄을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-179">You can change other lines as needed.</span></span>

<span data-ttu-id="6de27-180">두 번째 파일(${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt)은 신경망의 모습과 관련 입력 및 출력 파일을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="6de27-181">또한 학습 데이터 위치를 반영하도록 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="6de27-182">lenet_memory_train_test.prototxt에서 다음 부분을 변경합니다(클러스터에 대한 적절한 위치를 가리켜야 함).</span><span class="sxs-lookup"><span data-stu-id="6de27-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="6de27-183">"file:/Users/mridul/bigml/demodl/mnist_train_lmdb"를 "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="6de27-184">"file:/Users/mridul/bigml/demodl/mnist_test_lmdb/"를 "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe 구성](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="6de27-186">네트워크를 정의하는 방법에 대한 자세한 내용은 [MNIST 데이터 집합에 대한 Caffe 설명서](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6de27-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="6de27-187">이 블로그의 용도에 맞게 간단한 MNIST 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="6de27-188">헤드 노드에서 아래 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="6de27-189">기본적으로 이 명령은 필요한 파일(lenet_memory_solver.prototxt 및 lenet_memory_train_test.prototxt)을 각 YARN 컨테이너에 배포하며 각 Spark 드라이버/실행기의 관련 경로를 이전 코드 조각에서 CaffeOnSpark 라이브러리가 포함된 위치를 가리키도록 정의된 LD_LIBRARY_PATH로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="6de27-190">모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6de27-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="6de27-191">YARN 클러스터 모드를 사용 중이고 이 경우 임의 컨테이너(및 임의 작업자 노드)에 대해 Spark 드라이버가 예약되므로 콘솔에 다음과 같은 항목만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="6de27-192">어떤 작업이 발생했는지 알고 싶은 경우에는 일반적으로 자세한 정보가 포함된 Spark 드라이버 로그를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="6de27-193">이 경우 YARN UI로 이동하여 관련 YARN 로그를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="6de27-194">다음 URL로 YARN UI를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN UI](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="6de27-196">이 특정 응용 프로그램에 대해 얼마나 많은 리소스가 할당되는지를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="6de27-197">"Scheduler" 링크를 클릭하면 이 응용 프로그램에 대해 9개의 컨테이너가 실행 중인 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="6de27-198">YARN에 8개의 실행기를 제공하도록 요청하고 다른 컨테이너는 드라이버 프로세스용입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![YARN Scheduler](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="6de27-200">오류가 있는 경우 드라이버 로그 또는 컨테이너 로그를 확인하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="6de27-201">드라이버 로그의 경우 YARN UI에서 응용 프로그램 ID를 클릭한 후 [로그] 단추를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="6de27-202">드라이버 로그는 stderr에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-202">The driver logs are written into stderr.</span></span>

![YARN UI 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="6de27-204">예를 들어 드라이버 로그에서 아래와 같이 너무 많은 실행기를 할당했음을 나타내는 몇 가지 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

<span data-ttu-id="6de27-205">경우에 따라 드라이버보다는 실행기에서 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="6de27-206">이 경우 컨테이너 로그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="6de27-207">항상 컨테이너 로그를 가져온 후 실패한 컨테이너를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="6de27-208">예를 들어 Caffe를 실행할 때 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-208">For example, you might meet this failure when running Caffe.</span></span>

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

<span data-ttu-id="6de27-209">이 경우 실패한 컨테이너 ID(위의 경우 container_1485916338528_0008_05_000005)를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="6de27-210">그런 다음 헤드 노드에서 다음을</span><span class="sxs-lookup"><span data-stu-id="6de27-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="6de27-211">실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-211">from the headnode.</span></span> <span data-ttu-id="6de27-212">컨테이너 오류를 확인하면 lenet_memory_solver.prototxt에서 GPU 모드를 사용했기 때문입니다(여기서는 대신 CPU 모드를 사용해야 함).</span><span class="sxs-lookup"><span data-stu-id="6de27-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="6de27-213">결과 가져오기</span><span class="sxs-lookup"><span data-stu-id="6de27-213">Getting results</span></span>

<span data-ttu-id="6de27-214">8개의 실행기를 할당하고 네트워크 토폴로지가 간단하므로 결과를 실행하는 데 약 30분만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="6de27-215">명령줄에서 wasb:///mnist.model에 모델을 배치하고 wasb:///mnist_features_result라는 폴더에 결과를 배치한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="6de27-216">다음을 실행하여 결과를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="6de27-217">결과는 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="6de27-218">SampleID는 MNIST 데이터 집합에서 ID를 나타내며 레이블은 모델에서 식별하는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="6de27-219">결론</span><span class="sxs-lookup"><span data-stu-id="6de27-219">Conclusion</span></span>

<span data-ttu-id="6de27-220">이 설명서에서는 간단한 예를 실행하여 CaffeOnSpark를 설치하려고 시도했습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="6de27-221">HDInsight는 완전히 관리되는 클라우드 분산된 계산 플랫폼으로, 분산 심층 학습을 위해 대규모 데이터 집합에 대해 Machine Learning 및 고급 분석 워크로드를 실행하기 위한 최적의 장소이며 HDInsight Spark에서 Caffe를 사용하여 심층 학습 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6de27-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="6de27-222"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="6de27-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="6de27-223">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="6de27-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6de27-224">시나리오</span><span class="sxs-lookup"><span data-stu-id="6de27-224">Scenarios</span></span>
* [<span data-ttu-id="6de27-225">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="6de27-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6de27-226">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="6de27-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="6de27-227">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="6de27-227">Manage resources</span></span>
* [<span data-ttu-id="6de27-228">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="6de27-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

