---
title: "어떻게 toomanage AzureML 웹 서비스 API 관리를 사용 하 여 aaaLearn | Microsoft Docs"
description: "API 관리를 사용 하 여 toomanage AzureML 웹을 서비스 하는 방법을 보여 주는 가이드입니다."
keywords: "기계 학습, api 관리"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>API 관리를 사용 하 여 toomanage AzureML 웹을 서비스 하는 방법에 대해 알아봅니다
## <a name="overview"></a>개요
이 가이드에서는 tooquickly AzureML 웹 서비스 API 관리 toomanage를 사용 하 여 시작 합니다.

## <a name="what-is-azure-api-management"></a>Azure API 관리란?
Azure API 관리는 사용자 액세스, 사용 제한 및 대시보드 모니터링을 정의하여 REST API 끝점을 관리할 수 있는 Azure 서비스입니다. Azure API 관리에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/api-management/) 를 클릭하세요. 클릭 [여기](../api-management/api-management-get-started.md) tooget Azure API 관리 시작 하는 방법에 대 한 지침에 대 한 합니다. 이 가이드를 기반으로 하는 이 다른 가이드에서는 알림 구성, 가격 책정 계층, 응답 처리, 사용자 인증, 제품 생산, 개발자 구독 및 사용량 대시보딩을 포함하는 다양한 주제를 다룹니다.

## <a name="what-is-azureml"></a>AzureML이란?
AzureML는 tooeasily 빌드 수 있도록 하는 기계 학습에 대 한 Azure 서비스, 배포 및 고급 분석 솔루션 공유 합니다. AzureML에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/machine-learning/) 를 클릭하세요.

## <a name="prerequisites"></a>필수 조건
toocomplete 해야이 가이드:

