---
title: "기계 학습 aaaRetrain를 프로그래밍 방식으로 모델링 | Microsoft Docs"
description: "어떻게 tooprogrammatically 모델을 다시 학습 모델 및 업데이트 hello 웹 서비스 toouse hello 새로 학습 된 Azure 기계 학습에서에 대해 알아봅니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>프로그래밍 방식으로 기계 학습 모델 다시 학습
이 연습에서는 tooprogrammatically 다시 C# 및 hello 기계 학습 일괄 처리 실행 서비스를 사용 하는 Azure 기계 학습 웹 서비스를 학습 하는 방법을 배웁니다.

일단 hello 모델을 유지 하는 연습을 수행 하는 hello tooupdate 예측 웹 서비스에서 모델을 hello 하는 방법을 보여 줍니다.

* Hello 컴퓨터 학습 웹 서비스 포털의 기본 웹 서비스를 배포한 경우 참조 [클래식 웹 서비스를 다시 학습](machine-learning-retrain-a-classic-web-service.md)합니다. 
* 새 웹 서비스를 배포한 경우 참조 [hello 컴퓨터 학습 관리 cmdlet을 사용 하 여 새 웹 서비스를 다시 학습](machine-learning-retrain-new-web-service-using-powershell.md)합니다.

Hello 재교육 프로세스의 개요를 참조 하십시오. [기계 학습 모델을 다시 학습](machine-learning-retrain-machine-learning-model.md)합니다.

새 Azure 리소스 관리자 기반 웹 서비스는 기존 toostart 하려는 경우, 참조 [기존 예측 웹 서비스를 다시 학습](machine-learning-retrain-existing-resource-manager-based-web-service.md)합니다.

## <a name="create-a-training-experiment"></a>학습 실험 만들기
이 예제에서는 사용 합니다 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" hello Microsoft Azure 기계 학습 샘플에서 합니다. 

toocreate hello 실험:

1. TooMicrosoft Azure 기계 학습 스튜디오에 로그인 합니다. 
2. Hello의 오른쪽 아래 모서리 hello 대시보드, 클릭 **새로**합니다.
3. Microsoft 샘플 hello에서 샘플 5를 선택 합니다.
4. hello 실험 캔버스의 hello 위쪽 toorename hello 실험 hello 실험 이름을 선택 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합"입니다.
5. Census Model을 입력합니다.
6. Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.
7. **웹 서비스 설정**을 클릭하고 **재학습 웹 서비스**를 선택합니다. 

hello 다음 hello 초기 실험을 보여 줍니다.
   
   ![초기 실험.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>예측 실험을 만들고 웹 서비스로 게시
다음으로 서술적 실험을 만듭니다.

1. Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **예측 웹 서비스**합니다. Hello 모델을 학습 된 모델로 저장 웹 서비스 입력 및 출력 모듈을 추가 합니다. 
2. **실행**을 클릭합니다. 
3. Hello 실험 실행이 종료 된 후 클릭 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]**합니다.

> [!NOTE] 
> toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Hello 학습 실험을 교육 웹 서비스로 배포
tooretrain hello 학습 된 모델 Retraining 웹 서비스로 작성 하는 hello 학습 실험을 배포 해야 합니다. 이 웹 서비스는 *웹 서비스 출력* 모듈 연결 toohello  *[모델 학습] [ train-model]*  모듈, 새로운 toobe 수 tooproduce 학습 된 모델입니다.

