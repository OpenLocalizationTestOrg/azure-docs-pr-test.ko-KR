---
title: "데이터 카탈로그 aaaGet 시작 | Microsoft Docs"
description: "종단 간 자습서 hello 시나리오와 Azure 데이터 카탈로그의 기능을 제공 합니다."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Azure 데이터 카탈로그 시작
Azure Data Catalog는 기업 데이터 자산의 등록 시스템 및 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 자세한 개요는 [Azure Data Catalog란](data-catalog-what-is-data-catalog.md)을 참조하세요.

이 자습서는 Azure Data Catalog를 시작하는 데 도움이 됩니다. 이 자습서의 다음 절차를 수행 하는 hello을 수행 합니다.

| 절차 | 설명 |
|:--- |:--- |
| [데이터 카탈로그 프로비전](#provision-data-catalog) |이 절차에서는 Azure Data Catalog를 프로비전하거나 설정합니다. Hello 카탈로그 되지으로 전에 설정 된 경우에이 단계를 수행 합니다. Azure 계정과 연결된 여러 구독이 있는 경우라도 조직(Microsoft Azure Active Directory 도메인)당 하나의 데이터 카탈로그만을 사용할 수 있습니다. |
| [데이터 자산 등록](#register-data-assets) |이 절차에서는 hello 데이터 카탈로그를 사용 하 여 hello AdventureWorks2014 예제 데이터베이스에서 데이터 자산을 등록 합니다. 등록은 hello 프로세스 압축 풀기 키 구조 등의 메타 데이터 이름, 유형 및 위치 hello 데이터 원본과 해당 메타 데이터 toohello 카탈로그를 복사 합니다. hello 데이터 원본 및 데이터 자산 남아 있는 되지만 hello 메타 데이터를 사용 하 여 hello 카탈로그 toomake을 보다 쉽게 검색 가능 하 고 이해할 수 있도록 합니다. |
| [데이터 자산 검색](#discover-data-assets) |이 절차에서는 hello 이전 단계에서 등록 된 hello Azure Data Catalog 포털 toodiscover 데이터 자산 사용 합니다. Azure Data Catalog를 데이터 원본에 등록 한 후 필요한 hello 데이터에 대 한 사용자가 쉽게 검색할 수 있도록 해당 메타 데이터는 hello 서비스에 의해 인덱싱됩니다. |
| [데이터 자산에 주석 추가](#annotate-data-assets) |이 절차에서는 hello에 대 한 주석 (설명, 태그, 문서 또는 전문가 같은 정보) 데이터 자산을 제공 합니다. 이 정보는 hello 데이터 원본에서 추출 된 hello 메타 데이터를 보완 하 고 toomake hello 데이터 소스 더 많은 이해할 수 있는 toomore 사용자 키를 누릅니다. |
| [Toodata 자산 연결](#connect-to-data-assets) |이 절차에서는 통합 클라이언트 도구(Excel 및 SQL Server 데이터 도구 등)와 통합되지 않은 도구(SQL Server Management Studio)에서 데이터 자산을 엽니다. |
| [데이터 자산 관리](#manage-data-assets) |이 절차에서는 데이터 자산에 대한 보안을 설정합니다. 데이터 카탈로그 사용자 액세스 toohello 데이터 자체 제공 하지 않습니다. hello hello 데이터 원본 소유자는 데이터 액세스를 제어합니다. <br/><br/> 데이터 카탈로그와 데이터 원본 및 뷰 hello를 검색할 수 **메타 데이터** 관련 toohello 소스 hello 카달로그에 등록 합니다. 그러나 데이터 원본 위치 표시만 toospecific 사용자나 특정 그룹의 toomembers 해야 경우가 있을 수 있습니다. 이러한 시나리오에 대 한 hello 카탈로그 및 제어 hello의 표시 유형 소유 하는 hello 자산 내에서 등록 된 데이터 자산의 데이터 카탈로그 tootake 소유권을 사용할 수 있습니다. |
| [데이터 자산 제거](#remove-data-assets) |이 절차에서는 tooremove 데이터 자산에서 데이터 카탈로그를 hello 하는 방법을 배웁니다. |

## <a name="tutorial-prerequisites"></a>자습서 필수 구성 요소
### <a name="azure-subscription"></a>Azure 구독
tooset Azure Data Catalog를 hello 소유자 또는 Azure 구독의 공동 소유자를 여야 합니다.

Azure 구독에는 Azure 데이터 카탈로그와 같은 toocloud 서비스 리소스에 액세스를 구성할 수 있습니다. 리소스 사용을 보고하고, 요금을 청구하고, 지불하는 방식을 제어할 수도 있습니다. 각 구독은 청구 및 지불 설정이 다를 수 있으므로 부서, 프로젝트, 지사 등에 따라 구독 및 계획이 다를 수 있습니다. 모든 클라우드 서비스 tooa 구독 속하고 toohave Azure Data Catalog를 설정 하려면 먼저 구독 해야 합니다. toolearn 더 참조 [계정, 구독 및 관리 역할 관리](../active-directory/active-directory-how-subscriptions-associated-directory.md)합니다.

구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/) 을 참조하세요.

### <a name="azure-active-directory"></a>Azure Active Directory
tooset Azure Data Catalog를 있습니다 서명 해야 Azure Active Directory (Azure AD) 사용자 계정을 사용 합니다. Hello 소유자 또는 Azure 구독의 공동 소유자 여야 합니다.  

Azure AD 비즈니스 toomanage id 및 액세스 방법으로 hello 클라우드 및 온-프레미스에서 모두에 대 한는 쉬운 방법을 제공합니다. 단일 회사 또는 학교 계정 toosign tooany 클라우드에서 사용 하거나 온-프레미스 웹 응용 프로그램. Azure 데이터 카탈로그는 Azure AD tooauthenticate 로그인 사용 됩니다. toolearn 더 참조 [Azure Active Directory 란](../active-directory/active-directory-whatis.md)합니다.

### <a name="azure-active-directory-policy-configuration"></a>Azure Active Directory 정책 구성
Toosign toohello 데이터 원본 등록 도구에서 시도할 때 하지만 toohello Azure Data Catalog 포털에 로그인 할 수 있는 상황이 발생할 수, 로그인 수 없는 오류 메시지가 발생 합니다. Hello 회사 네트워크나 외부 hello 회사 네트워크에서 연결 하는 경우에이 오류가 발생할 수 있습니다.

hello 등록 도구를 사용 하 여 *폼 인증* toovalidate 사용자 로그인 Azure Active Directory에 대해 합니다. 성공한 로그인에 대 한 Azure Active Directory 관리자가 사용 하도록 설정 해야 hello에서 폼 인증 *전역 인증 정책*합니다.

Hello 전역 인증 정책으로 hello 다음 이미지와 같이 인트라넷 및 익스트라넷 연결에 대해 개별적으로 인증을 사용할 수 있습니다. 연결 중인 hello 네트워크에 대 한 폼 인증을 사용 하지 않는 경우 로그인 오류가 발생할 수 있습니다.

 ![Azure Active Directory 전역 인증 정책](./media/data-catalog-prerequisites/global-auth-policy.png)

자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.

## <a name="provision-data-catalog"></a>데이터 카탈로그 프로비전
조직(Azure Active Directory 도메인)당 하나의 데이터 카탈로그만 제공할 수 있습니다. 따라서 hello 소유자 또는 Azure Active Directory 도메인 toothis 속한 Azure 구독의 공동 소유자가 이미 카탈로그를 만든 경우 됩니다 수 toocreate 카탈로그 다시 여러 Azure 구독이 있는 경우에 합니다. tootest Azure Active Directory 도메인에서 사용자가 만든 데이터 카탈로그 여부 이동 toohello [Azure Data Catalog 홈 페이지](http://azuredatacatalog.com) hello 카탈로그를 참조 하는지 여부를 확인 합니다. 카탈로그를 이미 생성 되어 hello 다음 절차 및 go toohello 다음 섹션을 건너뜁니다.    

1. Toohello 이동 [데이터 카탈로그 서비스 페이지](https://azure.microsoft.com/services/data-catalog) 클릭 **시작**합니다.
   
    ![Azure Data Catalog - 마케팅 방문 페이지](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Hello 소유자 또는 Azure 구독의 공동 소유자 인 사용자 계정으로 로그인 합니다. Hello 페이지에 로그인 한 후 다음을 참조 합니다.
   
    ![Azure Data Catalog - 데이터 카탈로그 프로비전](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. 지정는 **이름** hello 데이터 카탈로그에 대 한 hello **구독** toouse, 고 hello **위치** hello 카탈로그에 대 한 합니다.
4. **가격 책정**을 확장하고 Azure Data Catalog **버전**(무료 또는 Standard)을 선택합니다.
    ![Azure Data Catalog--버전 선택](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. 확장 **카탈로그 사용자** 클릭 **추가** hello 데이터 카탈로그에 대 한 tooadd 사용자입니다. Toothis 그룹을 자동으로 추가 됩니다.
    ![Azure Data Catalog--사용자](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. 확장 **카탈로그 관리자** 클릭 **추가** tooadd hello 데이터 카탈로그에 대 한 추가 관리자가 있습니다. Toothis 그룹을 자동으로 추가 됩니다.
    ![Azure Data Catalog--관리자](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. 클릭 **카탈로그 만들기** 조직의 toocreate hello 데이터 카탈로그입니다. 만든 후 hello 데이터 카탈로그에 대 한 hello 홈 페이지를 참조 하십시오.
    ![Azure Data Catalog--생성됨](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>데이터 카탈로그 hello Azure 포털에서 찾기
1. Hello 웹 브라우저에서 또는 별도 웹 브라우저 창에서 별도 탭 이동 toohello [Azure 포털](https://portal.azure.com) 로 서명 hello 동일한 계정을 해당 하면 사용한 toocreate hello 데이터 카탈로그 hello 이전 단계에서 및 합니다.
2. **찾아보기**를 선택한 다음 **Data Catalog**를 클릭합니다.
   
    ![Azure Data Catalog-Azure 찾아보기](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) 사용자가 만든 카탈로그 hello 데이터를 표시 합니다.
   
    ![Azure Data Catalog - 목록에서 카탈로그 보기](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. 만든 hello 카탈로그를 클릭 합니다. Hello 참조 **데이터 카탈로그** 블레이드 hello 포털에서입니다.
   
   ![Azure Data Catalog - 포털의 블레이드 ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Hello 데이터 카탈로그의 속성을 볼 수 있으며 업데이트. 예를 들어 클릭 **가격 책정 계층** hello 버전을 변경 합니다.
   
    ![Azure Data Catalog - 가격 책정 계층](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Adventure Works 샘플 데이터베이스
이 자습서에서는 SQL Server 데이터베이스 엔진 hello에 대 한 hello AdventureWorks2014 예제 데이터베이스에서 데이터 자산 (테이블)를 등록 하지만 toowork 친숙 하 고 관련 tooyour 역할은 데이터를 사용 하려는 경우 모든 지원 되는 데이터 원본을 사용할 수 있습니다. 지원되는 데이터 원본 목록은 [지원되는 데이터 원본](data-catalog-dsr.md)을 참조하세요.

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Hello Adventure Works 2014 OLTP 데이터베이스 설치
hello Adventure Works 데이터베이스 제품, 판매 및 구매를 포함 하는 가상의 자전거 제조업체 (Adventure Works Cycles)에 대 한 표준 온라인 트랜잭션 처리 시나리오를 지원 합니다. 이 자습서에서는 제품에 대한 정보를 Azure Data Catalog에 등록합니다.

tooinstall hello Adventure Works 예제 데이터베이스:

1. CodePlex에서 [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) 을 다운로드합니다.
2. 컴퓨터에 toorestore hello 데이터베이스 hello 지침에 따라 [SQL Server Management Studio를 사용 하 여 데이터베이스 백업을 복원](http://msdn.microsoft.com/library/ms177429.aspx), 또는 이러한 단계에 따라:
   1. SQL Server Management Studio를 열고 toohello SQL Server 데이터베이스 엔진에 연결 합니다.
   2. **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원**을 클릭합니다.
   3. 아래 **데이터베이스 복원**, hello 클릭 **장치** 옵션에 대 한 **소스** 클릭 **찾아보기**합니다.
   4. **백업 장치 선택** 아래에서 **추가**를 클릭합니다.
   5. Hello 있는 이동 toohello 폴더 **AdventureWorks2014.bak** 파일, 파일 선택 hello 및 클릭 **확인** tooclose hello **백업 파일 찾기** 대화 상자.
   6. 클릭 **확인** tooclose hello **백업 장치 선택** 대화 상자.    
   7. 클릭 **확인** tooclose hello **데이터베이스 복원** 대화 상자.

이제 Azure Data Catalog를 사용 하 여 hello Adventure Works 샘플 데이터베이스에서 데이터 자산을 등록할 수 있습니다.

## <a name="register-data-assets"></a>데이터 자산 등록
이 연습에서는 hello 등록 도구 tooregister 데이터 자산 hello Adventure Works 데이터베이스에서를 사용 하 여 hello 카탈로그. 등록은 hello 과정 hello 데이터 원본 및 포함 된 hello 자산에서 이름, 유형 및 위치와 같은 키 구조적 메타 데이터를 추출 하 고 해당 메타 데이터 toohello 카탈로그 복사입니다. hello 데이터 원본 및 데이터 자산 남아 있는 되지만 hello 메타 데이터를 사용 하 여 hello 카탈로그 toomake을 보다 쉽게 검색 가능 하 고 이해할 수 있도록 합니다.

### <a name="register-a-data-source"></a>데이터 원본 등록
1. Toohello 이동 [Azure Data Catalog 홈 페이지](http://azuredatacatalog.com) 클릭 **데이터 게시**합니다.
   
   ![Azure Data Catalog - 데이터 게시 단추](media/data-catalog-get-started/data-catalog-publish-data.png)
2. 클릭 **응용 프로그램 시작** toodownload, 설치 및 컴퓨터에서 실행된 hello 등록 도구입니다.
   
   ![Azure Data Catalog - 시작 단추](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Hello에 **시작** 페이지 **로그인** 자격 증명을 입력 하 고 있습니다.     
   
    ![Azure Data Catalog - 시작 페이지](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Hello에 **Microsoft Azure Data Catalog** 페이지 **SQL Server** 및 **다음**합니다.
   
    ![Azure Data Catalog - 데이터 원본](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Hello SQL Server 연결 속성에 대 한 입력 **AdventureWorks2014** (다음 예제는 hello 참조)를 클릭 하 고 **연결**합니다.
   
   ![Azure Data Catalog - SQL Server 연결 설정](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. 데이터 자산의 hello 메타 데이터를 등록 합니다. 이 예제에서는 등록 **프로덕션/제품** hello AdventureWorks 프로덕션 네임 스페이스에서 개체:
   
   1. Hello에 **서버 계층** 트리를 확장 **AdventureWorks2014** 클릭 **프로덕션**합니다.
   2. Ctrl 키를 누른 채 **Product**, **ProductCategory**, **ProductDescription** 및 **ProductPhoto**를 클릭하여 선택합니다.
   3. Hello 클릭 **선택한 화살표 이동** (**>**). 이 작업 hello에 선택한 모든 개체를 이동 합니다. **등록 개체 toobe** 목록입니다.
      
      ![Azure Data Catalog 자습서 - 개체 찾기 및 선택](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. 선택 **미리 보기가 포함** tooinclude hello 데이터의 스냅숏 미리 보기. hello 스냅숏 각 테이블에서 too20 레코드를 포함 하 고 hello 카탈로그에 복사 됩니다.
   5. 선택 **포함 데이터 프로필** tooinclude hello 데이터 프로필에 대 한 hello 개체 통계에 대 한 스냅숏 (예: 행 수 열에 대 한 최소, 최대 및 평균 값).
   6. Hello에 **태그 추가** 필드에, 입력 **adventure 작동, 주기**합니다. 이 작업은 데이터 자산에 대한 검색 태그를 추가합니다. 태그는 toohelp 사용자가 등록 된 데이터 소스를 찾기 위한 훌륭한 방법입니다.
   7. hello 이름을 지정는 **전문가** (선택 사항)이이 데이터에 있습니다.
      
      ![Azure Data Catalog 자습서--개체 toobe 등록](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. **등록**을 클릭합니다. Azure 데이터 카탈로그는 선택한 개체를 등록합니다. 이 연습에서는 Adventure Works의 개체를 선택 하는 hello 등록 됩니다. hello 등록 도구는 hello 데이터 자산에서 메타 데이터를 추출 하 고 hello Azure Data Catalog 서비스로 해당 데이터를 복사 합니다. hello 데이터는 유지 여기서 현재 상주 하 고 hello 관리자의 hello 제어 및 정책의 hello 현재 시스템의 상태를 유지 합니다.
      
      ![Azure Data Catalog - 등록된 개체](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. toosee 등록 된 데이터 원본 개체를 클릭 하 여 **보기 포털**합니다. Hello Azure Data Catalog 포털에서 모든 4 개의 테이블과 hello 데이터베이스 hello 그리드 보기에 표시 되는지 확인 합니다.
      
      ![Hello Azure Data Catalog 포털에 있는 개체 ](media/data-catalog-get-started/data-catalog-view-portal.png)

이 연습에서는 쉽게 찾을 수 사용자가 조직에 있도록 hello Adventure Works 샘플 데이터베이스에서 개체를 등록 합니다. Hello 다음 연습에서는 toodiscover 데이터 자산을 등록 하는 방법을 배웁니다.

## <a name="discover-data-assets"></a>데이터 자산 검색
Azure Data Catalog에서 검색은 검색 및 필터링이라는 두 가지 기본 메커니즘을 사용합니다.

검색은 설계 된 toobe 직관적이 고 강력 합니다. 기본적으로 검색 단어 hello 카탈로그에서 사용자가 제공한 주석 포함 한 모든 속성에 대해 일치 합니다.

필터링 기능은 toocomplement 검색 합니다. 데이터 자산 및 tooconstrain 검색 일치 하는 태그 tooview toomatching 자산 결과 및 전문가, 데이터 원본 유형, 개체 유형 등의 특정 특성을 선택할 수 있습니다.

검색 및 필터링 조합의 사용 하 여 필요한 Azure Data Catalog toodiscover hello 데이터 자산에 등록 된 hello 데이터 소스를 신속 하 게 이동할 수 있습니다.

이 연습에서는 hello Azure Data Catalog 포털 toodiscover 데이터 자산 hello 이전 연습에서 등록을 사용 합니다. 검색 구문에 대한 자세한 내용은 [Data Catalog Search 구문 참조](https://msdn.microsoft.com/library/azure/mt267594.aspx) 를 참조하세요.

다음은 hello 카탈로그에 대 한 데이터 자산을 검색 하기 위한 몇 가지 예입니다.  

### <a name="discover-data-assets-with-basic-search"></a>기본 검색을 사용하여 데이터 자산 검색
기본 검색을 사용하면 하나 이상의 검색 용어를 사용하여 카탈로그를 검색할 수 있습니다. 결과 하나 이상의 지정 된 hello 용어와 속성에 대해 일치 하는 모든 자산입니다.

1. 클릭 **홈** hello Azure Data Catalog 포털에 있습니다. Hello 웹 브라우저를 닫은 경우 이동 toohello [Azure Data Catalog 홈 페이지](https://www.azuredatacatalog.com)합니다.
2. Hello 검색 상자에 입력 `cycles` 누릅니다 **ENTER**합니다.
   
    ![Azure Data Catalog - 기본 텍스트 검색](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. 모든 4 개의 테이블과 hello 데이터베이스 (AdventureWorks2014) hello 결과에 표시 되는지 확인 합니다. 간을 전환할 수 있습니다 **그리드 보기** 및 **목록 보기** hello 다음 이미지와 같이 hello 도구 모음에서 단추를 클릭 하 여 합니다. 때문에 해당 hello 검색 키워드 hello 검색 결과에서 강조 표시 hello **강조 표시** 옵션은 **ON**합니다. Hello 수를 지정할 수도 있습니다 **페이지당 결과** 검색 결과에 있습니다.
   
    ![Azure Data Catalog - 기본 텍스트 검색 결과](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    hello **검색** 왼쪽 hello 및 hello에 패널은 **속성** 패널은 오른쪽 hello에 있습니다. Hello에 **검색** 패널에서 검색 조건을 변경 하 고 결과 필터링 합니다. hello **속성** 패널 hello 표 또는 목록에서 선택한 개체의 속성을 표시 합니다.
4. 클릭 **제품** hello 검색 결과에 있습니다. Hello 클릭 **미리 보기**, **열**, **데이터 프로필**, 및 **설명서** 탭에서 또는 hello 화살표 tooexpand hello 아래쪽 창을 클릭 합니다.  
   
    ![Azure Data Catalog - 아래쪽 창](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Hello에 **미리 보기** 탭 hello에 hello 데이터의 미리 보기를 볼 **제품** 테이블입니다.  
5. Hello 클릭 **열** 열에 대 한 toofind 세부 정보 탭 (같은 **이름** 및 **데이터 형식을**) hello 데이터 자산에 합니다.
6. Hello 클릭 **데이터 프로필** toosee hello를 프로 파일링 데이터 탭 (예: 행, 데이터 또는 열에 값이 최소 크기의 숫자) hello 데이터 자산에 있습니다.
7. 사용 하 여 hello 결과 필터링 **필터** hello 왼쪽에 있습니다. 예를 들어 클릭 **테이블** 에 대 한 **개체 유형**, 4 hello 테이블만 참조, 데이터베이스 하지 hello 및 합니다.
   
    ![Azure Data Catalog - 검색 결과 필터링](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>속성 범위로 데이터 자산 검색
지정한 속성을 통해 hello로 hello 검색 단어와 일치 하는 데이터 자산 검색 범위를 지정 하는 속성입니다.

1. 지우기 hello **테이블** 에서 필터링 **개체 유형** 에 **필터**합니다.  
2. Hello 검색 상자에 입력 `tags:cycles` 누릅니다 **ENTER**합니다. 참조 [데이터 카탈로그 검색 구문 참조](https://msdn.microsoft.com/library/azure/mt267594.aspx) 모든 hello hello 데이터 카탈로그를 검색에 사용할 수 있는 속성에 대 한 합니다.
3. 모든 4 개의 테이블과 hello 데이터베이스 (AdventureWorks2014) hello 결과에 표시 되는지 확인 합니다.  
   
    ![Data Catalog - 검색 결과 속성 범위 지정](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Hello 검색 저장
1. Hello에 **검색** hello에 창 **현재 검색** 섹션 hello 검색에 대 한 이름을 입력 하 고 클릭 **저장**합니다.
   
    ![Azure Data Catalog - 검색 저장](media/data-catalog-get-started/data-catalog-save-search.png)
2. 아래 해당 hello 저장 된 검색에 표시 확인 **저장 된 검색**합니다.
   
    ![Azure Data Catalog - 저장된 검색](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Hello 저장 된 검색을 수행할 수는 hello 동작 중 하나를 선택 (**이름 바꾸기**, **삭제**, **기본값으로 저장** 검색).
   
    ![Azure Data Catalog - 저장된 검색 옵션](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>부울 연산자
부울 연산자를 사용하여 검색 범위를 넓히거나 좁힐 수 있습니다.

1. Hello 검색 상자에 입력 `tags:cycles AND objectType:table`, 누릅니다 **ENTER**합니다.
2. 테이블에만 (hello 데이터베이스가 아니라) hello 결과에 표시 되는지 확인 합니다.  
   
    ![Azure Data Catalog - 검색에서 부울 연산자](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>괄호로 그룹화
괄호로 묶어서 hello 쿼리 tooachieve 논리적 격리, 부울 연산자와 함께 특히의 부분을 그룹화 수 있습니다.

1. Hello 검색 상자에 입력 `name:product AND (tags:cycles AND objectType:table)` 누릅니다 **ENTER**합니다.
2. Hello만 표시 되는지 확인 **제품** hello 검색 결과에 테이블입니다.
   
    ![Azure Data Catalog - 검색 그룹화](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>비교 연산자
비교 연산자를 사용하면 숫자 및 날짜 데이터 유형이 있는 속성에 대한 일치가 아닌 비교를 사용할 수 있습니다.

1. Hello 검색 상자에 입력 `lastRegisteredTime:>"06/09/2016"`합니다.
2. 지우기 hello **테이블** 에서 필터링 **개체 유형**합니다.
3. **ENTER**키를 누릅니다.
4. Hello 표시 되는지 확인 **제품**, **ProductCategory**, **ProductDescription**, 및 **ProductPhoto** 테이블 및 hello AdventureWorks2014 데이터베이스 검색 결과에 등록 합니다.
   
    ![Azure Data Catalog - 비교 검색 결과](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

참조 [어떻게 toodiscover 데이터 자산](data-catalog-how-to-discover.md) 데이터 자산을 검색 하는 방법에 대 한 자세한 내용은 및 [데이터 카탈로그 검색 구문 참조](https://msdn.microsoft.com/library/azure/mt267594.aspx) 검색 구문에 대 한 합니다.

## <a name="annotate-data-assets"></a>데이터 자산에 주석 추가
이 연습에서는 사용 하 여 hello Azure Data Catalog 포털 tooannotate (추가 설명, 태그 또는 전문가 같은 정보) 데이터 자산 hello 카탈로그에서 이전에 등록 합니다. hello 주석 보완 및 등록 하는 동안 hello 데이터 원본에서 추출 된 hello 구조적 메타 데이터를 강화 하 고 hello 데이터 자산 훨씬 더 쉽게 toodiscover을 만들고 이해 합니다.

이 연습에서는 단일 데이터 자산(ProductPhoto)에 주석을 지정합니다. 이름 및 설명 toohello ProductPhoto 데이터 자산을 추가 합니다.  

1. Toohello 이동 [Azure Data Catalog 홈 페이지](https://www.azuredatacatalog.com) 사용 하 여 검색 및 `tags:cycles` toofind hello 데이터 자산을 등록 합니다.  
2. 검색 결과에서 **ProductPhoto** 를 클릭합니다.  
3. 입력 **제품 이미지** 에 대 한 **이름** 및 **마케팅 자료에 대 한 제품 사진을** hello에 대 한 **설명**합니다.
   
    ![Azure Data Catalog - ProductPhoto 설명](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    hello **설명** 다른 사람들이 검색 및 toouse hello 데이터 자산을 선택한 이유 및 방법을 이해 하는 데 도움이 됩니다. 더 많은 태그를 추가하고 열을 볼 수도 있습니다. Hello 설명 메타 데이터를 사용 하 여 검색 및 필터링 toodiscover 데이터 자산을 연습할 수 이제 toohello 카탈로그를 추가 했습니다.

수행할 수 있습니다이 페이지에서 다음 hello:

* 전문가 hello 데이터 자산에 대 한 추가 합니다. 클릭 **추가** hello에 **전문가** 영역입니다.
* Hello 데이터 집합 수준에서 태그를 추가 합니다. 클릭 **추가** hello에 **태그** 영역입니다. 태그는 사용자 태그 또는 용어집 태그일 수 있습니다. 데이터 카탈로그의 Standard Edition hello 중앙 비즈니스 분류를 정의 하는 카탈로그 관리자는 데 유용한 비즈니스 용어집를 활용 포함 되어 있습니다. 그런 다음 카탈로그 사용자는 용어집 용어를 사용하여 데이터 자산에 주석을 추가할 수 있습니다. 자세한 내용은 참조 [를 tooset 비즈니스 용어집를 활용 태그 지정 제어에 대 한 hello 하는 방법](data-catalog-how-to-business-glossary.md)
* Hello 열 수준에서 태그를 추가 합니다. 클릭 **추가** 아래 **태그** 원하는 tooannotate hello 열에 대 한 합니다.
* Hello 열 수준에서 설명을 추가 합니다. 열에 **설명** 을 입력합니다. Hello 데이터 원본에서 추출 된 hello 설명 메타 데이터를 볼 수 있습니다.
* 추가 **액세스 권한을 요청** toorequest toohello 데이터 자산을 액세스 하는 방법을 사용자가 보여 주는 정보입니다.
  
    ![Azure Data Catalog - 태그, 설명 추가](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Hello 선택 **설명서** 탭 및 hello 데이터 자산에 대 한 설명서를 제공 합니다. Azure Data Catalog 설명서 콘텐츠 리포지토리 toocreate 데이터 자산의 전체 narrative로 데이터 카탈로그를 사용할 수 있습니다.
  
    ![Azure Data Catalog - 설명서 탭](media/data-catalog-get-started/data-catalog-documentation.png)

또한 주석 toomultiple 데이터 자산을 추가할 수 있습니다. 예를 들어 모든 hello 데이터 자산을 등록를 선택 하 고을 전문가 지정 수 있습니다.

![Azure Data Catalog - 여러 데이터 자산에 주석 추가](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure 데이터 카탈로그 관중 소싱 접근 방식을 tooannotations를 지원합니다. 모든 데이터 카탈로그 사용자의 용도 및 데이터 자산에 큐브 뷰가 있는 모든 사용자를 해당 캡처된 관리자의 관점 및 사용 가능한 tooother 사용자가 가질 수 있습니다 태그 (사용자 또는 용어), 설명 및 기타 메타 데이터를 추가할 수 있습니다.

참조 [어떻게 tooannotate 데이터 자산](data-catalog-how-to-annotate.md) 데이터 자산에 주석 지정 하는 방법에 대 한 자세한 정보에 대 한 합니다.

## <a name="connect-toodata-assets"></a>Toodata 자산 연결
이 연습에서는 연결 정보를 사용하여 통합 클라이언트 도구(Excel)와 통합되지 않은 도구(SQL Server Management Studio)에서 데이터 자산을 엽니다.

> [!NOTE]
> Azure 데이터 카탈로그를 제공 하지 않으면 tooremember toohello 실제 데이터 원본 액세스 것이 중요-단순히 쉽게 있습니다 toodiscover 하 고 이해 합니다. Tooa 데이터 원본에 연결할 때 hello 클라이언트 응용 프로그램을 사용 하 여 사용자 Windows 자격 증명 또는 필요에 따라 자격 증명을 묻는 선택 합니다. 하지 이전에 부여 된 액세스 toohello 데이터 소스를 경우 toobe 연결 하려면 먼저 액세스를 부여 해야 합니다.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Excel에서 tooa 데이터 자산에 연결
1. 검색 결과에서 **상품** 을 선택합니다. 클릭 **다음에서 열기** hello 도구 모음 및 클릭 **Excel**합니다.
   
    ![Azure Data Catalog-toodata 자산에 연결](media/data-catalog-get-started/data-catalog-connect1.png)
2. 클릭 **열려** hello 다운로드 팝업 창에 있습니다. Hello 브라우저에 따라이 다를 수 있습니다.
   
    ![Azure Data Catalog - 다운로드한 Excel 연결 파일](media/data-catalog-get-started/data-catalog-download-open.png)
3. Hello에 **Microsoft Excel 보안 알림** 창 클릭 **사용**합니다.
   
    ![Azure Data Catalog - Excel 보안 팝업](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Hello에 hello 기본값을 유지 **데이터 가져오기** 대화 상자와 클릭 **확인**합니다.
   
    ![Azure Data Catalog - Excel 가져오기 데이터](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Excel에서 hello 데이터 원본 보기
   
    ![Azure Data Catalog - Excel의 제품 테이블](media/data-catalog-get-started/data-catalog-connect2.png)

이 연습에서는 Azure Data Catalog를 사용 하 여 검색 toodata 자산에 연결 되어 있습니다. Hello Azure Data Catalog 포털 hello 클라이언트 hello에 통합 된 응용 프로그램을 사용 하 여 직접 연결할 수 있습니다 **에 열려 있는** 메뉴. Hello 자산 메타 데이터에 포함 된 hello 연결 위치 정보를 사용 하 여 선택 하는 모든 응용 프로그램과 연결할 수 있습니다. 예를 들어이 자습서에 등록 하는 hello 데이터 자산에서 SQL Server Management Studio tooconnect toohello AdventureWorks2014 데이터베이스 tooaccess hello 데이터를 사용할 수 있습니다.

1. **SQL Server Management Studio**를 엽니다.
2. Hello에 **tooServer 연결** 대화 상자에서 hello hello 서버 이름을 입력 합니다 **속성** hello Azure Data Catalog 포털 창.
3. 적절 한 인증 및 자격 증명 tooaccess hello 데이터 자산을 사용 합니다. 액세스할 수 없는 경우 정보를 사용 하 여 hello에 **액세스 요청** 필드 tooget 것입니다.
   
    ![Azure Data Catalog - 액세스 요청](media/data-catalog-get-started/data-catalog-request-access.png)

클릭 **연결 문자열을 봅니다.** tooview 및 복사 ADF.NET, ODBC 및 OLEDB 연결 문자열 toohello 클립보드에 응용 프로그램에서 사용 합니다.

## <a name="manage-data-assets"></a>데이터 자산 관리
이 단계에서는 참조 방식을 tooset 데이터 자산에 대 한 보안을 합니다. 데이터 카탈로그 사용자 액세스 toohello 데이터 자체 제공 하지 않습니다. hello hello 데이터 원본 소유자는 데이터 액세스를 제어합니다.

데이터 카탈로그를 사용 하 여 toodiscover 데이터 원본 및 tooview hello 메타 데이터 관련 toohello 소스 hello 카달로그에 등록 합니다. 그러나 표시 toospecific 사용자 또는 toomembers 특정 그룹의 데이터 원본 수만 해야 경우가 있을 수 있습니다. 이러한 시나리오에 대 한 hello 카탈로그 내에서 등록 된 데이터 자산의 데이터 카탈로그 tootake 소유권 및 소유 하는 hello 자산의 toothen 제어 hello 표시 유형을 사용할 수 있습니다.

> [!NOTE]
> 이 연습에서 설명 하는 hello 관리 기능에서 사용할 수만 hello 표준 버전의 Azure 데이터 카탈로그에 없는 hello 무료 버전입니다.
> Azure Data Catalog에서 데이터 자산의 소유권, 공동 소유자 toodata 자산을 추가한 데이터 자산의 hello 표시 유형을 설정 합니다.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>데이터 자산 소유권 가져오기 및 표시 유형 제한
1. Toohello 이동 [Azure Data Catalog 홈 페이지](https://www.azuredatacatalog.com)합니다. Hello에 **검색** 텍스트 상자에 입력 `tags:cycles` 누릅니다 **ENTER**합니다.
2. Hello 결과 목록에서 항목을 클릭 하 고 클릭 **Take Ownership** hello 도구 모음입니다.
3. Hello에 **관리** hello 섹션 **속성** 에서 **Take Ownership**합니다.
   
    ![Azure Data Catalog - 소유권 가져오기](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. toorestrict 표시 여부 선택 **소유자 및 이러한 사용자** hello에 **가시성** 섹션 및 클릭 **추가**합니다. 키를 눌러 / hello 텍스트 상자에 사용자 전자 메일 주소를 입력 **ENTER**합니다.
   
    ![Azure Data Catalog - 액세스 제한](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>데이터 자산 제거
이 연습에서는 hello Azure Data Catalog 포털 tooremove 등록 된 데이터 자산 중에서 데이터를 미리 보기를 사용 하 고 hello 카탈로그에서 데이터 자산을 삭제 합니다.

Azure Data Catalog에서 개별 자산을 삭제하거나 여러 자산을 삭제할 수 있습니다.

1. Toohello 이동 [Azure Data Catalog 홈 페이지](https://www.azuredatacatalog.com)합니다.
2. Hello에 **검색** 텍스트 상자에 입력 `tags:cycles` 클릭 **ENTER**합니다.
3. Hello 결과 목록에서 항목을 선택 하 고 클릭 **삭제** hello 다음 이미지와 같이 hello 도구 모음에서:
   
    ![Azure Data Catalog - 그리드 항목 삭제](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Hello 목록 보기를 사용 하는 경우 hello 확인란이 hello 항목의 왼쪽 toohello hello 다음 이미지에에서 표시 된 대로:
   
    ![Azure Data Catalog - 목록 항목 삭제](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    또한 여러 개의 데이터 자산을 선택할 수 있으며 hello 다음 이미지와 같이 삭제:
   
    ![Azure Data Catalog - 여러 데이터 자산 삭제](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> hello 카탈로그의 기본 동작을 hello tooallow 모든 사용자 tooregister 모든은 데이터 원본과 tooallow 모든 사용자 toodelete에 등록 된 모든 데이터 자산입니다. hello 관리 기능 hello 표준 버전의 Azure Data Catalog에에서 포함 된 자산을 삭제할 수 있는 자산을 제한 하 고 자산을 검색할 수 있는 제한의 소유권을 획득 하기 위한 추가 옵션을 제공 합니다.
> 
> 

## <a name="summary"></a>요약
이 자습서에서는 엔터프라이즈 데이터 자산 등록, 주석 추가, 검색, 관리를 비롯하여 Azure Data Catalog의 필수 기능을 살펴보았습니다. 이제는 hello 자습서를 완료 하면이 시간 tooget 시작 합니다. 팀에 의존 하는 hello 데이터 소스를 등록 하 여 및 toouse hello 카탈로그 동료를 초대 하 여 오늘 시작 합니다.

## <a name="references"></a>참조
* [어떻게 tooregister 데이터 자산](data-catalog-how-to-register.md)
* [어떻게 toodiscover 데이터 자산](data-catalog-how-to-discover.md)
* [어떻게 tooannotate 데이터 자산](data-catalog-how-to-annotate.md)
* [어떻게 toodocument 데이터 자산](data-catalog-how-to-documentation.md)
* [어떻게 tooconnect toodata 자산](data-catalog-how-to-connect.md)
* [어떻게 toomanage 데이터 자산](data-catalog-how-to-manage.md)

