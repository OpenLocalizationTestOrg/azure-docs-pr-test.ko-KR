---
title: "Azure Data Catalog에서 데이터 원본을 aaaRegister | Microsoft Docs"
description: "이 문서는 hello 메타 데이터 필드를 비롯 한 Azure 데이터 카탈로그에서 tooregister 데이터 원본을 등록 하는 동안 추출 하는 방법을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Azure Data Catalog에서 데이터 원본 등록
## <a name="introduction"></a>소개
Azure Data Catalog는 기업 데이터 원본의 등록 시스템 및 검색 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 다시 말해서 데이터 카탈로그는 사람들이 데이터 원본을 검색하고 이해하고 사용하도록 도우면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다. 첫 번째 단계 toomaking 데이터 소스를 hello 데이터 카탈로그를 통해 검색할 수는 tooregister 해당 데이터 원본입니다.

## <a name="register-data-sources"></a>데이터 원본 등록
등록은 hello 과정을 hello 데이터 원본에서 메타 데이터를 추출 하 고 해당 데이터 toohello 데이터 카탈로그 서비스를 복사 합니다. hello 데이터는 유지 여기서 현재 상주 하 고 hello 관리자의 hello 제어 및 정책의 hello 현재 시스템의 상태를 유지 합니다.

데이터 원본 tooregister 다음 hello지 않습니다.
1. Hello Azure Data Catalog 포털 hello 데이터 카탈로그 데이터 원본 등록 도구를 시작 합니다. 
2. 동일한 hello로 회사 또는 학교 계정으로 로그인 toosign toohello 포털에서 사용 하는 Azure Active Directory 자격 증명입니다.
3. 원하는 tooregister hello 데이터 원본을 선택 합니다.

자세한 단계별 세부 정보에 대 한 참조 hello [Azure Data Catalog 시작](data-catalog-get-started.md) 자습서입니다.

Hello 데이터 소스를 등록 한 후 hello 카탈로그의 위치를 추적 하 고 해당 메타 데이터를 인덱싱합니다. 사용자 수 검색, 탐색 및 hello 데이터 원본 검색 및 다음 해당 위치 tooconnect tooit를 사용 하 여 hello 응용 프로그램이 나 선택한 도구를 사용 하 여 합니다.

## <a name="supported-data-sources"></a>지원되는 데이터 원본
현재 지원되는 데이터 원본 목록은 [데이터 카탈로그 DSR](data-catalog-dsr.md)을 참조하세요.

## <a name="structural-metadata"></a>구조적 메타데이터
데이터 소스를 등록할 때 hello 등록 도구 선택 하는 hello 개체의 hello 구조에 대 한 정보를 추출 합니다. 이 정보는 참조 된 tooas 구조적 메타 데이터입니다.

모든 개체에 대 한 구조적 메타 데이터가이 hello 데이터를 검색 하는 사용자가 선택한 hello 클라이언트 도구에서 해당 정보 tooconnect toohello 개체를 사용할 수 있도록 hello 개체의 위치가 포함 됩니다. 다른 구조적 메타데이터는 개체 이름과 유형 및 특성/열 이름과 데이터 유형을 포함합니다.

## <a name="descriptive-metadata"></a>설명이 포함된 메타데이터
또한 toohello 핵심 hello 데이터 원본에서 추출 된 구조적 메타 데이터, hello 데이터 원본 등록 도구 설명이 포함 된 메타 데이터를 추출 합니다. SQL Server Analysis Services 및 SQL Server Reporting Services에 대 한 이러한 서비스에서 노출 하는 hello 설명 속성에서이 메타 데이터를 가져옵니다. SQL Server, ms hello를 사용 하 여 제공 된 값에 대 한\_확장 속성 설명에서 추출 됩니다. Oracle 데이터베이스에 대 한 hello 데이터 원본 등록 도구 추출 hello 주석 열에서 모든 hello\_탭\_주석 보기.

또한 toohello 설명이 포함 된 메타 데이터의 hello 데이터 원본에서 추출 된 hello 데이터 원본 등록 도구를 사용 하 여 설명 메타 데이터를 입력할 수 있습니다. 사용자가 태그를 추가 하 고 등록 되는 hello 개체에 대 한 전문가 식별할 수 있습니다. 이 설명이 포함 된 메타 데이터는 모두 hello 구조적 메타 데이터와 함께 toohello 데이터 카탈로그 서비스를 복사 합니다.

