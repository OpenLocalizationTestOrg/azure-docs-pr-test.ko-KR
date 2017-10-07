---
title: "hello Linux 데이터 과학 가상 컴퓨터에 aaaData 과학 | Microsoft Docs"
description: "방식과 tooperform 몇 가지 일반 데이터 과학 작업 Linux 데이터 과학 VM hello로 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>데이터 과학 hello Linux 데이터 과학 가상 컴퓨터에
이 연습에서는 어떻게 tooperform 몇 가지 일반 데이터 과학 작업을 Linux 데이터 과학 VM hello로 보여 줍니다. hello Linux 데이터 과학 가상 컴퓨터 (DSVM)는 일반적으로 데이터 분석 및 기계 학습에 사용 되는 도구 모음 미리 설치 되어 있는 Azure에서 제공 되는 가상 컴퓨터 이미지입니다. hello에 hello 핵심 소프트웨어 구성 요소는 항목별로 [Linux 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-linux-dsvm-intro.md) 항목입니다. hello VM 이미지를 사용 하면 쉽게 tooget tooinstall 필요 없이 데이터 과학 분 후에 수행을 시작 하 고 각 hello 도구를 개별적으로 구성 합니다. 필요한 경우 VM hello을 확장 하 고 중지할 수 없으면에서 쉽게 있습니다. 따라서 이 리소스는 탄력적이고 비용 효율적입니다.

hello이 연습에서 설명 하는 데이터 과학 작업 단계에 따라 hello hello에 설명 된 [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)합니다. 이 프로세스는 데이터 과학자 tooeffectively hello 수명 주기 지능형 응용 프로그램 빌드를 통해 협력 하 여 팀 수 있게 하는 체계적 접근 방법 toodata 과학을 제공 합니다. hello 데이터 과학 프로세스는 또한으로 수행할 수 있는 데이터 과학을 위한 반복 되는 프레임 워크를 제공 합니다.