1. tooreturn toohello 학습 실험 hello 왼쪽된 창에서 hello 실험 아이콘 클릭 Census 모델 이라는 hello 실험을 클릭 합니다.  
2. Hello 검색 실험 항목 검색 상자에 웹 서비스를 입력 합니다. 
3. 끌어서는 *웹 서비스 입력* hello에 모듈 캔버스를 실험 하 고 해당 출력 toohello 연결 *누락 데이터 정리* 모듈입니다.  이렇게 하면 재교육 데이터 처리는 hello 동일한 방식으로 원래 학습 데이터입니다.
4. 두 개 *웹 서비스 출력* hello에 모듈 실험 캔버스입니다. Hello hello 출력에 연결 *모델 학습* 모듈 tooone 및 hello 출력의 hello *모델 평가* 다른 모듈 toohello 합니다. 에 대 한 웹 서비스 출력 hello **모델 학습** hello 새 학습 된 모델을 제공 합니다. 너무 연결 된 출력 hello**모델 평가** hello 성능 결과 해당 모듈의 출력을 반환 합니다.
5. **실행**을 클릭합니다. 

그런 다음 학습된 된 모델 및 모델 평가 결과 생성 하는 웹 서비스는 hello 학습 실험을 배포 해야 합니다. 기본 웹 서비스 또는 새 웹 서비스를 사용 하 여 작업할 여부에 종속 되어이 작업의 다음 집합 tooaccomplish 합니다.  

**기존 웹 서비스**

Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **웹 서비스 배포 [기본]**합니다. 웹 서비스 hello **대시보드** 일괄 처리 실행에 대 한 API 키와 hello API hello 도움말 페이지가 표시 됩니다. 학습 된 모델을 만들기 위한 hello 일괄 처리 실행 메서드를 사용할 수 있습니다.

**새 웹 서비스**

Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **웹 서비스 배포 [New]**합니다. hello 웹 서비스 Azure 컴퓨터 학습 웹 서비스 포털 toohello 배포 웹 서비스 페이지를 엽니다. 웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다. Hello 일괄 처리 실행 방법 학습 된 모델을 만드는 데 사용할 수 있습니다.

두 경우 모두 실험의 실행을 완료 한 후 hello 결과 워크플로가 표시 다음과 같습니다.

