---
title: "웹 서비스에는 기존 예측 aaaRetrain | Microsoft Docs"
description: "Tooretrain 모델 및 update hello 웹 서비스 toouse hello 새로 학습 된 모델에 Azure 기계 학습 방법에 대해 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>기존 예측 웹 서비스 재학습
이 문서에서는 hello를 재교육 시나리오를 따르는 hello에 대 한 프로세스를 설명 합니다.

* 조작 가능한 웹 서비스로 배포한 학습 실험 및 예측 실험이 있습니다.
* 새 데이터를 지정 하 여 예측 웹 서비스 toouse tooperform 해당 점수 매기기 해야 합니다.

> [!NOTE] 
> toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

기존 웹 서비스 및 실험 부터는 필요한 toofollow 다음이 단계:

1. Hello 모델을 업데이트 합니다.
   1. 웹 서비스 입력 및 출력에 대 한 학습 실험 tooallow 프로그램을 수정 합니다.
   2. Hello 학습 실험 재교육 웹 서비스로 배포 합니다.
   3. Hello 학습 실험 일괄 처리 실행 서비스 (BES) tooretrain hello 모델을 사용 합니다.
2. Hello Azure 컴퓨터 학습 PowerShell cmdlet tooupdate hello 예측 실험을 사용 합니다.
   1. Tooyour Azure 리소스 관리자 계정에에서 로그인 합니다.
   2. Hello 웹 서비스 정을 가져옵니다.
   3. JSON으로 hello 웹 서비스 정을 내보냅니다.
   4. Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.
   5. 웹 서비스 정의로 hello를 JSON을 가져옵니다.
   6. 새 웹 서비스 정의로 hello 웹 서비스를 업데이트 합니다.

## <a name="deploy-hello-training-experiment"></a>Hello 학습 실험 배포
재교육 웹 서비스로 toodeploy hello 학습 실험을 웹 서비스 입력 및 출력 toohello 모델을 추가 해야 합니다. 연결 하 여 한 *웹 서비스 출력* 모듈 toohello 실험  *[모델 학습] [ train-model]*  학습 실험 hello를 사용 하면 모듈을 tooproduce 새 학습 된 모델을 예측 하 여 실험에 사용할 수 있습니다. 있는 경우는 *모델 평가* 모듈을 출력으로 웹 서비스 출력 tooget hello 평가 결과 추가할 수 있습니다.

tooupdate 학습 실험:

1. 연결 된 *웹 서비스 입력* 모듈 tooyour 데이터 입력 (예를 들어 한 *누락 데이터 정리* 모듈). 일반적으로 입력된 데이터에서 처리 되는 tooensure 원하는 hello 동일한 방식으로 원래 학습 데이터입니다.
2. 연결 된 *웹 서비스 출력* 모듈 toohello 출력의 프로그램 *모델 학습* 모듈입니다.
3. 있는 경우는 *모델 평가* toooutput hello 평가 결과 원하는 모듈 하 고, 연결 된 *웹 서비스 출력* 모듈 toohello 출력의 프로그램 *모델 평가* 모듈입니다.

실험을 실행합니다.

다음으로 hello 학습 실험 학습된 된 모델 및 모델 평가 결과 생성 하는 웹 서비스로 배포 해야 합니다.  

Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정**를 선택한 후 **웹 서비스 배포 [New]**합니다. hello Azure 컴퓨터 학습 웹 서비스 포털도 열립니다 toohello **웹 서비스 배포** 페이지. 웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다. 학습 된 모델을 만들기 위한 hello 일괄 처리 실행 방법만 사용할 수 있습니다.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>BES를 사용 하 여 새 데이터를 사용 하 여 hello 모델을 다시 학습
이 예제에서는 C# toocreate hello 재교육 응용 프로그램 사용 합니다. 또한이 작업 Python 또는 R 샘플 코드 tooaccomplish를 사용할 수 있습니다.

Api 재교육 toocall hello:

1. Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.
2. 시스템 학습 웹 서비스 포털 toohello에 로그인 합니다.
3. 작업 하는 hello 웹 서비스를 클릭 합니다.
4. **사용**을 클릭합니다.
5. Hello hello 맨 아래에 **사용** 페이지 hello **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.
6. 일괄 처리 실행에 대 한 hello 샘플 C# 코드를 복사 하 고 hello Program.cs 파일에 붙여 넣습니다. 해당 hello 네임 스페이스는 그대로 있는지 확인 합니다.

Hello 설명에 지정 된 대로 Microsoft.AspNet.WebApi.Client, hello NuGet 패키지를 추가 합니다. tooadd hello 참조 tooMicrosoft.WindowsAzure.Storage.dll 먼저 해야 tooinstall hello [Azure 저장소 서비스에 대 한 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage)합니다.

hello 다음 스크린샷은 hello **사용** hello Azure 컴퓨터 학습 웹 서비스 포털의 페이지입니다.

![사용 페이지][1]

### <a name="update-hello-apikey-declaration"></a>Hello apikey 선언 업데이트
Hello 찾을 **apikey** 선언 합니다.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Hello에 **기본 소비 정보** hello 섹션 **사용** 페이지 hello 기본 키 찾아 toohello 복사 **apikey** 선언 합니다.

### <a name="update-hello-azure-storage-information"></a>Hello Azure 저장소 정보를 업데이트 합니다.
hello BES 샘플 코드는 로컬 드라이브 (예: "C:\temp\CensusIpnput.csv") tooAzure 저장소에서에서 파일을 업로드 하 고 처리 한 hello 결과 백 tooAzure 저장소를 씁니다.  

