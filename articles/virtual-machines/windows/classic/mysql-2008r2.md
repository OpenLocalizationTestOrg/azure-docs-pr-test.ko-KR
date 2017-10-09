---
title: "클래식 Azure VM aaaCreate MySQL을 실행 | Microsoft Docs"
description: "Windows Server 2012 r 2를 실행 하는 Azure 가상 컴퓨터를 만들고 hello 클래식 배포 모델을 사용 하 여 MySQL 데이터베이스 hello 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Windows Server 2016을 실행 하는 hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터에서 MySQL을 설치 합니다.
[MySQL](https://www.mysql.com) 은 인기 있는 오픈 소스 SQL 데이터베이스입니다. 이 자습서에서는 어떻게 tooinstall 및 실행 hello **커뮤니티 버전의 MySQL 5.7.18** 실행 가상 컴퓨터에서 MySQL 서버와 **Windows Server 2016**합니다. 다른 버전의 MySQL 또는 Windows Server에서는 작업 단계가 약간 다를 수 있습니다.

Linux에서 MySQL를 설치 하는 방법에 지침은 참조: [어떻게 tooinstall Azure에서 MySQL](../../linux/mysql-install.md)합니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Windows Server 2016을 실행하는 가상 컴퓨터 만들기
Windows Server 2016을 실행 하는 VM이 없는 경우이 사용할 수 있습니다 [자습서](./tutorial.md) toocreate hello 가상 컴퓨터.

## <a name="attach-a-data-disk"></a>데이터 디스크 연결
Hello 가상 컴퓨터를 만든 후 데이터 디스크를 필요에 따라 연결할 수 있습니다. Hello 운영 체제 포함 데이터 디스크는 프로덕션 작업 및 운영 체제 드라이브 (c:) hello에 공간이 부족 tooavoid에 권장를 추가 합니다.

참조 [tooattach 데이터 tooa Windows 가상 컴퓨터 디스크 하는 방법을](../attach-managed-disk-portal.md) 빈 디스크 연결에 대 한 hello 지침을 따릅니다. Hello 호스트 캐시 설정 너무 설정**None** 또는 **읽기 전용**합니다.

## <a name="log-on-toohello-virtual-machine"></a>Toohello 가상 컴퓨터에 로그온
[Toohello 가상 컴퓨터에 로그온](./connect-logon.md) MySQL을 설치할 수 있도록 합니다.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>설치 하 고 MySQL Community 서버 hello 가상 컴퓨터에서 실행
이러한 단계 tooinstall에 따라, 구성 및 hello 커뮤니티 버전의 MySQL Server를 실행 합니다.

> [!NOTE]
> Internet Explorer를 사용 하 여 항목을 다운로드할 때 hello IE를 설정할 수 있습니다 **보안 강화 구성** tooOff, 고 hello 다운로드 프로세스를 단순화 합니다. Hello 시작 메뉴에서 관리 도구/서버 관리자/로컬 서버를 클릭 한 다음 클릭 IE **보안 강화 구성** hello 구성 tooOff 설정).
>
>

1. 원격 데스크톱을 사용 하 여 toohello 가상 컴퓨터를 연결한 후 클릭 **Internet Explorer** hello 시작 화면에서 합니다.
2. 선택 hello **도구** hello 오른쪽 위 모서리 (hello cogged 휠 아이콘) 단추를 선택한 다음 클릭 **인터넷 옵션**합니다. Hello 클릭 **보안** 탭에서 hello **신뢰할 수 있는 사이트** 아이콘을 hello를 클릭 한 다음 **사이트** 단추입니다. 신뢰할 수 있는 사이트 http://*.mysql.com toohello 목록을 추가 합니다. **닫기**를 클릭한 후 **확인**을 클릭합니다.
3. hello 주소 표시줄의 Internet Explorer https://dev.mysql.com/downloads/mysql/를 입력 합니다.
4. MySQL 사이트 toolocate hello를 사용 하 고 hello hello MySQL Windows 용 설치 관리자의 최신 버전을 다운로드 합니다. Hello MySQL 설치 관리자를 선택할 때는 hello 파일 집합 (예를 들어 hello mysql-설치 프로그램-커뮤니티-5.7.18.0.msi 352.8 MB의 파일 크기)를 완료 하 고 hello 설치 관리자를 저장 된 hello 버전을 다운로드 합니다.
5. Hello 설치 관리자 다운로드 완료 되 면 클릭 **실행** toolaunch 설치 합니다.
6. Hello에 **사용권 계약** 페이지 hello 사용권 계약에 동의 하 고 클릭 **다음**합니다.
7. Hello에 **설치 유형을 선택 하면** 페이지에서 클릭 하 고 클릭 hello 설치 유형을 **다음**합니다. hello 다음 단계에서는 가정 hello hello 선택을 **서버만** 설치 유형입니다.
8. 경우 hello **요구 사항 확인** 페이지가 표시를 클릭 **Execute** toolet hello 설치 관리자는 누락 된 구성 요소를 설치 합니다. Hello c + + 재배포 가능 런타임과 같이 표시 하는 지침을 따릅니다.
9. Hello에 **설치** 페이지 **Execute**합니다. 설치가 완료되면 **다음**을 클릭합니다.

