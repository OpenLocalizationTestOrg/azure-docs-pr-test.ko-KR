---
title: "CDN aaaAzure 규칙 엔진 일치 조건을 | Microsoft Docs"
description: "Azure CDN 규칙 엔진 일치 조건 및 기능에 대한 참조 설명서"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Azure CDN 규칙 엔진 일치 조건
이 항목 목록에 자세히 설명에는 사용할 수 있는 일치 조건에 대 한 Azure 네트워크 CDN (콘텐츠 배달) hello [규칙 엔진](cdn-rules-engine.md)합니다.

규칙의 두 번째 부분 hello는 hello 일치 조건입니다. 일치 조건은 기능 집합에 대해 수행할 특정 요청 유형을 식별합니다.

예를 들어 요청 헤더 정보 또는 특정 IP 주소 또는 국가에서 생성 된 특정 위치에 콘텐츠에 대 한 사용된 toofilter 요청 수 있습니다.

## <a name="always"></a>항상

hello 항상 일치 조건이 디자인 된 tooapply 기능 tooall 요청의 기본 설정입니다.

## <a name="device"></a>장치

hello 장치 일치 조건은 해당 속성을 기반으로 하는 모바일 장치에서 수행 된 요청을 식별 합니다.  모바일 장치 검색은 [WURFL](http://wurfl.sourceforge.net/)을 통해 이루어집니다.  WURFL 기능 및 해당 CDN 규칙 엔진 변수는 아래에 나열되어 있습니다.

> [!NOTE] 
> hello에 아래 hello 변수는 지원 **클라이언트 요청 헤더를 수정** 및 **클라이언트 응답 헤더 수정** 기능입니다.

기능 | 변수 | 설명 | 샘플 값
-----------|----------|-------------|----------------
브랜드 이름 | %{wurfl_cap_brand_name} | Hello 장치의 hello 브랜드 이름을 나타내는 문자열입니다. | Samsung
장치 OS | %{wurfl_cap_device_os} | Hello 장치에 설치 된 hello 운영 체제를 나타내는 문자열입니다. | IOS
장치 OS 버전 | %{wurfl_cap_device_os_version} | Hello hello 장치에 설치 된 운영 체제의 hello 버전 번호를 나타내는 문자열입니다. | 1.0.1
이중 방향 | %{wurfl_cap_dual_orientation} | Hello 장치 이중 방향을 지원 하는지 여부를 나타내는 부울 값입니다. | true
HTML 기본 DTD | %{wurfl_cap_html_preferred_dtd} | HTML 콘텐츠에 대 한 hello 모바일 장치 기본 설정된 문서 형식 정의 (DTD)를 나타내는 문자열입니다. | 없음<br/>xhtml_basic<br/>html5
이미지 인라인 처리 | %{wurfl_cap_image_inlining} | 인코딩 이미지를 hello 장치 Base64 지원 하는지 여부를 나타내는 부울입니다. | false
Android 여부 | %{wurfl_vcap_is_android} | Hello 장치 hello Android OS를 사용 하는지 여부를 나타내는 부울 값입니다. | true
IOS 여부 | %{wurfl_vcap_is_ios} | Hello 장치에서 iOS를 사용 하는지 여부를 나타내는 부울입니다. | false
스마트 TV 여부 | %{wurfl_cap_is_smarttv} | Hello 장치 스마트 TV 인지 여부를 나타내는 부울입니다. | false
스마트폰 여부 | %{wurfl_vcap_is_smartphone} | Hello 장치가 smartphone 있는지 여부를 나타내는 부울입니다. | true
태블릿 여부 | %{wurfl_cap_is_tablet} | Hello 장치가 태블릿에서 있는지 여부를 나타내는 부울입니다. 이는 OS와 별개의 설명입니다. | true
무선 장치 여부 | %{wurfl_cap_is_wireless_device} | Hello 장치가 무선 장치 것으로 간주 하는지 여부를 나타내는 부울 값입니다. | true
마케팅 이름 | %{wurfl_cap_marketing_name} | Hello 장치 마케팅 이름을 나타내는 문자열입니다. | BlackBerry 8100 Pearl
모바일 브라우저 | %{wurfl_cap_mobile_browser} | Toorequest 콘텐츠 hello 장치를 사용 하는 hello 브라우저를 나타내는 문자열입니다. | Chrome
모바일 브라우저 버전 | %{wurfl_cap_mobile_browser_version} | Toorequest 콘텐츠 hello 장치를 사용 하는 hello 브라우저의 hello 버전을 나타내는 문자열입니다. | 31
모델 이름 | %{wurfl_cap_model_name} | Hello 장치의 모델 이름을 나타내는 문자열입니다. | s3
점진적 다운로드 | %{wurfl_cap_progressive_download} | 아직 다운로드 하는 동안 hello 장치의 오디오/비디오 재생 hello를 지원 하는지 여부를 나타내는 부울 값입니다. | true
릴리스 날짜 | %{wurfl_cap_release_date} | Toohello WURFL 데이터베이스를 추가 하는 hello 연도 및 월은 hello에 장치를 나타내는 문자열입니다.<br/><br/>형식: `yyyy_mm` | 2013_december
해상도 높이 | %{wurfl_cap_resolution_height} | Hello 장치 높이 픽셀 단위로 나타내는 정수입니다. | 768
해상도 너비 | %{wurfl_cap_resolution_width} | Hello 장치 너비 (픽셀) 나타내는 정수입니다. | 1024


## <a name="location"></a>위치

이러한 조건에 일치 hello 요청자의 위치에 따라 디자인 된 tooidentify 요청이 포함 됩니다.

이름 | 목적
-----|--------
AS 숫자 | 특정 네트워크에서 발생하는 요청을 식별합니다.
국가 | 지정 된 hello에서 발생 하는 요청을 식별 국가입니다.


## <a name="origin"></a>원본

이러한 조건에 일치 해당 지점 tooCDN 저장소나 고객 원본 서버 디자인 된 tooidentify 요청이 포함 됩니다.

이름 | 목적
-----|--------
CDN 원본 | CDN 저장소에 저장된 콘텐츠에 대한 요청을 식별합니다.
고객 원본 | 특정 고객 원본 서버에 저장된 콘텐츠에 대한 요청을 식별합니다.


## <a name="request"></a>요청

이러한 조건에 일치 해당 속성에 따라 디자인 된 tooidentify 요청이 포함 됩니다.

이름 | 목적
-----|--------
클라이언트 IP 주소 | 특정 IP 주소에서 발생하는 요청을 식별합니다.
쿠키 매개 변수 | 검사 hello 지정 hello에 대 한 각 요청을 연관 된 쿠키 값입니다.
쿠키 매개 변수 Regex | 확인 hello 쿠키 hello에 대 한 각 요청에 연결 된 정규식을 지정 합니다.
에지 Cname | Tooa 특정 가장자리 CNAME을 가리키는 요청을 식별 합니다.
참조 도메인 | 참조 하는 요청을 식별 hello hostname(s)를 지정 합니다.
요청 헤더 리터럴 | 지정 된 hello를 포함 하는 요청을 식별 헤더 집합 tooa 값을 지정 합니다.
요청 헤더 Regex | 지정 된 hello를 포함 하는 요청을 식별 헤더 집합 tooa 값 hello와 일치 하는 정규식을 지정 합니다.
요청 헤더 와일드카드 | 지정 된 hello를 포함 하는 요청을 식별 헤더 hello 지정 된 패턴과 일치 하는 tooa 값을 설정 합니다.
요청 메서드 | 해당 HTTP 메서드로 요청을 식별합니다.
요청 스키마 | 해당 HTTP 프로토콜로 요청을 식별합니다.

## <a name="url"></a>URL

조건에 일치 이러한 사이트의 Url에 따라 디자인 된 tooidentify 요청이 포함 됩니다.

이름 | 목적
-----|--------
URL 경로 디렉터리 | 해당 상대 경로로 요청을 식별합니다.
URL 경로 확장 | 해당 파일 확장명으로 요청을 식별합니다.
URL 경로 파일 이름 | 해당 파일 이름으로 요청을 식별합니다.
URL 경로 리터럴 | 요청을 비교 하 여의 상대 경로 toohello 값을 지정 합니다.
URL 경로 Regex | 요청을 비교 하 여의 상대 경로 toohello 지정 된 정규식입니다.
URL 경로 와일드카드 | 요청의 상대 경로 toohello 지정된 패턴과 비교합니다.
URL 쿼리 리터럴 | 요청을 비교 하 여의 쿼리 문자열 toohello 값을 지정 합니다.
URL 쿼리 매개 변수 | 지정된 된 패턴과 일치 하는 tooa 값을 설정 하는 문자열 매개 변수는 hello 지정 된 쿼리를 포함 하는 요청을 식별 합니다.
URL 쿼리 Regex | 지정 된 정규식과 일치 하는 tooa 값을 설정 하는 문자열 매개 변수는 hello 지정 된 쿼리를 포함 하는 요청을 식별 합니다.
URL 쿼리 와일드카드 | 비교 하 여 hello hello 요청 쿼리 문자열에 대 한 값을 지정 합니다.


## <a name="next-steps"></a>다음 단계
* [Azure CDN 개요](cdn-overview.md)
* [규칙 엔진 참조](cdn-rules-engine-reference.md)
* [규칙 엔진 조건식](cdn-rules-engine-reference-conditional-expressions.md)
* [규칙 엔진 기능](cdn-rules-engine-reference-features.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)

