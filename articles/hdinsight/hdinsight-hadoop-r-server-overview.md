---
title: "Azure HDInsight의 서버 aaaIntroduction tooR | Microsoft Docs"
description: "자세한 내용은 방법 빅 데이터 분석을 위해 HDInsight toocreate 응용 프로그램에 R Server toouse 합니다."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>소개 tooR 서버 및 HDInsight의 오픈 소스 R 기능

Microsoft R Server를 사용하면 Azure에서 HDInsight 클러스터를 만들 때 배포 옵션으로 사용할 수 있습니다. 이 새 기능에는 데이터 과학자, 통계학자, 및 HDInsight의 분석의 분산된 메서드 요청 시 액세스 tooscalable 있는 R 프로그래머 제공합니다.

클러스터 수 toohello 프로젝트와 작업에 적절 하 게 크기가 정 해지고 다음 삭제 하는 더 이상 필요 합니다. Azure HDInsight에 속하지 않기를 있으므로 이러한 클러스터 SLA 99.9% 가동률의 엔터프라이즈 수준의 연중 무휴 지원 함께 제공 되 고 hello Azure 에코 시스템에서에서 다른 구성 요소와 기능 toointegrate hello.

HDInsight에 R Server 거의 모든 크기 로드 tooeither Azure Blob 또는 데이터 레이크 저장소의 데이터 집합에 R 기반 분석에 대 한 hello 최신 기능을 제공합니다. R Server는 오픈 소스 R 기술을 기반으로 한 이후 hello에 R 기반 응용 프로그램을 빌드하면 hello 8000 + 오픈 소스 R 패키지를 활용할 수 있습니다. hello 루틴 ScaleR, R Server에 포함 된 Microsoft의 빅 데이터 분석 패키지에서에서 사용할 수 있습니다.

클러스터의 hello 가장자리 노드 R 스크립트 편리한 위치 tooconnect toohello 클러스터 및 toorun 제공합니다. 가장자리 노드 ScaleR의 hello distributed 옵션을 실행 중인 hello 평행 화 함수 hello에 지 노드 서버의 hello 코어 수 있습니다. 실행할 수도 있습니다 이러한 hello 클러스터의 hello 노드에서 ScaleR의 Hadoop 맵 감소 또는 Spark를 사용 하 여 계산 컨텍스트.