10. Hello에 **제품 구성** 페이지 **다음**합니다.

11. Hello에 **유형 및 네트워킹** 페이지에서 원하는 구성 유형 및 연결 옵션, 필요한 경우 hello TCP 포트를 포함 하 여 지정 합니다. **고급 옵션 표시**를 선택하고 **다음**을 클릭합니다.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Hello에 **계정과 역할** 페이지에서 강력한 MySQL 루트 암호를 지정 합니다. 필요에 따라 추가 MySQL 사용자 계정을 추가하고 **다음**을 클릭합니다.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Hello에 **Windows 서비스** 페이지, 필요에 따라 hello MySQL 서버를 Windows 서비스로 실행 하기 위한 변경 toohello 기본 설정을 지정 하 고 클릭 **다음**합니다.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. hello에 대 한 선택 사항 hello **플러그 인 및 확장** 페이지는 선택 사항입니다. 클릭 **다음** toocontinue 합니다.
15. Hello에 **고급 옵션** 페이지, 필요에 따라 변경 내용을 toologging 옵션을 지정 하 고 클릭 **다음**합니다.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Hello에 **서버 구성 적용** 페이지 **Execute**합니다. Hello 구성 단계가 완료 되 면 클릭 **마침**합니다.
17. Hello에 **제품 구성** 페이지 **다음**합니다.
18. Hello에 **설치 완료** 페이지 **복사 로그 tooClipboard** 나중 누른 tooexamine 하려는 경우 **마침**합니다.
19. Hello 시작 화면에서 입력 **mysql**, 클릭 하 고 **MySQL 5.7 명령줄 클라이언트**합니다.
20. 12 단계에서 지정한 hello 루트 암호를 입력 하 고 표시 되는 프롬프트 명령을 tooconfigure MySQL을 실행할 수 있습니다. 명령 및 구문을 hello 세부 정보를 참조 하십시오. [MySQL 참조 설명서](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html)합니다.

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. 또한 기본 hello 및 데이터 디렉터리 및 드라이브와 같은 서버 구성 기본 설정을 구성할 수 있습니다. 자세한 내용은 [6.1.2 서버 구성 기본값](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)을 참조하세요.

## <a name="configure-endpoints"></a>끝점 구성

컴퓨터용 hello MySQL 서비스 toobe 사용 가능한 tooclient hello 인터넷에 hello TCP 포트에 대 한 끝점을 구성 하 고 Windows 방화벽 규칙을 생성 해야 합니다. hello MySQL 클라이언트에 대 한 수신 대기 서비스는 hello MySQL Server에는 기본 포트 값은 3306 합니다. Hello 포트는 hello에 제공 하는 hello 값과 일치으로 다른 포트를 지정할 수 있습니다 **유형 및 네트워킹** (hello 이전 절차의 11 단계) 페이지.

> [!NOTE]
> 프로덕션 용도로 hello를 hello 인터넷에서 MySQL 서버 hello tooall 사용할 수 있는 컴퓨터에 서비스를 만드는 요소의 보안 문제도 고려해. Hello toouse hello 끝점은 액세스 제어 목록 (ACL)를 허용 되는 원본 IP 주소 집합을 정의할 수 있습니다. 자세한 내용은 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](setup-endpoints.md)합니다.
>
>

tooconfigure hello MySQL Server 서비스에 대 한 끝점:

1. Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)**MySQL 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **끝점**합니다.
2. Hello 명령 모음에서 **추가**합니다.
3. Hello에 **끝점 추가** 페이지에 대 한 고유한 이름을 입력 합니다 **이름**합니다.
4. 선택 **TCP** hello 프로토콜로 합니다.
5. 같은 hello 포트 번호를 입력 **3306**, 둘 다에서 **공용 포트** 및 **개인 포트**, 클릭 하 고 **확인**합니다.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Windows 방화벽 규칙 tooallow MySQL 트래픽 추가
hello 다음에서 명령을 실행 하는 hello 인터넷에서에서 MySQL 트래픽을 허용 하는 Windows 방화벽 규칙 tooadd는 _관리자 권한 Windows PowerShell 명령 프롬프트_ hello MySQL 서버 가상 컴퓨터.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>원격 연결 테스트
tootest 여 원격 연결 toohello Azure VM 실행 중인 hello MySQL 서버 서비스, VN hello를 포함 하는 hello 클라우드 서비스의 hello DNS 이름을 제공 해야 합니다.

1. Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)**MySQL server 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **개요**합니다.
2. Hello 가상 컴퓨터 대시보드에서 hello 참고 **DNS 이름** 값입니다. 다음은 예제입니다.

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. MySQL 사용자로의 명령 toolog 다음 hello MySQL 또는 hello MySQL 클라이언트를 실행 하는 로컬 컴퓨터를 실행 합니다.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   예를 들어 MySQL 사용자 이름을 사용 하 여 hello _dbadmin3_ 및 hello _testmysql.cloudapp.net_ hello 가상 컴퓨터에 대 한 DNS 이름, 다음 명령을 hello를 사용 하 여 MySQL을 시작할 수 있습니다.

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>다음 단계
MySQL을 실행에 대 한 더 toolearn 참조 hello [MySQL 설명서](http://dev.mysql.com/doc/)합니다.
