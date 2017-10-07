---
title: "Azure CDN 시작 aaaGetting | Microsoft Docs"
description: "이 항목에서는 tooenable Azure 콘텐츠 배달 네트워크 (CDN) hello 하는 방법을 보여 줍니다. hello 자습서 hello 새 CDN 프로필 및 끝점 만들기를 안내합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Azure CDN 시작
이 항목에서는 새로운 CDN 프로필 및 끝점을 만들어서 Azure CDN을 활성화하는 단계를 살펴봅니다.

> [!IMPORTANT]
> 소개 toohow CDN 작동으로 기능 목록은 참조 hello [CDN 개요](cdn-overview.md)합니다.
> 
> 

## <a name="create-a-new-cdn-profile"></a>새 CDN 프로필 만들기
CDN 프로필은 CDN 끝점의 컬렉션입니다.  각 프로필에는 CDN 끝점이 하나 이상 있습니다.  여러 프로필 tooorganize toouse를 지정할 수 있습니다 인터넷 도메인, 웹 응용 프로그램 또는 기타 일부 조건에 의해 CDN 끝점입니다.

> [!NOTE]
> 기본적으로 단일 Azure 구독은 제한 tooeight CDN 프로필입니다. CDN 프로필 각는 제한 된 tooten CDN 끝점입니다.
> 
> CDN 가격 hello CDN 프로필 수준에서 적용 됩니다. 원할 경우 toouse Azure CDN을 혼합 하 여 가격 책정 계층이 여러 CDN 프로필을 해야 합니다.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>새 CDN 끝점 만들기
**새 CDN 끝점 toocreate**

1. Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 탐색 합니다.  수 있는 고정 toohello 대시보드 hello 이전 단계에서 합니다.  경우 not, 있습니다 찾을 수 있습니다 것을 클릭 하 여 **찾아보기**, 다음 **CDN 프로필**, 인증서 및 hello 프로필 클릭 하면 tooadd를 끝점입니다.
   
    CDN 프로필 블레이드 hello 나타납니다.
   
    ![CDN 프로필][cdn-profile-settings]
2. Hello 클릭 **끝점 추가** 단추입니다.
   
    ![끝점 추가 단추][cdn-new-endpoint-button]
   
    hello **끝점 추가** 블레이드 나타납니다.
   
    ![끝점 추가 블레이드][cdn-add-endpoint]