![실행 후 결과 워크플로.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Hello 모델 BES를 사용 하 여 새 데이터를 보존 하기 위해
이 예제에서는 C# toocreate hello 재교육 응용 프로그램에 사용 하는 합니다. 사용할 수도 있습니다 hello Python 또는 R 샘플 코드 tooaccomplish이이 작업 합니다.

toocall hello 재교육 Api:

1. Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.
2. 기계 학습 웹 서비스 포털 toohello에 로그인 합니다.
3. 기존 웹 서비스를 사용하여 작업하는 경우 **Classic Web Services**를 클릭합니다.
   1. 사용 하는 hello 웹 서비스를 클릭 합니다.
   2. Hello 기본 끝점을 클릭 합니다.
   3. **사용**을 클릭합니다.
   4. Hello hello 맨 아래에 **사용** 페이지 hello **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.
   5. 이 절차의 5 toostep를 계속 합니다.
4. 새 웹 서비스를 사용하여 작업하는 경우 **Web Services**를 클릭합니다.
   1. 사용 하는 hello 웹 서비스를 클릭 합니다.
   2. **사용**을 클릭합니다.
   3. Hello hello에서 hello 사용 페이지 맨 아래에 **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.
5. 일괄 처리 실행에 대 한 hello 샘플 C# 코드를 복사 하 고 hello Program.cs 파일에 붙여넣습니다 이때 hello 네임 스페이스를 그대로 유지 해야 합니다.

Hello 설명에 지정 된 대로 Microsoft.AspNet.WebApi.Client hello Nuget 패키지를 추가 합니다. tooadd hello 참조 tooMicrosoft.WindowsAzure.Storage.dll Microsoft Azure 저장소 서비스에 대 한 tooinstall hello 클라이언트 라이브러리를 먼저 할 수 있습니다. 자세한 내용은 [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage)를 참조하세요.

### <a name="update-hello-apikey-declaration"></a>Hello apikey 선언 업데이트
Hello 찾을 **apikey** 선언 합니다.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Hello에 **기본 소비 정보** hello 섹션 **사용** 페이지 hello 기본 키 찾아 toohello 복사 **apikey** 선언 합니다.

### <a name="update-hello-azure-storage-information"></a>Hello Azure 저장소 정보를 업데이트 합니다.
hello BES 샘플 코드는 로컬 드라이브 (예: "C:\temp\CensusIpnput.csv") tooAzure 저장소에서에서 파일을 업로드 하 고 처리 한 hello 결과 백 tooAzure 저장소를 씁니다.  

tooaccomplish이이 태스크에서는 hello 코드의 값에 해당 하는 hello 업데이트 및 hello 클래식 Azure 포털에서 저장소 계정에 대 한 hello 저장소 계정 이름, 키 및 컨테이너 정보를 검색 해야 합니다. 

1. Toohello 클래식 Azure 포털에 로그인 합니다.
2. Hello 왼쪽된 탐색 열에서 클릭 **저장소**합니다.
3. Hello 저장소 계정 목록에서 선택 하나 toostore hello 모델을 유지 합니다.
4. Hello hello 페이지의 아래쪽에 있는 클릭 **액세스 키 관리**합니다.
5. 복사 하 고 hello 저장 **기본 액세스 키** 및 닫기 hello 대화 상자. 
6. Hello hello 페이지의 위쪽에 클릭 **컨테이너**합니다.
7. 기존 컨테이너를 선택 하거나 새 만들고 hello 이름을 저장 합니다.

Hello 찾을 *StorageAccountName*, *StorageAccountKey*, 및 *StorageContainerName* 선언 및에서 저장 하는 hello 값 업데이트 hello Azure 포털입니다.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

또한 hello 코드에서 지정 하는 hello 위치의 hello 입력된 파일을 사용할 수 확인 해야 합니다. 

### <a name="specify-hello-output-location"></a>Hello 출력 위치를 지정 합니다.
Hello 요청 페이로드를 hello 출력 위치를 지정할 때는 hello에 지정 된 hello 파일의 확장명 *RelativeLocation* ilearner로 지정 되어야 합니다. 

다음 예제는 hello를 참조 하십시오.

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> 출력 위치 hello 형태의 hello 웹 서비스 출력 모듈 추가한 hello 순서에 따라이 연습에서 hello에서 다를 수 있습니다. 이 두 개의 출력을 사용 하 여 학습 실험을 설정한 이후 hello 결과 둘 모두에 대 한 저장소 위치 정보를 포함 합니다.  
> 
> 

![재학습 출력][6]

다이어그램 4: 재학습 출력.

## <a name="evaluate-hello-retraining-results"></a>Hello 재교육 결과 평가
Hello 응용 프로그램을 실행 하면 hello 출력 hello URL이 포함 하 고 SAS 토큰 필요한 tooaccess hello 평가 결과입니다.

Hello를 결합 하 여 hello 다시 학습 되도록 모델의 hello 성능 결과 볼 수 있습니다 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 에 대 한 *output2* (에서처럼 hello 재교육 출력 이미지 이전) 및 hello 브라우저 주소 표시줄에 hello 전체 URL 붙여넣기 합니다.  

Hello 새로 학습 된 모델 하나 기존 tooreplace hello 충분히 잘 수행 하는지 여부 hello 결과 toodetermine를 검사 합니다.

복사 hello *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과 통해 사용할 것 hello 재교육 프로세스 중입니다.

## <a name="next-steps"></a>다음 단계
클릭 하 여 hello 예측 웹 서비스를 배포한 경우 **웹 서비스 배포 [기본]**, 참조 [클래식 웹 서비스를 다시 학습](machine-learning-retrain-a-classic-web-service.md)합니다.

클릭 하 여 hello 예측 웹 서비스를 배포한 경우 **웹 서비스 배포 [New]**, 참조 [hello 컴퓨터 학습 관리 cmdlet을 사용 하 여 새 웹 서비스를 다시 학습](machine-learning-retrain-new-web-service-using-powershell.md)합니다.

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
