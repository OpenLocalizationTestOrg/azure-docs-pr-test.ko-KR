---
title: "aaaManage 데이터베이스 역할 및 Azure Analysis Services의 사용자 | Microsoft Docs"
description: "역할 및 Azure에는 Analysis Services 서버에서 사용자 toomanage 데이터베이스 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>데이터베이스 역할 및 사용자 관리

Hello 모델 데이터베이스 수준에서 모든 사용자에 게 tooa 역할을 속해 있어야 합니다. 역할은 hello model 데이터베이스에 대 한 특정 사용 권한이 있는 사용자를 정의합니다. 모든 사용자 또는 보안 그룹 추가 tooa 역할 hello에 Azure AD 테 넌 트의 계정이 있어야 hello 서버와 동일한 구독 합니다.

역할을 정의 하는 방법에 hello 도구를 사용 하면 다른 따라 않으며 hello 효과 동일 hello는입니다.

역할 권한은 다음과 같습니다.
*  **관리자** -사용자가 있는 hello 데이터베이스에 대 한 모든 권한을 갖습니다. 관리자 권한이 있는 데이터베이스 역할은 서버 관리자와 다릅니다.
*  **프로세스** -사용자가 tooand 연결할 수 hello 데이터베이스에서 프로세스 작업을 수행 하 고 모델 데이터베이스 데이터를 분석 합니다.
*  **읽기** -는 클라이언트를 사용 하 여 사용자가 응용 프로그램 tooconnect tooand 모델 데이터베이스 데이터를 분석 합니다.

