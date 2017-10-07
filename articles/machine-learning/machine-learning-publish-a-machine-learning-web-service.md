---
title: "기계 학습 웹 서비스 aaaDeploy | Microsoft Docs"
description: "Tooconvert 학습 실험 tooa 예측 실험 하는 방법에 배포를 준비 다음 Azure 기계 학습 웹 서비스로 배포 하기 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Azure 기계 학습 웹 서비스 배포
Azure 기계 학습 하면 toobuild, 테스트 및 예측 분석 솔루션을 배포 합니다.

대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.

* **[학습 실험 만들기]**  -Azure 기계 학습 스튜디오는 tootrain를 사용 하 고 예측 분석을 테스트 하는 시각적 공동 개발 환경을 제공 하는 학습 데이터를 사용 하 여 모델링 합니다.
* **[Tooa 예측 실험으로 변환]**  -기존 데이터와 모델의 학습 및 준비 toouse 하 고 나면 그 tooscore 새 데이터를 준비 하 고 예측에 대 한 실험을 간소화 합니다.
* **[앱 서비스로 배포]** - 예측 실험을 [신규] 또는 [기존] Azure 웹 서비스로 배포할 수 있습니다. 사용자가 데이터 tooyour 모델 보내고 모델의 예측을 받을 수 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>학습 실험 만들기
Azure 기계 학습 스튜디오 toocreate 여기서 포함 다양 한 모듈 tooload 학습 데이터, 필요에 따라 hello 데이터 준비, 기계 학습 알고리즘을 적용 한 hello 결과 평가 학습 실험 사용 tootrain 예측 분석 모델 . 실험을 반복 하 고 다양 한 기계 학습 알고리즘 toocompare 한 hello 결과 평가 합니다.

hello 프로세스 만들기 및 관리 학습 실험의 다른 곳에서 완벽 하 게 적용 됩니다. 자세한 내용은 다음 문서를 참조하세요.

