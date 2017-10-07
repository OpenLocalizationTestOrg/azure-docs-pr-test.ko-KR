---
title: "Azure Active Directory Power BI 콘텐츠 팩 aaaHow toouse hello | Microsoft Docs"
description: "Toouse Azure Active Directory Power BI 콘텐츠 팩 hello 하는 방법에 대해 알아봅니다"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>어떻게 toouse hello Azure Active Directory Power BI 콘텐츠 팩

사용자가 Azure Active Directory 기능을 채택하고 사용하는 방법을 이해하는 것은 IT 관리자로서 중요한 일입니다. IT 인프라와 통신 tooincrease 사용 및 tooget AAD 기능을 활용할 가장 hello tooplan이 있습니다. Power BI 콘텐츠 팩 Azure Active Directory 기능 toofurther hello 제공 분석에 데이터 toounderstand hello에 대 한 자신의 Azure Active Directory와의 진행 상황에이 데이터 toogather 다양 한 정보를 사용 하는 방법에 대 한 다양 한 기능 하면 과도 하 게 에 의존 합니다.  Power BI로 Azure Active Directory Api의 hello 통합을 hello 미리 작성 된 콘텐츠 팩을 다운로드 하 고 파악 tooall hello 활동 풍부한 시각화 환경을 제공 하는 Power BI를 사용 하 여 Azure Active Directory 내에서 쉽게 수입니다. 사용자 고유의 대시보드를 만들고 조직 내 사람들과 쉽게 공유할 수 있습니다. 

이 항목에서는 사용자 환경에 포함 시킬 tooinstall 및 사용 방법을 콘텐츠를 hello에 대 한 단계별 지침을 제공 합니다.

## <a name="installation"></a>설치  

**tooinstall hello Power BI 콘텐츠 팩:**

