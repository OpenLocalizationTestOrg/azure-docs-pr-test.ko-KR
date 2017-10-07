---
title: "SQL 커넥터 단계별 aaaGeneric 단계 | Microsoft Docs"
description: "이 문서는 단계별 hello 제네릭 SQL 커넥터를 사용 하 여 단계별 간단한 HR 시스템을 통해."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>일반 SQL 커넥터 단계별 가이드
이 항목은 단계별 가이드입니다. 이 항목에서는 간단한 샘플 HR 데이터베이스를 만들고 이를 사용하여 일부 사용자와 해당 그룹 멤버 자격을 가져옵니다.

## <a name="prepare-hello-sample-database"></a>Hello 예제 데이터베이스를 준비 합니다.
SQL Server를 실행 중인 서버의 hello SQL 스크립트를 실행 [부록 A](#appendix-a)합니다. 이 스크립트는 GSQLDEMO hello 이름의 예제 데이터베이스를 만듭니다. hello에 대 한 hello 개체 모델 생성이 그림의 데이터베이스 같습니다.  
![개체 모델](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

또한 toouse tooconnect toohello 데이터베이스 사용자를 만듭니다. 이 연습에서는 hello 사용자가 FABRIKAM\SQLUser 호출 되 고 hello 도메인에 배치 됩니다.

## <a name="create-hello-odbc-connection-file"></a>Hello ODBC 연결 파일 만들기
일반 SQL 커넥터 hello ODBC tooconnect toohello 원격 서버를 사용 중입니다. 먼저 toocreate hello ODBC 연결 정보로 파일을 해야 합니다.

1. 서버에서 hello ODBC 관리 유틸리티를 시작 합니다.  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. 선택 hello 탭 **파일 DSN**합니다. **추가...**를 클릭합니다.  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. hello 기본적으로 드라이버 works 미세, 따라서 선택 하 고 클릭 **다음 >**합니다.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. 와 같은 hello 파일에 이름을 지정 **GenericSQL**합니다.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. **마침**을 클릭합니다.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. 시간 tooconfigure hello 연결입니다. Hello 데이터 소스를 적절 한 설명을 제공 하 고 SQL Server를 실행 하는 hello 서버 hello 이름을 제공 합니다.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. 방법을 선택 sql tooauthenticate 합니다. 이 예제에서는 Windows 인증을 사용합니다.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Hello 예제 데이터베이스의 hello 이름을 제공 **GSQLDEMO**합니다.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. 이 화면에서는 모든 항목을 기본값으로 유지합니다. **마침**을 클릭합니다.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. 모든 것이 예상 대로 작동 tooverify 클릭 **테스트 데이터 소스**합니다.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Hello 테스트 성공 인지 확인 합니다.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. 이제 hello ODBC 구성 파일 파일 DSN에 표시 됩니다.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Hello 파일을 및 필요 hello 커넥터 만들기를 시작 했습니다.

## <a name="create-hello-generic-sql-connector"></a>Hello 제네릭 SQL 커넥터 만들기
1. Hello 동기화 서비스 관리자 UI에서에서 선택 **커넥터** 및 **만들기**합니다. **일반 SQL(Microsoft)** 을 선택하고 설명이 포함된 이름을 입력합니다.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Hello 이전 섹션에서 만든 hello DSN 파일을 찾아 toohello 서버에 업로드 합니다. Hello 자격 증명 tooconnect toohello 데이터베이스를 제공 합니다.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. 이 연습에서는 작업을 쉽게 하기 위해 **User**와 **Group**이라는 두 개의 개체가 있다고 가정합니다.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. toofind hello 특성 hello 테이블 자체를 보면 커넥터 toodetect 특성 hello 두는 것이 좋습니다. 이후 **사용자** 예약어 tooprovide 사각형에서 대괄호 sql에서 필요 합니다.  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. 시간 toodefine hello 앵커 특성 및 hello DN 특성입니다. 에 대 한 **사용자**, hello 두 특성의 사용자 이름 및 EmployeeID의 hello 조합을 사용 합니다. **Group**의 경우 GroupName(실제로는 현실적이지 않지만 이 연습에서는 작동함)을 사용합니다.
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. 일부 특성 유형은 SQL 데이터베이스에서 검색할 수 없습니다. hello reference-type 특성 특히 할 수 없습니다. Hello 그룹 개체 유형에 대해 toochange hello OwnerID 및 tooreference memberid를 지정 해야합니다.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. hello 이전 단계에서 참조 특성 hello 개체 유형 이러한 값에 대 한 참조는 필요에 따라 hello 특성 선택 합니다. 경우에 hello 사용자 개체 유형입니다.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Hello 글로벌 매개 변수 페이지에서 선택 **워터 마크** hello 델타 전략으로 합니다. 또한 hello 날짜/시간 형식으로 입력 **yyyy-월-일 hh: mm:**합니다.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Hello에 **파티션 구성 및 계층** 페이지에서 두 개체 유형을 선택 합니다.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Hello에 **개체 유형 선택** 및 **특성 선택**, 개체 유형 및 모든 특성을 모두 선택 합니다. Hello에 **앵커 구성** 페이지 **마침**합니다.

## <a name="create-run-profiles"></a>실행 프로필 만들기
1. Hello 동기화 서비스 관리자 UI에서에서 선택 **커넥터**, 및 **실행 프로필 구성**합니다. **새 프로필**을 클릭합니다. **전체 가져오기**를 시작합니다.  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Hello 유형 선택 **전체 가져오기 (스테이지 전용)**합니다.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Hello 파티션을 선택 **개체 = 사용자**합니다.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. **테이블**을 선택하고 **[USERS]**를 입력합니다. Toohello 다중값된 개체 유형 섹션 아래로 스크롤하여 hello 다음 그림에서와 같이 hello 데이터를 입력 합니다. 선택 **마침** toosave hello 단계입니다.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. **새 단계**를 선택합니다. 이번에는 **OBJECT=Group**을 선택합니다. Hello 마지막 페이지에 hello 다음 그림에서와 같이 hello 구성을 사용 합니다. **마침**을 클릭합니다.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. 선택 사항: 원하는 경우 추가 실행 프로필을 구성할 수 있습니다. 이 연습에 대 한 전체 가져오기 hello만 사용 됩니다.
7. 클릭 **확인** toofinish 변경 실행 프로필.

## <a name="add-some-test-data-and-test-hello-import"></a>일부 테스트 데이터 및 테스트 hello 가져오기 추가
샘플 데이터베이스에서 일부 테스트 데이터를 입력합니다. 준비되었으면 **실행** 및 **전체 가져오기**를 선택합니다.

다음은 두 개의 전화 번호가 있는 사용자와 몇 명의 구성원이 있는 그룹입니다.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>부록 A
**SQL 스크립트 toocreate hello 예제 데이터베이스**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
