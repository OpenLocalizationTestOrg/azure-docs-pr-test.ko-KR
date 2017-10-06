---
title: "aaaConnect tooa 기계 학습 웹 서비스 | Microsoft Docs"
description: "C# 또는 Python으로 tooan 인증 키를 사용 하 여 Azure 컴퓨터 학습 웹 서비스를 연결 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Tooan Azure 기계 학습 웹 서비스를 연결 합니다.
Azure 기계 학습 개발자 환경 hello 입력된 데이터를 실시간으로 또는 일괄 처리 모드에서에서 웹 서비스 API toomake 예측입니다. Azure 기계 학습 스튜디오 toocreate 예측을 사용 하 고 Azure 컴퓨터 학습 웹 서비스를 배포 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

방법에 대 한 toolearn toocreate 기계 학습 스튜디오를 사용 하 여 컴퓨터 학습 웹 서비스 및 배포:

* 기계 학습 스튜디오에서 실험 참조 하는 toocreate 방법에 대 한 자습서 [첫 번째 실험 만들기](machine-learning-create-experiment.md)합니다.
* 방법에 대 한 자세한 내용은 toodeploy 웹 서비스 참조 [컴퓨터 학습 웹 서비스를 배포](machine-learning-publish-a-machine-learning-web-service.md)합니다.
* 기계 학습에 대 한 자세한 내용은 일반적으로 hello 방문 [기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.

## <a name="azure-machine-learning-web-service"></a>Azure Machine Learning 웹 서비스
Hello Azure 컴퓨터 학습 웹 서비스와 외부 응용 프로그램은 실시간으로 기계 학습 워크플로 점수 매기기 모델와 통신합니다. 컴퓨터 학습 웹 서비스 호출 tooan 외부 응용 프로그램 예측 결과 반환합니다. 컴퓨터 학습 웹 서비스 호출 toomake 예측을 배포할 때 생성 되는 API 키를 전달 합니다. hello 컴퓨터 학습 웹 서비스 나머지 부분에서는 웹 프로그래밍 프로젝트에 대 한 인기 있는 아키텍처 선택권을 기반으로 합니다.

Azure 기계 학습에는 다음 두 가지 유형의 서비스가 있습니다.

* 서비스 요청-응답 (RR)-짧은 대기 시간, toohello 상태 비저장 모델을 만들고 배포한 hello 기계 학습 스튜디오에서에서 인터페이스를 제공 하는 확장성이 높은 서비스입니다.
* BES(일괄 처리 실행 서비스) – 데이터 레코드의 점수를 일괄적으로 매기는 비동기 서비스입니다.

Machine Learning 웹 서비스에 대한 자세한 내용은 [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

## <a name="get-an-azure-machine-learning-authorization-key"></a>Azure 기계 학습 권한 부여 키 가져오기
실험을 배포 하면 hello 웹 서비스에 대 한 API 키가 생성 됩니다. 여러 위치에서 hello 키를 검색할 수 있습니다.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Hello Microsoft Azure 컴퓨터 학습 웹 서비스 포털에서
Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 포털입니다.

새 컴퓨터 학습 웹 서비스에 대 한 tooretrieve hello API 키:

1. Hello Azure 컴퓨터 학습 웹 서비스 포털에서 클릭 **웹 서비스** hello 상단 메뉴.
2. Tooretrieve hello 키 원하는 hello 웹 서비스를 클릭 합니다.
3. Hello 상단 메뉴에서 클릭 **사용**합니다.
4. 복사 하 고 hello 저장 **기본 키**합니다.

클래식 컴퓨터 학습 웹 서비스에 대 한 tooretrieve hello API 키:

1. Hello Azure 컴퓨터 학습 웹 서비스 포털에서 클릭 **웹 서비스를 클래식** hello 상단 메뉴.
2. 작업 중인 hello 웹 서비스를 클릭 합니다.
3. Tooretrieve hello 키 원하는 hello 끝점을 클릭 합니다.
4. Hello 상단 메뉴에서 클릭 **사용**합니다.
5. 복사 하 고 hello 저장 **기본 키**합니다.

### <a name="classic-web-service"></a>기존 웹 서비스
 기계 학습 스튜디오 또는 hello Azure 클래식 포털에서 기존 웹 서비스에 대 한 키를 검색할 수도 있습니다.

#### <a name="machine-learning-studio"></a>Machine Learning 스튜디오
1. 기계 학습 스튜디오에서 클릭 **웹 서비스** hello 왼쪽에 있습니다.
2. 웹 서비스를 클릭합니다. hello **API 키** hello에 **대시보드** 탭 합니다.

#### <a name="azure-classic-portal"></a>Azure 클래식 포털
1. 클릭 **기계 학습** hello 왼쪽에 있습니다.
2. 웹 서비스의 위치를 가리키는 hello 작업 영역을 클릭 합니다.
3. **웹 서비스**를 클릭합니다.
4. 웹 서비스를 클릭합니다.
5. 끝점을 클릭합니다. hello "API 키" hello 오른쪽 아래에서 다운 되었습니다.

## <a id="connect"></a>Tooa 컴퓨터 학습 웹 서비스 연결
Tooa HTTP 요청 및 응답을 지 원하는 모든 프로그래밍 언어를 사용 하 여 컴퓨터 학습 웹 서비스를 연결할 수 있습니다. Machine Learning 웹 서비스 도움말 페이지에서 C#, Python 및 R로 작성된 예제를 볼 수 있습니다.

**Machine Learning API 도움말** 웹 서비스를 배포하면 Machine Learning API 도움말이 생성됩니다. [Azure 기계 학습 연습 - 웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.
hello 컴퓨터 학습 API 도움말 예측 웹 서비스에 대 한 세부 정보를 포함합니다.

1. 작업 중인 hello 웹 서비스를 클릭 합니다.
2. Hello 끝점 원하는 tooview hello API 도움말 페이지를 클릭 합니다.
3. Hello 상단 메뉴에서 클릭 **사용**합니다.
4. 클릭 **API 도움말 페이지** hello 요청-응답 또는 일괄 처리 실행 끝점 중 하나입니다.

**새 웹 서비스에 대 한 tooview 컴퓨터 학습 API 도움말**

hello Azure 컴퓨터 학습 웹 서비스 포털:

1. 클릭 **웹 서비스** hello 최상위 메뉴에 있습니다.
2. Tooretrieve hello 키 원하는 hello 웹 서비스를 클릭 합니다.

클릭 **사용** tooget 요청 Reposonse hello 및 C#, R, 및 Python에서 일괄 처리 실행 서비스 및 샘플 코드에 대 한 Uri를 hello 합니다.

클릭 **Swagger API** tooget hello에서 호출 Api hello에 대 한 설명서를 기반으로 하는 Swagger Uri를 제공 합니다.

### <a name="c-sample"></a>C# 샘플
tooconnect tooa 컴퓨터 학습 웹 서비스를 사용 하 여 프로그램 **HttpClient** ScoreData 전달 합니다. ScoreData FeatureVector를 숫자 기능 ScoreData hello를 나타내는 경우 n 차원 벡터를 포함 합니다. API 키를 가진 toohello 기계 학습 서비스를 인증합니다.

tooconnect tooa 컴퓨터 학습 웹 서비스 hello **Microsoft.AspNet.WebApi.Client** NuGet 패키지를 설치 해야 합니다.

**Visual Studio에서 Microsoft.AspNet.WebApi.Client NuGet 설치**

1. UCI에서 hello 다운로드 데이터 집합 게시: 성인 2 클래스 dataset 웹 서비스입니다.
2. **도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 클릭합니다.
3. **Install-Package Microsoft.AspNet.WebApi.Client**를 선택합니다.

**toorun hello 코드 샘플**

1. 게시 "예제 1: UCI에서 데이터 집합 다운로드: 성인 2 클래스의 데이터 집합" 실험, hello 기계 학습 예제 컬렉션의 일부입니다.
2. 웹 서비스에서 hello 키를 가진 apiKey를 할당 합니다. 위의 **Azure 기계 학습 권한 부여 키 가져오기** 를 참조하세요.
3. ServiceUri hello 요청 URI로 할당 합니다.

### <a name="python-sample"></a>Python 샘플
tooconnect tooa 컴퓨터 학습 웹 서비스를 사용 하 여 hello **urllib2** 라이브러리 ScoreData 전달 합니다. ScoreData FeatureVector를 숫자 기능 ScoreData hello를 나타내는 경우 n 차원 벡터를 포함 합니다. API 키를 가진 toohello 기계 학습 서비스를 인증합니다.

**toorun hello 코드 샘플**

1. 배포 "예제 1: UCI에서 데이터 집합 다운로드: 성인 2 클래스의 데이터 집합" 실험, hello 기계 학습 예제 컬렉션의 일부입니다.
2. 웹 서비스에서 hello 키를 가진 apiKey를 할당 합니다. Hello 참조 **Azure 기계 학습 권한 부여 키 가져오기** hello 시작 부분 근처이 문서의 섹션.
3. ServiceUri hello 요청 URI로 할당 합니다.

