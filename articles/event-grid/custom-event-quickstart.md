---
title: "Azure 이벤트 표 형태에 대 한 이벤트 aaaCustom | Microsoft Docs"
description: "Toothat 이벤트 구독 및 Azure 이벤트 표 형태 toopublish 항목을 사용 합니다."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Azure Event Grid로 사용자 지정 이벤트 만들기 및 라우팅

Azure의 이벤트 표 형태에는 hello 클라우드에 대 한 이벤트 서비스입니다. Hello Azure CLI toocreate 사용자 지정 항목을 사용 하 여이 문서에서는 toohello 항목, 구독 및 hello 이벤트 tooview hello 결과 트리거합니다. 일반적으로 이벤트 tooan 끝점을 webhook 또는 Azure 함수와 같은 toohello 이벤트에 응답을 보냅니다. 그러나 toosimplify이 문서에서는, hello 메시지를 단순히 수집 하는 hello 이벤트 tooa URL을 보냅니다. 오픈 소스이면서 [RequestBin](https://requestb.in/)이라는 타사 도구를 사용하여 이 URL을 만듭니다.

>[!NOTE]
>**RequestBin**은 높은 처리량 사용을 위해 설계되지 않은 오픈 소스 도구입니다. 순수 하 게 가격은 hello 도구의 여기 hello 사용 됩니다. 한 번에 둘 이상의 이벤트를 밀어 넣으면 hello 도구에서 사용자 이벤트를 모두 표시 되지 않을 수 있습니다.

완료 했으면 hello 이벤트 데이터 tooan 끝점 전송 되었는지 확인할 수 있습니다.

![이벤트 데이터](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

이 문서 hello Azure CLI의 최신 버전을 실행 되 고 있는지 필요 tooinstall 선택한 hello CLI를 사용 하 여 로컬로 (2.0.14 이상 버전). toofind hello 버전을 실행 `az --version`합니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Event Grid 토픽은 Azure 리소스이며 Azure 리소스 그룹에 배치해야 합니다. hello 리소스 그룹은 리소스는 Azure에 배포 되 고 관리 하는 논리적 컬렉션입니다.

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *gridResourceGroup* hello에 *westus2* 위치 합니다.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>사용자 지정 토픽 만들기

토픽은 이벤트를 게시하는 사용자 정의 끝점을 제공합니다. hello 다음 예제에서는 hello 항목 리소스 그룹 `<topic_name>`을 토픽의 고유한 이름으로 바꿉니다. DNS 항목으로 표시 되기 때문에 hello 항목 이름은 고유 해야 합니다. 이벤트 표 형태 hello 미리 보기 릴리스에 대 한 지원 **westus2** 및 **westcentralus** 위치입니다.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>메시지 끝점 만들기

Toohello 항목, 구독 하기 전에 hello 이벤트 메시지에 대 한 hello 끝점을 만들어 보겠습니다. Toorespond toohello 이벤트 코드를 작성 하지 않고 빠르게 검색할 수 있도록 hello 메시지를 수집 하는 끝점을 만들어 보겠습니다. RequestBin는 오픈 소스, toocreate 끝점을 사용 하면 타사 도구 및 tooit 전송 되는 요청을 봅니다. 너무 이동[RequestBin](https://requestb.in/)를 클릭 하 고 **는 RequestBin 만들**합니다.  Toohello 항목 구독할 때 필요 하므로 hello bin URL을 복사 합니다.

## <a name="subscribe-tooa-topic"></a>Tooa 항목 구독

Tooa 항목 tootell 이벤트 표 형태를 구독 하면 이벤트 tootrack 원하는 합니다. hello 다음 예제에서는 구독 toohello 항목을 생성 하 고 이벤트 알림에 대 한 hello 끝점으로 RequestBin hello URL 전달 합니다. 대체 `<event_subscription_name>` 구독에 대 한 고유한 이름을 사용 하 고 `<URL_from_RequestBin>` hello 섹션 앞의 hello 값으로. 끝점을 구독할 때 지정 하 여 이벤트 표 형태 hello 이벤트 toothat 끝점의 라우팅을 처리 합니다. 에 대 한 `<topic_name>`, 이전에 만든 hello 값을 사용 합니다. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>이벤트 tooyour 항목 보내기

이제 보겠습니다 이벤트 toosee를 트리거할 이벤트 표 형태 hello 메시지 tooyour 끝점을 배포 하는 방법입니다. 첫째, hello URL 가져오고 hello 항목에 대 한 주요 보겠습니다. 다시, `<topic_name>`의 토픽 이름을 사용합니다.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify이이 문서에서는까지 설정한 샘플 이벤트 데이터 toosend toohello 항목입니다. 일반적으로 응용 프로그램 또는 Azure 서비스는 hello 이벤트 데이터를 보내는 것입니다. 다음 예제는 hello hello 이벤트 데이터를 가져옵니다.

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

경우 있습니다 `echo "$body"` hello 전체 이벤트를 볼 수 있습니다. hello `data` hello JSON 요소가 이벤트의 hello 페이로드입니다. 모든 잘 구성된(Well-Formed) JSON은 이 필드에 배치될 수 있습니다. 또한 고급 라우팅 및 필터링에 대 한 hello 제목 필드를 사용할 수 있습니다.

CURL은 HTTP 요청을 수행하는 유틸리티입니다. 이 문서에서는 CURL toosend hello 이벤트 tooour 항목을 사용합니다. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Hello 이벤트를 실행 하 고 이벤트 표 형태 구독할 때 구성한 hello 메시지 toohello 끝점으로 전송 합니다. Toohello 앞에서 만든 RequestBin URL를 찾습니다. 또는 열려 있는 RequestBin 브라우저에서 새로 고침을 클릭합니다. 방금 전송 받은 hello 이벤트가 표시 됩니다. 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>리소스 정리
이 이벤트는 toocontinue 컨트롤러로이 문서에서 만든 hello 리소스를 정리할 합니다. Toocontinue 않으려는 경우이 문서에서 만든 명령 toodelete hello 리소스 다음 hello를 사용 합니다.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>다음 단계

배웠으므로 어떻게 toocreate 항목과 이벤트 구독에 대 한 자세한 내용 이벤트 표 형태 수행할 수 있습니다 않습니다.

- [Event Grid 정보](overview.md)
- [Azure Event Grid 및 Logic Apps를 사용하여 가상 컴퓨터 변경 모니터링](monitor-virtual-machine-changes-event-grid-logic-app.md)
