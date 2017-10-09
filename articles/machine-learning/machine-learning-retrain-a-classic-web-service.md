---
title: "기본 웹 서비스 aaaRetrain | Microsoft Docs"
description: "어떻게 tooprogrammatically 모델을 다시 학습 모델 및 업데이트 hello 웹 서비스 toouse hello 새로 학습 된 Azure 기계 학습에서에 대해 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>기존 웹 서비스 재학습
hello 배포한 예측 웹 서비스는 hello 기본 점수 매기기 끝점용 합니다. 기본 끝점은 계속 동기화 hello 원래 학습 및 테스트를 평가 하 고 따라서 hello hello 기본 끝점에 대 한 학습 된 모델을 바꿀 수 없습니다. tooretrain hello 웹 서비스를 새 끝점 toohello 웹 서비스를 추가 해야 합니다. 

## <a name="prerequisites"></a>필수 조건
학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다. 

> [!IMPORTANT]
> hello 예측 실험 클래식 기계 학습 웹 서비스도 배포 되어야 합니다. 
> 
> 

웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

## <a name="add-a-new-endpoint"></a>새 끝점 추가
hello 배포한 예측 웹 서비스에는 점수 매기기 끝점용 hello 원래 학습 및 점수 매기기 실험 학습 된 모델와 동기화 유지 되는 기본 포함 되어 있습니다. tooupdate 프로그램 웹 서비스 toowith 새 학습 된 모델 점수 매기기 새 끝점을 만들 해야 있습니다. 

toocreate hello hello 학습 된 모델을 업데이트할 수 있는 예측 웹 서비스에 새 점수 매기기 끝점:

> [!NOTE]
> Hello 끝점 toohello 예측 웹 서비스, 하지 hello 학습 웹 서비스를 추가 하는 확인 해야 합니다. 학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다. hello 예측 웹 서비스 "[예측 내선 번호]"로 끝나야 합니다.
> 
> 

세 가지 방법으로 새 끝점 tooa 웹 서비스를 추가할 수 있습니다.

1. 프로그래밍 방식
2. Hello Microsoft Azure 웹 서비스 포털을 사용 하 여
3. Hello Azure 클래식 포털을 사용 하 여

### <a name="programmatically-add-an-endpoint"></a>프로그래밍 방식으로 끝점을 추가합니다.
이 제공 된 hello 샘플 코드를 사용 하 여 점수 매기기 끝점을 추가할 수 있습니다 [github 리포지토리](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)합니다.

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Hello Microsoft Azure 웹 서비스 포털 tooadd 끝점을 사용 하 여
1. 기계 학습 스튜디오에서는 hello 왼쪽된 탐색 열 웹 서비스를 클릭 합니다.
2. Hello 웹 서비스 대시보드 hello 아래쪽 클릭 **관리 끝점 미리 보기**합니다.
3. **추가**를 클릭합니다.
4. 이름 및 hello 새 끝점에 대 한 설명을 입력 합니다. Hello 로깅 수준 및 예제 데이터가 활성화 되어 있는지 여부를 선택 합니다. 자세한 내용은 [Machine Learning 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Azure 클래식 포털 tooadd 끝점 hello를 사용 하 여
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **기계 학습**합니다.
3. 이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.
4. 이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.
5. Hello hello 페이지의 아래쪽에 있는 클릭 **끝점 추가**합니다. 끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요. 

## <a name="update-hello-added-endpoints-trained-model"></a>업데이트 hello 끝점의 학습 된 모델 추가
toocomplete hello 재교육 프로세스를 사용자가 추가한 hello 새 끝점의 hello 학습 된 모델을 업데이트 해야 합니다.

* Hello 포털에서 hello 새 끝점의 이름을 클릭 다음 hello 수 hello 클래식 Azure 포털을 사용 하 여 hello 새 끝점을 추가한 경우 **UpdateResource** tooupdate hello 끝점의 모델 해야 tooget hello URL에 연결 합니다.
* Hello 샘플 코드를 사용 하 여 hello 끝점을 추가한 경우 여기에 hello로 식별 되는 hello 도움말 URL의 위치 *HelpLocationURL* hello 출력에는 값입니다.

tooretrieve hello 경로 URL:

1. 복사 하 여 브라우저에 hello URL을 붙여 넣습니다.
2. Hello 업데이트 리소스 링크를 클릭 합니다.
3. Hello hello PATCH 요청의 게시 URL을 복사 합니다. 예:
   
     패치 URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

이제 점수 매기기 끝점용 이전에 만든 hello 학습 된 모델 tooupdate hello를 사용할 수 있습니다.

표시 하는 샘플 코드 다음 hello toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, 및 패치 URL tooupdate hello 끝점입니다.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

hello *apiKey* 및 hello *endpointUrl* 에 hello 호출 끝점 대시보드에서 가져올 수 있습니다.

값의 hello hello *이름* 매개 변수에서 *리소스* 은 일치 hello hello의 리소스 이름은 학습 된 모델에에서 저장 hello 예측 실험 합니다. tooget hello 리소스 이름:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **기계 학습**합니다.
3. 이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.
4. 이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.
5. 추가한 hello 새 끝점을 클릭 합니다.
6. Hello 끝점 대시보드에서 **업데이트 리소스**합니다.
7. Hello hello hello 웹 서비스에 대 한 업데이트 리소스 API 설명서 페이지를 찾을 수 있습니다 **리소스 이름** 아래 **업데이트할 수 있는 리소스**합니다.

Hello 끝점을 업데이트를 완료 하기 전에 SAS 토큰에 만료 되 면 hello 작업 Id tooobtain 새로 토큰 상태로 GET을 수행 해야 합니다.

Hello 코드 성공적으로 실행 하는 경우 새 끝점의 hello 약 30 초 내에 다시 학습 되도록 hello 모델을 사용 하 여 시작 해야 합니다.

## <a name="summary"></a>요약
Api 재교육 hello를 사용 하 여, 예측 웹 서비스와 같은 시나리오를 지원의 hello 학습 된 모델을 업데이트할 수 있습니다.

* 새 데이터를 사용하는 주기적 모델 재학습.
* 자신의 데이터를 사용 하 여 hello 모델을 보존 하기 위해 이러한의 hello 목표 모델 toocustomers의 분포를 설정 합니다.

## <a name="next-steps"></a>다음 단계
[Azure 기계 학습 클래식 웹 서비스의 hello 재교육 문제 해결](machine-learning-troubleshooting-retraining-models.md)

