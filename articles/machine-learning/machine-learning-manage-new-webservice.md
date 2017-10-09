---
title: "aaaUse hello Azure 컴퓨터 학습 웹 서비스 포털 | Microsoft Docs"
description: "액세스 tooAzure 기계 학습 작업 영역, 관리 및 배포 하 고 기계 학습 API 웹 서비스 관리"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리
Hello Microsoft Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 컴퓨터 학습 새로 추가 되거나 기존의 웹 서비스를 관리할 수 있습니다. 기존 웹 서비스와 새 웹 서비스는 서로 다른 기본 기술에 기반하고 있으므로 서비스 각각에는 약간씩 다른 관리 기능이 있습니다.

Hello 컴퓨터 학습 웹 서비스 포털에서 다음을 수행할 수 있습니다.

* Hello 웹 서비스 사용 되는 방식을 모니터링 합니다.
* Hello 설명 구성 hello 웹에 대 한 hello 키를 업데이트 합니다 (새로만 해당) 서비스, 사용자 저장소 계정 키 (새로만 해당), 로깅 사용, 업데이트 및 사용 하도록 설정 또는 샘플 데이터를 사용 하지 않도록 설정 합니다.
* Hello 웹 서비스를 삭제 합니다.
* 청구 계획을 만들거나 삭제하거나 업데이트합니다(새 서비스에만 해당).
* 끝점을 추가하거나 삭제 합니다(기존 서비스에만 해당).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>사용 권한 toomanage 새 리소스 관리자 기반 웹 서비스

새 웹 서비스는 Azure 리소스로 배포됩니다. 이와 같이 hello 올바른 사용 권한이 toodeploy 고 해야 새 웹 서비스를 관리 합니다.  toodeploy 참가자를 할당 해야 하는 새 웹 서비스를 관리 또는 hello 구독 toowhich hello 웹 서비스에 대 한 관리자 역할을 배포 합니다. 다른 사용자 tooa 기계 학습 작업 영역을 초대 배포 하거나 웹 서비스를 관리 하려면 해당를 tooa 참가자 또는 관리자 역할 hello 구독에 할당 해야 있습니다. 

Hello 사용자 hello Azure 컴퓨터 학습 웹 서비스 포털에서 사용 권한을 tooaccess 리소스를 수정 하는 hello 없으면 toodeploy 웹 서비스는 동안 다음 오류가 hello를 받게 됩니다.

*웹 서비스 배포에 실패했습니다. 이 계정에는 충분 한 액세스 toohello hello 작업 영역을 포함 하는 Azure 구독이 없습니다. 순서 대로 toodeploy 웹 서비스 tooAzure, 동일한 계정 이어야 합니다 hello toohello 작업 영역을 초대 그리고 hello 작업 영역 포함 된 지정 된 액세스 toohello Azure 구독 수 있습니다.*

작업 영역을 만드는 방법에 대한 자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.

액세스 권한 설정에 대 한 자세한 내용은 참조 하십시오. [hello Azure 포털-공개 미리 보기의에서 사용자 및 그룹에 대 한 보기 액세스 할당](../active-directory/role-based-access-control-manage-assignments.md)합니다.


## <a name="manage-new-web-services"></a>새 웹 서비스 관리
toomanage 새 웹 서비스:

1. Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) Microsoft Azure 계정-연결 된 hello 계정 사용을 사용 하 여 포털 hello Azure 구독.
2. Hello 메뉴를 클릭 **웹 서비스**합니다.

그러면 구독에 배포된 웹 서비스의 목록이 표시됩니다. 

toomanage 웹 서비스를 웹 서비스를 클릭 합니다. Hello 웹 서비스 페이지에서 다음을 수행할 수 있습니다.

* Hello 웹 서비스 toomanage 클릭 것입니다.
* 웹 서비스 tooupdate hello에 대 한 대금 청구 계획 hello 클릭 것입니다.
* 웹 서비스를 삭제합니다.
* 웹 서비스 복사한 tooanother 영역을 배포 합니다.

웹 서비스를 클릭 하면 hello 웹 서비스 빠른 시작 페이지가 열립니다. hello 웹 서비스 빠른 시작 페이지에는 웹 서비스 toomanage를 허용 하는 두 가지 메뉴 옵션이 있습니다.