* Azure 계정. Azure 계정이 없으면 클릭 [여기](https://azure.microsoft.com/pricing/free-trial/) 방법에 대 한 자세한 내용은 toocreate 무료 평가판 계정 합니다.
* AzureML 계정. AzureML 계정이 없으면 클릭 [여기](https://studio.azureml.net/) 방법에 대 한 자세한 내용은 toocreate 무료 평가판 계정 합니다.
* hello 작업 영역, 서비스 및 웹 서비스로 배포 AzureML 실험에 api_key 합니다. 클릭 [여기](machine-learning-create-experiment.md) toocreate는 AzureML 실험 하는 방법에 대 한 내용은 합니다. 클릭 [여기](machine-learning-publish-a-machine-learning-web-service.md) 웹 서비스로 toodeploy는 AzureML 실험 하는 방법에 대 한 내용은 합니다. 또는 부록 A toocreate 및 간단한 AzureML 테스트 실험 하 고 웹 서비스로 배포 방법에 대 한 지침에 있습니다.

## <a name="create-an-api-management-instance"></a>API 관리 인스턴스 만들기
AzureML 웹 서비스 API 관리 toomanage를 사용 하 여 hello 단계는 다음과 같습니다. 먼저 서비스 인스턴스를 만듭니다. Toohello 로그인 [클래식 포털](https://manage.windowsazure.com/) 클릭 **새로** > **응용 프로그램 서비스** > **API 관리**  >  **만들**합니다.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

고유한 **URL**을 지정합니다. 이 가이드에서는 **demoazureml** – 해야 toochoose 서로 다른 무엇 인가입니다. 원하는 hello 선택 **구독** 및 **지역** 서비스 인스턴스에 대 한 합니다. 선택 항목에 확인 한 후 hello 다음 단추를 클릭 합니다.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Hello에 대 한 값을 지정 **조직 이름**합니다. 이 가이드에서는 **demoazureml** – 해야 toochoose 서로 다른 무엇 인가입니다. Hello에 전자 메일 주소를 입력 **관리자 전자 메일** 필드입니다. 이 전자 메일 주소는 hello API 관리 시스템에서에서 알림에 사용 됩니다.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Hello 확인란 toocreate 서비스 인스턴스를 클릭 합니다. *만든 새 서비스 toobe toothirty 분 차지*합니다.

## <a name="create-hello-api"></a>Hello API 만들기
Hello 서비스 인스턴스를 만든 후 hello 다음 단계는 toocreate hello API입니다. API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다. API 작업은 웹 서비스 프록시 tooexisting입니다. 이 가이드는 기존 AzureML RR 및 BES 웹 서비스 프록시 toohello 해당 Api를 만듭니다.

Api 생성 및 hello Azure 클래식 포털을 통해 액세스할 수 있는 hello API 게시자 포털에서 구성 됩니다. tooreach는 서비스 인스턴스를 게시자 포털에서 선택 hello 합니다.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

클릭 **관리** API 관리 서비스에 대 한 hello Azure 클래식 포털의에서.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **추가 API**합니다.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

형식 **AzureML 데모 API** hello로 **웹 API 이름**합니다. 형식 **https://ussouthcentral.services.azureml.net** hello로 **웹 서비스 URL**합니다. 형식 **azureml 데모** hello로 **웹 API URL 접미사**합니다. 확인 **HTTPS** hello로 **웹 API URL** 구성표입니다. **시작**을 **제품**으로 선택합니다. 완료 되 면 클릭 **저장** toocreate hello API입니다.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Hello 작업 추가
클릭 **추가 작업이** tooadd operations toothis API입니다.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

hello **새 작업** 창이 표시 되 고 hello **서명** 탭이 기본적으로 선택 됩니다.

## <a name="add-rrs-operation"></a>RRS 작업 추가
먼저 hello AzureML RR 서비스에 대 한 작업을 만듭니다. 선택 **POST** hello로 **HTTP 동사**합니다. 형식 **/workspaces/ {작업 영역} /services/ {서비스} / 실행? api 버전 {apiversion} = & 세부 정보 = {자세히}** hello로 **URL 템플릿**합니다. 형식 **RR 실행** hello로 **표시 이름**합니다.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다. 클릭 **저장** toosave이이 작업 합니다.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>BES 작업 추가
스크린 샷을 대 한 포함 되지 않습니다. hello RR 작업을 추가 하기 위한 매우 유사한 toothose 멤버인 BES 작업 hello 합니다.

### <a name="submit-but-not-start-a-batch-execution-job"></a>일괄 처리 실행 작업 제출(시작하지는 않음)
클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다. 선택 **POST** hello에 대 한 **HTTP 동사**합니다. 형식 **/workspaces/ {작업 영역} /services/ {서비스 (를) 작업 /? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다. 형식 **BES 제출** hello에 대 한 **표시 이름**합니다. 클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다. 클릭 **저장** toosave이이 작업 합니다.

### <a name="start-a-batch-execution-job"></a>일괄 처리 실행 작업 시작
클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다. 선택 **POST** hello에 대 한 **HTTP 동사**합니다. 형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid} / 시작? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다. 형식 **BES 시작** hello에 대 한 **표시 이름**합니다. 클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다. 클릭 **저장** toosave이이 작업 합니다.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Hello 상태 또는 일괄 처리 실행 작업의 결과 가져옵니다.
클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다. 선택 **가져오기** hello에 대 한 **HTTP 동사**합니다. 형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid}? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다. 형식 **BES 상태** hello에 대 한 **표시 이름**합니다. 클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다. 클릭 **저장** toosave이이 작업 합니다.

### <a name="delete-a-batch-execution-job"></a>일괄 처리 실행 작업 삭제
클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다. 선택 **삭제** hello에 대 한 **HTTP 동사**합니다. 형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid}? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다. 형식 **BES 삭제** hello에 대 한 **표시 이름**합니다. 클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다. 클릭 **저장** toosave이이 작업 합니다.

## <a name="call-an-operation-from-hello-developer-portal"></a>Hello 개발자 포털에서에서 작업 호출
작업 편리 tooview 제공 하는 hello 개발자 포털에서 직접 호출할 수 있습니다 및 API의 hello 작동을 테스트 합니다. 호출 하 게이 가이드 단계에서는 hello **RR 실행** toohello 추가 된 메서드가 **AzureML 데모 API**합니다. 클릭 **개발자 포털** hello에 hello 메뉴에서 hello 클래식 포털의 오른쪽 위에 있습니다.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

클릭 **Api** hello 상단 메뉴에서 **AzureML 데모 API** toosee hello 작업의 상태를 사용할 수 있습니다.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

선택 **RR 실행** hello 작업에 대 한 합니다. **사용해 보세요.**를 클릭합니다.

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

요청 매개 변수를 입력 하면 **작업 영역**, **서비스**, **2.0** hello에 대 한 **apiversion**, 및 **true**hello에 대 한 **세부 정보**합니다. 찾을 수 있습니다 프로그램 **작업 영역** 및 **서비스** hello AzureML 웹 서비스 대시보드에서 (참조 **hello 웹 서비스를 테스트할** 부록 A).

요청 헤더로는 **헤더 추가**를 클릭하고 **콘텐츠 유형** 및 **application/json**을 입력하고 나서, **헤더 추가**를 클릭하고 **자동화** 및 **전달자<YOUR AZUREML SERVICE API-KEY>**를 입력합니다. 찾을 수 있습니다 프로그램 **api 키** hello AzureML 웹 서비스 대시보드에서 (참조 **hello 웹 서비스를 테스트할** 부록 A).

형식 **{"입력": {"input1": {"ColumnNames": "값" ["Col2"]: [["이것이 좋은 하루"]]}}, "GlobalParameters": {}}** hello 요청 본문에 대 한 합니다.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

**보내기**를 클릭합니다.

![보내기](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

작업이 호출 hello 개발자 포털 hello 표시 **요청 URL** hello 백 엔드 서비스에서 hello **응답 상태**, hello **응답 헤더**, 임의의 **응답 콘텐츠**합니다.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>부록 A - 간단한 AzureML 웹 서비스 만들기 및 테스트
### <a name="creating-hello-experiment"></a>Hello 실험 만들기
간단한 AzureML 실험을 만들어 웹 서비스로 배포 하기 위한 hello 단계는 다음과 같습니다. 임의의 텍스트 열을 입력으로 웹 서비스는 hello 하 고 정수로 표시 되는 기능 집합을 반환 합니다. 예:

| 텍스트 | 해시된 텍스트 |
| --- | --- |
| This is a good day |1 1 2 2 0 2 0 1 |

첫째, 원하는 브라우저를 사용 하 여를 이동: [https://studio.azureml.net/](https://studio.azureml.net/) 사용자 자격 증명 toolog에를 입력 합니다. 그리고 새 실험을 만듭니다.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

너무 이름 바꾸기**SimpleFeatureHashingExperiment**합니다. **저장된 데이터 집합**을 확장하고 **Amazon의 도서 리뷰**를 실험으로 끌어서 놓습니다.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

**데이터 변환** 및 **조작**을 확장하고 **데이터 집합의 열 선택**을 실험으로 끌어서 놓습니다. 연결 **Amazon에서 책 검토** 너무**데이터 집합의 열 선택**합니다.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

**데이터 집합의 열 선택**, **열 선택기 시작**을 차례로 클릭하고 **Col2**를 선택합니다. 이러한 변경 내용을 확인 표시 tooapply hello를 클릭 합니다.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

확장 **텍스트 분석** 끌어서 **기능 해시** hello 실험에 있습니다. 연결 **데이터 집합의 열 선택** 너무**기능 해시**합니다.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

형식 **3** hello에 대 한 **해시 비트 크기**합니다. 8(23)개 열이 생성됩니다.

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

이 시점에서 tooclick 경우가 **실행** tootest hello 실험 합니다.

![실행](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>웹 서비스 만들기
이제 웹 서비스를 만듭니다. **웹 서비스**를 확장하고 **입력**을 실험으로 끌어서 놓습니다. 연결 **입력** 너무**기능 해시**합니다. **출력** 을 실험으로 끌어서 놓습니다. 연결 **출력** 너무**기능 해시**합니다.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

**웹 서비스 게시**를 클릭합니다.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

클릭 **예** toopublish hello 실험 합니다.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Hello 웹 서비스 테스트
AzureML 웹 서비스는 RSS(요청/응답 서비스) 및 BES(일괄 처리 실행 서비스) 끝점으로 구성됩니다. RSS는 동기 실행에 사용됩니다. BES는 비동기 작업 실행에 사용됩니다. tootest hello 샘플 Python 소스 아래와 웹 서비스를 할 수 있습니다 toodownload 및 설치 hello Azure SDK for Python (참조: [어떻게 tooinstall Python](../python-how-to-install.md)).

Hello 만들어야 **작업 영역**, **서비스**, 및 **api_key** hello 샘플 소스 아래에 대 한 실험의 합니다. 클릭 하 여 hello 작업 영역 및 서비스를 찾을 수 있습니다 **요청/응답** 또는 **일괄 처리 실행** hello 웹 서비스 대시보드를 사용 하 여 실험에 대 한 합니다.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Hello를 찾을 수 있습니다 **api_key** hello 웹 서비스 대시보드를 사용 하 여 실험을 클릭 하 여 합니다.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>RRS 끝점 테스트
##### <a name="test-button"></a>테스트 단추
쉽게 tootest hello RR 끝점은 tooclick **테스트** hello 웹 서비스 대시보드에서.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

**col2**로 **This is a good day**를 입력합니다. Hello 확인 표시를 클릭 합니다.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

다음과 같이 표시됩니다.

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>샘플 코드
또 다른 방법은 tootest 프로그램 RR 클라이언트 코드에서 시작 됩니다. 클릭 하면 **요청/응답** hello 대시보드 및 스크롤 toohello 아래쪽에 C#, Python 및 오른쪽에 대 한 샘플 코드를 표시 됩니다 Hello 요청 URI, 헤더 및 본문을 포함 하 여 hello RR 요청의 hello 구문이 나타납니다.

이 가이드에서는 작동하는 Python 예제를 보여 줍니다. Toomodify 해야 hello와 **작업 영역**, **서비스**, 및 **api_key** 실험의 합니다.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>BES 끝점 테스트
클릭 **일괄 처리 실행** hello 대시보드 및 스크롤 toohello 아래쪽에 있습니다. C#, Python 및 오른쪽에 대 한 샘플 코드에 표시 됩니다. Hello 구문을 hello BES 요청 toosubmit 작업, 작업 시작, hello 상태 또는 작업의 결과 및 작업 삭제도 나타납니다.

이 가이드에서는 작동하는 Python 예제를 보여 줍니다. Toomodify 필요한 hello와 **작업 영역**, **서비스**, 및 **api_key** 실험의 합니다. 또한 toomodify hello를 할 **저장소 계정 이름**, **저장소 계정 키**, 및 **저장소 컨테이너 이름**합니다. 마지막으로, 해야 toomodify hello 위치의 hello **입력된 파일** 및 hello의 hello 위치 **출력 파일**합니다.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
