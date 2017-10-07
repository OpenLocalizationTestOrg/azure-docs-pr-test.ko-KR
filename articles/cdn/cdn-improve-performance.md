---
title: "Azure CDN에서 파일을 압축 하 여 aaaImprove 성능을 | Microsoft Docs"
description: "Tooimprove 파일 속도 증가 페이지 로드 성능 Azure CDN에서 파일을 압축 하 여 전송 하는 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Azure CDN에서 파일을 압축하여 성능 향상
압축은 단순 하 고 효과적인 방법 tooimprove 파일 전송 속도 및 하기 전에 파일 크기를 줄여 증가 페이지 로드 성능 hello 서버에서 전송 됩니다. 대역폭 비용을 절감하고 사용자에게 반응이 빠른 환경을 제공합니다.

두 가지가 tooenable 압축:

* 이 경우 hello CDN 통과 hello 압축 된 파일 및 배달 요청 하는 압축 된 파일 tooclients 원본 서버에서 압축을 사용할 수 있습니다.
* 압축 사례 hello CDN 압축 파일 hello 및 hello 원본 서버에 의해 압축 되지 않은 경우에 tooend 사용자 제공 CDN 지 서버에서 직접 사용할 수 있습니다.

> [!IMPORTANT]
> CDN 구성 변경 내용이 hello 네트워크를 통해 일부 시간 toopropagate 합니다.  <b>Akamai의 Azure CDN</b> 프로필의 경우, 일반적으로 1분 이내에 전파가 완료됩니다.  <b>Verizon의 Azure CDN</b> 프로필의 경우, 변경 내용이 일반적으로 90분 내에 적용됩니다.  대기 하는 1 ~ 2 시간 toobe hello 압축 설정 문제를 해결 하기 전에 toohello Pop 전파 있는지 고려해 야 인 경우 hello 처음으로 CDN 끝점에 대 한 압축을 설정 했습니다.
> 
> 

## <a name="enabling-compression"></a>압축을 사용하도록 설정
> [!NOTE]
> hello Standard 및 Premium CDN 계층 제공 hello 같은 압축 기능을 하지만 hello 사용자 인터페이스 다릅니다.  Standard 및 Premium CDN 계층 hello 차이점에 대 한 자세한 내용은 참조 [Azure CDN 개요](cdn-overview.md)합니다.
> 
> 

### <a name="standard-tier"></a>표준 계층
> [!NOTE]
> 이 섹션을 너무 적용**Verizon에서 Azure CDN 표준** 및 **Akamai에서 Azure CDN 표준** 프로필입니다.
> 
> 

1. Hello CDN 프로필 페이지에서 원하는 toomanage hello CDN 끝점을 클릭 합니다.
   
    ![CDN 프로필 페이지 끝점](./media/cdn-file-compression/cdn-endpoints.png)
   
    hello CDN 끝점 페이지가 열립니다.
2. Hello 클릭 **구성** 단추입니다.
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-config-btn.png)
   
    hello CDN 구성 페이지가 열립니다.
3. **압축**을 켭니다.
   
    ![CDN 압축 옵션](./media/cdn-file-compression/cdn-compress-standard.png)
4. Hello 기본 형식을 사용 하거나 제거 하거나 파일 형식을 추가 하 여 hello 목록을 수정 합니다.
   
   > [!TIP]
   > While 가능한 ZIP, MP3, MP4, JPG 등 tooapply 압축 toocompressed 형식을 권장 되지 않습니다.
   > 
   > 
5. Hello을 클릭 하 여 변경한 후 **저장** 단추입니다.

### <a name="premium-tier"></a>프리미엄 계층
> [!NOTE]
> 이 섹션을 너무 적용**Verizon에서 Azure CDN Premium** 프로필입니다.
> 
> 

1. Hello CDN 프로필 페이지에서 클릭 hello **관리** 단추입니다.
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.  **압축**을 클릭합니다.

    ![파일 압축 선택](./media/cdn-file-compression/cdn-compress-select.png)
   
    압축 옵션이 표시됩니다.
   
    ![파일 압축](./media/cdn-file-compression/cdn-compress-files.png)
