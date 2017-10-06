---
title: "응용 프로그램 프록시 응용 프로그램을 만드는 aaaProblem | Microsoft Docs"
description: "Tootroubleshoot은 hello Azure AD 관리 포털에서 응용 프로그램 프록시 응용 프로그램을 만드는 발급 하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>응용 프로그램 프록시 응용 프로그램을 만들 때 문제 발생 

다음은 hello 일반적인 문제 중 일부 사용자 면 새 응용 프로그램 프록시 응용 프로그램을 만들 때입니다.

## <a name="recommended-documents"></a>권장되는 문서 

hello 관리자 포털을 통해 응용 프로그램 프록시 응용 프로그램 만들기에 대 한 더 toolearn 참조 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)합니다.

해당 문서의 hello 단계는 다음과 같습니다. 표시 되 게 hello 응용 프로그램을 만드는 동안 오류가 발생 하는 경우에 정보에 대 한 hello 오류 세부 정보 및 방법을 toofix hello 응용 프로그램에 대 한 제안을 참조 하십시오. 대부분의 오류 메시지에는 제안 수정이 포함되어 있습니다. 

## <a name="specific-things-toocheck"></a>특정 작업 toocheck

tooavoid 일반적인 오류를 확인 합니다.

-   관리자 권한 toocreate 응용 프로그램 프록시 응용 프로그램 사용

-   hello 내부 URL은 고유

-   hello 외부 URL이 고유

-   hello http 또는 https를 사용한 Url 시작 하 고 끝나야는 "/"

-   도메인 이름 및 IP 주소가 아니라 hello URL 이어야 합니다.

hello 응용 프로그램을 만들 때 hello 오른쪽 위 모서리에 hello 오류 메시지가 표시 되어야 합니다. Hello 알림 아이콘 toosee hello 오류 메시지를 선택할 수 있습니다.

   ![알림 프롬프트](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>다음 단계
[Hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)
