---
title: "aaaUnderstand Azure 사용을 자세히 설명 | Microsoft Docs"
description: "자세한 내용은 방법 tooread 하 고 Azure 구독에 대 한 자세한 사용 CSV의 hello 섹션 이해"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Microsoft Azure 세부 사용 요금 조건 이해 
자세한 사용 요금 CSV 파일에 포함 되어 매일 hello 및 측정기 수준 사용 요금이 청구 기간 현재 hello에 대 한 합니다. 

tooget 자세한 사용 파일을 참조 [어떻게 tooget 프로그램 Azure 청구 청구서 및 일일 사용량 데이터](billing-download-azure-invoice-daily-usage-date.md)합니다.
스프레드시트 응용 프로그램에서 열 수 있는 쉼표로 구분된 값(.csv) 파일 형식으로 제공됩니다. 사용할 수 있는 두 가지 버전이 표시되면 버전 2를 다운로드합니다. Hello 최신 파일 형식입니다.

사용 현황 청구 금액은 총 hello **월별** 는 구독에 대해 요금이 청구 합니다. 사용 요금에서는 신용 또는 할인이 고려되지 않습니다.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>세부 사용량 파일에 대한 자세한 내용 및 설명
hello 다음 섹션에서는 hello 중요 한 조건 설명 hello 자세한 사용 파일의 버전 2에에서 표시 된 것입니다.

### <a name="statement"></a>문
hello의 윗부분 hello 자세한 사용 현황 CSV 파일 표시 hello 서비스 hello 월 요금 청구 기간 동안 사용 합니다. hello 다음 표에 hello 용어 및 설명은이 섹션에 나와 있습니다.

| 용어 | 설명 |
| --- | --- |
|청구 기간 |hello 청구 기간의 hello 미터 사용 된 경우 |
|측정기 범주 |Hello hello 사용에 대 한 최상위 서비스를 식별합니다. |
|측정기 하위 범주 |Hello 유형을 hello 속도 영향을 줄 수 있는 Azure 서비스를 정의 합니다. |
|측정기 이름 |Hello hello 미터 사용 되는 측정 단위를 식별 합니다. |
|측정기 영역 |데이터 센터 위치에 따라 가격이 책정 됩니다 하는 특정 서비스에 대 한 hello 데이터 센터의 hello 위치를 식별 |
|SKU |각 Azure 미터에 대 한 hello 고유한 시스템 식별자를 식별합니다. |
|단위 |Hello hello 서비스에 청구 되는 단위를 식별 합니다. GB, 시간, 10,000초 등을 예로 들 수 있습니다. |
|소비된 수량 |hello 양을 hello 미터 hello 청구 기간 동안 사용 |
|표함된 수량 |hello 양을 프로그램 현재 청구 기간에 무료로 포함 된 hello 측정기 |
|초과 수량 |표시 hello 차이 중간 사용 수량 hello 및 포함 된 수량 hello 합니다. 이 수량에 대해 요금이 청구됩니다. Hello 제공 없는 포함 된 수량 제안용 속성을 종 량 제,이 합계 사용 수량 hello와 동일 hello 됩니다. |
|약정 기간 내 |6 개 12 개월 제품과 관련 된 프로그램 약정 금액에서 뺀 hello 미터 요금을 표시 합니다. 측정기 요금은 시간순으로 공제됩니다. |
|통화 |프로그램 현재 청구 기간에 사용 되는 hello 통화 |
|초과분 |6 개 12 개월 제품과 관련 된 프로그램 약정 금액을 초과 하는 hello 미터 요금을 보여 줍니다. |
|약정 요율 |6 개 12 개월 제품과 관련 된 hello 총 약정 금액에 따른 hello 약정 속도를 보여 줍니다. |
|비용 |청구 가능 단위당 청구 하는 hello 속도 |
|값 |Hello 결과를 곱하는 hello 초과 수량 열 단위 hello 속도를 보여 줍니다. Hello 사용 수량을 초과 하지 않는지 hello 포함 된 수량, 하는 경우는 무료가이 열에 있습니다. |

