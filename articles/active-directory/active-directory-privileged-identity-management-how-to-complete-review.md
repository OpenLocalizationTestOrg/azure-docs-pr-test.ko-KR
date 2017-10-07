---
title: "aaaHow toocomplete 액세스 검토 | Microsoft Docs"
description: "자세한 내용은 Azure AD Privileged Identity Management에 대 한 액세스 검토를 시작한 후 어떻게 toocomplete 하 고 보기 hello 결과"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>어떻게 toocomplete 액세스에서에서 검토 하 고 Azure AD Privileged Identity Management
[보안 검토가 시작](active-directory-privileged-identity-management-how-to-start-security-review.md)된 후에 권한 있는 역할 관리자가 권한이 있는 액세스를 검토할 수 있습니다. Azure AD Privileged Identity Management (PIM)에서는 자동으로 액세스 tooreview 사용자에 게 확인 전자 메일을 보냅니다. 사용자 전자 메일을 받지 못했음을 보낼 수 있습니다 이러한 hello 지침 [어떻게 tooperform 보안 검토](active-directory-privileged-identity-management-how-to-perform-security-review.md)합니다.

Hello 보안 검토 기간이 끝나면 또는 모든 hello 사용자 자신의 셀프 검토를 마친 후에이 문서 toomanage hello 검토의 hello 단계를 수행 하 고 hello 결과 확인 합니다.

## <a name="manage-security-reviews"></a>보안 검토 관리
1. Toohello 이동 [Azure 포털](https://portal.azure.com/) 및 선택 hello **Azure AD Privileged Identity Management** 동영상이 대시보드에서 응용 프로그램입니다.
2. 선택 hello **검토 액세스** hello 대시보드의 섹션.
3. 원하는 toomanage hello 액세스 검토를 선택 합니다.

Hello 액세스 검토 세부 정보 블레이드에서 해당 검토를 관리 하기 위한 숫자 옵션이 있습니다.

![PIM 액세스 검토 단추-스크린 샷][1]

### <a name="remind"></a>알림
액세스 검토 hello 사용자 자신을 검토할 수 있도록 설치 되 면 경우 hello **문제점이** 단추 알림을 보냅니다. 

### <a name="stop"></a>중지
모든 액세스 검토는 종료 날짜를 갖지만 hello를 사용할 수 있습니다 **중지** 단추 toofinish 일찍 것입니다. 모든 사용자가이 시간까지 검토 된 하지 않은 경우 그렇지 않은 것 수 tooafter hello 검토를 중지 합니다. 검토를 중단한 후에는 다시 시작할 수 없습니다.

### <a name="apply"></a>적용
액세스 검토 완료 되 면 하나 hello 종료 날짜에 도달 하거나 수동으로 중지 hello **적용** 단추 hello 검토의 hello 결과 구현 합니다. 검토 회의 hello 사용자의 액세스가 거부 되었습니다,이 역할 할당을 제거 하는 hello 단계입니다.  

### <a name="export"></a>내보내기
수동으로 hello 보안 검토의 tooapply hello 결과 찾으려는 경우 hello 검토를 내보낼 수 있습니다. hello **내보내기** 단추 CSV 파일을 다운로드 하기 시작 합니다. Hello 결과를 Excel 또는 CSV 파일을 여는 다른 프로그램을 관리할 수 있습니다.

### <a name="delete"></a>삭제
Hello에 관심이 없는 모든 추가로 검토, 삭제 합니다. hello **삭제** 단추 hello PIM 응용 프로그램에서에서 hello 검토를 제거 합니다.

> [!IMPORTANT]
> 하지 삭제 발생 하기 전에 경고가 발생 되 면 검토 toodelete 되도록 해야 합니다. 

## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