1. 에 로그인 할 [Power BI](https://app.powerbi.com/groups/me/getdata/services) Power BI 계정을 사용 하 여 (이 hello O365 또는 Azure AD 계정에 동일한 계정).

2. Hello hello 왼쪽된 탐색 창의 맨 아래에 선택 **데이터 가져오기**합니다.

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. Hello에 **서비스** 상자 **가져오기**합니다.
   
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  **Azure Active Directory** 검색

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  프롬프트가 나타나면 Azure AD 테넌트 ID를 입력한 후 **다음**을 클릭합니다.

    > [!TIP] 
    > Office 365 / Azure AD 테 넌 트에 대 한 신속 하 게 tooget hello 테 넌 트 Id는 toologin toohello Azure AD 포털, 드릴 다운 toohello 디렉터리 및 hello url에서 hello ID를 복사: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  **로그인**을 클릭합니다. 
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  사용자 이름 및 암호를 입력한 다음 **로그인**을 클릭합니다.
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  Hello 응용 프로그램의 동의 대화 상자에서 클릭 **Accept**합니다.
 
9.  Azure Active Directory 작업 로그 대시보드가 만들어지면 이를 클릭합니다.
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>이 콘텐츠 팩으로 무엇을 할 수 있습니까?

이 콘텐츠 팩으로 수행할 수 있는 이동, 전에 hello의 여기의 빠른 미리 보기가 hello 콘텐츠의 다양 한 보고서 팩입니다. 보고서 데이터 toohello 돌아갑니다 **지난 30 일 동안**합니다.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>이 버전의 Azure Active Directory 로그 콘텐츠 팩에 포함된 보고서

**응용 프로그램 사용 현황 및 추세 보고서**:에 사용 된 hello 앱에 대 한 정보 얻기 조직 및 사용 되는 기능과 가장 hello 및 시기. 최근에 조직의 출시 하는 응용 프로그램 사용 방법에 대 한이 보고서 toogather 정보를 사용 하거나 널리 사용 되는 앱을 확인 수 있습니다. 이 작업을 수행 하 여 hello 앱 사용 하지 않는 경우 표시 되 면 사용을 개선할 수 있습니다.

**위치 및 사용자가 로그인**: 모든 hello 로그인 Azure Id 및 제공 hello hello 사용자 id에 대 한 정보를 사용 하 여 수행에 대 한 정보를 가져옵니다. 이를 통해 개별 로그인에 대해 심층적으로 분석할 수 있으며 다음과 같은 질문에 답변할 수 있습니다.

- 이 사용자는 어디에서 로그인했는가?
- 사용자에 게 로그인 대부분 hello 및 여기서 수행 될 로그인에서? 
- 성공적으로 hello 로그인?  
 
특정 날짜 또는 위치를 클릭하여 세부 정보를 자세히 살펴볼 수 있습니다.

**앱당 고유 사용자**: 지정된 앱을 사용하여 모든 고유 사용자를 봅니다. 여기에는 응용 프로그램에 "*성공적으로*" 로그인한 사용자만 포함됩니다.

**장치 로그인**: hello 유형의 OS의 뷰를 표시 및 포함 하 여 hello 사용자에 대 한 자세한 정보를 통해 조직에서 사용자가 사용 되는 브라우저:

- 사용자 이름
- IP 주소
- 위치 
- 로그인 상태 

이 보고서를 통해 다양 한 장치 프로필 조직 내에서 사용 및 용도에 따라 장치 정책을 결정 하는 hello를 이해할 수 있습니다.

**SSPR 깔때기**: 조직에서 암호 재설정이 어떻게 수행되는지 알 수 있습니다. 살짝 개수 암호 재설정 hello SSPR 도구를 통해 시도한로 가져오고 얼마나 많이 정상적으로 수행 합니다. SSPR 깔때기형 hello를 사용 하 여 hello 암호 재설정 오류 자세히 하 고 특정 오류가 발생 한 이유를 이해 합니다. 이 보고서에 대 한 깊은 이해가 hello 올바른 결정을 내릴 수 있도록 hello SSPR 도구 조직에서 사용 되는 방법을 제공 합니다.

## <a name="customizing-azure-ad-activity-content-pack"></a>Azure AD 활동 콘텐츠 팩 사용자 지정

**시각화 변경**:을 클릭 하 여 보고서 시각화를 변경할 수 있습니다 **보고서 편집** 원하는 hello 시각화를 선택 합니다.
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**필드 추가 필드가 포함**: 필드 toohello 보고서를 추가 하거나 hello visual toowhich tooadd/제거 hello 필드를 선택 하 여 제거할 수 있습니다. Hello 아래 예제에서는 "상태를 로그인" 필드 toohello 테이블 뷰를 추가 하 I. 
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Pin 시각화 tooyour 대시보드**: 대시보드를 사용자 지정할 및 시각화 toohello 보고서를 포함 한 toohello 대시보드에 고정할 수 있습니다. Hello 아래 예제에서는 I "로그인 상태" 라는 새 필터를 추가 하 고 hello 보고서에 포함 합니다. I 또한 hello 시각화 tooa 꺾은선형 차트를 가로 막대형 차트에서 변경 되었으며이 새 시각적 toohello 대시보드에 고정할 수 있습니다.

![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**대시보드를 공유**: 원하는 hello 콘텐츠를 만든 후 있습니다 hello 대시보드 사용자와 공유할 수 hello 조직에 있습니다. Hello 보고서, 공유 되 면 hello 보고서에서 선택한 hello 필드를 볼 수 있습니다 점에 유의 하십시오.
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Power BI 보고서의 매일 새로 고침 예약

Power BI 보고서의 일일 새로 고침 tooschedule 너무 이동**데이터 집합 > 설정 > 새로 고침 예약** 아래 표시 된 것과 같이 설정 합니다.
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>콘텐츠 팩의 toonewer 버전 업데이트

Tooupdate 하려는 경우 콘텐츠 팩 tooget 최신 버전:

- Hello 새 콘텐츠 팩을 다운로드 하 고이 문서에 나열 된 지침에 따라 설정 합니다.

- 설정한, 일단 너무 이동**데이터 소스 > 설정 > 데이터 원본 자격 증명** 아래와 같이 자격 증명을 입력 하 고

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Hello hello 콘텐츠 팩의 새 버전으로 작업 하는 즉시 hello 기본 보고서 및 해당 콘텐츠 팩과 연결 된 데이터 집합을 삭제 하 여 필요한 경우 hello 이전 버전을 제거할 수 있습니다.

## <a name="still-having-issues"></a>아직도 문제가 있으십니까? 

[문제 해결 가이드](active-directory-reporting-troubleshoot-content-pack.md)를 확인하세요. Power BI와 관련된 일반적인 도움말은 이 [도움말 문서](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/)을 확인하세요.
 

## <a name="next-steps"></a>다음 단계

Reporting의 개요를 참조 hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md)합니다.
