---
title: "PowerShell과 함께 새 Azure 기계 학습 웹 서비스 aaaRetrain | Microsoft Docs"
description: "Tooprogrammatically 모델과 hello 웹 서비스 toouse hello 새로 학습 된 모델 업데이트 hello 컴퓨터 학습 관리 PowerShell cmdlet을 사용 하 여 Azure 기계 학습에서를 재 연습 하는 방법에 대해 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Hello 컴퓨터 학습 관리 PowerShell cmdlet을 사용 하 여 새 리소스 관리자 기반 웹 서비스를 다시 학습
새 웹 서비스를 다시 학습 hello 예측 웹 서비스 정의 tooreference hello 새 학습 된 모델을 업데이트 됩니다.  

## <a name="prerequisites"></a>필수 조건
학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다. 

> [!IMPORTANT]
> hello 예측 실험으로는 Azure 리소스 관리자 (새) 기반으로 기계 학습 웹 서비스 배포 되어야 합니다. toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

이 프로세스는 hello Azure 컴퓨터 학습 Cmdlet을 설치 했는지 필요 합니다. Hello 기계 학습 cmdlet을 설치 하는 정보에 대 한 참조 hello [Azure 컴퓨터 학습 Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) msdn 참조 합니다.

복사 된 hello 출력 재교육 hello에서 다음 정보:

* BaseLocation
* RelativeLocation

hello 단계를 수행 됩니다.

1. Tooyour Azure 리소스 관리자 계정에에서 로그인 합니다.
2. Hello 웹 서비스 정의 가져오기
3. JSON으로 hello 웹 서비스 정의 내보내기
4. Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.
5. 웹 서비스 정의 hello JSON 가져오기
6. 새 웹 서비스 정의 된 hello 웹 서비스를 업데이트 합니다.

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Tooyour Azure 리소스 관리자 계정에 로그인
먼저 tooyour hello를 사용 하 여 hello PowerShell 환경 내에서 Azure 계정에에서 로그인 해야 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition"></a>Hello 웹 서비스 정의 가져오기
다음으로 hello 호출 하 여 hello 웹 서비스를 가져올 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. hello 웹 서비스 정의 hello 웹 서비스의 hello 학습 된 모델의 내부 표현 되며 직접 수정할 수 없습니다. 예측 실험 및 하지 학습 실험에 대 한 웹 서비스 정의 hello 검색 되는지 확인 합니다.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello 리소스 그룹의 이름 구독에서 모든 매개 변수 toodisplay hello 웹 서비스 없이 hello AzureRmMlWebService Get cmdlet을 실행 하는 기존 웹 서비스입니다. Hello 웹 서비스를 찾은 다음 웹 서비스 ID 확인 hello hello 리소스 그룹 이름은 hello ID의 네 번째 요소 hello hello 직후 *resourceGroups* 요소입니다. 다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

또는 toodetermine hello 리소스의 그룹 이름 기존 웹 서비스, toohello Microsoft Azure 컴퓨터 학습 웹 서비스 포털에 로그온 합니다. Hello 웹 서비스를 선택 합니다. hello 리소스 그룹 이름은 hello 직후 hello 웹 서비스의 hello URL의 다섯 번째 요소 hello *resourceGroups* 요소입니다. 다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>JSON으로 hello 웹 서비스 정의 내보내기
toomodify hello 정의 toohello 학습 된 모델 toouse hello 새로 학습 된 모델, hello를 먼저 사용 해야 [내보내기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 것 tooa JSON 형식 파일입니다.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.
Hello 자산에서 hello [학습 된 모델], 업데이트 hello 찾습니다 *uri* hello 값 *locationInfo* hello hello ilearner blob의 URI로 노드. hello URI는 결합 하 여 생성 hello *BaseLocation* 및 hello *RelativeLocation* hello BES 재교육 호출의 hello 출력에서. Hello 경로 tooreference hello 새 학습 된 모델을 업데이트 합니다.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
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

## <a name="import-hello-json-into-a-web-service-definition"></a>웹 서비스 정의 hello JSON 가져오기
Hello를 사용 해야 [가져오기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello tooupdate hello 웹 서비스 정의 사용할 수 있는 웹 서비스 정의로 다시 JSON 파일을 수정 합니다.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>새 웹 서비스 정의 된 hello 웹 서비스를 업데이트 합니다.
사용 하는 마지막으로, [업데이트 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 웹 서비스 정의 합니다.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>요약
Hello 컴퓨터 학습 PowerShell 관리 cmdlet을 사용 하 여 예측 웹 서비스 같은 시나리오를 지원의 hello 학습 된 모델을 업데이트할 수 있습니다.

* 새 데이터를 사용하는 주기적 모델 재학습.
* 자신의 데이터를 사용 하 여 hello 모델을 보존 하기 위해 이러한의 hello 목표 모델 toocustomers의 분포를 설정 합니다.

