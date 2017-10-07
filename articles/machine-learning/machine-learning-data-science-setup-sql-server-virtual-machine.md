---
title: "IPython 노트북 서버와 SQL Server 가상 컴퓨터를 aaaSet | Microsoft Docs"
description: "SQL Server 및 IPython 서버를 사용하여 데이터 과학 가상 컴퓨터를 설정합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook으로 설정
이 항목에서는 방법을 tooprovision 및 클라우드 기반 데이터 과학 환경의 일부로 사용 하는 SQL Server 가상 컴퓨터 toobe를 구성 합니다. IPython 노트북, Azure 저장소 탐색기, AzCopy를 뿐 아니라 데이터 과학 프로젝트에 유용한 기타 유틸리티와 같은 도구를 지 원하는 hello Windows 가상 컴퓨터 구성 됩니다. Azure 저장소 탐색기 및 AzCopy를 예를 들어 편리 하 게 방법 tooupload 데이터 저장소를 제공할 tooAzure blob에서 로컬 컴퓨터 또는 toodownload 것 tooyour blob 저장소에서 로컬 컴퓨터입니다.

hello Azure 가상 컴퓨터 갤러리에는 Microsoft SQL Server가 포함 된 몇 가지 이미지가 포함 됩니다. 데이터 요구 사항에 적합한 SQL Server VM 이미지를 선택하세요. 권장 이미지는 다음과 같습니다.

* 작은 toomedium 데이터 크기에 대 한 SQL Server 2012 SP2 Enterprise
* SQL Server 2012 SP2 Enterprise 작업용으로 최적화 된 데이터 웨어하우징 큰 toovery 큰 데이터 크기에 대 한
  
  > [!NOTE]
  > SQL Server 2012 SP2 Enterprise 이미지에는 **데이터 디스크가 포함되어 있지 않습니다**. Tooadd 필요 하거나 하나 이상의 가상 하드 디스크 toostore 데이터 연결 합니다. Azure 가상 컴퓨터를 만들면 hello 매핑된 운영 체제 toohello C 드라이브에 대 한 디스크와 임시 디스크 매핑된 toohello D 드라이브에 있습니다. Hello D 드라이브 toostore 데이터를 사용 하지 마십시오. Hello 이름에서 알 수 있듯이 임시 저장소만 제공 합니다. Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.
  > 
  > 

## <a name="Provision"></a>Azure 클래식 포털 toohello 연결 하는 SQL Server 가상 컴퓨터를 프로 비전
1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/) 계정을 사용 합니다.
   Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.
