---
title: "기계 학습의 R 언어에 대 한 aaaQuickstart 자습서 | Microsoft Docs"
description: "이 R 신속 하 게 hello R 언어를 사용 하 여 Azure 기계 학습 스튜디오 toocreate 예측 솔루션으로 시작 하는 자습서 tooget 프로그래밍을 사용 합니다."
keywords: "빠른 시작, r 언어, r 프로그래밍 언어, r 프로그래밍 자습서"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Azure 기계 학습에 대 한 hello R 프로그래밍 언어에 대 한 빠른 시작 자습서

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>소개
이 빠른 시작 자습서를 사용 하면 신속 하 게 hello R 프로그래밍 언어를 사용 하 여 Azure 기계 학습 확장을 시작 합니다. 이 R 자습서 toocreate 프로그래밍, 테스트 하 고 Azure 기계 학습에서 R 코드를 실행 합니다. 자습서를 통해 작업 하는 동안 Azure 기계 학습에서 hello R 언어를 사용 하 여 완벽 한 예측 솔루션을 만들어집니다.  

Microsoft Azure 기계 학습에는 강력한 기계 학습 및 데이터 조작 모듈이 많이 포함되어 있습니다. hello 강력한 R 언어에 특별히 만들어진 분석의 hello 공통 언어 라고 설명할 수 있습니다. 다행히 오른쪽을 사용 하 여 Azure 기계 학습에서 분석 및 데이터 조작을 확장할 수 있습니다. 이 조합은 제공 hello 확장성 및 Azure 기계 학습의 배포의 용이성 hello 유연성 및 심층 분석은 R입니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>예측 및 hello 데이터 집합
예측은 널리 활용되고 매우 유용한 분석 방법입니다. 공통 최적의 재고 수준, toopredicting macroeconomic 변수 결정 계절 관련 항목에 대 한 판매 예측에서 범위를 사용 합니다. 일반적으로 예측은 시계열 모델을 통해 수행됩니다.

시계열 데이터는 hello 값 시간 인덱스를 포함할 수 있는 데이터입니다. 예를 들어 매월 또는 1 분 마다 hello 시간 인덱스 보통, 수 또는 비 정기적인 합니다. 시계열 모델은 시계열 데이터를 기반으로 합니다. hello R 프로그래밍 언어는 유연성 있는 프레임 워크 및 시계열 데이터에 대 한 광범위 한 분석을 포함합니다.

이 빠른 시작 가이드에서는 캘리포니아 유제품 생산 및 가격 데이터를 사용합니다. 이 데이터는 여러 유제품 hello 생산 및 우유 fat, 벤치 마크 물품의 hello 가격에 월별 정보를 포함 합니다.

hello 데이터는 R 스크립트와 함께이 문서에서 사용 가능 [여기에서 다운로드][download]합니다. 이 데이터를 원래 http://future.aae.wisc.edu/tab/production.html에 hello 위스콘신 대학에서에서 사용할 수 있는 정보에서 합성 됩니다.

### <a name="organization"></a>조직
Toocreate, 테스트 하 고 hello Azure 기계 학습 환경에서 분석 및 데이터 조작 R 코드를 실행 하는 방법을 배울 때 여러 단계가 진행 됩니다.  

* 먼저 hello R 언어를 사용 하 여 hello Azure 기계 학습 스튜디오 환경에서의 hello 기본 사항을 설명 합니다.
* 그런 다음 진행 하는 과정 toodiscussing hello Azure 기계 학습 환경에서 데이터, R 코드 그래픽과 대 한 I/O의 다양 한 측면입니다.
* 그런 다음 데이터 정리 및 변환에 대 한 코드를 만들어 예측 솔루션의 hello 첫 번째 부분을 만듭니다.
* 준비 된 데이터와이 데이터 집합에 있는 hello 변수의 여러 간의 hello 상관 관계에 대 한 분석을 수행 합니다.
* 마지막으로 우유 생산의 계절성 시계열 예측 모델을 만듭니다.

## <a id="mlstudio"></a>기계 학습 스튜디오에서 R 언어와 상호 작용
이 섹션에서는 R hello hello 기계 학습 스튜디오 환경에서 프로그래밍 언어와의 상호 작용의 몇 가지 기본 사항을 보여 줍니다. hello R 언어에는 강력한 도구 toocreate 사용자 지정 분석 및 데이터 조작 모듈 hello Azure 기계 학습 환경 내에서 제공합니다.

작은 규모의 RStudio toodevelop, 테스트 및 디버그 R 코드를 사용 합니다. 이 코드는 다음 잘라내기 및 붙여넣기에는 [R 스크립트 실행] [ execute-r-script] 준비 toorun 기계 학습 스튜디오의에서 모듈입니다.  

### <a name="hello-execute-r-script-module"></a>hello R 스크립트 실행 모듈
기계 학습 스튜디오에서 R 스크립트는 hello 내에서 실행 됩니다 [R 스크립트 실행] [ execute-r-script] 모듈입니다. Hello의 예로 [R 스크립트 실행] [ execute-r-script] 기계 학습 스튜디오의 모듈 그림 1에 표시 됩니다.

 ![R 프로그래밍 언어: 기계 학습 스튜디오에서 선택한 hello R 스크립트 실행 모듈][1]

*그림 1입니다. hello 기계 학습 스튜디오 환경 선택 hello R 스크립트 실행 모듈을 표시 합니다.*

Hello hello를 사용 하기 위한 hello 기계 학습 스튜디오 환경의 주요 부분 중 일부에 대해 살펴보겠습니다 tooFigure 1 참조, [R 스크립트 실행] [ execute-r-script] 모듈입니다.

* hello 실험에서 모듈 hello hello 가운데 창에 표시 됩니다.
* hello hello 오른쪽 창 위쪽 부분 창 tooview를 포함 하 고 R 스크립트를 편집 합니다.  
* hello의 일부 속성을 표시 하는 창 오른쪽의 아래쪽 hello [R 스크립트 실행][execute-r-script]합니다. 이 창의 hello 적절 한 지점을 클릭 하 여 hello 오류 및 출력 로그를 볼 수 있습니다.

여기, 물론,에서 설명할 hello [R 스크립트 실행] [ execute-r-script] hello이이 문서의 나머지 부분에 더 자세히 합니다.

복잡한 R 함수를 사용할 경우에는 RStudio에서 편집, 테스트 및 디버그하는 것이 좋습니다. 모든 소프트웨어 개발에서와 마찬가지로 코드를 점차적으로 확장하고 간단한 작은 테스트 사례에서 테스트하세요. 함수 hello의 hello R 스크립트 창에 붙여 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 이 방법을 사용 하면 tooharness 모두 hello RStudio 통합된 개발 환경 (IDE) 및 Azure 기계 학습의 hello.  

#### <a name="execute-r-code"></a>R 코드 실행
Hello의 모든 R 코드 [R 스크립트 실행] [ execute-r-script] hello를 클릭 하 여 hello 실험을 실행할 때 모듈을 실행할 **실행** 단추입니다. Hello에 확인 표시가 나타나면 실행이 완료 되었을 때 [R 스크립트 실행] [ execute-r-script] 아이콘입니다.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Azure 기계 학습용 방어 R 코딩
Azure 기계 학습을 사용하여 웹 서비스용 R 코드를 개발하는 경우 코드가 예기치 않은 데이터 입력 및 예외를 처리할 방법을 확실히 계획해야 합니다. toomaintain 명확성을 I 포함 하지 않고 거의 hello 방식으로 검사 또는 대부분의 표시 된 hello 코드 예제에서 예외 처리 합니다. 하지만 계속 진행하면서 R의 예외 처리 기능을 사용하는 몇 가지 함수 예를 제공하겠습니다.  

