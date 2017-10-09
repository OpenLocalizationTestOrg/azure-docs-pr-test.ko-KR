---
title: "HTTPS 통해 사용자 지정 도메인을 사용 하 여 aaaUsing hello Azure CDN tooaccess blob"
description: "HTTPS를 통해 사용자 지정 도메인이 있는 blob를 blob 저장소 tooaccess toointegrate hello Azure CDN 방법을 알아봅니다"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>HTTPS를 통해 사용자 지정 도메인에서 hello Azure CDN tooaccess blob 사용

이제 Azure CDN(콘텐츠 배달 네트워크)은 사용자 지정 도메인 이름에 대한 HTTPS를 지원합니다.
사용자 지정 도메인을 사용 하 여 HTTPS를 통해이 기능 tooaccess 저장소 blob을 활용할 수 있습니다. toodo blob 끝점 및 지도 hello CDN tooa 사용자 지정 도메인 이름의 Azure CDN tooenable 먼저 필요 합니다, 합니다. 이러한 단계를 수행 하면 되 면 한 번의 클릭 사용, 전체 인증서 관리를 통해와 없는 추가 비용 toonormal CDN 가격이 포함 된 모두 간소화은 사용자 지정 도메인에 대 한 HTTPS를 사용 합니다.

이 기능은 tooprotect hello 개인 및 전송 중에 중요 한 웹 응용 프로그램 데이터의 데이터 무결성 지원 수 있기 때문에 중요 한 있습니다. HTTPS 통해 SSL 프로토콜 tooserve 트래픽을 hello를 사용 하 여 데이터가 암호화 되도록 하는 hello을 통해 전송 될 때 인터넷 합니다. HTTPS는 신뢰할 수 있는 인증을 제공하며 공격으로부터 웹 응용 프로그램을 보호합니다.

> [!NOTE]
> 또한 hello world 응용 프로그램 toodeliver 고대역폭 콘텐츠 60px hello Azure CDN 사용자 지정 도메인 이름에 대 한 SSL 지원 tooproviding 수 있습니다.
> toolearn을 체크 아웃 [hello Azure CDN 개요](../../cdn/cdn-overview.md)합니다.
>
>

## <a name="quick-start"></a>빠른 시작

Hello 단계 필요한 tooenable HTTPS에 대 한 사용자 지정 blob 저장소 끝점은 다음과 같습니다.

1.  [Azure Storage 계정과 Azure CDN을 통합합니다](../../cdn/cdn-create-a-storage-account-with-cdn.md).
    이 문서에서는 하지 않았으면 지금 이미 경우 hello Azure 포털에서에서 저장소 계정을 만드는 과정을 안내 합니다.
2.  [맵 Azure CDN 콘텐츠 tooa 사용자 지정 도메인](../../cdn/cdn-map-content-to-custom-domain.md)합니다.
3.  [Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정합니다](../../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>공유 액세스 서명

Blob 저장소 끝점은 구성 된 toodisallow 익명 읽기 액세스를 tooprovide 해야 합니다는 [공유 액세스 서명 (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) tooyour 사용자 지정 도메인 확인 토큰을 각 요청에 있습니다. 기본적으로 Blob Storage 끝점은 익명 읽기 액세스를 허용하지 않습니다. 공유 액세스 서명에 관한 자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.

Azure CDN 어떠한 제한 추가 toohello SAS 토큰을 반영 하지 않습니다. 예를 들어 모든 SAS 토큰은 만료 시간이 있습니다. 이 즉, 콘텐츠 hello CDN 지 노드에에서 해당 콘텐츠는 제거 될 때까지 만료 된 SAS로 액세스할 수 있습니다. Hello 캐시 응답 헤더를 설정 하 여 hello CDN에서 데이터가 캐시 되는 시간을 제어할 수 있습니다. 지침에 관해서는 [Azure CDN에서 Azure Storage Blob 만료 관리](../../cdn/cdn-manage-expiration-of-blob-content.md)를 참조하세요.

Hello에 대 한 SAS Url을 여러 개 만들면 같은 blob 끝점 권장 Azure CDN에 대 한 쿼리 문자열 캐싱을 설정 합니다. 이 tooensure 각 URL은 고유 엔터티로 처리 하는 합니다. 자세한 내용은 [쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어](../../cdn/cdn-query-string.md)를 참조하세요.

## <a name="http-toohttps-redirection"></a>HTTP tooHTTPS 리디렉션

Tooredirect HTTP 트래픽을 tooHTTPS 선택할 수 있습니다. Verizon에서 Azure CDN 프리미엄 제품인 hello 사용을 해야 합니다. 너무 필요한[Azure CDN 규칙 엔진을 사용 하 여 재정의 HTTP 동작](../../cdn/cdn-rules-engine.md) 는 다음과 같은 규칙이 있습니다.

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Cdn 끝점 이름이" CDN 끝점에 대해 구성한 toohello 이름을 참조 합니다. Hello 드롭다운에서이 값을 선택할 수 있습니다. 정적 콘텐츠 있는 원본 저장소 계정 내에서 hello 경로 "원래 경로"를 참조 합니다.
단일 컨테이너의 모든 정적 콘텐츠를 호스팅하는 경우 해당 컨테이너의 hello 이름으로 "원래 경로"를 대체 합니다.

규칙에 자세히 알아보려면, hello를 참조 하십시오 [Azure CDN 규칙 엔진 기능](../../cdn/cdn-rules-engine-reference-features.md)합니다.

## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구

Azure CDN을 통해 blob를 액세스할 때 비용을 지불 [Blob 저장소 가격](https://azure.microsoft.com/pricing/details/storage/blobs/) hello 가장자리 노드와 hello 원점 (Blob storage) 간의 트래픽에 대 한 및 [CDN 가격](https://azure.microsoft.com/pricing/details/cdn/) hello 가장자리 노드 모두에서 액세스 되는 데이터에 대 한 합니다.

예를 들어, Azure CDN을 사용하여 액세스되는 저장소 계정이 미국 서부에 있습니다. Hello 영국에에서 다른 사람이 열려고 tooaccess hello 중 hello CDN 통해 해당 저장소 계정에서 blob, Azure는 먼저 해당 blob에 대 한 hello 영국에 가장 가까운 hello 가장자리 노드를 확인 합니다. 하는 경우 발견 hello blob의 해당 복사본에 액세스 하 고 CDN 가격 없으므로 사용할 hello CDN에 액세스 하는 합니다. 찾을 수 없는 경우, Azure는 송신 됩니다 hello blob toohello 가장자리 노드를 복사 및 트랜잭션 요금에 지정 된 hello로 Blob 저장소 가격 한 다음 있는 CDN 청구 됩니다 hello 가장자리 노드에 hello 파일에 액세스 합니다.

Hello 확인할 때 [가격 책정 페이지 CDN](https://azure.microsoft.com/pricing/details/cdn/), 사용자 지정 도메인 이름에 대 한 HTTPS 지원 참고는 Verizon 제품 (Standard 및 Premium)에서 Azure CDN에 사용할 수만 있습니다.

## <a name="next-steps"></a>다음 단계

[Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성](storage-custom-domain-name.md)
