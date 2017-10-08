---
title: "Azure 기계 학습에서 새 웹 서비스 aaaDeploying | Microsoft Docs"
description: "ARM 배포 hello 워크플로 기반 웹 서비스"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>새 웹 서비스 배포
기반으로 하는 웹 서비스를 제공 하는 Microsoft Azure 기계 이제 학습 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 새 청구 계획 옵션 및 배포 하 여 웹 서비스 toomultiple 영역에 대 한 허용 합니다.

다음은 hello 일반 워크플로 toodeploy Microsoft Azure 컴퓨터 학습 웹 서비스를 사용 하는 웹 서비스입니다.

* 예측 실험 만들기
* 배포
* 해당 이름 구성
* 요금제
* 테스트
* 사용

다음 그래픽 hello hello 워크플로를 보여 줍니다.

![웹 서비스 배포 워크플로][1]

## <a name="deploy-web-service-from-studio"></a>Studio에서 웹 서비스 배포
새 웹 서비스 실험 toodeploy 합니다. Hello 기계 학습 스튜디오에 로그인 하 고 새 예측 웹 서비스를 만듭니다. 

**참고**: 실험을 기존 웹 서비스로 이미 배포한 경우 새 웹 서비스로 배포할 수 없습니다.

클릭 **실행** hello hello 맨 아래에 캔버스를 실험 하 고 클릭 **웹 서비스 배포** 및 **웹 서비스 배포 [New]**합니다. hello 기계 학습 웹 서비스 관리자의 hello 배포 페이지가 열립니다.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>기계 학습 웹 서비스 관리자 배포 실험 페이지
Hello 실험 배포 페이지에서 hello 웹 서비스에 대 한 이름을 입력 합니다.
가격 책정 계획을 선택합니다. 기존 가격 책정 계획 선택할 수 있는 경우에 hello 서비스에 대 한 새 가격 계획을 만들어야 그렇지 않으면 합니다. 

1. Hello에 **가격 계획** 드롭 다운를 기존 계획을 선택 하거나 선택 hello **선택 새 계획** 옵션입니다.
2. **계획 이름**, 청구서에 hello 계획을 식별 하는 이름을 입력 합니다.
3. Hello 중 하나를 선택 **월별 계획 계층**합니다. 참고 hello 계획 계층 기본 기본 지역 및 웹 서비스에 대 한 toohello 계획 하는 배포 된 toothat 영역입니다.

클릭 **배포** 웹 서비스에 대 한 hello 빠른 시작 페이지를 엽니다.

## <a name="quickstart-page"></a>빠른 시작 페이지
hello 웹 서비스 빠른 시작 페이지 하면 액세스 및 지침 hello 새 웹 서비스를 만든 후 수행할 수는 가장 일반적인 작업에. 여기에서 쉽게 액세스할 수 있습니다 두 hello **테스트** 페이지 및 **사용** 페이지.

## <a name="testing-your-web-service"></a>웹 서비스 테스트
Hello 빠른 시작 페이지에서 일반적인 작업에서 테스트 웹 서비스를 클릭 합니다.   

tootest hello 웹 서비스 요청 응답 서비스 (RR)로:

* 클릭 **테스트** hello 메뉴 모음에서 합니다.
* **요청-응답**을 클릭합니다.
* Hello 실험의 입력된 열에 대 한 적절 한 값을 입력 합니다.
* **요청-응답**테스트를 클릭합니다.

결과 있습니다 hello의 오른쪽 hello 페이지에 표시 됩니다.

일괄 처리 실행 서비스 (BES) 웹 서비스 tootest CSV 파일을 사용 합니다.

* 클릭 **테스트** hello 메뉴 모음에서 합니다.
* **배치**를 클릭합니다.
* 입력을 찾아보기를 클릭 하 고 tooyour 예제 데이터 파일을 이동 합니다.
* **테스트**를 클릭합니다.

테스트의 hello 상태 표시 됩니다 **테스트 일괄 처리 작업이**합니다.

## <a name="consuming-your-web-service"></a>웹 서비스 사용
웹 서비스로 배포된 경우 Azure 기계 학습 실험에서는 광범위한 장치 및 플랫폼에서 사용할 수 있는 REST API를 제공합니다. 간단한 REST API를 받아들이고 JSON을 사용 하 여 응답 hello 형식의 메시지 때문입니다. hello Azure 기계 학습 포털에서는 사용할 수 있는 코드에서 R, C#, 및 Python toocall hello 웹 서비스입니다.

Hello Consuming 페이지에서 다음을 찾을 수 있습니다.

* hello API 키와 앱에서 웹 서비스 사용에 대 한 URI입니다.
* Excel 및 웹 응용 프로그램 템플릿 tookick 소비 프로세스를 시작 합니다.
* 샘플 코드에 C#, python 및 R tooget 시작 했습니다.

웹 서비스 사용에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

## <a name="next-steps"></a>다음 단계
웹 서비스 사용에 대한 자세한 내용은 다음을 참조하세요.

[어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)

[Azure 기계 학습 웹 서비스: 배포 및 사용](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
