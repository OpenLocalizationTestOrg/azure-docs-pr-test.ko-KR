---
title: "aaaTen 수행할 수 있는 작업에 hello 데이터 과학 가상 컴퓨터 | Microsoft Docs"
description: "Hello 데이터 과학 가상 컴퓨터에서 다양 한 데이터 탐색 및 모델링 작업을 수행 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Hello 데이터 과학 가상 컴퓨터에서 수행할 수 있는 10 개의 작업
Microsoft 데이터 과학 가상 컴퓨터 (DSVM) hello tooperform 하면 다양 한 데이터 탐색 및 모델링 태스크 수 있는 강력한 데이터 과학 개발 환경입니다. hello 환경 되어 이미 작성 되 고 번들로 묶인 여러 인기 있는 데이터와 분석 수 있는 도구를 쉽게 tooget 시작 신속 하 게 온-프레미스, 클라우드 또는 하이브리드에 대 한 분석 배포 합니다. hello DSVM 여러 Azure 서비스와 긴밀 하 게 작동 하 고 수 tooread 되어 azure, Azure SQL 데이터 웨어하우스, Azure 데이터 레이크, Azure 저장소 또는 Azure Cosmos DB에 이미 저장 된 데이터를 처리 합니다. 또한 Azure 기계 학습 및 Azure Data Factory와 같은 기타 분석 도구를 활용할 수 있습니다.

이 문서에서 우리 방법을 안내 하 toouse 프로그램 DSVM tooperform 다양 한 데이터 과학 작업 및 다른 Azure 서비스와 상호 작용 합니다. 다음은 hello DSVM에서 수행할 수 있는 hello 기능 중 일부입니다.