Hello에 나열 된 Wickham로 hello 책의 해당 섹션을 읽어 권장 R 예외 처리는 보다 완전 하 게 처리 해야 할 경우 [부록 B-추가 정보](#appendixb)합니다.

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>기계 학습 스튜디오에서 R 디버깅 및 테스트
tooreiterate, 필자 권장 테스트 및 소규모 RStudio에 대 한 R 코드를 디버깅 합니다. 그러나 hello에 대 한 R 코드 문제 아래로 tootrack 할 경우가 있습니다. [R 스크립트 실행] [ execute-r-script] 자체입니다. 또한 것이 좋습니다 toocheck에서 결과 기계 학습 스튜디오 합니다.

Hello 실행 하 고 hello Azure 기계 학습 플랫폼에서 R 코드의 출력은 주로 output.log 있습니다. 일부 추가 정보는 error.log에 표시됩니다.  

기계 학습 스튜디오에서 R 코드를 실행 하는 동안 오류가 발생, 작업의 첫 번째 과정 error.log에서 toolook 여야 합니다. 이 파일에 유용한 오류 메시지 toohelp 이해 하 고 오류를 해결 포함 될 수 있습니다. tooview error.log를 클릭 **오류 로그 보기** hello에 **속성 창** hello에 대 한 [R 스크립트 실행] [ execute-r-script] hello 오류를 포함 합니다.

예를 들어, 필자는 정의 되지 않은 변수 y에 R 코드에서 다음 hello는 [R 스크립트 실행] [ execute-r-script] 모듈:

    x <- 1.0
    z <- x + y

이 코드는 오류 조건이 발생 tooexecute를 실패 합니다. 클릭 하면 **오류 로그 보기** hello에 **속성 창** 생성 hello 그림 2에 표시 된 것으로 표시 합니다.

  ![오류 메시지 팝업][2]

*그림 2. 오류 메시지 팝업*

Toolook output.log toosee hello R 오류 메시지에 필요한 것 같습니다. Hello 클릭 [R 스크립트 실행] [ execute-r-script] hello를 클릭 하 고 **output.log 볼** hello에 대 한 항목 **속성 창** toohello 오른쪽입니다. 새 브라우저 창이 열리고 hello 다음 표시 됩니다.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

이 오류 메시지가 없는 예기치 않은 문제를 포함 하 고 명확 하 게 hello 문제를 식별 합니다.

R에서 모든 개체의 tooinspect hello 값, 이러한 값 toohello output.log 파일로 인쇄할 수 있습니다. 값은 기본적으로 개체를 검사 하는 것에 대 한 hello 규칙 대화형 R 세션에서와 같이 동일한 hello 합니다. 예를 들어 한 줄에 변수 이름을 입력 하는 경우 hello 개체의 hello 값 인쇄 toohello output.log 파일 됩니다.  

#### <a name="packages-in-machine-learning-studio"></a>기계 학습 스튜디오의 패키지
Azure 기계 학습은 350개가 넘는 사전 설치된 R 언어 패키지를 함께 제공합니다. Hello 코드 hello에 다음을 사용할 수 있습니다 [R 스크립트 실행] [ execute-r-script] 모듈 tooretrieve hello 목록이 미리 패키지를 설치 합니다.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

이 코드의 마지막 줄 hello hello 순간에 모르는 경우 계속 읽어 보십시오. Hello이이 문서의 나머지 부분에서 광범위 하 게 hello Azure 기계 학습 환경에서 R을 사용 하 여 설명 합니다.

### <a name="introduction-toorstudio"></a>소개 tooRStudio
RStudio는 r 널리 사용 되는 IDE 편집, 테스트 및 디버깅이 퀵 스타트 가이드에 사용 된 hello R 코드의 일부에 대 한 RStudio를 사용 합니다. R 코드를 테스트 및 준비 되 면 단순히 잘라내어 hello RStudio 편집기에서 기계 학습 스튜디오로 [R 스크립트 실행] [ execute-r-script] 모듈입니다.  

데스크톱 컴퓨터에 설치 된 R hello 프로그래밍 언어가 없는 경우 이렇게 하면 지금 것을 권장 합니다. 오픈 소스 R 언어의 무료 다운로드 hello 포괄적인 R 보관 네트워크 (CRAN)에서 사용할 수 있는에서 [http://www.r-project.org/](http://www.r-project.org/)합니다. Windows, Mac OS, Linux/UNIX용 다운로드가 있습니다. 주변 미러를 선택 하 고 hello 다운로드 지시를 따릅니다. 또한 CRAN에는 유용한 분석 및 데이터 조작 패키지가 풍부하게 들어 있습니다.

새 tooRStudio 인 경우에 다운로드 하 고 hello 데스크톱 버전을 설치 해야 합니다. Http://www.rstudio.com/products/RStudio/에 Windows, Mac OS 및 Linux/UNIX 용 RStudio를 다운로드 하는 hello를 찾을 수 있습니다. RStudio tooinstall 데스크톱 컴퓨터에서 제공 하는 hello 지시를 따릅니다.  

자습서 소개 tooRStudio https://support.rstudio.com/hc/sections/200107586-Using-RStudio에서 ´ ù입니다.

[부록 A][appendixa]에 RStudio 사용에 대한 추가 정보가 일부 제공됩니다.  

## <a id="scriptmodule"></a>Hello R 스크립트 실행 모듈 내부 및 외부 데이터 가져오기
이 섹션에서는 다음과 같은 작용이 hello 안팎으로 데이터를 가져오는 방법을 [R 스크립트 실행] [ execute-r-script] 모듈입니다. Toohandle 다양 한 데이터 형식을 읽는 방법 및 hello 외부로 검토할 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

이전에 다운로드 한 hello zip 파일에이 섹션에 대 한 hello 전체 코드가입니다.

### <a name="load-and-check-data-in-machine-learning-studio"></a>기계 학습 스튜디오에서 데이터 로드 및 확인
#### <a id="loading"></a>Hello 데이터 집합 로드
Hello를 로드 하 여 먼저 **csdairydata.csv** Azure 기계 학습 스튜디오로 파일입니다.

* Azure 기계 학습 스튜디오 환경을 시작합니다.
* 클릭 **+ 새로 만들기** hello에서 화면 및 선택의 왼쪽 하단 **Dataset**합니다.
* 선택 **로컬 파일에서**, 차례로 **찾아보기** tooselect hello 파일입니다.
* 선택 했는지 확인 **일반 CSV 파일 (.csv) 헤더로** hello 데이터 집합에 대 한 hello 종류로 합니다.
* Hello 확인 표시를 클릭 합니다.
* Hello를 클릭 하 여 hello 새 데이터 집합을 표시 해야 hello 데이터 집합을 업로드 후 **데이터 집합** 탭 합니다.  

#### <a name="create-an-experiment"></a>실험 만들기
기계 학습 스튜디오에서 일부 데이터를 만들었으므로 이제 해당 toocreate 실험 toodo hello 분석 해야 합니다.  

* 클릭 **+ 새로 만들기** hello에서 왼쪽 아래로 하 고 선택 **실험**, 다음 **빈 실험**합니다.
* 실험을 선택 하면 이름을 지정 하 고 hello 수정 수 **실험에 생성 중...**  hello hello 페이지 위쪽에는 제목입니다. 예를 들어 너무 변경**CA 유제품 분석**합니다.
* Hello hello 실험 페이지의 왼쪽의 확장 **저장 된 데이터 집합**, 차례로 **내 데이터 집합**합니다. Hello 표시 되어야 **cadairydata.csv** 이전에 업로드 합니다.
* 끌어서 놓기 hello **csdairydata.csv dataset** hello 실험에 있습니다.
* Hello에 **검색 항목을 실험** hello 맨 hello 왼쪽된 창에서 형식 상자 [R 스크립트 실행][execute-r-script]합니다. Hello 검색 목록에 표시 하는 hello 모듈을 표시 됩니다.
* 끌어서 놓기 hello [R 스크립트 실행] [ execute-r-script] 프로그램 팔레트에 모듈입니다.  
* Hello hello 출력에 연결 **csdairydata.csv dataset** toohello 맨 왼쪽 입력 (**Dataset1**)의 hello [R 스크립트 실행][execute-r-script]합니다.
* **저장 tooclick를 잊지 마십시오!**  

이때 실험이 그림 3과 같이 표시됩니다.

![데이터 집합 및 R 스크립트 실행 모듈을 시험해 hello CA 유제품 분석][3]

*그림 3입니다. hello CA 유제품 분석 데이터 집합 및 R 스크립트 실행 모듈으로 시험 합니다.*

#### <a name="check-on-hello-data"></a>Hello 데이터 확인
우리의 실험으로 로드 하는 hello 데이터를 살펴봅시다. Hello 실험에서 hello의 hello 출력에서 클릭 **cadairydata.csv dataset** 선택 **시각화**합니다. 그림 4와 같이 표시됩니다.  

![Hello cadairydata.csv 데이터 집합의 요약][4]

*그림 4. Hello cadairydata.csv 데이터 집합의 요약입니다.*

여기에서 많은 유용한 정보를 볼 수 있습니다. 았습니다 해당 데이터 집합의 첫 번째 여러 행을 hello 합니다. 열을 선택 하는 경우 hello 통계 섹션 hello 열에 대 한 자세한 정보를 표시 됩니다. 예를 들어 hello 기능 유형 행이 보여줍니다 Azure 기계 학습 스튜디오 할당 toohello 열 데이터 형식. 심각한 작업 toodo 시작 하기 전에 좋은 온전성 검사는 다음과 같이 신속 하 게 확인할 것입니다.

### <a name="first-r-script"></a>첫 번째 R 스크립트
Azure 기계 학습 스튜디오에서 간단한 첫 번째 R 스크립트 tooexperiment와를 만들어 보겠습니다. 만든를 있으며 hello 따라 RStudio에서 스크립트를 테스트 합니다.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

이제 tootransfer 스크립트 tooAzure 기계 학습 스튜디오가 필요합니다. 간단히 잘라내고 붙여넣을 수 있지만 이 경우에서는 R 스크립트를 zip 파일을 통해 전송하겠습니다.

### <a name="data-input-toohello-execute-r-script-module"></a>데이터 입력된 toohello R 스크립트 실행 모듈
Hello 입력 toohello에서 살펴봅시다 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 이 예제에서는 hello 캘리포니아 dairy 데이터 읽습니다 hello에 [R 스크립트 실행] [ execute-r-script] 모듈입니다.  

Hello에 대 한 입력이 세 가지 가능한 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 응용 프로그램에 따라 이러한 입력을 하나만 사용하거나 모두 사용할 수 있습니다. 또한 전혀 없는 입력을 사용 하는 완벽 하 게 합리적인 toouse R 스크립트입니다.  

Tooright 왼쪽된에서 이동 하는 이러한 입력을 살펴보겠습니다. Hello 입력 위에 커서를 놓으면 도구 설명 hello를 검토 하 여 각 hello 입력의 hello 이름을 볼 수 있습니다.  

#### <a name="script-bundle"></a>스크립트 번들
hello 스크립트 번들 입력 하면에 zip 파일의 toopass hello 내용을 [R 스크립트 실행] [ execute-r-script] 모듈입니다. Hello hello zip 파일의 명령을 tooread hello 내용을 R 코드를 다음 중 하나를 사용할 수 있습니다.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure 기계 학습 hello src 있는 것 처럼 hello zip에서 파일을 처리 / 디렉터리 tooprefix 파일에이 디렉터리 이름의 이름을 지정 해야 합니다. 예를 들어 경우 hello zip 파일이 hello `yourfile.R` 및 `yourData.rdata` hello zip hello 루트에 있는 사용자는 이러한 문제를 해결으로 `src/yourfile.R` 및 `src/yourData.rdata` 사용 하는 경우 `source` 및 `load`합니다.
> 
> 

로드 데이터 집합에서 이미 설명한 [hello 데이터 집합 로드](#loading)합니다. 만든 hello 이전 섹션에 표시 된 hello R 스크립트를 테스트 한 후 다음 hello지 않습니다.

1. Hello R 스크립트를 저장 한 합니다. R 파일입니다. 이 스크립트 파일을 "simpleplot.R"이라고 하겠습니다. Hello 내용을 다음과 같습니다.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Zip 파일을 만들고 스크립트를 이 zip 파일에 복사합니다. Windows에서는 hello 파일을 마우스 오른쪽 단추로 클릭 및 선택 수 **보내기**, 차례로 **압축 폴더**합니다. 이렇게 하면 hello "simpleplot 포함 된 zip 파일을 새로 만들어집니다. R"파일입니다.
3. 추가 파일 toohello **데이터 집합** hello 형식으로 지정 되는 기계 학습 스튜디오에서 **zip**합니다. 이제 데이터 집합에서 hello zip 파일이 표시 됩니다.
4. 끌어서 놓기 hello zip 파일에서 **데이터 집합** hello에 **기계 학습 스튜디오 캔버스**합니다.
5. Hello hello 출력에 연결 **데이터 zip** 아이콘 toohello **스크립트 번들** hello의 입력 [R 스크립트 실행] [ execute-r-script] 모듈입니다.
6. 형식 hello `source()` 함수 hello에 대 한 hello 코드 창에 zip 파일 이름으로 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 제 경우 `source("src/simpleplot.R")`를 입력합니다.  
7. 반드시 **저장**을 클릭하세요.

다음이 단계 완료 되 면 hello [R 스크립트 실행] [ execute-r-script] hello 실험 실행 될 때 모듈 hello zip 파일의 hello R 스크립트 실행 됩니다. 이때 실험이 그림 5와 같이 표시됩니다.

![압축된 R 스크립트를 사용한 실험][6]

*그림 5. 압축된 R 스크립트를 사용한 실험*

#### <a name="dataset1"></a>Dataset1
Dataset1 hello 입력을 사용 하 여 데이터 tooyour R 코드의 사각형 테이블을 전달할 수 있습니다. 이 간단한 스크립트 hello에 `maml.mapInputPort(1)` 함수 포트 1에서에서 hello 데이터를 읽습니다. 이 데이터 tooa 코드에서 변수 이름 데이터 프레임 할당 됩니다. 간단한 스크립트 코드의 첫 번째 줄 hello hello 할당을 수행합니다.

    cadairydata <- maml.mapInputPort(1)

Hello를 클릭 하 여 실험을 실행 **실행** 단추입니다. Hello 실행이 끝날 때 클릭 hello [R 스크립트 실행] [ execute-r-script] 모듈과 클릭 **출력 로그 보기** hello 속성 창에서. 새 페이지를 보여주는 hello output.log 파일의 내용을 hello 브라우저에 표시 됩니다. 스크롤할 때 표시 되어야 hello 다음과 같습니다.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

멀리 hello 아래로 페이지는 hello 다음과 유사할는 hello 열에 대 한 더 자세한 정보입니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

이러한 결과 228 관측값과 hello 데이터 프레임에서 9 열이 있는 예상 대로 대부분 합니다. Hello 열 이름, hello R 데이터 형식 및 각 열의 예제를 볼 수 있습니다.

> [!NOTE]
> 이 동일한 인쇄 출력은 hello hello의 R 장치 출력에서에서 편리 하 게 사용할 수 있는 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 다음과 같은 작용이 hello의 hello 출력 [R 스크립트 실행] [ execute-r-script] hello 다음 섹션에는 모듈입니다.  
> 
> 

#### <a name="dataset2"></a>Dataset2
hello hello Dataset2 입력의 동작은 Dataset1의 동일한 toothat입니다. 이 입력을 사용하여 두 번째 사각형의 데이터 테이블을 R 코드에 전달할 수 있습니다. 함수 hello `maml.mapInputPort(2)`, hello 인수 2는 사용 되는 toopass이이 데이터입니다.  

### <a name="execute-r-script-outputs"></a>R 스크립트 실행 출력
#### <a name="output-a-dataframe"></a>데이터 프레임 출력
Hello를 사용 하 여 hello 결과 Dataset1 포트를 통해 사각형 테이블로 R 데이터 프레임의 hello 내용을 출력할 수 `maml.mapOutputPort()` 함수입니다. 간단한 R 스크립트에서이 다음 줄 hello 하 여 수행 됩니다.

    maml.mapOutputPort('cadairydata')

실행 중인 hello 실험 한 후 hello 결과 Dataset1 출력 포트를 클릭 하 고 클릭 한 다음 **시각화**합니다. 그림 6과 같이 표시됩니다.

![hello 캘리포니아 dairy 데이터의 hello 출력의 hello 시각화][7]

*그림 6입니다. hello 캘리포니아 dairy 데이터의 hello 출력의 hello 시각화 합니다.*

이 출력이 똑같습니다 동일한 toohello 입력이 필요 합니다.  

### <a name="r-device-output"></a>R 장치 출력
hello의 장치 출력 hello [R 스크립트 실행] [ execute-r-script] 모듈 메시지와 그래픽 출력을 포함 합니다. R에서 메시지를 모두 표준 출력과 표준 오류 toohello R 장치 출력 포트로 전송 됩니다.  

R 장치 출력으로 hello 포트를 선택한 다음 클릭 tooview hello **시각화**합니다. Hello 표준 출력과 표준 오류 그림 7에 hello R 스크립트에서 보면 됩니다.

![표준 출력과 표준 오류 hello R 장치 포트에서][8]

*그림 7. 표준 출력과 표준 오류 hello R 장치 포트에서*

म 아래로 그림 8에 R 스크립트에서 hello 그래픽 출력 표시 합니다.  

![R 장치 포트 hello 그래픽 출력][9]

*그림 8. R 장치 포트 hello에서 출력 하는 그래픽입니다.*  

## <a id="filtering"></a>데이터 필터링 및 변환
이 섹션에서는 기본 데이터 필터링 및 변환 작업 hello 캘리포니아 dairy 데이터에 몇 가지를 수행 합니다. 이 섹션의 hello 끝으로 데이터 분석 모델을 작성 하는 데 적합 한 형식에 있는 됩니다.  

더욱 구체적으로 설명하자면 이 섹션에서 여러 일반적인 데이터 정리 및 변환 작업(형식 변환, 데이터 프레임 필터링, 새 계산 열 추가, 값 변환)을 수행합니다. 이 배경은 실제 문제에서 발생 하는 여러 변형이 hello로 처리 하는 데 도움이 됩니다.

이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에 사용할 수 있습니다.

### <a name="type-transformations"></a>형식 변환
Hello 캘리포니아 dairy 데이터 hello hello R 코드를 읽을 수 했으므로 [R 스크립트 실행] [ execute-r-script] 모듈 hello hello 열에는 데이터에는 의도 한 hello 유형 및 형식을 tooensure 필요 합니다.  

R은는 동적으로 형식화 된 언어는 데이터 형식에서 필요에 따라 하나의 tooanother 강제 변환 됩니다. hello 원자성 데이터 형식을 R에서 숫자, 논리 및 문자를 포함합니다. hello 요소 형식은 사용 되는 toocompactly 범주 데이터를 저장 합니다. hello 참조에서 데이터 형식에 대 한 자세한 정보를 제공 수 [부록 B-추가 읽기](#appendixb)합니다.

테이블 형식 데이터를 외부 소스에서 R로 읽을 때 항상 hello 열에서 형식으로 인해 발생 하는 것이 좋습니다 toocheck hello 합니다. 문자 형식의 열을 원하더라도 많은 경우 이 열은 요소로 표시되거나 그 반대로 요소가 문자 형식으로 표시됩니다. 그 밖의 경우 구상 중인 열은 부동 소수점 숫자가 아닌 문자 데이터, 즉 1.23이 아닌 '1.23'으로 나타내야 합니다.  

다행히 매핑이 불가능으로 쉽게 tooconvert 하나 형식 tooanother, 됩니다. 예를 들어 '네바다' 숫자 값으로 변환할 수는 없지만 tooa 요소 (범주 변수)를 변환할 수 있습니다. 또 다른 예로 숫자 1을 문자 '1'이나 요소로 변환할 수 있습니다.  

이러한 변환에 대 한 hello 구문은 간단: `as.datatype()`합니다. 이러한 형식 변환 함수 hello 다음을 포함 합니다.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Hello 데이터 종류 hello 입력의 열에서는 hello 이전 섹션에서 확인: 숫자, 'Month' 형식 문자는 hello 열을 제외한 형식의 모든 열이 있습니다. 이 tooa 요소를 변환 하 고 테스트 결과 hello 살펴보겠습니다.  

Hello scatterplot 행렬을 만들고 hello 'Month' 열 tooa 요소를 변환 하는 줄을 추가 하는 hello 줄을 삭제 했습니다. 내 실험에서 필자는 방금 잘라내기 및 붙여넣기 hello R 코드의 hello hello 코드 창에 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 도 hello zip 파일을 업데이트 하 고 tooAzure 기계 학습 스튜디오에 업로드할 수 마이그레이션하지만이 간단 합니다.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

이 코드를 실행 하 고 R 스크립트 hello에 대 한 hello 출력 로그를 살펴보겠습니다. hello hello 로그에서 관련 데이터는 그림 9에 표시 됩니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*그림 9. 계수 변수로 hello 데이터 프레임의 요약입니다.*

월에 대 한 hello 유형 이어야 이제 '**14 개 수준 w / 비율**'. 이것이 문제가 hello 연도에 12 개월만 있기 때문입니다. 형식 hello toosee을 확인할 수 있습니다에 **시각화** hello 결과 데이터 집합의 포트는 '**범주별**'.

hello 문제는 해당 hello 'Month' 열 체계적으로 코딩 되지 않았습니다. 어떤 경우에는 April라고 하고 또 어떤 경우에는 Apr로 줄여서 표시하기도 합니다. Hello 문자열 too3 문자 트리밍 하 여이 문제를 해결할 수 있습니다. 이제 코드 줄 hello hello 다음과 같이 표시 됩니다.

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Hello 실험을 다시 실행 하 고 hello 출력 로그를 봅니다. hello 예상 결과 그림 10에 표시 됩니다.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*그림 10. 올바른 요소 수준 수가 hello 데이터 프레임의 요약입니다.*

변수는 hello 원하는 12 개의 수준이 되었습니다.

### <a name="basic-data-frame-filtering"></a>기본 데이터 프레임 필터링
R 데이터 프레임은 강력한 필터링 기능을 지원합니다. 행이나 열에 논리 필터를 사용하여 데이터 집합을 하위 집합으로 만들 수 있습니다. 대부분의 경우 복잡한 필터 조건을 입력해야 합니다. 참조 하는 hello [부록 B-추가 읽기](#appendixb) 데이터 프레임을 필터링 하는 광범위 한 예제가 포함 되어 있습니다.  

이 데이터 집합에서 수행해야 하는 필터링이 하나 있습니다. Hello cadairydata 데이터 프레임의 hello 열을 보면 두 개의 불필요 한 열 표시 됩니다. hello 첫 번째 열에는 방금 매우 유용 하지 않는 행 번호를 보유 합니다. hello 두 번째 열에서 Year.Month, 중복 된 정보를 포함합니다. 쉽게 hello 다음 R 코드를 사용 하 여 이러한 열을 제외할 수 있습니다.

> [!NOTE]
> 이 섹션에서는 방금 드리도록 하겠습니다 이제 있습니다 hello hello에 추가 하 고 I 하는 추가 코드 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 각 새 줄에 추가 합니다. **전에** hello `str()` 함수입니다. 사용이 함수 tooverify 결과 Azure 기계 학습 스튜디오에서.
> 
> 

Hello 줄 toomy R 코드 hello에 다음을 추가 하려면 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

실험에서이 코드를 실행 하 고 출력 로그 hello hello 결과 확인 합니다. 이러한 결과는 그림 11에 나와 있습니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*그림 11. 제거 하는 두 개의 열이 있는 hello 데이터 프레임의 요약입니다.*

기쁘게도 Hello 예상 결과가 있습니다.

### <a name="add-a-new-column"></a>새 열 추가
시계열 모델의 toocreate 편리한 toohave hello 시계열 hello 시작 된 이후 개월 hello 포함 하는 열 수 있습니다. 'Month.Count'라는 열을 새로 만듭니다.

첫 번째 간단한 함수를 만듭니다 hello 코드를 구성 하는 toohelp `num.month()`합니다. 다음 함수 toocreate hello 데이터 프레임에서 새 열이 적용 됩니다. hello 새 코드는 다음과 같습니다.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

이제 업데이트 hello 실험을 실행 하 고 hello 결과물 로그 tooview hello를 사용 합니다. 이러한 결과는 그림 12에 나와 있습니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*그림 12. Hello 추가 열이 있는 hello 데이터 프레임의 요약입니다.*

모두 제대로 작동하는 것 같으며 Hello hello 예상 값을 가진 새 열이 데이터 프레임에 있는 합니다.

### <a name="value-transformations"></a>값 변환
이 섹션의 hello 값이 데이터 프레임의 hello 열 중 일부에 대해 몇 가지 간단한 변환을 수행 합니다. hello R 언어에는 거의 임의의 값 변환을 지원 합니다. 참조 하는 hello [부록 B-추가 정보](#appendixb) 광범위 한 예가 포함 되어 있습니다.

Hello 값이 데이터 프레임의 hello 요약에서 보면 표시 되어야 뭔가 이상 여기 합니다. 캘리포니아에서 아이스크림이 우유보다 더 많이 생산되나요? 아니요, 물론,이 인해 이해,이 팩트로 sad 수 하지 미국 toosome 아이스크림 입력. hello 단위 서로 다릅니다. hello 가격 파운드, 우유 1m 단위로 1,000 단위로 미국 파운드, 아이스크림은 US 갤런, 이며 별장 cheese 1, 000 미국 파운드 단위에서 우리는 단위에서입니다. 아이스크림 정도와 갤런 당 약 6.5 파운드 라고 가정할 경우을 활용해 서 쉽게 이들 값이 1, 000 파운드의 단위를 같은 모두에 맞게 곱하기 tooconvert hello지 않습니다.

이 예측 모델의 경우 이 데이터의 추세 및 계절성 조정을 위해 승법 모형을 사용합니다. 로그 변환을 toouse이이 과정을 단순화 하는 선형 모델을 수 있습니다. Hello 동일 함수 hello 승수 적용 되는 위치에 hello 로그 변환을 적용할 수 있습니다.

새 함수를 정의 하려면 코드 다음 hello에서 `log.transform()`, hello 숫자 값이 포함 된 toohello 행을 적용 합니다. hello R `Map()` 함수는 사용 되는 tooapply hello `log.transform()` 함수 toohello hello 데이터 프레임의 열을 선택 합니다. `Map()`너무 유사`apply()` 둘 이상의 인수 toohello 함수 목록이 수 있습니다. 승수 목록이 두 번째 인수 toohello hello를 제공 하는 참고 `log.transform()` 함수입니다. hello `na.omit()` 함수는 약간의 정리 tooensure 없으므로 누락 또는에 정의 되지 않은 값 hello 데이터 프레임으로 사용 됩니다.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Hello에는 비트 상황이 발생 하지는 `log.transform()` 함수입니다. 이 코드의 대부분을 hello 인수도 잠재적인 문제에 대 한 확인 되었거나 여전히 hello 계산 하는 동안 발생할 수 있는 예외를 처리 합니다. 이 코드의 몇 줄만 실제로 계산 hello지 않습니다.

hello 방어 프로그래밍의 hello 목표는 처리를 계속할 수 없는 단일 함수의 tooprevent hello 실패입니다. 장기 실행 분석의 갑작스런 실패는 사용자에게 상당한 불만을 초래할 수 있습니다. 이 경우 기본 반환 값을 선택 해야 하는 제한 tooavoid 손상 toodownstream 처리 합니다. 메시지 무언가 떨어졌습니다. 잘못 생성 된 tooalert 사용자 이기도 합니다.

R에서 사용 되는 toodefensive 프로그래밍 없는 경우이 모든 코드는 약간 어려울 수 있습니다. 필자는 안내 hello 주요 단계:

1. 네 개 메시지의 벡터가 정의됩니다. 이러한 메시지는이 코드에서 발생할 수 있는 hello 가능한 오류와 예외 중 일부에 대 한 사용 되는 toocommunicate 정보입니다.
2. 각각의 경우에 대해 NA 값을 반환합니다. 부작용이 더 적을 수 있는 다른 가능성이 많습니다. 예를 들어 0의 벡터 또는 원래 입력된 벡터 hello 반환할 수 I.
3. 검사는 hello 인수 toohello 함수에서 실행 됩니다. 각각의 경우에서 오류가 감지 되 면 기본값을 반환 되 고 메시지 hello에 의해 생성 되 `warning()` 함수입니다. 사용 하 고 `warning()` 대신 `stop()` hello 후자를 정확히 무엇 려 실행 종료 처럼 tooavoid 합니다. 이 코드의 경우 함수 접근 방법으로 작성하면 복잡하고 난해해 보이므로 프로시저 방식으로 작성하였습니다.
4. hello 로그 계산에 래핑됩니다.이 `tryCatch()` 를 예외 갑자기 중지 tooprocessing 발생 하지 것입니다. `tryCatch()`가 없으면 R 함수에 의해 발생한 대부분의 오류는 중지 작업을 수행하는 중지 신호가 됩니다.

실험에서이 R 코드를 실행 하 고 hello 살펴보면 hello output.log 파일에 출력을 인쇄 합니다. 그림 13에 표시 된 것 처럼 이제 hello hello 열 4 개 로그의 hello 변형 값이 표시 됩니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*그림 13. Hello 요약 hello 데이터 프레임의 값을 변환 되지 않습니다.*

변환 된 hello 값이 표시 됩니다. 이제 우유 생산이 다른 모든 유제품 생산을 훨씬 초과합니다. 현재 로그 눈금으로 보고 있다는 사실을 상기하세요.

이 시점에서 데이터가 정리되며 모델링할 준비가 됩니다. Hello 시각화 hello 결과 데이터 집합의 출력에 대 한 요약을 보면 우리의 [R 스크립트 실행] [ execute-r-script] 모듈을 나타납니다 hello 'Month' 열이 '범주' 12 고유 값으로 다시 싶었기와 마찬가지로, .

## <a id="timeseries"></a>시계열 개체 및 상관관계 분석
이 섹션에서는 몇 가지 기본 R 시간 시계열 개체를 탐색 하 고 hello 변수 중 일부는 간의 hello 상관 관계를 분석 합니다. 목표는 데이터 프레임 hello 쌍으로 된 상관 관계 정보를 포함 하에서 여러 시퀀스 번호 보다 낮은 toooutput는 합니다.

이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에입니다.

### <a name="time-series-objects-in-r"></a>R의 시계열 개체
이미 언급했듯이 시계열은 시간으로 인덱싱된 일련의 데이터 값입니다. R 시간 시계열 개체는 사용 되는 toocreate 고 hello 시간 인덱스를 관리 합니다. 여러 가지 이점을 toousing 시간 계열 개체가 있습니다. 시간 series 개체 해소 hello에서 많은 세부 사항을 hello 개체에 캡슐화 하는 hello 시간 시계열 인덱스 값을 관리 합니다. 또한 시간 series 개체 메서드 수 있도록 toouse hello 많은 시간 시계열 플롯을 모델링 등 인쇄 합니다.

hello POSIXct 시간 시계열 클래스는 일반적으로 사용 및는 비교적 간단 합니다. 이 시간 시계열 클래스에서 hello hello epoch, 1970 년 1 월 1 일 시작 시간을 측정합니다. 이 예제에서는 POSIXct 시계열 개체를 사용합니다. 널리 사용되는 다른 R 시계열 개체 클래스에는 확장 가능한 시계열인 zoo와 xts가 있습니다.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>시계열 개체 예
예제로 시작해 보겠습니다. **새** [R 스크립트 실행][execute-r-script] 모듈을 실험에 끌어다 놓습니다. Hello 기존 hello 결과 Dataset1 출력 포트에 연결 [R 스크립트 실행] [ execute-r-script] 모듈 toohello Dataset1 입력 포트의 새 hello [R 스크립트 실행] [ execute-r-script] 모듈입니다.

첫 번째 예제를 보려면 hello 했던 것 처럼 것으로 hello 예제에서 몇 가지 사항 볼 수 있는 것을 통해 진행률만 hello 증분 각 단계에서 R 코드의 줄 합니다.  

#### <a name="reading-hello-dataframe"></a>읽기 hello 데이터 프레임
첫 번째 단계로, 보겠습니다 데이터 프레임이 읽고 얻을 수 있는 예상 hello 결과 있는지 확인 합니다. hello 다음 코드 수행할지 hello 작업 합니다.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

이제 hello 실험을 실행 합니다. hello 새 R 스크립트 실행 도형의 hello 로그 그림 14과 같아야 합니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*(그림 14). Hello R 스크립트 실행 모듈의 hello 데이터 프레임의 요약입니다.*

이 데이터를 예상 하는 hello 형식 및 형식입니다. Note hello 'Month' 열은 형식 인수 및 hello 수준 수를 예상 했습니다.

#### <a name="creating-a-time-series-object"></a>시계열 개체 만들기
Tooadd 시간 시계열 개체 tooour 데이터 프레임이 필요합니다. POSIXct 클래스의 새 열을 추가 하는 hello 다음 hello 현재 코드를 바꿉니다.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

이제 hello 로그를 확인 합니다. 그림 15와 같이 표시됩니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*그림 15. 요약 시간 시계열 개체와 데이터 hello 프레임입니다.*

해당 hello 새 열이 실제로 클래스 POSIXct hello 요약에서 볼 수 있습니다.

### <a name="exploring-and-transforming-hello-data"></a>탐색 하 고 hello 데이터 변환
이 데이터 집합에 hello 변수 중 일부를 살펴보겠습니다. Scatterplot 행렬은 좋은 방법 tooproduce를 빠르게 확인 합니다. Hello 교체 중인 I `str()` hello 다음 줄으로 hello 이전 R 코드의 함수입니다.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

이 코드를 실행하고 결과를 살펴보세요. R 장치 포트 hello에 생성 된 hello 점도 그림 16과 같아야 합니다.

![선택한 변수의 산점도 행렬][17]

*그림 16. 선택한 변수의 산점도 행렬*

이러한 변수 간의 hello 관계에 있는 일부 odd-looking 구조는. 아마도이 म 하지 표준화 hello 변수 hello 팩트 및 추세 hello 데이터에서에서 발생 합니다.

### <a name="correlation-analysis"></a>상관관계 분석
tooboth 필요 tooperform 상관 관계 분석 추세를 취소 하 고 hello 변수 표준화 합니다. 단순히 사용 하 여 hello R `scale()` 모두 센터 및 변수 크기를 조정 하는 함수입니다. 이 함수가 더 빨리 실행될 수 있지만 그러나 tooshow 원하는 하면 R에서 방어 프로그래밍의 예

hello `ts.detrend()` 아래 표시 된 함수는 이러한 작업을 모두 수행 합니다. hello 다음 두 줄의 코드 hello 데이터 추세를 취소 하 고 hello 값을 표준화 합니다.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Hello에는 비트 상황이 발생 하지는 `ts.detrend()` 함수입니다. 이 코드의 대부분을 hello 인수도 잠재적인 문제에 대 한 확인 되었거나 여전히 hello 계산 하는 동안 발생할 수 있는 예외를 처리 합니다. 이 코드의 몇 줄만 실제로 계산 hello지 않습니다.

방어적 프로그램의 예는 [값 변환](#valuetransformations)에서 이미 설명했습니다. 두 계산 블록이 모두 `tryCatch()`로 래핑됩니다. 일부 오류는 감지 tooreturn hello 원래 입력된 벡터 및 다른 경우에 0으로 벡터를 반환 합니다.  

Hello 취소 추세 분석에 사용 되는 선형 회귀는 문제는 시간 시계열입니다. hello 예측자 변수 시간 시계열 개체입니다.  

한 번 `ts.detrend()` 정의 우리의 데이터 프레임에 대 한 관심의 toohello 변수에 적용 했습니다. Hello 결과 목록에서 만든 강제 변환 해야 우리 `lapply()` 를 사용 하 여 데이터 프레임 toodata `as.data.frame()`합니다. 방어 측면으로 인해 `ts.detrend()`, 오류 tooprocess hello 변수 중 하나가 되더라도 해결 hello 처리 다른 사용자입니다.  

코드의 마지막 줄 hello pairwise scatterplot를 만듭니다. Hello R 코드를 실행 한 후 hello scatterplot의 hello 결과 17 그림에에서 표시 됩니다.

![비추세화되고 표준화된 시계열의 쌍별 산점도][18]

*그림 17. 비추세화되고 표준화된 시계열의 쌍별 산점도*

이러한 결과 toothose 그림 16을 비교할 수 있습니다. Hello로 추세 제거 하 고 표준화 변수 hello는 훨씬 덜 구조 이러한 변수 간의 hello 관계를 표시 합니다.

hello 코드 toocompute hello 상관 관계 R ccf 개체로 다음과 같습니다.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

그림 18 같이 hello 로그를 생성이 코드를 실행 합니다.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*그림 18. Ccf 목록이 hello 쌍으로 된 상관 관계 분석에서 개체입니다.*

각 지연에 대해 상관관계 값이 있습니다. 이러한 상관 관계 값은 중요 한 충분히 큰 toobe입니다. 따라서 각 변수를 독립적으로 모델링할 수 있다는 결론을 얻을 수 있습니다.

### <a name="output-a-dataframe"></a>데이터 프레임 출력
R ccf 개체 목록으로 hello 쌍으로 된 상관 관계 계산가 했습니다. 이 hello 출력 포트 결과 데이터 집합의 데이터 프레임이 실제로 필요에 따라 약간의 문제가 발생 합니다. 또한 hello ccf 개체는 자체 및 원하는 hello 값만 hello hello에 hello 상관 관계가 목록의 첫 번째 요소에 다양 한 시퀀스 번호 보다 낮은 합니다.

다음 코드 추출 hello 지연 값 목록을 사용 하는 ccf 개체의 hello 목록에서 번호입니다.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

hello 첫 번째 코드 줄에는 약간 까다로울 이며 것을 이해 하는 데 일부 설명은 도움이 될 수 있습니다. Hello 다음 했습니까 hello 빌드된 프로젝트에서 작업 해야 합니다.

1. hello '**[[**'hello 인수와 함께 연산자'**1**'가 선택 되어 hello hello hello ccf 개체 목록의 첫 번째 요소에서 시퀀스 번호 보다 낮은 hello에 대 한 상관 관계의 벡터입니다.
2. hello `do.call()` 함수 hello 적용 `rbind()` hello 목록의 hello 요소를 마우스로 함수 반환 `lapply()`합니다.
3. hello `data.frame()` 함수에서 생성 하는 hello 결과 강제 변환 `do.call()` tooa 데이터 프레임입니다.

Hello 행 이름이 hello 데이터 프레임의 열에 있는 참고 합니다. Hello에서 출력 될 때 hello 행 이름을 유지 이렇게 [R 스크립트 실행][execute-r-script]합니다.

그림 19 hello 출력 하는 hello 코드 실행을 생성 할 때 I **시각화** hello hello 결과 데이터 집합 포트에 출력 합니다. hello 행 이름은 의도 한 대로 hello 첫 번째 열에 있습니다.

![Hello 상관 관계 분석에서 출력 결과][20]

*그림 19. Hello 상관 관계 분석에서 출력 된 결과입니다.*

## <a id="seasonalforecasting"></a>시계열 예: 계절별 예측
데이터 형식이 이제 분석에 적합 한 형식 및 hello 변수 간의 상관 없는 중요 한 관계는 있음을 확인 했습니다. 이제 시계열 예측 모델을 만들어 보겠습니다. 이 모델을 사용 하 여 우리 예측 캘리포니아 우유 프로덕션 hello에 대 한 12 개월의 2013.

예측 모델에는 두 가지 구성 요소, 즉 추세 구성 요소와 계절 구성 요소가 포함됩니다. hello 전체 예측은 hello 곱일이 두 구성 요소입니다. 이런 형식의 모델을 승법 모형이라고 합니다. hello는 대체 항목은 가산적 모델입니다. 이미 tractable이 분석을 낮추는 관심 있는 로그 변환 toohello 변수 적용 했습니다.

이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에입니다.

### <a name="creating-hello-dataframe-for-analysis"></a>Hello 데이터 프레임 분석을 위해 만들기
추가 하 여 시작 된 **새** [R 스크립트 실행] [ execute-r-script] 모듈 tooyour 실험 합니다. Hello 연결 **결과 데이터 집합** hello 기존 출력 [R 스크립트 실행] [ execute-r-script] 모듈 toohello **Dataset1** hello 새 모듈의 입력 합니다. hello 결과 그림 20과 비슷합니다.

![hello 추가 hello 새 R 스크립트 실행 모듈을 시험해][21]

*그림 20입니다. hello는 hello 새 R 스크립트 실행 모듈 추가 사용해 보십시오.*

으로 hello 상관 관계 분석에서는 방금 완료 해야 tooadd POSIXct 시간 시계열 개체를 지정 된 열입니다. hello 코드 다음에이 위해 됩니다.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

이 코드를 실행 하 고 hello 로그를 확인 합니다. hello 결과 그림 21 같아야 합니다.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*그림 21. Hello 데이터 프레임의 요약입니다.*

이 결과와 toostart 준비 하는 분석 합니다.

### <a name="create-a-training-dataset"></a>학습 데이터 집합 만들기
생성 된 hello 데이터 프레임으로 학습 데이터 집합 toocreate가 필요 합니다. 이 데이터 모두 포함 되며 2013 hello 연도의 마지막 12 hello 점을 제외 하 고 hello 관찰의 변수인 우리의 테스트 데이터 집합입니다. hello 다음 하위 집합 hello 데이터 프레임을 코드로 바꾸고 hello dairy 프로덕션 및 price 변수 플롯을 만듭니다. Hello 차트가 프로덕션 및 price 변수 4 개 다음 만듭니다. 익명 함수 사용 되는 toodefine 점도 대 한 일부 보완 이며 hello hello 목록이 반복 다른 두 개의 인수를 `Map()`합니다. 여기서는 For 루프가 잘 작동했겠지만 R은 함수 언어이므로 함수를 사용한 접근 방식을 보여 주고 있습니다.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

그림 22와 hello R 장치 출력에서 일련의 시계열을 그리는 hello를 생성 hello 코드를 실행 합니다. 날짜, 계열을 그릴 메서드 hello 시간의 훌륭한 장점 단위는 해당 hello 시간 축 note 합니다.

![캘리포니아 유제품 생산 및 가격 데이터의 첫 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![캘리포니아 유제품 생산 및 가격 데이터의 두 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![캘리포니아 유제품 생산 및 가격 데이터의 세 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![캘리포니아 유제품 생산 및 가격 데이터의 네 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*그림 22. 캘리포니아 유제품 생산 및 가격 데이터의 시계열 도표*

### <a name="a-trend-model"></a>추세 모델
시간 series 개체 및 hello 데이터에 살펴보고 필요를 만들었으면 tooconstruct hello 캘리포니아 우유 프로덕션 데이터에 대 한 추세 모델을 시작 하겠습니다. 시계열 회귀로 이 작업을 수행할 수 있습니다. 그러나 되기 hello 그림에서는 모델링 해 볼 필요는 기울기가 고 절편 tooaccurately 이상 hello hello 학습 데이터의 추세를 관찰 합니다.

Hello hello 데이터의 작은 규모를 매개 변수로 받아 I 됩니다 RStudio에 추세에 대 한 hello 모델을 작성 하 고 잘라내기 및 붙여넣기 hello 결과 모델 Azure 기계 학습에 합니다. RStudio는 이러한 유형의 대화형 분석에 대화형 환경을 제공합니다.

첫 번째 시도 같이 I too3 힘을 다항식 회귀를 시도 합니다. 이러한 종류의 모형을 과적합하게 하는 것은 매우 위험합니다. 따라서 것이 가장 좋은 tooavoid 상위 용어입니다. hello `I()` hello 내용의 해석을 제한 하는 함수 ('있는 그대로' hello 내용을 해석) 하 고 회귀 수식에 toowrite 문자 그대로 해석 된 함수를 허용 합니다.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Hello 다음을 생성합니다.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

P 값에서 (Pr (> | t |))는 hello 알 수 있습니다이 출력 제곱된 용어 상당한 되지 않을 수 있습니다. Hello를 사용 합니다 `update()` 삭제 hello 하 여이 모델 용어 제곱 toomodify 작동 합니다.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Hello 다음을 생성합니다.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

보기가 더 낫습니다. Hello 단어를 모두 의미가 있습니다. 그러나 hello 2e 16 값 기본 값 이며 너무 심각 하 게 수행 해야 합니다.  

온전성 테스트로 표시 된 hello 추세 곡선이 있는 hello 캘리포니아 dairy 프로덕션 데이터의 시간 시계열 그림을 만들어 보겠습니다. Hello 코드 hello Azure 기계 학습에서에서 다음을 추가 했지만 [R 스크립트 실행] [ execute-r-script] 모델 (하지 RStudio) toocreate 모델 hello 및 플롯을 확인 합니다. 그림 23에서 hello 결과가 표시 됩니다.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![추세 모델을 표시한 캘리포니아 우유 생산 데이터](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*그림 23. 추세 모델을 표시한 캘리포니아 우유 생산 데이터*

Hello 추세 모델 hello 데이터를 상당히 잘 맞는 것 같습니다. 또한 찾을 과잉 맞춤이의 toobe 증거 하나는 홀수 hello 모델 곡선의 선분 흔듭니다 등입니다.  

### <a name="seasonal-model"></a>계절 모델
손 모양에 추세 모델에서는 toopush에 및 필요 hello 계절 관련 영향을 포함 합니다. Hello 연도의 달 hello hello 선형 모델 toocapture hello-월별 효과 더미 변수로 사용 합니다. 모델로 인수 변수를 사용할 때 hello 절편 하지 계산 해야 참고 합니다. 이렇게 하지 않으면 hello 공식은 과다 하 게 지정 하 고 R 짧아집니다 면 hello 중 원하는 요인 있지만 hello 절편 용어 합니다.

Hello 사용할 수 있으므로 만족 스러운 추세 모델 `update()` 함수 tooadd hello 새 조건 toohello 기존 모델입니다. hello 업데이트 수식에서-1 hello hello 절편 용어를 삭제합니다. Hello 잠시 동안 RStudio를 계속 합니다.

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Hello 다음을 생성합니다.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

해당 hello 모델이 더 이상 절편 용어 고 12 월 중요 한 요소에 표시 합니다. 이것은 의도 했던 toosee 합니다.

Hello 계절별 모델 얼마나 잘 작동 하는 hello 캘리포니아 dairy 프로덕션 데이터 toosee의 다른 시간 시계열 그림을 만들어 보겠습니다. Hello 코드 hello Azure 기계 학습에서에서 다음을 추가 했지만 [R 스크립트 실행] [ execute-r-script] toocreate 모델 hello 및 플롯을 확인 합니다.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

그림 24 같이 hello 그림을 생성 Azure 기계 학습에서이 코드를 실행 합니다.

![계절의 영향이 포함된 캘리포니아 우유 생산 모델](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*그림 24. 계절의 영향이 포함된 캘리포니아 우유 생산 모델*

hello 적합된 한 toohello 데이터 그림 24에 표시 된 것은 아니라 높이면 서입니다. Hello 추세와 hello 계절 관련 영향 (월별 변형)을 모두 적절 한 확인합니다.

이 모델에 다른 검사 방법으로 hello 잉여를 살펴보면 죠. hello 다음 코드에서는 두 당사의 모델에서 예측된 값 hello, 계산 hello 계절 관련 모델에 대 한 hello 잉여 하 고 표시 hello 학습 데이터에 대 한 이러한 잉여 합니다.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

그림 25에서 hello 잔여 그림 표시 됩니다.

![잉여 hello 학습 데이터에 대 한 hello 계절 관련 모델의](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*그림 25. Hello 학습 데이터에 대 한 hello 계절 관련 모델의 나머지를 제공 합니다.*

이 정도의 오차는 적절해 보입니다. 이 모델에 대 한 고려 되지 않습니다는 hello 2008 2009 경기의 hello 효과 제외 하 고 특정 없는 구조는 특히 잘 합니다.

그림 25 같이 hello 점도 hello 잉여에 시간 종속적 패턴을 감지 하는 데 유용 합니다. 안녕하세요 명시적 방법을 컴퓨팅 나머지 하 고 그리는 hello 사용의 hello 그림에서 시간 순서에 hello 잉여를 배치 합니다. 경우 hello에 다른 손 I에 점으로 표시 `milk.lm$residuals`, 시간 순서로 hello 점도 않았을 것입니다.

사용할 수도 있습니다 `plot.lm()` tooproduce 일련의 진단 점도 합니다.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

이 코드는 그림 26에서 보여 주는 일련의 진단 도표를 생성합니다.

![Hello 계절 관련 모델에 대 한 진단 점도 중 첫 번째](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Hello 계절 관련 모델에 대 한 진단 점도 중 두 번째](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Hello 계절 관련 모델에 대 한 진단 점도의 3](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Hello 계절 관련 모델에 대 한 진단 점도 중 네 번째](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*그림 26. Hello 계절 관련 모델에 대 한 진단 표시합니다.*

이러한 점도 이지만에서 식별 된 몇 가지 높은 영향력 지점이 toocause 매우 중요 합니다. 또한 확인할 수 있습니다 hello 보통 Q Q 그림에서는 hello 잉여 닫기 toonormally 배포 된 경우 선형 모델에 대 한 중요 한 가정을 합니다.

### <a name="forecasting-and-model-evaluation"></a>예측 및 모델 평가
예에서 사용 하는 한 더 많은 작업 toodo toocomplete 합니다. Hello 오류 hello 실제 데이터를 비교 하 여 측정 및 toocompute 예측 필요 합니다. 이 예측 hello에 대 한 12 개월의 2013 수 있습니다. 우리는 학습 데이터 집합에 속하지 않는이 예측된 toohello 실제 데이터에 대 한 측정 하는 오류를 계산할 수 있습니다. 또한 비교할 수 있습니다 성능 hello에 학습 데이터 toohello 18 세 테스트 데이터의 12 개월입니다.  

사용 된 메트릭 개수가 시계열 모델의 toomeasure hello 성능. 경우에 hello 제곱 평균 (RMS) 오류를 사용 합니다. hello 다음 함수를 계산합니다. 두 계열 간의 hello RMS 오류입니다.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Hello와 마찬가지로 `log.transform()` 함수에서 설명한 섹션 "변환 값" hello,이 함수에서 오류 검사 및 예외 복구 코드의 많습니다. hello 원칙은 데 사용 된 동일한 hello 됩니다. hello 작업에 래핑된 두 위치에서 `tryCatch()`합니다. 첫째, 시계열 hello 되므로 exponentiated, hello 값의 hello 로그 노력입니다. 둘째, hello 실제 RMS 오류 계산 됩니다.  

함수 toomeasure hello RMS 오류로 equipped, 보겠습니다 빌드하고 hello RMS 오류를 포함 하는 데이터 프레임을 출력 합니다. 단독 hello 추세 모델에 대 한 사용 약관 계절 관련 요소로 hello 전체 모델 기능이 포함 될 합니다. hello 다음 코드는 hello 작업에서는 생성 한 hello 두 선형 모델을 사용 하 여 합니다.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

그림 27 hello 결과 데이터 집합 출력 포트에 표시 된 hello 출력을 생성이 코드를 실행 합니다.

![RMS에 대 한 오류 hello 모델 비교][26]

*그림 27. Hello 모델에 대 한 RMS 오류 비교 합니다.*

이 결과에서 추가 hello 계절 관련 요인 toohello 모델 줄어든다는 hello RMS 오류 크게 표시 됩니다. 너무 레지스터 hello 학습 데이터에 대 한 RMS hello 오류는 다소 보다 작은 hello에 대 한 예측 합니다.

## <a id="appendixa"></a>부록 a: 가이드 tooRStudio
이 부록에 제공 합니다 일부 링크 toohello hello RStudio 설명서 tooget 시작한의 주요 섹션 RStudio 매우 잘 설명 되어 있습니다.

1. 프로젝트 만들기
   
   R RStudio를 사용하여 R 코드를 프로젝트에서 구성하고 관리할 수 있습니다. 프로젝트를 사용 하 여 hello 설명서 https://support.rstudio.com/hc/articles/200526207-Using-Projects에서 찾을 수 있습니다.
   
   다음이 단계를 수행 하 고이 문서에서 hello R 코드 예제에 대 한 프로젝트를 만드는 것이 좋습니다.  
2. R 코드 편집 및 실행
   
   RStudio는 R 코드의 편집 및 실행을 위해 통합 환경을 제공합니다. 설명서는 https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code(영문)에서 찾을 수 있습니다.
3. 디버그
   
   RStudio에는 강력한 디버그 기능이 포함되어 있습니다. 이러한 기능에 대한 설명서는 https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio(영문)에서 찾을 수 있습니다.
   
   hello 중단점 문제 해결 기능 https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting에 설명 되어 있습니다.

## <a id="appendixb"></a>부록 B - 추가 정보
프로그래밍의 자습서에서는 hello 기초가이 R 항목에 대 할 toouse hello Azure 기계 학습 스튜디오를 사용 하는 R 언어입니다. R에 익숙하지 않은 경우 CRAN에서 두 가지 소개 자료를 사용할 수 있습니다.

* Emmanuel Paradis 여 초보자를 위한 R http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf에 좋은 위치 toostart입니다.  
* 소개 tooR 여 W. n입니다. Venables et. al. 이 쓴 'An Introduction to R(R에 대한 소개)'에서 더 심도있게 다루고 있으며 http://cran.r-project.org/doc/manuals/R-intro.html(영문)에서 확인할 수 있습니다.

R을 시작하는 데 도움을 되는 서적이 많이 있습니다. 몇 가지 유용한 서적은 다음과 같습니다.

* 아트의 R 프로그래밍 hello: A 둘러보기의 통계 소프트웨어 디자인 Norman Matloff 여은 R에서는 뛰어난 소개 tooprogramming  
* Paul Teetor 하 여 R Cookbook 오른쪽은 문제 및 솔루션 접근 방식 toousing를 제공합니다.  
* 'R in Action'(저자: Robert Kabacoff)(영문)도 유용한 입문서입니다. hello 도우미 빠른 R 웹 사이트는 http://www.statmethods.net/에 유용한 리소스입니다.
* Patrick Burns 하 여 R 르노는 오른쪽 hello 책에서 프로그래밍할 때 발생할 수 있는 작업은 복잡할 및 어려운 항목의 수를 처리 하는 매우 유머 책 http://www.burns-stat.com/documents/books/the-r-inferno/에서 무료로 제공 됩니다.
* R에서 고급 항목에 심층 분석 하려는 경우 살펴본 hello 책 Hadley Wickham 하 여 고급 R 합니다. 이 설명서의 온라인 버전 hello http://adv-r.had.co.nz/에서 무료로 제공 됩니다.

시계열 분석에 대 한 hello CRAN 작업 보기에서에서 R 시간 시계열 패키지의 카탈로그를 확인할 수 있습니다: http://cran.r-project.org/web/views/TimeSeries.html 합니다. 특정 시간 시계열 개체 패키지에 대 한 자세한 내용은 해당 패키지에 대 한 toohello 설명서를 참조 해야 합니다.

hello 책 Paul Cowpertwait 및 Andrew Metcalfe에서 R로 소개 시계열 시계열 분석에 대 한 소개 toousing R을 제공합니다. 많은 이론서에서 R 예제를 제공합니다.

다음은 유용한 인터넷 리소스입니다.

* DataCamp: DataCamp hello 편안 하 게 코딩 연습 및 비디오 단원 브라우저에서에서 R 보여 줍니다. Hello 최신 R 기술 및 패키지에 대 한 대화형 자습서 있습니다. Https://www.datacamp.com/courses/introduction-to-r에 hello 무료 대화형 R 자습서를 수행 합니다.
* Programiz에서 R을 시작하는 가이드 https://www.programiz.com/r-programming
* 클라크슨 대학교의 Kelly Black이 제공하는 빠른 R 자습서 http://www.cyclismo.org/tutorial/R/
* 60 개 이상의 R 리소스 http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