hello 모델 또는 예측에 대 한 분석 결과 다운로드할 수 있는 온-프레미스를 사용 합니다. 또한 특히 [Azure Machine Learning Studio](http://studio.azureml.net) [웹 서비스](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md)를 통해 Azure의 다른 곳에서 작동할 수 있습니다.

## <a name="get-started-with-r-on-hdinsight"></a>HDInsight에서 R 시작
R Server는 HDInsight 클러스터에서 tooinclude, hello Azure 포털을 사용 하 여 HDInsight 클러스터를 만들 때 hello R 서버 클러스터 종류를 선택 해야 합니다. R 서버 클러스터 유형 hello hello 클러스터의 hello 데이터 노드 및 가장자리 노드에 R 서버 기반 분석에 대 한 시작 영역으로 사용 되는 R Server 포함 됩니다. 참조 [HDInsight에 R Server 시작](hdinsight-hadoop-r-server-get-started.md) toocreate 클러스터 hello 하는 방법을 보여주는 연습은 합니다.

## <a name="learn-about-data-storage-options"></a>데이터 저장소 옵션에 대해 자세히 알아보기
HDInsight 클러스터의 hello HDFS 파일 시스템에 대 한 기본 저장소는 Azure 저장소 계정 또는 Azure 데이터 레이크 스토어와 연결할 수 있습니다. 이 연결 하면 모든 데이터는 업로드 toohello 클러스터 저장소 분석 하는 동안을 영구적으로 설정 됩니다. Hello 데이터 전송 toohello 저장소 옵션 hello 저장소 계정 및 hello의 hello 포털 기반 업로드 기능을 포함 하 여 선택 하는 처리 하기 위한 다양 한 도구는 [AzCopy](../storage/common/storage-use-azcopy.md) 유틸리티입니다.

Hello 클러스터 프로 비전 프로세스에서 사용 하 여 hello 주 저장소 옵션에 관계 없이 하는 동안 액세스 tooadditional Blob 및 데이터 레이크 저장소를 추가 하는 hello 선택할을 수 있습니다. 참조 [HDInsight에 R Server 시작](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) 액세스 tooadditional 계정 추가에 대 한 내용은 합니다. Hello 보충 참조 [HDInsight에 R Server에 대 한 Azure 저장소 옵션](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) 여러 저장소 계정을 사용 하는 방법에 대 한 자세한 문서 toolearn 합니다.

사용할 수도 있습니다 [Azure Files](../storage/files/storage-how-to-use-files-linux.md) hello 가장자리 노드에서 사용 하기 위해 저장소 옵션으로 합니다. Azure 파일 toomount Azure 저장소 toohello Linux 파일 시스템에서에서 만든 파일 공유를 수 있습니다. HDInsight 클러스터의 R Server에 대한 데이터 저장소 옵션에 대한 자세한 내용은 [HDInsight 클러스터의 R Server에 대한 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)을 참조하세요.

## <a name="access-r-server-on-hello-cluster"></a>R 서버 hello 클러스터에 액세스
서버를 제공 하는 브라우저를 사용 하 여 hello 가장자리 노드에 tooinclude RStudio 서버 hello를 프로 비전 프로세스 중 선택한 tooR 연결할 수 있습니다. Hello 클러스터를 프로 비전 할 때에 다음이 설치 하지 않은, 나중에 추가할 수 있습니다. 클러스터를 만든 후에 RStudio Server를 설치하는 방법에 대한 자세한 내용은 [HDInsight 클러스터에 RStudio Server 설치](hdinsight-hadoop-r-server-install-r-studio.md)를 참조하세요. SSH/PuTTY tooaccess hello R 콘솔을 사용 하 여 toohello R 서버를 연결할 수도 있습니다. 

## <a name="develop-and-run-r-scripts"></a>R 스크립트 개발 및 실행
hello R 스크립트를 만들어 실행 hello 8000 + 더하기 toohello에서 오픈 소스 R 패키지 평행 화 및 hello ScaleR 라이브러리에서 사용할 수 있는 루틴 배포를 사용할 수 있습니다. 일반적으로 hello 가장자리 노드에서 R server 실행할 스크립트를 해당 노드의 hello R 인터프리터 내에서 실행 됩니다. hello 예외 toocall ScaleR 함수 tooHadoop 맵 감소 (RxHadoopMR) 또는 Spark (RxSpark)를 설정 하는 계산 컨텍스트를 사용 해야 하는 단계입니다. 이 경우 hello 함수 hello 클러스터의 참조 하는 hello 데이터에 연결 된 해당 데이터 (작업) 노드에 걸쳐 분산 방식에서 실행 합니다. Hello 다른 계산 컨텍스트 옵션에 대 한 자세한 내용은 참조 [HDInsight에 R Server에 대 한 상황에 맞는 옵션 계산](hdinsight-hadoop-r-server-compute-contexts.md)합니다.

## <a name="operationalize-a-model"></a>모델 운영
데이터 모델링 완료 되 면 Azure와 온-프레미스에서 새 데이터에 대 한 hello 모델 toomake 예측 실제로 운영할 수 있습니다. 이 프로세스를 점수 매기기라고 합니다. 점수 매기기는 HDInsight, Azure Machine Learning 또는 온-프레미스에서 수행할 수 있습니다.

### <a name="score-in-hdinsight"></a>HDInsight에서 점수 매기기
HDInsight의 tooscore 프로그램 모델 toomake 예측이 새 데이터 파일에 대 한 저장소 계정 tooyour를 로드 한를 호출 하는 R 함수를 작성 합니다. 그런 다음 hello 예측 백 toohello 저장소 계정을 저장 합니다. 클러스터 또는 예약된 된 작업을 사용 하 여 hello 가장자리 노드에 hello 일상적인 주문형으로 실행할 수 있습니다.  

### <a name="score-in-azure-machine-learning-aml"></a>AML(Azure Machine Learning)에서 점수 매기기
AML 웹 서비스를 사용 하 여 hello를 사용 하 여 tooscore 라고 소스 Azure 컴퓨터 학습 R 패키지를 열어 [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish Azure 웹 서비스로 모델입니다. 편의 위해이 패키지는 hello 가장자리 노드 미리 설치 되어 있습니다. 다음을 hello 웹 서비스에 대 한 hello 기계 학습 toocreate 사용자 인터페이스 기능을 사용 하 고 점수를 매기기 위해 필요에 따라 다음 hello 웹 서비스를 호출 합니다.

이 옵션을 선택 하는 경우 tooconvert ScaleR 모델 개체 tooequivalent 오픈 소스 모델 개체에 대 한 hello 웹 서비스와 함께 사용 해야 합니다. 이 변환은 앙상블 기반 모델에 대해 ScaleR 강제 변환 함수(예: `as.randomForest()` )를 통해 수행할 수 있습니다.

### <a name="score-on-premises"></a>온-프레미스 점수 매기기
tooscore 온-프레미스 모델을 만든 후, R, 다운로드, 취소 serialize 한 다음 새 데이터의 점수를 매기기 위해 사용 하 여 hello 모델 serialize 할 수 있습니다. 이미 설명한 hello 접근 방식을 사용 하 여 새 데이터의 점수 [HDInsight의 점수 매기기](#scoring-in-hdinsight) 또는 사용 하 여 [DeployR](https://deployr.revolutionanalytics.com/)합니다.

## <a name="maintain-hello-cluster"></a>Hello 클러스터 유지 관리
### <a name="install-and-maintain-r-packages"></a>R 패키지 설치 및 유지 관리
대부분의 사용자를 사용 하는 hello R 패키지 hello 가장자리 노드 그곳에서 실행 하 여 R 스크립트의 대부분 단계 이후 필요 합니다. tooinstall 추가 R 패키지 hello 가장자리 노드 일반적인 hello를 사용할 수 있습니다 `install.packages()` R에서 메서드

바로 사용할 경우 루틴 hello ScaleR 라이브러리에서 hello 클러스터를 일반적으로 불필요 tooinstall hello 데이터 노드 추가 R 패키지 합니다. 그러나 추가 패키지 toosupport hello 사용 할 수 있습니다 **rxExec** 또는 **RxDataStep** hello 데이터 노드는 실행 합니다.

이러한 경우 hello 클러스터를 만든 후 hello 추가 패키지를 스크립트 동작을 설치할 수 있습니다. 자세한 내용은 [R 서버를 사용하여 HDInsight 클러스터 만들기](hdinsight-hadoop-r-server-get-started.md)를 참조하세요.   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Hadoop Map Reduce 메모리 설정 변경
클러스터 맵 축소 작업 실행 되는 경우 서버 tooR를 사용할 수 있는 메모리의 수정 된 toochange hello 양이 될 수 있습니다. toomodify 클러스터에서 클러스터에 대해 Azure 포털 블레이드 hello를 통해 사용할 수 있는 Apache Ambari UI hello를 사용 합니다. 클러스터에 대해 tooaccess Ambari UI hello 하는 방법에 대 한 지침은 [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.

너무 hello 호출에서 Hadoop 스위치를 사용 하 여 서버 tooR를 사용할 수 있는 메모리의 가능한 toochange hello 양을 이기도**RxHadoopMR** 다음과 같습니다.

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>클러스터 규모 조정
기존 클러스터 hello 포털을 통해 위로 또는 아래로 확장할 수 있습니다. 를 확장 하 여 hello에 더 큰 처리 작업에 필요할 수 있는 추가 용량을 얻을 수 있습니다 또는 축소할 수도 있습니다는 클러스터 유휴 상태일 때. 방법에 대 한 지침은 tooscale 클러스터 참조 [관리할 HDInsight 클러스터](hdinsight-administer-use-portal-linux.md)합니다.

### <a name="maintain-hello-system"></a>Hello 시스템 유지 관리
유지 관리 tooapply OS 패치 및 기타 업데이트는 hello 근무 하는 HDInsight 클러스터에 Linux Vm 내부에서 수행 됩니다. 일반적으로 모든 월요일과 목요일 오전 3시 30분 (현지 시간 hello VM hello에 기반)에 유지 관리 수행 됩니다. 한 번에 둘 이상의 분기 hello 클러스터의 영향을 미치지 하는 방식으로 수행 됩니다.  

Hello 헤드 노드를 중복 하 고 영향을 받는 모든 데이터 노드를이 시간 동안 실행 중인 모든 작업이 느려질 수 있습니다. 그러나 toocompletion, 실행 계속 되도록 합니다. 모든 사용자 지정 소프트웨어 또는 로컬 데이터는 클러스터를 다시 빌드해야 하는 심각한 오류가 발생하지 않는 한 이러한 유지 관리에서 보존됩니다.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>HDInsight 클러스터의 R 서버에 대한 IDE 옵션에 대해 자세히 알아보기
HDInsight 클러스터의 hello Linux 가장자리 노드는 hello R 기반 분석에 대 한 영역을 방문 합니다. Hello 커뮤니티 버전의 설치에 대 한 기본 옵션을 제공 하는 최신 버전의 HDInsight [RStudio 서버](https://www.rstudio.com/products/rstudio-server/) 브라우저 기반 IDE와 hello 가장자리 노드에 있습니다. RStudio 서버 hello 개발을 위한 IDE 활용 및 R 스크립트의 실행 hello R 콘솔을 사용할 때 보다 훨씬 생산성 수 있습니다. 만드는 클러스터 hello 하면서 tooadd 때 하지 tooadd RStudio 서버를 선택한 경우 것 이라면 다음 참조 [HDInsight 클러스터에 R Studio Server 설치](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

또 다른 전체 IDE 옵션 tooinstall 데스크톱 IDE 이며 원격 맵 감소 또는 Spark 계산 컨텍스트를 사용 하 여 tooaccess hello 클러스터를 사용 합니다. Microsoft의 RTVS([Visual Studio용 R 도구](https://www.visualstudio.com/features/rtvs-vs.aspx)), RStudio 및 Walware의 Eclipse 기반 [StatET](http://www.walware.de/goto/statet) 등의 옵션도 있습니다.

마지막으로 입력 하 여 hello 가장자리 노드에서 hello R 서버 콘솔에 액세스할 수 있습니다 **R** PuTY 또는 SSH를 통해 연결 하는 hello Linux 명령 프롬프트입니다. Hello 콘솔 인터페이스를 사용할 때 편리 하 게 toorun 다른 창에서 R 스크립트 개발에 대 한 텍스트 편집기 및 잘라내기 이며 필요에 따라 스크립트의 섹션 hello R 콘솔에 붙여 넣을 합니다.

## <a name="learn-about-pricing"></a>가격 책정에 대해 알아보기
hello HDInsight 클러스터 R 서버와 연관 된 요금 구조가 유사 toohello 요금 hello 표준 HDInsight 클러스터에 대 한 합니다. Hello 크기 조정의 hello hello 이름, 데이터 및 코어 시간 uplift hello 추가 가장자리 노드 간에 Vm 내부에 기반 합니다. HDInsight 가격 및 30 일 무료 평가판의 가용성을 hello에 대 한 자세한 내용은 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.

## <a name="next-steps"></a>다음 단계
toolearn toouse HDInsight와 R 서버 클러스터에 대 한 자세한 hello 다음 항목을 참조 하세요.

* [HDInsight에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)
* [RStudio 서버 tooHDInsight 추가 (클러스터를 만드는 동안 설치 되지 않은) 하는 경우](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight의 R 서버에 대한 Compute 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight에서 R Server의 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)
