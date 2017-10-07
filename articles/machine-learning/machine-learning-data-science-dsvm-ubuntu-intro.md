---
title: "데이터 과학 가상 컴퓨터에 대 한 Azure에서 Linux (Ubuntu)에 aaaProvision hello | Microsoft Docs"
description: "Azure toodo 분석에는 데이터 과학 가상 컴퓨터에 대 한 Linux (Ubuntu)을 구성 하 고 만들고 기계 학습 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 037c126c0a35d8065fc89c591089df73d2b91425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-data-science-virtual-machine-for-linux-ubuntu"></a>Linux (Ubuntu)에 대 한 hello 데이터 과학 가상 컴퓨터를 프로 비전
Ubuntu 기반 hello Linux에 대 한 데이터 과학 가상 컴퓨터는 쉽게 tooget를 사용 하면 가상 컴퓨터 이미지를 Azure에서 심층 학습 하기 시작 합니다. 심층 학습 도구에는 다음이 포함됩니다.

  * [Caffe](http://caffe.berkeleyvision.org/): 속도, 표현도 및 모듈화를 위해 구축된 심층 학습 프레임워크
  * [Caffe2](https://github.com/caffe2/caffe2): Caffe의 플랫폼 간 버전
  * [CNTK(Computational Network Toolkit)](https://github.com/Microsoft/CNTK): Microsoft Research의 심화 학습 소프트웨어 도구 키트
  * [H2O](https://www.h2o.ai/): 오픈 소스 빅 데이터 플랫폼 및 그래픽 사용자 인터페이스
  * [Keras](https://keras.io/): Python의 Theano 및 TensorFlow용 고급 신경망 네트워크 API
  * [MXNet](http://mxnet.io/): 많은 언어 바인딩을 사용하는 유연하고 효율적인 심층 학습 라이브러리
  * [NVIDIA DIGITS](https://developer.nvidia.com/digits): 일반적인 심층 학습 작업을 단순화하는 그래픽 시스템
  * [TensorFlow](https://www.tensorflow.org/): Google의 컴퓨터 인텔리전스를 위한 오픈 소스 라이브러리
  * [Theano](http://deeplearning.net/software/theano/): 다차원 배열과 관련된 수학 식을 정의하고, 최적화하고, 효율적으로 계산하기 위한 Python 라이브러리
  * [Torch](http://torch.ch/): 기계 학습 알고리즘을 광범위하게 지원하는 공학용 계산 프레임워크
  * CUDA, cuDNN, 및 hello NVIDIA 드라이버
  * 많은 샘플 Jupyter 노트북

모든 라이브러리는 hello GPU 버전, 경우에 hello CPU에서 실행 됩니다.

또한 hello Linux에 대 한 데이터 과학 가상 컴퓨터를 포함 하 여 데이터 과학 및 개발 작업을 위한 인기 있는 도구를 포함 되어 있습니다.

* Microsoft R Open을 포함하는 Microsoft R Server Developer Edition
* 널리 사용되는 데이터 분석 라이브러리를 포함한 Anaconda Python 배포(버전 2.7 및 3.5)
* JuliaPro - 인기 있는 과학 및 데이터 분석 라이브러리와 함께 Julia 언어의 큐레이트 배포
* 독립 실행형 Spark 인스턴스 및 단일 노드 Hadoop(HDFS, Yarn)
* JupyterHub - R, Python, PySpark, Julia 커널을 지원하는 다중 사용자 Jupyter Notebook 서버
* Azure Storage 탐색기
* Azure 리소스 관리를 위한 Azure CLI(명령줄 인터페이스)
* 기계 학습 도구
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): 온라인, 해시, allreduce, 축소, learning2search, 활성 및 대화형 학습 등의 기술을 지원하는 속성 기계 학습 시스템
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): 기능이 향상된 빠르고 정확한 트리 구현을 제공하는 도구
  * [Rattle](http://rattle.togaware.com/): R에서 데이터 분석 및 기계 학습을 쉽게 시작할 수 있도록 하는 그래픽 도구
  * [LightGBM](https://github.com/Microsoft/LightGBM): 빠른 분산형 고성능 그라데이션 향상 프레임워크
* Java, Python, node.js, Ruby, PHP의 Azure SDK
* Azure 기계 학습 및 기타 Azure 서비스에서 사용하기 위한 R 및 Python의 라이브러리
* 개발 도구 및 편집자(RStudio, PyCharm, IntelliJ, Emacs, vim)


데이터 과학을 수행하려면 일련의 작업에 대해 다음 작업을 반복합니다.

1. 데이터 찾기, 로드 및 전처리
2. 모델 빌드 및 테스트
3. 지능형 응용 프로그램의 소비에 대 한 hello 모델 배포

데이터 과학자는 다양 한 도구 toocomplete 이러한 작업을 사용합니다. 시간이 많이 소요 toofind hello 적절 한 버전의 hello 소프트웨어 수 및 toodownload, 컴파일 및 이러한 버전을 설치 합니다.

hello Linux에 대 한 데이터 과학 가상 컴퓨터는 대체로 이러한 부담을 줄일 수 있습니다. 대신 toojump start 분석 프로젝트. Toowork를 R, Python, SQL, Java 및 c + +를 포함 하 여 다양 한 언어로 작업에 있습니다. hello hello VM에에서 포함 된 Azure SDK 있습니다 toobuild hello Microsoft 클라우드 플랫폼에 대 한 Linux에서 다양 한 서비스를 사용 하 여 응용 프로그램입니다. 또한, 액세스 tooother 언어 Ruby, Perl, PHP 및 node.js 같은 미리 설치 되어 있을 수 있습니다.

이 데이터 과학 VM 이미지에 대한 소프트웨어 요금은 부과되지 않습니다. 만 hello Azure 하드웨어 사용 요금을 hello 프로 비전 하는 hello 가상 컴퓨터 크기에 따라 평가 하는 비용을 지불 합니다. Hello에 대 한 자세한 내용은 계산 요금 hello에서 확인할 수 있습니다 [hello Azure Marketplace에서 VM 목록 페이지](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/)합니다.

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>다른 버전의 hello 데이터 과학 가상 컴퓨터
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) hello 많이 동일 Ubuntu 이미지 hello과 도구, 이미지도 있습니다. [Windows](machine-learning-data-science-provision-vm.md) 이미지도 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
Linux용 데이터 과학 가상 컴퓨터를 만들려면 먼저 Azure 구독이 있어야 합니다. 하나의 tooobtain 참조 [가져오기 Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.

## <a name="create-your-data-science-virtual-machine-for-linux"></a>Linux용 데이터 과학 가상 컴퓨터 만들기
Hello 단계 toocreate hello Linux에 대 한 데이터 과학 가상 컴퓨터의 인스턴스는 다음과 같습니다.

1. Hello에 나열 된 toohello 가상 컴퓨터를 이동 [Azure 포털](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vm-ubuntulinuxdsvmubuntu)합니다.
2. 클릭 **만들기** (아래쪽 hello) hello 마법사 toobring.![ 구성-데이터-과학-vm](./media/machine-learning-data-science-dsvm-ubuntu-intro/configure-data-science-virtual-machine.png)
3. 다음 섹션 hello toocreate hello Microsoft 데이터 과학 가상 컴퓨터를 사용 하는 hello에서 각 단계 (hello hello 앞 그림의 오른쪽에 열거 된) hello 마법사에 대 한 hello 입력을 제공 합니다. Hello 필요한 입력 tooconfigure 각 단계는 다음과 같습니다.
   
   a. **기본 사항**:
   
   * **이름**: 만들려는 데이터 과학 서버 이름
   * **사용자 이름**: 첫 번째 계정 로그인 ID입니다.
   * **암호**: 첫 번째 계정 암호입니다. 암호 대신 SSH 공개 키를 사용할 수 있습니다.
   * **구독**: 선택 hello는 hello 않습니다 컴퓨터가 만들어지고 비용이 청구 toobe 하나에 둘 이상의 구독이 있는 경우. 이 구독에 대한 리소스 만들기 권한이 있어야 합니다.
   * **리소스 그룹**: 새 그룹을 만들거나 기존 그룹을 사용할 수 있습니다.
   * **위치**: 가장 적합 한 선택 hello 데이터 센터입니다. 일반적으로 대부분의 프로그램 데이터는 가장 빠른 네트워크 액세스에 가장 가까운 tooyour 실제 위치 또는 hello 데이터 센터를입니다.
   
   b. **크기**:
   
   * 기능 요구 사항 및 비용 제약 조건을 충족 하는 hello 서버 유형 중 하나를 선택 합니다. 선택 **모두 보기** toosee VM 크기 중 더 선택 합니다. GPU 학습을 위한 NC 클래스 VM을 선택합니다.
   
   c. **설정**:
   
   * **디스크 유형**: SSD(반도체 드라이브)를 선호하는 경우 **프리미엄**을 선택합니다. 그렇지 않은 경우에는 **표준**을 선택합니다. GPU VM에는 표준 디스크가 필요합니다.
   * **저장소 계정**: 있습니다 수 새 Azure 저장소 계정에서 구독을 만들거나 hello에서 기존 구성을 사용 하 여 hello에 선택 된 동일한 위치 **기본 사항** hello 마법사의 단계입니다.
   * **다른 매개 변수**: 대부분의 경우에만 hello 기본값이 사용 합니다. tooconsider 기본값이 아닌 값, hello에 대 한 정보 링크를 가리키도록 hello 특정 필드에 대 한 도움말입니다.
   
   d. **요약**:
   
   * 입력한 모든 정보가 올바른지 확인합니다.
   
   e. **구입**:
   
   * toostart 프로 비전 hello, 클릭 **구입**합니다. 링크는 toohello 약관 hello 트랜잭션 제공 됩니다. hello VM hello에서 선택한 hello 서버 크기에 대 한 hello 계산 이외의 추가 비용이 없는 **크기** 단계입니다.

hello를 프로 비전 약 5-10 분 소요 됩니다. hello를 프로 비전의 hello 상태 hello Azure 포털에 표시 됩니다.

## <a name="how-tooaccess-hello-data-science-virtual-machine-for-linux"></a>Linux 용 tooaccess 데이터 과학 가상 컴퓨터 hello 하는 방법
VM이 생성 하는 hello, 후 SSH를 사용 하 여 tooit에 서명할 수 있습니다. Hello에서 만든 hello 계정 자격 증명을 사용 하 여 **기본 사항** 섹션 hello 텍스트 셸 인터페이스에 대 한 3 단계. Windows에서는 [Putty](http://www.putty.org)와 같은 SSH 클라이언트 도구를 다운로드할 수 있습니다. 그래픽 데스크톱 (X Windows 시스템)를 선호 하는 경우 Putty에서 X11를 사용 하 여 또는 hello X2Go 클라이언트를 설치할 수 있습니다.

> [!NOTE]
> hello X2Go 클라이언트 크게 수행 테스트 X11 보다 우수 합니다. 데스크톱의 그래픽 인터페이스에 대 한 hello X2Go 클라이언트를 사용 하는 것이 좋습니다.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>X2Go 클라이언트 설치 및 구성
Linux VM hello가 X2Go 서버 및 준비 tooaccept 클라이언트 연결을 이미 프로 비전 합니다. tooconnect toohello Linux VM 그래픽 데스크톱 클라이언트에서 다음 hello지 않습니다.

1. 다운로드 및 설치에서 클라이언트 플랫폼에 대 한 클라이언트 hello X2Go [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient)합니다.    
2. Hello X2Go 클라이언트를 실행 하 고 선택 **새 세션**합니다. 여러 탭이 있는 구성 창이 열립니다. Hello 구성 매개 변수를 다음을 입력 합니다.
   * **세션 탭**:
     * **호스트**: hello 호스트 이름 또는 데이터 과학 Linux VM의 IP 주소입니다.
     * **로그인**: hello Linux VM의 사용자 이름입니다.
     * **SSH 포트**: 22, hello 기본값에 둡니다.
     * **세션 유형**: hello 값 tooXFCE 변경 합니다. 현재 Linux VM hello XFCE 데스크톱만 지원합니다.
   * **미디어 탭**: 사운드 지원 및 클라이언트 toouse 필요는 없지만 인쇄를 해제할 수 있습니다 이러한.
   * **공유 폴더**: hello Linux VM에 탑재 된 클라이언트 컴퓨터에서 디렉터리를 원하는 경우이 탭에서 VM hello로 tooshare 원하는 hello 클라이언트 컴퓨터 디렉터리를 추가 합니다.

Hello SSH 클라이언트 또는 hello X2Go 클라이언트를 통해 XFCE 그래픽 데스크톱을 사용 하 여 toohello VM에에서 로그인 후에 설치 되 고 hello VM에 구성 하는 hello 도구를 사용 하 여 준비 toostart 됩니다. XFCE, 대부분의 hello 도구에 대 한 응용 프로그램 메뉴 바로 가기 및 바탕 화면 아이콘을 볼 수 있습니다.

## <a name="tools-installed-on-hello-data-science-virtual-machine-for-linux"></a>Linux 용 hello 데이터 과학 가상 컴퓨터에 설치 된 도구
### <a name="deep-learning-libraries"></a>심층 학습 라이브러리

#### <a name="cntk"></a>CNTK
Microsoft Cognitive Toolki-CNTK-hello는 오픈 소스, 심층 학습 도구 키트입니다. Python 바인딩은 hello 루트 및 py35 Conda 환경에서 사용할 수 있는입니다. Hello 경로에 이미 있는 명령줄 도구 (cntk)에 있습니다.

샘플 Python 노트북은 JupyterHub에서 사용할 수 있습니다. hello 명령줄에서 기본 샘플 toorun hello 명령을 hello 셸에서 다음 실행 합니다.

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

자세한 내용은 참조의 CNTK 섹션 hello [GitHub](https://github.com/Microsoft/CNTK), 및 hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki)합니다.

#### <a name="caffe"></a>Caffe
Caffe는 hello Berkeley 비전에서에서 프레임 워크 및 학습 센터 학습 깊습니다. /opt/caffe에서 사용할 수 있습니다. 예제는 /opt/caffe/examples에서 찾을 수 있습니다.

#### <a name="caffe2"></a>Caffe2
Caffe2는 Caffe를 기반으로 제작된 Facebook의 심층 학습 프레임워크입니다. Hello Conda 루트 환경에서 Python 2.7 제공 됩니다. tooactivate 것 hello 셸에서 hello 다음 실행:

    source /anaconda/bin/activate root

JupyterHub에서 몇 가지 예제 Notebook이 제공됩니다.

#### <a name="h2o"></a>H2O
H2O는 빠른 메모리 내 분산형 기계 학습 및 예측 분석 플랫폼입니다. Python 패키지 hello 루트 및 py35 Anaconda 환경에 설치 됩니다. R 패키지도 설치됩니다. 실행 하는 hello commandline H2O toostart `java -jar /dsvm/tools/h2o/current/h2o.jar`; 다양 한 가지 [명령줄 옵션](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/starting-h2o.html#from-the-command-line) tooconfigure를 원하는 수 있습니다. 웹 UI 흐름 hello toohttp://localhost:54321 tooget 시작을 검색 하 여 액세스할 수 있습니다. 샘플 노트북은 JupyterHub에서도 사용할 수 있습니다.

#### <a name="keras"></a>Keras
Keras는 Tensorflow 또는 Theano에서 실행될 수 있는 Python의 고급 신경망 네트워크 API입니다. Hello 루트 및 py35 Python 환경 제공 됩니다. 

#### <a name="mxnet"></a>MXNet
MXNet은 효율성과 유연성을 위해 디자인된 심층 학습 프레임워크입니다. R 및 Python 바인딩 DSVM hello에 포함 되어 있음 샘플 노트북은 JupyterHub에 포함되어 있고 샘플 코드는 /dsvm/samples/mxnet에서 사용할 수 있습니다.

#### <a name="nvidia-digits"></a>NVIDIA DIGITS
hello NVIDIA 심층 학습 GPU 교육 시스템 자리 수로 알려진는 시스템 toosimplify 심층 학습 / 같은 일반적인 작업 데이터, 디자인 및 GPU 시스템에서는 신경망 학습 관리 고급 시각화 실시간에서 성능 모니터링입니다. 

DIGITS는 digits라는 서비스로 사용할 수 있습니다. Hello 서비스를 시작 하 고 찾아보기 toohttp://localhost:5000 tooget 시작 합니다.

숫자는 Python 모듈로 hello Conda 루트 환경에도 설치 됩니다.

#### <a name="tensorflow"></a>TensorFlow
TensorFlow는 Google의 심층 학습 라이브러리입니다. 데이터 흐름 그래프를 사용한 숫자 계산을 위한 오픈 소스 소프트웨어 라이브러리입니다. TensorFlow hello py35 Python 환경에서 사용할 수 있으며 일부 샘플 노트북이 JupyterHub에 포함 됩니다.

#### <a name="theano"></a>Theano
Theano는 효율적인 숫자 계산을 위한 Python 라이브러리입니다. Hello 루트 및 py35 Python 환경 제공 됩니다. 

#### <a name="torch"></a>Torch
Torch는 기계 학습 알고리즘을 광범위하게 지원하는 공학용 계산 프레임워크입니다. /Dsvm/tools/torch에서 사용할 수 있으며 hello 번째 대화형 세션 및 luarocks 패키지 관리자는 hello 명령줄에서 제공 됩니다. 예제는 /dsvm/samples/torch에서 사용할 수 있습니다.

PyTorch는 hello 루트 Anaconda 환경에서 사용할 수 이기도합니다. 예제는 /dsvm/samples/pytorch에 있습니다.

### <a name="microsoft-r-server"></a>Microsoft R 서버
R은 데이터 분석 및 기계 학습에 사용 된 hello 가장 인기 있는 언어 중 하나입니다. R toouse 여 분석을 위해 원하는 경우 수학 커널 라이브러리 (MKL) 및 Microsoft R Server (부인은 어) hello Microsoft R Open (MRO)로 hello VM에 있습니다. hello MKL 분석 알고리즘에 공통 수학 작업을 최적화합니다. MRO CRAN R 호환 100% 이며 CRAN에 게시 하는 hello R 라이브러리 MRO hello에 설치할 수 있습니다. MRS는 R 모델의 크기 조정 및 운영을 웹 서비스에 제공합니다. RStudio, vi, 또는 Emacs 같은 hello 기본 편집기 중 하나에 따라 R 프로그램을 편집할 수 있습니다. 참고 ESS (Emacs 말하는 통계), 해당 hello Emacs 패키지 hello Emacs 편집기를 사용 중인 경우 간소화 R 파일 hello Emacs 편집기 내에서 작업을 미리 설치 되었습니다.

toolaunch R 콘솔 입력 하기만 하면 **R** hello 셸에서 합니다. Tooan 대화형 환경을 이동합니다. toodevelop R 프로그램 일반적으로 Emacs 또는 vi와 같은 편집기를 사용 하 고 다음 오른쪽 내 hello 스크립트 실행 RStudio, R 프로그램 전체 그래픽 IDE 환경 toodevelop 수 있습니다.

R 스크립트 tooinstall hello에 대 한 이기도 [상위 20 R 패키지](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) 들어 있습니다. 입력할 수 있습니다 (설명 했 듯이)을 입력 하 여 hello R 대화형 인터페이스에서이 스크립트를 실행 하려면 **R** hello 셸에서 합니다.  

### <a name="python"></a>Python
Python을 사용하여 개발하는 경우를 위해, Anaconda Python 배포 2.7 및 3.5가 설치되었습니다. 이 배포 hello가 포함 되어 기본 Python의 hello 가장 인기 있는 수학 엔지니어링 및 데이터 분석 패키지의 약 300 함께 합니다. Hello 기본 텍스트 편집기를 사용할 수 있습니다. 또한 Anaconda Python 배포에 번들로 포함된 Python IDE인 Spyder를 사용할 수도 있습니다. Spyder를 사용하려면 그래픽 데스크톱 또는 X11 전달이 필요합니다. 바로 가기 tooSpyder hello 그래픽 바탕 화면에서 제공 됩니다.

Toospecifically Python 2.7 및 3.5를 둘 다는 것이 아니므로 해야 원하는 hello Python 버전 (conda 환경)에서 hello에 toowork 현재 세션을 활성화 합니다. hello 정품 인증 과정 hello 경로 변수 toohello Python의 원하는 버전을 설정합니다.

tooactivate hello Python 2.7 conda 환경, hello 셸에서 hello 다음 실행:

    source /anaconda/bin/activate root

Python 2.7은 */anaconda/bin*에 설치됩니다.

tooactivate hello Python 3.5 conda 환경, hello 셸에서 hello 다음 실행:

    source /anaconda/bin/activate py35


Python 3.5는 */anaconda/envs/py35/bin*에 설치됩니다.

Python 대화형 세션 tooinvoke 입력 **python** hello 셸에서 합니다. 입력할 수는 그래픽 인터페이스에 있거나 X11 집합을, 경우 **pycharm** toolaunch hello PyCharm 인 Python IDE 인 합니다.

추가 Python 라이브러리 tooinstall 해야 toorun ```conda``` 또는 ````pip```` sudo에서 명령을 클릭 한 hello Python 패키지 관리자의 전체 경로 (conda 또는 pip) tooinstall toohello 올바른 Python 환경을 제공 합니다. 예:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter Notebook
Jupyter 노트북, 환경 tooshare 코드 및 분석 hello Anaconda 배포도 제공 됩니다. hello Jupyter 노트북 JupyterHub 통해 액세스 됩니다. 로컬 Linux 사용자 이름 및 암호를 사용하여 로그인합니다.

hello Jupyter 노트북 서버 Python 2, Python 3, R 커널을와 미리 구성 되었습니다. 바탕 화면 아이콘 "Jupyter 노트북" toolaunch hello 브라우저 tooaccess hello 노트북 서버 이름이 있습니다. 또한 방문할 수 있는 SSH 또는 X2Go 클라이언트를 통해 VM hello에 있는 경우 [https://localhost:8000 /](https://localhost:8000/) tooaccess hello Jupyter 노트북 서버입니다.

> [!NOTE]
> 인증서 경고가 나타나는 경우 계속 진행하세요.
> 
> 

Hello Jupyter 노트북 서버는 모든 호스트에서 액세스할 수 있습니다. *https://\<VM DNS 이름 또는 IP 주소\>:8000/*만 입력하면 됩니다.

> [!NOTE]
> 포트 8000 hello VM 프로 비전 될 때 기본적으로 hello 방화벽에서 열립니다.
> 
> 

샘플 전자 필기장-하나에 Python 및 R에서 하나를 패키지에서는 로컬 Linux 사용자 이름 및 암호를 사용 하 여 toohello Jupyter 노트북을 인증 한 후 hello 노트북 홈 페이지에 hello 링크 toohello 샘플을 볼 수 있습니다. 새 전자 필기장을 선택 하 여 만들 수 있습니다 **새로**, 및 다음 hello 적절 한 언어 커널 합니다. Hello 표시 되지 않으면 **새로** 단추를 클릭 hello **Jupyter** hello 노트북 서버 hello 맨 위 왼쪽된 toogo toohello 홈 페이지에서 아이콘입니다.

### <a name="apache-spark-standalone"></a>Apache Spark 독립 실행형 
Apache Spark의 독립 실행형 인스턴스를 테스트 하 고 대규모 클러스터에 배포 하기 전에 먼저 Spark 응용 프로그램을 로컬로 개발 하는 Linux DSVM toohelp hello에 사전 설치 합니다. Hello Jupyter 커널을 통해 PySpark 프로그램을 실행할 수 있습니다. Jupyter 열고 hello "새로 만들기" 단추를 클릭 하면 사용할 수 있는 커널 목록이 표시 됩니다. hello "Spark-Python"는 hello PySpark 커널 Spark Python 언어를 사용 하 여 응용 프로그램을 빌드할 수 있도록 합니다. Python IDE 인 PyCharm 또는 Spyder toobuild 멤버 수와 같은 사용할 수 있습니다 프로그램입니다. 이후, 독립 실행형 인스턴스인을 hello Spark 스택 클라이언트 프로그램을 호출 하는 hello 내에서 실행 하세요. 이 통해 더 빠르게 하 고 쉽게 tootroubleshoot 문제 비교 toodeveloping Spark 클러스터에서 키를 누릅니다. 

Jupyter hello Jupyter ($HOME/노트북/SparkML/pySpark)의 홈 디렉터리 아래의 hello "SparkML" 디렉터리에서 찾을 수 있는 샘플 PySpark 노트북 제공 됩니다. 

Spark용 R에서 프로그래밍하는 경우 Microsoft R Server, SparkR 또는 sparklyr을 사용할 수 있습니다. 

Microsoft R Server에서 Spark 컨텍스트를 실행 하기 전에 한 번 설치 단계 tooenable Hadoop HDFS 로컬 단일 노드 및 Yarn 인스턴스 toodo 필요 합니다. Hadoop 서비스는 기본적으로 설치 되지만 DSVM hello를 사용 하지 않도록 설정 됩니다. 순서 tooenable, 되어야 처음으로 명령을 루트 hello로 다음 toorun hello.

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

중지할 수 hello Hadoop 관련 서비스를 실행 하 여 필요 하지 않을 때 ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` (즉, DSVM hello에 독립 실행형 Spark 인스턴스의 hello) 원격 Spark 컨텍스트에서 toodevelop 및 테스트 부인은 어 제공 되어 hello 에서에서사용할수있는방법을설명하는예제`/dsvm/samples/MRS` 디렉터리입니다. 

### <a name="ides-and-editors"></a>IDE 및 편집기
여러 코드 편집기 중에서 선택할 수 있습니다. vi/VIM, Emacs, PyCharm, RStudio 및 IntelliJ를 포함합니다. IntelliJ, RStudio PyCharm 그래픽 편집기 및 ी toobe 로그인 tooa 그래픽 데스크톱 toouse 해당 합니다. 이러한 편집기에는 데스크톱 및 응용 프로그램 메뉴 바로 가기 toolaunch 해당 합니다.

**VIM** 및 **Emacs**는 텍스트 기반 편집기입니다. Emacs에 Emacs 말하는 통계 (ESS) hello Emacs 편집기 내에서 R로 작업을 쉽게 이라는 추가 기능 패키지를 설치 합니다. 자세한 내용은 [ESS](http://ess.r-project.org/)를 참조하세요.

**LaTex** Emacs 추가 기능을 함께 hello texlive 패키지를 통해 설치 된 [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) Emacs 내 LaTex 문서 작성을 단순화 하는 패키지입니다.  

### <a name="databases"></a>데이터베이스

#### <a name="graphical-sql-client"></a>그래픽 SQL 클라이언트
**SQL 스 쿼 럴**, 그래픽 SQL 클라이언트 (예: Microsoft SQL Server 및 MySQL) tooconnect toodifferent 데이터베이스 및 SQL 쿼리 toorun 제공 되었습니다. (예를 들어 hello X2Go 클라이언트 사용) 그래픽 데스크톱 세션에서이 실행할 수 있습니다. 스 쿼 럴 SQL tooinvoke hello hello 바탕 화면 아이콘에서 시작 하거나 hello hello 셸에서 다음 명령을 실행 합니다.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Hello 하기 전에 처음 사용 하는 드라이버 및 데이터베이스 별칭을 설정 합니다. hello JDBC 드라이버는 위치에 있습니다.

*/usr/share/java/jdbcdrivers*

자세한 내용은 [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots)을 참조하세요.

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Microsoft SQL Server에 액세스하기 위한 명령줄 도구
SQL Server에 대 한 hello ODBC 드라이버 패키지는 또한 두 명령줄 도구와 함께 제공 합니다.

**bcp**: hello bcp 유틸리티 대량 복사의 Microsoft SQL Server 인스턴스 및 데이터 파일 간에 데이터를 사용자 지정 형식에서입니다. hello bcp 유틸리티에 사용 되는 tooimport 많은 수의 SQL Server 테이블 또는 테이블 데이터 파일로 테이블에서 데이터를 tooexport에 새 행 될 수 있습니다. 테이블로 tooimport 데이터를 해당 테이블에 대해 만든 서식 파일을 사용 하거나 hello 테이블 및 해당 열에 대해 사용할 수 있는 데이터 형식의 hello hello 구조를 이해 합니다.

자세한 내용은 [bcp를 사용하여 연결](https://msdn.microsoft.com/library/hh568446.aspx)을 참조하세요.

**sqlcmd**: hello sqlcmd 유틸리티, 뿐만 아니라 시스템 프로시저 TRANSACT-SQL 문을 입력 하 고 스크립트 hello 명령 프롬프트에서 파일입니다. 이 유틸리티는 ODBC tooexecute TRANSACT-SQL 일괄 처리를 사용합니다.

자세한 내용은 [sqlcmd를 사용하여 연결](https://msdn.microsoft.com/library/hh568447.aspx)을 참조하세요.

> [!NOTE]
> 이 유틸리티는 Linux 플랫폼과 Windows 플랫폼에서 다소 다릅니다. 자세한 내용은 hello 설명서를 참조 하십시오.
> 
> 

#### <a name="database-access-libraries"></a>데이터베이스 액세스 라이브러리
R 및 Python tooaccess 데이터베이스에서 사용 가능한 라이브러리 있습니다.

* R에서는 hello **RODBC** 패키지 또는 **dplyr** 패키지 tooquery 있습니다 또는 hello 데이터베이스 서버에서 SQL 문을 실행 합니다.
* Python에서 hello **pyodbc** hello 기본 계층으로 라이브러리는 odbc 데이터베이스 액세스를 제공 합니다.  

### <a name="azure-tools"></a>Azure 도구
Azure tools를 수행 하는 hello hello VM에 설치 됩니다.

* **Azure 명령줄 인터페이스**: hello Azure CLI toocreate 있으며 셸 명령을 통해 Azure 리소스 관리. tooinvoke hello Azure 도구, 입력 **azure 도움말**합니다. 자세한 내용은 참조 hello [Azure CLI 설명서 페이지](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.
* **Microsoft Azure 저장소 탐색기**: Microsoft Azure 저장소 탐색기는 Azure 저장소 계정 및 Azure blob에서 데이터 tooand tooupload 및 다운로드에 저장 된 hello 개체를 통해 사용 되는 toobrowse 되는 그래픽 도구입니다. 저장소 탐색기 hello 바탕 화면 바로 가기 아이콘에서 액세스할 수 있습니다. **StorageExplorer**를 입력하면 셸 프롬프트에서 Storage Explorer를 호출할 수 있습니다. Toobe X2Go 클라이언트에서 로그인 또는 X11 집합을 있어야 합니다.
* **Azure Libraries**: hello 다음은 hello 사전 설치 된 라이브러리의 일부입니다.
  
  * **Python**: 설치 된 Python에서 hello Azure 관련 라이브러리는 **azure**, **azureml**, **pydocumentdb**, 및 **pyodbc** . Hello 처음 세 개의 라이브러리와, Azure 저장소 서비스, Azure 기계 학습 및 Azure Cosmos DB (Azure에서 NoSQL 데이터베이스)에 액세스할 수 있습니다. hello 네 번째 라이브러리, hello 기반 Microsoft ODBC driver for SQL Server), (함께 pyodbc ODBC 인터페이스를 사용 하 여 액세스 tooSQL Server, Azure SQL 데이터베이스 및 Python에서 Azure SQL 데이터 웨어하우스를 사용 하면 됩니다. 입력 **pip 목록** toosee hello 모든 라이브러리를 나열 합니다. 이 명령에 Python 2.7 두 hello 및 3.5 환경 있는지 toorun 수 있습니다.
  * **R**: hello Azure 관련 라이브러리 R에서 설치 되는 **AzureML** 및 **RODBC**합니다.
  * **Java**: hello Azure Java 라이브러리 목록이 hello 디렉터리에 있습니다 **/dsvm/sdk/AzureSDKJava** hello VM에 있습니다. hello 키 라이브러리는 Azure 저장소 및 관리 Api, Azure Cosmos DB, 및 JDBC 드라이버가 SQL Server 용입니다.  

Hello에 액세스할 수 있습니다 [Azure 포털](https://portal.azure.com) hello 사전 설치 된 Firefox 브라우저에서 합니다. Hello Azure 포털에서 만들 관리 고 Azure 리소스를 모니터링할 수 있습니다.

### <a name="azure-machine-learning"></a>Azure 기계 학습
Azure 기계 학습은 toobuild 수 있도록 하는 완전히 관리 되는 클라우드 서비스를 배포 하 고 예측 분석 솔루션 공유 합니다. Azure Machine Learning Studio에서 실험 및 모델을 빌드합니다. 방문 하 여 hello 데이터 과학 가상 컴퓨터에서 웹 브라우저에서 액세스할 수 있습니다 [Microsoft Azure 기계 학습](https://studio.azureml.net)합니다.

TooAzure 기계 학습 스튜디오에에서 로그인 할 액세스 tooan 실험 캔버스 hello 기계 학습 알고리즘에 대 한 논리 흐름을 작성할 수 있습니다 사용할 수 있습니다. 또한 Azure 기계 학습에서 호스트 되는 액세스 tooa Jupyter 노트북 있고 기계 학습 스튜디오에서 실험 hello 원활 하 게 작업할 수 있습니다. Hello 기계 학습 웹 서비스 인터페이스에서 래핑하여 구축한 모델을 운용 합니다. 이 통해 hello 기계 학습 모델의에서 모든 언어 tooinvoke 예측에 작성 된 클라이언트입니다. 자세한 내용은 참조 hello [기계 학습 설명서](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.

Hello VM, Python 또는 R에서 모델을 작성할 수 있으며 하 한 다음 Azure 기계 학습에서 프로덕션 환경에서 배포할 수 있습니다. R에서 라이브러리를 설치 했습니다 (**AzureML**) 및 Python (**azureml**) tooenable이이 기능입니다.

Azure 기계 학습에 toodeploy R 및 Python에서 모델링 하는 방법에 대 한 정보를 참조 하십시오. [hello 데이터 과학 가상 컴퓨터에서 수행할 수 있는 10 개의 작업](machine-learning-data-science-vm-do-ten-things.md) (특히 hello 섹션 "R, Python을 사용 하 여 모델을 작성 및 해당 운영 화 사용 하 여 Azure 기계 학습 ").

> [!NOTE]
> 이러한 지침은 hello Windows 버전의 hello 데이터 과학 VM 용으로 작성 합니다. 하지만 모델 tooAzure 기계 학습의 배포에 제공 된 하는 hello 정보는 적용 가능한 toohello Linux VM입니다.
> 
> 

### <a name="machine-learning-tools"></a>기계 학습 도구
hello VM 도구와 미리 컴파일된 미리 로컬에 설치 되어 있는 알고리즘을 학습 하는 몇 가지 컴퓨터 함께 제공 됩니다. 내용은 다음과 같습니다.

* **Vowpal Wabbit**: 속성 온라인 학습 알고리즘입니다.
* **xgboost**: 최적화되고 향상된 트리 알고리즘을 제공하는 도구입니다.
* **Rattle**: 쉬운 데이터 탐색 및 모델링을 위한 R 기반 그래픽 도구입니다.
* **Python**: Anaconda Python에서는 Scikit-learn 등의 라이브러리가 포함된 기계 학습 알고리즘이 번들로 제공됩니다. Hello를 사용 하 여 다른 라이브러리를 설치할 수 있습니다 `pip install` 명령입니다.
* **LightGBM**: 의사 결정 트리 알고리즘을 기준으로 하는 빠른 분산형 고성능 그라데이션 향상 프레임워크입니다.
* **R**: 컴퓨터 학습 함수의 풍부한 라이브러리를 r 사용할 수 사전 설치 된 hello 라이브러리의 일부는 lm, glm, randomForest, rpart입니다. 다음 명령을 실행하면 다른 라이브러리를 설치할 수 있습니다.
  
        install.packages(<lib name>)

다음은 hello에 대 한 몇 가지 추가 정보 처음 세 컴퓨터 학습 도구 hello 목록에서입니다.

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit은 온라인, 해시, allreduce, 축소, learning2search, 활성 및 대화형 학습 등의 기술을 사용하는 기계 학습 시스템입니다.

매우 기본적인 예제에서 toorun hello 도구는 다음 hello지 않습니다.

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

해당 디렉터리에는 더 큰 다른 데모도 있습니다. VW에 대 한 자세한 내용은 참조 하십시오. [GitHub의이 섹션](https://github.com/JohnLangford/vowpal_wabbit), 및 hello [Vowpal Wabbit wiki](https://github.com/JohnLangford/vowpal_wabbit/wiki)합니다.

#### <a name="xgboost"></a>XGBoost
향상된 (트리) 알고리즘을 위해 디자인되고 최적화된 라이브러리입니다. hello이이 라이브러리는 toopush hello 계산 제한을 컴퓨터 toohello 극단적인 예측, 되는 확장 가능한 휴대용, 정확 하 게 tooprovide 대규모 트리 승격 필요 합니다.

R 라이브러리뿐만 아니라 명령줄로도 제공됩니다.

toouse R에서이 라이브러리에 대화형 R 세션을 시작할 수 있습니다 (입력 하 여 **R** hello 셸에서), 및 hello 라이브러리를 로드 합니다.

R 프롬프트에서 실행할 수 있는 간단한 예제는 다음과 같습니다.

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

toorun hello xgboost 명령줄 hello 셸에서 hello 명령을 tooexecute 다음과 같습니다.

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


.Model 파일에 지정 된 toohello 디렉터리를 기록 됩니다. 이 데모 예제에 대한 정보는 [GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification)에서 찾을 수 있습니다.

Xgboost에 대 한 자세한 내용은 참조 hello [xgboost 설명서 페이지](https://xgboost.readthedocs.org/en/latest/), 및 해당 [GitHub 리포지토리](https://github.com/dmlc/xgboost)합니다.

#### <a name="rattle"></a>Rattle
래 틀 (hello **R** **A**nalytical **T**ool **T**o **L**폭 **E** asily) GUI 기반 데이터 탐색 및 모델링을 사용합니다. 통계 표시 및 visual 데이터를 쉽게 모델링 될 수 있는 변환 데이터 요약 hello 데이터에서 감독 되지 않은 및 감독 모델, 표시 합니다. 모델의 성능을 그래픽으로 hello 빌드하고 점수 새 데이터를 설정 합니다. 또한 R에서 직접 실행 하거나 추가 분석을 위해 시작 지점으로 사용할 수 있는 UI hello hello 작업을 복제 하는 R 코드를 생성 합니다.

래 틀 toorun 그래픽 데스크톱 로그인 세션에 toobe가 있어야합니다. Hello 터미널 입력 ```R``` tooenter hello R 환경입니다. Hello R 프롬프트에서 다음 명령 hello를 입력 합니다.

    library(rattle)
    rattle()

이제 그래픽 인터페이스가 열리고 일련의 탭이 표시됩니다. 빠른 시작 단계 필요한 래 틀 toouse 샘플 날씨 데이터 집합 및 모델을 작성 하는 hello는 다음과 같습니다. 일부 아래 hello 단계에서 증명된 tooautomatically 설치 되 고 hello 시스템에 없는 일부 필요한 R 패키지를 로드 합니다.

> [!NOTE]
> Hello 시스템 디렉터리 (hello 기본값)에서 액세스 tooinstall hello 패키지 없다면 R 콘솔 창 tooinstall 패키지 tooyour 개인 라이브러리에 메시지가 나타날 수 있습니다. 이러한 메시지가 표시되면 *y* 로 응답합니다.
> 
> 

1. **실행**을 클릭합니다.
2. 대화 상자가 표시, toouse hello 예제 날씨 데이터 집합을 원하는 경우 요청 합니다. 클릭 **예** tooload hello 예제입니다.
3. Hello 클릭 **모델** 탭 합니다.
4. 클릭 **Execute** toobuild 의사 결정 트리 합니다.
5. 클릭 **그리기** toodisplay hello 의사 결정 트리 합니다.
6. Hello 클릭 **포리스트** 라디오 단추를 클릭 하 고 **Execute** toobuild 임의 포리스트 합니다.
7. Hello 클릭 **평가** 탭 합니다.
8. Hello 클릭 **위험** 라디오 단추를 클릭 하 고 **Execute** toodisplay 두 위험 (누적) 성능 점도 합니다.
9. Hello 클릭 **로그** 탭 tooshow hello 작업 앞에 오는 hello에 대 한 R 코드를 생성 합니다.
   (Tooinsert 래 틀의 hello 현재 릴리스에서 tooa 버그 인해 필요한는  *#*  앞에 문자 *...이 로그 내보내기*  hello 로그 hello 텍스트에.)
10. Hello 클릭 **내보내기** 라는 단추 toosave hello R 스크립트 파일 *weather_script 합니다. R* toohello 홈 폴더입니다.

래 틀와 오른쪽 종료 수 있습니다. 이제 생성 된 hello R 스크립트를 수정 하거나 toorun 그대로 사용할 수 있습니다이 언제 든 지 toorepeat hello 래 틀 UI 내에서 수행 된 모든 항목입니다. R에서 초보자를 위해 특별히 tooquickly 분석 및 기계 학습은 간단한 그래픽 인터페이스에서 자동으로 R toomodify에 코드를 생성 하는 동안 및/또는 자세한 쉽게 이것이입니다.

## <a name="next-steps"></a>다음 단계
학습과 탐색을 계속하는 방법은 다음과 같습니다.

* hello [hello Linux에 대 한 데이터 과학 가상 컴퓨터에서 데이터 과학](machine-learning-data-science-linux-dsvm-walkthrough.md) 연습에서는 어떻게 tooperform 몇 가지 일반 데이터 과학 작업을 여기에 프로 비전 하는 Linux 데이터 과학 VM hello로 합니다. 
* 다양 한 데이터 과학 도구에서이 문서에서 설명 하는 hello 도구를 시험 하 여 데이터 과학 VM hello hello를 탐색 합니다. 실행할 수도 있습니다 *dsvm 더 정보* hello 셸 hello VM에 설치 된 hello 도구에 대 한 기본적인 소개 및 포인터 toomore 정보 hello 가상 컴퓨터 내에서.  
* 체계적으로 사용 하 여 종단 간 분석 솔루션 toobuild hello 하는 방법에 대해 알아봅니다 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.
* Hello 방문 [Cortana 분석 갤러리](http://gallery.cortanaanalytics.com) 컴퓨터 학습 및 데이터 분석 샘플 Cortana Analytics Suite를 사용 하 여 hello에 대 한 합니다.