* [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md)
* [Azure 기계 학습을 사용하여 예측 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)
* [Azure 기계 학습 스튜디오에 학습 데이터 가져오기](machine-learning-data-science-import-data.md)
* [Azure 기계 학습 스튜디오에서 반복 실험 관리](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Hello 학습 실험 tooa 예측 실험으로 변환
모델을 학습할 준비 tooconvert 교육 실험를 예측 실험 tooscore 새 데이터에 수 있습니다.

예측 tooa 변환 하 여 실험, 점수 매기기 웹 서비스로 배포 하 여 학습 된 모델을 준비 toobe 가져오는 합니다. 입력된 데이터 tooyour 모델 및 모델 백 hello 예측 결과 기준으로 송신할 hello 웹 서비스 사용자를 보낼 수 있습니다. 변환할 때 예측 tooa 실험, 원하는 다른 사용자가 사용 하 여 모델 toobe 염두에서에 둬야 합니다.

tooconvert 예측 하 여 학습 실험 tooa 실험, 클릭 **실행** hello 실험 캔버스의 hello 맨 아래에 클릭 **웹 서비스 설정**을 선택한 후 **예측 웹 서비스** .

![Tooscoring 실험으로 변환](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

방법에 대 한 자세한 내용은 tooperform이이 변환에서는 참조 [어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델](machine-learning-convert-training-experiment-to-scoring-experiment.md)합니다.

hello 다음 단계에서는 새 웹 서비스로 예측 실험 배포. 또한 기본 웹 서비스로 hello 실험을 배포할 수 있습니다.

## <a name="deploy-it-as-a-web-service"></a>웹 서비스로 배포

새 웹 서비스 또는 기본 웹 서비스로 hello 예측 실험을 배포할 수 있습니다.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>새 웹 서비스로 hello 예측 실험 배포
Hello 예측 실험 준비 했으므로 새 Azure 웹 서비스로 배포할 수 있습니다. Hello 웹 서비스를 사용 하면 데이터 tooyour 모델을 보낼 수 있습니다 및 hello 모델의 예측이 반환 합니다.

toodeploy 실험을 클릭 하면 예측 **실행** 실험 캔버스 hello hello 맨 아래에 있습니다. Hello 실험 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [새로]**합니다.  hello 기계 학습 웹 서비스 포털의 hello 배포 페이지가 열립니다.

> [!NOTE] 
> toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다. 자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Machine Learning 웹 서비스 포털 배포 실험 페이지
Hello 실험 배포 페이지에서 hello 웹 서비스에 대 한 이름을 입력 합니다.
가격 책정 계획을 선택합니다. 기존 가격 책정 계획 선택할 수 있는 경우에 hello 서비스에 대 한 새 가격 계획을 만들어야 그렇지 않으면 합니다.

1. Hello에 **가격 계획** 드롭 다운를 기존 계획을 선택 하거나 선택 hello **선택 새 계획** 옵션입니다.
2. **계획 이름**, 청구서에 hello 계획을 식별 하는 이름을 입력 합니다.
3. Hello 중 하나를 선택 **월별 계획 계층**합니다. hello 계획 계층 toohello 계획 기본 지역 및 웹 서비스에 대 한 기본 배포 toothat 영역입니다.

클릭 **배포** 및 hello **퀵 스타트** 웹 서비스에 대 한 페이지가 열립니다.

hello 웹 서비스 빠른 시작 페이지 하면 액세스 및 지침 hello 웹 서비스를 만든 후 수행할 수는 가장 일반적인 작업에. 여기에서는 hello 테스트 페이지와 페이지 사용을 쉽게 액세스할 수 있습니다.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>새 웹 서비스 테스트
tootest 새 웹 서비스를 클릭 하 여 **웹 서비스를 테스트할** 일반 작업입니다. Hello 테스트 페이지에서 서비스 요청-응답 (RR)으로 웹 서비스 또는 일괄 처리 실행 서비스 (BES)을 테스트할 수 있습니다.

hello RR 테스트 페이지 hello 입력, 출력 및 hello 실험에 정의 된 모든 전역 매개 변수를 표시 합니다. tootest hello 웹 서비스를 수동으로 입력할 수 있습니다 적절 한 값 hello 입력 또는 공급 장치에 대 한 hello 테스트 값을 포함 하는 쉼표로 구분 된 값 (CSV) 형식이 지정 된 파일입니다.

RR을 사용 하 여 tootest hello 목록 뷰 모드에서 hello 입력에 대 한 적절 한 값을 입력 하 고 클릭 **테스트 요청-응답**합니다. 예측 결과 hello 출력 열 toohello 왼쪽에 표시 합니다.

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

tootest 프로그램 BES 클릭 **일괄 처리**합니다. Hello 일괄 처리 테스트 페이지를 사용자의 입력에서 찾아보기를 클릭 하 고 적절 한 샘플 값이 포함 된 CSV 파일을 선택 합니다. CSV 파일에 없는 경우 예측 실험 기계 학습 스튜디오를 사용 하 여 만든 예측 하 여 실험에 대 한 hello 데이터 집합을 다운로드 하 고 사용 하 여 수 있습니다.

toodownload hello 데이터 집합, 기계 학습 스튜디오를 엽니다. 예측 하 여 실험을 열고 마우스 오른쪽 단추로 클릭 하 여 실험에 대 한 hello 입력 합니다. Hello 상황에 맞는 메뉴에서 선택 **dataset** 선택한 후 **다운로드**합니다.

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

**테스트**를 클릭합니다. 일괄 처리 실행 작업의 hello 상태 표시 toohello 권리도 **테스트 일괄 처리 작업이**합니다.

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Hello에 **구성** 페이지 hello 설명, 제목, hello 저장소 계정 키 업데이트를 웹 서비스에 대 한 예제 데이터를 사용 합니다.

![Hello 웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Hello 웹 서비스를 배포 하 고 나면 다음 작업을 수행할 수 있습니다.

* **액세스** hello 웹 서비스 API를 통해 것입니다.
* **관리** 웹 서비스 포털 Azure 기계 학습을 통해 또는 Azure 클래식 포털을 환영 합니다.
* **업데이트** 

#### <a name="access-your-new-web-service"></a>새 웹 서비스 액세스
기계 학습 스튜디오에서 웹 서비스를 배포한 후 데이터 toohello 서비스 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.

hello **사용** 페이지 tooaccess 웹 서비스를 해야 하는 모든 hello 정보를 제공 합니다. 예를 들어 hello API 키를 권한이 tooallow 액세스 toohello 서비스를 제공 합니다.

기계 학습 웹 서비스에 액세스 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

#### <a name="manage-your-new-web-service"></a>새 웹 서비스 관리
새 웹 서비스 Machine Learning 웹 서비스 포털을 관리할 수 있습니다. Hello에서 [포털 기본 페이지](https://services.azureml-test.net/), 클릭 **웹 서비스**합니다. Hello 웹 서비스 페이지에서 삭제 하거나 서비스를 복사할 수 있습니다. 특정 서비스 toomonitor hello 서비스를 클릭 한 다음 클릭 **대시보드**합니다. hello 웹 서비스와 관련 된 toomonitor 일괄 처리 작업이 클릭 **일괄 처리 요청 로그**합니다.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Hello 예측 실험을 기본 웹 서비스로 배포

Hello 예측 실험 충분히 준비 했으므로 클래식 Azure 웹 서비스로 배포할 수 있습니다. Hello 웹 서비스를 사용 하면 데이터 tooyour 모델을 보낼 수 있습니다 및 hello 모델의 예측이 반환 합니다.

toodeploy 실험을 클릭 하면 예측 **실행** hello hello 맨 아래에 캔버스를 실험 하 고 클릭 **웹 서비스 배포**합니다. hello 웹 서비스 설정 및 웹 서비스 대시보드 hello에에서 배치 됩니다.

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>기존 웹 서비스 테스트

Hello 컴퓨터 학습 웹 서비스 포털 또는 기계 학습 스튜디오에서 hello 웹 서비스를 테스트할 수 있습니다.

tootest hello 요청 응답 웹 서비스는 hello 클릭 **테스트** hello 웹 서비스 대시보드에서 단추입니다. 대화 상자가 표시 tooask 있습니다 hello hello 서비스에 대 한 입력된 데이터에 대 한 합니다. 이들은 실험 점수 매기기 hello에 필요한 hello 열입니다. 데이터 집합을 입력하고 **확인**을 클릭합니다. hello 웹 서비스에 의해 생성 된 hello 결과 hello hello 대시보드 맨 아래에 표시 됩니다.

Hello를 클릭할 수 있는 **테스트** hello 새 웹 서비스 섹션에서에서 이전에 표시 된 것 처럼 링크 tootest hello Azure 컴퓨터 학습 웹 서비스 포털에서 서비스를 미리 합니다.

tootest hello 배치 실행 서비스 클릭 **테스트** 미리 보기 링크 합니다. Hello 일괄 처리 테스트 페이지를 사용자의 입력에서 찾아보기를 클릭 하 고 적절 한 샘플 값이 포함 된 CSV 파일을 선택 합니다. CSV 파일에 없는 경우 예측 실험 기계 학습 스튜디오를 사용 하 여 만든 예측 하 여 실험에 대 한 hello 데이터 집합을 다운로드 하 고 사용 하 여 수 있습니다.

![Hello 웹 서비스 테스트](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Hello에 **구성** 페이지 hello 서비스의 hello 표시 이름을 변경 하 고 설명을 부여할 수 있습니다. hello 이름 및 설명을 hello에 표시 됩니다 [Azure 클래식 포털](http://manage.windowsazure.com/) 웹 서비스를 관리 하는 위치입니다.

**입력 스키마**, **출력 스키마** 및 **웹 서비스 매개 변수**의 각 열에 문자열을 입력하여 입력 데이터, 출력 데이터 및 웹 서비스 매개 변수에 대한 설명을 제공할 수 있습니다. 이러한 설명은 hello 웹 서비스에 대해 제공 하는 hello 샘플 코드 설명서에 사용 됩니다.

웹 서비스에 액세스할 때 표시 되는 모든 오류 로깅 toodiagnose를 사용할 수 있습니다. 자세한 내용은 [기계 학습 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.

![Hello 웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

또한 Azure 컴퓨터 학습 웹 서비스 포털 비슷한 toohello 프로시저 hello 새 웹 서비스 섹션의에서 앞에 표시 된 hello에 hello 웹 서비스에 대 한 hello 끝점을 구성할 수 있습니다. hello 옵션은 서로 다른, 추가 하거나 hello 서비스 설명, 로깅 사용 및 테스트에 대 한 사용 샘플 데이터를 변경할 수 있습니다.

#### <a name="access-your-classic-web-service"></a>기존 웹 서비스 액세스
기계 학습 스튜디오에서 웹 서비스를 배포한 후 데이터 toohello 서비스 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.

hello 대시보드 tooaccess 웹 서비스를 원하는 모든 hello 정보를 제공 합니다. 예를 들어 hello API 키에는 tooallow 액세스 toohello 서비스에 권한이 있고 API 도움말 페이지 코드 작성을 시작 하려면 toohelp 제공 제공 됩니다.

기계 학습 웹 서비스에 액세스 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

#### <a name="manage-your-classic-web-service"></a>기존 웹 서비스 관리
다양 한 작업의 toomonitor 웹 서비스를 수행할 수 있습니다. 업데이트 및 삭제할 수 있습니다. 배포할 때 만들어지는 추가 toohello 기본 끝점에 추가 끝점 tooa 클래식 웹 서비스를 추가할 수도 있습니다.

자세한 내용은 참조 [는 Azure 기계 학습 작업 영역을 관리](machine-learning-manage-workspace.md) 및 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Hello 웹 서비스를 업데이트 합니다.
Hello 모델 추가 학습 데이터로 업데이트 하는 등 tooyour 웹 서비스를 변경할 수 있으며 덮어쓰지 hello 원래 웹 서비스를 다시 배포.

tooupdate hello 웹 서비스 toodeploy hello 웹 서비스를 사용한 예측 실험 원래 hello를 열고 클릭 하 여 편집 가능한 복사본을 만들 **SAVE AS**합니다. 변경한 다음 **웹 서비스 배포**를 클릭합니다.

하기 전에이 실험을 배포한 때문에 toooverwrite (클래식 웹 서비스) 또는 업데이트 (새 웹 서비스) hello 기존 서비스 묻는 메시지가 표시 됩니다. 클릭 하면 **예** 또는 **업데이트** hello 기존 웹 서비스를 중지 하 고 배포 hello 새 예측 실험 그 자리에 배포 됩니다.

> [!NOTE]
> Hello 원래 웹 서비스의 구성을 변경 하는 경우 예를 들어 새로운 표시 이름이 나 설명, 입력 값이 필요 합니다 tooenter 이러한 다시 합니다.
> 
> 

웹 서비스를 업데이트 하기 위한 한 가지 옵션은 프로그래밍 방식으로 tooretrain hello 모델입니다. 자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.

<!-- internal links -->
[학습 실험 만들기]: #create-a-training-experiment
[Tooa 예측 실험으로 변환]: #convert-the-training-experiment-to-a-predictive-experiment
[앱 서비스로 배포]: #deploy-it-as-a-web-service
[신규]: #deploy-the-predictive-experiment-as-a-new-Web-service
[기존]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