### <a name="daily-usage"></a>일일 사용량

hello hello CSV 파일의 일별 사용 현황 섹션 hello에 대 한 요율 정보에 영향을 주는 사용 정보를 보여 줍니다. hello 다음 표에 hello 용어 및 설명은이 섹션에 나와 있습니다.

| 용어 | 설명 |
| --- | --- |
|사용 날짜 |hello 날짜 hello 미터 사용 된 시기 |
|측정기 범주 |이 사용법을 속한 hello 최상위 서비스 식별 |
|측정기 ID |hello 청구 tooprice 청구 사용량 사용 미터 식별자 |
|측정기 하위 범주 |Hello 속도 영향을 줄 수 있는 hello Azure 서비스 유형을 정의합니다 |
|측정기 이름 |Hello hello 미터 사용 되는 측정 단위를 식별 합니다. |
|측정기 영역 |데이터 센터 위치에 따라 가격이 책정 됩니다 하는 특정 서비스에 대 한 hello 데이터 센터의 hello 위치를 식별 |
|단위 |식별 hello 단위는 hello 미터에 청구 됩니다. GB, 시간, 10,000초 등을 예로 들 수 있습니다. |
|소비된 수량 |해당 날짜에 대해 소비 된 hello 미터의 hello 양 |
|리소스 위치 |Hello 측정기 실행 되 고 있는 hello 데이터 센터를 식별 합니다. |
|사용되는 서비스 |hello 사용한 Azure 플랫폼 서비스 |
|리소스 그룹 |hello 리소스 그룹에서 실행 중인 배포 된 미터는 hello에 있습니다. <br/><br/>자세한 내용은 [Azure Resource Manager 개요](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 참조하세요. |
|인스턴스 ID | hello 식별자 hello 미터입니다. <br/><br/> hello 식별자를 만들 때 hello 미터에 지정한 hello 이름은 포함 되어 있습니다. Hello 리소스의 hello 이름 중 하나 인지 hello 정규화 된 리소스 id입니다. 자세한 내용은 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)를 참조하세요. |
|태그들 | 태그 toohello 측정기를 할당 합니다. 태그 toogroup 청구 레코드를 사용 합니다.<br/><br/>예를 들어 hello 측정기를 사용 하 여 hello 부서별로 태그 toodistribute 비용을 사용할 수 있습니다. 내보내는 태그를 지 원하는 서비스를 가상 컴퓨터, 저장소 및 네트워킹 서비스 hello를 사용 하 여 사용자를 프로 비전 된 [Azure 리소스 관리자 API](https://docs.microsoft.com/rest/api/resources/resources)합니다. 자세한 내용은 [태그를 사용하여 Azure 리소스 구성](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/)을 참조하세요. |
|추가 정보 |서비스 특정 메타데이터입니다. 예를 들어 가상 컴퓨터용 이미지 형식입니다. |
|서비스 정보 1 |구독 tooon 속한 서비스 hello hello 프로젝트 이름 |
|서비스 정보 2 |선택적 서비스 특정 메타데이터를 캡처하는 레거시 필드입니다. |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>자세한 사용 파일의 hello 요금 정확한 지 확인 하려면 어떻게 해야 합니까?
세부 사용량 파일에 더 자세한 내용을 보려는 요금이 있는 경우 [Microsoft Azure 청구서 이해](./billing-understand-your-bill.md)를 참조하세요.

## <a name="external"></a>외부 서비스 요금은 어떤가요?
외부 서비스(또는 Marketplace 주문)는 독립 서비스 공급업체에서 제공하며 별도로 청구됩니다. hello 요금 hello Azure 청구서에 표시 하지 않습니다. toolearn 더 참조 [사용자의 Azure 외부 서비스 요금 이해](billing-understand-your-azure-marketplace-charges.md)합니다.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?)하여 문제를 신속하게 해결하세요.
