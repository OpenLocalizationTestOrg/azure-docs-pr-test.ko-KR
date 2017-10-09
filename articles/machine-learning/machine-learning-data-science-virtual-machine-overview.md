---
title: "aaaWhat은 데이터 과학 가상 컴퓨터 인지 확인 | Microsoft Docs"
description: "Tooget 주요 분석 시나리오가 데이터 과학 가상 컴퓨터와 함께 시작 하는 방법"
keywords: "데이터 과학 도구, 데이터 과학 가상 컴퓨터, 데이터 과학용 도구, linux 데이터 과학"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>소개 toohello Linux 및 Windows에 대 한 데이터 과학 가상 컴퓨터 클라우드 기반
hello 데이터 과학 가상 컴퓨터 (DSVM)는 Microsoft Azure 클라우드 데이터 과학을 수행 하에 맞게 만들어졌으며 사용자 지정된 된 VM 이미지입니다. 많은 일반적인 데이터 과학을 포함 하 고 다른 도구 미리 설치 되어 미리 구성 toojump 시작 고급 분석을 위해 지능형 응용 프로그램을 구축 합니다. DSVM은 Windows Server 및 Linux에서 사용할 수 있습니다. Windows Server 2016 및 2012에서 Windows 버전의 DSVM이 제공됩니다. Hello DSVM 16.04 Ubuntu LTS 및 OpenLogic 7.2 CentOS 기반 Linux 배포판의 Linux 버전을 제공합니다. 

이 항목에서는 데이터 과학 VM hello로 수행할 수 있는, VM hello를 사용 하는 hello 주요 시나리오 중 일부에 대해 간략하게 설명, Windows hello와 Linux 버전에서 사용할 수 있는 주요 기능 hello 항목별로 정리한 것 고 tooget 시작을 사용 하는 방법에 대해 설명 합니다.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>데이터 과학 가상 컴퓨터 hello로 어떻게 해야 합니까?
hello hello 데이터 과학 가상 컴퓨터의 목적은 간편 데이터 과학 환경 사용 하 여 모든 역할과 기술 수준에 tooprovide 데이터 전문가입니다. 이 VM은 유사한 환경을 직접 운영할 경우 들어가는 시간을 상당히 줄여 줍니다. 대신에 새로 작성된 VM 인스턴스에서 데이터 과학 프로젝트를 바로 시작할 수 있습니다. 

데이터 과학 VM hello는 디자인 하 고 사용 하는 광범위 한 사용 시나리오에 대해 구성 합니다. 프로젝트의 요구가 변함에 따라 환경을 확장하거나 축소할 수 있습니다. 있습니다 수 toouse 사용자 기본 설정된 언어 tooprogram 데이터 과학 작업 됩니다. 다른 도구를 설치할 수 있으며 hello 시스템 요구 사항에 대 한 사용자 지정할 수 있습니다.

## <a name="key-scenarios"></a>주요 시나리오
이 섹션에는 몇 가지 주요 시나리오는 hello에 대 한 데이터 과학 VM 배포 수 제안 합니다.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Hello 클라우드에서 분석 데스크톱 미리 구성
데이터 과학 VM hello tooreplace 관리 되는 클라우드 데스크톱을 사용 하 여 로컬 데스크톱을 찾고 데이터 과학 팀에 대 한 초기 구성을 제공 합니다. 이 기준선을 팀에서 모든 hello 데이터 과학자는 tooverify 실험을 사용 하 여 일관 된 설치 하 고 공동 작업을 유도 되도록 합니다. Hello sysadmin 부담을 줄여 한 비용을 낮추는 하 고 다양 한 소프트웨어 패키지 필요한 tooevaluate, 설치 및 유지 hello hello 시간에 저장 한 고급 분석 toodo를 필요 합니다.  

### <a name="data-science-training-and-education"></a>데이터 과학 학습 및 교육
엔터프라이즈 담당자 및 교육자에 일반적으로 데이터 과학 클래스를 설명 하는 가상 컴퓨터 이미지 tooensure 학생 들 한지 일관성 있는 설치 하 고 hello 샘플 예상 대로 작동 하는지를 제공 합니다. 데이터 과학 VM hello hello 지원 및 비 호환성 문제를 쉽게 처리할 수 있는 일관 된 설치 프로그램을 주문형으로 환경을 만듭니다. 이러한 환경 toobe 할 수 있는 경우 특히 더 짧은 교육 과정에 대 한 자주 작성, 대체로 활용 합니다.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>대규모 프로젝트를 위한 주문형 탄력적 용량
데이터 과학 해카톤/시합 또는 대규모 데이터 모델링 탐사에는, 일반적으로 짧은 기간 동안 확장된 하드웨어 용량이 필요합니다. 데이터 과학 VM hello hello 데이터 과학 환경을 신속 하 게 요청 시 복제, 필요한 고성능 컴퓨팅 리소스 toobe 실험을 허용 하는 수평 확장 된 서버에서 실행 시킬 수 있습니다.