* **대시보드** -tooview 웹 서비스 사용을 허용 합니다.
* **구성** -웹 서비스 hello와 연결 된 hello 저장소 계정에 대 한 업데이트 hello 키 tooadd 설명 텍스트를 허용 하 고 사용 하도록 설정 하거나 예제 데이터를 사용 하지 않도록 설정 합니다.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Hello 웹 서비스 사용 되는 방식을 모니터링
Hello 클릭 **대시보드** 탭 합니다.

Hello 대시보드에서 시간 동안 웹 서비스의 전반적인 사용량을 볼 수 있습니다. Hello 기간 tooview hello hello 사용 현황 차트의 오른쪽 위에 있는 hello 기간 드롭다운 메뉴에서 선택할 수 있습니다. hello 대시보드 hello 다음 정보를 보여 줍니다.

* **시간에 따른 요청** hello 특정 기간을 통해 요청 hello 수 단계 그래프를 표시 합니다. 사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.
* **요청-응답 요청** hello hello 서비스 hello 선택한 기간 및 그 중 실패 한를 통해 수신한 요청-응답 호출의 총 수를 표시 합니다.
* **평균 시간을 계산 하는 요청-응답** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.
* **일괄 처리 요청** 표시 hello의 총 일괄 처리 요청 hello 서비스 기간을 선택 하는 hello를 통해을 얼마나 많이 실패 했습니다.
* **평균 작업 대기 시간** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.
* **오류** toohello 웹 서비스 호출에서 발생 한 오류를 hello 집계 수를 표시 합니다.
* **서비스 비용** hello 서비스와 연결 된 hello 청구 계획에 대 한 hello 요금을 표시 합니다.

### <a name="configuring-hello-web-service"></a>Hello 웹 서비스 구성
Hello 클릭 **구성** 메뉴 옵션입니다.

Hello 다음과 같은 속성을 업데이트할 수 있습니다.

* **설명** tooenter hello 웹 서비스에 대 한 설명이 있습니다.
* **제목** tooenter hello 웹 서비스에 대 한 title 있습니다
* **키** toorotate 사용 하면 기본 및 보조 API 키입니다.
* **저장소 계정 키** hello 웹 서비스 변경과 관련 된 hello 저장소 계정에 대 한 tooupdate hello 키 있습니다. 
* **예제 데이터 사용** tooprovide 예제 데이터 tootest hello 요청 응답 서비스를 사용할 수 있습니다. 기계 학습 스튜디오에서 hello 웹 서비스를 만든 경우 hello 예제 데이터에서에서 가져온 것 hello 데이터에 사용 되는 tootrain 모델입니다. Hello 서비스를 프로그래밍 방식으로 만든 경우 hello 데이터 hello JSON 패키지의 일부로 제공 하는 hello 예제 데이터에서 가져옵니다.

### <a name="managing-billing-plans"></a>청구 계획 관리
Hello 클릭 **계획** hello 웹 서비스 빠른 시작 페이지에서 메뉴 옵션입니다. 계획 하는 특정 웹 서비스 toomanage와 연결 된 hello 계획을 선택할 수도 있습니다.

* **새** toocreate 새 계획을 사용 하면 됩니다.
* **추가/제거 계획 인스턴스** 사용 하면 너무 "확장" 하 여 기존 계획 tooadd 용량이 있습니다.
* **업그레이드/다운 그레이드** 사용 하면 너무 "확장" 하 여 기존 계획 tooadd 용량이 있습니다.
* **삭제** toodelete 계획 수 있습니다.

계획 tooview 대시보드를 클릭 합니다. hello 대시보드에서 선택한 기간 동안 스냅숏 또는 계획 사용량을 보이도록합니다. tooselect 시간 기간 tooview hello, hello 클릭 **기간** hello 대시보드의 오른쪽 위에서 드롭다운에서 합니다. 

계획 대시보드 hello hello를 다음 정보를 제공 합니다.