hello 저장소 계정 이름, 키 및 컨테이너 hello Azure 클래식 포털에서에서 저장소 계정에 대 한 정보와 다음 실험을 실행 한 후 업데이트 hello correspondi hello 결과 검색 해야 tooupdate hello Azure 저장소 정보 워크플로 비슷한 toohello 다음과 같아야 합니다.

![실행 후 결과 워크플로][4]hello 코드의 ng 값입니다.

1. Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 탐색 열에서 클릭 **저장소**합니다.
3. Hello 저장소 계정 목록에서 선택 하나 toostore hello 모델을 유지 합니다.
4. Hello hello 페이지의 아래쪽에 있는 클릭 **액세스 키 관리**합니다.
5. 복사 하 고 hello 저장 **기본 액세스 키** 및 닫기 hello 대화 상자.
6. Hello hello 페이지의 위쪽에 클릭 **컨테이너**합니다.
7. 기존 컨테이너를 선택 하거나 새 만들고 hello 이름을 저장 합니다.

Hello 찾을 *StorageAccountName*, *StorageAccountKey*, 및 *StorageContainerName* 선언 및 hello 클래식 포털에 저장 된 hello 값 업데이트 .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

또한 hello이 입력된 파일은 hello 코드에서 지정 된 hello 위치에서 사용할 수 있는 확인 해야 합니다.

### <a name="specify-hello-output-location"></a>Hello 출력 위치를 지정 합니다.
Hello 요청 페이로드를 hello 출력 위치를 지정 하는 경우에 지정 된 hello 파일의 확장명 hello *RelativeLocation* 로 지정 해야 `ilearner`합니다. 다음 예제는 hello를 참조 하십시오.

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

hello 다음은 출력 재교육의 예: ![재교육 출력][6]

## <a name="evaluate-hello-retraining-results"></a>Hello 재교육 결과 평가 합니다.
Hello 응용 프로그램을 실행 하면 hello 출력 hello URL 및 필요한 tooaccess hello 평가 결과 해당 하는 공유 액세스 서명 토큰을 포함 합니다.

Hello를 결합 하 여 hello 다시 학습 되도록 모델의 hello 성능 결과 볼 수 있습니다 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 에 대 한 *output2* (에서처럼 hello 재교육 출력 이미지 이전) 및 hello 브라우저 주소 표시줄에 hello 전체 URL 붙여넣기 합니다.  

Hello 새로 학습 된 모델 하나 기존 tooreplace hello 충분히 잘 수행 하는지 여부 hello 결과 toodetermine를 검사 합니다.

복사 hello *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 합니다.

## <a name="retrain-hello-web-service"></a>Hello 웹 서비스를 다시 학습
새 웹 서비스를 다시 학습 hello 예측 웹 서비스 정의 tooreference hello 새 학습 된 모델을 업데이트 됩니다. hello 웹 서비스 정의 hello 웹 서비스의 hello 학습 된 모델의 내부 표현 되며 직접 수정할 수 없습니다. 예측 실험 및 하지 학습 실험에 대 한 hello 웹 서비스 정의 검색 되는지 확인 합니다.

## <a name="sign-in-tooazure-resource-manager"></a>리소스 관리자 tooAzure에 로그인
먼저 hello를 사용 하 여 tooyour hello PowerShell 환경 내에서 Azure 계정에에서 로그인 해야 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Hello 웹 서비스 정의 개체 가져오기
다음으로 호출 hello 여 hello 웹 서비스 정의 개체를 가져올 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello 리소스 그룹의 이름 구독에서 모든 매개 변수 toodisplay hello 웹 서비스 없이 hello AzureRmMlWebService Get cmdlet을 실행 하는 기존 웹 서비스입니다. Hello 웹 서비스를 찾은 다음 웹 서비스 ID 확인 hello hello 리소스 그룹 이름은 hello ID의 네 번째 요소 hello hello 직후 *resourceGroups* 요소입니다. 다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

또는 toodetermine hello 리소스 그룹 이름은 기존 웹 서비스, toohello Azure 컴퓨터 학습 웹 서비스 포털에 로그인 합니다. Hello 웹 서비스를 선택 합니다. hello 리소스 그룹 이름은 hello 직후 hello 웹 서비스의 hello URL의 다섯 번째 요소 hello *resourceGroups* 요소입니다. 다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Hello 웹 서비스 정의 개체를 JSON으로 내보내기
새로 학습 된 모델의 학습 된 모델 toouse hello hello toomodify hello 정의 hello를 먼저 사용 해야 [내보내기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 것 tooa JSON 형식의 파일입니다.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Hello 참조 toohello ilearner blob를 업데이트 합니다.
Hello 자산에서 hello [학습 된 모델], 업데이트 hello 찾습니다 *uri* hello 값 *locationInfo* hello hello ilearner blob의 URI로 노드. hello URI는 결합 하 여 생성 hello *BaseLocation* 및 hello *RelativeLocation* hello BES 재교육 호출의 hello 출력에서.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>웹 서비스 정의 개체에 hello JSON 가져오기
Hello를 사용 해야 [가져오기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello tooupdate hello predicative 실험에 사용할 수 있는 웹 서비스 정의 개체에 다시 JSON 파일을 수정 합니다.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Hello 웹 서비스를 업데이트 합니다.
마지막으로 hello를 사용 하 여 [업데이트 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 실험 예측 합니다.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
