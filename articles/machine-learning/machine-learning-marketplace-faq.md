---
title: "aaa(deprecated) FAQ-게시 하 고 기계 학습 응용 프로그램을 사용 하 여 Azure 마켓플레이스에서 | Microsoft Docs"
description: "(사용 되지 않음) Hello Azure Marketplace에서에서 기계 학습 응용 프로그램을 게시 하는 방법에 대 한 질문과 대답"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(사용 되지 않음) 게시 하 고 기계 학습 응용 프로그램을 사용 하 여 hello Azure Marketplace의에서: FAQ

> [!NOTE]
> DataMarket 및 Data Services는 종료되며 기존 구독은 2017년 3월 31일부터 종료 및 취소됩니다. 결과적으로,이 문서는 사용되지 않습니다. 
> 
> 기계 학습 실험 toohello를 게시할 수 있습니다 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/) hello hello 데이터 과학 커뮤니티의 혜택을 받을 수 있습니다. 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)합니다.


## <a name="questions-about-consuming-from-marketplace"></a>마켓플레이스에서의 사용 관련 질문
**1. 왜 hello 웹 서비스에 대 한 입력을 입력 해도 다음과 같은 오류 메시지가 hello:**

**hello 요청 시간 초과 백 엔드 또는 백 엔드 오류가 발생 했습니다. hello 팀 hello 문제를 조사 합니다. 하는 hello 불편을 드려 죄송 합니다. (500)**

사용자 입력된 매개 변수가 toohello hello 특정 웹 서비스에 대 한 필요한 형식을 따르지 않을 합니다. 입력된 매개 변수 및이 웹 서비스의 hello 제한 사항에 대 한 toohello 해당 설명서 링크 toofind hello 올바른 형식을 참조 하십시오.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. "이 데이터이 집합 탐색" 페이지 hello 및 tooaccess hello 결과 사용 하 고 어떻게 해야 하는 자격 증명 다른 브라우저 창에 붙여에 나타나는 hello 웹 서비스에 대 한 API hello 링크를 복사 하는 경우 해당 확인할 수 있나요?**

마켓플레이스 계정 hello 암호와 hello 사용자 이름 및 hello 기본 계정 키로 사용 해야 합니다. hello에 hello 기본 계정 키를 찾을 수 **이 데이터 집합 탐색** hello hello 웹 서비스 설명 페이지 (hello 클릭 **표시** 단추). hello 결과 hello 브라우저에 표시 될 수 있습니다 또는 너무 사용할 수 사용 중인 브라우저에 따라 다운로드 합니다.

**3. 왜 hello 입력 hello 웹 서비스에 대 한 hello "이 데이터이 집합 탐색" 페이지에서 입력 해도 다음과 같은 오류 메시지가 hello:** 

**요청을 처리하는 동안 예기치 않은 오류가 발생했습니다. 나중에 다시 시도하세요.**

웹 서비스의 하나 이상의 입력된 매개 변수 초과 했을 수 hello 길이 제한 hello 마켓플레이스에서 hello 웹 서비스를 이용할 때 **이 데이터 집합 탐색** 페이지. HTTP POST 메서드를 사용 하 여 더 이상 입력된 길이와 hello 서비스를 호출할 수 있습니다. 예제를 보려면 [예제 기계 학습 및 게시 된 tooMarketplace에서 R을 사용 하 여 솔루션](machine-learning-r-csharp-web-service-examples.md)합니다.

**4. 이유 보이지 않는 hello Azure 클래식 포털에에서 hello "API 탐색기" 탭 int hello 저장소에에서 아무 것도?** 

Azure 클래식 포털 Marketplace hello로 알려진된 문제입니다. hello 팀이이 문제 tooresolve 노력가 있습니다. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>마켓플레이스에 있는 Azure 기계 학습에서의 게시에 대한 질문
**1. 내 웹 서비스에 대해 내 로고 또는 이미지 트랜잭션 수가 새로 고쳐지지 않는 이유는 무엇인가요?** 

Hello 게시 포털에 로고와 이미지는 캐시 되 고 새 로고 hello 나 hello 포털에서 이미지 tooupdate too10 일이 걸릴 수도 있습니다.

**2. 오류 메시지를 표시 하는 시장에 내 웹 서비스의 hello "정보" 탭을 이유는 무엇입니까?**

서비스 세부 정보에 대 한 기계 학습 tooAzure 연결할 때 알려진된 마켓플레이스 문제가 있습니다. hello 팀이이 문제 tooresolve 노력가 있습니다.

**3. 이유 hello hello Azure 기계 학습 웹 서비스에서 R 샘플 코드가 작동 하지 않습니다 시장에서 소비 hello 웹 서비스에 대 한?**

hello 마켓플레이스를 통해 tooconnecting toothese 웹 서비스에 비해 tooAzure 기계 학습 웹 서비스를 직접 연결 hello 인증 시스템 서로 다릅니다. Marketplace에서 hello 서비스는 OData 서비스 및 GET 또는 POST 메서드를 호출할 수 있습니다. 

**4. 내 제품 중 일부에 대해 제대로 업데이트 하지 않는 제공 hello 지원 링크 내 웹 서비스의 이유는?**

hello 지원 링크 당 게시자, 제품 단위가 아니라 전체 적용 됩니다. 

**5. 마켓플레이스에서 일괄 처리 입력 모드를 통해 웹 서비스를 게시하는 방법은 무엇인가요?**

hello 일괄 처리 입력된 모드 현재 Marketplace 웹 서비스에서 지원 되지 않습니다.

**6. 가 문의 해야 합니까 tooget 도움말 데이터 게시자가 관련 질문이 있는 경우 또는 게시 하는 동안 문제가 있습니까?**

hello Azure 마켓플레이스 팀에 문의 하거나 < mailto:datamarketbd@microsoft.com > 자세한 정보에 대 한 합니다.

