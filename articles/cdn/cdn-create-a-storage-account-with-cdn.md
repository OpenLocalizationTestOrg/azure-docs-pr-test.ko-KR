---
title: "Azure CDN 사용 되는 Azure 저장소 계정과 aaaIntegrate | Microsoft Docs"
description: "Toouse hello Azure 콘텐츠 배달 네트워크 (CDN) toodeliver 고대역폭 콘텐츠를 캐시 하 여 Azure 저장소에서 blob 하는 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Azure CDN과 Azure Storage 계정 통합
CDN 사용된 toocache Azure 저장소에서 콘텐츠를 수 있습니다. Blob 및 hello 미국, 유럽, 아시아, 오스트레일리아 및 남아메리카에 있는 물리적 노드에서 계산 인스턴스의 정적 콘텐츠를 캐시 하 여 고대역폭 콘텐츠를 배달 하기 위한 글로벌 솔루션 개발자에 게 제공 합니다.

## <a name="step-1-create-a-storage-account"></a>1 단계: 저장소 계정 만들기
다음 프로시저 toocreate Azure 구독에 대 한 새 저장소 계정을 hello를 사용 합니다. 저장소 계정을 통해 Azure 저장소 서비스에 액세스할 수 있습니다. hello 저장소 계정은 hello 최고 수준의 각 hello Azure 저장소 서비스 구성 요소에 액세스 하기 위한 hello 네임 스페이스를 나타냅니다: Blob 서비스, 큐 서비스 및 테이블 서비스입니다. 자세한 내용은 참조 toohello [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md)합니다.

서비스 관리자에 게 또는 연결 된 hello에 대 한 공동 관리자 여야 합니다 toocreate 저장소 계정, 구독 합니다.

> [!NOTE]
> 몇 가지가 toocreate hello Azure 포털 및 Powershell을 포함 하 여 저장소 계정을 사용할 수 있습니다.  이 자습서에서는 Azure 포털 hello를 사용해 보겠습니다.  
> 
> 

**Azure 구독에 대 한 저장소 계정 toocreate**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 위 모서리에서 선택 **새로**합니다. Hello에 **새로** 대화 상자에서 **데이터 + 저장소**, 클릭 **저장소 계정**합니다.
    
    hello **저장소 계정 만들기** 블레이드 나타납니다.   

    ![저장소 계정 만들기][create-new-storage-account]  

3. Hello에 **이름** 필드 하위 도메인 이름을 입력 합니다. 이 입력에는 3-24자의 소문자와 숫자를 사용할 수 있습니다.
   
    이 값은 hello hello 구독에 대 한 Blob, 큐 또는 테이블 리소스를 처리 하는 데 사용 되는 URI 내에서 hello 호스트 이름이 됩니다. 하려면 hello Blob 서비스에서에서 컨테이너 리소스에 주소를 사용 하는 URI, 형식에 따라 hello에 여기서  *&lt;StorageAccountLabel&gt;*  toohello 값에 입력 한 참조 **URL입력**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **중요:** URL 레이블 forms hello 하위 도메인의 hello 저장소 계정 URI hello 및 Azure에서 모든 호스팅된 서비스에서 고유 해야 합니다.
   
    이 값은 프로그래밍 방식으로이 계정에 액세스할 때 hello 또는 hello 포털에서이 저장소 계정 이름으로도 사용 됩니다.
4. 에 대 한 hello 기본값 그대로 두고 **배포 모델**, **kind 계정**, **성능**, 및 **복제**합니다. 
5. 선택 hello **구독** 된와 hello 저장소 계정은 사용 됩니다.
6. **리소스 그룹**을 선택하거나 만듭니다.  리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
7. 저장소 계정의 위치를 선택합니다.
8. **만들기**를 클릭합니다. hello hello 저장소 계정을 만드는 과정은 몇 분 toocomplete를 걸릴 수 있습니다.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Hello 저장소 계정에 대해 CDN을 사용 하는 2 단계:

Hello 최신 통합 저장소 포털 확장을 종료 하지 않고 저장소 계정에 대해 CDN을 지금 설정할 수 있습니다. 