3. 이 CDN 끝점에 대한 **이름** 을 입력합니다.  이 이름은 hello 도메인에서 캐시 된 리소스 사용된 tooaccess 됩니다 `<endpointname>.azureedge.net`합니다.
4. Hello에 **원본 형식을** 드롭다운에서 원본 형식을 선택 합니다.  Azure Storage 계정에 대해 **저장소**, Azure 클라우드 서비스에 대해 **클라우드 서비스**, Azure 웹앱에 대해 **웹앱**을 선택하고 기타 공개적으로 액세스할 수 있는 웹 서버 원본(Azure 또는 다른 곳에서 호스팅)에 대해 **사용자 지정 원본**을 선택합니다.
   
    ![CDN 원본 형식](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. Hello에 **원본 호스트 이름을** 드롭다운을 선택 하거나 원본 도메인을 입력 합니다.  hello 드롭다운 4 단계에서 지정한 hello 형식의 모든 사용할 수 있는 원본을 나열 합니다.  선택한 경우 *사용자 지정 원본* 으로 프로그램 **원본 형식을**, 사용자 지정 원본의 hello 도메인에 입력 됩니다.
6. Hello에 **원래 경로** 텍스트 상자에 원하는 toocache, 또는 leave 빈 tooallow 캐시 5 단계에서 지정한 hello 도메인에서 리소스 hello 경로 toohello 리소스를 입력 합니다.
7. Hello에 **원본 호스트 헤더**각 요청과 함께 CDN toosend hello 원하는 hello 호스트 헤더를 입력 하거나 hello 기본값을 사용 합니다.
   
   > [!WARNING]
   > 원본 Azure 저장소 및 웹 응용 프로그램 같은 일부 유형의 hello 원본 hello 호스트 헤더 toomatch hello 도메인이 필요합니다. 해당 도메인에서 다른 호스트 헤더를 요구 하는 원본이 없는 경우 hello 기본값을 유지 해야 합니다.
   > 
   > 
8. 에 대 한 **프로토콜** 및 **원본 포트**hello 프로토콜을 지정 하 고 hello 원점에 리소스 사용 되는 tooaccess 포트입니다.  프로토콜을 적어도 하나는(HTTP 또는 HTTPS) 선택해야 합니다.
   
   > [!NOTE]
   > hello **원본 포트** hello 원점에서 tooretrieve 정보를 사용 하는 어떤 포트 hello 끝점에만 적용 합니다.  hello 자체 끝점에만 됩니다 hello 기본 HTTP 및 HTTPS 포트 (80 및 443) hello에 관계 없이 사용할 수 있는 tooend 클라이언트 **원본 포트**합니다.  
   > 
   > **Akamai에서 azure CDN** 끝점 출처에 대 한 hello 전체 TCP 포트 범위를 허용 하지 않습니다.  허용되지 않는 원본 포트 목록을 보려면 [Akamai 허용된 원본 포트의 Azure CDN](https://msdn.microsoft.com/library/mt757337.aspx)를 참조하세요.  
   > 
   > CDN에 액세스할 HTTPS를 사용 하 여 콘텐츠 hello 제약 조건 뒤에 있습니다.
   > 
   > * Hello CDN에서 제공 하는 hello SSL 인증서를 사용 해야 합니다. 타사 인증서는 지원되지 않습니다.
   > * Hello CDN에서 제공한 도메인을 사용 해야 합니다 (`<endpointname>.azureedge.net`) tooaccess HTTPS 콘텐츠입니다. HTTPS 지원을 사용할 수 없는 경우 사용자 지정 도메인 이름 (Cname)에 대 한 hello CDN이 이번에 사용자 지정 인증서를 지원 하지 않으므로
   > 
   > 
9. Hello 클릭 **추가** 단추 toocreate hello 새 끝점입니다.
10. Hello 끝점을 만들 되 면 hello 프로필에 대 한 끝점의 목록에 나타납니다. hello 목록 보기 hello URL toouse tooaccess 캐시 hello 원본 도메인 뿐만 아니라 콘텐츠를 표시 합니다.
    
    ![CDN 끝점][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > hello 끝점 즉시 됩니다 사용 하기 위해 사용할 수 있는 대로 hello CDN 통해 hello 등록 toopropagate 시간이 걸립니다.  <b>Akamai의 Azure CDN</b> 프로필의 경우 일반적으로 1분 이내에 전파가 완료됩니다.  <b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.
    > 
    > 사용자가 hello 끝점 구성을 toohello Pop 전파 전에 toouse hello CDN 도메인 이름을 시도 HTTP 404 응답 코드를 받게 됩니다.  끝점을 만든 후 몇 시간 후에도 404 응답이 수신되는 경우 [404 상태를 반환하는 CDN 끝점 문제 해결](cdn-troubleshoot-endpoint.md)을 참조하세요.
    > 
    > 

## <a name="see-also"></a>참고 항목
* [쿼리 문자열이 포함된 요청의 캐싱 동작 제어](cdn-query-string.md)
* [어떻게 tooMap CDN 콘텐츠 tooa 사용자 지정 도메인](cdn-map-content-to-custom-domain.md)
* [Azure CDN 끝점에 자산 미리 로드](cdn-preload-endpoint.md)
* [Azure CDN 끝점 삭제](cdn-purge-endpoint.md)
* [404 상태를 반환하는 CDN 끝점 문제 해결](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