3. Hello를 클릭 하 여 압축을 사용 하도록 설정 **압축 사용** 라디오 단추입니다.  Hello MIME 형식을 입력 toocompress hello에 쉼표로 구분 된 목록 (공백 없이)으로 원하는 **파일 형식을** 텍스트 상자에 붙여넣습니다.
   
   > [!TIP]
   > While 가능한 ZIP, MP3, MP4, JPG 등 tooapply 압축 toocompressed 형식을 권장 되지 않습니다. 
   > 
   > 
4. Hello을 클릭 하 여 변경한 후 **업데이트** 단추입니다.

## <a name="compression-rules"></a>압축 규칙
이 테이블은 모든 시나리오에 적용되는 Azure CDN 압축 동작을 설명합니다.

> [!IMPORTANT]
> **Verizon의 Azure CDN** (Standard 및 Premium)의 경우, 적합한 파일만 압축될 수 있습니다.  압축에 적합 toobe, 파일을 수행 해야합니다.
> 
> * 128바이트 초과.
> * 1MB 미만.
> 
> **Akamai의 Azure CDN**의 경우, 모든 파일이 압축에 적합합니다.
> 
> 모든 Azure CDN 제품의 경우, 파일은 [압축용으로 구성된](#enabling-compression)MIME 형식이어야 합니다.
> 
> **Verizon의 Azure CDN** 프로필(Standard 및 Premium)은 **gzip**(GNU zip), **deflate** 또는 **bzip2** 또는 **br**(Brotli) 인코딩을 지원합니다. Brotli 인코딩에 hello 압축 hello 가장자리에만 수행 됩니다. hello 클라이언트/브라우저가 Brotli 인코딩에 대 한 hello 요청을 전송 해야 하 고 hello 압축된 자산 해야 압축 된 hello 원본 쪽에서 먼저 합니다. 
>
>**Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.
> 
> **Akamai에서 azure CDN** 끝점 항상 요청 **gzip** 인코드된 hello 클라이언트 요청에 관계 없이 hello 원점에서 파일입니다. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>압축이 비활성화되었거나 파일이 압축에 부적합
| 클라이언트 요청 형식(Accept-Encoding 헤더를 통한) | 캐시된 파일 형식 | CDN 응답 toohello 클라이언트 | 참고 사항 |
| --- | --- | --- | --- |
| 압축 |압축 |압축 | |
| 압축 |미압축 |미압축 | |
| 압축 |캐시되지 않음 |압축 또는 미압축 |원본 응답에 따라 결정 |
| 미압축 |압축 |미압축 | |
| 미압축 |미압축 |미압축 | |
| 미압축 |캐시되지 않음 |미압축 | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>압축이 활성화되고 파일이 압축에 적합
| 클라이언트 요청 형식(Accept-Encoding 헤더를 통한) | 캐시된 파일 형식 | CDN 응답 toohello 클라이언트 | 참고 사항 |
| --- | --- | --- | --- |
| 압축 |압축 |압축 |지원되는 형식 간 CDN 코드 변환 |
| 압축 |미압축 |압축 |CDN이 압축 수행 |
| 압축 |캐시되지 않음 |압축 |원본이 미압축 상태로 반환되면 CDN가 압축을 수행합니다.  **Azure CDN에서 Verizon** 전달 hello hello 첫 번째 요청과 다음 압축에 대해 압축 되지 않은 파일 및 캐시 hello 후속 요청에 대 한 파일입니다.  `Cache-Control: no-cache` 헤더를 포함한 파일을 압축되지 않습니다. |
| 미압축 |압축 |미압축 |CDN이 압축 해제 수행 |
| 미압축 |미압축 |미압축 | |
| 미압축 |캐시되지 않음 |미압축 | |

## <a name="media-services-cdn-compression"></a>미디어 서비스 CDN 압축
미디어 서비스 CDN 사용 스트리밍 끝점을 압축 콘텐츠 유형만 hello에 대 한 기본으로 설정 됩니다: 응용 프로그램/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, 응용 프로그램/f4m + xml입니다. 있습니다 수 없는 설정/해제 hello에 대 한 압축 hello Azure 포털을 사용 하 여 형식을 설명 합니다.  

## <a name="see-also"></a>참고 항목
* [CDN 파일 압축 문제 해결](cdn-troubleshoot-compression.md)    

