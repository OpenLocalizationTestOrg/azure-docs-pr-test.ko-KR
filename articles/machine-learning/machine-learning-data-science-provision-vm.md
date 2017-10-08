---
title: "aaaProvision hello Microsoft 데이터 과학 가상 컴퓨터 | Microsoft Docs"
description: "분석 및 기계 학습을 수행하기 위해 Azure에서 데이터 과학 가상 컴퓨터 구성 및 만들기"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Hello Microsoft 데이터 과학 가상 컴퓨터를 프로 비전
hello Microsoft 데이터 과학 가상 컴퓨터는 Windows Azure 가상 컴퓨터 (VM) 이미지 사전 설치 하 고 데이터 분석 및 기계 학습에 일반적으로 사용 되는 인기 있는 여러 가지 도구를 사용 하 여 구성 합니다. hello 도구가 포함 되어 있습니다.

* Microsoft R Server Developer Edition
* Enthought Python 배포
* Jupyter Notebook(R, Python 커널 포함)
* Visual Studio Community Edition
* Power BI 데스크톱
* SQL Server 2016 Developer Edition
* 기계 학습 및 데이터 분석 도구
  * [CNTK(Computational Network Toolkit)](https://github.com/Microsoft/CNTK): Microsoft Research의 심화 학습 소프트웨어 도구 키트
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): 온라인, 해시, allreduce, 축소, learning2search, 활성 및 대화형 학습 등의 기술을 지원하는 속성 기계 학습 시스템
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): 기능이 향상된 빠르고 정확한 트리 구현을 제공하는 도구
  * [래 틀](http://rattle.togaware.com/) (tooLearn R 분석 도구를 쉽게 hello): 데이터 분석 및 기계 간편해, GUI 기반 데이터 탐색, R에서 학습 하 고 R 코드를 자동 생성 된 모델링 시작 하는 도구입니다.
  * [mxnet](https://github.com/dmlc/mxnet): 효율성과 유연성을 위해 디자인된 심층 학습 프레임워크
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): Java 형식의 시각적인 데이터 마이닝 및 기계 학습 소프트웨어.
  * [Apache Drill](https://drill.apache.org/): Hadoop, NoSQL 및 클라우드 저장소용의 스키마가 없는 SQL 쿼리 엔진.  ODBC 및 JDBC 인터페이스 tooenable PowerBI, Excel, Tableau와 같은 표준 BI 도구에서 파일 및 비 Sql 쿼리를 지원 합니다.
* Azure 기계 학습 및 기타 Azure 서비스에서 사용하기 위한 R 및 Python의 라이브러리
* Git Bash toowork GitHub, Visual Studio Team Services를 포함 하 여 소스 코드 저장소를 비롯 한 Git
* 명령 프롬프트를 통해 액세스할 수 있는 몇 가지 인기 있는 Linux 명령줄 유틸리티(awk, sed, perl, grep, find, wget, curl 등 포함)의 Windows 포트 

데이터 과학을 수행하려면 일련의 작업에 대해 다음 작업을 반복합니다.

1. 데이터 찾기, 로드 및 전처리
2. 모델 빌드 및 테스트
3. 지능형 응용 프로그램의 소비에 대 한 hello 모델 배포

데이터 과학자는 다양 한 도구 toocomplete 이러한 작업을 사용합니다. 것 수 수 시간이 많이 소요 toofind hello 적절 한 버전의 hello 소프트웨어를 다운로드 한 후 설치 합니다. hello Microsoft 데이터 과학 가상 컴퓨터는 모든 몇 가지 일반적인 도구 미리 설치 및 구성 프로 비전 할 수 있는 사용 가능한 준비 이미지를 Azure에서 제공 하 여 이러한 부담을 줄일 수 있습니다. 

hello Microsoft 데이터 과학 가상 컴퓨터 사용을 활성화 시키는 분석 프로젝트. Toowork를 R, Python, SQL 및 C#을 비롯 한 다양 한 언어에 작업에 있습니다. Visual Studio IDE toodevelop 제공 하 고 코드를 쉽게 toouse 테스트. hello hello VM에에서 포함 된 Azure SDK 있습니다 toobuild를 Microsoft의 클라우드 플랫폼에서 다양 한 서비스를 사용 하 여 응용 프로그램. 

이 데이터 과학 VM 이미지에 대한 소프트웨어 요금은 부과되지 않습니다. 만 지불 hello Azure 사용 요금에 대 한 hello 가상 컴퓨터를 프로 비전의 hello 크기에 종속 됩니다. Hello에 대 한 자세한 내용은 계산 요금 hello hello에 가격 책정 세부 정보 섹션에서에서 확인할 수 있습니다 [데이터 과학 가상 컴퓨터](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 페이지. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>다른 버전의 hello 데이터 과학 가상 컴퓨터
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) 이미지도를 사용할 수 있는 다양 한 hello와 동일한 Windows 이미지 hello과 도구입니다. [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) 이미지도 비슷한 많은 도구 및 심층 학습 프레임워크와 함께 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
Microsoft 데이터 과학 가상 컴퓨터를 만들기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**: tooobtain 하나, 참조 [가져오기 Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)합니다.
* **Azure 저장소 계정**: toocreate 하나, 참조 [Azure 저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다. 또는 hello 저장소 계정 hello toouse 기존 계정을 하지 않을 경우 hello VM을 만드는 과정의 일환으로 만들 수 있습니다.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Microsoft 데이터 과학 가상 컴퓨터 만들기
다음과 같습니다. hello 단계 toocreate hello Microsoft 데이터 과학 가상 컴퓨터의 인스턴스

1. 에 나열 된 toohello 가상 컴퓨터를 이동 [Azure 포털](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)합니다.
2. 선택 hello **만들기** 마법사에는 고려해 hello 아래쪽 toobe에 단추.![ 구성-데이터-과학-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Microsoft 데이터 과학 가상 컴퓨터 필요 hello 사용 마법사 toocreate hello **입력** 각 hello에 대 한 **5 단계** hello이이 그림의 오른쪽에 열거 합니다. Hello 필요한 입력 tooconfigure 각 단계는 다음과 같습니다.
   
   1. **기본 사항**
      
      1. **이름**: 만들려는 데이터 과학 서버 이름
      2. **사용자 이름**: 관리자 계정 로그인 ID
      3. **암호**: 관리자 계정 암호
      4. **구독**: 선택 hello는 hello 않습니다 컴퓨터가 만들어지고 비용이 청구 toobe 하나에 둘 이상의 구독이 있는 경우.
      5. **리소스 그룹**: 새 그룹을 만들거나 기존 그룹을 사용할 수 있습니다.
      6. **위치**: 가장 적합 한 선택 hello 데이터 센터입니다. 일반적으로 대부분의 데이터는 가장 빠른 네트워크 액세스에 가장 가까운 tooyour 실제 위치 또는 hello 데이터 센터를입니다.
   2. **크기**: 기능 요구 사항 및 비용 제약 조건을 충족 하는 hello 서버 유형 중 하나를 선택 합니다. "모두 보기"를 선택하면 보다 다양한 VM 크기를 선택할 수 있습니다.
   3. **설정**:
      
      1. **디스크 유형**: SSD(반도체 드라이브)를 선호하는 경우 프리미엄을 선택하고 그렇지 않은 경우 "표준"을 선택합니다.
      2. **저장소 계정**: hello에서 기존 구성을 사용 하거나 구독에서 새 Azure 저장소 계정을 만들 수 있습니다 동일한 *위치* hello에 위해서입니다 **기본 사항** hello 마법사의 단계입니다.
      3. **다른 매개 변수**: hello 기본값만 사용 하는 일반적으로 합니다. 기본이 아닌 값이 tooconsider hello 사용 하려는 경우 hello hello 특정 필드에 대 한 정보 링크를 가리키면 수 있습니다.
   4. **요약**: 입력한 모든 정보가 올바른지 확인합니다.
   5. **구입**: 클릭 **구입** toostart hello 프로 비전 합니다. 링크는 toohello 약관 hello 트랜잭션 제공 됩니다. hello VM hello에서 선택한 hello 서버 크기에 대 한 hello 계산 이외의 추가 비용이 없는 **크기** 단계입니다. 

> [!NOTE]
> hello를 프로 비전 약 10-20 분 소요 됩니다. hello를 프로 비전의 hello 상태 hello Azure 포털에 표시 됩니다.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>어떻게 tooaccess hello Microsoft 데이터 과학 가상 컴퓨터
한 번 hello VM이 생성, 하면 원격 데스크톱 hello 앞에서 구성한 hello 관리자 계정 자격 증명을 사용 하 여 **기본 사항** 섹션. 

VM을 만들고 프로 비전 설치 되 고 구성 하는 hello 도구를 사용 하 여 준비 toostart 됩니다. 시작 메뉴 타일 및 대부분의 hello 도구에 대 한 바탕 화면 아이콘 있습니다. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Toocreate Jupyter 및 시작에 대 한 강력한 암호를 노트북 서버 hello 하는 방법
기본적으로 hello Jupyter 노트북 서버 미리 구성 된 이지만 Jupyter 암호를 설정 하기 전에 hello VM에서 사용할 수 없습니다. toocreate hello 컴퓨터에 설치 하는 hello Jupyter 노트북 서버에 대 한 강력한 암호를 다음 데이터 과학 가상 컴퓨터 또는 제공 된 hello 바탕 화면 바로 가기를 두 번 클릭 하는 hello에 명령 프롬프트에서 명령이 실행된 hello 라는  **Jupyter 암호 설정 및 시작** VM 로컬 관리자 계정에서 합니다.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Hello 메시지를 수행 하 고 메시지가 표시 되 면 강력한 암호를 선택 합니다.

hello 이전 스크립트에서는 암호 해시 및 저장소에 있는 hello Jupyter 구성 파일에: **C:\ProgramData\jupyter\jupyter_notebook_config.py** hello 매개 변수 이름에서 ***c 합니다. NotebookApp.password***합니다.

또한 hello 스크립트 사용 하도록 설정 하 고 hello Jupyter 서버 hello 백그라운드에서 실행 합니다. Jupyter 서버 라고도 하는 windows 작업 hello WIndows 작업 스케줄러에서에서 만든 **Start_IPython_Notebook**합니다.  브라우저에서 hello 전자 필기장을 열기 전에 hello 암호를 설정한 후 몇 초 동안 toowait이 있을 수 있습니다. Hello 라는 아래의 단원을 참조 **Jupyter 노트북** tooaccess Jupyter 노트북 서버 hello 하는 방법에 있습니다. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Hello Microsoft 데이터 과학 가상 컴퓨터에 설치 된 도구

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
여 분석을 위해 toouse R을 원할 경우 hello VM에 설치 된 Microsoft R Server Developer edition. Microsoft R Server는 지원되고 확장 가능하며 안전한 R에 따라 광범위하게 배포 가능한 엔터프라이즈급 분석 플랫폼입니다. 다양 한 빅 데이터 통계, 예측 모델링 및 기계 학습 기능을 지 원하는 R 서버 hello의 전체 분석 범위 – 탐색, 분석, 시각화 및 모델링을 지원 합니다. 오픈 소스 R을 확장 및 사용 하 여 Microsoft R Server는 R 스크립트, 함수 및 CRAN 패키지와 엔터프라이즈 규모로 데이터 tooanalyze 완벽 하 게 호환 합니다. 또한 병렬 및 청크 분할 된 데이터의 처리를 추가 하 여 열기 소스 R의 hello 메모리 내 한계를 해결 합니다. 이렇게 하면 주 메모리에 적합 한 기능 보다 훨씬 더 큰 데이터 분석 toorun 있습니다.  VM에 오른쪽 작업 하기 위한 전체 IDE를 제공 하는 Visual Studio 확장에 대 한 hello R 도구를 포함 하는 hello에 포함 된 visual Studio Community Edition 또한 다운로드 하 고도 같은 기타 Ide를 사용 하 여 수 [RStudio](http://www.rstudio.com)합니다. 

### <a name="python"></a>Python
Python을 사용하여 개발하는 경우를 위해, Anaconda Python 배포 2.7 및 3.5가 설치되었습니다. 이 배포 hello가 포함 되어 기본 Python의 hello 가장 인기 있는 수학 엔지니어링 및 데이터 분석 패키지의 약 300 함께 합니다. 에 대 한 Visual Studio PTVS () hello Visual Studio 2015 Community edition 또는 Ide 유휴 또는 Spyder 같은 Anaconda 함께 제공 되는 hello 중 하나 내에서 설치 된 Python 도구를 사용할 수 있습니다. Hello 검색 표시줄에서 검색 하 여 다음 중 하나를 시작할 수 있습니다 (**Win** + **S** 키)입니다.

> [!NOTE]
> toopoint hello Anaconda Python 2.7에 Visual Studio 용 Python 도구 및 3.5 각 버전에 대 한 사용자 지정 환경을 toocreate 필요. tooset hello Visual Studio 2015 Community Edition에에서 이러한 환경 경로 탐색 너무**도구** -> **Python Tools** -> **Python환경** 클릭 하 고 **+ 사용자 지정**합니다. 
> 
> 

Anaconda Python 2.7은 C:\Anaconda 아래에 설치되어 있으며 Anaconda Python 3.5는 c:\Anaconda\envs\py35 아래에 설치되어 있습니다. 자세한 단계는 [PTVS 설명서](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 를 참조하세요. 

### <a name="jupyter-notebook"></a>Jupyter 노트북
Jupyter 노트북, 환경 tooshare 코드 및 분석 anaconda 배포도 제공 됩니다. Jupyter 노트북 서버는 Python 2.7, Python 3.4, Python 3.5 및 R 커널로 미리 구성되었습니다. 이름이 "Jupyter 노트북 toolaunch hello 브라우저 tooaccess 노트북 서버 hello 하는 데 사용 바탕 화면 아이콘 합니다. 또한 방문할 수 있는 원격 데스크톱을 통해 VM hello에 있는 경우 [https://localhost:9999 /](https://localhost:9999/) tooaccess hello Jupyter 노트북 서버 toohello VM에에서 기록 될 때입니다.

> [!NOTE]
> 인증서 경고가 나타나는 경우 계속 진행하세요. 
> 
> 

Python에서 여러 개의 샘플 전자 필기장 패키지로 만든 하 고 R에서 Jupyter 노트북 표시를 어떻게 hello toowork Microsoft R Server, SQL Server 2016 R Services (in-database 분석), Python, Microsoft Cognitive 도구 키트 (CNTK)에 대 한 심층 학습 및 기타 Azure 기술 tooJupyter에 로그인 합니다. 이전 단계에서 만든 hello 암호를 사용 하 여 toohello Jupyter 노트북을 인증 한 후 hello 노트북 홈 페이지에 hello 링크 toohello 샘플을 볼 수 있습니다. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition hello VM에 설치 합니다. Hello의 무료 버전 평가 목적 및 소규모 팀을 사용할 수 있는 microsoft 인기 있는 IDE. Hello 라이선스 조건을 확인할 수 있습니다 [여기](https://www.visualstudio.com/support/legal/mt171547)합니다.  Hello 바탕 화면 아이콘 또는 hello를 두 번 클릭 하 여 Visual Studio를 열고 **시작** 메뉴. 또한 **Win** + **S**를 누른 후 "Visual Studio"를 입력하여 프로그램을 검색할 수도 있습니다. 여기서 C#, Python, R, node.js와 같은 언어로 된 프로젝트를 만들 수 있습니다. 플러그 인 Azure Data Catalog, Azure HDInsight (Hadoop, Spark) 및 Azure 데이터 레이크와 같은 Azure 서비스와 편리한 toowork 있도록도 설치 됩니다. 

> [!NOTE]
> 평가 기간이 만료되었다는 메시지가 나타날 수 있습니다. Microsoft 계정 자격 증명을 입력 하거나 새 무료 계정을 tooget 액세스 toohello Visual Studio Community 버전을 만듭니다. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
R Services toorun 데이터베이스에서 분석을 SQL Server 2016의 개발자 버전 hello VM에 제공 됩니다. R 서비스는 지능형 응용 프로그램을 개발하고 배포하기 위한 플랫폼을 제공합니다. Hello 풍부 하 고 강력한 R 언어를 사용 하 여 지정 하 고 hello hello 커뮤니티 toocreate 모델에서 다 수의 패키지 및 SQL Server 데이터에 대 한 예측을 생성 합니다. SQL Server R Services (in-database) 통합 hello R 언어 분석 닫기 toohello 데이터를 유지할 수 있습니다. 이렇게 하면 hello 비용 및 데이터 이동과 연관 된 보안 위험에 없습니다.

> [!NOTE]
> hello SQL Server 2016 developer edition 개발에만 사용할 수 및 테스트 목적으로 합니다. 필요한 라이선스 toorun 프로덕션에서 합니다. 
> 
> 

시작 하 여 hello SQL server에 액세스할 수 **SQL Server Management Studio**합니다. VM 이름 hello 서버 이름으로 채워집니다. Hello Windows에 대 한 관리자 권한으로 로그인 할 때 Windows 인증을 사용 합니다. SQL Server Management Studio에서 다른 사용자를 만들고, 데이터베이스를 만들며, 데이터를 가져오고, SQL 쿼리를 실행할 수 있습니다. 

in-database tooenable 분석 hello 다음 하나로 명령을 실행 하 고 Microsoft R을 사용 하 여 hello 서버 관리자로 로그인 한 후 SQL Server management studio에서 작업 시간입니다. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
여러 Azure tools는 hello VM에 설치 됩니다.

* Hello Azure SDK 설명서가 바탕 화면 바로 가기를 tooaccess 합니다. 
* **AzCopy**: Microsoft Azure 저장소 계정 간에 toomove 데이터를 사용 합니다. toosee 사용량, 형식 **Azcopy** 에서 명령 프롬프트 toosee hello 사용 합니다. 
* **Microsoft Azure 저장소 탐색기**: toobrowse에서 Azure 저장소에 Azure 저장소 계정 및 전송 데이터 tooand 내에서 저장 한 hello 개체를 통해 사용 합니다. 입력할 수 **저장소 탐색기** 검색 또는 찾기를 hello Windows 시작 메뉴 tooaccess이이 도구입니다. 
* **Adlcopy**: toomove 데이터 tooAzure 데이터 레이크를 사용 합니다. toosee 사용량, 형식 **adlcopy** 명령 프롬프트에서 합니다. 
* **dtui**: toomove 데이터 tooand Azure Cosmos DB hello 클라우드에서 NoSQL 데이터베이스에서에서 사용 합니다. 명령 프롬프트에 **dtui** 를 입력하면 됩니다. 
* **Microsoft 데이터 관리 게이트웨이**: 온-프레미스 데이터 원본과 클라우드 간에 데이터를 이동할 수 있도록 합니다. Azure Data Factory와 같은 도구 내에서 사용됩니다. 
* **Microsoft Azure Powershell**: 사용할 수 있는 도구 tooadminister Azure 리소스에 hello Powershell 스크립트 언어 VM에도 설치 됩니다. 

### <a name="power-bi"></a>Power BI
toohelp 빌드할 대시보드와 멋진 시각화 hello **Power BI Desktop** 가 설치 되어 있습니다. 이 도구 toopull 데이터를 사용 하 여 다양 한 원본 tooauthor에서에서 대시보드 및 보고서 및 toopublish 해당 toohello 클라우드입니다. 내용은 hello를 참조 하십시오. [Power BI](http://powerbi.microsoft.com) 사이트입니다. Hello 시작 메뉴에서 Power BI desktop을 찾을 수 있습니다. 

> [!NOTE]
> Power BI는 Office 365 계정 tooaccess가 필요합니다. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>추가 Microsoft 개발 도구
hello [ **Microsoft 웹 플랫폼 설치 관리자** ](https://www.microsoft.com/web/downloads/platform.aspx) 사용된 toodiscover 수 있고 다른 Microsoft 개발 도구를 다운로드 합니다. Hello Microsoft 데이터 과학 가상 컴퓨터 바탕 화면에서 제공 되는 바로 가기 toohello 도구 이기도 합니다.  

## <a name="important-directories-on-hello-vm"></a>Hello VM에서 중요 한 디렉터리
| 항목 | 디렉터리 |
| --- | --- |
| Jupyter Notebook 서버 구성 |C:\ProgramData\jupyter |
| Jupyter Notebook 예제 홈 디렉터리 |c:\dsvm\notebooks |
| 다른 샘플 |c:\dsvm\samples |
| Anaconda(기본값: Python 2.7) |c:\Anaconda |
| Anaconda Python 3.5 환경 |c:\Anaconda\envs\py35 |
| R 서버 독립 실행형 인스턴스 디렉터리(R3.2.2 기반 기본 R 인스턴스) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| R 서버 데이터베이스 내 인스턴스 디렉터리(R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Microsoft R Open(R3.3.1) 인스턴스 디렉터리 |C:\Program Files\Microsoft\MRO-3.3.1 |
| 기타 도구 |c:\dsvm\tools |

> [!NOTE]
> Hello 테이블 앞에 지정 된 보다 약간 다른 디렉터리 구조를 사용 하는 hello (이전 2016 년 9 월 3 일) 1.5.0가 전에 만든 Microsoft 데이터 과학 가상 컴퓨터의 인스턴스. 
> 
> 

## <a name="next-steps"></a>다음 단계
학습 및 탐색 다음 몇 가지 단계 toocontinue 다음과 같습니다. 

* Hello hello를 클릭 하 여 데이터 과학 VM에서 다양 한 데이터 과학 도구 시작 메뉴 및 체크 아웃 hello 메뉴에 나열 된 hello 도구 hello를 탐색 합니다.
* 너무 이동**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** 엔터프라이즈 규모로 데이터 분석을 지 원하는 R에서 hello RevoScaleR 라이브러리를 사용 하는 샘플에 대 한 합니다.  
* Hello 문서 읽기: [hello 데이터 과학 가상 컴퓨터에서 수행할 수 있는 10 가지](http://aka.ms/dsvmtenthings)
* Toobuild 끝 tooend 분석 솔루션 체계적으로 사용 하 여 hello 하는 방법에 대해 알아봅니다 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)합니다.
* Hello 방문 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com) 컴퓨터 학습 및 데이터 분석 샘플를 사용 하 여 hello Cortana Intelligence Suite에 대 한 합니다. Hello에 아이콘 제공 되며 또한 **시작** 메뉴 및 hello 가상 컴퓨터 toothis 갤러리의 hello 데스크톱에 있습니다.

