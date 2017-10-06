---
title: "hello Azure 포털을 사용 하 여 끝점을 스트리밍 aaaManage | Microsoft Docs"
description: "이 항목에서는 toomanage 스트리밍 끝점이 Azure 포털 hello 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Azure 포털 hello로 스트리밍 끝점을 관리

이 항목에서는 toouse Azure 포털 toomanage 스트리밍 끝점을 hello 하는 방법을 보여 줍니다. 

>[!NOTE]
>있는지 tooreview hello 확인 [개요](media-services-streaming-endpoints-overview.md) 항목입니다. 

어떻게 tooscale hello 스트리밍 끝점에 대 한 정보를 참조 하십시오. [이](media-services-portal-scale-streaming-endpoints.md) 항목입니다.

## <a name="start-managing-streaming-endpoints"></a>스트리밍 끝점 관리 시작 

회원님의 계정에 대 한 스트리밍 끝점을 관리 하는 toostart 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. Hello에 **설정** 블레이드를 **스트리밍 끝점**합니다.
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> 스트리밍 끝점이 실행 중인 상태일 때만 요금이 청구됩니다.

## <a name="adddelete-a-streaming-endpoint"></a>스트리밍 끝점 추가/삭제

>[!NOTE]
>hello 기본 스트리밍 끝점을 삭제할 수 없습니다.

tooadd/삭제 스트리밍 끝점에 사용 하 여 Azure 포털 hello, 다음 hello지 않습니다.

1. 스트리밍 끝점 tooadd 클릭 hello **+ 끝점** hello hello 페이지 위쪽에 있습니다. 

    Toohave 하려는 경우에 여러 개의 스트리밍 끝점을 할 수 있습니다 다른 Cdn 또는 CDN 및 직접 액세스 합니다.

2. 스트리밍 끝점 toodelete 키를 눌러 **삭제** 단추입니다.      
3. Hello 클릭 **시작** 단추 toostart hello 스트리밍 끝점입니다.
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Hello 스트리밍 끝점을 구성합니다.
스트리밍 끝점 tooconfigure hello를 다음 속성이 있습니다.

* Access Control
* 캐시 제어
* 교차 사이트 액세스 정책

이러한 속성에 대한 자세한 정보는 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)를 참조하세요.

Hello 다음을 수행 하 여 스트리밍 끝점을 구성할 수 있습니다.

1. 스트리밍 끝점 tooconfigure 원하는 hello를 선택 합니다.
2. **설정**을 클릭합니다.

Hello 필드에 대 한 간단한 설명은 다음과 같습니다.

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. 최대 캐시 정책: tooconfigure 사용 되는 자산의 캐시 수명을이 스트리밍 끝점을 통해 제공 됩니다. 설정 된 hello 기본값이 사용 됩니다. Azure 저장소에 직접 hello 기본값을 정의할 수도 있습니다. Azure CDN hello 스트리밍 끝점을 사용 하도록 구성 되어 600 초 보다 hello 캐시 정책 값 tooless를 설정 하지 않아야 합니다.  
2. 허용 된 IP 주소: toospecify IP 주소는 허용 tooconnect toohello 스트리밍 끝점을 게시 하는 데 사용 합니다. IP 주소가 지정 된 없는 경우 모든 IP 주소 수 tooconnect입니다. IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소 및 CIDR 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1/22') 또는 IP 주소와 점으로 구분된 십진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.255.0)')로 지정할 수 있습니다.
3. Akamai 서명 헤더 인증에 대 한 구성을: toospecify Akamai 서버의 서명 헤더 인증 요청 구성 방법을 사용 합니다. 만료 시간은 UTC 단위입니다.

## <a name="scale-your-premium-streaming-endpoint"></a>프리미엄 스트리밍 끝점 규모 조정

자세한 내용은 [이 항목](media-services-portal-scale-streaming-endpoints.md) 을 참조하세요.

## <a id="enable_cdn"></a>Azure CDN 통합 사용

새 계정을 만들면 기본 스트리밍 끝점 Azure CDN 통합이 기본적으로 설정됩니다.

나중에 CDN 사용 toodisable/hello, 원하는 경우 스트리밍 끝점 hello에 있어야 **중지** 상태입니다. CDN을 팝 하는 모든 hello에서 hello Azure CDN 통합 tooget 사용 하도록 설정 하 고 hello 변경 toobe 활성 too2 시간이 걸릴 수입니다. 그러나 수 있습니다 hello 스트리밍 끝점에서에서 스트리밍 끝점과 중단 없이 스트림 시작 하 고 hello 통합 완료 되 면 hello 스트림 hello CDN에서에서 제공 됩니다. Hello 기간을 프로 비전 하는 동안 하려면 스트리밍 끝점에 포함 됩니다 **시작** 상태 및 있습니다 degredad 성능을 알 수 있습니다.

CDN 통합은 모든 Azure 데이터 센터 execpt 중국 hello 및 연방 Goverment 영역에서 사용 됩니다.

활성화 되 면 hello **액세스 제어**, **사용자 지정 호스트 이름** 및 **Akamai 서명 인증** 구성을 사용할 수 없게 가져옵니다.
 
> [!IMPORTANT]
> Azure Media Services와 Azure CDN의 통합은 **Verizon의 Azure CDN**에서 표준 스트리밍 끝점에 구현됩니다. 프리미엄 스트리밍 끝점은 모든 **Azure CDN 가격 책정 및 공급자**를 사용하여 구성할 수 있습니다. Azure CDN 기능에 대 한 자세한 내용은 참조 hello [CDN 개요](../cdn/cdn-overview.md)합니다.
 
### <a name="additional-considerations"></a>추가 고려 사항

* 스트리밍 끝점에 CDN을 사용할 때 클라이언트 hello 원본에서 직접 콘텐츠를 요청할 수 없습니다. CDN 유무 콘텐츠 hello 기능 tootest 해야 할 경우 CDN을 사용 하도록 설정 되지 않은 다른 스트리밍 끝점을 만들 수 있습니다.
* 스트리밍 끝점 호스트 이름은 유지 CDN을 사용 하도록 설정한 후 같은 hello 합니다. CDN을 사용 하도록 설정한 후 모든 변경 내용을 tooyour 미디어 서비스 워크플로 toomake 필요 하지 않습니다. 예를 들어 프로그램 스트리밍 끝점 호스트 이름 CDN을 사용 하도록 설정한 후 strasbourg.streaming.mediaservices.windows.net, 경우 hello 정확히 동일한 호스트 이름이 사용 됩니다.
* 새 스트리밍 끝점에 대 한; 새로운 끝점을 만들고 하기만 CDN을 사용할 수 있습니다. 기존 스트리밍 끝점 toofirst 중지 hello 끝점과 설정/해제 hello CDN이 필요 합니다.
* 표준 스트리밍 끝점은 Azure 관리 포털에서 **Verizon 표준 CDN 공급자**를 통해서만 구성할 수 있습니다. 그러나 REST API를 사용하여 다른 Azure CDN 공급자를 사용하도록 설정할 수 있습니다.

## <a name="configure-cdn-profile"></a>CDN 프로필 구성

Hello를 선택 하 여 hello CDN 프로필을 구성할 수 있습니다 **CDN 관리** hello 위에서 단추입니다.

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