* **계획 설명** hello 비용과 hello 계획과 연결 된 용량에 대 한 정보를 표시 합니다.
* **사용을 계획** hello 트랜잭션과 hello 계획에 따라 요금이 청구 되었다는 계산 시간 수를 표시 합니다.
* **웹 서비스** 이 계획을 사용 하는 웹 서비스의 hello 수를 표시 합니다.
* **웹 서비스 호출 하 여 상위** hello 계획에 따라 부과 된 호출 하는 hello 상위 4 개 웹 서비스를 표시 합니다.
* **계산 시간 기준으로 웹 서비스를 상위** hello 계획에 따라 요금이 청구 되는 계산 리소스를 사용 하는 hello 상위 4 개 웹 서비스를 표시 합니다.

## <a name="manage-classic-web-services"></a>기존 웹 서비스 관리
> [!NOTE]
> 이 섹션의 절차에서는 hello는 hello Azure 컴퓨터 학습 웹 서비스 포털을 통해 관련 toomanaging 클래식 웹 서비스입니다. 클래식 웹 관리에 대 한 내용은 서비스를 통해 기계 학습 스튜디오 hello 및 hello Azure 클래식 포털에서 참조 [는 Azure 기계 학습 작업 영역을 관리](machine-learning-manage-workspace.md)합니다.
> 
> 

toomanage 클래식 웹 서비스:

1. Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) Microsoft Azure 계정-연결 된 hello 계정 사용을 사용 하 여 포털 hello Azure 구독.
2. Hello 메뉴를 클릭 **웹 서비스를 클래식**합니다.

웹 서비스를 클래식 toomanage 클릭 **웹 서비스를 클래식**합니다. Hello 클래식 웹 서비스 페이지에서 다음을 수행할 수 있습니다.

* Hello 웹 서비스 tooview hello 연결 된 끝점을 클릭 합니다.
* 웹 서비스를 삭제합니다.

기존의 웹 서비스를 관리 하는 경우 사용 하면 각 hello 끝점 별도로 관리할 합니다. Hello 웹 서비스 페이지에서 웹 서비스를 클릭 하면 hello hello 서비스와 연결 된 끝점 목록이 열립니다. 

Hello 클래식 웹 서비스 끝점 페이지에 추가 하 고 hello 서비스에 끝점을 삭제할 키를 누릅니다. 끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.

Hello 끝점 tooopen hello 웹 서비스 빠른 시작 페이지 중 하나를 클릭 합니다. Hello 빠른 시작 페이지에서 옵션에는 두 가지 메뉴 toomanage 수 있는 웹 서비스

* **대시보드** -tooview 웹 서비스 사용을 허용 합니다.
* **구성** -tooadd 설명 텍스트를 사용 하면 오류 로깅을 켜고, 업데이트 hello 키 웹 서비스 hello와 관련 된 hello 저장소 계정에 대해 사용 하도록 설정 하 고 예제 데이터를 사용 하지 않도록 설정 합니다.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Hello 웹 서비스 사용 되는 방식을 모니터링
Hello 클릭 **대시보드** 탭 합니다.

Hello 대시보드에서 시간 동안 웹 서비스의 전반적인 사용량을 볼 수 있습니다. Hello 기간 tooview hello hello 사용 현황 차트의 오른쪽 위에 있는 hello 기간 드롭다운 메뉴에서 선택할 수 있습니다. hello 대시보드 hello 다음 정보를 보여 줍니다.

* **시간에 따른 요청** hello 특정 기간을 통해 요청 hello 수 단계 그래프를 표시 합니다. 사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.
* **요청-응답 요청** hello hello 서비스 hello 선택한 기간 및 그 중 실패 한를 통해 수신한 요청-응답 호출의 총 수를 표시 합니다.
* **평균 시간을 계산 하는 요청-응답** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.
* **일괄 처리 요청** 표시 hello의 총 일괄 처리 요청 hello 서비스 기간을 선택 하는 hello를 통해을 얼마나 많이 실패 했습니다.
* **평균 작업 대기 시간** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.
* **오류** toohello 웹 서비스 호출에서 발생 한 오류를 hello 집계 수를 표시 합니다.
* **서비스 비용** hello 서비스와 연결 된 hello 청구 계획에 대 한 hello 요금을 표시 합니다.

