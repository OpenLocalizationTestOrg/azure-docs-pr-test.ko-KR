---
title: "Azure Machine Learning 웹 서비스: 배포 및 사용 | Microsoft Docs"
description: "웹 서비스 배포 및 사용을 위한 리소스입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Azure 기계 학습 웹 서비스: 배포 및 사용
웹 서비스로 toodeploy 기계 학습 워크플로에 Azure 기계 학습 및 모델을 사용할 수 있습니다. 이러한 웹 서비스 응용 프로그램에서 사용 되는 toocall hello 기계 학습 모델을 통해 실시간으로 또는 일괄 처리 모드에서 hello 인터넷 toodo 예측 될 수 있습니다. RESTful hello 웹 서비스 이므로, Excel 등의 응용 프로그램 및 다양 한 프로그래밍 언어와.NET 및 Java와 같은 플랫폼에서 호출할 수 있습니다.

다음 섹션에서는 hello 링크 toowalkthroughs, 코드 및 설명서 toohelp 드리겠습니다 제공 합니다.

## <a name="deploy-a-web-service"></a>웹 서비스 배포
### <a name="with-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오 사용
기계 학습 스튜디오 및 hello Microsoft Azure 컴퓨터 학습 웹 서비스 포털 배포 하 고 코드를 작성 하지 않고도 웹 서비스를 관리 하는 데 도움이 됩니다.

hello 다음 링크를 제공 방법에 대 한 일반 정보 toodeploy 새 웹 서비스:

* Toodeploy Azure 리소스 관리자에 기반 하는 새 웹 서비스를 확인 하려면 어떻게 해야 하는 방법에 대 한 개요에 대 한 [새 웹 서비스를 배포](machine-learning-webservice-deploy-a-web-service.md)합니다.
* 방법에 대 한 연습은 toodeploy 웹 서비스 참조 [Azure 기계 학습 웹 서비스를 배포](machine-learning-publish-a-machine-learning-web-service.md)합니다.
* 방법에 대 한 전체 연습은 toocreate 웹 서비스를 배포 하 고, 참조 [연습 1 단계: 기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)합니다.
* 웹 서비스 배포의 특정 예제는 다음을 참조하세요.

  * [5 단계를 연습: hello Azure 기계 학습 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)
  * [웹 toodeploy toomultiple 영역을 서비스 하는 방법](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>웹 서비스 리소스 공급자 API(Azure Resource Manager API) 사용
웹 서비스에 대 한 hello Azure 기계 학습 리소스 공급자 REST API 호출을 사용 하 여 웹 서비스의 배포 및 관리를 수 있습니다. 자세한 내용은 MSDN의 [Machine Learning 웹 서비스(REST)](/rest/api/machinelearning/index) 참조를 참조하세요.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>PowerShell cmdlet 사용
웹 서비스에 대한 Azure 기계 학습 리소스 공급자는 PowerShell cmdlet을 사용하여 웹 서비스의 배포 및 관리를 활성화합니다.

toouse hello cmdlet을 처음에 로그인 해야 tooyour hello PowerShell 환경 내에서 Azure 계정 hello를 사용 하 여 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. 에 익숙한 경우 어떻게 toocall PowerShell 명령 하는 관리자에 기반 리소스를 참조 하십시오 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account)합니다.

tooexport 실험를 사용 하면 예측 [이 샘플 코드](https://github.com/ritwik20/AzureML-WebServices)합니다. Hello 코드에서 hello.exe 파일을 만든 후 입력할 수 있습니다.

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

웹 서비스 JSON 템플릿을 만들고 hello 응용 프로그램을 실행 합니다. toouse hello 템플릿 toodeploy 웹 서비스는 hello 다음 정보를 추가 해야 합니다.

* 저장소 계정 이름 및 키

    어느 hello에서 hello 저장소 계정 이름과 키를 얻을 수 있습니다 [Azure 포털](https://portal.azure.com/) 또는 hello [Azure 클래식 포털](http://manage.windowsazure.com/)합니다.
* 약정 계획 ID

    Hello에서 hello 계획 ID를 가져올 수 있습니다 [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 계획 이름을 클릭 하 고 로그인 하 여 포털입니다.

Hello의 자식으로 toohello JSON 템플릿 추가 *속성* hello로 수준 동일 hello에 노드 *MachineLearningWorkspace* 노드.

예를 들면 다음과 같습니다.

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Hello 다음 문서를 참조 하 고 추가 세부 정보에 대 한 코드 샘플:

* [Azure 기계 학습 Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 참조
* GitHub의 샘플 [연습](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt)

## <a name="consume-hello-web-services"></a>Hello 웹 서비스 사용
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Hello Azure 컴퓨터 학습 웹 서비스 UI (테스트)에서
Hello Azure 컴퓨터 학습 웹 서비스 포털에서 웹 서비스를 테스트할 수 있습니다. 일괄 처리 실행 서비스 (BES) 인터페이스 및 테스트 hello 요청 응답 서비스 (RR)이 있습니다.

* [새 웹 서비스 배포](machine-learning-webservice-deploy-a-web-service.md)
* [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)
* [5 단계를 연습: hello Azure 기계 학습 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>엑셀에서
Hello 웹 서비스를 사용 하는 Excel 서식 파일을 다운로드할 수 있습니다.

* [Excel에서 Azure 기계 학습 웹 서비스 사용](machine-learning-consuming-from-excel.md)
* [Azure 기계 학습 웹 서비스용 Excel 추가 기능](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>REST 기반 클라이언트에서
Azure 기계 학습 웹 서비스는 RESTful API입니다. .NET, Python, R, Java, hello 등과 같은 다양 한 플랫폼에서 이러한 Api를 소비할 수 있는 **사용** hello에 웹 서비스에 대 한 페이지 [Microsoft Azure 컴퓨터 학습 웹 서비스 포털](https://services.azureml.net) 예제가 수 있는 코드를 시작 하세요. 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.
