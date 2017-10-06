---
title: "Azure RemoteApp을 사용 하 여 Azure aaaSQL | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure RemoteApp을 사용 하 여 SQL Azure입니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>Azure RemoteApp을 사용하는 SQL Azure 
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

고객이 선택 toohost Windows 응용 프로그램에서 Azure RemoteApp hello 클라우드의 경우도 전체 클라우드 배포에 대 한 예: SQL 서버 hello에 데이터를 클라우드 toomigrate 또한 합니다. 그러면 Azure RemoteApp을 사용하여 어디서나 언제든지 장치에서 액세스할 수 있는 전체 클라우드 호스팅 솔루션이 가능합니다. 다음은 링크 및 참조 지침 toohelp 함께 하면이 프로세스와 합니다.  

## <a name="migrate-your-sql-data"></a>SQL 데이터 마이그레이션
로 시작 [SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](../sql-database/sql-database-cloud-migrate.md)합니다. 

## <a name="configure-azure-remoteapp"></a>Azure RemoteApp 구성
Azure RemoteApp에서 Windows 응용 프로그램을 호스트합니다. 다음은 단계별로 매우 높은 수준입니다.

1. Hello 만들기 [Azure RemoteApp 템플릿 VM](remoteapp-imageoptions.md)합니다. 
2. Hello VM에 필요한 hello 응용 프로그램을 설치 합니다.
3. SQL DB toohello 연결 되므로 hello 응용 프로그램을 구성 하 고 작동 하는지 확인 합니다.
4. Sysprep 및 종료 hello VM입니다. Azure와 함께 사용하기 위해 이미지 형식으로 캡처합니다. **참고:** tooensure hello 신청이 hello sysprep 프로세스를 통해 수 tooretain hello DB 연결 정보가 필요 합니다. Hello 응용 프로그램 toocheck tooengage hello 공급 업체를 할 수 없습니다 tooretain hello DB 연결 정보가 hello 응용 프로그램을 사용 하는 경우 어떻게 hello 연결 문자열을 지정할 수 있습니다.
5. 위치 선택 하 고 hello 적절 한 지리적 SQL Azure 배포에 있는 Azure RemoteApp 라이브러리로 hello 사용자 지정 이미지를 가져옵니다. 
6. 동일한 데이터 센터 템플릿 위에 hello를 사용 하 여 SQL Azure 배포로와 hello 응용 프로그램을 게시 하는 hello에 RemoteApp 컬렉션을 배포 합니다. Hello에 Azure RemoteApp을 배포 hello 가장 빠른 연결 속도 및 대기 시간을 줄일 SQL Azure 배포와 동일한 데이터 센터 하도록 할 수 있습니다. 

## <a name="app-and-sql-configuration-considerations"></a>앱 및 SQL 구성 고려 사항
SQL Azure RemoteApp과 함께 사용 하는 경우 지점 tooconsider 몇 가지 있습니다.

자세한 내용은 [tooconfigure Azure SQL 데이터베이스 방화벽](../sql-database/sql-database-firewall-configure.md)합니다. 발췌 한 구문을 hello 문서 상태의 "처음에 모든 액세스 tooyour Azure SQL 데이터베이스 서버는 방화벽에 의해 차단 hello 합니다. Azure SQL 데이터베이스 서버를 사용 하 여 순서 toobegin, toohello 클래식 포털을 이동 하 고 액세스 tooyour Azure SQL 데이터베이스 서버를 사용할 수 있는 하나 이상의 서버 수준 방화벽 규칙을 지정 해야 합니다. Hello 방화벽 규칙 toospecify 인터넷 허용 hello에서 어떤 IP 주소 범위를 사용 하 여 및 여부 Azure 응용 프로그램 tooconnect tooyour Azure SQL 데이터베이스 서버를 시도할 수 있습니다. "

또한 tooconnect tooyour 데이터베이스 서버 hello 인터넷에서에서 시도 하는 컴퓨터, hello 방화벽 시작 IP 주소를 서버 수준 중 일부만 hello에 대 한 hello 요청의 hello 확인 (필요한 경우) 및 데이터베이스 수준 방화벽 규칙입니다. "Hello 요청의 hello IP 주소 중 한 hello 서버 수준 방화벽 규칙에 지정 된 hello 범위 내에 있으면 hello 연결이 승인 됩니다 tooyour Azure SQL 데이터베이스 서버입니다." 따라서 개별 원본 IP 주소 뿐만 아니라 IP 범위를 사용할 수 있습니다.

Hello 단계별 지침에 따라 [하는 방법: hello Azure 포털을 사용 하 여 SQL 데이터베이스에서 방화벽 설정 구성](../sql-database/sql-database-configure-firewall-settings.md) toospecify hello IP 범위. Hello SQL 방화벽 규칙을 구성 하는 hello Azure RemoteApp 컬렉션에 지정 된 hello 서브넷의 hello IP 범위를 지정 하십시오. 동적으로-할당 된 IP 주소가 없지만 tooconnect toohello SQL DB hello ARA 서버 사용 해야이 있습니다.

## <a name="troubleshooting"></a>문제 해결
Hello 발생 tooa SQL 연결 하는 Azure RemoteApp에서 호스팅되는 클라이언트 응용 프로그램을 사용 하 여 Azure에서 호스팅되는 위치를 데이터베이스 또는 온-프레미스 느리게 있을 수 있는 몇 가지 이유 이유는 합니다.  

* 장치 tooAzure에서 네트워크 대기 시간이 깁니다. 최상의 성능을 위해 수 toohello 가장 쉽고 빠르게 네트워크 연결을 이동 합니다. 사용 하 여 [azurespeed.com](http://azurespeed.com/) 일반 도구 tootest으로 장치 대기 시간 tooAzure 데이터 센터입니다.  
* Azure RemoteApp에서 호스팅되는 클라이언트 앱은 부하가 높습니다. Premium 청구와 같은 다른 요금제를 선택하면 성능이 향상됩니다. 또 다른 방법은 toomonitor hello 리소스 응용 프로그램를 소비 하는 것입니다: 활성 세션 동안 SAS 화면 작업 관리자를 선택 하 고 앱에 대 한 리소스 사용률을 관찰 하는 hello 시작 됩니다는 ctrl alt 간 키 시퀀스를 수행 합니다.
* SQL Server은 부하가 많거나 최적화되지 않습니다. 문제 해결에 대한 SQL 지침을 따릅니다. 

