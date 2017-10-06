---
title: "Azure Analysis Services에서 aaaAuthentication 및 사용자 권한을 | Microsoft Docs"
description: "Azure Analysis Services의 인증 및 사용자 권한에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>인증 및 사용자 권한
Azure Analysis Services는 ID 관리 및 사용자 인증에 Azure AD(Azure Active Directory)를 사용합니다. 만드는 모든 사용자, 관리 또는 tooan Azure Analysis Services에 연결 서버 있어야 올바른 사용자 id는 [Azure AD 테 넌 트](../active-directory/active-directory-administer.md) hello에 동일한 구독 합니다.

Azure Analysis Services는 [Azure AD B2B 공동 작업](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)을 지원합니다. B2B를 사용하여 Azure AD 디렉터리의 게스트 사용자로 조직 외부의 사용자를 초대할 수 있습니다. 게스트는 다른 Azure AD 테넌트 디렉터리나 모든 유효한 메일 주소에서 가져올 수 있습니다. 한 번 초대 및 hello 사용자가 수락 hello 초대의 전자 메일을 통해 azure에서 hello 사용자 id toohello 테 넌 트 디렉터리에 추가 됩니다. Id 만으로 추가할 수 있습니다 toosecurity 그룹 또는 서버 관리자 또는 데이터베이스 역할의 구성원으로 합니다.

