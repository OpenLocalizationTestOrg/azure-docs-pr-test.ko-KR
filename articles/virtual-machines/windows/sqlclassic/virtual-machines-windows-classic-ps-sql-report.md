---
title: "aaaUse PowerShell tooCreate VM으로는 기본 모드 보고서 서버 | Microsoft Docs"
description: "이 항목에 설명 하 고 SQL Server Reporting Services 기본 모드 보고서 서버는 Azure 가상 컴퓨터에서의 hello 배포 및 구성을 안내 합니다. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>PowerShell tooCreate는 Azure VM으로는 기본 모드 보고서 서버를 사용 하 여
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

이 항목에 설명 하 고 SQL Server Reporting Services 기본 모드 보고서 서버는 Azure 가상 컴퓨터에서의 hello 배포 및 구성을 안내 합니다. hello 단계에서이 문서는 수동 단계 toocreate hello 가상 컴퓨터와 Windows PowerShell 스크립트를 사용 tooconfigure Reporting Services hello VM에서. hello 구성 스크립트는 HTTP 또는 HTTPs에 대 한 방화벽 포트 열기를 포함 합니다.

> [!NOTE]
> 필요 하지 않은 경우 **HTTPS** hello 보고서 서버의 **2 단계를 건너뛰고**합니다.
> 
> 1 단계에서 hello VM을 만든 후 toohello 섹션 스크립트 tooconfigure hello 보고서 서버 사용 및 HTTP를 이동 합니다. Hello 스크립트를 실행 한 후 hello 보고서 서버가 준비 toouse 합니다.

