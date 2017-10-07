---
title: "hello Azure Marketplace의에서 가상 컴퓨터 이미지 aaaManaging | Microsoft Docs"
description: "어떻게 toomanage 가상 컴퓨터 이미지 hello Azure Marketplace에서에서 초기 게시 한 후에 자세한 가이드"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>가상 컴퓨터에 대 한 제작 후 가이드 hello Azure Marketplace에서 제공
이 문서는 가상 컴퓨터 실시간 행사 hello Azure Marketplace에서에서 업데이트 하는 방법을 설명 합니다. 하나 이상의 새 Sku tooan 기존 제안을 추가 hello 과정을 안내 합니다. 또한 과정을 안내 hello 프로세스 hello Marketplace에서에서 가상 컴퓨터 실시간 제안 또는 SKU를 제거 합니다.

Hello에 제안을/SKU를 준비 하는 후 [Azure 포털](http://portal.azure.com), hello 텍스트 상자에 다음을 변경할 수 없습니다.

* **식별자를 제공**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다. **VM 이미지** > **제품 식별자**를 클릭합니다.
* **SKU 식별자**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다. **SKU** > **SKU 추가**를 클릭합니다.
* **게시자 Namespace**: hello 게시 포털 이동 너무**가상 컴퓨터** > **연습** > **알려 주세요.에 대 한 사용자 회사** ("단계 2 등록 Your Company" 아래에서 찾을 수) > **게시자 Namespace** > **Namespace**합니다.

Hello 제공/SKU hello에 나열 된 후 [마켓플레이스](http://azure.microsoft.com/marketplace), hello 텍스트 상자에 다음을 변경할 수 없습니다.

* **식별자를 제공**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다. **VM 이미지** > **제품 식별자**를 클릭합니다.
* **SKU 식별자**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다. **SKU** > **SKU 추가**를 클릭합니다.
* **게시자 Namespace**: hello 게시 포털 이동 너무**가상 컴퓨터** > **연습** > **알려 주세요.에 대 한 사용자 회사** ("단계 2 등록" 아래에서 찾을 수) **게시자 Namespace** > **Namespace**합니다.
* **포트**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다. **VM 이미지** > **포트 열기**를 클릭합니다.
* **나열된 SKU의 가격 책정 변경**
* **나열된 SKU의 청구 모델 변경**
* **나열된 SKU의 청구 지역 제거**
* **변화 하는 hello 데이터 디스크 나열된 SKU(s) 개수**

## <a name="update-hello-technical-details-of-a-sku"></a>SKU의 hello 기술 세부 정보 업데이트
새 버전 toohello tooadd SKU를 나열 하 고 자신의 구독을 다시 게시, 다음이 단계를 수행:

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭 합니다.
4. Hello에 **Sku** 섹션에서 hello tooupdate SKU를 찾습니다.
5. Hello SKU에 대 한 새 버전 번호를 추가 하 고 hello 클릭  **+**  단추입니다. hello 새 버전은 X, Y 및 Z는 정수 x.y.z 형식이 며 형식에서 이어야 합니다. 버전 변경은 증분되어야만 합니다.
6. Hello에 **OS VHD URL** 상자 hello 공유 액세스 서명 URI 생성 hello 운영 체제 VHD에 대 한 입력 하 고 hello 변경 내용을 저장 합니다.

   > [!IMPORTANT]
   > 있습니다 수 증가/감소 나열 된 SKU의 hello 데이터 디스크 개수입니다. 이 경우 새로운 SKU toocreate가 필요합니다. 자세한 지침은 toohello 섹션을 참조 하십시오. [아래 나열 된 제품은 새로운 SKU 추가](#add-a-new-sku-under-a-listed-offer)합니다.
   >
   >
7. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
8. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![VM 이미지](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>제공 하는 서비스 또는 SKU의 hello 기술 세부 정보 업데이트
Hello 배경이 (마케팅, 법률, 지원, 범주)을 업데이트할 수 있습니다 hello Marketplace에서에서 라이브 제안 또는 SKU의 세부 정보입니다.

### <a name="update-hello-offer-description-and-logos"></a>Hello 서비스 설명 및 로고를 업데이트 합니다.
tooupdate hello 세부 정보를 제공 하 고 자신의 구독을 다시 게시, 다음이 단계를 수행:

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.
4. **영어(미국)**을 클릭합니다.
5. Hello 클릭 **세부 정보** 탭 합니다. Hello에 **설명** 섹션, 업데이트에서 hello 제공 **제목**, **요약**, 및 **세부 요약** hello 변경 내용을 저장 합니다.

   > [!NOTE]
   > Hello SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해 야 합니다. 
   * Hello 서비스 설명 및 hello SKU 설명에 대 한 중복 텍스트를 입력 하지 마십시오.
   * Hello SKU 제목과 hello 제공 긴 요약에 대 한 중복 텍스트를 입력 하지 마십시오. 
   * Hello SKU 제목과 hello 제공 요약에 대 한 중복 텍스트를 입력 하지 마십시오.
   >
   >

    ![세부 정보](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. Hello에 **로고** hello 섹션 **세부 정보** 탭, hello 로고를 업데이트 합니다. Hello 로고 hello 따라야 [Azure 마켓플레이스 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.

   > [!NOTE]
   > 대표 아이콘은 선택 사항입니다. Hero 아이콘 하지 tooupload를 선택할 수 있습니다. 그러나 hero 아이콘을 업로드 한 후이 없는 프로 비전 toodelete hello에서 포털을 게시 합니다. Hello에 따라 [hero 아이콘 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.
   >
   >
7. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
8. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![로고](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>업데이트 hello SKU 설명
SKU에 자세히 설명 하 고 자신의 구독을 다시 게시 tooupdate hello 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.
4. **영어(미국)**을 클릭합니다.
5. Hello 클릭 **계획** 탭 합니다. Hello에 **Sku** 섹션, SKU hello 업데이트 **제목**, **요약**, 및 **설명** hello 변경 내용을 저장 합니다.

   > [!NOTE]
   > Hello SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해 야 합니다. 
   * Hello 서비스 설명 및 hello SKU 설명에 대 한 중복 텍스트를 입력 하지 마십시오. 
   * Hello SKU 제목과 hello 제공 긴 요약에 대 한 중복 텍스트를 입력 하지 마십시오. 
   * Hello SKU 제목과 hello 제공 요약에 대 한 중복 텍스트를 입력 하지 마십시오.
   >
   >
6. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
7. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![요금제](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>기존 링크 변경 또는 새 링크 추가
toochange 기존 연결 또는 새 링크를 추가 하 고 제안을 다시 게시 한 다음, 다음이 단계를 수행 합니다.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.
4. **영어(미국)**을 클릭합니다.
5. Hello 클릭 **링크** 탭 합니다.
6. 새 링크를 hello tooadd **링크** 섹션에서 클릭 **+ 링크 추가**합니다. Hello에 **링크 추가** 대화 상자에서 hello 링크 입력 **제목** 및 **URL** hello 변경 내용을 저장 합니다. 고객에게 도움이 될 수 있는 정보를 포함하는 모든 링크를 입력할 수 있습니다.
7. hello 링크를 선택 하 고 hello 클릭 tooupdate 또는 기존 링크를 삭제 **편집** 단추나 hello **삭제** 단추입니다.

   > [!NOTE]
   > 이러한 링크 프로덕션 요청 프로세스 중에 유효성이 검사 가져오기 때문에이 섹션에 입력 한 hello 링크가 제대로 작동 하는지 확인 합니다.
   >
   >
8. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
9. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![링크](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![링크 추가](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>기존 샘플 이미지 변경 또는 새 샘플 이미지 추가
기존 샘플 toochange 이미지 또는 새 샘플 이미지를 추가 하 고 다음 제안을 다시 게시, 다음이 단계를 수행 합니다.

> [!NOTE]
> Hello에 하나의 샘플 이미지가 표시 되어 [Azure 포털](https://portal.azure.com)합니다.
>
>

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.
4. **영어(미국)**을 클릭합니다.
5. Hello 클릭 **샘플 이미지가** 탭 합니다.
6. tooadd hello에서 새 샘플 이미지 **샘플 이미지** 섹션에서 클릭 **새 이미지 업로드** hello 변경 내용을 저장 합니다.

   > [!NOTE]
   > 샘플 이미지를 포함하는 것은 선택적입니다.
   >
7. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
8. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![샘플 이미지](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Hello 법적 콘텐츠 업데이트
tooupdate 법적 콘텐츠 hello 및 제안을 다시 게시, 다음이 단계를 수행 합니다.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.
4. **영어(미국)**을 클릭합니다.
5. Hello 클릭 **법적** 탭 합니다. Hello에 **법적** 섹션에서 사용자 정책/사용 약관을 업데이트 합니다. 입력 하거나 hello 정책/조건 hello에 붙여 **사용 약관** 상자 고 hello 변경 내용을 저장 합니다.
6. 사용 약관 hello에 대 한 hello 문자 제한 길이 1 백만 자 합니다.
7. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
8. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![법적 정보](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Hello 지원 정보를 업데이트 합니다.
tooupdate hello 지원 정보 및 제안 다시 게시 하 고, 다음이 단계를 수행 합니다.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **지원** 탭 합니다.
4. Hello에 **엔지니어링 문의** 섹션 업데이트 hello 엔지니어링 연락처 정보입니다. 이러한 세부 정보는만 hello 파트너와 Microsoft 간의 내부 통신에 사용 됩니다.
5. Hello에 **고객 지원 서비스** 섹션에서 업데이트 hello 지원 연락처 정보 및 hello **지원 URL**합니다. 이러한 세부 정보는만 hello 파트너와 Microsoft 간의 내부 통신에 사용 됩니다.

   > [!NOTE]
   > Tooprovide만 전자 메일 지원을 원하는 경우 hello에 더미 전화 번호를 입력 **고객 지원 서비스** 섹션. 이 경우 사용자가 제공한 hello 전자 메일을 대신 사용 됩니다.
   >
   >
6. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
7. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![지원](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>업데이트 hello 범주
범주 제안에 대 한 섹션 및 제품을 다시 게시 tooupdate hello 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **범주** 탭 합니다.
4. Hello에 **범주** 섹션, 자신의 구독에 대 한 hello 범주를 업데이트 하 고, hello 변경 내용을 저장 합니다. Hello Azure 마켓플레이스 갤러리에 대 한 toofive 범주를 선택할 수 있습니다.
5. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
6. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![범주](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>나열된 제품에 새 SKU 추가
라이브 해당 제품에 대 한 새로운 SKU tooadd 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다. 그런 다음 **SKU 추가**를 클릭합니다. 
4. Hello 대화 상자에서 입력 한 **SKU 식별자** 소문자로 표시 합니다. 선택 hello **라이선스 (BYOL) 청구 모델에 고유한** 확인란 toopublish 선택 hello 새로운 SKU BYOL 청구 모델을 사용 합니다. 그렇지 않으면 hello 확인란의 선택을 취소 합니다. Hello 눈금 표시가 toocreate 새로운 SKU를 클릭 합니다. Hello BYOL 청구 모델을 선택 하지 않은 hello 청구 모델 toohourly 자동 설정 됩니다. Hello 시간별 요금 청구 모델에 대 한 hello 30 일 무료 평가판 선택 **ׁ ´ ** 에 대 한 **무료 평가판을 사용할 수 있습니까?** 그렇지 않은 경우 **평가판 없음**을 선택합니다. (**무료 평가판을 사용할 수 있는?**  새로운 SKU hello를 만드는 동안 BYOL 선택 하지 않은 경우에 나타납니다.)

   > [!IMPORTANT]
   > **솔루션 템플릿을 통해 항상 구입 해야 하기 때문에이 SKU hello Marketplace에서에서 숨기기** 해야 **예** *만* 솔루션 템플릿을 게시 하기 위한 승인 하는 경우. 그렇지 않은 경우 이 옵션은 항상 **아니요**로 표시되어야 합니다.
   >
   >
4. Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭과 확인 hello 사용자가 만든 새로운 SKU입니다.
5. tooset 최대 새로운 SKU hello, 참조 [VM 이미지에 대 한 인증을 가져오는](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) 지침에 대 한 합니다.
6. tooadd 마케팅 자료에 대 한 새로운 SKU hello, 참조 [마케팅 콘텐츠 제공 마켓플레이스](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.
7. tooadd 가격 정보에 대 한 새로운 SKU hello, 참조 [가격 설정](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)합니다.
8. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
9. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![SKU 추가](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>나열 된 SKU에 대 한 hello 데이터 디스크 개수 변경
있습니다 수 증가/감소 나열 된 SKU의 hello 데이터 디스크 개수입니다. 이 경우 새로운 SKU toocreate가 필요합니다. 자세한 지침은 toohello 섹션을 참조 하십시오. [아래 나열 된 제품은 새로운 SKU 추가](#add-a-new-sku-under-a-listed-offer)합니다.

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Hello Marketplace에서에서 나열 된 제안을 삭제 합니다.
다양 한 측면 toobe 요청 tooremove 라이브 제품의 hello 경우에서 처리 해야 합니다. 다음이 단계를 수행 하는 hello 지원 팀 tooremove hello Marketplace에서에서 나열 된 제품의에서 tooget 지침:

1. Hello에 지원 티켓을 발생 시키는 [인시던트를 만들](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) 페이지.

2. **제품 관리**로 **문제 형식**을 선택하고 **프로덕션 환경에서 제품 및/또는 SKU 수정**으로 **범주**를 선택합니다.
3. Hello 요청을 제출 합니다.

hello 지원 팀 hello 제공/SKU 삭제 프로세스를 안내합니다.

> [!NOTE]
> 초안 상태 (하지만 준비 또는 프로덕션) 되는 동안 항상 hello 제공을 삭제할 수 있습니다. Hello에 **기록** 탭을 클릭 **초안 버리기**합니다.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Hello Marketplace에서에서 나열 된 SKU를 삭제 합니다.
toodelete hello Marketplace에서에서 나열 된 SKU는 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.

2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 창에서 클릭 hello **SKU** 탭 합니다.
4. 선택 hello SKU toodelete, 원하고 hello 클릭 **삭제** 단추입니다.
5. Toohello 이동 **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** hello Marketplace에서에서 toorepublish hello 제공 합니다.
6. Hello 제품은 시장 hello에 다시 게시 하면 hello SKU 마켓플레이스 hello 및 hello Azure 포털에서 삭제 됩니다.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Hello Marketplace에서에서 나열 된 SKU의 hello 현재 버전을 삭제 합니다.
다음이 단계를 수행 하는 hello toodelete hello Marketplace에서에서 나열 된 SKU의 현재 버전: 

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.

2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭 합니다.
4. 인 현재 SKU hello 선택 버전 hello 누르고 toodelete, 원하는 **삭제** 단추입니다.
5. Toohello 이동 **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** hello Marketplace에서에서 toorepublish hello 제공 합니다.
6. Hello 제안을 가져옵니다 hello Marketplace에에서 다시 게시 하면 후 hello 현재 버전의 hello 나열 된 SKU hello 마켓플레이스와 hello Azure 포털에서 삭제 됩니다. hello SKU 다음 롤백됩니다 tooits 이전 버전입니다.

## <a name="revert-hello-listing-price-tooproduction-values"></a>가격 tooproduction 값을 나열 하는 hello 되돌리기
toorevert hello 목록 가격 tooproduction 값 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.
2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **가격 책정** 탭 합니다.
4. 가격 원하는 지역을 선택 tooreset 합니다.

    ![가격 책정 지역](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Sku 시간별 요금 청구 모델에 대 한 hello 선택한 영역에 대 한 프로덕션에 있는 것 처럼 모든 hello 코어에 대 한 hello 가격 다시 설정 합니다. BYOL 청구 모델에 대 한 Sku, 확인 hello hello hello SKU에 대 한 확인란을 선택 하 여 hello 지역에서 사용할 수 있는 SKU hello **EXTERNALLY-LICENSED (BYOL) SKU 가용성** 섹션.

    ![가격 책정 모델](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. **미국의 가격에 따라 다른 마켓의 가격 자동 설정**을 클릭합니다.

   > [!NOTE]
   > hello 단추의 레이블을 선택 하는 hello 지역에 따라 달라질 수 있습니다. 미국을 선택 하는 것 때문에 hello 단추인 **AUTOPRICE 다른 시장 기반 ON 가격 IN 통합 상태**합니다.
   >
   >

    ![가격 자동 설정](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. 에 hello Autoprice 마법사의 1 페이지 hello 기본 시장을 선택 하 고 hello 클릭 **화살표** 단추입니다.

    ![기본 시장](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. 2 페이지 서비스 계획과 미터 (코어)를 선택 하 고 hello 클릭 **화살표** 단추입니다.

    ![서비스 계획 및 미터](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. 3 페이지 클릭 **토글 모든** tooselect 모든 지역입니다. 또는 특정 지역에 대한 확인란을 수동으로 선택할 수 있습니다. Hello 클릭 **화살표** 단추입니다.

    ![시장 선택](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. 4 페이지 hello 환율을 검토 하 고 클릭 **마침**합니다. hello 마법사 tooyour 선택 항목에 따라 가격 hello를 다시 설정 합니다.

11. Hello에 **가격 책정** 탭을 클릭 **보기 및 변경 내용 요약**합니다.
    **버전 보기**에서 **초안**을 선택하고 **비교 대상**에서 **프로덕션**을 선택합니다. 가격 책정 차이점이 표시 되 면 hello 가격 되돌릴 toohello 프로덕션 값 성공적으로.

    ![요약 및 변경 내용 보기](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
13. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

## <a name="revert-hello-billing-model-tooproduction-values"></a>청구 모델 tooproduction 값 hello 되돌리기
toorevert hello 청구 모델 tooproduction 값을 다음이 단계를 따르십시오.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.

2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다.
4. Hello 클릭 **편집** 단추 toorevert hello에 대 한 청구 모델입니다. Hello 창이 열리면을 늘리거나 hello **대금 청구 및 라이선스 (즉, Bring Your 자체 라이선스) Azure에서 외부에서 수행 되** 확인란 합니다.

    ![청구 편집](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. 이 문서의 "Revert hello 가격 tooproduction 값 나열 하 는" hello 단계를 수행 합니다.
6. Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다. 참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.
7. 제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다. 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>나열 된 SKU toohello 프로덕션 값의 표시 유형 설정 hello 되돌리기
다음이 단계를 수행 하는 나열 된 SKU toohello 프로덕션 값의 toorevert hello 표시 유형을 설정 합니다.

1. Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.

2. Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.
3. Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다.
4. SKU을 선택 하 고 hello SKU toohello 프로덕션 값의 표시 유형을 설정 hello를 되돌립니다.

    ![표시 유형](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Hello 변경을 마친 후 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.

## <a name="see-also"></a>참고 항목
* [시작: 제안 toohello Azure 마켓플레이스에서 게시](marketplace-publishing-getting-started.md)
* [지급 보고 이해](marketplace-publishing-report-payout.md)
* [클라우드 솔루션 공급자 재판매인 인센티브 변경](marketplace-publishing-csp-incentive.md)
* [Hello Marketplace에서에서 일반적인 게시 문제 해결](marketplace-publishing-support-common-issues.md)
* [게시자로 지원 받기](marketplace-publishing-get-publisher-support.md)
* [온-프레미스 VM 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)
* [Hello Azure 미리 보기 포털에서 Windows를 실행 하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