### <a name="short-term-experimentation-and-evaluation"></a>단기 실험 및 평가
hello 데이터 과학 VM 수 사용된 tooevaluate 하거나 배울 수 있는 도구 Microsoft R Server, SQL Server와 같은 Visual Studio 도구의 심층 학습 Jupyter / 기계 학습 도구 키트 및에 자주 사용 되는 새로운 도구 hello 커뮤니티에는 최소한의 설치 노력 합니다. 데이터 과학 VM hello를 신속 하 게 설정할 수 있습니다, 때문에 게시 된 실험, 데모, 온라인 세션 또는 회의 자습서의 다음 연습에서는 실행을 복제와 같은 다른 단기 사용 시나리오에 적용할 수 있습니다.

### <a name="deep-learning"></a>심층 학습
GPU (그래픽 처리 장치) 기반된 하드웨어에 심층 학습 알고리즘을 사용 하 여 학습 모델에 대 한 hello 데이터 과학 VM을 사용할 수 있습니다. VM의 Azure 클라우드 기능 확장를 활용 하 DSVM 사용 하면 GPU 기반 하드웨어를 사용 하 여 필요에 따라 hello 클라우드에 있습니다. 전환할 수 하나 필요 하 게 유지 하면서 고속 계산 hello 동일한 운영 체제 디스크 또는 tooa GPU 큰 모델을 학습할 때 VM을 기반으로 합니다.  hello Windows Server 2016 버전 DSVM의 사전 설치 된 프레임 워크 및 GPU 버전 hello 심층 학습 알고리즘의 GPU 드라이버와 함께 제공 됩니다. Linux hello에 GPU에서 학습 깊습니다 hello에 대해서만 사용 하도록 설정 [(Ubuntu) Linux 버전에 대 한 데이터 과학 가상 컴퓨터](http://aka.ms/dsvm/ubuntu)합니다. 이 경우 모든 hello 심층 학습 프레임 워크는 대체 (fallback) toohello CPU 모드 hello Ubuntu/Windows-2016 버전 데이터 과학 VM toonon GPU 기반 Azure 가상 컴퓨터를 배포할 수 있습니다. 이전에는 Windows Server 2012용으로 [심층 학습 도구 키트](http://aka.ms/dsvm/deeplearning)가 게시되었지만, 이제 Windows 기반 심층 학습 작업에는 Windows Server 2016을 사용하는 것이 좋습니다. hello CentOS 기반 Linux 버전의 hello DSVM CPU hello 심층 학습 도구 (CNTK, Tensorflow, MXNet)의 일부를 작성은 하지만 hello GPU 드라이버 프레임 워크와 사전 설치 된이 제공 되지 않는 유일한 hello 포함 되어 있습니다. 

## <a name="whats-included-in-hello-data-science-vm"></a>요소에 포함 된 데이터 과학 VM hello?
hello 데이터 과학 가상 컴퓨터에 많은 일반적인 데이터 과학 및 심층 학습 도구를 이미 설치 및 구성 합니다. 또한 쉽게 toowork 다양 한 Azure 데이터 및 분석 제품을 구성 하는 도구가 포함 되어 있습니다. 탐색 하 고 hello Microsoft R Server 또는 SQL Server 2016을 사용 하 여 대규모 데이터 집합에 예측 모델을 작성할 수 있습니다. Microsoft와 오픈 소스 커뮤니티 hello에서에서 다른 도구의 호스트 포함으로 샘플 코드와 전자 필기장 됩니다. hello 다음 표에서 항목별로 정리 하 고 Windows hello 및 hello 데이터 과학 가상 컴퓨터의 Linux 버전에 포함 된 hello 주요 구성 요소를 비교 합니다.


| **도구**                                                           | **Windows 버전** | **Linux 버전** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| 인기 있는 패키지가 사전 설치된 [Microsoft R Open](https://mran.microsoft.com/open/)   |Y                      | Y             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition은 다음을 포함합니다. <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) 병렬 및 분산된 고성능 R 프레임워크<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) -Microsoft의 새로운 기계 학습 알고리즘 <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [R 운영](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |Y                      | Y <br/> (MicrosoftML은 아직 사용할 수 없음)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro-Plus(공유 정품 인증) - Excel, Word 및 PowerPoint   |Y                      |N              |
| 인기 있는 패키지가 사전 설치된 [Anaconda Python](https://www.continuum.io/) 2.7, 3.5    |Y                      |Y              |
| Julia 언어에 대해 인기 있는 패키지가 사전 설치된 [JuliaPro](https://juliacomputing.com/products/juliapro.html)                         |Y                      |Y              |
| 관계형 데이터베이스                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| 데이터베이스 도구                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * ODBC/JDBC 드라이버| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/)(쿼리 도구), <br /> * bcp, sqlcmd <br /> * ODBC/JDBC 드라이버|
| SQL Server R Services를 통한 확장성 있는 데이터베이스 내 분석 | Y     |N              |
| 다음의 커널이 있는 **[Jupyter 노트북 서버](http://jupyter.org/),**                                  | Y     | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 & 3.5 | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (Ubuntu에만 해당) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | Y |
| JupyterHub(다중 사용자 노트북 서버)| N | Y |
| **개발 도구, IDE 및 코드 편집기**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017(Community Edition)](https://www.visualstudio.com/community/) - Git 플러그 인, Azure HDInsight(Hadoop), Data Lake, SQL Server Data Tools, [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs) 및 [RTVS(Visual Studio용 R 도구)](http://microsoft.github.io/RTVS-docs/) 포함 | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio Code](https://code.visualstudio.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (Julia IDE)](http://junolab.org/)| Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim 및 Emacs | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git 및 GitBash | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | Y | N |
| PowerBI Desktop | Y | N |
| Sdk tooaccess Azure 및 서비스의 Cortana Intelligence 도구 모음 | Y | Y |
| **데이터 이동 및 관리 도구** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Storage Explorer | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azure CLI](https://docs.microsoft.com/cli/azure/overview) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy(Azure Data Lake 저장소)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [DocDB 데이터 마이그레이션 도구](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft 데이터 관리 게이트웨이](https://msdn.microsoft.com/library/dn879362.aspx) : 온-프레미스 및 클라우드 간 데이터 이동 | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Unix/Linux 명령줄 유틸리티 | Y | Y |
| 데이터 탐색에 대한 [Apache Drill](http://drill.apache.org) | Y | Y |
| **Machine Learning 도구** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)(R, Python)과 통합 | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (Ubuntu에만 해당) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | N | Y (Ubuntu에만 해당) |
| **GPU 기반 심층 학습 도구** |Windows Server 2016 버전  |Ubuntu 버전 |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | Y | Y|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe & Caffe2](https://github.com/caffe2/caffe2) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CUDA, CUDNN, Nvidia 드라이버](https://developer.nvidia.com/cuda-toolkit) | Y | Y |
| **빅 데이터 플랫폼(Devtest에만 해당)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* 로컬 [Spark](http://spark.apache.org/) 독립 실행형 | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* 로컬 [Hadoop](http://hadoop.apache.org/)(HDFS, YARN) | N | Y |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Tooget은 데이터 과학 VM Windows hello로 시작 하는 방법
* 로 이동 하 여 원하는 hello Windows DSVM 버전의 인스턴스를 만듭니다.
  * [Windows Server 2016 기반 DSVM](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  또는 
  * [Windows Server 2012 기반 DSVM](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Hello 클릭 **GET IT 이제** 단추입니다.
* Hello VM을 만들 때 지정한 hello 자격 증명을 사용 하 여 원격 데스크톱에서 toohello VM에에서 로그인 합니다.
* 를 사용할 수 있는 toodiscover 및 시작 hello 도구 클릭 hello **시작** 메뉴.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Linux 데이터 과학 VM hello로 시작.
* 원하는 hello의 인스턴스를 만들고 너무 이동 하 여 Linux DSVM 버전
  * [Ubuntu 기반 DSVM](http://aka.ms/dsvm/ubuntu)

  또는

  * [OpenLogic CentOS 기반 DSVM](http://aka.ms/dsvm/centos)

  
* Hello 클릭 **지금 사용해 보세요** 단추입니다.
* SSH를 사용 하 여 명령을 hello VM을 만들 때 지정한 hello 자격 증명 또는 Putty 같은 SSH 클라이언트에서 toohello VM에에서 로그인 합니다.
* Hello 셸 프롬프트에서 dsvm 더 이상 정보를 입력 합니다.
* 그래픽 데스크톱에 대 한 클라이언트 플랫폼에 대 한 hello X2Go 클라이언트 다운로드 [여기](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) hello Linux 데이터 과학 VM 문서에서 hello 지침 [프로 비전 hello Linux 데이터 과학 가상 컴퓨터](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>다음 단계
### <a name="for-hello-windows-data-science-vm"></a>데이터 과학 VM Windows hello에 대 한
* 특정 toorun 도구 hello Windows 버전에서 사용할 수 있는 방법에 대 한 자세한 내용은 참조 하십시오. [Microsoft 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-provision-vm.md) 및
* Hello Windows VM의 데이터 과학 프로젝트에 필요한 다양 한 작업이 참조 하는 tooperform 방법에 대 한 자세한 내용은 [hello 데이터 과학 가상 컴퓨터에서 수행할 수 있는 10 개의 작업](machine-learning-data-science-vm-do-ten-things.md)합니다.

### <a name="for-hello-linux-data-science-vm"></a>Linux 데이터 과학 VM hello에 대 한
* 특정 toorun 도구 hello Linux 버전에서 사용할 수 있는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-linux-dsvm-intro.md)합니다.
* 어떻게 tooperform 몇 가지 일반 데이터 과학 작업을 Linux VM hello로 보여 주는 연습을 참조 하십시오. [hello Linux 데이터 과학 가상 컴퓨터에서 데이터 과학](machine-learning-data-science-linux-dsvm-walkthrough.md)합니다.

