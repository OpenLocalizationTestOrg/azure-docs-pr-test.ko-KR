---
title: "분산된 심층 학습에 대 한 Azure HDInsight Spark에 Caffe aaaUse | Microsoft Docs"
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
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용


## <a name="introduction"></a>소개

심층 학습 의료 tootransportation toomanufacturing에 이르기까지 등에 영향을 합니다. 회사와 같은 toosolve 어려운 문제 학습 toodeep 켜거나 [이미지 분류](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [음성 인식](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), 인식, 개체 및 기계 번역입니다. 

[Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano 등 [널리 사용되는 수많은 프레임워크](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software)가 있습니다. Caffe는 hello 중 가장 유명한 아닌 기호 (명령적) 신경망 프레임 워크 이며 컴퓨터 비전을 포함 하 여 다양 한 측면에서 널리 사용 되는. 또한 [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep)는 Caffe와 Apache Spark를 결합한 것으로 기존의 Hadoop 클러스터에서 Spark ETL 파이프라인과 함께 심층 학습을 쉽게 사용할 수 있어서 시스템 복잡성 및 종단 간 학습에 대한 대기 시간을 줄일 수 있습니다.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) hello은 사용할 수 있는 제공 하는 완전히 관리 되는 클라우드 Hadoop 제공 스파크, Hive, MapReduce, HBase, 스톰, Kafka, 및 SLA는 99.9% 뒷받침 되며 R 서버에 대해 오픈 소스 분석 클러스터를 최적화 합니다. 이러한 각 빅 데이터 기술과 ISV 응용 프로그램은 엔터프라이즈급 보안과 모니터링으로 관리 클러스터 형태로 쉽게 배포 가능합니다.

일부 사용자는 요청 하는 방법에 대 한 toouse 심층 HDInsight에 Microsoft의 PaaS Hadoop 제품에 배웁니다. 에서는 더 많은 tooshare hello 미래에 하지만 toosummarize 방법에 대 한 기술 블로그 원하는 오늘 toouse Caffe HDInsight Spark에 있습니다.

이전에 Caffe를 설치했다면 이 프레임워크를 설치하는 것이 약간 어렵다는 것을 알 수 있습니다. 이 블로그에서 먼저 설명할 방법을 tooinstall [Spark에 Caffe](https://github.com/yahoo/CaffeOnSpark) 는 HDInsight 클러스터에 대 한 다음 사용 하 여 기본 제공 MNIST 데모 toodemostrate hello 어떻게 toouse Cpu에서 HDInsight Spark를 사용 하 여 분산 심층 학습 합니다.

HDInsight에서 작동 하는 4 개의 주요 단계 tooget 가지가 있습니다.

1. 모든 hello 노드에서 hello 필요한 종속성을 설치 합니다.
2. Hello 헤드 노드에 Caffe HDInsight 용 Spark에 구축
3. 필요한 hello 라이브러리 tooall hello 작업자 노드를 배포 합니다.
4. Caffe 모델 구성 및 분산 실행

HDInsight PaaS 솔루션 이므로, 기능을 제공 뛰어난 플랫폼-매우 쉽게 tooperform 이므로 몇 가지 작업입니다. 이 블로그 게시물에서 많이 사용 하는 hello 기능 중 하나가 호출 될 [스크립트 동작](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), 실행할 수 있습니다와 셸 명령이 toocustomize 클러스터 노드 (헤드 노드, 작업자 노드 또는 가장자리 노드).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>1 단계: 모든 hello 노드에서 필요한 hello 종속성 설치

시작 tooget, 필요한 tooinstall hello 종속성이 필요 합니다. hello Caffe 사이트 및 [CaffeOnSpark 사이트](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) YARN 모드 (HDInsight Spark에 대 한 hello 모드)에 Spark에 대 한 hello 종속성을 설치 하기 위한 매우 유용한 몇 가지 wiki 제공 있지만 이러한 tooadd 몇 가지 종속성 HDInsight 플랫폼에 대 한 합니다. 아래와 같이 hello 스크립트 작업을 사용 하 고 모든 hello 헤드 노드 및 노드 작업자에서 실행 합니다. 해당 종속성은 다른 패키지에도 종속되므로 이 스크립트 작업은 약 20분이 소요됩니다. HDInsight 클러스터는 GitHub 위치나 hello 기본 BLOB 저장소 계정 등 tooyour를 액세스할 수 있는 일부 위치에 두어야 합니다.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

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


위의 hello 스크립트 동작에서 두 개의 단계가 있습니다. hello 첫 번째 단계는 tooinstall 모든 hello 필수 라이브러리입니다. 이러한 라이브러리는 모두 Caffe (예: gflags glog) 컴파일하고 실행 하기 위한 Caffe (예: numpy) hello 필요한 라이브러리를 포함 됩니다. Libatlas 사용 하 여 CPU 최적화 하지만 항상 MKL 또는 CUDA (예: GPU) 등의 다른 최적화 라이브러리를 설치 하는 방법에 대 한 hello CaffeOnSpark wiki를 수행 합니다.

hello 두 번째 단계는 toodownload, 컴파일 및 런타임 중 Caffe에 대 한 2.5.0 protobuf를 설치 합니다. Protobuf 2.5.0 [필요](https://github.com/yahoo/CaffeOnSpark/issues/87)toocompile 하므로이 버전은 Ubuntu 16에 패키지로 사용할 수 없습니다, hello 소스 코드에서. 또한 몇 가지에 리소스가 방법은 인터넷 hello toocompile,와 같은 [이](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply 시작, 실행 하기만 하면이 스크립트 동작이 프로그램 클러스터 tooall hello 작업자에 대 한 노드 및 헤드 노드 (예: HDInsight 3.5). 실행 중인 클러스터에 대 한 hello 스크립트 작업을 실행 하거나 또는 hello 클러스터 프로 비전 시 hello 스크립트 동작을 실행할 수도 있습니다. Hello 스크립트 동작에 대 한 자세한 내용은 hello 설명서를 참조 하십시오 [여기](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![스크립트 동작 tooInstall 종속성](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>2 단계: hello 헤드 노드에서 Caffe HDInsight 용 Spark에 빌드

hello 두 번째 단계는 hello 헤드 노드에 Caffe toobuild 하 고 hello 컴파일된 라이브러리 tooall hello 작업자 노드를 배포 합니다. 이 단계에서는 해야 너무[ssh 여 헤드 노드에](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), 따르십시오 hello [CaffeOnSpark 빌드 프로세스](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), 몇 가지 추가 단계 toobuild CaffeOnSpark를 사용할 수 있는 hello 스크립트는 합니다. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Toodo 할 수 있습니다 CaffeOnSpark의 어떤 hello 설명서에 따르면 보다 더 합니다. hello 변경이합니다.
- TooCPU만 변경 하 고이 특정 목적에 대 한 libatlas를 사용 합니다.
- 액세스할 수 있는 tooall 작업자 노드 나중에 사용할 수 있는 공유 위치가 있는 hello 데이터 집합 toohello BLOB 저장소를 넣습니다.
- Put hello Caffe 라이브러리 tooBLOB 저장소 컴파일되고 나중에 스크립트 동작 tooavoid 추가 컴파일 시간을 사용 하 여 해당 라이브러리 tooall hello 노드를 복사 합니다.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>문제 해결: Ant BuildException 발생: exec 반환됨: 2

Toobuild CaffeOnSpark를 처음 시도할 때 경우에 따라 것은 말

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

"새로 만들기"에서 간단히 정리 hello 코드 리포지토리 및 실행된 "확인 빌드" hello 올바른 종속성으로이 문제를 해결 합니다.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>문제 해결: Maven 리포지토리 연결 시간 초과

경우에 따라 maven에서 제공 hello 연결 시간 초과 오류, 유사한 toobelow:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

몇 분 정도 기다린 후 확인 되 고 toorebuild hello 코드 하면 메뉴, Maven 수도 있으므로 어떻게 하 든 제한 hello 지정된 된 IP 주소의 트래픽만 합니다.


### <a name="troubleshooting-test-failure-for-caffe"></a>문제 해결: Caffe 테스트 실패

아마도 CaffeOnSpark, 아래와 유사한에 대 한 hello 최종 확인을 수행 하는 경우 테스트 실패를 표시 됩니다. 이 u t F-8 인코딩으로 관련 prabably 아니지만 Caffe hello 사용 하는 데 영향을 주지 않아야

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>3 단계: 필요한 hello 라이브러리 tooall hello 작업자 노드를 배포 합니다.

hello 다음 단계는 toodistribute hello 라이브러리 (기본적으로 CaffeOnSpark/caffe-공용/배포/lib에서 라이브러리를 hello/및 CaffeOnSpark/caffe-패키지가/배포/lib /) tooall hello 노드. 2 단계에서에서 BLOB 저장소에 이러한 라이브러리 포함 하 고이 단계에서는 스크립트 작업 toocopy 사용 합니다 것 tooall hello 헤드 노드와 작업자 노드.

toodo 아래와 같이 스크립트 동작 실행이, 단순 (toopoint toohello 오른쪽 위치 특정 tooyour 클러스터 필요):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

2 단계에서 우리에 넣습니다. BLOB 저장소에 액세스할 수 있는 tooall hello 노드 용량 hello, 때문에이 단계에서는 하는 것 복사할 tooall hello 노드.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>4단계: Caffe 모델 구성 및 분산 실행

Hello 단계를 실행 한 후 Caffe 매핑하려고 hello 헤드 노드에 설치 되며 좋은 toogo 하는 합니다. hello 다음 단계는 toowrite Caffe 모델입니다. 

Caffe 아키텍처를 사용 하는 "표현", 정당한 하면 모델을 작성 하기 위한 toodefine 구성 파일을 필요 하 고 전혀 (대부분의 경우) 코드 하지 않고 있습니다. 따라서 이에 대해 살펴보겠습니다. 

오늘 교육 할지 म hello 모델은 MNIST 학습에는 샘플 모델. 필기 자릿수 hello MNIST 데이터베이스의 60, 000 예제 학습 집합과 테스트 집합의 10, 000 예제에 있습니다. NIST에서 제공되는 큰 집합의 하위 집합입니다. 크기 정규화 되 고 고정 크기 이미지의 가운데에 맞출지 hello 자릿수 되었을 수 있습니다. CaffeOnSpark 일부 스크립트 toodownload hello dataset 않았으며 hello 올바른 형식으로 변환 됩니다.

CaffeOnSpark는 MNIST 학습을 위한 몇 가지 네트워크 토폴로지를 제공합니다. Hello 네트워크 아키텍처 (hello 네트워크의 hello 토폴로지) 및 최적화 분할의 훌륭한 디자인을가지고 있습니다. 이 경우 다음 두 파일이 필요합니다. 

hello "찾기" 파일 (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) hello 최적화 커지고 매개 변수 업데이트를 생성 하는 데 사용 됩니다. CPU 또는 GPU 사용할지, hello 가속도, 반복 횟수 됩니다, 란 정의 예를 들어, 등입니다. 또한 어떤 뉴런 네트워크 토폴로지 (즉, 필요한 hello 두 번째 파일) 프로그램에서 사용 hello 해야 정의 합니다. 찾기에 대 한 자세한 내용은 참조 하십시오 너무[Caffe 설명서](http://caffe.berkeleyvision.org/tutorial/solver.html)합니다.

예를 들어, GPU를 사용 하지 않고 CPU 사용 하 고 있으므로 변경 해야 hello 마지막 줄:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe 구성](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

필요에 따라 다른 줄을 변경할 수 있습니다.

hello 두 번째 파일 (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) hello 뉴런 네트워크를 표시 하는 방법 및 hello 관련 입력 및 출력 파일을 정의 합니다. 또한 tooupdate hello 파일 tooreflect hello 학습 데이터 위치를 해야합니다. Hello 부분 lenet_memory_train_test.prototxt (toopoint toohello 오른쪽 위치 특정 tooyour 클러스터 필요)에 따라 변경 합니다.

- 도 file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" 변경 "wasb: / / / 프로젝트/machine_learning/image_dataset/mnist_train_lmdb"
- 도 "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" 변경 "wasb: / / / 프로젝트/machine_learning/image_dataset/mnist_test_lmdb"

![Caffe 구성](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Toodefine 네트워크 hello 하는 방법에 대 한 자세한 내용은 hello를 확인 하십시오 [MNIST dataset에서 Caffe 설명서](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

이 블로그 hello 목적으로이 간단한 MNIST 예제만 사용 합니다. Hello 헤드 노드에서 아래 hello 명령을 실행 해야 합니다.

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

기본적으로 필요한 hello 배포 파일 (lenet_memory_solver.prototxt 및 lenet_memory_train_test.prototxt) tooeach YARN 컨테이너 및 설정 hello hello에 정의 된 각 스파크 드라이버/실행자 tooLD_LIBRARY_PATH의 관련 경로 이전 코드 조각 및 포인트 toohello 위치 CaffeOnSpark 라이브러리에 있는입니다. 

## <a name="monitoring-and-troubleshooting"></a>모니터링 및 문제 해결

YARN 클러스터 모드를 사용 하 고 있으므로 예약 된 tooan 임의의 컨테이너 (및 임의의 작업자 노드) hello Spark 드라이버가 됩니다는 쿼리에서 표시 되어야 같은 내용을 hello 콘솔 출력에서:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

원하는 tooknow 무슨 상황이 발생 하는 경우 일반적으로 tooget hello Spark 드라이버의 로그에는 자세한 정보가 필요 합니다. 이 경우 toogo toohello YARN UI toofind hello 관련 YARN 로그 해야 합니다. 이 URL에 의해 YARN UI hello를 얻을 수 있습니다. 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN UI](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

이 특정 응용 프로그램에 대해 얼마나 많은 리소스가 할당되는지를 살펴볼 수 있습니다. Hello "스케줄러" 링크를 클릭 하 고이 응용 프로그램에 대해 실행 되는 9 컨테이너는 표시 됩니다. YARN tooprovide 8 executor, 요청 하 고 다른 컨테이너로 드라이버 프로세스는 합니다. 

![YARN Scheduler](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

오류가 발생 하는 경우 toocheck hello 드라이버 로그 또는 컨테이너의 로그를 할 수 있습니다. 드라이버 로그에 대 한 YARN UI에 hello 응용 프로그램 ID 클릭 hello "Logs" 단추를 클릭 합니다. hello 드라이버 로그가 stderr에 기록 됩니다.

![YARN UI 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

예를 들어 표시 일부 hello 드라이버 로그에서 아래의 hello 오류가 너무 많은 executor 할당을 나타내는 있습니다.

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

경우에 따라 드라이버를 사용 하지 않고 단일 실행 hello 문제가 발생할 수 있습니다. 이 경우 toocheck hello 컨테이너 로그 해야 합니다. 항상 hello 컨테이너 로그를 얻을 수 있으며 다음 hello 실패 한 컨테이너를 가져올 수 없습니다. 예를 들어 Caffe를 실행할 때 이 오류가 발생할 수 있습니다.

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

이 경우 tooget 실패 hello 컨테이너 ID가 필요 하면 (대/소문자 위에 hello에 container_1485916338528_0008_05_000005). Toorun 필요 

    yarn logs -containerId container_1485916338528_0008_03_000005

hello 헤드 노드에 있습니다. 컨테이너 오류를 확인하면 lenet_memory_solver.prototxt에서 GPU 모드를 사용했기 때문입니다(여기서는 대신 CPU 모드를 사용해야 함).

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>결과 가져오기

8 executor를 할당 하 고 hello 네트워크 토폴로지는 간단를 작성할 수 약 30 분 toorun hello 결과입니다. Hello 명령줄에서 우리 hello 모델 toowasb:///mnist.model 배치 및 hello 결과 tooa 폴더 wasb 라는 배치 볼 수 있습니다: / / / mnist_features_result 합니다.

실행 하 여 hello 결과 얻을 수 있습니다.

    hadoop fs -cat hdfs:///mnist_features_result/*

및 hello 결과 다음과 같습니다.

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

hello SampleID hello MNIST 데이터 집합의 hello ID 나타내며 hello 레이블 모델 hello hello 번호 식별 합니다.


## <a name="conclusion"></a>결론

이 설명서에는 간단한 예제를 실행 하 여 tooinstall CaffeOnSpark 하려고 했습니다. HDInsight는 전체 관리 되는 클라우드 분산된 된 계산 플랫폼 고 hello 큰 데이터 집합에 기계 학습 및 고급 분석 워크 로드를 실행 하는 데 가장 적합 하 고 분산된 심층 학습에 대 한 Caffe HDInsight Spark tooperform 심층 학습에서 사용할 수 있습니다. 작업입니다.


## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)