테이블 형식 모델 프로젝트를 만들 때 역할 만들고 SSDT의 역할 관리자를 사용 하 여 사용자 또는 그룹 toothose 역할을 추가 합니다. 배포 된 tooa 서버를 사용 하는 경우 SSMS [Analysis Services PowerShell cmdlet](https://msdn.microsoft.com/library/hh758425.aspx), 또는 [테이블 형식 모델 스크립팅 언어](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd 또는 역할 및 사용자 멤버를 제거 합니다.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd 또는 역할 및 SSDT의 사용자 관리  
  
1.  SSDT > **테이블 형식 모델 탐색기**에서 **역할**을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  **역할 관리자**에서 **새로 만들기**를 클릭합니다.  
  
3.  Hello 역할에 대 한 이름을 입력 합니다.  
  
     기본적으로 hello 이름 hello 기본 역할의 각 새 역할에 대해 매겨집니다 됩니다. 예를 들어 재무 관리자 또는 인적 자원 전문가 hello 멤버 유형을 분명 하 게 식별 하는 이름을 입력 하는 것이 좋습니다.  
  
4.  다음 권한을 hello 중 하나를 선택 합니다.  
  
    |사용 권한|설명|  
    |----------------|-----------------|  
    |**없음**|멤버는 hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.|  
    |**읽기**|멤버 (행 필터에 기반) 데이터를 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.|  
    |**읽기 및 처리**|멤버는 데이터 (에 따라 행 수준 필터) 및 실행된 처리 및 모두 처리 작업을 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.|  
    |**프로세스**|멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다. Hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.|  
    |**관리자**|멤버는 hello 모델 스키마를 수정 하 고 모든 데이터를 쿼리할 수 있습니다.|   
  
5.  hello 역할 만들기에 대 한 읽기 또는 읽기 및 처리 권한을 DAX 수식을 사용 하 여 행 필터를 추가할 수 있습니다. Hello 클릭 **행 필터** 탭, 다음 테이블을 클릭 한 다음 hello **DAX 필터** 필드를 선택한 다음 DAX 수식을 입력 합니다.
  
6.  **멤버** > **외부 추가**를 클릭합니다.  
  
8.  **외부 멤버 추가**에서 Azure AD 테넌트의 사용자 또는 그룹을 메일 주소로 입력합니다. [확인]을 클릭하고 [역할 관리자]를 닫으면 역할 및 역할 멤버가 [테이블 형식 모델 탐색기]에 나타납니다. 
 
     ![테이블 형식 모델 탐색기의 역할 및 사용자](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Tooyour Azure Analysis Services 서버를 배포 합니다.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd 또는 역할 및 SSMS에서 사용자 관리
역할 및 사용자 tooa tooadd 배포 된 모델 데이터베이스, 서버 관리자 또는 관리자 권한 가진 데이터베이스 역할에 이미 연결 된 toohello 서버 여야 합니다.

1. 개체 탐색기에서 **역할**을 마우스 오른쪽 단추로 클릭 > **새 역할**을 클릭합니다.

2. **역할 만들기**에서 역할 이름 및 설명을 입력합니다.

3. 사용 권한을 선택합니다.
   |사용 권한|설명|  
   |----------------|-----------------|  
   |**모든 권한(관리자)**|구성원 hello 모델 스키마를 수정할 수 있습니다, 처리 하 고 모든 데이터를 쿼리할 수 있습니다.| 
   |**데이터베이스 처리**|멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다. Hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.|  
   |**읽기**|멤버 (행 필터에 기반) 데이터를 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.|  
  
4. **멤버 자격**을 클릭한 다음 Azure AD 테넌트의 사용자나 그룹을 메일 주소로 입력합니다.

     ![사용자 추가](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. 만들려는 hello 역할에 읽기 권한이 있는 경우에 DAX 수식을 사용 하 여 행 필터를 추가할 수 있습니다. 클릭 **행 필터**테이블을 선택 하 고 hello에서 DAX 수식을 입력 합니다 **DAX 필터** 필드입니다. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd 역할 및 TMSL 스크립트를 사용 하 여 사용자
SSMS에서 또는 PowerShell을 사용 하 여 hello XMLA 창에 TMSL 스크립트를 실행할 수 있습니다. 사용 하 여 hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) 명령과 hello [역할](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) 개체입니다.

**샘플 TMSL 스크립트**

이 샘플에서는 B2B 외부 사용자와 그룹 hello SalesBI 데이터베이스에 대 한 읽기 권한 가진 toohello 분석가 역할을 추가 됩니다. 둘 다 hello 외부 사용자 및 그룹 같은 Azure AD 테 넌 트에 있어야 합니다.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd 역할 및 PowerShell을 사용 하 여 사용자
hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) 모듈은 작업 별로 데이터베이스 관리 cmdlet 및 hello 범용 Invoke-ascmd cmdlet 스크립팅 언어 TMSL (Tabular Model) 쿼리 또는 스크립트를 허용 하를 제공 합니다. hello cmdlet을 다음 데이터베이스 역할 및 사용자 관리에 사용 됩니다.
  
|Cmdlet|설명|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Tooa 데이터베이스 역할 구성원을 추가 합니다.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|데이터베이스 역할에서 구성원을 제거합니다.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|TMSL 스크립트를 실행합니다.|

## <a name="row-filters"></a>행 필터  
행 필터는 특정 역할의 멤버가 쿼리할 수 있는 테이블의 행을 정의합니다. 행 필터는 DAX 수식을 사용하여 모델의 각 테이블에 대해 정의됩니다.  
  
행 필터는 읽기와 읽기 및 처리 권한이 있는 역할에 대해서만 정의할 수 있습니다. 기본적으로 특정 테이블에 대 한 행 필터 정의 되지 않은 경우 다른 테이블에서 교차 필터링이 적용 하지 않는 한 멤버 hello 테이블의 모든 행에 쿼리할 수 있습니다.
  
 행 필터 tooa TRUE/FALSE 값, 해당 역할의 멤버가 쿼리할 수 있는 toodefine hello 행을 평가 해야 하는 DAX 수식을 사용 해야 합니다. Hello DAX 수식에에서 포함 되지 않은 행을 쿼리할 수 없습니다. 예를 들어 다음 행 필터 식은 hello로 Customers 테이블을 hello *고객 [Country] = = "미국"*, hello Sales 역할의 멤버인 hello USA의에서 고객만 볼만 수 있습니다.  
  
행 필터 적용 toohello 지정 된 행과 관련 된 행입니다. 테이블에 여러 관계가 있는 경우 필터는 hello는 활성 관계에 대 한 보안을 적용 합니다. 행 필터는 관련 테이블에 대해 정의된 다른 행 필터와 교차됩니다. 예를 들면 다음과 같습니다.  
  
|테이블|DAX 식|  
|-----------|--------------------|  
|지역|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|트랜잭션|=Transactions[Year]=2016|  
  
 hello 순수 효과 멤버를 hello 고객이 hello 미국에, hello 제품 범주, bicycles 이며 hello year가 2016 데이터 행을 쿼리할 수 있습니다. 사용자가 되지 않은 트랜잭션은 자전거나 트랜잭션을 하지 2016에는 이러한 권한을 부여 하는 다른 역할의 멤버가 아닌 hello 미국 이외의 국가에서 발생을 쿼리할 수 없습니다.
  
 Hello 필터를 사용할 수 있습니다 *=FALSE()*, 전체 테이블에 대 한 toodeny 액세스 tooall 행입니다.

## <a name="next-steps"></a>다음 단계
  [서버 관리자 관리](analysis-services-server-admins.md)   
  [PowerShell을 사용하여 Azure Analysis Services 관리](analysis-services-powershell.md)  
  [TMSL(테이블 형식 모델 스크립트 언어) 참조](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