1. Hello 저장소 계정을 선택를 다음 검색 "CDN" 또는 스크롤 등에 hello 왼쪽된 탐색 메뉴에서 "Azure CDN"를 클릭 합니다.
    
    hello **Azure CDN** 블레이드 나타납니다.

    ![cdn 사용 탐색][cdn-enable-navigation]
    
2. Hello 필요한 정보를 입력 하 여 새 끝점 만들기
    - **CDN 프로필**: 새 프로필을 만들거나 기존 프로필을 사용할 수 있습니다.
    - **가격 책정 계층**: tooselect 새 CDN 프로필을 만드는 경우는 가격 책정 계층에 하면 됩니다.
    - **CDN 끝점 이름**: 원하는 끝점 이름을 입력합니다.

    > [!TIP]
    > 만든 hello CDN 끝점이 기본적으로 원점으로 저장소 계정의 hello 호스트 이름을 사용합니다.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. 를 만든 후 hello 새 끝점에에서 표시 됩니다 위의 hello 끝점 목록입니다.

    ![CDN 저장소 새 끝점][cdn-storage-new-endpoint]

> [!NOTE]
> 또한 tooAzure CDN 확장 tooenable CDN을 이동할 수 있습니다. [자습서](#Tutorial-cdn-create-profile)합니다.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>3단계: 추가 CDN 기능 사용

저장소 계정 "Azure CDN" 블레이드에서 hello 목록 tooopen CDN 구성 블레이드에서 hello CDN 끝점을 클릭 합니다. 전송에 대해 압축, 쿼리 문자열, 지역 필터링 등과 같은 추가 CDN 기능을 사용하도록 설정할 수 있습니다. 사용자 지정 도메인 매핑에 tooyour CDN 끝점을 추가 하 고 사용자 지정 도메인 HTTPS를 사용 하도록 설정 수도 있습니다.
    
![CDN 저장소 CDN 구성][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>4단계: CDN 콘텐츠 액세스
hello 포털에서 사용 하 여 hello CDN URL 제공 tooaccess hello CDN에서 콘텐츠를 캐시 합니다. 캐시 된 blob에 대 한 hello 주소 비슷한 toohello 다음 됩니다.

http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> CDN 액세스 tooa 저장소 계정을 사용 하도록 설정 하면 공개적으로 사용 가능한 모든 개체가 CDN에 지 캐싱 대상이 됩니다. 현재 hello CDN에에서 캐시 된 개체를 수정 하면 hello CDN 캐시 hello 콘텐츠 활성 시간 기간이 만료 된 경우 콘텐츠를 새로 고칠 때까지 hello 새 콘텐츠는 hello CDN 통해 사용할 수 없습니다.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>5 단계: hello CDN에서에서 콘텐츠를 제거 합니다.
더 이상 원할 경우 toocache 개체 hello Azure 콘텐츠 배달 네트워크 (CDN)의 단계를 수행 하는 hello 중 하나를 수행할 수 없습니다.

* Hello 공용이 아닌 전용 컨테이너를 만들 수 있습니다. 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../storage/blobs/storage-manage-access-to-resources.md) 자세한 정보에 대 한 합니다.
* 사용 하지 않도록 설정 하거나 관리 포털 hello를 사용 하 여 hello CDN 끝점을 삭제할 수 있습니다.
* 에 호스팅된 서비스 toono 긴 응답 toorequests hello 개체에 대 한를 수정할 수 있습니다.

이미 hello CDN에에서 캐시 된 개체는 hello 끝점은 제거 하거나 hello 개체에 대 한 hello 활성 시간 기간이 만료 될 때까지 캐싱된 상태로 유지 됩니다. Hello 활성 시간 기간이 만료 되 면 hello CDN 끝점이 여전히 유효한 지 여부 및 익명 액세스할 수 hello 개체 hello CDN toosee를 확인 합니다. 그렇지 않은 경우에 hello 개체가 더 이상 캐시 됩니다.

## <a name="additional-resources"></a>추가 리소스
* [어떻게 tooMap CDN 콘텐츠 tooa 사용자 지정 도메인](cdn-map-content-to-custom-domain.md)
* [사용자 지정 도메인에 대해 HTTPS 사용](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
