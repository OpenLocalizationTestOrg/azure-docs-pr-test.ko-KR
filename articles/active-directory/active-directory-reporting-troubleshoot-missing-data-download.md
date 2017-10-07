---
title: "문제 해결: Azure Active Directory 작업 로그 다운로드 한 hello에 누락 된 데이터 | Microsoft Docs"
description: "다운로드 한 Azure Active Directory 작업 로그에서 확인 toomissing 데이터를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>내가 다운로드 한 hello Azure Active Directory 작업 로그에서 모든 데이터를 찾을 수 없는


## <a name="symptoms"></a>증상

I (감사 또는 로그인) hello 활동 로그를 다운로드 하 고 hello 시간 선택에 대 한 모든 hello 레코드가 표시 되지 않는 키를 누릅니다. 그 이유는 

 ![보고](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>원인

Hello 눈금 too120K 레코드를 가장 하 여 정렬 제한 되어 hello Azure 포털에서에서 활동 로그를 다운로드 하면 최신입니다. 

## <a name="resolution"></a>해결 방법

활용할 수 있는 [Azure AD Reporting Api](active-directory-reporting-api-getting-started.md) toofetch 특정된 시점에서 tooa 백만 레코드를 합니다. 이 권장 방법은 toorun hello 보고 Api toofetch를 호출 하는 일정에 따라 스크립트를 증분 방식에서 시간 동안 기록 (예:: 매일 또는 매주)입니다.

## <a name="next-steps"></a>다음 단계
Hello 참조 [FAQ를 보고 하는 Azure Active Directory](active-directory-reporting-faq.md)합니다.