## <a name="prerequisites-and-assumptions"></a>필수 조건 및 가정
* **Azure 구독**: hello Azure 구독에서 사용할 수 있는 코어 수를 확인 합니다. V M 크기를 권장 하는 hello를 만들면 **A3**, 필요한 **4** 사용 가능한 코어입니다. **A2**의 VM 크기를 사용하는 경우 **2**개의 사용 가능한 코어가 필요합니다.
  
  * hello Azure 클래식 포털에서에서 구독을 tooverify hello 코어 제한을 hello 상단 메뉴에서 왼쪽된 창의 hello 한 다음 클릭 사용 설정을 클릭 합니다.
  * tooincrease hello 코어 할당량, 연락처 [Azure 지원](https://azure.microsoft.com/support/options/)합니다. VM 크기 정보는 [Azure에 대한 가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
* **Windows PowerShell 스크립팅**: hello 항목의 Windows PowerShell 기본 작업 지식이 있다고 가정 합니다. Windows PowerShell을 사용 하는 방법에 대 한 자세한 내용은 hello 다음을 참조 하십시오.
  
  * [Windows Server에서 Windows PowerShell 시작](https://technet.microsoft.com/library/hh847814.aspx)
  * [Windows PowerShell 시작](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>1단계: Azure 가상 컴퓨터 프로비전
1. Azure 클래식 포털 toohello를 찾습니다.
2. 클릭 **가상 컴퓨터** hello 왼쪽된 창에서.
   
    ![Microsoft Azure 가상 컴퓨터](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. **새로 만들기**를 클릭합니다.
   
    ![새 단추](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. **갤러리에서**를 클릭합니다.
   
    ![갤러리의 새 VM](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. 클릭 **SQL Server 2014 RTM Standard – Windows Server 2012 R2** hello 화살표 toocontinue 클릭 하 고 있습니다.
   
    ![다음](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Hello Reporting Services 데이터 기반 구독 기능이 필요 하면 선택 **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**합니다. SQL Server 버전 및 기능 지원에 대 한 자세한 내용은 참조 하십시오. [hello SQL Server 2012 버전에서 지 원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx#Reporting)합니다.
6. Hello에 **가상 컴퓨터 구성** 페이지에서 다음 필드는 hello를 편집 합니다.
   
   * 둘 이상 있는 경우 **버전 릴리스 날짜**, 선택 hello 가장 최신 버전입니다.
   * **가상 컴퓨터 이름**: hello 컴퓨터 이름으로도 사용 됩니다 hello 다음 구성 페이지에서 hello 기본 클라우드 서비스 DNS 이름입니다. hello DNS 이름은 Azure 서비스 hello 고유 해야 합니다. VM에 사용 되는 hello를 설명 하는 컴퓨터 이름으로 hello VM을 구성 하는 것이 좋습니다. 예를 들어 ssrsnativecloud입니다.
   * **계층**: 표준
   * **크기: A3** hello SQL Server 작업에 대 한 VM 크기가 좋습니다. VM이 보고서 서버로 사용 되어, hello 보고서 서버의 작업이 크지 않은 한 VM 크기가 a 2의 충분 한 됩니다. VM 가격 책정 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)을 참조하세요.
   * **새 사용자 이름**: hello 이름을 제공 하는 hello VM에서 관리자 권한으로 생성 됩니다.
   * **새 암호** 및 **확인**. 이 암호 hello 새 관리자 계정을 사용 하 고 강력한 암호를 사용 하는 것이 좋습니다.
   * **다음**을 누릅니다. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Hello 다음 페이지에서 다음 필드는 hello를 편집 합니다.
   
   * **클라우드 서비스**: **새 클라우드 서비스 만들기**를 선택합니다.
   * **클라우드 서비스 DNS 이름**: hello hello VM hello와 연결 된 클라우드 서비스의 공용 DNS 이름입니다. 기본 이름은 hello hello VM 이름에 입력 하는 hello 이름이입니다. Hello 항목의 이후 단계에서 신뢰할 수 있는 SSL 인증서를 만들고 hello DNS 이름이 hello의 hello 값에 사용 되는 다음 "**에 발급**" hello 인증서의 합니다.
   * **지역/선호도 그룹/가상 네트워크**: hello 지역 가장 가까운 tooyour 최종 사용자를 선택 합니다.
   * **저장소 계정**: 자동으로 생성된 저장소 계정을 사용합니다.
   * **가용성 집합**: 없습니다.
   * **끝점** 유지 hello **원격 데스크톱** 및 **PowerShell** 끝점 다음 환경에 따라 HTTP 또는 HTTPS 끝점을 추가 합니다.
     
     * **HTTP**: 기본 공용 및 개인 포트는 hello **80**합니다. 80 이외의 개인 포트를 사용 하는 경우 수정 하는 참고 **$HTTPport = 80** hello http 스크립트에 있습니다.
     * **HTTPS**: 기본 공용 및 개인 포트는 hello **443**합니다. 보안 모범 사례는 toochange hello 개인 포트 하 고 방화벽 및 hello 보고서 서버 toouse hello 개인 포트를 구성 합니다. 끝점에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooSet 가상 컴퓨터와 통신](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다. 443 이외의 포트를 사용 하는 경우 hello 매개 변수를 변경 하는 참고 **$HTTPsport = 443** hello HTTPS 스크립트에서에서 합니다.
   * 다음을 클릭합니다. ![다음](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Hello 마법사의 마지막 페이지 hello hello 기본값을 그대로 두고 **hello VM 에이전트 설치** 선택 합니다. hello이 항목의 단계를 이용 하지 않는 hello VM 에이전트가 있지만이 VM tookeep 하려는 경우 hello VM 에이전트 및 확장 하면 tooenhance 그 CM 합니다.  Hello VM 에이전트에 대 한 자세한 내용은 참조 하십시오. [VM 에이전트 및 확장-1 부](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/)합니다. 실행 하는 hello 기본 설치 된 확장 ad 중 하나는 hello VM 데스크톱에서 표시 하는 hello "BGINFO" 확장, 시스템 정보 같은 내부 ip 주소 및 사용 가능한 드라이브 공간입니다.
9. 완료를 클릭합니다. ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. hello **상태** 의 VM으로 표시 하는 hello **시작 (프로 비전)** hello 프로 비전 프로세스 및으로 표시 하는 동안 **실행** 때 hello VM 프로 비전 되 고 준비 toouse 합니다.

## <a name="step-2-create-a-server-certificate"></a>2단계: 서버 인증서 만들기
> [!NOTE]
> 수 hello 보고서 서버에 HTTPS를 요구 하지 않는 **2 단계를 건너뛰고** toohello 섹션 이동 **스크립트 tooconfigure hello 보고서 서버 및 HTTP를 사용 하 여**합니다. 사용 하 여 hello HTTP 스크립트 tooquickly hello 보고서 서버 및 서버를 준비 toouse 수 hello 보고서를 구성 합니다.

순서 toouse hello VM에서 HTTPS, SSL 인증서를 신뢰할 수 있는 해야합니다. 시나리오에 따라 hello 다음 두 가지 방법 중 하나를 사용할 수 있습니다.

* CA(인증 기관)에서 발급하고 Microsoft에서 신뢰하는 유효한 SSL 인증서. hello CA 루트 인증서는 필수 toobe hello Microsoft 루트 인증서 프로그램을 통해 배포 합니다. 이 프로그램에 대 한 자세한 내용은 참조 [Windows 및 Windows Phone 8 SSL 루트 인증서 프로그램 (회원 Ca)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) 및 [Microsoft 루트 인증서 프로그램 소개 toohello](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx)합니다.
* 자체 서명된 인증서. 자체 서명된 인증서는 프로덕션 환경에 권장되지 않습니다.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse 신뢰할 수 있는 인증 기관 (CA)에서 발급 한 인증서
1. **인증 기관에서 hello 웹 사이트에 대 한 서버 인증서를 요청**합니다. 
   
    요청을 보내는 tooa 인증 기관 또는 toogenerate 온라인 인증 기관에 대 한 인증서 요청 파일 (Certreq.txt) 중 하나가 toogenerate hello 웹 서버 인증서 마법사를 사용할 수 있습니다. 예를 들어 Windows Server 2012의 Microsoft 인증서 서비스입니다. 서버 인증서에서 제공 되는 식별 보증의 hello 수준에 따라 일 tooseveral 수개월 동안 인증 기관 tooapprove hello에 대 한 요청 되며 인증서 파일을 보냅니다. 
   
    서버 인증서를 요청 하는 방법에 대 한 자세한 내용은 hello 다음을 참조 하십시오. 
   
   * [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx) 사용.
   * 보안 도구 tooAdminister Windows Server 2012
     
     [보안 도구 tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > hello **에 발급** 필드 hello의 SSL 인증서 해야 수 hello 동일 hello로 신뢰할 수 있는 **클라우드 서비스 DNS 이름** 에서 사용한 새 VM hello 합니다.

2. **웹 서버 hello에 hello 서버 인증서 설치**합니다. 이 경우 hello 웹 서버는 hello VM 호스트에는 보고서 서버 hello 및 Reporting Services를 구성 하는 경우 이후 단계에서 hello 웹 사이트가 만들어집니다. Hello 인증서 MMC 스냅인을 사용 하 여 hello 웹 서버에 hello 서버 인증서를 설치 하는 방법에 대 한 자세한 내용은 참조 [서버 인증서를 설치](https://technet.microsoft.com/library/cc740068)합니다.
   
    이 항목에서는 tooconfigure hello 보고서 서버에 포함 된 toouse hello 스크립트 hello hello 인증서의 값 **지문** hello 스크립트의 매개 변수로 필요 합니다. Tooobtain hello 인증서의 지문을 hello 하는 방법에 대 한 자세한 내용은 hello 다음 섹션을 참조 하십시오.
3. Hello 서버 인증서 toohello 보고서 서버를 할당 합니다. hello 할당 hello 보고서 서버를 구성할 때 hello 다음 섹션에서 완료 됩니다.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>toouse hello 가상 컴퓨터 자체 서명 된 인증서
자체 서명 된 인증서는 hello VM 프로 비전 된 경우 hello VM에서 작성 되었습니다. hello 인증서 이름은 VM DNS 이름과 hello 이름이 hello에 있습니다. 순서 tooavoid 인증서 오류에 필요할 때 해당 hello 인증서가 VM 자체에 hello 뿐만 아니라 hello 사이트의 모든 사용자가 신뢰할 수 있는 합니다.

1. hello 로컬 VM에서 hello 인증서 tootrust hello 루트 CA 인증서 toohello hello 추가 **신뢰할 수 있는 루트 인증 기관**합니다. hello 다음은 필요한 hello 단계에 대 한 요약입니다. Tootrust CA hello 하는 방법에 대 한 자세한 내용은 참조 하십시오. [서버 인증서를 설치](https://technet.microsoft.com/library/cc740068)합니다.
   
   1. Hello Azure 클래식 포털에서에서 VM hello를 선택 하 고 연결을 클릭 합니다. 브라우저 구성에 따라.rdp 파일 toohello VM을 연결 하기 위한 증명된 toosave 수도 있습니다.
      
       ![tooazure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hello 사용자 VM 이름, 사용자 이름 및 hello VM을 만들 때 구성한 암호를 사용 합니다. 
      
       예를 들어 다음 이미지는 hello, hello VM 이름은 **ssrsnativecloud** hello 사용자 이름이 고 **testuser**합니다.
      
       ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Mmc.exe를 실행합니다. 자세한 내용은 참조 [하는 방법: MMC 스냅인 hello로 인증서 보기](https://msdn.microsoft.com/library/ms788967.aspx)합니다.
   3. Hello 콘솔 응용 프로그램에서 **파일** 메뉴 추가 hello **인증서** 스냅인을 선택 **컴퓨터 계정** 메시지가 표시 되 고 클릭 **다음**.
   4. 선택 **로컬 컴퓨터** toomanage 클릭 하 고 **마침**합니다.
   5. 클릭 **확인** hello를 차례로 확장 하 고 **인증서-개인** 노드와 클릭 **인증서**합니다. hello 인증서 hello VM의 이름과 같은 hello DNS 이름을 지정 하 고 끝나는 **cloudapp.net**합니다. Hello 인증서 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **복사**합니다.
   6. Hello 확장 **신뢰할 수 있는 루트 인증 기관** 노드 마우스 오른쪽 단추로 **인증서** 클릭 하 고 **붙여넣기**합니다.
   7. double toovalidate hello 인증서 아래에서 이름을 클릭 **신뢰할 수 있는 루트 인증 기관** 오류가 없는 고 인증서가 표시 있는지 확인 하십시오. Toouse hello HTTPS 스크립트 tooconfigure hello 보고서 서버에서이 항목에 포함 된 hello 인증서의 값을 hello **지문** hello 스크립트의 매개 변수로 필요 합니다. **tooget hello 지문 값**, hello 다음을 수행 합니다. 섹션에는 PowerShell 샘플 tooretrieve hello 지문도는 [스크립트 tooconfigure hello 보고서 서버와 HTTPS를 사용 하 여](#use-script-to-configure-the-report-server-and-HTTPS)합니다.
      
      1. 예를 들어 ssrsnativecloud.cloudapp.net hello 인증서의 hello 이름을 두 번 클릭 합니다.
      2. Hello 클릭 **세부 정보** 탭 합니다.
      3. 왼쪽 창에서 **지문**. hello 지문 안녕하세요 값 a6 예를 들어 hello 세부 정보 필드에 표시 됩니다 08 3c df f9 0b f7 e3 7 c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.
      4. Hello 지문을 복사 나중에 대 한 hello 값을 저장 하거나 지금 hello 스크립트를 편집 합니다.
      5. (*) Hello 스크립트를 실행 하기 전에 hello 값 쌍 사이의 hello 공백을 제거 합니다. 예를 들어 위 hello 지 문은 a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f는 이제 것입니다.
      6. Hello 서버 인증서 toohello 보고서 서버를 할당 합니다. hello 할당 hello 보고서 서버를 구성할 때 hello 다음 섹션에서 완료 됩니다.

자체 서명 된 SSL 인증서를 사용 하는 경우 hello hello 인증서 이름이 이미 hello VM의 hello 호스트 이름과 일치 합니다. 따라서 hello hello 컴퓨터의 DNS는 이미 전역으로 등록 및 모든 클라이언트에서 액세스할 수 있습니다.

## <a name="step-3-configure-hello-report-server"></a>3 단계: hello 보고서 서버 구성
이 섹션에서는 Reporting Services 기본 모드 보고서 서버로 hello VM을 구성 하는 과정을 안내 합니다. Hello 메서드 tooconfigure hello 보고서 서버를 다음 중 하나를 사용할 수 있습니다.

* Hello 스크립트 tooconfigure hello 보고서 서버를 사용 하 여
* 구성 관리자를 사용 하 여 tooConfigure hello 보고서 서버입니다.

자세한 단계는 hello 섹션을 참조 [연결 toohello 가상 컴퓨터와 시작 hello Reporting Services 구성 관리자](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager)합니다.

**인증 참고:** Windows 인증 hello 권장 되는 인증 방법 이며 hello 기본 Reporting Services 인증입니다. Hello VM에 구성 되어 있는 사용자만 Reporting Services에 액세스할 수 및 tooReporting 서비스 역할을 할당 합니다.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>스크립트 tooconfigure hello 보고서 서버와 HTTP 사용
toouse hello Windows PowerShell 스크립트 tooconfigure hello 보고서 서버에서 전체 hello 단계를 수행 합니다. hello 구성에는 HTTP, HTTPS가 아닌 포함 됩니다.

1. Hello Azure 클래식 포털에서에서 VM hello를 선택 하 고 연결을 클릭 합니다. 브라우저 구성에 따라.rdp 파일 toohello VM을 연결 하기 위한 증명된 toosave 수도 있습니다.
   
    ![tooazure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hello 사용자 VM 이름, 사용자 이름 및 hello VM을 만들 때 구성한 암호를 사용 합니다. 
   
    예를 들어 다음 이미지는 hello, hello VM 이름은 **ssrsnativecloud** hello 사용자 이름이 고 **testuser**합니다.
   
    ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Hello VM에서 엽니다 **Windows PowerShell ISE** 관리자 권한으로 합니다. hello PowerShell ISE는 Windows server 2012에 기본적으로 설치 됩니다. Hello 스크립트 hello ISE에 붙여 넣습니다 하, hello 스크립트를 수정 하 고 hello 스크립트를 실행 수 있도록 하려면 표준 Windows PowerShell 창 대신 ISE hello를 사용 하는 것이 좋습니다.
3. Windows PowerShell ISE에서 클릭 hello **보기** 메뉴를 차례로 클릭 **스크립트 창 표시**합니다.
4. 다음 스크립트를 hello 복사한 hello 스크립트 hello Windows PowerShell ISE 스크립트 창에 붙여 넣습니다.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. 80 이외의 HTTP 포트를 사용 하 여 hello VM을 만든 경우 수정 hello 매개 변수 $HTTPport = 80입니다.
6. hello 스크립트는 현재 Reporting Services에 대해 구성 됩니다. Reporting Services에 대해 toorun hello 스크립트를 원하는 경우 hello 경로 toohello 네임 스페이스의 hello 버전 부분을 너무 수정할 "v11" hello Get-wmiobject 문의 합니다.
7. Hello 스크립트를 실행 합니다.

**유효성 검사**: hello 기본 보고서 서버 기능이 작동 하는지 tooverify 참조 hello [확인 hello 구성](#verify-the-configuration) 이 항목의 뒷부분에 나오는 섹션.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>스크립트 tooconfigure hello 보고서 서버 및 HTTPS를 사용 하 여
toouse Windows PowerShell tooconfigure hello 보고서 서버에서 전체 hello 단계를 수행 합니다. hello 구성은 HTTP가 아닌 HTTPS를 포함합니다.

1. Hello Azure 클래식 포털에서에서 VM hello를 선택 하 고 연결을 클릭 합니다. 브라우저 구성에 따라.rdp 파일 toohello VM을 연결 하기 위한 증명된 toosave 수도 있습니다.
   
    ![tooazure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hello 사용자 VM 이름, 사용자 이름 및 hello VM을 만들 때 구성한 암호를 사용 합니다. 
   
    예를 들어 다음 이미지는 hello, hello VM 이름은 **ssrsnativecloud** hello 사용자 이름이 고 **testuser**합니다.
   
    ![로그인에 VM 이름 포함](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Hello VM에서 엽니다 **Windows PowerShell ISE** 관리자 권한으로 합니다. hello PowerShell ISE는 Windows server 2012에 기본적으로 설치 됩니다. Hello 스크립트 hello ISE에 붙여 넣습니다 하, hello 스크립트를 수정 하 고 hello 스크립트를 실행 수 있도록 하려면 표준 Windows PowerShell 창 대신 ISE hello를 사용 하는 것이 좋습니다.
3. tooenable hello 다음 Windows PowerShell 명령을 실행 하는 스크립트 실행:
   
        Set-ExecutionPolicy RemoteSigned
   
    Hello tooverify hello 정책에 따라 실행할 수 있습니다.
   
        Get-ExecutionPolicy
4. **Windows PowerShell ISE**, hello 클릭 **보기** 메뉴를 차례로 클릭 **스크립트 창 표시**합니다.
5. 다음 스크립트를 hello Windows PowerShell ISE 스크립트 창에 붙여 hello를 복사 합니다.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Hello 수정 **$certificatehash** hello 스크립트의 매개 변수:
   
   * 이는 **필수** 매개 변수입니다. Hello 이전 단계에서 hello 인증서 값을 저장 하지 않은 경우 hello hello 인증서 지 문에서 메서드 toocopy hello 인증서 해시 값을 다음 중 하나를 사용 합니다.:
     
       Hello VM에서 Windows PowerShell ISE를 열고 hello 다음 명령을 실행 합니다.
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       hello 출력은 유사한 toohello 다음 표시 됩니다. 예를 들어 구성 된 인증서 hello 스크립트에서 빈 줄을 반환 하는 경우 VM hello가 없습니다 hello 섹션을 참조 하십시오. [toouse hello 가상 컴퓨터 자체 서명 된 인증서](#to-use-the-virtual-machines-self-signed-certificate)합니다.
     
     또는
   * Hello mmc.exe VM에서 실행 되 고 다음 hello 추가 **인증서** 스냅인.
   * Hello에서 **신뢰할 수 있는 루트 인증 기관** 노드 인증서 이름을 두 번 클릭 합니다. Hello hello VM의 자체 서명 된 인증서를 사용 하는 경우 hello 인증서 hello VM의 이름과 같은 hello DNS 이름을 지정 하 고 끝나야 **cloudapp.net**합니다.
   * Hello 클릭 **세부 정보** 탭 합니다.
   * 왼쪽 창에서 **지문**. 예를 들어 af 11 60 b6 4b 28 8 d 89 0a hello 세부 정보 필드에 표시 hello 값 hello 손도장을 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Hello 스크립트를 실행 하기 전에**, hello 값 쌍 사이의 hello 공백을 제거 합니다. 예를 들어 af1160b64b288d890a8212ff6ba9c3664f319048입니다.
7. Hello 수정 **$httpsport** 매개 변수: 
   
   * 포트 443을 사용 하는 hello HTTPS 끝점에 대 한 경우 다음 불필요 tooupdate hello 스크립트에서이 매개 변수입니다. 그렇지 않으면 hello VM에서 hello HTTPS 개인 끝점을 구성할 때 선택한 hello 포트 값을 사용 합니다.
8. Hello 수정 **$DNSName** 매개 변수: 
   
   * hello 스크립트 $DNSName 와일드 카드 인증서에 대해 구성 된 = "+". 와일드 카드 인증서 바인딩에 대 한 원하는 tooconfigure 하지 않으면 $DNSName 주석 = "+"및 줄, hello 전체 $DNSNAme 참조, # # $DNSName="$server.cloudapp.net 다음 hello를 사용 하도록 설정" 합니다.
     
       Reporting Services에 대 한 toouse hello 가상 컴퓨터의 DNS 이름을 하지 않을 경우 hello $DNSName 값을 변경 합니다. Hello 매개 변수를 사용 하는 경우 hello 인증서가이 이름을 사용 해야 하 고 DNS 서버에 전체적으로 hello 이름이 등록 합니다.
9. hello 스크립트는 현재 Reporting Services에 대해 구성 됩니다. Reporting Services에 대해 toorun hello 스크립트를 원하는 경우 hello 경로 toohello 네임 스페이스의 hello 버전 부분을 너무 수정할 "v11" hello Get-wmiobject 문의 합니다.
10. Hello 스크립트를 실행 합니다.

**유효성 검사**: hello 기본 보고서 서버 기능이 작동 하는지 tooverify 참조 hello [확인 hello 구성](#verify-the-connection) 이 항목의 뒷부분에 나오는 섹션. tooverify hello 인증서 바인딩을 관리자 권한으로 명령 프롬프트를 열고 하 고 다음 명령을 hello를 실행 하십시오.

    netsh http show sslcert

hello 결과 hello 다음을 포함 됩니다.

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>구성 관리자를 사용 하 여 tooConfigure hello 보고서 서버
Toorun hello PowerShell 스크립트 tooconfigure hello 보고서 서버 하지 않을 경우이 서버에 있는 섹션 toouse hello Reporting Services 기본 모드 구성 관리자 tooconfigure hello 보고서 hello 단계를 수행 합니다.

1. Hello Azure 클래식 포털에서에서 VM hello를 선택 하 고 연결을 클릭 합니다. Hello 사용자 이름 및 hello VM을 만들 때 구성한 암호를 사용 합니다.
   
    ![tooazure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Windows update를 실행 하 고 업데이트 toohello VM을 설치 합니다. Hello VM의 다시 시작이 필요한 경우 hello VM을 다시 시작 하 고 hello Azure 클래식 포털에서에서 VM toohello 다시 연결 합니다.
3. Hello VM에 hello 시작 메뉴에서 입력 **Reporting Services** 엽니다 **Reporting Services 구성 관리자**합니다.
4. Hello에 대 한 기본값을 유지 **서버 이름** 및 **보고서 서버 인스턴스**합니다. **Connect**를 클릭합니다.
5. Hello 왼쪽된 창에서 클릭 **웹 서비스 URL**합니다.
6. 기본적으로 RS는 IP가 “모두 할당됨"으로 HTTP 포트 80에 대해 구성됩니다. tooadd HTTPS:
   
   1. **SSL 인증서**: 선택 hello 인증서 toouse, 예를 들어 [VM name]. cloudapp.net에 합니다. Hello 섹션을 참조 하는 경우 인증서가 목록 **2 단계: 서버 인증서 만들기** 어떻게 tooinstall와 신뢰 hello hello VM에 인증서에 대 한 내용은 합니다.
   2. **SSL 포트**에서: 443을 선택합니다. 다른 개인 포트로 VM hello hello HTTPS 개인 끝점을 구성한 경우 여기 해당 값을 사용 합니다.
   3. 클릭 **적용** hello 작업 toocomplete 될 때까지 기다립니다.
7. Hello 왼쪽된 창에서 클릭 **데이터베이스**합니다.
   
   1. **데이터베이스 변경**을 클릭합니다.
   2. **새 보고서 서버 데이터베이스 만들기**를 클릭한 후 **다음**을 클릭합니다.
   3. Hello 기본값을 사용 **서버 이름**: hello VM으로 이름을 지정 하 고 기본값을 hello **인증 유형** 으로 **현재 사용자** – **통합보안**. **다음**을 누릅니다.
   4. Hello 기본 둡니다 **데이터베이스 이름** 으로 **ReportServer** 클릭 **다음**합니다.
   5. Hello 기본 둡니다 **인증 유형** 으로 **서비스 자격 증명** 클릭 **다음**합니다.
   6. 클릭 **다음** hello에 **요약** 페이지.
   7. Hello 구성이 완료 되 면 클릭 **마침**합니다.
8. Hello 왼쪽된 창에서 클릭 **보고서 관리자 URL**합니다. Hello 기본 둡니다 **가상 디렉터리** 으로 **보고서** 클릭 **적용**합니다.
9. 클릭 **종료** tooclose hello Reporting Services 구성 관리자.

## <a name="step-4-open-windows-firewall-port"></a>4단계: Windows 방화벽 포트 열기
> [!NOTE]
> Hello 스크립트 tooconfigure hello 보고서 서버 중 하나를 사용 하는 경우에이 섹션을 건너뛸 수 있습니다. hello 스크립트 단계 tooopen hello 방화벽 포트를 포함 합니다. hello 기본 포트 80에 HTTP 및 HTTPS에 포트 443 했습니다.
> 
> 

tooconnect 원격으로 tooReport 관리자 또는 hello 보고서 서버 hello 가상 컴퓨터, TCP 끝점 hello VM에 필요 합니다. 이 동일한 hello VM의 방화벽에서 포트 필요한 tooopen hello입니다. hello VM 프로 비전 된 경우 hello 끝점을 만들었습니다.

이 섹션에서는 tooopen 방화벽 포트를 hello 하는 방법에 기본 정보를 제공 합니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Hello 스크립트 tooconfigure hello 보고서 서버를 사용 하는 경우에이 섹션을 건너뛸 수 있습니다. hello 스크립트 단계 tooopen hello 방화벽 포트를 포함 합니다.
> 
> 

Https의 경우 443 이외의 개인 포트를 구성한 경우 다음 스크립트를 적절 하 게 hello를 수정 합니다. tooopen 포트 **443** hello Windows 방화벽에 hello 다음을 수행 합니다.

1. 관리자 권한으로 Windows PowerShell 창을 엽니다.
2. 를 hello VM에서 hello HTTPS 끝점을 구성할 때 443 이외의 포트를 사용 하는 경우 다음 명령을 hello에 hello 포트를 업데이트 하 고 hello 명령을 실행 하십시오.
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Hello 명령이 완료 되 면 **확인** hello 명령 프롬프트에 표시 됩니다.

tooverify hello 포트를 열면 Windows PowerShell 창을 열고 다음 명령이 실행된 hello:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Hello 구성 확인
hello 기본 보고서 서버 기능이 이제 작동을 tooverify 관리자 권한을 가진 브라우저를 열고 한 다음 찾아보기 toohello 다음 보고 서버 보고서 관리자 URL:

* VM hello toohello 보고서 서버 URL을 찾습니다.
  
        http://localhost/reportserver
* VM hello toohello 보고서 관리자 URL을 찾습니다.
  
        http://localhost/Reports
* 로컬 컴퓨터에서 toohello 찾아보기 **원격** hello VM에서 보고서 관리자입니다. 다음 예제를 적절 하 게 hello에서 hello DNS 이름을 업데이트 합니다. 암호에 대 한 메시지가 표시 되 면 hello VM 준비 되었을 때 만든 hello 관리자 자격 증명을 사용 합니다. hello 사용자 이름은 [Domain] hello\[사용자 이름] 여기서 hello은 hello VM 컴퓨터 이름, 예를 들어 ssrsnativecloud\testuser 형식입니다. HTTP를 사용 하지 않는 경우**S**, hello 제거 **s** hello url에서입니다. VM에서 추가 사용자를 만드는 방법에 hello 내용은 다음 섹션을 참조 하십시오.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* 로컬 컴퓨터에서 toohello 원격 보고서 서버 URL을 찾습니다. 다음 예제를 적절 하 게 hello에서 hello DNS 이름을 업데이트 합니다. HTTPS를 사용 하지 않는 경우 hello s hello URL에서 제거 합니다.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>사용자 만들기 및 역할 할당
구성 하 고 hello 확인 보고서 서버는 일반적인 관리 작업 toocreate 여러 사용자에 게는 고 사용자 tooReporting 서비스 역할을 할당 합니다. 자세한 내용은 hello 다음을 참조 하십시오.

* [로컬 사용자 계정 만들기](https://technet.microsoft.com/library/cc770642.aspx)
* [보고서 서버 (보고서 관리자) 사용자 액세스 권한 부여 tooa](https://msdn.microsoft.com/library/ms156034.aspx))
* [역할 할당 만들기 및 관리](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate 및 보고서 게시 toohello Azure 가상 컴퓨터
hello 다음 표에 요약 되어 hello 옵션 사용 가능한 toopublish hello Microsoft Azure 가상 컴퓨터에서 호스트 되는 온-프레미스 컴퓨터 toohello 보고서 서버에서 기존 보고서의 일부:

* **RS.exe 스크립트**:에서 사용 하 여 RS.exe 스크립트 toocopy 보고서 항목 및 기존 보고서 서버는 Microsoft Azure 가상 컴퓨터를 tooyour 합니다. 자세한 내용은 hello "기본 모드 tooNative 모드-Microsoft Azure 가상 컴퓨터" 섹션의 참조 [샘플 Reporting Services rs.exe 스크립트 tooMigrate 보고서 서버 간 콘텐츠](https://msdn.microsoft.com/library/dn531017.aspx)합니다.
* **보고서 작성기**: hello 가상 컴퓨터 포함 hello 클릭-Microsoft SQL Server 보고서 작성기의 버전에 한 번입니다. toostart 보고서 작성기 hello hello 가상 컴퓨터에 처음으로:
  
  1. 관리자 권한으로 브라우저를 시작합니다.
  2. Tooreport 관리자 hello 가상 컴퓨터를 찾아 클릭 **보고서 작성기** hello 리본 메뉴의 합니다.
     
     자세한 내용은 [보고서 작성기 설치, 제거 및 지원](https://technet.microsoft.com/library/dd207038.aspx)을 참조하세요.
* **SQL Server Data Tools: VM**: SQL Server 2012를 사용 하 여 hello VM을 만든 경우 SQL Server Data Tools hello 가상 컴퓨터에 설치 하 고 사용 하는 toocreate 수 **보고서 서버 프로젝트** 및 가상 hello에 대 한 보고서 컴퓨터입니다. SQL Server Data Tools는 hello hello 가상 컴퓨터에서 toohello 보고서 서버 보고서를 게시할 수 있습니다.
  
    SQL server 2014 사용 하 여 hello VM을 만든 경우에 SQL Server 데이터 도구-visual Studio 용 BI를 설치할 수 있습니다. 자세한 내용은 hello 다음을 참조 하십시오.
  
  * [Microsoft SQL Server Data Tools - Visual Studio 2013용 비즈니스 인텔리전스](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Visual Studio 2012용 비즈니스 인텔리전스](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SSDT-BI(SQL Server Data Tools 및 SQL Server Business Intelligence)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools: 원격**: 로컬 컴퓨터에서 SQL Server Data Tools로 Reporting Services 보고서가 포함된 Reporting Services 프로젝트를 만듭니다. Hello 프로젝트 tooconnect toohello 웹 서비스 URL을 구성 합니다.
  
    ![SSRS 프로젝트의 SSDT 프로젝트 속성](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **스크립트를 사용 하 여**: 스크립트 toocopy 보고서 서버 콘텐츠를 사용 합니다. 자세한 내용은 참조 [샘플 Reporting Services rs.exe 스크립트 tooMigrate 보고서 서버 간 콘텐츠](https://msdn.microsoft.com/library/dn531017.aspx)합니다.

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>VM hello를 사용 하지 않는 경우의 비용 최소화
> [!NOTE]
> hello Azure 클래식 포털에서에서 VM hello toominimize 요금에 대 한 Azure 가상 컴퓨터 사용에 없는 경우 종료 합니다. Hello VM 아래로 VM tooshut 내 hello Windows 전원 옵션을 사용 하는 경우 계속 요금이 청구 되므로 hello hello VM에 대 한 amount 동일 합니다. tooreduce 요금이 tooshut hello Azure 클래식 포털에서에서 VM hello 다운 해야 합니다. VM hello를 더 이상 필요 하면 toodelete hello VM을 기억 하 고 연결 된.vhd 파일 tooavoid 저장소 비용은 hello 합니다. 자세한 내용은에 hello FAQ 섹션을 참조 하십시오. [가상 컴퓨터 가격 정보](https://azure.microsoft.com/pricing/details/virtual-machines/)합니다.

## <a name="more-information"></a>추가 정보
### <a name="resources"></a>리소스
* 비슷한 내용을 tooa 단일 서버 배포와 관련 된 SQL Server Business Intelligence 및 SharePoint 2013의 참조 [Windows PowerShell을 사용 하 여 tooCreate는 Azure VM SQL Server BI 및 SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx)합니다.
* SQL Server Business Intelligence 및 SharePoint 2013의 다중 서버 배포 참조에 대 한 유사 콘텐츠 관련된 tooa [SQL Server Business Intelligence 배포 Azure 가상 컴퓨터의](https://msdn.microsoft.com/library/dn321998.aspx)합니다.
* 일반 정보에 대 한 Azure 가상 컴퓨터의 SQL Server Business Intelligence의 관련된 toodeployments 참조 [Azure 가상 컴퓨터의 SQL Server Business Intelligence](virtual-machines-windows-classic-ps-sql-bi.md)합니다.
* Azure 컴퓨팅 요금의 비용 hello에 대 한 자세한 내용은 참조의 가상 컴퓨터 탭 hello [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines)합니다.

### <a name="community-content"></a>커뮤니티 콘텐츠
* 참조에 대 한 단계별 지침은 어떻게 toocreate Reporting Services 기본 모드 보고서 서버 스크립트를 사용 하지 않고, [호스팅 SQL 보고 서비스에서 Azure 가상 컴퓨터](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html)합니다.

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Azure Vm에서 SQL Server에 대 한 링크 tooother 리소스
[Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