## <a name="include-previews"></a>미리 보기 포함
기본적으로 이해 데이터 원본을 더 자주 쉽게 포함 된 hello 데이터의 샘플을 볼 수 있을 때 데이터 원본 및 복사한 toohello 데이터 카탈로그 서비스 에서만 메타 데이터만 추출 됩니다.

데이터 카탈로그 데이터 소스 hello 등록 도구를 사용 하 여 각 테이블 및 등록 된 보기에 hello 데이터의 스냅숏을 미리 보기를 포함할 수 있습니다. 등록 중 tooinclude 미리 보기를 선택 하면 hello 등록 도구에서 각 테이블 및 뷰의 too20 레코드를 포함 합니다. 이 스냅숏은 다음 복사 hello 구조적 및 설명이 포함 된 메타 데이터와 함께 toohello 카탈로그입니다.

> [!NOTE]
> 다수의 열을 포함하는 넓은 테이블은 미리 보기의 레코드가 20개 미만이 될 수 있습니다.
>
>

## <a name="include-data-profiles"></a>데이터 프로필 포함
포함 하 여 미리 보기 Data Catalog에서 데이터 원본을 검색 하는 사용자에 대 한 중요 한 컨텍스트를 제공와 마찬가지로 데이터 프로필을 포함 하 여 만들 수 쉽게 toounderstand 검색 데이터 원본.

데이터 카탈로그 데이터 소스 hello 등록 도구를 사용 하 여 각 테이블 및 등록 된 보기에 대 한 데이터 프로필을 포함할 수 있습니다. Hello 등록 도구 hello 데이터에 대 한 집계 통계에 포함 되어 각 테이블 및 보기에 등록 하는 동안 데이터 프로필 tooinclude 선택 하면 포함 하 여:

* hello hello 개체에 hello 데이터 크기 및 행 개수입니다.
* hello 데이터와 hello 개체 스키마의 hello 가장 최근의 업데이트에 대 한 hello 날짜입니다.
* hello null 레코드 및 열에 대 한 고유 값 개수입니다.
* 열에 대 한 hello 최소값, 최대값, 평균 및 표준 편차 값입니다.

이러한 통계는 다음 복사 hello 구조적 및 설명이 포함 된 메타 데이터와 함께 toohello 카탈로그입니다.

> [!NOTE]
> 텍스트 및 날짜 열은 해당 데이터 프로필의 평균 또는 표준 편차 통계에 포함되지 않습니다.
>
>

## <a name="update-registrations"></a>등록 업데이트
데이터 원본 등록 하면 데이터 카탈로그에서 검색 가능한 hello 메타 데이터 및 등록 하는 동안 추출 하는 선택적 미리 보기를 사용 하는 경우 있습니다. 데이터 소스 hello toobe hello 카탈로그 (예를 들어 경우 개체의 hello 스키마가 변경 하 고, 원래 제외 테이블에 포함 되어야 할지 또는 hello 미리 보기에 포함 된 tooupdate hello 데이터)에서 업데이트 해야 하는 경우 hello 데이터 원본 등록 도구 다시 실행할 수 있습니다.

이미 등록된 데이터 원본의 재등록은 병합 “upsert” 작업을 수행합니다. 기존 개체는 업데이트되고 새 개체가 생성됩니다. Hello Data Catalog 포털을 통해 사용자가 제공 된 모든 메타 데이터가 유지 됩니다.

## <a name="summary"></a>요약
데이터 원본 toohello 카탈로그 서비스에서 구조적 및 설명이 포함 된 메타 데이터를 복사 하기 때문에 데이터 카탈로그에 hello 데이터 원본 등록 hello 데이터 보다 쉽게 toodiscover 만들고 이해 합니다. Hello 데이터 소스를 등록 한 후 주석을 달 수, 관리 및 hello Data Catalog 포털을 사용 하 여 검색 합니다.

## <a name="next-steps"></a>다음 단계
데이터 원본 등록에 대 한 자세한 내용은 참조 hello [Azure Data Catalog 시작](data-catalog-get-started.md) 자습서입니다.
