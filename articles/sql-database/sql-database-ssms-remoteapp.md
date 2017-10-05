---
title: "Azure RemoteApp에서 SQL Server Management Studio를 사용하여 SQL 데이터베이스에 연결 | Microsoft Docs"
description: "이 자습서에서는 SQL 데이터베이스에 연결할 때 보안 및 성능을 위해 Azure RemoteApp에서 SQL Server Management Studio를 사용하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a>Azure RemoteApp에서 SQL Server Management Studio를 사용하여Azure SQL 데이터베이스에 연결

> [!IMPORTANT]
> Azure RemoteApp은 중단될 예정입니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
>

## <a name="introduction"></a>소개
이 자습서에서는 Azure RemoteApp에서 SSMS(SQL Server Management Studio)를 사용하여 SQL 데이터베이스에 연결하는 방법을 보여줍니다. Azure RemoteApp에서 SQL Server Management Studio를 설정하는 과정을 안내하고 이점을 설명하며 Azure Active Directory에서 사용할 수 있는 보안 기능을 보여줍니다.

**예상 완료 시간:** 45분

## <a name="ssms-in-azure-remoteapp"></a>Azure RemoteApp의 SSMS
Azure RemoteApp은 응용 프로그램을 제공하는 Azure의 RDS 서비스입니다. [RemoteApp이란?](../remoteapp/remoteapp-whatis.md)

Azure RemoteApp에서 실행되는 SSMS은 SSMS를 로컬로 실행할 때와 동일한 환경을 제공합니다.

![Azure RemoteApp에서 실행되는 SSMS를 보여주는 스크린 샷][1]

## <a name="benefits"></a>이점
다음을 비롯하여 Azure RemoteApp에서 SSMS를 사용하는 많은 이점이 있습니다.

* Azure SQL Server의 포트 1433은 외부에서(Azure 외부)에 노출될 필요가 없습니다.
* Azure SQL Server 방화벽에서 IP 주소를 계속 추가하고 제거할 필요가 없습니다.
* Azure RemoteApp 연결은 모두 암호화된 원격 데스크톱 프로토콜을 사용하여 포트 443에서 HTTPS를 통해 발생합니다.
* 다중 사용자이며 확장할 수 있습니다.
* SQL 데이터베이스와 동일한 지역에 있는 SSMS에서 성능 향상이 있습니다.
* 사용자 작업 보고서가 있는 Azure Active Directory의 Premium Edition으로 Azure RemoteApp의 사용을 감사할 수 있습니다.
* Multi-Factor Authentication(MFA)을 사용할 수 있습니다.
* iOS, Android, Mac, Windows Phone 및 Windows PC을 포함하는 지원되는 Azure RemoteApp 클라이언트 중 하나를 사용하는 경우 언제든 SSMS를 액세스합니다.

## <a name="create-the-azure-remoteapp-collection"></a>Azure RemoteApp 컬렉션 만들기
SSMS를 사용하여 Azure RemoteApp 컬렉션을 만드는 단계는 다음과 같습니다.

### <a name="1-create-a-new-windows-vm-from-image"></a>1. 이미지에서 새 Windows VM 만들기
갤러리에서 "Windows Server 원격 데스크톱 세션 호스트 Windows Server 2012 R2" 이미지를 사용하여 새 VM을 만듭니다.