### <a name="configuring-hello-web-service"></a>Hello 웹 서비스 구성
Hello 클릭 **구성** 메뉴 옵션입니다.

Hello 다음과 같은 속성을 업데이트할 수 있습니다.

* **설명** tooenter hello 웹 서비스에 대 한 설명이 있습니다. 설명은 필수 필드입니다.
* **로깅** hello 끝점에 대 한 로깅을 tooenable 또는 사용 안 함 오류가 있습니다. 로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.
* **예제 데이터 사용** tooprovide 예제 데이터 tootest hello 요청 응답 서비스를 사용할 수 있습니다. 기계 학습 스튜디오에서 hello 웹 서비스를 만든 경우 hello 예제 데이터에서에서 가져온 것 hello 데이터에 사용 되는 tootrain 모델입니다. Hello 서비스를 프로그래밍 방식으로 만든 경우 hello 데이터 hello JSON 패키지의 일부로 제공 하는 hello 예제 데이터에서 가져옵니다.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>허용 또는 hello 포털에서 사용자에 대 한 액세스 tooWeb 서비스를 일시 중단
Hello Azure 클래식 포털을 사용 하 여, 허용 하거나 toospecific 사용자 액세스를 거부할 수 있습니다.

### <a name="access-for-users-of-new-web-services"></a>새 웹 서비스 사용자의 액세스
tooenable hello Azure 컴퓨터 학습 웹 서비스 포털에서 웹 서비스와 다른 사용자가 toowork에 추가 해야 공동 관리자와 Azure 구독에 있습니다.

Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) Microsoft Azure를 사용 하 여 계정-Azure 구독 hello와 관련 된 hello 계정을 사용 합니다.

1. Hello 탐색 창에서 클릭 **설정**, 클릭 **관리자**합니다.
2. Hello hello 창의 아래쪽에 있는 클릭 **추가**합니다. 
3. Hello A 공동 관리자 추가 대화 상자, 공동 관리자 및 공동 관리자 tooaccess hello를 선택한 후 hello 구독으로 tooadd 원하는 hello 사람의 hello 전자 메일 주소를 입력 합니다.
4. **Save**를 클릭합니다.

### <a name="access-for-users-of-classic-web-services"></a>기존 웹 서비스 사용자의 액세스
작업 영역 toomanage:

Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) Microsoft Azure를 사용 하 여 계정-Azure 구독 hello와 관련 된 hello 계정을 사용 합니다.

1. Hello Microsoft Azure 서비스 패널에서 **기계 학습**합니다.
2. 원하는 toomanage hello 작업 영역을 클릭 합니다.
3. Hello 클릭 **구성** 탭 합니다.

Hello 구성 탭에서 일시 중지할 수 있습니다 액세스 toohello 기계 학습 작업 영역을 클릭 하 여 **DENY**합니다. 사용자가 더 이상 기계 학습 스튜디오에서 수 tooopen hello 작업 영역 됩니다. toorestore 액세스 클릭 **허용**합니다.

toospecific 사용자:

기계 학습 스튜디오에서 작업 한 toohello 영역 액세스 권한이 있는 toomanage 추가 계정을 클릭 **로그인 tooML Studio** hello에 **대시보드** 탭 합니다. 작업 영역을 hello 기계 학습 스튜디오에서 열립니다. 여기에서 클릭 hello **설정** 탭 한 다음 **사용자**합니다. 클릭할 수 있는 **더 사용자 초대** toogive 사용자 toohello 작업 영역 액세스 또는 사용자 선택 하 고 클릭 **제거**합니다.

> [!NOTE]
> hello **로그인 tooML Studio** 링크 hello 현재 로그인 하는 Microsoft 계정을 사용 하 여 기계 학습 스튜디오를 엽니다. hello toosign toohello Azure 클래식 포털 toocreate 작업 영역에서에서 사용한 Microsoft 계정에 자동으로 없는 권한 tooopen 작업 영역을 합니다. 작업 영역에서 tooopen toohello hello 영역의 hello 소유자로 정의 된 Microsoft 계정에에서 서명 해야 하거나 tooreceive hello 소유자 toojoin hello 작업 영역에서 초대장이 필요 합니다.
> 
> 