1. 데이터를 탐색 하 고 Microsoft R Server Python을 사용 하 여 DSVM hello에 로컬로 모델을 개발
2. Jupyter 노트북 tooexperiment 확장성과 성능을 위한 설계 하는 R의 enterprise 준비 버전 Python 2, Python 3 Microsoft R을 사용 하 여 브라우저에서 데이터와 함께 사용 하 여
3. 클라이언트 응용 프로그램이 간단한 웹 서비스 인터페이스를 사용하여 모델에 액세스할 수 있도록 Azure 기계 학습에서 R 및 Python을 사용하여 구축된 모델 운영
4. Azure Portal 또는 Powershell을 사용하여 Azure 리소스 관리
5. Azure File Storage를 DSVM에 탑재 가능한 드라이브로 만들어 저장소 공간을 확장하고 전체 팀에서 대규모 데이터 집합/코드 공유
6. GitHub를 사용 하 여 팀과 함께 코드를 공유 하 고 hello 사전 설치 된 Git 클라이언트-Git Bash Git GUI를 사용 하 여 저장소 액세스 키를 누릅니다.
7. Azure Blob Storage, Azure Data Lake, Azure HDInsight(Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse, 데이터베이스 등의 다양한 Azure 데이터 및 분석 서비스에 액세스
8. 보고서 및 hello DSVM hello에 미리 설치 된 Power BI Desktop을 사용 하 여 대시보드를 빌드하고 hello 클라우드에 배포 합니다
9. 동적으로 확장 하는 프로젝트에 필요한 프로그램 DSVM toomeet
10. 가상 컴퓨터에 추가 도구 설치   

> [!NOTE]
> 다양 한 hello 추가 데이터 저장소 및 분석에에서 나열 된 서비스가이 문서에 대 한 추가 사용 요금이 부과 됩니다. Toohello를 참조 하십시오 [Azure 가격](https://azure.microsoft.com/pricing/) 페이지 참조 합니다.
> 
> 

**필수 구성 요소**

* Azure 구독이 필요합니다. [여기](https://azure.microsoft.com/free/)서 평가판에 등록할 수 있습니다.
* Hello Azure 포털에서 데이터 과학 가상 컴퓨터 프로 비전에 대 한 지침은 [가상 컴퓨터를 만드는](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)합니다.

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Microsoft R 서버 또는 Python을 사용하여 데이터 탐색 및 모델 개발
R 및 Python toodo과 같은 언어 데이터 분석 hello DSVM의 오른쪽에 사용할 수 있습니다.

R에 대 한 "Revolution R Enterprise 8.0" 이라는 hello 시작 메뉴 또는 hello 바탕 화면에서 찾을 수 있는 IDE를 사용할 수 있습니다. Microsoft는 hello Open 소스/CRAN R tooenable 확장 가능한 분석 워크 로드와 hello 기능 tooanalyze 데이터 청크 분할된 병렬 분석을 수행 하 여 허용 된 hello 메모리 크기 보다 큰 맨 위에 추가 라이브러리를 제공 합니다. [RStudio](https://www.rstudio.com/products/rstudio-desktop/)와 같은 선택으로 R IDE를 설치할 수도 있습니다.

Python에 대 한 사전 설치 된 Visual Studio PTVS () 확장에 대 한 Python Tools hello에 Visual Studio Community Edition 등의 IDE를 사용할 수 있습니다. 기본적으로 기본 Python 2.7만(SciKit, Pandas 같은 분석 라이브러리 없이) PTVS에 구성됩니다. 순서 tooenable Anaconda Python 2.7 및 3.5 toodo hello 다음이 필요합니다.

* 너무 이동 하 여 각 버전에 대 한 사용자 지정 환경을 만들**도구** -> **Python Tools** -> **Python 환경** 클릭 한 다음 " **+ 사용자 지정**에서"hello Visual Studio 2015 Community Edition
* 대 한 설명을 지정 하 고 hello 환경으로 접두사 경로 설정할 *c:\anaconda* Anaconda Python 2.7 또는 *c:\anaconda\envs\py35* Anaconda Python 3.5에 대 한
* 클릭 **자동 검색** 차례로 **적용** toosave hello 환경입니다.

다음은 Visual Studio에서 처럼 보이지만 어떤 hello 사용자 지정 환경을 설치 합니다.

![PTVS 설치](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Hello 참조 [PTVS 설명서](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 방법에 대 한 자세한 내용은 toocreate Python 환경입니다.

이제 새 Python 프로젝트 toocreate를 설정 됩니다. 너무 이동**파일** -> **새로** -> **프로젝트** -> **Python** 의 hello 유형 선택 Python 응용 프로그램을 작성 하는입니다. Hello Python 환경 버전에 대 한 hello 현재 프로젝트 toohello 원하는 (Anaconda 2.7 또는 3.5)을 설정할 수 있습니다: 마우스 오른쪽 단추로 클릭 hello **Python 환경**선택, **추가/제거 Python 환경**, 및 그런 다음 select hello hello 프로젝트와 함께 환경 tooassociate를 원하는입니다. PTVS hello 제품에서 작업 하는 방법에 대 한 자세한 정보를 찾을 수 [설명서](https://github.com/Microsoft/PTVS/wiki) 페이지.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Jupyter 노트북 tooexplore와 모델을 Python 또는 R 데이터 사용
hello Jupyter 노트북 데이터 탐색 및 모델링에 대 한 브라우저 기반 "IDE를"를 제공 하는 강력한 환경입니다. Jupyter 노트북에서 Python 2, 3 Python 또는 R (오픈 소스 및 Microsoft R Server hello)를 사용할 수 있습니다.

hello 시작 메뉴 아이콘에서 클릭 toolaunch hello Jupyter 노트북 바탕 화면 아이콘 이라는 / **Jupyter 노트북**합니다. Hello DSVM에서 찾아볼 수도 있습니다 너무 "https://localhost:9999 /" tooaccess hello Jupiter 전자 필기장 합니다. 암호를 요청 하기 hello에 제공 된 지침을 사용 하 여 ***어떻게 toocreate Jupyter 노트북 서버 hello에 강력한 암호를*** hello 섹션 [프로 비전 hello Microsoft 데이터 과학 가상 컴퓨터](machine-learning-data-science-provision-vm.md)항목 toocreate 강력한 암호 tooaccess hello Jupyter 노트북 합니다. 

Hello 노트북을 연 후 DSVM hello에 패키지 되는 몇 가지 예제 전자 필기장 포함 된 디렉터리를 볼 수 있습니다. 이제 다음을 수행할 수 있습니다.

* hello 노트북 toosee hello 코드에서 클릭 합니다.
* **SHIFT-ENTER**를 눌러 각 셀 실행
* 클릭 하 여 hello 전체 전자 필기장 실행 **셀** -> **실행**
* hello Jupyter 아이콘 (왼쪽된 상단 모서리)를 클릭 하 고 다음을 클릭 하 여 새 전자 필기장 만들 **새로** 에 있는 단추 오른쪽 hello와 다음 hello 노트북 언어 (커널 라고도 함)을 선택 합니다.   

> [!NOTE]
> 현재 Python 2.7 지원, Python 3.5 및 오른쪽 hello R 커널 오픈 소스 R 뿐만 아니라 hello 엔터프라이즈에서 프로그래밍을 지원 확장 가능한 Microsoft R Server.   
> 
> 

Hello 노트북에 있는 경우 데이터를 탐색 하 hello 모델을 작성을 사용자가 선택한 라이브러리를 사용 하 여 hello 모델을 테스트할 수 있습니다.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. R 또는 Python을 사용하여 모델을 구축하고 Azure 기계 학습을 사용하여 운영
모델 hello 다음 단계는 일반적으로 toodeploy 작성 하 고 유효성을 검사 했으면 프로덕션 환경에 해당 합니다. 그러면 클라이언트 응용 프로그램 tooinvoke hello 모델 예측이 실시간으로 또는 일괄 처리 모드 별로 있습니다. Azure 기계 학습 Python 또는 R에서 생성 된 모델로 메커니즘 toooperationalize를 제공 합니다.

Azure 기계 학습에서 모델을 운용 클라이언트 toomake REST 호출 입력된 매개 변수를 전달 하는 출력으로 hello 모델에서 예측을 얻을 수 있는 웹 서비스 노출 됩니다.   

> [!NOTE]
> 등록 하지 않은 아직 Azure 기계 학습, 무료 작업 영역 또는 표준 작업 영역 hello를 방문 하 여 얻을 수 [Azure 기계 학습 스튜디오](https://studio.azureml.net/) 클릭 하 고 홈 페이지에서 "시작"입니다.   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Python 모델 구축 및 운영
Hello SciKit 배우기 라이브러리를 사용 하는 간단한 모델을 작성 하는 Python Jupyter 노트북에서 개발 된 코드의 코드 조각은 다음과 같습니다.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

hello toodeploy python 모델 tooAzure을 함수로 기계 학습 래핑하고 hello 예측 hello 모델의 사용 방법과 Azure 컴퓨터를 의미 하는 hello 사전 설치 된 Azure 기계 학습 python 라이브러리에서 제공 하는 특성으로 데코 레이트 학습 작업 영역 ID, API 키 및 hello 입력과 매개 변수를 반환 합니다.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

클라이언트 호출 toohello 웹 서비스가 사용할 수 있습니다. Hello REST API 요청을 생성 하는 편리한 래퍼 있습니다. 샘플 코드 tooconsume hello 웹 서비스는 다음과 같습니다.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> hello Azure 기계 학습 라이브러리는 Python 2.7에서 현재 지원만.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>R 모델 구축 및 운영
비슷한 toohow Python에 대 한 완료 하는 방식으로 또는 다른 위치에서 Azure 기계 학습 hello 데이터 과학 가상 컴퓨터에 기본 제공 R 모델을 배포할 수 있습니다. 그녀의 hello 단계:

* 작업 영역 ID와 인증 토큰 hello 아래의 코드 예제와 같이 settings.json 파일 tooprovide를 만듭니다.
* hello 모델의 예측 함수에 대 한 래퍼를 작성 합니다.
* 호출 ```publishWebService``` hello 함수 래퍼에 Azure 기계 학습 라이브러리 toopass hello에 있습니다.  

Hello 절차 및 코드 조각 수를 사용 하는 tooset 수, 빌드, 게시 및을 웹 서비스로 Azure 기계 학습에서 모델을 사용 하는 다음과 같습니다.

#### <a name="setup"></a>설정
1. 입력 하 여 hello 컴퓨터 학습 R 패키지 설치 ```install.packages("AzureML")``` Revolution R Enterprise 8.0 IDE 또는 R IDE에 있습니다.
2. [여기](https://cran.r-project.org/bin/windows/Rtools/)에서 RTools를 다운로드합니다. Hello zip hello 경로 (및 명명 된 zip.exe)의 유틸리티 toooperationalize R 패키지에 필요한 기계 학습 합니다.
3. 라는 디렉터리를 settings.json 파일을 만듭니다 ```.azureml``` 홈 디렉터리에서 Azure 기계 학습 작업 영역에서 hello 매개 변수를 입력 하 고 있습니다.

settings.json 파일 구조:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>R에서 모델을 구축하고 Azure Machine Learning에 게시
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Azure 기계 학습에서 배포 된 hello 모델 사용
클라이언트 응용 프로그램에서 tooconsume hello 모델을 사용 하 여 hello hello Azure 기계 학습 라이브러리 toolook hello를 사용 하 여 이름 웹 서비스를 게시 `services` API 호출 toodetermine hello 끝점입니다. Hello 호출 하면 다음 `consume` 작동 하 고 hello 데이터 프레임 toobe 예측에 전달 합니다.
hello 코드 다음은 Azure 기계 학습 웹 서비스로 게시 사용 되는 tooconsume hello 모델입니다.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Hello Azure 컴퓨터 학습 R 라이브러리에 대 한 자세한 정보를 찾을 수 [여기](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf)합니다.

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Azure 포털 또는 Powershell을 사용하여 Azure 리소스 관리
hello DSVM 뿐만 아니라 있습니다 toobuild 분석 솔루션에 로컬로 hello 가상 컴퓨터 뿐만 아니라 있습니다 있습니다 tooaccess Microsoft Azure 클라우드 서비스입니다. Azure는 DSVM에서 관리 및 액세스할 수 있는 여러 가지 계산, 저장소, 데이터 분석 서비스 및 기타 서비스를 제공합니다.

tooadminister 브라우저 및 지점 toothe 사용할 수 있습니다 하 여 Azure 구독 및 클라우드 리소스 [Azure 포털](https://portal.azure.com)합니다. Azure 구독 및 리소스 스크립트를 통해 Azure Powershell tooadminister를 사용할 수도 있습니다.
Hello 바탕 화면에서 바로 가기를에서 Azure Powershell을 실행 하거나 hello에서 "Microsoft Azure Powershell" 라는 메뉴를 시작할 수 있습니다. Windows Powershell 스크립트를 사용하여 Azure 구독 및 리소스를 관리하는 방법에 대한 자세한 내용은 [Microsoft Azure Powershell 설명서](../powershell-azure-resource-manager.md) 를 참조하세요.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. 공유 파일 시스템으로 저장소 공간 확장
데이터 과학자는 큰 데이터 집합, 코드 또는 기타 리소스 hello 팀 내에서 공유할 수 있습니다. hello 자체 DSVM 약 70 g B의 사용 가능한 공간에 있습니다. tooextend 사용할 수 있습니다 프로그램 저장소 hello Azure 파일 서비스 및 DSVM hello에 탑재 하거나 REST API를 통해 액세스 합니다.   

> [!NOTE]
> hello Azure 파일 서비스 공유의 hello 최대 공간 5TB 이며 개별 파일 크기 제한은 1TB입니다.   
> 
> 

Azure Powershell toocreate Azure 파일 서비스 공유를 사용할 수 있습니다. Azure PowerShell toocreate Azure 파일 서비스 공유에서 hello 스크립트 toorun 다음과 같습니다.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Azure 파일 공유를 만들었으니 이제 Azure의 모든 가상 컴퓨터에 파일을 마운트할 수 있습니다. 해당 hello VM 전송 요금이 hello 저장소 계정 tooavoid 대기 시간 및 데이터와 동일한 Azure 데이터 센터에는 것이 좋습니다. Azure Powershell에서 실행할 수 있는 DSVM hello에 hello 명령을 toomount hello 드라이브는 다음과 같습니다.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


이제 hello VM의 모든 기본 드라이브와 마찬가지로이 드라이브를 액세스할 수 있습니다.

## <a name="6-share-code-with-your-team-using-github"></a>6. GitHub를 사용하여 팀과 코드 공유
GitHub는 hello 개발자 커뮤니티에서 공유 하는 다양 한 기술을 사용 하 여 다양 한 도구에 대 한 많은 샘플 코드와 소스를 찾을 수 있는 코드 리포지토리입니다. Git를 사용 하 여 hello hello 코드 파일의 기술 tootrack와 저장소 버전으로 합니다. GitHub는 플랫폼 이기도 팀의 공유 코드 및 설명서 리포지토리 toostore 직접 만들 수 있는 버전 제어 및 구현도 컨트롤 액세스 tooview를가지고 있고 코드를 제공 합니다. Hello를 방문 하십시오 [GitHub 도움말 페이지](https://help.github.com/) Git를 사용 하 여 대 한 자세한 내용은 합니다. Hello 방법으로 toocollaborate 중 하나로 GitHub를 사용 하 여 팀과 함께 지정, hello 커뮤니티에서 개발 된 코드를 사용 하 여 및 코드 백 toohello 커뮤니티 기여 합니다.

hello DSVM 이미가 작동 하는 클라이언트 도구와 함께 로드 둘 다 잘 GUI tooaccess GitHub 리포지토리도 명령줄 Git 및 GitHub와 hello 명령줄 도구 toowork Git Bash 라고 합니다. Hello DSVM에 설치 된 visual Studio는 hello Git 확장이 있습니다. Hello 시작 메뉴 및 바탕 화면 hello에 이러한 도구에 대 한 시작 아이콘을 찾을 수 있습니다.

toodownload 코드 hello를 사용 하면 GitHub 리포지토리에서 ```git clone``` 명령입니다. 예를 들어 hello 현재 디렉터리에 Microsoft에서 게시 toodownload 데이터 과학 리포지토리 실행할 수 있습니다에 있는 경우 다음 명령을 hello ```git-bash```합니다.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Visual Studio에서 할 수 있는 동일한 복제 작업이 hello 합니다. 다음 스크린 샷에서 hello Visual Studio에서 Git 및 GitHub tooaccess 도구 하는 방법을 보여 줍니다.

![Visual Studio의 Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Git toowork github.com에 사용할 수 있는 몇 가지 리소스에서 GitHub 리포지토리에 사용에 대 한 자세한 내용은 찾을 수 있습니다. hello [치트 시트](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) 유용한 참조 됩니다.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. 다양한 Azure 데이터 및 분석 서비스에 액세스
### <a name="azure-blob"></a>Azure Blob
Azure Blob은 크고 작은 데이터를 위한 경제적이면서 안정적인 클라우드 저장소입니다. 에 대해 알아보겠습니다 어떻게 데이터 tooAzure Blob 및 Azure Blob에 저장 된 액세스 데이터를 이동할 수 있습니다.

**필수 요소**

* **[Azure 포털](https://portal.azure.com)에서 고유한 Azure Blob 저장소 계정을 만듭니다.**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* 찾을 수 있으며 해당 hello 사전 설치 명령줄 AzCopy 도구 확인 ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```합니다. 이 도구를 실행할 때 hello 디렉터리 포함 hello azcopy.exe tooyour PATH 환경 변수 tooavoid 입력 hello 전체 명령 경로 추가할 수 있습니다. AzCopy tool에 대 한 자세한 정보에 대 한 참조 하십시오 너무[AzCopy 설명서](../storage/common/storage-use-azcopy.md)
* Hello Azure 저장소 탐색기 도구를 시작 합니다. 이 도구는 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)에서 다운로드할 수 있습니다. 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**VM tooAzure Blob에서에서 데이터 이동: AzCopy**

로컬 파일 및 blob 저장소 간에 데이터를 toomove, 명령줄에서 AzCopy를 사용할 수 있습니다 또는 PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

대체 **C:\myfolder** 파일에 저장 된 toohello 경로 **mystorageaccount** tooyour blob 저장소 계정 이름 **mycontainer** toohello 컨테이너 이름 **저장소 계정 키** tooyour blob 저장소 액세스 키입니다. 저장소 계정 자격 증명은 [Azure 포털](https://portal.azure.com)에서 찾을 수 있습니다.

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

PowerShell 또는 명령 프롬프트에서 AzCopy 명령을 실행합니다. 다음은 AzCopy 명령을 사용하는 예입니다.

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



실행 된 AzCopy 명령 toocopy tooan 프로그램 파일을 참조 하는 Azure blob에에서 표시 Azure 저장소 탐색기 곧 합니다.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**VM tooAzure Blob에서에서 데이터 이동: Azure 저장소 탐색기**

Azure 저장소 탐색기를 사용 하 여 VM에서 hello 로컬 파일에서 데이터를 업로드할 수도 있습니다.

* tooupload 데이터 tooa 컨테이너, 선택 hello 대상 컨테이너와 클릭 hello **업로드** 단추.![ 저장소 탐색기에 업로드](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Hello 클릭 **...**  hello의 오른쪽 toohello **파일** 상자 hello 파일 시스템에서 하나 또는 여러 개의 파일 tooupload를 선택 하 고 클릭 **업로드** toobegin hello 파일을 업로드 합니다.![ Tooblob 파일 업로드](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Azure Blob에서 데이터 읽기: Machine Learning 판독기 모듈**

Azure 기계 학습 스튜디오에서 사용할 수 있습니다는 **데이터 가져오기 모듈** tooread 데이터 blob에서 합니다.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Azure Blob에서 데이터 읽기: Python ODBC**

사용할 수 있습니다 **BlobService** Jupyter 노트북 또는 Python 프로그램에서 blob에서 직접 라이브러리 tooread 데이터입니다.

먼저 필요한 패키지를 가져옵니다.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

그런 다음 Azure Blob 계정 자격 증명을 연결하고 Blob에서 데이터를 읽습니다.

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

hello 데이터에서 데이터 프레임으로 읽혀집니다.

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure 데이터 레이크
빅 데이터 분석 작업용의 초대형 리포지토리인 Azure Data Lake Storage는 HDFS(Hadoop 분산 파일 시스템)와 호환됩니다. Hello Hadoop 에코 시스템 및 hello Azure Data Lake 분석 모두 작동합니다. Hello Azure Data Lake 저장소에 데이터를 이동 합니다. Azure Data Lake 분석을 사용 하 여 분석을 실행 하는 방법을 보여줍니다.

**필수 요소**

* [Azure 포털](https://portal.azure.com)에서 Azure Data Lake Analytics를 만듭니다.

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* hello **Azure 데이터 레이크 도구** 에 **Visual Studio** 이 발견 [링크](https://www.microsoft.com/download/details.aspx?id=49504) hello hello 가상 컴퓨터에 있는 Visual Studio Community Edition에 이미 설치 되어 있습니다. Visual Studio를 시작 하 고 Azure 구독에 로그인 한 후 Azure 데이터 분석 계정 및 저장소 hello Visual Studio의 왼쪽된 창에 표시 됩니다.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**VM tooData 호수에서 데이터 이동: Azure 데이터 레이크 탐색기**

사용할 수 있습니다 **Azure 데이터 레이크 탐색기** tooupload hello 로컬 파일의에서 데이터 가상 컴퓨터 tooData Lake 저장소에 있습니다.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

빌드할 수도 있습니다는 데이터 파이프라인 tooproductionize Azure 데이터 레이크에서 데이터 이동을 tooor 프로그램 hello를 사용 하 여 [Azure 데이터 Factory(ADF)](https://azure.microsoft.com/services/data-factory/)합니다. 여기서 스 toothis [문서](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) 파이프라인 tooguide hello 단계 toobuild hello 데이터 안내 합니다.

**Azure Blob tooData 레이크에서 데이터를 읽을: U-SQL**

데이터가 Azure Blob 저장소에 상주하는 경우 U SQL 쿼리를 사용하여 Azure 저장소 Blob에서 직접 데이터를 읽을 수 있습니다. U SQL 쿼리를 작성 하기 전에 blob 저장소 계정에 연결 된 Azure 데이터 레이크 tooyour 인지를 확인 합니다. 너무 이동**Azure 포털**, Azure 데이터 레이크 분석 대시보드를 찾을, 클릭 **데이터 소스 추가**, 너무 저장소 유형을 선택**Azure 저장소** Azure 저장소에 연결 계정 이름 및 키입니다. Hello 저장소 계정에 저장 된 수 tooreference hello 데이터는 합니다.

![저장소 계정 및 키 입력](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

Visual Studio에서 일부 데이터 조작, 기능 엔지니어링 및 출력 hello 결과 데이터 tooeither Azure 데이터 레이크 또는 Azure Blob 저장소를 수행 합니다 blob 저장소에서 데이터를 읽을 수 있습니다. Blob 저장소의 hello 데이터를 참조할 때 사용할 **wasb: / /**hello 데이터를 사용 하 여 Azure 데이터 레이크를 참조 하는 경우; **swbhdfs: / /**

![데이터 프레임](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Visual Studio에서 U SQL 쿼리를 수행 하는 hello를 사용할 수 있습니다.

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



쿼리는 제출 된 toohello 서버 작업의 hello 상태를 표시 하는 다이어그램 표시 됩니다.

![작업 상태 다이어그램](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Data Lake의 데이터 쿼리: U SQL**

Hello 데이터 집합은 수집 된 Azure 데이터 레이크도, 이후에 사용할 수 있습니다 [U SQL 언어](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery hello 데이터를 탐색 하 고 있습니다. U-SQL 언어 비슷한 tooT SQL 이지만 사용자 지정 된 모듈, 사용자 정의 함수 및 등 사용자가 쓸 수 있도록 C#에서 일부 기능을 결합 합니다. Hello 스크립트 hello 이전 단계에서 사용할 수 있습니다.

Hello 후 쿼리 제출 된 tooserver, tripdata_summary입니다. CSV에 곧 있습니다 **Azure 데이터 레이크 탐색기**, hello 파일을 마우스 오른쪽 단추로 클릭 하 여 hello 데이터를 미리 볼 수 있습니다.

![Azure Data Lake Explorer의 파일](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

toosee hello 파일 정보:

![파일 요약](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>HDInsight Hadoop 클러스터
Azure HDInsight는 hello 클라우드에서 Apache Hadoop, Spark, HBase, 및 Storm 관리 되는 서비스. Hello 데이터 과학 가상 컴퓨터에서 Azure HDInsight 클러스터와 쉽게 작업할 수 있습니다.

**필수 요소**

* [Azure 포털](https://portal.azure.com)에서 고유한 Azure Blob 저장소 계정을 만듭니다. 이 저장소 계정은 HDInsight 클러스터에 대 한 사용 되는 toostore 데이터입니다.

![Azure Blob Storage 계정 만들기](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* [Azure 포털](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * 만들어질 때 HDInsight 클러스터를 사용 하 여 만든 hello 저장소 계정을 연결 해야 합니다. 이 저장소 계정은 hello 클러스터 내에서 처리할 수 있는 데이터에 액세스 하기 위해 사용 됩니다.

![HDInsight 클러스터를 사용 하 여 만든 toostorage 계정 연결](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* 사용 하도록 설정 해야 **원격 액세스** hello 클러스터를 만든 후의 toohello 헤드 노드. Hello 원격 액세스 (생성 시 hello 클러스터에 대 한 지정 된 것과 다른) 여기에서 지정한 자격 증명 기억: hello 후속 프로시저에 필요 합니다.

![원격 액세스 사용](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Azure Machine Learning 작업 영역을 만듭니다. Machine Learning 실험이 이 Machine Learning 작업 영역에 저장됩니다. 다음 스크린 샷에서 hello와 같이 포털에서 강조 표시 하는 hello 옵션을 선택 합니다.

![Azure 기계 학습 작업 영역 만들기](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* 작업 영역에 대 한 hello 매개 변수를 입력 한 다음

![Machine Learning 작업 영역 매개 변수 입력](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* IPython Notebook을 사용하여 데이터를 업로드합니다. 필요한 패키지를 가져오려면 먼저 하 자격 증명에 연결 하는 db 저장소 계정의 만들기 다음 tooHDI 클러스터 데이터를 로드 합니다.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* 이 따를 수 또는 [연습](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC 택시 데이터 tooHDI 클러스터입니다. 주요 단계는 다음과 같습니다.
  
  * AzCopy: 공용 blob tooyour 로컬 폴더에서 압축 된 CSV 다운로드
  * AzCopy: 압축 푼된 CSV의 로컬 폴더 tooHDI 클러스터에서 업로드
  * Hadoop 클러스터의 헤드 노드 hello에 로그인 하 고 예비 데이터 분석을 위해 준비 합니다.

Hello 데이터 로드 tooHDI 클러스터 되 면 Azure 저장소 탐색기에서 데이터를 확인할 수 있습니다. 그리고 HDI 클러스터에서 만든 데이터베이스 nyctaxidb가 있습니다.

**데이터 탐색: Python에서 Hive 쿼리**

Hello pyodbc 패키지 tooconnect tooHadoop를 사용할 수 있으므로 hello 데이터는 Hadoop 클러스터에 클러스터와 하이브 toodo 탐색 및 기능 엔지니어링 팀을 사용 하 여 데이터베이스를 쿼리 합니다. Hello 사전 준비 단계에서 만든 hello 기존 테이블을 볼 수 있습니다.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![기존 테이블 보기](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

각 월과 hello 빈도의 레코드 수가 hello 살펴보겠습니다 기울어진 또는 hello 여행 테이블에 없습니다.

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![월별 레코드 수에 대한 도표](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![팁 빈도 도표](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

또한 픽업 위치와 dropoff 위치 간의 hello 거리를 계산 하 고 toohello 비교 수 म 여행 거리입니다.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![승차 및 하차 테이블](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![픽업/dropoff 거리 tootrip 거리의 그림](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

이제 모델링을 위한 다운샘플링(1%) 데이터 집합을 준비하겠습니다. Machine Learning 판독기 모듈에서 이 데이터를 사용할 수 있습니다.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

잠시 후 hello 데이터가 Hadoop 클러스터에서 로드를 확인할 수 있습니다.

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![데이터 테이블](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Machine Learning을 사용하여 HDI에서 데이터 읽기: 판독기 모듈**

Hello를 사용할 수 있습니다 **판독기** Hadoop 클러스터에서 tooaccess hello 데이터베이스 기계 학습 스튜디오의에서 모듈입니다. HDI 클러스터의 hello 자격 증명에 연결 하 고 Azure 저장소 계정 tooenable HDI 클러스터에 있는 데이터베이스를 사용 하 여 모델을 학습 하는 연산 컴퓨터를 빌드합니다.

![판독기 모듈 속성](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

hello 점수가 매겨진된 데이터 집합 볼 수 있습니다.

![채점된 데이터 집합 보기](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL 데이터 웨어하우스 및 데이터베이스
Azure SQL 데이터 웨어하우스는 엔터프라이즈급 SQL Server 환경의 서비스로 탄력적인 데이터 웨어하우스입니다.

이 제공 하는 hello 지침에 따라 Azure SQL 데이터 웨어하우스를 구축할 수 있습니다 [문서](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)합니다. Azure SQL 데이터 웨어하우스를 프로 비전 되 면이 사용할 수 있습니다 [연습](machine-learning-data-science-process-sqldw-walkthrough.md) toodo 데이터 업로드, 탐색 및 hello SQL 데이터 웨어하우스 내에서 데이터를 사용 하 여 모델링 합니다.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure Cosmos DB는 hello 클라우드에서 NoSQL 데이터베이스입니다. Toowork JSON 같은 문서와 함께 사용 하면 하 고 hello 문서 toostore 및 쿼리가 있습니다.

DSVM hello에서 별로 구성 요소 단계 tooaccess Azure Cosmos DB 다음 toodo hello가 필요 합니다.

1. DocumentDB Python SDK를 설치합니다(명령 프롬프트에서 ```pip install pydocumentdb``` 실행).
2. [Azure Portal](https://portal.azure.com)에서 Azure Cosmos DB 계정과 데이터베이스를 만듭니다.
3. "Azure Cosmos DB 마이그레이션 도구"를 다운로드 [여기](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) tooa 디렉터리로 추출 합니다.
4. JSON 데이터 (화산 데이터)에 저장 된 가져오기는 [공용 blob](https://cahandson.blob.core.windows.net/samples/volcano.json) Cosmos DB 다음 명령 매개 변수 toohello 마이그레이션 도구의 (dtui.exe hello Cosmos DB 마이그레이션 도구를 설치한 hello 디렉터리에서)에 있습니다. 이러한 매개 변수를 사용 하 여 hello 소스 및 대상 위치를 입력 합니다.
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

TooJupyter 및 이라는 열기 hello 노트북 hello 데이터를 가져온 후 이동할 수 있습니다 *DocumentDBSample* tooaccess DocumentDB 코드 python을 포함 하 고 몇 가지 기본적인 쿼리를 수행 합니다. Hello 서비스를 방문 하 여 자세한 Cosmos DB에 대 한 내용은 [설명서 페이지](https://docs.microsoft.com/azure/cosmos-db/)합니다.

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Hello Power BI Desktop을 사용 하 여 대시보드 및 보고서 작성
Hello Cosmos DB 예제 hello 데이터로 Power BI toogain 시각적 통찰력에서 앞에서 살펴본 hello 화산 JSON 파일을 시각화 알려 주세요. 자세한 단계 hello에서 사용할 수 있는 [Power BI 문서](../cosmos-db/powerbi-visualize.md)합니다. Hello 상위 수준 단계는 다음과 같습니다.

1. Power BI Desktop을 열고 "Get Data"를 수행합니다. 으로 hello URL 지정: https://cahandson.blob.core.windows.net/samples/volcano.json
2. 목록으로 가져온 hello JSON 레코드 나타나야 합니다.
3. Power BI 작동할 수 있도록 hello로 동일 hello 목록 tooa 테이블 변환
4. 확장 하 고 hello를 클릭 하 여 hello 열 확장 아이콘 (hello 하나 hello "왼쪽된 화살표 및 오른쪽 화살표" 아이콘이 hello hello 열의 오른쪽에 있는)
5. 위치가 "레코드" 필드인 것을 볼 수 있습니다. Hello 레코드를 확장 하 고만 hello 좌표를 선택 합니다. 좌표는 목록 열입니다.
6. 새 열을 추가 열 tooconvert hello 목록 좌표 hello 수식을 사용 하 여 hello 좌표 목록 필드에 hello 두 요소를 연결 하는 쉼표로 개별 LatLong 열으로 ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```합니다.
7. 마지막으로 hello 변환 ```Elevation``` 열 tooDecimal 및 선택 hello **닫기** 및 **적용**합니다.

붙여 넣을 수 대신 이전 단계를 코드에 사용 된 hello 단계를 스크립팅 하는 다음 hello hello 쿼리 언어로 toowrite hello 데이터 변환을 사용 하면 Power BI에서 고급 편집기입니다.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



이제 Power BI 데이터 모델에 hello 데이터 준비 되었습니다. Power BI Desktop이 다음과 같이 표시됩니다.

![Power BI 데스크톱](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

보고서 및 시각화 hello 데이터 모델을 사용 하 여 빌드를 시작할 수 있습니다. 이 hello 단계를 따르면 [Power BI 문서](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild 보고서입니다. hello 최종 결과 다음과 같은 hello 하는 보고서입니다.

![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. 동적으로 확장 하는 프로젝트에 필요한 프로그램 DSVM toomeet
프로젝트에 필요한 hello DSVM toomeet 위쪽 및 아래쪽 확장할 수 있습니다. Hello 저녁 또는 주말에 toouse hello VM 필요가 없는 경우 종료할 수 있습니다만 hello에서 VM hello [Azure 포털](https://portal.azure.com)합니다.

> [!NOTE]
> Hello VM에서 운영 체제 종료 단추 바로 hello를 사용 하는 경우 계산 비용이 발생 합니다.  
> 
> 

일부 대규모 분석 toohandle 필요 하 고 CPU 및/또는 메모리 및/또는 디스크 용량이 더 필요할 경우 다양 한 CPU 코어, 메모리 용량 및 계산 및 예산 요구를 충족 하는 디스크 형식 (솔리드 스테이트 드라이브)를 기준으로 VM 크기를 찾을 수 있습니다. hello 해당 시간당 계산 가격 책정 함께 Vm의 전체 목록에 있는 hello [Azure 가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/) 페이지.

마찬가지로, VM 처리 용량에 대 한 요구 사항에 감소 하는 경우 (예: 주요 작업 tooa Hadoop 또는 Spark 클러스터를 이동한 후), hello에서 hello 클러스터 줄일 수 [Azure 포털](https://portal.azure.com) VM의 toohello 설정을 이동 하 고 인스턴스입니다. 다음은 스크린샷입니다.

![VM 인스턴스 설정](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. 가상 컴퓨터에 추가 도구 설치
생각 되는 다양 한 hello 일반적인 데이터 분석 요구 사항 및를 절약할 수 시간 tooinstall 것을 방지 하 여 및 환경의 개별적으로 구성 되어 있는 리소스에 대해서만 지불 하면 비용을 줄일 수 tooaddress 있는 여러 가지 도구를 압축 한 했습니다. 사용 합니다.

다른 Azure 데이터를 활용할 수 있습니다 및 분석 환경에서이 문서 tooenhance 프로 파일링 분석 서비스입니다. 하지만 경우에 따라 독점적 타사 도구를 비롯한 추가 도구가 필요할 수도 있습니다. Hello 가상 컴퓨터 tooinstall 새로운 도구 필요한 모든 관리 권한이 있습니다. 또한 사전 설치되지 않은 추가 패키지를 Python 및 R에 설치할 수 있습니다. Python의 경우 ```conda``` 또는 ```pip```를 사용할 수 있습니다. R에 대 한 hello를 사용할 수 있습니다 ```install.packages()``` hello R 콘솔 hello IDE를 사용 하 고 선택 "**패키지** -> **설치 패키지...** ".

## <a name="summary"></a>요약
이들은 일부가 hello 작업 hello Microsoft 데이터 과학 가상 컴퓨터에서 수행할 수 있습니다. 작업 toomake 할 수 있는 더 많은 많으며 것 효과적인 분석 환경입니다.

