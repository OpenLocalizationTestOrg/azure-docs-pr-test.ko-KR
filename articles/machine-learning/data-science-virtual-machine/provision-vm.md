---
title: "Azure에서 Windows 데이터 과학 Virtual Machine 프로비전 | Microsoft Docs"
description: "분석 및 기계 학습을 수행하기 위해 Azure에서 데이터 과학 Virtual Machine 구성 및 만들기"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 09/10/2017
ms.author: bradsev
ms.openlocfilehash: d71d8e44d0327515ed302c5c902ce87587e36c7d
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="provision-the-windows-data-science-virtual-machine-on-azure"></a>Azure에서 Windows 데이터 과학 Virtual Machine 프로비전
Microsoft 데이터 과학 Virtual Machine은 데이터 분석 및 기계 학습에 흔히 사용되는 몇 가지 인기 있는 도구로 사전 설치 및 구성된 Microsoft Azure VM(가상 머신) 이미지입니다. 포함된 도구는 다음과 같습니다.

* [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning-services/) Workbench
* [Microsoft ML Server](https://docs.microsoft.com/machine-learning-server/index) 디벨로퍼 버전
* Enthought Python 배포
* Jupyter Notebook(R, Python, PySpark 커널 포함)
* Visual Studio Community Edition
* Power BI 데스크톱
* SQL Server 2017 디벨로퍼 버전
* 로컬 개발 및 테스트를 위한 독립 실행형 Spark 인스턴스
* [JuliaPro](https://juliacomputing.com/products/juliapro.html)
* 기계 학습 및 데이터 분석 도구
  * 심화 학습 프레임워크: [Microsoft Cognitive 도구 키트](https://www.microsoft.com/en-us/cognitive-toolkit/), [TensorFlow](https://www.tensorflow.org/), [Chainer](https://chainer.org/), mxNet, Keras를 비롯한 다양한 AI 프레임 워크가 VM에 포함되어 있습니다.
  * 
            [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): 온라인, 해시, allreduce, 축소, learning2search, 활성 및 대화형 학습 등의 기술을 지원하는 속성 기계 학습 시스템.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): 기능이 향상된 빠르고 정확한 트리 구현을 제공하는 도구
  * 
            [Rattle](http://rattle.togaware.com/) (R Analytical Tool To Learn Easily): GUI 기반 데이터 탐색 및 모델링을 자동 R 코드 생성과 함께 사용하여 R에서의 데이터 분석 및 기계 학습을 쉽게 시작할 수 있도록 돕는 도구.
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): Java 형식의 시각적인 데이터 마이닝 및 기계 학습 소프트웨어.
  * [Apache Drill](https://drill.apache.org/): Hadoop, NoSQL 및 클라우드 저장소용의 스키마가 없는 SQL 쿼리 엔진.  NoSQL 및 PowerBI, Excel, Tableau와 같은 표준 BI 도구의 파일에 쿼리가 가능하도록 ODBC 및 JDBC 인터페이스를 지원합니다.
* Azure Machine Learning 및 기타 Azure 서비스에서 사용하기 위한 R 및 Python의 라이브러리
* GitHub, Visual Studio Team Services를 포함하는 소스 코드 리포지토리에 작동하는 Git Bash를 포함하는 Git
* 명령 프롬프트를 통해 액세스할 수 있는 몇 가지 인기 있는 Linux 명령줄 유틸리티(awk, sed, perl, grep, find, wget, curl 등 포함)의 Windows 포트 

데이터 과학을 수행하려면 일련의 작업에 대해 다음 작업을 반복합니다.

1. 데이터 찾기, 로드 및 전처리
2. 모델 빌드 및 테스트
3. 지능형 응용 프로그램에서 사용하기 위해 모델 배포

데이터 과학자는 다양한 도구를 사용하여 이러한 작업을 완료합니다. 소프트웨어의 적합한 버전을 찾고 다운로드하여 설치하는 데 소비되는 시간이 상당히 걸릴 수 있습니다. Microsoft 데이터 과학 Virtual Machine은 몇 가지 인기 있는 도구가 미리 설치되고 구성된 상태로 Azure에 프로비정될 수 있는 사용 가능 이미지를 제공하여 이러한 부담을 덜어줄 수 있습니다. 

Microsoft 데이터 과학 Virtual Machine은 분석 프로젝트를 빠르게 시작합니다. R, Python, SQL 및 C# 등의 다양한 언어로 작업을 수행할 수 있습니다. Visual Studio는 사용하기 쉬운 코드를 개발하고 테스트하기 위해 IDE를 제공합니다. VM에 포함된 Azure SDK를 통해 Microsoft의 클라우드 플랫폼에서 다양한 서비스를 사용하여 응용 프로그램을 빌드할 수 있습니다. 

이 데이터 과학 VM 이미지에 대한 소프트웨어 요금은 부과되지 않습니다. 프로비전하는 가상 머신의 크기에 따른 Azure 사용 비용만 지불하면 됩니다. 계산 비용에 대한 자세한 내용은 [데이터 과학 Virtual Machine](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.windows-data-science-vm?tab=PlansAndPrice) 페이지의 가격 책정 세부 정보 섹션에 나와 있습니다. 

## <a name="other-versions-of-the-data-science-virtual-machine"></a>다른 버전의 데이터 과학 Virtual Machine
[Ubuntu](dsvm-ubuntu-intro.md) 이미지도 비슷한 많은 도구 및 몇 가지 추가적인 심층 학습 프레임워크와 함께 사용할 수 있습니다. [CentOS](linux-dsvm-intro.md) 이미지도 사용할 수 있습니다. 몇 가지 도구는 Windows Server 2016 버전에서만 사용할 수 있지만 [Windows Server 2012 버전](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.standard-data-science-vm)의 데이터 과학 가상 컴퓨터도 제공됩니다.  그렇지 않은 경우 이 문서는 Windows Server 2012 버전에도 적용됩니다.

## <a name="prerequisites"></a>필수 구성 요소
Microsoft 데이터 과학 Virtual Machine을 만들려면 먼저 다음이 있어야 합니다.

* **Azure 구독**: 다운로드하려면 [Azure 무료 평가판 받기](http://azure.com/free)를 참조하세요.


## <a name="create-your-microsoft-data-science-virtual-machine"></a>Microsoft 데이터 과학 Virtual Machine 만들기
Microsoft 데이터 과학 Virtual Machine의 인스턴스를 만드는 단계는 다음과 같습니다.

1. [Azure 포털](https://portal.azure.com/#create/microsoft-ads.windows-data-science-vmwindows2016)에서 가상 머신 목록으로 이동합니다.
2. 마법사로 이동하려면 아래에 있는 **만들기** 단추를 선택합니다.![configure-data-science-vm](./media/provision-vm/configure-data-science-virtual-machine.png)
3. Microsoft 데이터 과학 Virtual Machine을 만드는 데 사용되는 마법사에는 이 그림의 오른쪽에 열거된 **4단계** 각각에 대한 **입력**이 필요합니다. 다음은 이러한 각 단계를 구성하는 데 필요한 입력입니다.
   
   1. **기본 사항**
      
      1. **이름**: 만들려는 데이터 과학 서버 이름
      2. **VM 디스크 유형**: SSD 또는 HDD 중 선택합니다. GPU(NC 시리즈)의 경우 **HDD**를 디스크 유형으로 선택합니다. 
      3. **사용자 이름**: 관리자 계정 로그인 ID
      4. **암호**: 관리자 계정 암호
      5. **구독**: 둘 이상의 구독을 보유한 경우, 컴퓨터를 만들고 요금을 청구할 구독 하나를 선택합니다.
      6. **리소스 그룹**: 새 그룹을 만들거나 기존 그룹을 사용할 수 있습니다.
      7. **위치**: 가장 적합한 데이터 센터를 선택합니다. 이는 대개 대부분의 데이터가 저장되어 있거나 네트워크에 가장 빠르게 액세스하기 위해 물리적 위치와 가장 가까이 있는 데이터 센터입니다.
   2. **크기**: 기능 요구 사항과 비용 제약 조건에 부합하는 서버 유형 중 하나를 선택합니다. "모두 보기"를 선택하면 보다 다양한 VM 크기를 선택할 수 있습니다.
   3. **설정**:
      
      1. **Managed Disks 사용**: Azure가 VM용 디스크를 관리하도록 하려면 관리를 선택합니다.  그렇지 않으면 새 또는 기존 저장소 계정을 지정해야 합니다. 
      2. **기타 매개 변수**: 일반적으로 기본값을 사용합니다. 기본값이 아닌 것을 사용하려는 경우 특정 필드의 정보 링크를 가리키면 도움말을 볼 수 있습니다.
   4. **요약**: 입력한 모든 정보가 올바른지 확인하고 **만들기**를 클릭합니다. **참고**: VM은 **크기** 단계에서 선택한 서버 크기에 대한 계산 이외에 추가 요금이 발생하지 않습니다. 

> [!NOTE]
> 프로비전은 약 10-20분 정도 소요됩니다. 프로비전의 상태는 Azure 포털에 표시됩니다.
> 
> 

## <a name="how-to-access-the-microsoft-data-science-virtual-machine"></a>Microsoft 데이터 과학 Virtual Machine에 액세스하는 방법
VM이 만들어지면 이전의 **기본 사항** 섹션에서 구성한 관리자 계정 자격 증명을 사용하여 원격 데스크톱으로 액세스할 수 있습니다. 

VM이 만들어지고 프로비전되면 여기에 설치 및 구성되는 도구를 사용하여 시작할 준비가 되었습니다. 여러 도구에 대한 시작 메뉴 타일 및 데스크톱 아이콘이 있습니다. 


## <a name="tools-installed-on-the-microsoft-data-science-virtual-machine"></a>Microsoft 데이터 과학 Virtual Machine에 설치된 도구

### <a name="azure-machine-learning-workbench"></a>Azure Machine Learning Workbench

Azure Machine Learning Workbench는 데스크톱 응용 프로그램 및 명령줄 인터페이스입니다. 워크벤치에는 사용자가 데이터 준비를 수행할 때 해당 단계를 학습한 데이터 준비가 기본 제공됩니다. 생산성을 높이도록 프로젝트 관리, 실행 기록 및 노트북 통합도 제공됩니다. TensorFlow, Cognitive 도구 키트, Spark ML 및 모델 개발을 위한 scikit-learn을 비롯한 최고의 오픈 소스 프레임워크를 활용할 수 있습니다. DSVM에 Azure Machine Learning Workbench를 각 사용자의 %LOCALAPPDATA% 디렉터리에 로컬로 추출하기 위한 바탕 화면 아이콘(InstallAMLFromLocal)이 제공됩니다. Workbench를 사용해야 하는 각 사용자는 각자의 Workbench 인스턴스를 설치하기 위해 InstallAMLFromLocal 바탕 화면 아이콘을 두 번 클릭하는 일회성 작업을 수행해야 합니다. 또한 Azure Machine Learning은 %LOCALAPPDATA%\amlworkbench\python에 추출되는 사용자별 Python 환경을 만들고 사용합니다.

### <a name="microsoft-ml-server-developer-edition"></a>Microsoft ML Server 디벨로퍼 버전
분석을 위해 확장성 있는 R 또는 Python용 Microsoft 엔터프라이즈 라이브러리를 사용하려는 경우 VM에 Microsoft ML Server 디벨로퍼 버전(이전에는 Microsoft R Server로 알려져 있음)이 설치되어 있습니다. Microsoft ML Server는 R 및 Python 모두에 사용할 수 있고 광범위하게 배치할 수 있는 엔터프라이즈급 분석 플랫폼이며 확장성 있고 상업적으로 지원되며 안전합니다. ML Server는 다양한 빅 데이터 통계, 예측 모델링 및 기계 학습 기능을 지원하며 탐색, 분석, 시각화 및 모델링의 전 범위 분석을 지원합니다. Microsoft ML Server는 오픈 소스 R 및 Python을 사용하고 확장하여 R/Python 스크립트, 함수 및 CRAN/pip/Conda 패키지와 완벽하게 호환되기 때문에 엔터프라이즈 규모로 데이터를 분석할 수 있습니다. 또한 데이터의 병렬 및 청크된 처리를 추가하여 오픈 소스 R의 메모리 내 한계를 해결합니다. 이렇게 하면 사용자가 주 메모리에 맞는 것보다 훨씬 큰 데이터에서 분석을 실행할 수 있습니다.  VM에 포함된 Visual Studio Community Edition에는 R 또는 Python 작업을 위한 전체 IDE를 제공하는 Visual Studio용 R 도구 및 Visual Studio용 Python 도구 확장이 포함되어 있습니다. 또한 VM에 [RStudio](http://www.rstudio.com) 및 [PyCharm Community 버전](https://www.jetbrains.com/pycharm/)과 같은 다른 IDE도 제공됩니다. 

### <a name="python"></a>파이썬
Python을 사용하여 개발하는 경우를 위해, Anaconda Python 배포 2.7 및 3.5가 설치되었습니다. 이 배포 버전에는 약 300개의 가장 인기 있는 수학, 엔지니어링 및 데이터 분석 패키지와 함께 기본 Python이 포함되어 있습니다. Visual Studio 2015 Community 버전 또는 IDLE이나 Spyder 등의 Anaconda와 함께 제공되는 IDE 중 하나에 설치된 PTVS(Python Tools for Visual Studio)를 사용할 수 있습니다. 검색 표시줄에서 검색(**Win** + **S** 키)하여 다음 중 하나를 시작할 수 있습니다.

> [!NOTE]
> Anaconda Python 2.7 및 3.5의 Python Tools for Visual Studio를 가리키려면 각 버전에 대한 사용자 지정 환경을 만들어야 합니다. Visual Studio 2015 Community Edition에서 이러한 환경 경로를 설정하려면 **도구** -> **Python 도구** -> **Python 환경**으로 이동한 다음 **+ 사용자 지정**을 클릭합니다. 
> 
> 

Anaconda Python 2.7은 C:\Anaconda 아래에 설치되어 있으며 Anaconda Python 3.5는 c:\Anaconda\envs\py35 아래에 설치되어 있습니다. 자세한 단계는 [PTVS 설명서](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 를 참조하세요. 

### <a name="jupyter-notebook"></a>Jupyter 노트북
Anaconda 배포는 코드 및 분석을 공유하는 환경인 Jupyter 노트북도 제공됩니다. Jupyter 노트북 서버는 Python 2.7, Python 3.5, PySpark, Julia 및 R 커널로 미리 구성되었습니다. Jupyter 서버를 시작하고 브라우저를 실행하여 노트북 서버에 액세스하는 "Jupyter Notebook"이라는 바탕 화면 아이콘이 있습니다. 

> [!NOTE]
> 인증서 경고가 나타나는 경우 계속 진행하세요. 
> 
> 

Python 및 R에 몇 가지 샘플 노트북이 패키지되어 있습니다. Jupyter 노트북은 Jupyter에 액세스한 후 Microsoft ML Server, SQL Server ML Services(데이터베이스 내 분석), Python, Microsoft Cognitive 도구 키트, Tensorflow 및 기타 Azure 기술을 사용하는 방법을 보여줍니다. 이전 단계에서 만든 암호를 사용하여 Jupyter 노트북에 인증한 후에 노트북 홈 페이지에서 샘플에 대한 링크를 볼 수 있습니다. 

### <a name="visual-studio-2017-community-edition"></a>Visual Studio 2017 Community edition
VM에 설치된 Visual Studio Community edition 평가 목적이나 작은 팀에 사용할 수 있는 Microsoft의 인기 있는 IDE의 무료 버전입니다. 사용 조건은 [여기](https://www.visualstudio.com/support/legal/mt171547)에서 확인할 수 있습니다.  바탕 화면 아이콘이나 **시작** 메뉴를 두 번 클릭하여 Visual Studio를 엽니다. 또한 **Win** + **S**를 누른 후 "Visual Studio"를 입력하여 프로그램을 검색할 수도 있습니다. 여기서 C#, Python, R, node.js와 같은 언어로 된 프로젝트를 만들 수 있습니다. 또한 Azure Data Catalog, Azure HDInsight(Hadoop, Spark) 및 Azure Data Lake와 같은 Azure 서비스로 작동하기 편하게 하는 플러그 인이 설치되어 있습니다. 

> [!NOTE]
> 평가 기간이 만료되었다는 메시지가 나타날 수 있습니다. Visual Studio Community Edition에 액세스하는 데 필요한 Microsoft 계정 자격 증명을 입력하거나 무료 계정을 새로 만듭니다. 
> 
> 

### <a name="sql-server-2017-developer-edition"></a>SQL Server 2017 디벨로퍼 버전
데이터베이스 내 분석을 실행하는 ML Services가 포함된 개발자 버전의 SQL Server 2017은 R 또는 Python으로 VM에 제공됩니다. ML Services는 지능형 응용 프로그램을 개발하고 배포하기 위한 플랫폼을 제공합니다. 풍부하고 강력한 언어와 커뮤니티의 여러 패키지를 사용하여 모델을 만들고 SQL Server 데이터에 대한 예측을 생성할 수 있습니다. ML Services(데이터베이스 내)는 SQL Server 내에서 R 및 Python 언어를 모두 통합하기 때문에 데이터에 근접한 분석을 유지할 수 있습니다. 이렇게 하면 데이터 이동과 관련된 비용 및 보안 위험이 없어집니다.

> [!NOTE]
> SQL Server 디벨로퍼 버전은 개발 및 테스트 목적으로만 사용할 수 있습니다. 프로덕션에서 실행하려면 라이선스가 필요합니다. 
> 
> 

**SQL Server Management Studio**를 시작하여 SQL Server에 액세스할 수 있습니다. 사용 중인 VM 이름이 서버 이름으로 사용됩니다. Windows의 관리자 권한으로 로그인할 때 Windows 인증을 사용합니다. SQL Server Management Studio에서 다른 사용자를 만들고, 데이터베이스를 만들며, 데이터를 가져오고, SQL 쿼리를 실행할 수 있습니다. 

SQL ML Services를 사용하여 데이터베이스 내 분석을 사용하도록 설정하려면 서버 관리자 권한으로 로그인한 후에 SQL Server Management Studio에서 일회성 작업으로 다음 명령을 실행합니다. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace the %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
몇 개의 Azure 도구가 VM에 설치됩니다.

* 바탕 화면에 Azure SDK 설명서에 액세스하는 바로 가기가 있습니다. 
* **AzCopy**: Microsoft Azure Storage 계정 내부/외부로 데이터를 이동시키는 데 사용합니다. 사용법을 보려면 명령 프롬프트에 **Azcopy** 를 입력합니다. 
* **Microsoft Azure Storage Explorer**: Azure Storage 계정 내에 저장한 개체를 검색하고, Azure Storage 내부/외부로 데이터를 전송하는 데 사용합니다. 검색에 **Storage Explorer** 를 입력하거나 Windows 시작 메뉴에서 찾은 후 이 도구에 액세스할 수 있습니다. 
* **Adlcopy**: Azure Data Lake로 데이터를 이동하는 데 사용합니다. 사용법을 보려면 명령 프롬프트에 **adlcopy** 를 입력하면 됩니다. 
* **dtui**: 클라우드의 NoSQL 데이터베이스인 Azure Cosmos DB로 데이터를 이동하거나 그 반대로 이동하는 데 사용됩니다. 명령 프롬프트에 **dtui** 를 입력하면 됩니다. 
* **Azure Data Factory Integration Runtime**: 온-프레미스 데이터 원본과 클라우드 간에 데이터를 이동할 수 있도록 합니다. Azure Data Factory와 같은 도구 내에서 사용됩니다. 
* **Microsoft Azure Powershell**: VM에도 설치된 Powershell 스크립트 언어의 Azure 리소스를 관리하는 데 사용되는 도구입니다. 

### <a name="power-bi"></a>Power BI
대시보드와 멋진 시각화를 구축할 수 있도록 **Power BI Desktop** 이 설치되어 있습니다. 이 도구를 사용하여 여러 원본에서 데이터를 추출하고, 대시보드 및 보고서를 작성하며, 클라우드에 게시합니다. 자세한 내용은 [Power BI](http://powerbi.microsoft.com) 사이트를 참조하세요. 시작 메뉴에서 Power BI 데스크톱을 찾을 수 있습니다. 

> [!NOTE]
> Power BI에 액세스하기 위해서는 Office 365 계정이 필요합니다. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>추가 Microsoft 개발 도구
[**Microsoft 웹 플랫폼 설치 관리자**](https://www.microsoft.com/web/downloads/platform.aspx)는 다른 Microsoft 개발 도구를 검색하고 다운로드하는 데 사용할 수 있습니다. 또한 Microsoft 데이터 과학 Virtual Machine 데스크톱에서 제공되는 도구에 대한 바로 가기도 있습니다.  

## <a name="important-directories-on-the-vm"></a>VM의 중요 디렉터리
| 항목 | 디렉터리 |
| --- | --- |
| Jupyter Notebook 서버 구성 |C:\ProgramData\jupyter |
| Jupyter Notebook 예제 홈 디렉터리 |c:\dsvm\notebooks |
| 다른 샘플 |c:\dsvm\samples |
| Anaconda(기본값: Python 2.7) |c:\Anaconda |
| Anaconda Python 3.5 환경 |c:\Anaconda\envs\py35 |
| Microsoft ML Server 독립 실행형 Python  | C:\Program Files\Microsoft\ML Server\PYTHON_SERVER |
| 기본 R 인스턴스(ML Server 독립 실행형) |C:\Program Files\Microsoft\ML Server\R_SERVER |
| SQL ML Services 데이터베이스 내 인스턴스 디렉터리 |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER |
| Azure Machine Learning Workbench(사용자 단위) | %localappdata%\amlworkbench | 
| 기타 도구 |c:\dsvm\tools |

> [!NOTE]
> 1.5.0(2016년 9월 3일 이전) 이전에 만든 Microsoft 데이터 과학 Virtual Machine 인스턴스는 이전 표에 지정된 디렉터리 구조와는 약간 다른 디렉터리 구조를 사용합니다. 
> 
> 

## <a name="next-steps"></a>다음 단계
학습 및 탐색을 계속하려면 다음 단계는 다음과 같습니다. 

* 시작 메뉴를 클릭하여 메뉴에 나열된 도구를 확인하여 데이터 과학 VM에 다양한 데이터 과학 도구를 탐색합니다.
* Azure Machine Learning Services 및 Workbench에 대해 자세히 알아보려면 [빠른 시작 및 자습서 페이지](https://docs.microsoft.com/azure/machine-learning/preview/)를 참조하세요. 
* 엔터프라이즈 규모로 데이터 분석을 지원하는 R의 RevoScaleR 라이브러리를 사용하는 샘플을 보려면 **C:\Program Files\Microsoft\ML Server\R_SERVER\library\RevoScaleR\demoScripts**로 이동하세요.  
* 문서 참조: [데이터 과학 Virtual Machine으로 할 수 있는 10가지 일](http://aka.ms/dsvmtenthings)
* 체계적으로 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)를 사용하여 종단 간 분석 솔루션을 구축하는 방법을 알아봅니다.
* Azure의 Azure Machine Learning 및 관련 데이터 서비스를 사용하는 기계 학습 및 데이터 분석 샘플을 보려면 [Azure AI 갤러리](http://gallery.cortanaintelligence.com)를 방문하세요. 또한 가상 머신의 **시작** 메뉴 및 데스크톱에 이 갤러리에 대한 아이콘을 제공합니다.

