---
title: "azure Blob 저장소에 의해 트리거되는 함수 aaaCreate | Microsoft Docs"
description: "항목에 의해 호출 되는 서버가 없는 함수를 사용 하 여 Azure 함수 toocreate tooAzure Blob 저장소를 추가 합니다."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Azure Blob Storage에 의해 트리거되는 함수 만들기

어떻게 toocreate 파일은 때 트리거되는 함수 업로드 tooor Azure Blob 저장소에서 업데이트에 대해 알아봅니다.

![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>필수 조건

+ 다운로드 및 설치 hello [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.
+ Azure 구독. 구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure Function 앱 만들기

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

다음으로 hello 새 함수 앱에서 함수를 만듭니다.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Blob Storage 트리거 함수 만들기

1. 함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다. Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다. 이 함수 템플릿의 hello 전체 집합을 표시합니다.

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. 선택 hello **BlobTrigger** 원하는 언어 및 hello 테이블에 지정 된 hello 설정 사용에 대 한 서식 파일입니다.

    ![Hello Blob 트리거되는 저장소 함수를 만듭니다.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | 설정 | 제안 값 | 설명 |
    |---|---|---|
    | **Path**   | mycontainer/{name}    | 모니터링되는 Blob Storage의 위치입니다. hello로 hello 바인딩을 hello blob의 hello 파일 이름을 전달 _이름_ 매개 변수입니다.  |
    | **Storage 계정 연결** | AzureWebJobStorage | Hello 함수 응용 프로그램에서 이미 사용 되는 저장소 계정 연결을 사용 하거나 새로 만들 수 있습니다.  |
    | **함수 이름 지정** | 함수 앱에서 고유 | 이 Blob 트리거 함수의 이름입니다. |

3. 클릭 **만들기** toocreate 함수입니다.

다음으로 tooyour Azure 저장소 계정을 연결 하 고 hello 만들 **mycontainer** 컨테이너입니다.

## <a name="create-hello-container"></a>Hello 컨테이너 만들기

1. 함수에서 **통합**을 클릭하고 **설명서**를 확장하여 **계정 이름** 및 **계정 키**를 모두 복사합니다. 이러한 자격 증명 tooconnect toohello 저장소 계정을 사용합니다. 저장소 계정에 이미 연결한 경우 toostep 4를 건너뜁니다.

    ![Hello 저장소 계정 연결 자격 증명을 가져옵니다.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Hello 실행 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/) 도구를 hello 클릭 연결 hello 왼쪽에 있는 아이콘을 선택 **저장소 계정 이름과 키를 사용 하 여**를 클릭 하 고 **다음**합니다.

    ![Hello 저장소 계정 탐색기 도구를 실행 합니다.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Hello 입력 **계정 이름** 및 **계정 키** 1 단계에서 클릭 **다음** 차례로 **연결**합니다. 

    ![Hello 저장소 자격 증명을 입력 하 고 연결 합니다.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Hello 연결 된 저장소 계정, 마우스 오른쪽 단추로 클릭 **Blob 컨테이너**, 클릭 **blob 컨테이너 만들기**, 형식 `mycontainer`, enter 키를 누릅니다.

    ![저장소 큐 만들기.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Blob 컨테이너를가지고 파일 toohello 컨테이너를 업로드 하 여 hello 함수를 테스트할 수 있습니다.

## <a name="test-hello-function"></a>테스트 hello 함수

1. Hello Azure 포털에 다시 찾아보기 tooyour 함수 확장 hello **로그** hello 있는지 확인 하 고 hello 페이지 맨 아래에 해당 로그 스트리밍 없는 일시 중지 합니다.

1. Storage 탐색기에서 저장소 계정, **Blob 컨테이너** 및 **mycontainer**를 확장합니다. **업로드**를 클릭한 후 **파일 업로드...**를 클릭합니다.

    ![파일 toohello blob 컨테이너를 업로드 합니다.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. Hello에 **파일 업로드** 대화 상자를 클릭 hello **파일** 필드입니다. 이미지 파일과 같은 로컬 컴퓨터에 tooa 파일 찾아보기 선택 하 고 클릭 **열려** 차례로 **업로드**합니다.

1. Tooyour 기능 로그를 다시 이동 하 고 해당 hello blob를 읽었음을 확인 합니다.

   ![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > 함수 앱 hello 기본 소비 계획을 실행할 때 있을 수 있습니다 tooseveral 추가 되거나 업데이트 되 고 blob hello와 hello 간 시간 (분)을 지연 트리거된 작동 합니다. Blob 트리거 함수에서 대기 시간을 줄여야 하는 경우 App Service 계획에서 함수 앱을 실행하는 것이 좋습니다.

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>다음 단계

Blob 저장소에 blob가 업데이트 tooor 추가 될 때 실행 되는 함수를 만들었습니다. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Blob Storage 트리거에 대한 자세한 내용은 [Azure Functions Blob Storage 바인딩](functions-bindings-storage-blob.md)을 참조하세요.
