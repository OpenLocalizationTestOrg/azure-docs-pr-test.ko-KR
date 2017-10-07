---
title: "Azure 시간 시계열 Insights의 aaaData 액세스 정책 | Microsoft Docs"
description: "이 자습서에서는 시간 시계열 Insights의 데이터 액세스 정책을 toomanage를 설명"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Azure 포털을 사용 하 여 권한 부여 데이터 액세스 tooa 시간 계열 Insights 환경

Time Series Insights 환경에는 다음과 같은 두 가지 독립적인 액세스 정책이 있습니다.

* 관리 액세스 정책
* 데이터 액세스 정책

두 정책 모두 Azure Active Directory 주체(사용자 및 앱)에게 특정 환경에 대한 다양한 권한을 부여합니다. hello 이름 (사용자 및 응용 프로그램)의 구성원 이어야 toohello active hello 환경을 포함 하는 hello 구독과 연결 된 디렉터리 (또는 "Azure 테 넌 트").

와 같은 권한을 부여 사용 권한 관련된 toohello 구성 hello 환경의 관리 액세스 정책
*   이벤트 소스 hello 환경의 생성 및 삭제 참조 데이터 집합 및
*   Hello 데이터 액세스 정책 관리 합니다.

데이터 액세스 정책을 tooissue 데이터 쿼리, 사용 권한을 부여 hello 환경에서 참조 데이터를 조작 하 고 hello 환경에 연결 된 큐브 뷰 및 저장 된 쿼리를 공유 합니다.

hello 두 가지 정책 명확히 구분 hello 환경의 액세스 toohello 관리 및 hello 환경 내 toohello 데이터 액세스를 허용합니다. 예를 들어, hello 소유자/hello 환경의 작성자 hello 데이터 액세스에서 제거 되는 가능한 toosetup 환경입니다. 사용자 및 서비스 허용 되는 hello 환경에서 tooread 데이터 뿐 아니라 부여할 수 있습니다 hello 환경의 액세스 toohello 구성이 없습니다.

## <a name="grant-data-access"></a>데이터 액세스 권한 부여
hello 다음 단계 표시 toogrant 데이터는 사용자 계정에 대 한 액세스 하는 방법을:

1.  Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2.  Hello hello Azure 포털의 왼쪽에 hello 메뉴에서 "모든 리소스"를 클릭 합니다.
3.  Time Series Insights 환경을 선택합니다.

  ![Hello 시간 계열 Insights 원본 관리-환경](media/data-access/getstarted-grant-data-access1.png)

4.  “데이터 평면 액세스”를 선택하고 “추가”를 클릭합니다.

  ![Hello 시간 계열 Insights 원본 관리-추가](media/data-access/getstarted-grant-data-access2.png)

5.  “사용자 선택”을 클릭합니다.
6.  검색 하 고 hello 전자 메일을 통해 사용자를 선택 합니다.
7.  “사용자 선택” 블레이드에서 “선택”을 클릭합니다.

  ![Hello 시간 계열 Insights 원본 관리-사용자 선택](media/data-access/getstarted-grant-data-access3.png)

8.  “역할 선택”을 클릭합니다.
9.  큐브 뷰 및 저장 된 쿼리를 다른 사용자와 공유할 hello 환경의 tooallow 사용자 toochange 참조 데이터를 원할 경우 "기여자"를 선택 합니다. 그렇지 않으면 hello 환경에서 "Reader" tooallow 사용자 쿼리 데이터를 선택 하 고 hello 환경에서 개인 (공유) 쿼리를 저장 합니다.
10. Hello "선택 역할" 블레이드에서 "확인"을 클릭 합니다.

  ![Hello 시간 계열 Insights 원본 관리-역할 선택](media/data-access/getstarted-grant-data-access4.png)

11. Hello "사용자 역할 선택" 블레이드에서 "확인"을 클릭 합니다.
12. 다음과 같은 결과가 표시됩니다.

  ![Hello 시간 계열 Insights 원본 관리-결과](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>다음 단계

* [이벤트 원본 만들기](time-series-insights-add-event-source.md)
* [이벤트를 보내는](time-series-insights-send-events.md) toohello 이벤트 소스
* [Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기
