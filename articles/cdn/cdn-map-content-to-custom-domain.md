---
title: "aaaMap Azure CDN 콘텐츠 tooa 사용자 지정 도메인 | Microsoft Docs"
description: "Azure CDN toomap tooa 사용자 지정 도메인 콘텐츠 하는 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Azure CDN 콘텐츠 tooa 사용자 지정 도메인 매핑
Url toocached 콘텐츠 azureedge.net의 하위 도메인을 사용 하는 대신 자체 도메인 이름을 순서 toouse에 사용자 지정 도메인 tooa CDN 끝점에 매핑할 수 있습니다.

사용자 지정 도메인 tooa CDN 끝점은 두 가지 방법으로 toomap:

1. [도메인 등록 기관과 함께 CNAME 레코드를 만들고 사용자 지정 도메인 및 하위 도메인 toohello CDN 끝점 매핑합니다](#register-a-custom-domain-for-an-azure-cdn-endpoint)합니다.
   
    CNAME 레코드는 같은 원본 도메인을 매핑하는 DNS 기능 `www.contosocdn.com` 또는 `cdn.contoso.com`, tooa 대상 도메인입니다. Hello 원본 도메인의 사용자 지정 도메인 및 하위 도메인은이 예제의 (하위 도메인, like **www** 또는 **cdn** 가 항상 필요). hello 대상 도메인은 CDN 끝점입니다.  
   
    그러나의 사용자 지정 도메인 tooyour CDN 끝점을 매핑할 때의 hello 프로세스 hello Azure 포털에서에서 hello 도메인을 등록 하는 동안 hello 도메인에 대 한 가동 중지 시간이 짧은 기간 동안에 될 수 있습니다.
2. [**cdnverify**를 사용하여 중간 등록 단계 추가](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    사용자 지정 도메인은 현재 있어야 가동 중지 시간 없이 서비스 수준 계약 (SLA)으로 응용 프로그램을 지 원하는 경우 hello Azure를 사용할 수 있습니다 **cdnverify** 하위 도메인 tooprovide 중간 등록 사용자가 될 수 있도록 수 tooaccess 하는 동안 도메인 단계 hello DNS 매핑 수행 합니다.  

Hello 위의 절차 중 하나를 사용 하 여 사용자 지정 도메인을 등록 하면 좋습니다 너무[해당 hello 사용자 지정 하위 도메인을 CDN 끝점 참조 확인](#verify-that-the-custom-subdomain-references-your-cdn-endpoint)합니다.

> [!NOTE]
> CNAME 레코드를 도메인 등록자 toomap와 도메인 toohello CDN 끝점을 만들 해야 있습니다. CNAME 레코드는 `www.contoso.com` 또는 `cdn.contoso.com` 같은 특정 하위 도메인을 매핑합니다. 없으면 가능한 toomap CNAME 레코드 tooa 루트 도메인에 같은 `contoso.com`합니다.
> 
> 하위 도메인은 하나의 CDN 끝점에만 연결될 수 있습니다. 주소를 지정 하는 모든 트래픽을 라우팅합니다. hello CNAME 레코드를 만들면 하위 도메인 toohello toohello 끝점을 지정 합니다.  예를 들어 `www.contoso.com` 을 CDN 끝점에 연결하는 경우 저장소 계정 끝점이나 클라우드 서비스 끝점과 같은 다른 Azure 끝점에는 연결할 수 없습니다. 그러나 hello에서 여러 하위 도메인을 사용할 수 있습니다 다른 서비스 끝점에 대해 동일한 도메인입니다. 여러 하위 도메인 toohello 매핑할 수도 있습니다 동일한 CDN 끝점입니다.
> 
> 에 대 한 **Verizon에서 Azure CDN** (Standard 및 Premium) 끝점을 차지 한다는 것 너무 유의**90 분** toopropagate tooCDN 가장자리 노드를 변경 하는 사용자 지정 도메인에 대 한 합니다.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Azure CDN 끝점에 대한 사용자 지정 도메인 등록
1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **찾아보기**, 다음 **CDN 프로필**, 다음 CDN 프로필을 hello toomap tooa 사용자 지정 도메인을 원하는 hello 끝점을 사용 합니다.  
3. Hello에 **CDN 프로필** 블레이드에서 tooassociate hello 하위 도메인 하려는 hello CDN 끝점을 클릭 합니다.
4. Hello 끝점 블레이드의 hello 위쪽 hello 클릭 **사용자 지정 도메인 추가** 단추입니다.  Hello에 **사용자 지정 도메인 추가** 블레이드에서 hello 끝점 호스트 이름, 새 CNAME 레코드를 만드는 toouse CDN 끝점에서 파생 된 표시 됩니다. hello 호스트 이름 주소의 hello 형식으로 나타납니다.  **&lt;EndpointName >. azureedge.net**합니다.  이 호스트 이름 toouse hello CNAME 레코드를 만드는에 복사할 수 있습니다.  
5. Tooyour 도메인 등록 기관의 웹 사이트를 탐색 하 고 DNS 레코드를 만들기 위한 hello 섹션을 찾습니다. **도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.
6. CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다. Toogo tooan 고급 설정 페이지를 가질 수 고 CNAME, 별칭 또는 하위 도메인 hello 단어를 검색할 수 있습니다.
7. 선택된 된 하위 도메인을 매핑하는 새 CNAME 레코드를 만듭니다 (예를 들어 **www** 또는 **cdn**) hello에 제공 된 toohello 호스트 이름 **사용자 지정 도메인 추가** 블레이드입니다. 
8. Toohello 반환 **사용자 지정 도메인 추가** 블레이드에서 hello 하위 도메인을 포함 하 여 hello 대화 상자에서 사용자 지정 도메인을 입력 합니다. 예를 들어 hello 형식을 hello 도메인 이름을 입력 `www.contoso.com` 또는 `cdn.contoso.com`합니다.   
   
   Azure는 입력 한 hello 도메인 이름에 대 한 hello CNAME 레코드가 있는지 확인 합니다. Hello CNAME이 올바르면 사용자 지정 도메인의 유효성이 검사 됩니다.  그러나에 대 한 **Verizon에서 Azure CDN** (Standard 및 Premium) 끝점 걸릴 수 있습니다를 사용자 지정 도메인 설정 toopropagate tooall CDN 지 노드에 too90 분 합니다.  
   
   사례 중 일부는 hello 인터넷에서 CNAME 레코드 toopropagate tooname 서버 hello에 대 한 시간이 걸릴 수 있습니다. 도메인의 유효성이 즉시 검사 되지 않습니다 hello CNAME 레코드는 올바른 판단 되는 경우 몇 분 정도 기다렸다가 하 고 다시 시도 하십시오.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Hello 중간 cdnverify 하위 도메인을 사용 하는 Azure CDN 끝점에 대 한 사용자 지정 도메인 등록
1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **찾아보기**, 다음 **CDN 프로필**, 다음 CDN 프로필을 hello toomap tooa 사용자 지정 도메인을 원하는 hello 끝점을 사용 합니다.  
3. Hello에 **CDN 프로필** 블레이드에서 tooassociate hello 하위 도메인 하려는 hello CDN 끝점을 클릭 합니다.
4. Hello 끝점 블레이드의 hello 위쪽 hello 클릭 **사용자 지정 도메인 추가** 단추입니다.  Hello에 **사용자 지정 도메인 추가** 블레이드에서 hello 끝점 호스트 이름, 새 CNAME 레코드를 만드는 toouse CDN 끝점에서 파생 된 표시 됩니다. hello 호스트 이름 주소의 hello 형식으로 나타납니다.  **&lt;EndpointName >. azureedge.net**합니다.  이 호스트 이름 toouse hello CNAME 레코드를 만드는에 복사할 수 있습니다.
5. Tooyour 도메인 등록 기관의 웹 사이트를 탐색 하 고 DNS 레코드를 만들기 위한 hello 섹션을 찾습니다. **도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.
6. CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다. Toogo tooan 고급 설정 페이지를 hello 단어를 검색할 수도 있습니다 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.
7. 새 CNAME 레코드를 만들고 hello를 포함 하는 하위 도메인 별칭을 제공 **cdnverify** 하위 도메인입니다. 예를 들어, 지정 하는 hello 하위 도메인 hello 형태로 표시 됩니다 **cdnverify.www** 또는 **cdnverify.cdn**합니다. 다음 CDN 끝점 hello 형태로 표시 되는 hello 호스트 이름을 제공 **cdnverify.&lt; EndpointName >. azureedge.net**합니다. DNS 매핑은 다음과 같습니다.`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Toohello 반환 **사용자 지정 도메인 추가** 블레이드에서 hello 하위 도메인을 포함 하 여 hello 대화 상자에서 사용자 지정 도메인을 입력 합니다. 예를 들어 hello 형식을 hello 도메인 이름을 입력 `www.contoso.com` 또는 `cdn.contoso.com`합니다. 이 단계에서 수행 하지 해야 toopreface hello 하위 도메인을 **cdnverify**합니다.  
   
    Azure는 입력 한 hello cdnverify 도메인 이름에 대 한 hello CNAME 레코드가 있는지 확인 합니다.
9. 이 시점에서 Azure에 의해 확인 된 사용자 지정 도메인 하지만 아직 트래픽 tooyour 도메인 라우트된 tooyour CDN 끝점을 되지 않습니다. 충분히 길어야 tooallow hello 사용자 지정 도메인 설정 toopropagate를 대기 하는 동안 toohello CDN에 지 노드 (90 분 정도 **Verizon에서 Azure CDN**, 1-2 분 정도 **Akamai에서 Azure CDN**), DNS tooyour 반환 등록 기관의 웹 사이트 및 하위 도메인 tooyour CDN 끝점을 매핑하는 다른 CNAME 레코드를 만듭니다. 예를 들어 hello 하위 도메인으로 지정 **www** 또는 **cdn**, 호스트 이름으로 hello 및  **&lt;EndpointName >. azureedge.net**합니다. 이 단계를 통해 사용자 지정 도메인의 hello 등록 완료 되었습니다.
10. 마지막으로 사용 하 여 만든 hello CNAME 레코드를 삭제할 수 있습니다 **cdnverify**는 중간 단계로 필요 했기, 합니다.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>해당 hello 사용자 지정 하위 도메인을 CDN 끝점 참조 확인
* 사용자 지정 도메인의 hello 등록을 완료 한 후에 hello 사용자 지정 도메인을 사용 하 여 CDN 끝점에서 캐시 된 콘텐츠를 액세스할 수 있습니다.
  Hello 끝점에서 캐시 된 공개 콘텐츠가 있는지 먼저 확인 합니다. 예를 들어 CDN 끝점이 저장소 계정과 연결 되는 경우 CDN hello 공용 blob 컨테이너의 콘텐츠를 캐시 합니다. tootest hello 사용자 지정 도메인을 컨테이너가 tooallow 공용 액세스를 설정 되어 있고 blob을 하나 이상 포함 되어 있는지 확인 합니다.
* 브라우저에서 사용자 지정 도메인 hello를 사용 하 여 hello blob의 toohello 주소를 이동 합니다. 예를 들어, 사용자 지정 도메인은 `cdn.contoso.com`, hello URL tooa 캐시 된 blob url 비슷한 toohello 됩니다: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>참고 항목
[TooEnable는 네트워크 CDN (콘텐츠 배달) Azure 용 hello 하는 방법](cdn-create-new-endpoint.md)  

