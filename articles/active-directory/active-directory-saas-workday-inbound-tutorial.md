---
title: "자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Active Directory와 Azure Active Directory에 대 한 id 데이터의 원본으로 Workday 합니다."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성
hello이이 자습서의 일부 특성 tooWorkday의 선택적 쓰기 저장으로 작업일에서 tooperform tooimport 사용자는 Active Directory 및 Azure Active Directory에 필요한 단계를 hello tooshow가 합니다. 



## <a name="overview"></a>개요

hello [서비스 프로 비전 하는 Azure Active Directory 사용자](active-directory-saas-app-provisioning.md) hello와 통합 되어 [Workday 인적 자원 API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) 의 순서로 tooprovision 사용자 계정입니다. Azure AD 사용자 프로 비전 워크플로가 다음이 연결 tooenable hello를 사용 합니다.

* **사용자가 tooActive 디렉터리를 프로 비전** -하나 이상의 Active Directory 포리스트를 선택한 유형의 작업일에서 사용자가 동기화 합니다. 

* **클라우드 전용 사용자 tooAzure Active Directory 프로비저닝** -하이브리드 사용자에 게는 Active Directory 및 Azure Active Directory에 존재 hello 후자 사용 하 여 프로 비전 할 수 [AAD Connect](connect/active-directory-aadconnect.md)합니다. 그러나 클라우드 전용 사용자가 서비스를 프로 비전 하는 Azure AD 사용자 hello tooAzure Active Directory를 사용 하 여 Workday에서 직접 프로 비전 할 수 있습니다.

* **전자 메일의 쓰기 저장 주소 tooWorkday** -서비스를 프로 비전 하는 hello Azure AD 사용자 Azure AD 사용자 특성 백 tooWorkday, 예: hello 전자 메일 주소를 선택 합니다. 쓸 수 있습니다.

### <a name="scenarios-covered"></a>포함되는 시나리오

hello Workday 사용자 서비스를 프로 비전 하는 hello Azure AD 사용자가 지원 되는 워크플로 프로 비전 hello 다음 인적 자원 및 id 수명 주기 관리 시나리오의 자동화를 지원 합니다.

* **새 직원을 채용** -새 직원 tooWorkday를 추가 하는 경우 사용자 계정을 자동으로 만들어집니다 Active Directory, Azure Active Directory와 선택적으로 Office 365 및 [Azure AD에서 지 원하는 다른 SaaS 응용 프로그램 ](active-directory-saas-app-provisioning.md), hello 전자 메일 주소 tooWorkday 뒷면 쓰기입니다.

* **직원 특성 및 프로필 업데이트** - Workday에서 이름, 직함, 관리자 등의 직원 레코드가 업데이트되면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 업데이트됩니다.

* **직원 퇴사** - Workday에서 직원이 퇴사하면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 비활성화됩니다.

* **직원 채용 다시** -직원이 Workday에서 rehired 되 면 이전 계정으로 자동으로 다시 활성화할 수 있습니다 (기본 설정)에 따라 다시 프로 비전된 tooActive 디렉터리, Azure Active Directory 및 필요에 따라 Office 365 및 또는[Azure AD에서 지 원하는 다른 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)합니다.


## <a name="planning-your-solution"></a>솔루션 계획

Workday의 통합을 시작 하기 전에 아래과 읽기 hello 방법에 대 한 지침을 따르면 hello 필수 구성 요소를 확인, 현재 Active Directory 아키텍처와 사용자에 게 요구를 프로 비전 hello 활성 Azure에서 제공 하는 솔루션이 toomatch 디렉터리입니다.

