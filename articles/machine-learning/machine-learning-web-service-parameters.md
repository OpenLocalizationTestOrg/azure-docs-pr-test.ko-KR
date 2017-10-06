---
title: "Azure 컴퓨터 학습 웹 서비스 매개 변수가 aaaUse | Microsoft Docs"
description: "어떻게 toouse Azure 컴퓨터 학습 웹 서비스 매개 변수가 toomodify hello hello 웹 서비스에 액세스할 때 모델의 동작입니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Azure 기계 학습 웹 서비스 매개 변수 사용
Azure 기계 학습 웹 서비스는 구성 가능한 매개 변수로 모듈이 포함된 실험을 게시하여 만듭니다. 경우에 따라 hello 웹 서비스가 실행 중인 동안 toochange hello 모듈 동작을 원하는 수 있습니다. *웹 서비스 매개 변수* toodo 사용 하면이 작업 합니다. 

일반적인 예로 hello를 설정 하 고 [데이터 가져오기] [ reader] 모듈의 hello 해당 hello 사용자 웹 서비스 게시 hello 웹 서비스에 액세스할 때 다른 데이터 원본을 지정할 수 있습니다. Hello 구성 또는 [데이터 내보내기] [ writer] 모듈 다른 위치를 지정할 수 있도록 합니다. 다른 몇 가지 예를 들어 hello hello에 대 한 비트 수를 변경 [기능 해시] [ feature-hashing] hello에 대 한 원하는 기능의 수를 모듈 또는 hello [필터 기반 기능 선택] [ filter-based-feature-selection] 모듈입니다. 

실험에서 웹 서비스 매개 변수를 설정하여 하나 이상의 모듈 매개 변수와 연결하고 이러한 매개 변수가 필수인지 또는 선택 사항인지 지정할 수 있습니다. 다음 hello 웹 서비스의 hello 사용자 hello 웹 서비스를 호출할 때 이러한 매개 변수에 대해 값을 제공할 수 있습니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>어떻게 tooset 및 사용 하 여 웹 서비스 매개 변수
Hello 아이콘 다음 toohello 매개 변수는 모듈에 대 한 "웹 서비스 매개 변수로 설정"을 선택 하 여 웹 서비스 매개 변수를 정의 합니다. 이렇게 하면 새 웹 서비스 매개 변수를 만들고이 toothat: 모듈 매개 변수를 연결 합니다. 그런 다음 hello 웹 서비스에 액세스 하는 hello 사용자는 웹 서비스 매개 변수 hello에 대 한 값을 지정할 수 있습니다 및 적용 된 toohello 모듈 매개 변수입니다.

사용 가능한 tooany는 웹 서비스 매개 변수를 정의한 다음 다른: hello 실험에서 모듈 매개 변수입니다. 동일한 웹 서비스 매개 변수가 hello 매개 변수 예상 값 같은 유형의으로 hello로 하나의 모듈에 대 한 매개 변수와 연결 된 웹 서비스 매개 변수를 정의 하는 경우, 다른 모듈에 대 한 사용할 수 있습니다. 예를 들어 hello 웹 서비스 매개 변수는 숫자 값 이면 다음만 사용할 수 있습니다에 대 한 숫자 값을 예상 하는 모듈 매개 변수입니다. Hello 사용자 웹 서비스 매개 변수 hello에 대 한 값을 설정 하는 경우 관련 된 적용된 tooall 모듈 매개 변수를 됩니다.

결정할 수 tooprovide 기본 hello 웹 서비스 매개 변수 값 여부. 다음 hello를 매개 변수는 hello 웹 서비스의 hello 사용자에 대 한 선택 사항. 기본값을 제공 하지 않으면, 다음 hello 사용자가 필요한 tooenter 값 hello 웹 서비스에 액세스 합니다.

hello hello 웹 서비스에 대 한 API 설명서에는 어떻게 toospecify hello 웹 서비스 매개 변수 프로그래밍 방식으로 hello 웹 서비스에 액세스할 때에 hello 웹 서비스 사용자에 대 한 정보가 포함 됩니다.

> [!NOTE]
> 클래식 웹 서비스는 hello를 통해 제공 됩니다에 대 한 API 설명서 hello **API 도움말 페이지** hello 웹 서비스에서 링크 **대시보드** 기계 학습 스튜디오에서. 새 웹 서비스는 hello를 통해 제공 됩니다에 대 한 API 설명서 hello [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/Quickstart) hello에 포털 **사용** 및 **Swagger API** 페이지에 대 한 사용자 웹 서비스입니다.
> 
> 

## <a name="example"></a>예제
예를 들어 있다고 가정해를 실험 한 [데이터 내보내기] [ writer] 정보 tooAzure blob 저장소에서 전송 하는 모듈입니다. 여기서 "Blob 경로" 라는 웹 서비스 매개 변수는 hello 서비스에 액세스할 때 hello 웹 서비스 사용자 toochange hello 경로 toohello blob 저장소 수 있도록 합니다.

1. 기계 학습 스튜디오에서 클릭 hello [데이터 내보내기] [ writer] 모듈 tooselect 것입니다. 해당 속성이 hello 속성 창 toohello hello 실험 캔버스의 오른쪽에 표시 됩니다.
2. Hello 저장소 유형을 지정 합니다.
   
   * **데이터 대상 지정**에서 "Azure Blob 저장소"를 선택합니다.
   * **인증 유형 지정**에서 "계정"을 선택합니다.
   * Hello Azure blob 저장소에 대 한 hello 계정 정보를 입력 합니다. 
     <p />
3.Hello 아이콘 toohello hello의 오른쪽 클릭 **tooblob 컨테이너 매개 변수와 함께 시작 하는 경로**합니다. 다음과 같이 표시됩니다.
   
   ![웹 서비스 매개 변수 아이콘][icon]
   
   "웹 서비스 매개 변수로 설정"을 선택합니다.
   
   아래 항목에 추가 되 **웹 서비스 매개 변수가** hello hello 이름 "경로 tooblob 시작으로 컨테이너" hello 속성 창 맨 아래에 있습니다. 이것은 웹 서비스 매개 변수는 이제를 hello와 연결 된 [데이터 내보내기] [ writer] : 모듈 매개 변수입니다.
4. toorename 웹 서비스 매개 변수를 hello hello 이름, "Blob 경로"를 입력을 hello 키를 누릅니다 **Enter** 키입니다. 
5. tooprovide hello 웹 서비스 매개 변수 기본값을 클릭 hello 아이콘 toohello hello 이름 오른쪽의 "기본값을 제공 합니다.", "(예:" container1/output1.csv), 값을 입력 하 고 선택한 hello 키를 누릅니다 **Enter** 키입니다.
   
   ![웹 서비스 매개 변수][parameter]
6. **실행**을 클릭합니다. 
7. 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]** toodeploy hello 웹 서비스입니다.

> [!NOTE] 
> toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

hello 웹 서비스의 hello 사용자 hello에 대 한 새 대상을 지정할 수 [데이터 내보내기] [ writer] hello 웹 서비스에 액세스할 때 모듈입니다.

## <a name="more-information"></a>자세한 정보
더 자세한 예제를 보려면 hello [웹 서비스 매개 변수가](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) hello에 항목 [기계 학습 블로그](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)합니다.

기계 학습 웹 서비스 액세스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

