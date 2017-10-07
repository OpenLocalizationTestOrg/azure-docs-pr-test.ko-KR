---
title: "GitHub webhook에 의해 트리거되는 Azure에서 함수 aaaCreate | Microsoft Docs"
description: "Azure 함수 toocreate GitHub webhook 호출 하는 서버가 없는 함수를 사용 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>GitHub webhook를 통해 트리거되는 함수 만들기

자세한 내용은 방법 toocreate GitHub 특정 페이로드를 사용한 HTTP webhook 요청에 의해 트리거되는 함수입니다.

![Github Webhook hello Azure 포털에서에서 함수를 트리거](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>필수 조건

+ 하나 이상의 프로젝트와 함께 GitHub 계정.
+ Azure 구독. 구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure Function 앱 만들기

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

다음으로 hello 새 함수 앱에서 함수를 만듭니다.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>GitHub 웹후크 트리거 함수 만들기

1. 함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다. Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다. 이 함수 템플릿의 hello 전체 집합을 표시합니다.

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. 선택 hello **GitHub WebHook** 원하는 언어에 대 한 서식 파일입니다. **함수 이름을 지정한** 후 **만들기**를 선택합니다.

     ![Hello Azure 포털에서에서 새 GitHub 트리거되는 webhook 함수 만들기](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. 클릭 하 여 새 함수에 **<> / Get 함수 URL**, 복사 및 hello 값을 저장 합니다. 동일한 작업에 대 한 hello 마십시오 **<> / 가져오기 GitHub 비밀**합니다. GitHub에서 이러한 값 tooconfigure hello webhook을 사용합니다.

    ![Hello 함수 코드를 검토 합니다.](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

다음으로 GitHub 리포지토리에 webhook를 만듭니다.

## <a name="configure-hello-webhook"></a>Hello webhook 구성

1. Github를 소유 하 고 있는 tooa 저장소를 이동 합니다. 분기된 모든 리포지토리를 사용할 수도 있습니다. 사용 하 여 저장소 toofork 해야 할 경우 <https://github.com/Azure-Samples/functions-quickstart>합니다.

1. **설정**, **Webhooks**, **webhook 추가**를 차례로 클릭합니다.

    ![GitHub 웹후크를 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Hello 테이블에 지정 된 설정을 사용 하 고 클릭 **webhook 추가**합니다.

    ![Webhook URL에 hello 및 암호를 설정 합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| 설정 | 제안 값 | 설명 |
|---|---|---|
| **페이로드 URL** | 복사된 값 | 반환 하는 hello 값을 사용 하 여 **<> / Get 함수 URL**합니다. |
| **비밀**   | 복사된 값 | 반환 하는 hello 값을 사용 하 여 **<> / 가져오기 GitHub 비밀**합니다. |
| **콘텐츠 형식** | application/json | hello 함수는 JSON 페이로드가 필요합니다. |
| 이벤트 트리거 | 개별 이벤트를 선택하겠습니다. | Tootrigger 문제 메모 이벤트에만 포함 하려고 합니다.  |
| | 문제 주석 |  |

이제 webhook hello 새 문제 메모 추가 될 때 구성 된 tootrigger 함수 됩니다.

## <a name="test-hello-function"></a>테스트 hello 함수

1. GitHub 리포지토리에 hello를 열고 **문제** 새 브라우저 창에서 탭 합니다.

1. Hello 새 창에서 클릭 **새 문제**, 제목을 입력 하 고 클릭 **새 문제를 제출**합니다.

1. Hello 문제에서 설명을 입력 하 고 클릭 **주석**합니다.

    ![GitHub 문제 주석을 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Toohello 포털 돌아가서 hello 로그를 확인 하십시오. Hello 새 주석 텍스트와 함께 추적 항목이 표시 됩니다.

     ![Hello 로그에 hello 주석 텍스트를 봅니다.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>다음 단계

GitHub 웹후크에서 요청을 수신할 때 실행되는 함수를 만들었습니다.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

웹후크 트리거에 대한 자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](functions-bindings-http-webhook.md)을 참조하세요.
