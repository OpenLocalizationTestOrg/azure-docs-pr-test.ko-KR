---
title: "기계 학습 웹 서비스에 대 한 aaaLogging | Microsoft Docs"
description: "자세한 내용은 방법 tooenable 로깅에 대 한 기계 학습 웹 서비스입니다. 로깅은 toohelp hello Api 문제를 해결 하는 추가 정보를 제공 합니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>기계 학습 웹 서비스에 대해 로깅 사용
이 문서는 기계 학습 웹 서비스의 기능 로깅 hello에 정보를 제공 합니다. 로깅에는 오류 번호와 프로그램 호출 toohello 컴퓨터 학습 Api 문제를 해결 하는 데 도움이 되는 메시지 범위를 벗어나는 추가 정보를 제공 합니다.  

## <a name="how-tooenable-logging-for-a-web-service"></a>어떻게 웹 서비스에 대 한 tooenable 로깅

Hello에서 로깅을 사용 하면 [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 포털입니다. 

1. Toohello Azure 컴퓨터 학습 웹 서비스 포털에 로그인 [https://services.azureml.net](https://services.azureml.net)합니다. 기본 웹 서비스에 대 한 가져올 수도 있습니다 toohello 포털 클릭 하 여 **새 웹 서비스 환경을** 기계 학습 스튜디오에서 hello 컴퓨터 학습 웹 서비스 페이지에 있습니다.

   ![새 웹 서비스 환경 링크](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Hello 상단 메뉴 모음에서 **웹 서비스** 는 새로 만들기에 대 한 웹 서비스 키를 누르거나 **웹 서비스를 클래식** 기존에 대 한 웹 서비스입니다.

   ![새로운 또는 클래식 웹 서비스 선택](media/machine-learning-web-services-logging/select-web-service.png)

3. 새 웹 서비스에 대 한 hello 웹 서비스 이름을 클릭 합니다. 기본 웹 서비스에 대 한 hello 웹 서비스 이름을 클릭 하 고 hello 다음 페이지에서 hello 적절 한 끝점을 클릭 합니다.

4. Hello 상단 메뉴 모음에서 **구성**합니다.

5. 집합 hello **Enable Logging** 옵션*오류* (toolog만 오류) 또는 *모든* (로깅에 대 한 전체).

   ![로깅 수준 선택](media/machine-learning-web-services-logging/enable-logging.png)

6. **Save**를 클릭합니다.

7. 기본 웹 서비스에 대 한 hello 만들 **ml 진단** 컨테이너입니다.

   모든 웹 서비스 로그는 라는 blob 컨테이너에 저장 됩니다. **ml 진단** hello 웹 서비스와 관련 된 hello 저장소 계정에 있습니다. 새 웹 서비스에 대 한 처음 hello 웹 서비스에 액세스 하면이 컨테이너 hello를 생성 됩니다. 기본 웹 서비스에 대 한 존재 하지 않는 경우 toocreate hello 컨테이너가 필요 합니다. 

   1. Hello에 [Azure 포털](https://portal.azure.com), 이동 hello 웹 서비스와 관련 된 toohello 저장소 계정입니다.

   2. **Blob Service**에서 **컨테이너**를 클릭합니다.

   3. 경우 hello 컨테이너 **ml 진단** 존재를 클릭 하지 **+ 컨테이너**을 hello 컨테이너 hello 이름 "ml-진단"을 지정 하 고 hello 선택 **액세스 형식** "Blob"으로 합니다. **확인**을 클릭합니다.

      ![로깅 수준 선택](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> 기본 웹 서비스에 대 한 기계 학습 스튜디오에서 웹 서비스 대시보드 hello 스위치 tooenable 로깅을 있습니다. 그러나 로깅 현재 hello 웹 서비스 포털을 통해 관리 되는, 때문에이 문서에 설명 된 대로 hello 포털을 통해 로깅 tooenable가 필요 합니다. Studio 로그인 이미 사용 하는 경우 웹 서비스 포털 hello 로깅을 사용 하지 않도록 설정 하 고 다시 활성화 합니다.


## <a name="hello-effects-of-enabling-logging"></a>로깅의 hello 효과
Hello에 hello 진단 및 hello 웹 서비스 끝점에서 오류는 기록 로깅이 사용 되 면 **ml 진단** hello Azure 저장소 계정에서에서 blob 컨테이너 hello 사용자의 작업 영역에 연결 합니다. 이 컨테이너는이 저장소 계정에 연결 된 모든 hello 작업 영역에 대 한 모든 hello 웹 서비스 끝점에 대 한 모든 hello 진단 정보를 보유 합니다.

여러 가지 도구 사용 가능한 tooexplore Azure 저장소 계정을 hello 중 하나를 사용 하 여 hello 로그를 볼 수 있습니다. hello 쉬운 hello Azure 포털에서에서 toonavigate toohello 저장소 계정이 될 수 있습니다, 클릭 **컨테이너**, hello 컨테이너를 클릭 한 다음 **ml 진단**합니다.  

## <a name="log-blob-detail-information"></a>Blob 세부 정보 기록
작업을 수행 하는 hello 중 정확히 하나에 대 한 hello 진단 정보를 보유 하는 각 컨테이너의 blob에 hello:

* 일괄 처리 실행 hello 메서드의 실행  
* 요청-응답 hello 메서드의 실행  
* 요청-응답 컨테이너 초기화

각 blob의 이름은 hello hello 다음 폼의 접두사에 있습니다. 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


여기서 _로그 유형_ hello 다음 값 중 하나입니다.  

* 일괄 처리  
* score/requests  
* score/init  