### <a name="2-install-ssms-from-sql-express"></a>2. SQL Express에서 SSMS 설치
새 VM으로 이동하고 다음 다운로드 페이지로 이동합니다. [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

SSMS를 다운로드하는 옵션이 있습니다. 다운로드한 후에 설치 디렉터리로 이동하고 SSMS를 설치하려면 설치 프로그램을 실행합니다.

또한 SQL Server 2014 서비스 팩 1을 설치해야 합니다. 다음에서 다운로드할 수 있습니다. [Microsoft SQL Server 2014 Service Pack 1(SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 서비스 팩 1에는 Azure SQL 데이터베이스로 작업하기 위한 중요한 기능이 포함됩니다.

### <a name="3-run-validate-script-and-sysprep"></a>3. 유효성 검사 스크립트 및 Sysprep 실행
VM의 바탕 화면에는 유효성 검사라는 PowerShell 스크립트가 있습니다. 두 번 클릭하여 실행합니다. VM이 응용 프로그램의 원격 호스팅에 사용할 준비가 되었는지 확인합니다. 확인이 완료되면 sysprep을 실행할지 묻습니다. 실행을 선택하세요.

sysprep이 완료되면 VM이 종료됩니다.

Azure RemoteApp 이미지 만들기에 대해 자세히 알아보려면 [Azure에서 RemoteApp 템플릿 이미지를 만드는 방법](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. 이미지 캡처
VM의 실행이 중지될 때 현재 포털에서 찾아서 캡처합니다.

이미지를 캡처하는 방법을 자세히 알아보려면 [클래식 배포 모델을 사용하여 만든 Azure Windows 가상 컴퓨터의 이미지 캡처](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-to-azure-remoteapp-template-images"></a>5. Azure RemoteApp 템플릿 이미지에 추가
현재 포털의 Azure RemoteApp 섹션에서 템플릿 이미지 탭으로 이동하고 추가를 클릭합니다. 팝업 상자에서 "가상 컴퓨터 라이브러리에서 이미지 가져오기"를 선택한 다음 방금 만든 이미지를 선택합니다.

### <a name="6-create-cloud-collection"></a>6. 클라우드 컬렉션 만들기
현재 포털에서 새 Azure RemoteApp 클라우드 컬렉션을 만듭니다. 거기에 설치된 SSMS를 사용하여 가져온 템플릿 이미지를 선택합니다.

![새 클라우드 컬렉션 만들기][2]

### <a name="7-publish-ssms"></a>7. SSMS 게시
새 클라우드 컬렉션의 게시 탭의 시작 메뉴에서 응용 프로그램 게시를 선택하고 목록에서 SSMS를 선택합니다.

![앱 게시][5]

### <a name="8-add-users"></a>8. 사용자 추가
사용자 액세스 탭에서 SSMS 포함하는 Azure RemoteApp 컬렉션에 액세스할 사용자를 선택할 수 있습니다.

![사용자 추가][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a>9. Azure RemoteApp 클라이언트 응용 프로그램 설치
다음에 Azure RemoteApp 클라이언트를 다운로드하고 설치할 수 있습니다. [다운로드 | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Azure SQL Server 구성
필요한 유일한 구성은 Azure 서비스가 방화벽에 설정되도록 하는 것입니다. 이 솔루션을 사용하는 경우 방화벽을 열기 위해 모든 IP 주소를 추가할 필요가 없습니다. SQL Server에 허용되는 네트워크 트래픽은 다른 Azure 서비스에서 가져옵니다.

![Azure 허용][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication(MFA)
MFA는 이 응용 프로그램에 구체적으로 사용될 수 있습니다. Azure Active Directory의 응용 프로그램 탭으로 이동합니다. Microsoft Azure RemoteApp에 대한 항목을 찾습니다. 해당 응용 프로그램을 클릭한 다음 구성하는 경우 이 응용 프로그램에 MFA를 사용하는 아래 페이지가 표시됩니다.

![MFA 사용][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Azure Active Directory Premium으로 사용자 작업 감사
Azure AD Premium이 없는 경우 디렉터리의 라이선스 섹션에서 사용하도록 설정해야 합니다. Premium을 사용하면 Premium 수준에 사용자를 할당할 수 있습니다.

Azure Active Directory에서 사용자에 이동할 때 Azure RemoteApp에 대한 로그인 정보를 보려면 작업 탭으로 이동할 수 있습니다.

## <a name="next-steps"></a>다음 단계
위의 모든 단계를 완료한 후에 Azure RemoteApp 클라이언트를 실행하고 할당된 사용자로 로그인할 수 있습니다. SSMS가 응용 프로그램 중 하나로 나타나고 Azure SQL Server에 액세스할 수 있는 컴퓨터에 설치되어 있는 경우처럼 실행할 수 있습니다.

SQL 데이터베이스에 연결하는 방법에 대한 자세한 내용은 [SQL Server Management Studio로 SQL 데이터베이스에 연결 및 샘플 T-SQL 쿼리 수행](sql-database-connect-query-ssms.md)을 참조하세요.

이게 전부입니다. 마음껏 즐기세요!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png