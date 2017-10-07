---
title: Azure Analysis Services aaaManage | Microsoft Docs
description: "어떻게 toomanage Analysis Services에 대해 알아봅니다 Azure의 서버입니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Analysis Services 관리
Azure에서 Analysis Services 서버를 만들면에 일부 바로 tooperform 사용 해야 하는 관리 및 관리 작업 또는 잠시 아래쪽 hello도로 수 있습니다. 예를 들어 서버의 상태를 모니터링 하거나 hello 모델 서버에 액세스할 수 있는 제어 toohello 새로 고침 데이터 처리를 실행 합니다. 일부 관리 작업은 Azure 포털에서만, 일부 다른 작업은 SSMS(SQL Server Management Studio)에서만, 일부 작업은 둘 중 하나에서 수행할 수 있습니다.

## <a name="azure-portal"></a>Azure portal
[Azure 포털](http://portal.azure.com/) 는 여기서 수 생성 하 고 서버를 삭제, 서버 리소스를 모니터링, 크기를 변경 하 고 액세스 tooyour 서버에 있는 사람을 관리할 합니다.  몇 가지 문제가 발생하면 지원 요청을 제출할 수도 있습니다.

![Azure에서 서버 이름 가져오기](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
조직에서 tooa 서버 인스턴스에 연결 하는 것 처럼은 Azure에서 tooyour 서버에 연결 합니다. SSMS에서 다양 한 hello 동일 데이터 처리와 같은 작업 또는 처리 스크립트 만들기, 역할을 관리 및 PowerShell을 사용 하 여 수행할 수 있습니다.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>SSMS 다운로드 및 설치
tooget, 그러면 최신 기능 및 hello 매끄러운 경험이 tooyour Azure Analysis Services 서버에 연결 하는 경우 모든를 hello에 hello 최신 버전의 SSMS 사용 하는 합니다. 

[SQL Server Management Studio를 다운로드합니다](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>SSMS로 tooconnect
 Tooyour 서버 hello 처음으로 연결 하기 전에 SSMS를 사용 하는 경우 사용자 이름을 hello Analysis Services 관리자 그룹에 포함 되어 있는지 확인 합니다. toolearn 더 참조 [서버 관리자](#server-administrators) 이 문서의 뒷부분에 나오는 합니다.

1. 에 연결 하기 전에 tooget hello 서버 이름이 필요 합니다. **Azure 포털** > 서버 > **개요** > **서버 이름**, hello 서버 이름 복사.
   
    ![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. SSMS > **개체 탐색기**에서 **연결** > **Analysis Services**를 클릭합니다.
3. Hello에 **tooServer 연결** 대화 상자, 붙여넣기 hello 서버 이름에 다음에 **인증**, hello 인증 유형을 다음 중 하나를 선택 합니다.
   
    **Windows 인증** toouse Windows 도메인 \ 사용자 이름 및 암호 자격 증명입니다.

    **Active Directory 암호 인증** toouse 조직 계정입니다. 예를 들어 비도메인 가입 컴퓨터에서 연결하는 경우에 이 옵션을 사용합니다.

    **Active Directory 유니버설 인증** toouse [비 대화형 또는 multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md)합니다. 
   
    ![SSMS에서 연결](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>서버 관리자 및 데이터베이스 사용자
Azure Analysis Services에서는 두 가지 유형의 사용자, 서버 관리자 및 데이터베이스 사용자가 있습니다. 두 가지 유형의 사용자 모두 Azure Active Directory에 포함되어야 하며 조직 전자 메일 주소 또는 UPN으로 지정해야 합니다. toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.


## <a name="troubleshooting-connection-problems"></a>연결 문제 해결
연결할 때 문제가 발생 하는 경우 SSMS를 사용 하 여, tooclear hello 로그인 캐시를 할 수 있습니다. 캐시 된 toodisc은 nothing입니다. tooclear hello 캐시 닫기 및 다시 시작 hello 프로세스를 연결합니다. 

## <a name="next-steps"></a>다음 단계
이미 테이블 형식 모델 tooyour 새 서버를 배포 하지 않은 경우 이제는 좋습니다. toolearn 더 참조 [tooAzure Analysis Services 배포](analysis-services-deploy.md)합니다.

모델 tooyour 서버를 배포한 경우에 클라이언트 또는 브라우저를 사용 하 여 준비 tooconnect tooit 것입니다. toolearn 더 참조 [Azure Analysis Services 서버에서 데이터를 가져올](analysis-services-connect.md)합니다.