![Azure Analysis Services 인증 아키텍처](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>인증
모든 클라이언트 응용 프로그램 및 도구 hello Analysis Services 중 하나 이상을 사용 하 여 [클라이언트 라이브러리](analysis-services-data-providers.md) (AMO, MSOLAP ADOMD) tooconnect tooa 서버입니다. 

세 클라이언트 라이브러리는 Azure AD 대화형 흐름과 비대화형 인증 방법을 모두 지원합니다. 두 가지 비 대화형 방법을 hello, Active Directory 암호 및 Active Directory 통합 인증 방법을 AMOMD 및 MSOLAP를 활용 하는 응용 프로그램에서 사용할 수 있습니다. 이러한 두 가지 방법을 사용할 경우 팝업 대화 상자가 절대 표시되지 않습니다.

Hello 최신 버전의 hello 라이브러리 업데이트를 설치 하는 SSDT 및 SSMS와 같은 도구 및 클라이언트 응용 프로그램 같은 Excel 및 Power BI Desktop toohello 최신 릴리스 합니다. Power BI Desktop, SSMS 및 SSDT는 매월 업데이트됩니다. Excel은 [Office 365로 업데이트](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516)됩니다. Office 365 업데이트를 보다 긴 및 hello 지연 된 채널을 사용 하는 일부 조직에서는, toothree 월을 의미 업데이트가 지연 됩니다.

 Hello 클라이언트 응용 프로그램 또는 도구를 사용에 따라 인증 및 로그인 방법 hello 형식은 다 수 있습니다. 각 응용 프로그램 Azure Analysis Services와 같은 toocloud 서비스를 연결 하기 위한 다양 한 기능을 지원할 수 있습니다.


### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Azure Analysis Services 서버는 Windows 인증, Active Directory 암호 인증 및 Active Directory 유니버설 인증을 사용하여 [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 이상에서 연결하는 것을 지원합니다. 일반적으로 다음과 같은 이유로 Active Directory 유니버설 인증을 사용하는 것이 좋습니다.

*  대화형 및 비대화형 인증 방법을 지원합니다.

*  Hello Azure AS 테 넌 트에 초대 Azure B2B 게스트 사용자를 지원 합니다. Tooa 서버에 연결할 때 toohello 서버에 연결 하는 경우 게스트 사용자에 게 Active Directory 유니버설 인증을 선택 해야 합니다.

*  MFA(Multi-Factor Authentication)를 지원합니다. Azure MFA를 사용 하면 보호 액세스 toodata 및 확인 옵션의 범위를 응용 프로그램: 전화 통화, 문자 메시지, 스마트 카드와 해당 pin 또는 모바일 앱 알림을 합니다. Azure AD를 사용하는 대화형 MFA는 유효성 검사를 위한 팝업 대화 상자를 표시할 수 있습니다.

### <a name="sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)
SSDT는 tooAzure Analysis Services MFA 지 원하는 Active Directory 유니버설 인증을 사용 하 여 연결 합니다. 사용자가 조직 ID (전자 메일)를 사용 하 여 hello 첫 번째 배포에서 tooAzure에서 증명된 toosign가 있습니다. 사용자가 tooAzure hello 서버에 배포 하는 서버 관리자 권한이 있는 계정으로 로그인 해야 합니다. 처음으로 tooAzure hello에 서명, 토큰을 지정 됩니다. SSDT은 hello 토큰 메모리에 대 한 이후 다시 연결을 캐시합니다.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop tooAzure Analysis Services MFA 지 원하는 Active Directory 유니버설 인증을 사용 하 여 연결 합니다. 사용자가 조직 ID (전자 메일)를 사용 하 여 hello 첫 번째 연결에서 tooAzure에서 증명된 toosign가 있습니다. 사용자가 tooAzure 서버 관리자 또는 데이터베이스 역할에 포함 되어 있는 계정으로 로그인 해야 합니다.

### <a name="excel"></a>Excel
Excel 사용자는 Windows 계정, 조직 ID (전자 메일 주소) 또는 외부 전자 메일 주소를 사용 하 여 tooa 서버를 연결할 수 있습니다. 게스트 사용자로 Azure AD hello에서 외부 전자 메일 id가 있어야 합니다.

## <a name="user-permissions"></a>사용자 권한

**서버 관리자** 특정 tooan Azure Analysis Services 서버 인스턴스가 됩니다. 데이터베이스를 추가 하 고 사용자 역할 관리 등의 tooperform 작업 Azure 포털, SSMS 및 SSDT와 같은 도구와 연결 합니다. 기본적으로 만드는 hello 서버 hello 사용자를 Analysis Services 서버 관리자로 자동 추가 됩니다. 다른 관리자는 Azure Portal이나 SSMS를 사용하여 추가할 수 있습니다. 서버 관리자는 hello에 hello Azure AD 테 넌 트의 계정이 있어야 동일한 구독 합니다. toolearn 더 참조 [서버 관리자 관리](analysis-services-server-admins.md)합니다. 


**데이터베이스 사용자** Excel 또는 Power BI와 같은 클라이언트 응용 프로그램을 사용 하 여 toomodel 데이터베이스를 연결 합니다. 사용자가 toodatabase 역할을 추가 해야 합니다. 데이터베이스 역할은 데이터베이스에 대해 관리자, 처리 또는 읽기 권한을 정의합니다. 관리자 권한 가진 역할의 toounderstand 데이터베이스 사용자가 서버 관리자와 다른 유용 합니다. 그러나 기본적으로 서버 관리자는 데이터베이스 관리자이기도 합니다. toolearn 더 참조 [데이터베이스 역할 및 사용자 관리](analysis-services-database-users.md)합니다.

**Azure 리소스 소유자**. 리소스 소유자는 Azure 구독에 대한 리소스를 관리합니다. 리소스 소유자 수 참가자 역할 또는 Azure AD 사용자 identities tooOwner 구독 내에서 사용 하 여 추가 **액세스 제어** Azure 포털에서 또는 Azure 리소스 관리자 템플릿을 사용 합니다. 

![Azure Portal의 액세스 제어](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

이 수준에서 역할에는 toousers 또는 필요한 hello 포털 또는 Azure 리소스 관리자 템플릿을 사용 하 여 완료할 수 있는 tooperform 작업 계정에 적용 됩니다. toolearn 더 참조 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)합니다. 


## <a name="database-roles"></a>데이터베이스 역할

 테이블 형식 모델에 대해 정의된 역할이 데이터베이스 역할입니다. 즉, hello 역할에는 Azure AD 사용자가 구성 된 멤버 포함 및 model 데이터베이스에 해당 멤버 hello 동작을 정의 하는 특정 권한을 있는 보안 그룹에서 수행할 수 있습니다. 데이터베이스 역할 hello 데이터베이스에 별도 개체로 생성 되 고 해당 역할이 생성만 toohello 데이터베이스에 적용 됩니다.   
  
 기본적으로 새 테이블 형식 모델 프로젝트를 만들 때 hello 모델 프로젝트에 없는 모든 역할입니다. SSDT의 hello 역할 관리자 대화 상자를 사용 하 여 역할을 정의할 수 있습니다. 모델 프로젝트 디자인 하는 동안 역할 정의 되 면 이들은 적용된만 toohello 모델 작업 영역 데이터베이스입니다. Hello 모델을 배포할 때 hello 동일한 역할은 배포 적용된 toohello 모델입니다. 모델을 배포한 후 서버 및 데이터베이스 관리자는 SSMS를 사용하여 역할 및 멤버를 관리할 수 있습니다. toolearn 더 참조 [데이터베이스 역할 및 사용자 관리](analysis-services-database-users.md)합니다.
  


## <a name="next-steps"></a>다음 단계

[Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](../active-directory/active-directory-manage-groups.md)   
[데이터베이스 역할 및 사용자 관리](analysis-services-database-users.md)  
[서버 관리자 관리](analysis-services-server-admins.md)  
[역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)  