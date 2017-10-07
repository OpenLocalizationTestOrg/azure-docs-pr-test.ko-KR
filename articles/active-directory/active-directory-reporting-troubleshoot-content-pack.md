---
title: "Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결 | Microsoft Docs"
description: "Hello Azure Active Directory 작업 콘텐츠 팩 및 단계 toofix의 오류 메시지 목록을 제공 하 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결 


Azure Active Directory 미리 보기에 대 한 Power BI 콘텐츠 팩 hello를 작업할 때 된 hello 다음 오류를 실행 하는 있습니다. 

- [새로 고침 실패](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [실패 한 tooupdate 데이터 원본 자격 증명](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [데이터를 가져오는 데 너무 오래 걸립니다.](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
이 항목에서는 hello 가능한 원인에 대 한 정보 및 방법 toofix 이러한 오류입니다.
 
## <a name="refresh-failed"></a>새로 고침 실패 
 
**이 오류가 표시 되는 어떻게**: Power BI 또는 hello 새로 고침 기록에 실패 한 상태에서 전자 메일입니다. 


| 원인 | 어떻게 toofix |
| ---   | ---        |
| 재생 오류 toohello 콘텐츠 팩을 연결 하는 hello 사용자의 hello 자격 증명 다시 설정 되었지만 hello 콘텐츠 팩의 hello의 hello 연결 설정에서 업데이트 되지 않은 경우 오류가 발생할 수 있습니다. | Power BI에서 hello dataset 해당 toohello Azure Active Directory 작업 로그 대시보드 (Azure Active Directory 작업 로그의 경우)를 찾을, 새로 고침 일정을 선택 하 고 Azure AD 자격 증명을 입력 합니다. |
| 새로 고침의 기본 콘텐츠 팩 hello toodata 문제 인해 실패할 수 있습니다. | 지원 티켓을 파일로 저장합니다. 자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>실패 한 tooupdate 데이터 원본 자격 증명 
 
**이 오류가 표시 되는 어떻게**:에서 Power BI에서는 toohello Azure Active Directory 작업 로그 (미리 보기) 콘텐츠 팩을 연결 하는 경우. 

| 원인 | 어떻게 toofix |
| ---   | ---        |
| hello 연결 하는 사용자가 전역 관리자와 보안 판독기가 아니고 보안 관리자 | 보안 판독기 또는 전역 관리자 계정을 사용 하거나 보안 관리 tooaccess hello 콘텐츠 팩. |
| 사용자의 테넌트가 프리미엄 테넌트가 아니거나 적어도 프리미엄 라이선스 파일이 있는 사용자가 없습니다. | 지원 티켓을 파일로 저장합니다. 자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>데이터를 가져오는 데 너무 오래 걸립니다. 
 
**이 오류가 표시 되는 어떻게**: Power BI 콘텐츠 팩을 연결 하 고 나면 hello 데이터 가져오기 프로세스 시작 tooprepare Azure Active Directory 작업 로그에 대 한 대시보드 합니다. Hello 메시지 표시: "*... 데이터 가져오기* "  

| 원인 | 어떻게 toofix |
| ---   | ---        |
| 테 넌 트의 hello 크기에 따라이 단계는 몇 분 too30 분에서 아무 곳 이나 걸릴 수 있습니다. | 기다려 주세요. Hello 메시지 변경 되지 않는 경우 tooshowing 대시보드 1 시간 내에, 지원 티켓을 보관 하십시오. 자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.|

## <a name="next-steps"></a>다음 단계

Azure Active Directory 미리 보기의 경우 Power BI 콘텐츠 팩 tooinstall hello 클릭 [여기](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/)합니다.


