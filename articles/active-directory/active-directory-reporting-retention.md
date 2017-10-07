---
title: "aaaAzure Active Directory 보고서 보존 정책 | Microsoft Docs"
description: "Azure Active Directory에서 보고서 데이터 보존 정책"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Azure Active Directory 보고서 보존 정책


이 항목 toohello Azure Active Directory에서 각기 다른 활동이 보고서 hello에 대 한 데이터 보존 hello와 함께에서 가장 일반적인 질문을 답변 제공합니다. 

**Q: 시작 작업 데이터의 hello 컬렉션 어떻게 얻을 수 있습니까?**

**A:**

| Azure AD 버전 | 수집 시작 |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | 구독 등록 시 |
| Azure AD Free | 처음으로 열면 hello hello [Azure Active Directory 블레이드](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) hello를 사용 하 여 또는 [Api를 보고 합니다.](https://aka.ms/aadreports)  |

---
**Q: 언제 활동 데이터 hello Azure 포털에서에서 사용할 수 있는?**

**A:**

- **즉시** -hello Azure 클래식 포털에서에서 보고서를 이미 작업 한 경우
- **2 시간 이내에** -켜지 않은 reporting hello Azure 클래식 포털에서에서 하는 경우

---
**Q: 시작 하는 보안 신호의 hello 컬렉션 어떻게 얻을 수 있습니까?**  

**A:** 보안 신호에 대 한 hello 수집 프로세스가 때 옵트인 toouse hello Identity 보호 센터를 시작 합니다. 


---
**Q: 얼마나 오래 hello 수집 된 데이터 저장 됩니다.**

**A:**

**작업 보고서**    

| 보고서                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| 디렉터리 감사        | 7 일        | 30일             | 30일             |
| 로그인 작업       | 7 일        | 30일             | 30일             |

**보안 신호**

| 보고서         | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| 위험에 노출된 사용자  | 7 일        | 30일             | 90일             |
| 위험한 로그인 | 7 일        | 30일             | 90일             |

---