Hello 분석 [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 이 연습에서 데이터 집합입니다. 스팸 또는 햄 (스팸 없는 의미), 표시 된 전자 메일의 집합은 또한 hello 전자 메일의 hello 내용에 대 한 일부 통계를 포함 합니다. 포함 하는 hello 통계는 한 개의 절 이지만 다음 hello에 설명 되어 있습니다.

## <a name="prerequisites"></a>필수 조건
Linux 데이터 과학 가상 컴퓨터를 사용 하려면 먼저 hello 다음이 있어야 합니다.

* **Azure 구독**. 아직 없을 경우 [지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free/)를 참조하세요.
* [**Linux 데이터 과학 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). 이 VM을 프로 비전에 대 한 정보를 참조 하십시오. [Linux 데이터 과학 가상 컴퓨터 프로 비전 hello](machine-learning-data-science-linux-dsvm-intro.md)합니다.
* [X2Go](http://wiki.x2go.org/doku.php) . **X2Go 클라이언트**설치 및 구성에 대한 자세한 내용은 [X2Go 클라이언트 설치 및 구성](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)을 참조하세요. 
* **AzureML 계정**. 아직 없는 새 하나씩 hello에 등록 한 경우 [AzureML 홈 페이지](https://studio.azureml.net/)합니다. 시작 하는 데 사용 가능한 계층 toohelp이 있습니다.

## <a name="download-hello-spambase-dataset"></a>Hello spambase 데이터 집합 다운로드
hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 데이터 집합은 상대적으로 작은 4601 예제를 포함 하는 데이터 집합이 있습니다. 이것이 보여는 hello 그대로 hello 데이터 과학 VM의 주요 기능 중 일부 유지 hello 리소스 요구 사항을 적당 한 때 편리한 크기 toouse입니다.

> [!NOTE]
> 이 연습은 D2 v2 크기의 Linux 데이터 과학 가상 컴퓨터에서 만들었습니다. 이 크기 DSVM는 hello이이 연습의 프로시저에에서 처리할 수 있습니다.
>
>

더 많은 저장 공간이 필요한 경우 추가 디스크를 만들 수 있으며 tooyour VM을 연결 합니다. 이러한 디스크 사용 영구 Azure 저장소의 데이터는 보존 hello 서버 다시 프로 비전 하는 경우에 due tooresizing 또는 종료 될 합니다. 디스크 tooadd hello 지침에 따라, tooyour VM을 연결 하 고 [디스크 tooa Linux VM 추가](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 이러한 단계는 hello DSVM hello에 이미 설치 되어 Azure 명령줄 인터페이스 (Azure CLI)를 사용 합니다. 따라서 hello VM 자체에서이 절차를 수행할 수 있습니다. 다른 옵션 tooincrease 저장소는 toouse [Azure 파일](../storage/files/storage-how-to-use-files-linux.md)합니다.

toodownload hello 데이터 터미널 윈도우를 열고이 명령을 실행 합니다.

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

hello 다운로드 한 파일이 머리글 행이 되어, 만들어야 헤더에는 다른 파일 없습니다. Hello 적절 한 헤더와 함께이 명령 toocreate 파일을 실행 합니다.

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

다음 hello hello 명령과 함께 두 개의 파일을 연결 합니다.

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

hello 데이터 집합에 각 전자 메일에서 여러 유형의 통계:

* 열 같은 ***단어\_등호\_단어*** 일치 하는 hello 전자 메일에 있는 단어의 hello 백분율을 나타내는 *단어*합니다. 예를 들어 경우 *단어\_등호\_확인* hello 전자 메일에 있는 모든 단어의 1% 된 다음에 1, *확인*합니다.
* 열 같은 ***char\_등호\_CHAR*** hello 전자 메일에 있는 모든 문자가 hello 백분율로 나타내는 *CHAR*합니다.
* ***자본\_실행\_길이\_가장 긴*** hello 가장 긴 시퀀스의 대문자로 길이입니다.
* ***자본\_실행\_길이\_평균*** hello의 대문자로 모든 시퀀스의 평균 길이입니다.
* ***자본\_실행\_길이\_총*** hello의 대문자로 모든 시퀀스의 총 길이입니다.
* ***스팸*** 여부 hello 전자 메일 스팸이 간주 되는지를 나타내는 (1 = 스팸, 0 = 스팸이 아닌).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Microsoft R Open과 hello 데이터 집합 탐색
보겠습니다 hello 데이터를 검사 하 고 몇 가지 기본 기계 학습 데이터 과학 VM와 함께 제공 되는 오른쪽 hello로 실행 [Microsoft R Open](https://mran.revolutionanalytics.com/open/) 미리 설치 되어 있습니다. hello R의이 버전에서는 다중 스레드 수학 라이브러리 더 나은 성능을 제공 단일 스레드 다양 한 버전입니다. Microsoft R Open 제공 재현 가능성 hello CRAN 패키지 저장소의 스냅숏을 사용 하 여 합니다.

hello tooget 복사본 코드 복제 hello이이 연습에서 사용 하는 샘플 **Azure-컴퓨터-학습-데이터-과학** 리포지토리를 사용 하 여 git를 hello VM 미리 설치 되어 있습니다. Hello git 명령줄에서 실행 합니다.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

터미널 창을 열고 R hello 대화형 콘솔을 통해 새 R 세션을 시작 합니다.

> [!NOTE]
> 다음 절차를 수행 하는 hello에 대 한 RStudio를 사용할 수도 있습니다. RStudio, tooinstall 터미널에서이 명령을 실행 합니다.`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

tooimport hello 데이터와 hello 환경 설정 실행 합니다.

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

각 열에 대 한 요약 통계를 toosee:

    summary(data)

에 대 한 hello 데이터의 다른 보기:

    str(data)

여기에 각 변수의 형식을 hello 및 hello 데이터 집합에 적은 수의 값을 먼저 hello 표시 합니다.

hello *스팸* 를 정수로 열 읽은 이지만 실제로 범주 변수 (또는 계수). tooset 해당 형식:

    data$spam <- as.factor(data$spam)

toodo 몇 가지 탐구 분석, 사용 하 여 hello [ggplot2](http://ggplot2.org/) 패키지 하 고, VM hello에 이미 설치 되어 R에 대 한 그래프는 인기 있는 라이브러리입니다. 참고 hello 요약 데이터에서 앞에서 표시 된 hello 주파수 hello 느낌표 문자에 요약 통계 있으며 이러한 시각화는. 다음 명령을 hello로 여기 해당 주파수를 그릴 보겠습니다.

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Hello 0 막대는 hello 점도 기울이기 이후 보겠습니다 제거:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

흥미롭게도 1보다 큰 특수한 밀도가 있습니다. 해당 데이터를 살펴보겠습니다.

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

스팸과 햄으로 분할합니다.

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

이 예제에서는 해야 사용 하면 hello toomake 비슷한 차트가 다른 열 tooexplore hello 여기에 포함 된 데이터입니다.

## <a name="train-and-test-an-ml-model"></a>ML 모델 학습 및 테스트
이제 학습 기계 학습의 두 hello 데이터 집합의 tooclassify hello 전자 메일을 모델링 하는 보겠습니다 중 하나를 포함 하는 것에 걸쳐 실행 하거나 햄 합니다. 이 섹션에서 의사 결정 트리 모델 및 임의 포리스트 모델을 학습하고 해당 예측의 정확도를 테스트합니다.

> [!NOTE]
> hello 코드 다음에 사용 되는 hello rpart (재귀 분할 및 회귀 트리) 패키지는 데이터 과학 VM hello에 이미 설치 되어 있습니다.
>
>

첫째, 학습 및 테스트 집합으로 hello 데이터 집합을 분할 해 보겠습니다.

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

한 다음 전자 메일 의사 결정 트리 tooclassify hello를 만듭니다.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Hello 결과 다음과 같습니다.

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

hello 교육에 얼마나 잘 수행 toodetermine 설정, 코드 다음 hello를 사용 하 여:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

toodetermine 얼마나 잘 hello 테스트 집합에 대해 수행 합니다.

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

임의 포리스트 모델도 살펴보겠습니다. 임의 포리스트는 다 수의 의사 결정 트리를 학습 및 hello 모드 hello 개별 의사 결정 트리의 모든 hello 분류 하는 클래스를 출력 합니다. 의사 결정 트리 모델 toooverfit 학습 데이터 집합의 hello 경향에 대 한 올바른 것으로 접근 방식 학습 더 강력한 시스템을 제공 합니다.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>모델 tooAzure ML 배포
[Azure 기계 학습 스튜디오](https://studio.azureml.net/) (AzureML)는 쉽게 toobuild를 사용 하면 예측 분석 모델을 배포 하는 클라우드 서비스입니다. AzureML의 hello 훌륭한 기능 중 하나에 모든 R 웹 서비스로 작동 하는 기능 toopublish입니다. hello AzureML R 패키지 선택 하면 배포 쉽게 toodo 우리의 R 세션에서 바로 hello DSVM 됩니다.

toodeploy hello 의사 결정 트리 코드 hello 이전 섹션에서 toosign tooAzure 기계 학습 스튜디오에에서 필요합니다. 작업 영역 ID와에 권한 부여 토큰 toosign가 필요 합니다. toofind 다음 값과 이러한 초기화 hello AzureML 변수:

선택 **설정을** hello 왼쪽 메뉴에 있습니다. **작업 영역 ID**를 적어둡니다. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

선택 **권한 부여 토큰** hello 오버 헤드 메뉴 및 메모에서 프로그램 **기본 권한 부여 토큰**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

부하 hello **AzureML** 패키지 하 고 hello DSVM에 R 세션에서의 토큰 및 작업 영역 ID 사용 하 여 hello 변수 값을 설정 합니다.

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


보겠습니다 hello 모델 toomake이 데모 쉽게 tooimplement을 단순화 합니다. Hello 의사 결정 트리 가장 가까운 toohello 루트에서 hello 세 개의 변수를 선택 하 고 이러한 3 개의 변수를 사용 하 여 새 트리를 만들 키를 누릅니다.

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

입력으로 hello 기능을 사용 하는 예측 함수 필요 하 고 반환 hello 예측된 값:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Hello predictSpam 함수 tooAzureML hello를 사용 하 여 게시 **publishWebService** 함수:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

이 함수는 hello **predictSpam** 함수, 웹 서비스를 만든 **spamWebService** 와 입력 및 출력을 정의 하 고 hello 새 끝점에 대 한 정보를 반환 합니다.

Hello 명령 사용 하 여 해당 API 끝점 및 액세스 키를 포함 하 여 웹 서비스를 게시 하는 hello의 세부 정보 보기:

    spamWebService[[2]]

tootry hello 테스트 집합의 처음 10 개 행을 hello 하는지에:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>사용 가능한 다른 도구 사용
나머지 단원 들을 hello toouse hello 도구 중 일부에 설치 하거나 Linux 데이터 과학 VM hello 하는 방법을 보여 줍니다. 다음은 도구 설명 hello 목록이입니다.

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL 및 Squirrel SQL
* SQL Server 데이터 웨어하우스

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) 는 빠르고 정확하게 향상된 트리 구현을 제공하는 도구입니다.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost는 python 또는 명령줄에서 호출할 수도 있습니다.

## <a name="python"></a>Python
Python을 사용 하 여 개발 하는 경우 hello Anaconda Python 분포 2.7 및 3.5 DSVM hello에 설치 되었습니다.

> [!NOTE]
> hello Anaconda 배포 포함 [Condas](http://conda.pydata.org/docs/index.html)이며 서로 다른 버전 및/또는 패키지에 설치 되어 있는 Python에 대 한 사용된 toocreate 환경 사용자 지정 될 수 있습니다.
>
>

보겠습니다 hello spambase 데이터 집합의 일부 읽기 및 지원 벡터 컴퓨터 scikit와 hello 전자 메일을 분류-에 대해 알아봅니다.

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake 예측:

    clf.predict(X.ix[0:20, :])

tooshow 어떻게 AzureML 끝점 toopublish 보겠습니다 더 간단한 모델 만들기 hello로 3 개의 변수 했던 이전에 hello R 모델을 게시 했습니다.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello 모델 tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> 이 작업은 python 2.7에만 사용할 수 있으며 3.5에는 아직 지원되지 않습니다. **/anaconda/bin/python2.7**을 사용하여 실행합니다.
>
>

## <a name="jupyterhub"></a>Jupyterhub
hello에 hello Anaconda 배포 DSVM Jupyter 노트북, 플랫폼 간 환경 tooshare Python, R, 또는 Julia 코드 및 분석 함께 제공 됩니다. hello Jupyter 노트북 JupyterHub 통해 액세스 됩니다. ***https://\<VM DNS 이름 또는 IP 주소\>:8000/***에서 로컬 Linux 사용자 이름 및 암호를 사용하여 로그인합니다. JupyterHub에 대한 모든 구성 파일은 **/etc/jupyterhub**디렉터리에서 찾을 수 있습니다.

여러 개의 샘플 전자 필기장 hello VM에 이미 설치 됩니다.

* Hello 참조 [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) 샘플 Python 전자 필기장에 대 한 합니다.
* 샘플 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 노트북에 대한 내용은 **IntroTutorialinR** 을 참조하세요.
* Hello 참조 [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) 다른 샘플 **Python** 노트북 합니다.

> [!NOTE]
> Julia 언어 hello hello Linux 데이터 과학 VM에 hello 명령줄에서 사용할 수도 있습니다.
>
>

## <a name="rattle"></a>Rattle
[래 틀](https://cran.r-project.org/web/packages/rattle/index.html) (tooLearn R 분석 도구를 쉽게 hello)는 데이터 마이닝을 위한 그래픽 R 도구입니다. 에 쉽게 tooload 있게 해 주는 직관적인 인터페이스가, 탐색 및 데이터를 변환 하 고 빌드 및 모델 평가 합니다.  hello 문서 [래 틀: A R에 대 한 데이터 마이닝 GUI](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) 해당 기능을 보여 주는 연습을 제공 합니다.

설치 하 고 다음 명령을 hello로 래 틀을 시작 합니다.

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> 설치는 DSVM hello에 필요 하지 않습니다. 하지만 래 틀 묻는 메시지를 tooinstall 추가 패키지를 로드할 때.
>
>

Rattle은 탭 기반 인터페이스를 사용합니다. Toosteps hello에 해당 하는 대부분의 hello 탭 [데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)와 같은 데이터를 로드 하거나 탐색 합니다. hello 데이터 과학 프로세스에서 왼쪽된 tooright hello 탭을 통해 이동합니다. 하지만 hello 마지막 탭 래 틀 여를 실행 하는 hello R 명령에 대 한 로그를 포함 합니다.

tooload hello 데이터 집합을 구성 합니다.

* tooload hello 파일, 선택 hello **데이터** 탭 한 다음
* 너무 hello 선택기를 다음 선택**Filename** 선택 **spambaseHeaders.data**합니다.
* tooload hello 파일입니다. 선택 **Execute** hello 단추의 맨 위 행에서입니다. 각 열에 입력, 대상 또는 다른 유형의 변수, 고유 값 수가 hello 여부의 확인 된 데이터 형식 등의 요약이 표시 됩니다.
* 래 틀에서 hello 제대로 식별 **스팸** hello 대상으로 하는 열입니다. 선택 hello 스팸 열에 있으면 집합 hello **대상 데이터 형식** 너무**Categoric**합니다.

tooexplore hello 데이터:

* 선택 hello **탐색** 탭 합니다.
* 클릭 **요약**, 다음 **Execute**, toosee hello 변수 형식 및 일부 요약 통계에 대 한 정보입니다.
* tooview 같은 기타 옵션을 선택 하는 다른 유형의 각 변수에 대 한 통계 **Describe** 또는 **기본 사항**합니다.

hello **탐색** 탭도 있습니다 toogenerate 통찰력 많은 표시 합니다. tooplot hello 데이터의 막대 그래프.

* **배포**를 선택합니다.
* **word_freq_remove** 및 **word_freq_you**에 대해 **히스토그램**을 선택합니다.
* **실행**을 선택합니다. 두 밀도 "제거" 보다 전자 메일에 훨씬 더 자주 나타나는 "있습니다" hello 단어 선택을 취소 하는 단일 그래프 창에 표시 하는 것이 나타납니다.

hello 상관 관계 플롯 흥미로운도 있습니다. toocreate 하나:

* 선택 **상관 관계** hello로 **형식**, 한 다음
* **실행**을 선택합니다.
* 권장 최대 변수는 40개라는 경고 메시지가 표시됩니다. 선택 **예** tooview hello 그림입니다.

시작 하는 몇 가지 흥미로운 상관 관계는: "기술" 강한 상관 관계가 너무 "HP" 및 "랩" 예. 또한 강력한 상관 관계가 있다는 너무 "650", hello dataset 기부자 hello 지역 번호 650 이므로 합니다.

단어 사이의 hello 상관 관계에 대 한 hello 숫자 값은 hello 탐색 창에서 사용할 수 있습니다. 예를 들어, "사용자"와 "기술" 연관 부정적인 되어 toonote 흥미롭고 "money" 이며

래 틀 hello dataset toohandle 몇 가지 일반적인 문제를 변형할 수 있습니다. 예를 들어, 있습니다 toorescale 기능, 누락 된 값으로 돌립니다, 그리고 이상 값 처리 및 변수 또는 관찰 누락 된 데이터를 제거 합니다. Rattle은 관찰 및/또는 변수 간의 연결 규칙을 식별할 수도 있습니다. 이러한 탭은 이 소개용 연습에 대한 범위를 벗어납니다.

Rattle은 클러스터 분석을 수행할 수도 있습니다. 일부 기능 toomake hello 출력 쉽게 tooread를 제외 해 보겠습니다. Hello에 **데이터** 탭에서 선택 **무시** hello 변수 이러한 10 개의 항목 제외 하 고 다음 tooeach:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

이동 하 여 다시 toohello **클러스터** 탭에서 선택 **KMeans**, 및 집합 hello *클러스터 수* too4 합니다. 그런 다음 **실행**을 클릭합니다. hello 결과 hello 출력 창에 표시 됩니다. 한 클러스터가 "george" 및 "hp"의 빈도가 높고 아마도 합법적인 비즈니스 메일입니다.

toobuild 간단한 의사 결정 트리 기계 학습 모델:

* 선택 hello **모델** 탭
* 선택 **트리** hello로 **형식**합니다.
* 선택 **Execute** hello에 대 한 텍스트 형태로 toodisplay hello 트리 출력 창.
* 선택 hello **그리기** 단추 tooview 그래픽 버전입니다. 이러한 사용 하 여 이전을 얻 었 toohello 트리를 매우 유사 하 게 *rpart*합니다.

Hello 래 틀의 훌륭한 기능 중 하나는 해당 기능 toorun 여러 기계 학습 방법 및 신속 하 게 평가 합니다. Hello 절차는 다음과 같습니다.

* 선택 **모든** hello에 대 한 **형식**합니다.
* **실행**을 선택합니다.
* 완료 된 후 클릭할 수 있는 단일 **형식**처럼 **SVM**, hello 결과 확인 합니다.
* Hello를 사용 하 여 설정 하는 hello 유효성 검사에 hello 모델의 hello 성능을 비교할 수도 있습니다 **평가** 탭 합니다. 예를 들어 hello **오류 매트릭스** 선택 보면 hello 혼동 행렬, 전체 오류 및 각 모델에 대 한 평균된 클래스 오류 hello 유효성 검사 집합에 있습니다.
* 또한 ROC 곡선을 그림으로 나타내고, 민감도 분석을 수행하고, 다른 유형의 모델 평가를 수행할 수도 있습니다.

모델 작성 작업을 완료 되 면 선택 hello **로그** 세션 동안 래 틀에서 실행 한 tooview hello R 코드를 탭 합니다. Hello를 선택할 수 있습니다 **내보내기** 단추 toosave 것입니다.

> [!NOTE]
> 현재 릴리스의 Rattle에 버그가 있습니다. toomodify 스크립트 hello 또는 toorepeat 사용할 단계를 앞에 # 문자를 삽입 해야 하는 나중 *...이 로그 내보내기 * hello 로그 hello 텍스트에 합니다.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL 및 Squirrel SQL
hello DSVM 설치 PostgreSQL 함께 제공 됩니다. PostgreSQL은 정교한 오픈 소스 관계형 데이터베이스입니다. 이 섹션에서는 어떻게 tooload 우리의 PostgreSQL에 데이터 집합을 스팸 및 쿼리할 수 있습니다.

Hello 데이터를 로드할 수 있습니다, 전에 hello localhost에서 tooallow 암호 인증을 해야 합니다. 명령 프롬프트에서:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Hello 구성 파일의 hello 아래 근처는 연결을 허용 하는 hello에 자세히 설명 하는 여러 줄:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

사용자 이름 및 암호를 사용 하 여 로그인 할 수 있도록 hello "로컬 연결 IPv4" 줄 toouse md5 ident, 대신 변경 합니다.

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

고 hello postgres 서비스를 다시 시작 합니다.

    sudo systemctl restart postgresql

toolaunch psql, PostgreSQL hello 기본 제공 postgres 사용자로는 대화형 터미널 hello 프롬프트에서 다음 명령을 실행 합니다.

    sudo -u postgres psql

새 사용자 계정 만들기, 사용 하 여 hello Linux 계정 이름으로 현재 로그온에 따라 동일한 사용자 이름 hello 및 암호 제공:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

그런 다음 사용자로 toopsql 로그인:

    psql

하 여 새 데이터베이스로 hello 데이터를 가져옵니다.

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

이제 hello 데이터를 탐색 하 고 사용 하 여 일부 쿼리를 실행 하겠습니다 **스 쿼 럴 SQL**, JDBC 드라이버를 통해 데이터베이스와 상호 작용할 수 있게 하는 그래픽 도구입니다.

tooget 시작, 스 쿼 럴 SQL hello 응용 프로그램 메뉴에서 시작 합니다. tooset hello 드라이버를 구성 합니다.

* **Windows**를 선택한 다음 **드라이버 보기**를 선택합니다.
* **PostgreSQL**을 마우스 오른쪽 단추로 클릭하고 **드라이버 수정**을 선택합니다.
* **추가 클래스 경로**를 선택한 다음 **추가**를 선택합니다.
* 입력 ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello에 대 한 **파일 이름** 및
* **열기**를 선택합니다.
* 드라이버 목록을 선택한 다음 **클래스 이름**에서 **org.postgresql.Driver**를 선택하고 **확인**을 선택합니다.

hello 연결 toohello 로컬 서버를 tooset:

* **Windows**를 선택한 다음 **별칭 보기**를 선택합니다.
* Hello 선택  **+**  단추 toomake 새 별칭입니다.
* 이름을 *스팸 데이터베이스*, 선택 **PostgreSQL** hello에 **드라이버** 드롭 다운 합니다.
* 너무 hello URL 설정*jdbc:postgresql://localhost/spam*합니다.
* *사용자 이름* 및 *암호*를 입력합니다.
* **확인**을 클릭합니다.
* tooopen hello **연결** 창의 hello를 두 번 클릭 ***스팸 데이터베이스*** 별칭입니다.
* **연결**을 선택합니다.

toorun 일부 쿼리:

* 선택 hello **SQL** 탭 합니다.
* 단순 쿼리를 같은 입력 `SELECT * from data;` hello SQL 탭의 hello 위쪽 hello 쿼리 텍스트 상자에 있습니다.
* 키를 눌러 **Ctrl + Enter** toorun 것입니다. 기본적으로 스 쿼 럴 SQL hello 처음 100 개 행 반환 쿼리에서 합니다.

많은 더 많은 쿼리가이 데이터 tooexplore를 실행할 수 있습니다. 예를 들어 hello은 어떻게 hello 단어의 주파수 *확인* 스팸과 햄 차이?

    SELECT avg(word_freq_make), spam from data group by spam;

자주 포함 하는 전자 메일의 hello 특징은 무엇 또는 *3d*?

    SELECT * from data order by word_freq_3d desc;

상위 항목에 있는 대부분의 전자 메일 *3d* 예측 모델 tooclassify hello 전자 메일을 작성 하기 위한 유용한 기능 수 있도록는 스팸 명백 하 게 됩니다.

PostgreSQL 데이터베이스에 저장 된 데이터 tooperform 기계 학습을 원하는 경우 사용해 볼 [MADlib](http://madlib.incubator.apache.org/)합니다.

## <a name="sql-server-data-warehouse"></a>SQL Server 데이터 웨어하우스
Azure SQL 데이터 웨어하우스는 거대한 양의 관계형 및 비관계형 데이터를 처리할 수 있는 클라우드 기반 규모 확장 데이터베이스입니다. 자세한 내용은 [Azure SQL Data Warehouse란?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello 데이터 웨어하우스 및 명령 프롬프트에서 명령이 실행된 hello 다음 hello 테이블을 만듭니다.

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

그런 다음 프롬프트 hello sqlcmd:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

bcp를 사용하여 데이터 복사:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> hello 다운로드 한 파일의 줄 끝에 hello Windows 스타일 있지만 bcp와 hello-r 플래그는 tootell bcp 하므로 UNIX 스타일을 예상 합니다.
>
>

sqlcmd를 사용하여 쿼리:

    select top 10 spam, char_freq_dollar from spam;
    GO

Squirrel SQL을 사용하여 쿼리할 수도 있습니다. 사용 하 여 hello Microsoft MSSQL Server JDBC 드라이버에서 찾을 수 있는 PostgreSQL에 대 한 비슷한 단계에 따라 ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***합니다.

## <a name="next-steps"></a>다음 단계
Azure의 hello 데이터 과학 프로세스를 구성 하는 hello 작업을 안내 하는 항목의 개요를 참조 하십시오. [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess)합니다.

특정 시나리오에 대 한 hello 팀 데이터 과학 프로세스의에서 hello 단계를 보여 주는 다른 종단 간 연습에 대 한 참조 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md)합니다. hello 연습도 방법을 toocombine 클라우드 및 온-프레미스 도구 및 워크플로 또는 파이프라인 toocreate에 서비스는 지능형 응용 프로그램입니다.