### <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 전역 관리자 액세스 권한이 있는 유효한 Azure AD Premium P1 구독
* 테스트 및 통합을 위한 Workday 구현 테넌트
* Workday toocreate 시스템 통합 사용자에에서 대 한 관리자 권한이 및 테스트 목적으로 확인 tootest 직원 데이터를 변경 합니다
* 사용자 프로 비전 tooActive 디렉터리, 2012 또는 큰 Windows 서비스를 실행 하는 도메인에 가입 된 서버는 필요한 toohost hello [온-프레미스 동기화 에이전트](https://go.microsoft.com/fwlink/?linkid=847801)
* Active Directory와 Azure AD 간의 동기화를 위한 [Azure AD Connect](connect/active-directory-aadconnect.md)

> [!NOTE]
> 유럽의 Azure AD 테 넌 트 있으면 hello를 참조 하십시오 [알려진 문제](#known-issues) 아래 섹션.


### <a name="solution-architecture"></a>솔루션 아키텍처

Azure AD에서는 다양 한 프로 비전 및 id 수명 주기 관리 Workday tooActive 디렉터리를 Azure AD에서 SaaS 응용 프로그램에서에서와 같거나 이보다 뒤 해결 커넥터 toohelp 프로 비전을 제공 합니다. 사용 되는 기능 하 고 hello 솔루션을 설정 하는 방법을 조직 환경 및 요구 사항에 따라 달라 집니다. 첫 번째 단계로, hello 다음의 수가 존재 하 고 조직에 배포 된의 재고를 수행 합니다.

* Active Directory 포리스트를 몇 개나 사용하고 있나요?
* Active Directory 도메인을 몇 개나 사용하고 있나요?
* Active Directory OU(조직 구성 단위)를 몇 개나 사용하고 있나요?
* Azure Active Directory 테넌트를 몇 개나 사용하고 있나요?
* 사용자를 프로 비전 toobe tooboth Active Directory와 Azure Active Directory (예: "하이브리드" 사용자)에 게 있나요?
* Active Directory 사용자를 프로 비전 toobe tooAzure 하지만 Active Directory 없습니다 (예: "클라우드 전용" 사용자의 경우) 해야 하는 사용자가 있습니까?
* 사용자 전자 메일 주소를 다시 tooWorkday 기록 toobe 필요 합니까?

대답 toothese 질문을 만든 후 다음 hello 설명서 아래에서 배포를 프로 비전 하면 업무를 계획할 수 있습니다.

#### <a name="using-provisioning-connector-apps"></a>프로비전 커넥터 앱 사용

Azure Active Directory는 Workday용으로 사전 통합된 프로비전 커넥터와 수많은 기타 SaaS 응용 프로그램을 지원합니다. 

하나의 프로비저닝 커넥터 단일 원본 시스템의 hello API와 상호 작용 하 고 프로 비전 데이터 tooa 단일 대상 시스템을 지원 합니다. 대부분의 프로 비전 커넥터를 지 원하는 Azure AD는 단일 소스 및 대상 시스템 (예: Azure AD tooServiceNow) 수 있으며 설치 hello 앱을 추가 하기만 하면 문제의 hello Azure AD 앱 갤러리 (예: ServiceNow)에서 합니다. 

Azure AD의 프로비전 커넥터 인스턴스와 앱 인스턴스는 일대일 관계입니다.

| 원본 시스템 | 대상 시스템 |
| ---------- | ---------- | 
| Azure AD 테넌트 | SaaS 응용 프로그램 |


그러나 Workday 및 Active Directory를 사용할 때는 간주 여러 소스 및 대상 시스템 toobe 가지.

| 원본 시스템 | 대상 시스템 | 참고 사항 |
| ---------- | ---------- | ---------- |
| Workday | Active Directory 포리스트 | 각 포리스트는 고유한 대상 시스템으로 처리됨 |
| Workday | Azure AD 테넌트 | 클라우드 전용 사용자에 필요한 경우 |
| Active Directory 포리스트 | Azure AD 테넌트 | 이 흐름은 현재 AAD Connect에서 처리 |
| Azure AD 테넌트 | Workday | 이메일 주소의 쓰기 저장 |

toofacilitate 이러한 여러 개의 워크플로 toomultiple 소스 및 대상 시스템에 Azure AD hello Azure AD 앱 갤러리에서 추가할 수 있는 여러 프로비저닝 커넥터 앱을 제공 합니다.

![AAD 앱 갤러리](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **디렉터리 프로비저닝이 workday tooActive** -이 앱 Workday tooa 단일 Active Directory 포리스트의 사용자 계정 프로비저닝을 용이 하 게 합니다. 여러 포리스트에 있는 경우에 tooprovision 필요한 각 Active Directory 포리스트에 대 한 hello Azure AD 앱 갤러리에서이 응용 프로그램의 인스턴스 하나를 추가할 수 있습니다.

* **Workday tooAzure AD 프로 비전** -동안 AAD Connect는 hello 도구 사용된 toosynchronize Active Directory 사용자 tooAzure Active Directory 되어야 하는이 앱에 사용 되는 toofacilitate 될 수 있습니다 Workday tooa 단일에서 클라우드 전용 사용자 프로 비전 Azure Active Directory 테 넌 트입니다.

* **Workday 쓰기 저장** -이 앱에서 Azure Active Directory tooWorkday 사용자의 전자 메일 주소의 쓰기 저장을 용이 하 게 합니다.

> [!TIP]
> hello 일반 "Workday" 응용 프로그램은 Azure Active Directory와 Workday에서 single sign-on을 설정 하기 위한 사용 됩니다. 

어떻게 tooset 및 이러한 특별 한 구성 섹션에서는이 자습서의 나머지 hello의 hello 주제는 커넥터 응용 프로그램을 프로 비전 합니다. 테 넌 트 환경에서 되 tooconfigure, tooprovision 개수 Active Directory 포리스트 및 Azure AD 필요는 시스템에 따라 달라 집니다 선택 하는 앱입니다.

![개요](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Workday에서 시스템 통합 사용자 구성
모든 hello Workday 프로비저닝 커넥터의 일반적인 요구 사항은 Workday 시스템 통합 계정 tooconnect toohello Workday 인적 자원 API에 대 한 자격 증명이 필요한입니다. 이 섹션에서는 Workday의 toocreate 시스템 통합을 고려 하는 방법을 설명 합니다.

> [!NOTE]
> 가능한 toobypass이이 절차 이며 대신 hello 시스템 통합 계정으로 Workday 전역 관리자 계정을 사용 합니다. 이 방법이 데모에서는 제대로 작동할 수 있지만 프로덕션 배포에는 권장하지 않습니다.

### <a name="create-an-integration-system-user"></a>통합 시스템 사용자 만들기

**통합 시스템 사용자 toocreate:**

1. Administrator 계정을 사용하여 Workday 테넌트에 로그인합니다. Hello에 **Workday Workbench**, 입력 hello 검색 상자에 사용자를 만들고 클릭 **통합 시스템 사용자 만들기**합니다. 
   
    ![사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "사용자 만들기")
2. 전체 hello **통합 시스템 사용자 만들기** 새 통합 시스템 사용자에 대 한 사용자 이름 및 암호를 제공 하 여 작업 합니다.  
 * Hello 둡니다 **다음 로그인 시 새 암호 필요** 옵션을 선택 하지 않는 경우이 사용자에 프로그래밍 방식으로 로그인 때문에 합니다. 
 * Hello 둡니다 **세션 제한 시간 (분)** 0의 기본 값을 갖는 것을 방지할 hello 사용자 세션이 중간 초과 합니다. 
   
    ![통합 시스템 사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "통합 시스템 사용자 만들기")

### <a name="create-a-security-group"></a>보안 그룹 만들기
제한 없는 통합 시스템 보안 그룹 toocreate 필요 하 고이 정보를 사용자 tooit hello를 할당 합니다.

**toocreate 보안 그룹:**

1. 입력 hello 검색 상자에 보안 그룹을 만들고 클릭 **보안 그룹 만들기**합니다. 
   
    ![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "보안 그룹 만들기")
2. 전체 hello **보안 그룹 만들기** 작업 합니다.  
3. 통합 시스템 보안 그룹 선택-hello에서 제약 없이 **종류의 테 넌 트 보안 그룹** 드롭다운입니다.
4. 추가 될 멤버가 명시적으로 보안 그룹 toowhich를 만듭니다. 
   
    ![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "보안 그룹 만들기")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Hello 통합 시스템 사용자 toohello 보안 그룹에 할당

**tooassign hello 통합 시스템 사용자:**

1. 보안 그룹 편집 hello 검색 상자에 입력 한 다음 클릭 **보안 그룹 편집**합니다. 
   
    ![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "보안 그룹 편집")
2. 를 검색 하 고 이름으로 hello 새 통합 보안 그룹을 선택 합니다. 
   
    ![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "보안 그룹 편집")
3. Hello 새 통합 시스템 사용자 toohello 새 보안 그룹을 추가 합니다. 
   
    ![시스템 보안 그룹](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "시스템 보안 그룹")  

### <a name="configure-security-group-options"></a>보안 그룹 옵션 구성
이 단계에서는 있습니다 toohello 새 보안 그룹에 권한을 부여 **가져오기** 및 **배치** hello 다음 도메인 보안 정책으로 보호 되는 hello 개체에 대 한 작업:

* 외부 계정 프로비저닝
* 작업자 데이터: 공용 작업자 보고서
* 작업자 데이터: 모든 위치
* 작업자 데이터: 현재 인력 관리 정보
* 작업자 데이터: 작업자 프로필 직함

**tooconfigure 보안 그룹 옵션:**

1. 도메인 보안 정책을 hello 검색 상자에 입력 한 다음 링크를 클릭 hello **기능 영역에 대 한 도메인 보안 정책**합니다.  
   
    ![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "도메인 보안 정책")  
2. 시스템 및 선택 hello에 대 한 검색 **시스템** 기능 영역입니다.  **확인**을 클릭합니다.  
   
    ![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "도메인 보안 정책")  
3. Hello hello 시스템 기능 영역에 대 한 보안 정책 목록에서 확장 **보안 관리** hello 도메인 보안 정책을 선택 하 고 **외부 계정 프로 비전**합니다.  
   
    ![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "도메인 보안 정책")  
4. 클릭 **사용 권한 편집**를 선택한 후 hello **사용 권한 편집**대화 상자 페이지에서 hello 새 보안 그룹 toohello 목록으로 보안 그룹의 추가 **가져오기** 및 **배치** 통합 사용 권한. 
   
    ![사용 권한 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "사용 권한 편집")  
5. 기능 영역을 선택 하기 위한 tooreturn toohello 화면 위의 1 단계와 검색 인력 선택 hello 반복 **인력 기능 영역** 클릭 **확인**합니다.
   
    ![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "도메인 보안 정책")  
6. Hello hello 인력 기능 영역에 대 한 보안 정책 목록에서 확장 **작업자 데이터: 직원 배치** 및 보안 정책에 남아 있는이 각각에 대해 4 단계를 반복 합니다.

   * 작업자 데이터: 공용 작업자 보고서
   * 작업자 데이터: 모든 위치
   * 작업자 데이터: 현재 인력 관리 정보
   * 작업자 데이터: 작업자 프로필 직함
   
7. Tooreturn toohello 화면 선택 기능 영역에 대 한 위의 1 단계를 반복 하 고이 시간에 대 한 검색 **연락처 정보**, hello 인력 기능 영역을 선택 하 고 클릭 **확인**합니다.

8.  Hello hello 인력 기능 영역에 대 한 보안 정책 목록에서 확장 **작업자 데이터: 작업 연락처 정보**, 및 아래 hello 보안 정책에 대 한 위의 4 단계를 반복 합니다.

    * 작업자 데이터: 업무용 메일

    ![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "도메인 보안 정책")  
    
### <a name="activate-security-policy-changes"></a>보안 정책 변경 사항 활성화

**tooactivate 보안 정책 변경 내용:**

1. 입력 hello 검색 상자에 활성화 하 고 hello 링크를 클릭 한 다음 **보류 중인 보안 정책 변경 내용 활성화**합니다. 
   
    ![활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "활성화") 
2. 보류 중인 보안 정책 변경 내용 활성화 감사할 목적에 대 한 설명을 입력 하 여 작업 하 고 클릭 한 다음 시작 hello **확인**합니다. 
   
    ![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "보류 중인 보안 활성화")   
3. Hello hello 확인란을 선택 하 여 다음 화면에서 작업 완료 hello **확인**, 클릭 하 고 **확인**합니다. 
   
    ![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "보류 중인 보안 활성화")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Workday tooActive 디렉터리에서에서 사용자 프로비저닝 구성
이러한 지침 tooconfigure 사용자 계정 프로 비전 필요로 하는 Active Directory 포리스트 Workday tooeach에서 프로 비전을 수행 합니다.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello를 추가 하 고 hello 연결 tooWorkday 만들기

**tooconfigure Workday tooActive 디렉터리 프로비저닝이:**

1.  너무 이동<https://portal.azure.com>

2.  Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**

3.  **엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.

4.  선택 **응용 프로그램 추가**, 및 select hello **모든** 범주입니다.

5.  검색할 **Workday에 프로 비전 tooActive 디렉터리**, hello 갤러리에서 해당 앱을 추가 합니다.

6.  선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**

7.  변경 hello **프로 비전** **모드** 너무**자동**

8.  전체 hello **관리자 자격 증명** 다음과 같은 섹션:

   * **관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다. **다음과 같은 형태여야 합니다. username@contoso4**

   * **관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력

   * **테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다. 이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl hello 올바른 환경 문자열으로 대체 됩니다.

   * **Active Directory 포리스트-** hello Get ADForest powershell commandlet에 의해 반환 된 Active Directory 포리스트 "Name" hello 합니다. 일반적으로 *contoso.com* 형태의 문자열입니다.

   * **Active Directory 컨테이너-** AD 포리스트에 있는 모든 사용자가 포함 된 hello 컨테이너 문자열을 입력 합니다. 예: *OU=Standard Users,OU=Users,DC=contoso,DC=test*

   * **알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.

   * Hello 클릭 **연결 테스트** 단추입니다. Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다. 실패 한 경우 hello Workday 자격 증명이 Workday에 유효한 지 다시 확인 하십시오. 

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>2부: 특성 매핑 구성 

이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.

1.  Hello 프로 비전 탭에서 **매핑**, 클릭 **Workday 작업자 동기화 tooOnPremises**합니다.

2.  Hello에 **소스 개체 범위** 필드에서 어떤 유형의 사용자가 Workday의 tooAD, 일련의 특성 기반 필터를 정의 하 여 프로 비전에 대 한 범위에 속해야 합니다. 선택할 수 있습니다. hello 기본 범위는 "업무 시간에 모든 사용자". 예제 필터:

   * 예: 1000000 사이의 2000000 작업자 Id를 가진 toousers 범위

      * 특성: WorkerID

      * 연산자: REGEX Match

      * 값: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * 예: 정규직 직원만 포함하고 비정규직 직원은 포함하지 않음 

      * 특성: EmployeeID

      * 연산자: IS NOT NULL

3.  Hello에 **대상 개체 작업** 필드 어떤 작업이 Active Directory에 수행 하는 toobe 허용 전체적으로 필터링 할 수 있습니다. **만들기** 및 **업데이트**가 가장 일반적입니다.

4.  Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다.

5. 기존 특성 매핑 tooupdate를 클릭 하거나 클릭 **새 매핑을 추가** hello 화면 tooadd 새 매핑 hello 맨 아래에 있습니다. 개별 특성 매핑은 다음 속성을 지원합니다.

      * **매핑 유형**

         * **직접** – hello 변경 하지 않고 hello Workday 특성 toohello AD 특성의 값을 씁니다.

         * **상수** -hello AD 특성에 정적 상수 문자열 값을 기록

         * **식** – toowrite hello AD 특성에 하나 이상의 Workday 특성을 기반으로 사용자 지정 값을 허용 합니다. [자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **원본 특성** -작업일에서 hello 사용자 특성입니다.

      * **기본값** – 선택 사항입니다. Hello 원본 특성 값이 비어 있으면 hello 매핑이이 값 대신 기록 합니다.
            가장 일반적인 구성은 빈 tooleave 합니다.

      * **대상 특성** – Active Directory의 사용자 특성 hello 합니다.

      * **이 특성을 사용 하 여 개체를 일치** 이 매핑을 사용할지 여부-toouniquely Workday와 Active Directory 간에 사용자를 식별 합니다. 일반적으로 Active Directory의 hello 직원 ID 특성 중 하나에 매핑되는 Workday에 일반적으로 작업자 ID 필드에서 설정 됩니다.

      * **일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다. 일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다. 일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.

      * **이 매핑 적용**
       
         * **항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.

         * **만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.

6. toosave 매핑을 클릭 **저장** hello 위쪽 특성 매핑 섹션에 있습니다.

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**아래는 몇 가지 일반적인 식을 사용한 Workday와 Active Directory 간의 특성 매핑을 보여주는 예입니다.**

-   toohello parentDistinguishedName AD 특성을 매핑하는 hello 식을 사용 하는 특정 OU 특성을 기반으로 하나 이상의 Workday 소스 사용자 tooa tooprovision 수 있습니다. 이 예에서는 Workday의 도시 데이터에 따라 사용자를 여러 OU에 배치합니다.

-   toohello AD userPrincipalName 특성을 매핑하는 hello 식의 UPN을 만들려면 firstName.LastName@contoso.com합니다. 또한 잘못된 특수 문자를 바꿉니다.

-   [식을 쓰는 방법에 대한 설명서는 여기](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| WORKDAY 특성 | ACTIVE DIRECTORY 특성 |  ID 일치 여부 | 만들기/업데이트 |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **예** | 만들기 작업 시에만 기록 | 
|  **Municipality**   |   l   |     | 만들기 + 업데이트 |
|  **Company**         | company   |     |  만들기 + 업데이트 |
|  **CountryReferenceTwoLetter**      |   co |     |   만들기 + 업데이트 |
| **CountryReferenceTwoLetter**    |  C  |     |         만들기 + 업데이트 |
| **SupervisoryOrganization**  | department  |     |  만들기 + 업데이트 |
|  **PreferredNameData**  |  displayName |     |   만들기 + 업데이트 |
| **EmployeeID**    |  cn    |   |   만들기 작업 시에만 기록 |
| **Fax**      | facsimileTelephoneNumber     |     |    만들기 + 업데이트 |
| **FirstName**   | givenName       |     |    만들기 + 업데이트 |
| **Switch(\[Active\], , "0", "True", "1",)** |  accountDisabled      |     | 만들기 + 업데이트 |
| **Mobile**  |    mobile       |     |       만들기 작업 시에만 기록 |
| **EmailAddress**    | mail    |     |     만들기 + 업데이트 |
| **ManagerReference**   | manager  |     |  만들기 + 업데이트 |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  만들기 + 업데이트 |
| **PostalCode**  |   postalCode  |     | 만들기 + 업데이트 |
| **LocalReference** |  preferredLanguage  |     |  만들기 + 업데이트 |
| **Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.) \*\$](file:///\\.) *$)", , "", , )**      |    sAMAccountName            |     |         만들기 작업 시에만 기록 |
| **LastName**   |   sn   |     |  만들기 + 업데이트 |
| **CountryRegionReference** |  st     |     | 만들기 + 업데이트 |
| **AddressLineData**    |  streetAddress  |     |   만들기 + 업데이트 |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | 만들기 작업 시에만 기록 |
| **BusinessTitle**   |  title     |     |  만들기 + 업데이트 |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | 만들기 + 업데이트                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  만들기 + 업데이트 |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>3 부: hello 온-프레미스 동기화 에이전트를 구성 합니다.

순서 tooprovision tooActive Directory 온-프레미스에 hello desire Active Directory 포리스트에 도메인에 가입 된 서버에 에이전트를 설치 합니다. Hello 절차를 완료 하려면 자격 증명이 필요 도메인 관리자 (또는 엔터프라이즈 관리자)입니다.

**[Hello 온-프레미스 동기화 에이전트 여기를 다운로드할 수 있습니다.](https://go.microsoft.com/fwlink/?linkid=847801)**

에이전트를 설치한 후 사용자 환경에 대 한 tooconfigure hello 에이전트 다음과 같은 hello Powershell 명령을 실행 합니다.

**명령 #1**

> cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent

> import-module AADSyncAgent.psd1

**명령 #2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* 입력: "Directory Name"에 대 한 입력 hello AD 포리스트 이름 일부를 입력 한 대로 \#2
* 입력: Active Directory 포리스트의 관리 사용자 이름 및 암호 입력

**명령 #3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* 입력: Azure AD 테넌트의 전역 관리 사용자 이름 및 암호

**명령 #4**

> Get-AdSyncAgentProvisioningTasks

* 작업: 데이터가 반환되었는지 확인합니다. 이 명령은 Azure AD 테넌트에서 Workday 프로비전 앱을 자동으로 검색합니다. 예제 출력:

> Name          : My AD Forest
>
> Enabled       : True
>
> DirectoryName : mydomain.contoso.com
>
> Credentialed  : False
>
> Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**명령 #5**

> Start-AdSyncAgentSynchronization -Automatic

**명령 #6**

> net stop aadsyncagent

**명령 #7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>4 단계: hello 서비스 시작
파트 1-3가 완료 되 면 hello hello Azure 관리 포털에 다시 서비스를 프로 비전을 시작할 수 있습니다.

1.  Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.

2. **Save**를 클릭합니다.

3. 가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.

4. Workday에서 사용자가 같은 개별 동기화 이벤트를 읽어 되 고 다음 hello에 이후에 추가 되거나 업데이트 된 tooActive 디렉터리를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**

5.  hello 에이전트 컴퓨터에서 Windows 응용 프로그램 로그 hello hello 에이전트를 통해 수행 되는 모든 작업 표시 됩니다.

6. 작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>사용자 프로비저닝 tooAzure Active Directory를 구성 합니다.
프로 비전 tooAzure Active Directory를 구성 하는 방법 hello 테이블 아래에 설명 된 대로 프로 비전 요구 사항에 따라 달라 집니다.

| 시나리오 | 해결 방법 |
| -------- | -------- |
| **사용자를 프로 비전 toobe tooActive 디렉터리와 Azure AD 사용자가 필요** | **[AAD Connect](connect/active-directory-aadconnect.md)** 사용 |
| **사용자가 필요한 사용자를 프로 비전 toobe tooActive 디렉터리만** | **[AAD Connect](connect/active-directory-aadconnect.md)** 사용 |
| **사용자가 필요한 사용자를 프로 비전 toobe tooAzure AD만 (클라우드 전용)** | 사용 하 여 hello **Workday tooAzure Active Directory 프로비저닝** hello 응용 프로그램 갤러리에서 응용 프로그램 |

Azure AD Connect 설치에 자세한 내용은 hello [Azure AD Connect 설명서](connect/active-directory-aadconnect.md)합니다.

다음 섹션 hello tooprovision 클라우드 전용 사용자 Workday와 Azure AD 간의 연결 설정을 설명 합니다.

> [!IMPORTANT]
> 클라우드 전용 사용자 프로 비전 toobe tooAzure AD 및 온-프레미스 Active Directory 하지 필요로 하는 경우에 아래 hello 절차를 따릅니다.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello Azure AD 추가 하 고 hello 연결 tooWorkday 만들기

**tooconfigure 클라우드 전용 사용자에 대 한 Workday tooAzure Active Directory 프로비저닝.**

1.  너무 이동<https://portal.azure.com>합니다.

2.  Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**

3.  **엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.

4.  선택 **응용 프로그램 추가**를 선택한 후 hello **모든** 범주입니다.

5.  검색할 **Workday tooAzure AD 프로 비전**, hello 갤러리에서 해당 앱을 추가 합니다.

6.  선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**

7.  변경 hello **프로 비전** **모드** 너무**자동**

8.  전체 hello **관리자 자격 증명** 다음과 같은 섹션:

   * **관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다. 다음과 같은 형태여야 합니다. username@contoso4

   * **관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력

   * **테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다. 이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl 아래 템플릿으로 바뀝니다 hello 올바른 환경 문자열 (필요한 경우).

   * **알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.

   * Hello 클릭 **연결 테스트** 단추입니다.

   * Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다. 실패 한 경우 해당 hello 작업일 URL을 다시 확인 하 고 자격 증명이 Workday에서 유효 합니다.


### <a name="part-2-configure-attribute-mappings"></a>2부: 특성 매핑 구성 

이 섹션에서는 클라우드 전용 사용자의 사용자 데이터가 Workday에서 Azure Active Directory로 흐르는 방식을 구성하겠습니다.

1.  Hello 프로 비전 탭에서 **매핑**, 클릭 **동기화 작업자 tooAzure AD**합니다.

2.   Hello에 **소스 개체 범위** 필드에서 어떤 유형의 사용자가 Workday의 특성 기반 필터 집합을 정의 하 여 tooAzure 광고를 프로 비전에 대 한 범위에 속해야 합니다. 선택할 수 있습니다. hello 기본 범위는 "업무 시간에 모든 사용자". 예제 필터:

   * 예: 1000000 사이의 2000000 작업자 Id를 가진 toousers 범위

      * 특성: WorkerID

      * 연산자: REGEX Match

      * 값: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * 예: 비정규직 직원만 포함하고 정규직 직원은 포함하지 않음

      * 특성: ContingentID

      * 연산자: IS NOT NULL

3.  Hello에 **대상 개체 작업** 필드 어떤 작업이 Azure AD에 수행 하는 toobe 허용 전체적으로 필터링 할 수 있습니다. **만들기** 및 **업데이트**가 가장 일반적입니다.

4.  Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다.

5. 기존 특성 매핑 tooupdate를 클릭 하거나 클릭 **새 매핑을 추가** hello 화면 tooadd 새 매핑 hello 맨 아래에 있습니다. 개별 특성 매핑은 다음 속성을 지원합니다.

   * **매핑 유형**

      * **직접** – hello 변경 하지 않고 hello Workday 특성 toohello AD 특성의 값을 씁니다.

      * **상수** -hello AD 특성에 정적 상수 문자열 값을 기록

      * **식** – toowrite hello AD 특성에 하나 이상의 Workday 특성을 기반으로 사용자 지정 값을 허용 합니다. [자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **원본 특성** -작업일에서 hello 사용자 특성입니다.

   * **기본값** – 선택 사항입니다. Hello 원본 특성 값이 비어 있으면 hello 매핑이이 값 대신 기록 합니다.
            가장 일반적인 구성은 빈 tooleave 합니다.

   * **대상 특성** – Azure AD의 사용자 특성 hello 합니다.

   * **이 특성을 사용 하 여 개체를 일치** 이 매핑을 사용할지 여부-toouniquely Workday와 Azure AD 간에 사용자를 식별 합니다. 일반적으로 Azure AD에서 일반적으로 hello 직원 ID 특성 (새) 또는 확장 특성에 매핑되는 Workday에 대 한 작업자 ID 필드에서 설정 됩니다.

   * **일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다. 일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다. 일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.

   * **이 매핑 적용**

     * **항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.

     * **만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.

6. toosave 매핑을 클릭 **저장** hello 위쪽 특성 매핑 섹션에 있습니다.

### <a name="part-3-start-hello-service"></a>3 부: hello 서비스 시작
파트 1-2가 완료 되 면 hello 서비스를 프로 비전을 시작할 수 있습니다.

1.  Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.

2. **Save**를 클릭합니다.

3. 가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.

4. Hello에 개별 동기화 이벤트를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**

5. 작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>전자 메일 주소 tooWorkday의 쓰기 저장 구성
Azure Active Directory tooWorkday에서 사용자 전자 메일 주소의 이러한 지침 tooconfigure 쓰기 저장을 수행 합니다.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello를 추가 하 고 hello 연결 tooWorkday 만들기

**tooconfigure Workday tooActive 디렉터리 프로비저닝이:**

1.  너무 이동<https://portal.azure.com>

2.  Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**

3.  **엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.

4.  선택 **응용 프로그램 추가**을 선택한 후 hello **모든** 범주입니다.

5.  검색할 **Workday 쓰기 저장**, hello 갤러리에서 해당 앱을 추가 합니다.

6.  선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**

7.  변경 hello **프로 비전** **모드** 너무**자동**

8.  전체 hello **관리자 자격 증명** 다음과 같은 섹션:

   * **관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다. 다음과 같은 형태여야 합니다. username@contoso4

   * **관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력

   * **테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다. 이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl 아래 템플릿으로 바뀝니다 hello 올바른 환경 문자열 (필요한 경우).

   * **알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.

   * Hello 클릭 **연결 테스트** 단추입니다. Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다. 실패 한 경우 해당 hello 작업일 URL을 다시 확인 하 고 자격 증명이 Workday에서 유효 합니다.


### <a name="part-2-configure-attribute-mappings"></a>2부: 특성 매핑 구성 


이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.

1.  Hello 프로 비전 탭에서 **매핑**, 클릭 **동기화 Azure AD 사용자 tooWorkday**합니다.

2.  Hello에 **소스 개체 범위** 필드를 필요에 따라가 전자 메일 주소로 서 면으로 다시 tooWorkday 어떤 유형의 Azure Active Directory에서 사용자가 필터링 할 수 있습니다. hello 기본 범위는 "Azure AD의 모든 사용자". 

3.  Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다. 기본적으로 hello 전자 메일 주소에 대 한 매핑이 있습니다. 그러나 일치 하는 ID hello Workday에 해당 하는 항목이으로 Azure AD에 업데이트 된 toomatch 사용자 여야 합니다. 일치 하는 인기 있는 메서드는 toosynchronize hello Workday 작업자 ID 또는 직원 tooextensionAttribute1 15 Azure AD에서 ID이 고 Workday에 다시 toomatch 사용자가 Azure AD에서이 특성을 사용 합니다.

4.  toosave 매핑을 클릭 **저장** hello 위쪽 hello 특성 매핑 섹션에 있습니다.

### <a name="part-3-start-hello-service"></a>3 부: hello 서비스 시작
파트 1-2가 완료 되 면 hello 서비스를 프로 비전을 시작할 수 있습니다.

1.  Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.

2. **Save**를 클릭합니다.

3. 가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.

4. Hello에 개별 동기화 이벤트를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**

5. 작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.

## <a name="known-issues"></a>알려진 문제

* **감사 로그 유럽 로캘의** -hello이 기술 미리 보기 릴리스는 hello로 알려진된 문제 [감사 로그](active-directory-saas-provisioning-reporting.md) hello에 표시 되지 않는 hello Workday 커넥터 앱에 대 한 [Azure포털](https://portal.azure.com) hello Azure AD 테 넌 트 유럽 데이터 센터에 있는 경우. 이 문제에 대한 픽스가 곧 출시될 예정입니다. 가까운 미래 업데이트에 대 한 hello에 다시이 공간을 확인 하십시오. 

## <a name="additional-resources"></a>추가 리소스
* [자습서: Workday와 Azure Active Directory 간 Single Sign-On 구성](active-directory-saas-workday-tutorial.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>다음 단계

* [Tooreview 기록 하는 방법을 알아보고 프로 비전 활동에 대 한 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