2. Hello hello 웹 페이지의 왼쪽 아래에 hello Azure 클래식 포털에서 클릭 **+ 새로 만들기**, 클릭 **계산**, 클릭 **가상 컴퓨터**, 클릭 하 고 **FROM 갤러리**합니다.
3. Hello에 **가상 컴퓨터를 만들** 페이지 데이터 요구 사항에 따라 SQL Server를 포함 하는 가상 컴퓨터 이미지를 선택 하 고 hello hello 페이지의 오른쪽 맨 아래에 다음 화살표를 클릭 합니다. Hello에 hello 최신 정보는 Azure에서 SQL Server 이미지를 지원, 참조 [Azure 가상 컴퓨터의 SQL Server 시작](http://go.microsoft.com/fwlink/p/?LinkId=294720) hello에 대 한 항목 [Azure 가상 컴퓨터의 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719) 설명서 집합입니다.
   
   ![SQL Server VM 선택][1]
4. Hello에 첫 번째 **가상 컴퓨터 구성** 페이지에서 다음 정보를 제공 합니다.
   
   * **가상 컴퓨터 이름**을 입력합니다.
   * Hello에 **새 사용자 이름** 상자 hello VM 로컬 관리자 계정에 대 한 고유한 사용자 이름을 입력 합니다.
   * Hello에 **새 암호** 상자에 강력한 암호를 입력 합니다. 자세한 내용은 [강력한 암호](http://msdn.microsoft.com/library/ms161962.aspx)를 참조하십시오.
   * Hello에 **암호 확인** 상자 hello 암호를 다시 입력 합니다.
   * 적절 한 선택 hello **크기** hello에서 드롭 다운 목록입니다.
     
     > [!NOTE]
     > hello 크기 hello 가상 컴퓨터의 프로 비전 중에 지정 된: a 2는 hello 프로덕션 작업에 권장 되는 가장 작은 크기입니다. SQL Server Enterprise Edition을 사용할 경우 가상 컴퓨터의 최소 권장 크기는 A3입니다. SQL Server Enterprise Edition을 사용할 경우 A3 이상을 선택합니다. 트랜잭션 작업 이미지에 최적화된 SQL Server 2012 또는 2014 Enterprise를 사용할 때는 A4를 선택합니다.
     > 데이터 웨어하우스 작업 이미지에 최적화된 SQL Server 2012 또는 2014 Enterprise를 사용할 때는 A7을 선택합니다. 데이터 디스크를 구성할 수 있습니다 수를 제한 하는 hello 크기를 선택 합니다. Tooa 가상 컴퓨터를 연결할 수 있는 사용 가능한 가상 컴퓨터 크기 및 데이터 디스크 개수 hello에 최신 정보를 참조 하십시오. [Azure 위한 가상 컴퓨터 크기](http://msdn.microsoft.com/library/azure/dn197896.aspx)합니다. 가격 책정 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)을 참조하세요.
     > 
     > 
   
   Hello hello 맨 아래 오른쪽 toocontinue에서 다음 화살표를 클릭 합니다.
   
   ![VM 구성][2]
5. Hello에 두 번째 **가상 컴퓨터 구성** 페이지 네트워킹, 저장소 및 가용성에 대 한 리소스를 구성 합니다.
   
   * Hello에 **클라우드 서비스** 상자 **새 클라우드 서비스를 만들**합니다.
   * Hello에 **클라우드 서비스 DNS 이름** 상자 부분을 제공 hello 첫 번째 사용자가 선택한 DNS 이름의 형식에서으로 이름이 완성 되도록 **TESTNAME.cloudapp.net**
   * Hello에 **지역/선호도 그룹/가상 네트워크** 상자에서이 가상 이미지가 호스팅될 여기서 지역을 선택 합니다.
   * Hello에 **저장소 계정**, 기존 저장소 계정을 선택 하거나 자동으로 생성 된를 선택 합니다.
   * Hello에 **가용성 집합** 상자 **(없음)**합니다.
   * 읽고 hello 가격 정보에 동의 합니다.
6. Hello에 **끝점** 섹션에서 아래에서 빈 드롭다운에서 hello **이름**를 선택 하 고 **MSSQL** hello (데이터베이스엔진인스턴스의hello포트번호를입력합니다**1433** hello 기본 인스턴스에 대 한).
7. SQL Server VM을 IPython Notebook 서버로 사용할 수도 있습니다. 이는 이후 단계에서 구성합니다.
   IPython 노트북 서버에 대 한 새 끝점 toospecify hello 포트 toouse를 추가 합니다. Hello에 이름을 입력 **이름** 열 hello 공용 포트에 대 한 사용자가 선택한 포트 번호를 선택 하 고 hello 개인 포트에 대 한 9999입니다.
   
   Hello hello 맨 아래 오른쪽 toocontinue에서 다음 화살표를 클릭 합니다.
   
   ![MSSQL 및 IPython 포트 선택][3]
8. Hello 기본값을 그대로 **설치 VM 에이전트** 옵션 채로 hello hello 마법사 toocomplete hello VM 프로 비전 프로세스의 맨 아래 오른쪽 모서리에 hello hello 확인 표시를 클릭 합니다.
   
   `![VM 최종 옵션][4]
9. Azure에서 가상 컴퓨터를 준비하는 동안 기다립니다. 통해 가상 컴퓨터 상태 tooproceed hello를 예상 합니다.
   
   * 시작 중(프로비전 중)
   * 중지됨
   * 시작 중(프로비전 중)
   * 실행 중(프로비전 중)
   * 실행 중

## <a name="RemoteDesktop"></a>원격 데스크톱 및 전체 설치를 사용 하 여 hello 가상 컴퓨터를 열려면
1. 프로 비전 완료 되 면 가상 컴퓨터 toogo toohello 대시보드 페이지의 hello 이름을 클릭 합니다. Hello hello 페이지의 아래쪽에 있는 클릭 **연결**합니다.
2. Windows 원격 데스크톱 프로그램 hello를 사용 하 여 tooopen hello rpd 파일 선택 (`%windir%\system32\mstsc.exe`).
3. Hello에 **Windows 보안** 대화 상자를 이전 단계에서 지정한 로컬 관리자 계정에 대 한 hello 암호를 제공 합니다.
   (메시지가 나타날 수 있습니다 hello 가상 컴퓨터의 tooverify hello 자격 증명입니다.)
4. hello 처음 toothis 가상 컴퓨터에 로그온 할 때 여러 프로세스가 해야 설치 하 여 데스크톱, Windows 업데이트 및 hello Windows 초기 구성 작업 (sysprep)의 완료를 포함 하 여 toocomplete 합니다. Windows sysprep가 완료되면 SQL Server 설치 프로세스에서 구성 작업을 완료합니다. 이러한 작업으로 인해 완료되는 동안 잠시 지연이 발생할 수 있습니다. `SELECT @@SERVERNAME`SQL Server 설치를 완료 하 고 SQL Server Management Studio hello 시작 페이지에서 보이는 하지 못할 때까지 hello 올바른 이름을 반환할 수 있습니다.

Windows 원격 데스크톱으로 가상 컴퓨터를 연결 된 toohello 되 면 hello 가상 컴퓨터 작동과 거의 동일한 다른 컴퓨터. Hello에 toohello 기본 인스턴스 (hello 가상 컴퓨터에서 실행) 하는 SQL Server Management Studio를 사용 하 여 SQL server 연결 일반적인 방법입니다.

## <a name="InstallIPython"></a>IPython Notebook 및 기타 지원 도구 설치
tooconfigure IPython 노트북 서버 및 설치 추가 지원으로 하 여 새 SQL Server VM tooserve 이러한 AzCopy, Azure 저장소 탐색기, 유용한 데이터 과학 Python 패키지 및 다른 도구, 특수 한 사용자 지정 스크립트가 tooyou 제공 됩니다. tooinstall:

1. 마우스 오른쪽 단추로 클릭 hello **Windows 시작** 아이콘을 클릭 하 여 **명령 프롬프트 (관리자)**
2. Hello 다음 명령을 복사한 hello 명령 프롬프트에 붙여 넣습니다.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. 대화 상자가 나타나면 IPython 노트북 서버 hello에 대 한 원하는 암호를 입력 합니다.
4. hello 사용자 지정 스크립트를 포함 하는 몇 가지 설치 후 프로시저 자동화할 수 있습니다.
    * IPython Notebook 서버 설치 및 설정
    * 앞에서 만든 hello 끝점에 대 한 hello Windows 방화벽에서 TCP 포트를 열기:
    * SQL Server 원격 연결
    * IPython Notebook 서버 원격 연결
    * 샘플 IPython Notebook 및 SQL 스크립트 가져오기
    * 유용한 데이터 과학 Python 패키지 다운로드 및 설치
    * AzCopy 및 Azure 저장소 탐색기 와 같은 Azure 도구 다운로드 및 설치   
    <br>
5. 액세스 및 IPython 노트북 hello 양식의 URL을 사용 하 여 모든 로컬 또는 원격 브라우저에서 실행할 수 있습니다 `https://<virtual_machine_DNS_name>:<port>`, 여기서 hello 가상 컴퓨터 프로 비전 하는 동안 선택한 hello IPython 공용 포트는 포트입니다.
6. IPython 노트북 서버 백그라운드 서비스로 실행 되 고 hello 가상 컴퓨터를 다시 시작할 때 자동으로 시작 됩니다.

## <a name="Optional"></a>필요에 따라 데이터 디스크 연결
VM 이미지에는 C 드라이브 (운영 체제 디스크) 및 (임시 디스크)를 D 드라이브 이외의 디스크가 즉, 데이터 디스크를 하나 tooadd 필요 하거나 더 많은 데이터 디스크 toostore 데이터. SQL Server 2012 SP2 Enterprise 작업용으로 최적화 된 데이터 웨어하우징에 대 한 hello VM 이미지는 SQL Server 데이터 및 로그 파일에 대 한 추가 디스크도 미리 구성 되어 제공 됩니다.

> [!NOTE]
> Hello D 드라이브 toostore 데이터를 사용 하지 마십시오. Hello 이름에서 알 수 있듯이 임시 저장소만 제공 합니다. Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.
> 
> 

tooattach 추가 데이터 디스크에 설명 된 hello 단계에 따라 [어떻게 tooAttach 데이터 디스크 tooa Windows 가상 컴퓨터](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)는 과정을 안내 합니다.

1. 이전 단계에서 사용자를 프로 비전 하는 빈 디스크 toohello 가상 컴퓨터를 연결 합니다.
2. Hello hello 가상 컴퓨터에 새 디스크의 초기화

## <a name="SSMS"></a>TooSQL Server Management Studio를 연결 하 고 혼합된 모드 인증 사용
SQL Server 데이터베이스 엔진 hello 도메인 환경이 없는 Windows 인증을 사용할 수 없습니다. 다른 컴퓨터에서 데이터베이스 엔진 tooconnect toohello 혼합된 모드 인증에 대 한 SQL Server를 구성 합니다. 혼합 모드 인증은 SQL Server 인증과 Windows 인증을 모두 허용합니다. SQL 인증 모드에서 SQL Server VM 데이터베이스에서 직접 순서 tooingest 데이터에서 필요한는 [Azure 기계 학습 스튜디오](https://studio.azureml.net) hello 데이터 가져오기 모듈을 사용 합니다.

1. 원격 데스크톱을 사용 하 여 가상 컴퓨터를 연결 된 toohello 하는 동안 Windows hello를 사용 하 여 **검색** 창과 형식 **SQL Server Management Studio** (SMSS). Toostart hello SQL Server Management Studio (SSMS)를 클릭 합니다. 나중에 사용할 바로 가기 tooSSMS tooadd 바탕 화면에서 할 수 있습니다.
   
   ![SSMS 시작][5]
   
   처음으로 Management Studio hello 사용자가 Management Studio 환경을 만들어야 열 번호입니다. 어느 정도 시간이 걸릴 수 있습니다.
2. Management Studio hello 제공을 열 때 **tooServer 연결** 대화 상자. Hello에 **서버 이름** 상자 hello 개체 탐색기로 hello 가상 컴퓨터 tooconnect toohello 데이터베이스 엔진의 hello 이름을 입력 합니다.
   (Hello 가상 컴퓨터 이름 대신 사용할 수도 있습니다 **(local)** 또는 hello로 단일 기간의 **서버 이름**합니다. 선택 **Windows 인증**, 둡니다  ***프로그램\_VM\_이름*\\프로그램\_로컬\_관리자**  hello에 **사용자 이름** 상자입니다. **Connect**를 클릭합니다.
   
   ![TooServer 연결][6]
   
   <br>
   
   > [!TIP]
   > Windows 레지스트리 키 변경 또는 hello SQL Server Management Studio를 사용 하 여 hello SQL Server 인증 모드를 변경할 수 있습니다. hello 레지스트리 키 변경 시작을 사용 하 여 toochange 인증 모드는 **새 쿼리** hello 다음 스크립트를 실행 합니다.
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    SQL Server management Studio를 사용 하 여 toochange hello 인증 모드:

1. **SQL Server Management Studio 개체 탐색기**, SQL Server (hello 가상 컴퓨터 이름)의 hello 인스턴스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.
   
   ![서버 속성][7]
2. Hello에 **보안** 페이지의 **서버 인증**선택, **SQL Server 및 Windows 인증 모드**, 클릭 하 고 **확인** .
   
   ![인증 모드 선택][8]
3. Hello에 **SQL Server Management Studio** 대화 상자를 클릭 **확인** hello 요구 사항 toorestart SQL Server를 승인 하는 데 있습니다.
4. **개체 탐색기**에서 서버를 마우스 오른쪽 단추로 클릭한 후 **다시 시작**을 클릭합니다. SQL Server 에이전트가 실행 중인 경우 에이전트도 다시 시작해야 합니다.
   
   ![다시 시작][9]
5. Hello에 **SQL Server Management Studio** 대화 상자에서 클릭 **예** toorestart SQL Server 되도록 동의 해야 합니다.

## <a name="Logins"></a>SQL Server 인증 로그인 만들기
다른 컴퓨터에서 tooconnect toohello 데이터베이스 엔진, SQL Server 인증 로그인을 하나 이상 만들어야 합니다.  

새 SQL Server 로그인을 프로그래밍 방식으로 만들 수 있습니다 또는 SQL Server Management Studio hello를 사용 하 여 합니다. SQL 인증을 사용 하는 새 sysadmin 사용자를 프로그래밍 방식으로 시작 toocreate는 **새 쿼리** hello 다음 스크립트를 실행 합니다. <새 사용자 이름\> 및 <새 암호\>를 원하는 *사용자 이름* 및 *암호*로 바꿉니다. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


필요에 따라 hello 암호 정책을 조정 (hello 샘플 코드 해제 검사 및 암호 만료 정책). SQL Server 로그인에 대한 자세한 내용은 [로그인 만들기](http://msdn.microsoft.com/library/aa337562.aspx)를 참조하십시오.  

toocreate 새 SQL Server 로그인 hello SQL Server Management Studio를 사용 하 여:

1. **SQL Server Management Studio 개체 탐색기**, toocreate hello에 대 한 새 로그인 원하는 hello 서버 인스턴스의 hello 폴더를 확장 합니다.
2. 마우스 오른쪽 단추로 클릭 hello **보안** 폴더를 너무 가리킨**새로**, 선택한 **로그인...** .
   
   ![새 로그인][10]
3. Hello에 **로그인-신규** 대화 상자의 hello **일반** 페이지에서 hello에 hello 새 사용자의 hello 이름을 입력 **로그인 이름** 상자입니다.
4. **SQL Server 인증**을 선택합니다.
5. Hello에 **암호** 상자에 새 사용자 hello에 대 한 암호를 입력 합니다. Hello에 해당 암호를 다시 입력 **암호 확인** 상자입니다.
6. 복잡성 및 강제 적용에 대 한 암호 정책 옵션 tooenforce 선택 **암호 정책 강제 적용** (권장). SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.
7. 만료에 대 한 암호 정책 옵션 tooenforce 선택 **암호 만료 강제 적용** (권장). 암호 정책 강제 적용이 확인란을 선택한 tooenable 여야 합니다. SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.
8. hello에 처음 로그인 한 후 새 암호를 사용 하는 tooforce hello 사용자 toocreate 선택 **사용자는 다음 로그인 시 암호를 변경 해야** (있으면이 로그인은 사용자에 대 한 다른 toouse 권장 합니다. 사용자는 용도 대 한 hello 로그인 경우이 옵션 선택 하지 않으면이.) 암호 만료 강제 적용이 확인란을 선택한 tooenable 여야 합니다. SQL Server 인증을 선택할 경우 이 항목은 기본 옵션입니다.
9. Hello에서 **기본 데이터베이스** 목록 hello 로그인에 대 한 기본 데이터베이스를 선택 합니다. **마스터** 이 옵션에 대 한 hello 기본값입니다. 사용자 데이터베이스를 아직 만들지 않은 경우에이 둡니다**마스터**합니다.
10. Hello에 **기본 언어** 목록에서 둡니다 **기본** hello 값으로.
    
    ![로그인 속성][11]
11. Hello 처음 로그인을 만들려는 경우에 SQL Server 관리자는이 로그인을 지정 하는 것이 좋습니다. 그렇게 하는 경우 **서버 역할** 페이지에서 **sysadmin**을 선택합니다.
    
    > [!IMPORTANT]
    > Hello sysadmin 고정 서버 역할의 멤버가 데이터베이스 엔진 hello를 완전히 제어할 수 있습니다. 보안상의 이유로 이 역할의 구성원은 신중하게 제한해야 합니다.
    > 
    > 
    
    ![sysadmin][12]
12. 확인을 클릭합니다.

## <a name="DNS"></a>Hello 가상 컴퓨터의 DNS 이름을 hello 결정
tooconnect toohello 다른 컴퓨터에서 SQL Server 데이터베이스 엔진, hello DNS 도메인 이름 ()를 알고 있어야 hello 가상 컴퓨터의 이름입니다.

(이 hello 이름 hello 인터넷 사용 하 여 tooidentify hello 가상 컴퓨터. Hello IP 주소를 사용할 수 있지만 Azure에서 중복성 이나 유지 관리에 대 한 리소스 이동할 때 hello IP 주소가 변경 될 수 있습니다. 기 hello DNS 이름은 안정적인 것 tooa 새 IP 주소를 리디렉션됩니다.)

1. Hello Azure 클래식 포털에서에서 (또는 hello 이전 단계의) 선택 **가상 컴퓨터**합니다.
2. Hello에 **가상 컴퓨터 인스턴스** 페이지 hello **DNS 이름** 나타나는 hello 가상 컴퓨터에 대 한 열, 찾기 및 복사 hello DNS 이름 앞에 **http://**합니다. (hello 사용자 인터페이스 hello 전체 이름 보이지 않을 수도 있지만, 마우스 오른쪽 단추로 클릭 하 고 복사본을 선택할 수).

## <a name="cde"></a>다른 컴퓨터에서 toohello 데이터베이스 엔진 연결
1. 컴퓨터에서 연결 toohello 인터넷, SQL Server Management Studio를 엽니다.
2. Hello에 **tooServer 연결** 또는 **tooDatabase 엔진 연결** 대화 상자의 hello **서버 이름** (hello에서 결정 합니다. 가상 컴퓨터의 hello DNS 이름을 입력 합니다 이전 작업)과의 hello 형식에 공용 끝점 포트 번호 *DNSName, portnumber* 같은 **tutorialtestVM.cloudapp.net,57500**합니다.
3. Hello에 **인증** 상자 **SQL Server 인증**합니다.
4. Hello에 **로그인** 상자 이전 작업에서 만든 로그인의 hello 이름을 입력 합니다.
5. Hello에 **암호** 상자에서 이전 태스크에서 만드는 hello 로그인의 hello 암호를 입력 합니다.
6. **Connect**를 클릭합니다.

## <a name="amlconnect"></a>Azure 기계 학습에서 toohello 데이터베이스 엔진 연결
Hello 팀 데이터 과학 프로세스의 이후 단계를 사용 하 여 hello [Azure 기계 학습 스튜디오](https://studio.azureml.net) toobuild 및 기계 학습 모델을 배포 합니다. tooingest 데이터베이스의에서 데이터에 SQL Server VM에 Azure 기계 학습, 평가 또는 학습에 대 한 직접 사용 하 여 hello **데이터 가져오기** 새 모듈 [Azure 기계 학습 스튜디오](https://studio.azureml.net) 시험 합니다. 이 항목은 hello 팀 데이터 과학 프로세스 지침 링크를 통해 자세한 내용을 다룹니다. 지침은 [Azure 기계 학습 스튜디오란?](machine-learning-what-is-ml-studio.md)을 참조하세요.

1. Hello에 **속성** hello의 창 [데이터 가져오기 모듈](https://msdn.microsoft.com/library/azure/dn905997.aspx)선택, **Azure SQL 데이터베이스** hello에서 **데이터 원본** 드롭다운 목록입니다.
2. Hello에 **데이터베이스 서버 이름** 텍스트 상자에 입력 합니다`tcp:<DNS name of your virtual machine>,1433`
3. Hello에 hello SQL 사용자 이름 입력 **서버 사용자 계정 이름** 입력란.
4. Hello에 hello sql 사용자의 암호를 입력 **서버 사용자 계정 암호** 입력란.
   
   ![Azure 기계 학습 데이터 가져오기][13]

## <a name="shutdown"></a>사용하지 않을 때 가상 컴퓨터 종료 및 할당 해제
Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다. 되 고 있지 tooensure toobe hello에가 가상 컴퓨터를 사용 하지 않는 경우 대금 청구를 **중지 (할당 취소)** 상태입니다.

> [!NOTE]
> Hello 가상 컴퓨터 종료에서 (Windows 전원 옵션 사용), 내부 hello VM을 중지 했지만 할당 된 상태로 유지 됩니다. tooensure 있습니다를 청구 되는, hello에서 가상 컴퓨터를 항상 중지 [Azure 클래식 포털](http://manage.windowsazure.com/)합니다. 너무 "PostShutdownAction" 동일한 ShutdownRoleOperation를 호출 하 여 hello Powershell 통해 VM을 중지할 수도 있습니다 "StoppedDeallocated" 합니다.
> 
> 

tooshutdown hello 가상 컴퓨터 할당 취소 및:

1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/) 계정을 사용 합니다.  
2. 선택 **가상 컴퓨터** hello 왼쪽된 탐색 모음에서 합니다.
3. 가상 컴퓨터의 hello 목록에서 가상 컴퓨터 아니면 이동 toohello hello 이름을 클릭 **대시보드** 페이지.
4. Hello hello 페이지의 아래쪽에 있는 클릭 **종료**합니다.

![VM 종료][15]

hello 가상 컴퓨터를 할당 취소 되지만 삭제 되지 않습니다. Hello Azure 클래식 포털에서에서 언제 든 지 가상 컴퓨터를 다시 시작할 수 있습니다.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Azure SQL Server VM이 준비 toouse: 다음 내용은 무엇입니까?
가상 컴퓨터가 데이터 과학 연습에서 준비 toouse 되었습니다. hello 가상 컴퓨터를 Azure 기계 학습 및 hello 팀 데이터 과학 프로세스 (TDSP) hello 탐색 및 데이터의 처리에 대 한 IPython 노트북 서버와 함께에서 다른 작업으로 사용 하기 위해 준비 이기도합니다.

hello hello 데이터 과학 프로세스의 다음 단계에에서 매핑된 hello [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) HDInsight, 프로세스에 데이터를 이동 하 고 Azure 컴퓨터와 것이 있으면 hello 데이터 로부터 학습을 위한 준비 과정에서 샘플링 하는 단계를 포함할 수 있습니다 알 수 있습니다.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

