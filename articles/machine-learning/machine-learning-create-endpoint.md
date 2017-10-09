---
title: "기계 학습에서 웹 서비스 끝점 aaaCreating | Microsoft Docs"
description: "Azure Machine Learning에서 웹 서비스 끝점 만들기"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>끝점 만들기
> [!NOTE]
>  이 항목에서는 기술을 적용 가능한 tooa 설명 **클래식** 컴퓨터 학습 웹 서비스입니다.
> 
> 

정방향 tooyour 고객을 판매 하는 웹 서비스를 만들 서비스를 만들 때 어떤 hello 웹에서에서 여전히 연결 된 toohello 실험은 tooprovide 학습 된 모델 tooeach 고객이 필요 합니다. 또한 toohello 실험 해야 업데이트 선택적 적용 tooan 끝점 hello 사용자 지정 항목을 덮어쓰지 않고 합니다.

tooaccomplish이를 Azure 기계 학습 toocreate을 사용 하면 배포 된 웹 서비스에 대 한 여러 끝점입니다. 각 끝점 hello 웹 서비스에에서 독립적으로 주소가 지정 된 제한 하 여 있고, 관리 합니다. 각 끝점은 고유한 URL 및 권한 부여 키 tooyour 고객을 배포할 수 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>끝점 tooa 웹 서비스 추가
끝점 tooa 웹 서비스는 세 가지 방법으로 tooadd 합니다.

* 프로그래밍 방식
* Hello Azure 컴퓨터 학습 웹 서비스 포털을 통해
* 그러나 Azure 클래식 포털을 hello

Hello 끝점을 만든 후에 동기 Api 일괄 처리, Api 통해 사용할 수 있으며 excel 워크시트 수 있습니다. 또한이 UI 통해 tooadding 끝점을 사용할 수도 있습니다 hello 끝점 관리 Api tooprogrammatically 끝점을 추가 합니다.

> [!NOTE]
> 추가 끝점 toohello 웹 서비스를 추가한 경우 hello 기본 끝점을 삭제할 수 없습니다.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>프로그래밍 방식으로 끝점 추가
프로그래밍 방식으로 hello를 사용 하는 끝점 tooyour 웹 서비스를 추가할 수 있습니다 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드입니다.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 끝점 추가
1. 기계 학습 스튜디오에서는 hello 왼쪽된 탐색 열 웹 서비스를 클릭 합니다.
2. Hello 웹 서비스 대시보드 hello 아래쪽 클릭 **끝점을 관리**합니다. hello Azure 컴퓨터 학습 웹 서비스 포털 hello 웹 서비스에 대 한 toohello 끝점 페이지를 엽니다.
3. **새로 만들기**를 클릭합니다.
4. 이름 및 hello 새 끝점에 대 한 설명을 입력 합니다. 끝점 이름은 길이가 24자 이하이고 알파벳 소문자 또는 숫자로 구성되어야 합니다. Hello 로깅 수준 및 예제 데이터가 활성화 되어 있는지 여부를 선택 합니다. 로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Hello Azure 클래식 포털을 사용 하 여 끝점 추가
1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com), 클릭 **기계 학습** hello 왼쪽된 열에 있습니다. 관심이 있는 hello 웹 서비스를 포함 하는 hello 작업 영역을 클릭 합니다.
   
    ![Tooworkspace 이동](./media/machine-learning-create-endpoint/figure-1.png)
2. **웹 서비스**를 클릭합니다.
   
    ![TooWeb 서비스 탐색](./media/machine-learning-create-endpoint/figure-2.png)
3. 사용 가능한 끝점의 toosee hello 목록에 관심이 hello 웹 서비스를 클릭 합니다.
   
    ![Tooendpoint 이동](./media/machine-learning-create-endpoint/figure-3.png)
4. Hello hello 페이지의 아래쪽에 있는 클릭 **끝점 추가**합니다. 이름 및 설명을 입력 하을이 웹 서비스의 이름과 같은 이름을 hello로 다른 끝점이 있는지 확인 합니다. 특별 한 요구 사항이 없다면 hello 제한 수준을 값이 기본값으로 둡니다. 제한에 대해 자세히 toolearn 참조 [API 끝점 확장](machine-learning-scaling-webservice.md)합니다.
   
    ![끝점 만들기](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>다음 단계
[어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

