---
title: Server Business Intelligence aaaSQL | Microsoft Docs
description: "이 항목 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 하 고 Azure 가상 컴퓨터 (Vm)에서 실행 중인 SQL Server에 대 한 사용할 수 있는 hello BI (비즈니스 인텔리전스) 기능을 설명 합니다."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Azure 가상 컴퓨터의 SQL Server Business Intelligence
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

hello Microsoft Azure 가상 컴퓨터 갤러리는 SQL Server 설치가 포함 된 이미지를 포함 합니다. hello hello 갤러리 이미지에서 지원 되는 버전은 SQL Server hello 동일한 설치 파일 tooon 온-프레미스 컴퓨터와 가상 컴퓨터를 설치할 수 있습니다. 이 항목에서는 SQL Server BI (Business Intelligence) hello 요약 hello 이미지에 설치 된 기능 및 가상 컴퓨터가 프로 비전 된 후 필요한 구성 단계입니다. 이 항목은 BI 기능에 대해 지원되는 배포 토폴로지 및 모범 사례도 설명합니다.

## <a name="license-considerations"></a>라이선스 고려 사항
Microsoft Azure 가상 컴퓨터의 SQL Server에 두 가지 방법으로 toolicense 가지가 있습니다.

1. Software Assurance에 속한 라이선스 이동 혜택. 자세한 내용은 [Azure에서 Software Assurance를 통한 라이선스 이동](https://azure.microsoft.com/pricing/license-mobility/)을 참조하세요.
2. SQL Server가 설치된 Azure 가상 컴퓨터의 시간당 요금. 참조에서 "SQL Server" 섹션을 hello [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql)합니다.

라이선스 및 현재 요금에 대한 자세한 내용은 [가상 컴퓨터 라이선스 FAQ](https://azure.microsoft.com/pricing/licensing-faq/%20/)를 참조하세요.

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Azure 가상 컴퓨터 갤러리에서 사용 가능한 SQL Server 이미지
hello Microsoft Azure 가상 컴퓨터 갤러리에 Microsoft SQL Server가 포함 된 몇 가지 이미지가 있습니다. hello 가상 컴퓨터 이미지에 설치 된 hello 소프트웨어 hello 버전의 hello 운영 체제 및 SQL Server의 hello 버전에 따라 다릅니다. hello hello Azure 가상 컴퓨터 갤러리에서 사용할 수 있는 이미지 목록은 자주 변경 됩니다.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Azure VM 갤러리의 SQL 이미지](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) hello 다음 PowerShell 스크립트를 반환 hello ImageName에에서 "SQL Server"가 포함 된 Azure 이미지 목록을 hello:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

SQL Server에서 지 원하는 버전과 기능에 대 한 자세한 내용은 hello 다음을 참조 하십시오.

* [SQL Server 버전](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Hello SQL Server 2016 버전에서 지원 되는 기능](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>SQL Server 가상 컴퓨터 갤러리 이미지 hello에 BI 기능 설치
hello 다음 표에 요약 되어 SQL Server에 대 한 hello 공용 Microsoft Azure 가상 컴퓨터 갤러리 이미지에 설치 된 hello Business Intelligence 기능:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| SQL Server BI 기능 | Hello 갤러리 이미지에 설치 | 참고 사항 |
| --- | --- | --- |
| **Reporting Services 기본 모드** |예 |설치 있지만 hello 보고서 관리자 URL을 포함 하 여 구성 해야 합니다. Hello 섹션을 참조 [Reporting Services 구성](#configure-reporting-services)합니다. |
| **Reporting Services SharePoint 모드** |아니요 |hello Microsoft Azure 가상 컴퓨터 갤러리 이미지는 SharePoint 또는 SharePoint 설치 파일입니다. <sup>1</sup> |
| **Analysis Services 다차원 및 데이터 마이닝(OLAP)** |예 |설치 및 구성으로 hello 기본 Analysis Services 인스턴스 |
| **Analysis Services 테이블 형식** |아니요 |SQL Server 2012, 2014 및 2016 이미지에서 지원되지만 기본적으로 설치되지 않습니다. Analysis Services의 다른 인스턴스를 설치합니다. Hello 섹션을 참조 합니다.이 항목의 다른 SQL Server 서비스 및 기능을 설치 합니다. |
| **SharePoint용 Analysis Services 파워 피벗** |아니요 |hello Microsoft Azure 가상 컴퓨터 갤러리 이미지는 SharePoint 또는 SharePoint 설치 파일입니다. <sup>1</sup> |

<sup>1</sup> SharePoint 및 Azure Virtual Machines에 대한 추가 정보는 [SharePoint 2013용 Microsoft Azure 아키텍처](https://technet.microsoft.com/library/dn635309.aspx) 및 [Microsoft Virtual Machines에 SharePoint 배포](https://www.microsoft.com/download/details.aspx?id=34598)를 참조하세요.

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello 서비스 이름에 다음 PowerShell 명령을 tooget hello 목록이 "SQL"을 포함 하는 설치 된 서비스를 실행 합니다.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>일반 권장 사항 및 모범 사례
* 최소 권장 크기는 가상 컴퓨터는 hello **A3** SQL Server Enterprise Edition을 사용 하는 경우. hello **A4** 가상 컴퓨터 크기는 Analysis Services 및 Reporting Services의 SQL Server BI 배포에 권장 됩니다.
  
    Hello 현재 VM 크기에 대 한 자세한 내용은 참조 [Azure 위한 가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* 디스크 관리에 대 한 가장 좋은 방법은 toostore 데이터, 로그 및 백업 파일을 드라이브에가 아닌 **C**: 및 **D**: 합니다. 예를 들어 데이터 디스크 **E**: 및 **F**:를 만듭니다.
  
  * hello 드라이브 캐싱 정책은 hello 기본 드라이브에 대 한 **C**: 데이터로 작업 적합 하지 않습니다.
  * hello **D**: 드라이브는 hello 페이지 파일에 주로 사용 되는 임시 드라이브입니다. hello **D**: 드라이브는 영구 저장소가 아니며 blob 저장소에 저장 되지 않습니다. 가상 컴퓨터 크기 변경 toohello hello를 다시 설정 등의 관리 태스크 **D**: 드라이브입니다. 너무 좋습니다**하지** hello를 사용 하 여 **D**: tempdb를 비롯 한 데이터베이스 파일에 대 한 드라이브입니다.
    
    만들고 디스크를 연결에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooAttach 데이터 디스크 tooa 가상 컴퓨터](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
* 중지 하거나 toouse 계획이 아닌 서비스를 제거 합니다. 예제 hello 가상 컴퓨터만 사용 하는 경우 Reporting Services에 대 한 중지 또는 Analysis Services 및 SQL Server Integration Services를 제거 합니다. hello 다음 이미지는 기본적으로 시작 하는 hello 서비스의 예입니다.
  
    ![SQL Server 서비스](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > hello SQL Server 데이터베이스 엔진 지원 hello BI 시나리오에 필요 합니다. 단일 서버 VM 토폴로지에서 hello 데이터베이스 엔진은 필요한 toobe에서 실행 되는 동일한 VM hello 합니다.
  
    자세한 내용은 hello 다음을 참조 하십시오.: [Reporting Services 제거](https://msdn.microsoft.com/library/hh479745.aspx) 및 [Analysis Services의 인스턴스 제거](https://msdn.microsoft.com/library/ms143687.aspx)합니다.
* **Windows 업데이트**에서 새 '중요 업데이트'를 확인합니다. hello Microsoft Azure 가상 컴퓨터 이미지 자주 새로 고쳐집니다. 그러나 중요 한 업데이트를 사용할 수 있게 되에서 **Windows Update** hello VM 이미지가 마지막으로 새로 고친 후 합니다.

## <a name="example-deployment-topologies"></a>배포 토폴로지 예
Microsoft Azure 가상 컴퓨터를 사용 하는 예제 배포는 hello 다음과가 같습니다. 이 다이어그램의 hello 토폴로지는 일부 hello 가능한 토폴로지 SQL Server BI 기능 및 Microsoft Azure 가상 컴퓨터를 사용할 수 있습니다.

### <a name="single-virtual-machine"></a>단일 가상 컴퓨터
Analysis Services, Reporting Services, SQL Server 데이터베이스 엔진 및 데이터 원본이 단일 가상 컴퓨터에 있습니다.

![가상 컴퓨터 1을 사용하는 bi iass 시나리오](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>두 가상 컴퓨터
* Analysis Services, Reporting Services 및 SQL Server 데이터베이스 엔진이 단일 가상 컴퓨터에 hello 합니다. 이 배포에는 hello 보고서 서버 데이터베이스가 포함 됩니다.
* 데이터 원본은 두 번째 VM에 있습니다. hello 두 번째 VM에는 SQL Server 데이터베이스 엔진 데이터 원본으로

![가상 컴퓨터 2를 사용하는 bi iaas 시나리오](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>혼합된 Azure – Azure SQL 데이터베이스의 데이터
* Analysis Services, Reporting Services 및 SQL Server 데이터베이스 엔진이 단일 가상 컴퓨터에 hello 합니다. 이 배포에는 hello 보고서 서버 데이터베이스가 포함 됩니다.
* 데이터 원본은 Azure SQL 데이터베이스입니다.

![bi iaas 시나리오 vm 및 데이터 원본으로 AzureSQL 사용](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>하이브리드 – 데이터 온-프레미스
* 이 예제 배포에서는 Analysis Services, Reporting Services 및 SQL Server 데이터베이스 엔진 hello 단일 가상 컴퓨터에서 실행 합니다. 가상 컴퓨터 호스트 hello hello 보고서 서버 데이터베이스. hello 가상 컴퓨터가 다른 VPN 터널링 솔루션 또는 Azure 가상 네트워킹을 통해 온-프레미스 도메인에 가입된 tooan 있습니다.
* 데이터 원본은 온-프레미스입니다.

![bi iaas 시나리오 vm 및 온-프레미스 데이터 원본](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Reporting Services 기본 모드 구성
SQL Server에 대 한 hello 가상 컴퓨터 갤러리 이미지 hello 보고서 서버가 구성 되지 않은 있지만 Reporting Services 기본 모드 설치를 포함 합니다. 이 섹션의 단계 hello hello Reporting Services 보고서 서버를 구성합니다. Reporting Services 기본 모드 구성에 대한 자세한 내용은 [Reporting Services 기본 모드 보고서 서버(SSRS)](https://msdn.microsoft.com/library/ms143711.aspx)를 참조하세요.

> [!NOTE]
> Windows PowerShell 스크립트 tooconfigure hello 보고서 서버를 사용 하는 비슷한 내용을 보려면 [PowerShell 사용 하 여 tooCreate는 Azure VM 서 기본 모드 보고서 서버로](../classic/ps-sql-report.md)합니다.

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Toohello 가상 컴퓨터를 연결 하 고 hello Reporting Services 구성 관리자를 시작
가지 tooan Azure 가상 컴퓨터를 연결 하기 위한 두 가지 일반적인 워크플로가 있습니다.

* hello에서 tooconnect hello 가상 컴퓨터의 이름을 hello를 클릭 한 다음 클릭 **연결**합니다. 원격 데스크톱 연결이 열리고 hello 컴퓨터 이름이 자동으로 채워집니다.
  
    ![tooazure 가상 컴퓨터에 연결](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Windows 원격 데스크톱 연결 toohello 가상 컴퓨터를 연결 합니다. 사용자 인터페이스의 원격 데스크톱 hello hello:
  
  1. 형식 hello **클라우드 서비스 이름** hello 컴퓨터 이름으로 합니다.
  2. 콜론 (:)을 입력 하 고 hello hello TCP 원격 데스크톱 끝점에 대해 구성 된 공용 포트 번호입니다.
     
      Myservice.cloudapp.net:63133
     
      자세한 내용은 [클라우드 서비스란?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/)을 참조하세요.


**Reporting Services 구성 관리자 시작**

**Windows Server 2012/2016**에서:

1. Hello에서 **시작** 화면에서 **Reporting Services** toosee 앱 목록이 있습니다.
2. **Reporting Services 구성 관리자**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.

**Windows Server 2008 R2**에서:

1. **시작**을 클릭한 다음 **모든 프로그램**을 클릭합니다.
2. **Microsoft SQL Server 2016**을 클릭합니다.
3. **구성 도구**를 클릭합니다.
4. **Reporting Services 구성 관리자**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.

또는

1. **시작**을 클릭합니다.
2. Hello에 **프로그램 및 파일 검색** 대화 상자 유형을 **reporting services**합니다. Hello VM에서 Windows Server 2012를 실행 하는 경우 입력 **reporting services** hello Windows Server 2012 시작 화면에 있습니다.
3. **Reporting Services 구성 관리자**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.
   
    ![SSRS 구성 관리자 검색](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Reporting Services 구성
**서비스 계정 및 웹 서비스 URL:**

1. Hello 확인 **서버 이름** hello 로컬 서버 이름 및 클릭 **연결**합니다.
2. 빈 참고 hello **보고서 서버 데이터베이스 이름**합니다. hello 구성이 완료 되 면 hello 데이터베이스가 만들어집니다.
3. Hello 확인 **보고서 서버 상태** 은 **Started**합니다. Hello 서비스는 hello tooverify hello 서비스 Windows Server Manager에서 원한다 면 **SQL Server Reporting Services** Windows 서비스입니다.
4. 클릭 **서비스 계정** 필요에 따라 hello 계정을 변경 합니다. Hello 가상 컴퓨터는 도메인이 아닌 조인 된 환경에서 사용 하는 경우 기본 제공 hello **ReportServer** 계정이 면 충분 합니다. Hello 서비스 계정에 대 한 자세한 내용은 참조 하십시오. [서비스 계정](https://msdn.microsoft.com/library/ms189964.aspx)합니다.
5. 클릭 **웹 서비스 URL** hello 왼쪽된 창에서.
6. 클릭 **적용** tooconfigure hello 기본값입니다.
7. 참고 hello **보고서 서버 웹 서비스 Url**합니다. Note. hello 기본 TCP 포트는 80 이며 hello URL의 일부입니다. 이후 단계에서 hello 포트에 대 한 Microsoft Azure 가상 컴퓨터 끝점을 만들 수 있습니다.
8. Hello에 **결과** 창 hello 작업이 성공적으로 완료를 확인 합니다.

**데이터베이스:**

1. 클릭 **데이터베이스** hello 왼쪽된 창에서.
2. **데이터베이스 변경**을 클릭합니다.
3. **새 보고서 서버 데이터베이스 만들기** 가 선택되었는지 확인한 후 다음을 클릭합니다.
4. **서버 이름**을 확인하고 **연결 테스트**를 클릭합니다.
5. Hello 결과가 **테스트 연결에 성공 했습니다**, 클릭 **확인** 클릭 하 고 **다음**합니다.
6. 참고 hello 데이터베이스 이름이 **ReportServer** 및 hello **보고서 서버 모드** 은 **네이티브** 클릭 **다음**합니다.
7. 클릭 **다음** hello에 **자격 증명** 페이지.
8. 클릭 **다음** hello에 **요약** 페이지.
9. 클릭 **다음** hello에 **진행 후 마침** 페이지.

**2012 및 2014용 웹 포털 URL 또는 보고서 관리자 URL:**

1. 클릭 **웹 포털 URL**, 또는 **보고서 관리자 URL** hello 왼쪽된 창에서 2012 및 2014에 대 한 합니다.
2. **Apply**를 클릭합니다.
3. Hello에 **결과** 창 hello 작업이 성공적으로 완료를 확인 합니다.
4. **종료**를 클릭합니다.

보고서 서버 사용 권한에 대한 자세한 내용은 [기본 모드 보고서 서버에 대한 사용 권한 부여](https://msdn.microsoft.com/library/ms156014.aspx)를 참조하세요.

### <a name="browse-toohello-local-report-manager"></a>Toohello 찾아보기 로컬 보고서 관리자
hello VM에서 찾아보기 tooreport 관리자 tooverify hello 구성 합니다.

1. Hello VM에서 관리자 권한으로 Internet Explorer를 시작 합니다.
2. Hello VM에 toohttp://localhost/reports를 찾습니다.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>tooConnect tooRemote 웹 포털 또는 2012 및 2014에 대 한 보고서 관리자
Hello 가상 컴퓨터에서 원격 컴퓨터에서 2012 및 2014에 대 한 tooconnect toohello 웹 포털 또는 보고서 관리자를 사용할 경우 새 가상 컴퓨터 TCP 끝점을 만듭니다. 기본적으로 hello 보고서 서버에서 HTTP 요청에 대 한 수신 **포트 80**합니다. Hello 보고서 서버 Url toouse 다른 포트를 구성 하는 경우에 지침을 진행 하는 hello에 해당 포트 번호를 지정 해야 합니다.

1. Hello TCP 포트 80의 가상 컴퓨터에 대 한 끝점을 만듭니다. 자세한 내용은 참조 하십시오 hello [가상 컴퓨터 끝점 및 방화벽 포트](#virtual-machine-endpoints-and-firewall-ports) 이 문서의 섹션.
2. Hello 가상 컴퓨터의 방화벽에서 포트 80을 엽니다.
3. Toohello 웹 포털 또는 Azure 가상 컴퓨터를 사용 하 여 보고서 관리자를 찾아보기 **DNS 이름** hello URL에 hello 서버 이름으로 합니다. 예:
   
    **보고서 서버**: http://uebi.cloudapp.net/reportserver **웹 포털**: http://uebi.cloudapp.net/reports
   
    [보고서 서버 액세스를 위한 방화벽 구성](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate 및 보고서 게시 toohello Azure 가상 컴퓨터
hello 다음 표에 요약 되어 hello 옵션 사용 가능한 toopublish hello Microsoft Azure 가상 컴퓨터에서 호스트 되는 온-프레미스 컴퓨터 toohello 보고서 서버에서 기존 보고서의 일부:

* **보고서 작성기**: hello 클릭을 포함 하는 hello 가상 컴퓨터-SQL 2014 및 2012 용 Microsoft SQL Server 보고서 작성기의 버전에 한 번입니다. toostart 보고서 작성기 hello SQL 2016 hello 가상 컴퓨터에 처음으로:
  
  1. 관리자 권한으로 브라우저를 시작합니다.
  2. Hello 가상 컴퓨터에서 toohello 웹 포털을 찾아 hello 선택 **다운로드** hello 오른쪽 위에 있는 아이콘입니다.
  3. **보고서 작성기**를 선택합니다.
     
     자세한 내용은 [보고서 작성기 시작](https://msdn.microsoft.com/library/ms159221.aspx)을 참조하세요.
* **SQL Server Data Tools**: VM: SQL Server Data Tools hello 가상 컴퓨터에 설치 되어 있으며 사용 되는 toocreate 수 **보고서 서버 프로젝트** 및 hello 가상 컴퓨터에 대 한 보고서입니다. SQL Server Data Tools는 hello hello 가상 컴퓨터에서 toohello 보고서 서버 보고서를 게시할 수 있습니다.
* **SQL Server Data Tools: 원격**: 로컬 컴퓨터에서 SQL Server Data Tools로 Reporting Services 보고서가 포함된 Reporting Services 프로젝트를 만듭니다. Hello 프로젝트 tooconnect toohello 웹 서비스 URL을 구성 합니다.
  
    ![SSRS 프로젝트의 SSDT 프로젝트 속성](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* 만들기는 합니다. 보고서가 포함 되어 다음 업로드 하 고 hello 드라이브 연결 하드 드라이브 VHD입니다.
  
  1. 로컬 컴퓨터에서 보고서가 포함되는 .VHD 하드 드라이브를 만듭니다.
  2. 관리 인증서를 만들고 설치합니다.
  3. Hello VHD 파일 tooAzure hello Add-azurevhd cmdlet을 사용 하 여 업로드 [만들기 및 업로드 Windows Server VHD tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
  4. Hello 디스크 toohello 가상 컴퓨터를 연결 합니다.

## <a name="install-other-sql-server-services-and-features"></a>다른 SQL Server 서비스 및 기능 설치
tooinstall 추가 SQL Server 서비스, Analysis Services 테이블 형식 모드에서와 같은 hello SQL server 설치 마법사를 실행합니다. hello 설치 파일 hello 가상 컴퓨터의 로컬 디스크에 있습니다.

1. **시작**을 클릭한 다음 **모든 프로그램**을 클릭합니다.
2. **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** 또는 **Microsoft SQL Server 2012**를 클릭한 다음 **구성 도구**를 클릭합니다.
3. **SQL Server 설치 센터**를 클릭합니다.

또는 C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe, C:\SQLServer_11.0_full\setup.exe를 실행합니다.

> [!NOTE]
> hello 처음으로 더 많은 설치 파일을 다운로드할 수 있습니다 및 hello 가상 컴퓨터를 다시 부팅 하 고 SQL Server 설치의 다시 시작 해야 합니다. SQL Server 설치 프로그램을 실행 합니다.
> 
> Toorepeatedly 해야 할 경우 hello Microsoft Azure 가상 컴퓨터에서에서 선택한 hello 이미지를 사용자 지정, 사용자 고유의 SQL Server 이미지를 만드는 것이 좋습니다. Analysis Services SysPrep 기능은 SQL Server 2012 SP1 CU2에서 사용하도록 설정되어 있습니다. 자세한 내용은 [SysPrep을 사용하여 SQL Server 설치에 대한 고려 사항](https://msdn.microsoft.com/library/ee210754.aspx) 및 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall Analysis Services 테이블 형식 모드
이 섹션의 단계를 hello **요약** hello Analysis Services 테이블 형식 모드를 설치 합니다. 자세한 내용은 hello 다음을 참조 하십시오.

* [테이블 형식 모드에서 Analysis Services 설치](https://msdn.microsoft.com/library/hh231722.aspx)
* [테이블 형식 모델링(Adventure Works 자습서)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall Analysis Services 테이블 형식 모드:**

1. Hello SQL Server 설치 마법사에서 클릭 **설치** 왼쪽된 창의 hello와 클릭 **새 SQL server 독립 실행형 설치 또는 추가 기능 tooan 기존 설치**합니다.
   
   * Hello 표시 되 면 **폴더 찾아보기**, tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full 또는 c:\SQLServer_11.0_full 찾은 다음 클릭 **확인**합니다.
2. 클릭 **다음** on hello 제품 업데이트 페이지.
3. Hello에 **설치 유형을** 페이지에서 **SQL Server의 새로 설치** 클릭 **다음**합니다.
4. Hello에 **설치 역할** 페이지 **SQL Server 기능 설치**합니다.
5. Hello에 **기능 선택** 페이지 **Analysis Services**합니다.
6. Hello에 **인스턴스 구성** 페이지와 같은 설명이 포함 된 이름을 입력 합니다 **Tabular** 에 **명명 된 인스턴스** 및 **인스턴스 Id** 텍스트 상자입니다.
7. Hello에 **Analysis Services 구성** 페이지에서 **테이블 형식 모드**합니다. Hello 현재 사용자 toohello 관리 권한 목록에 추가 합니다.
8. 완료 하 고 hello SQL Server 설치 마법사를 닫습니다.

## <a name="analysis-services-configuration"></a>Analysis Services 구성
### <a name="remote-access-tooanalysis-services-server"></a>원격 액세스 tooAnalysis 서비스 서버
Analysis Services 서버는 Windows 인증만 지원합니다. Analysis Services SQL Server Management Studio 또는 SQL Server Data Tools와 같은 클라이언트 응용 프로그램에서 원격으로 tooaccess, hello 가상 컴퓨터에 toobe 조인된 tooyour 로컬 도메인을 Azure 가상 네트워킹을 사용 하 여 필요 합니다. 자세한 내용은 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md)를 참조하세요.

Analysis Services의 **기본 인스턴스**는 TCP 포트 **2383**에서 수신합니다. Hello 가상 컴퓨터 방화벽에서 hello 포트를 엽니다. 또한 Analysis Services의 클러스터된 명명된 인스턴스도 **2383**포트에서 수신합니다.

에 대 한는 **명명 된 인스턴스** hello SQL Server Browser 서비스는 필요한 Analysis services, toomanage 포트 액세스 합니다. hello SQL Server Browser 기본 구성은 포트 **2382**합니다.

Hello 가상 컴퓨터 방화벽에서 포트를 열고 **2382** 정적 Analysis Services 명명 된 인스턴스 포트를 만듭니다.

1. 에 이미 있는 tooverify 포트 hello VM 및 hello 포트를 사용 중인 프로세스에서 사용 하 여, hello 다음 명령을 관리자 권한으로 실행 합니다.
   
        netstat /ao
2. 사용 하 여 SQL Server Management Studio toocreate 정적 Analysis Services 명명 된 인스턴스 포트 '포트' 업데이트 하 여 값의 테이블 형식 AS 인스턴스 일반 속성입니다. 자세한 내용은 참조에서 "고정된 포트를 사용 하 여 기본 또는 명명 된 인스턴스" hello [hello Windows 방화벽 tooAllow Analysis Services 액세스를 구성](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed)합니다.
3. Hello hello Analysis Services 서비스의 테이블 형식 인스턴스를 다시 시작 합니다.

자세한 내용은 참조 하십시오 hello **가상 컴퓨터 끝점 및 방화벽 포트** 이 문서의 섹션.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>가상 컴퓨터 끝점 및 방화벽 포트
이 섹션에는 Microsoft Azure 가상 컴퓨터 끝점 toocreate 및 포트 tooopen hello 가상 컴퓨터 방화벽에 요약 되어 있습니다. hello 다음 표에 요약 되어 hello **TCP** 포트에 대 한 toocreate 끝점 및 hello 가상 컴퓨터 방화벽에서 포트 tooopen hello 합니다.

* 단일 VM을 사용 하는 hello 다음 두 항목에 해당할 경우 toocreate VM 끝점 필요가 없습니다 및 hello 방화벽 hello VM에서 tooopen hello 포트 필요가 없습니다.
  
  * Toohello SQL Server 기능 hello VM에 원격으로 연결 하지 않습니다. 원격 데스크톱 연결 toohello VM을 설정 하 고 hello VM에서 로컬로 hello SQL Server 기능에 액세스 하는 원격 연결 toohello SQL Server 기능을 고려 하지 않습니다.
  * Azure 가상 네트워킹이 나 다른 VPN 터널링 솔루션을 통해 hello VM tooan 온-프레미스 도메인에 조인 하지 마십시오.
* Hello 가상 컴퓨터는 도메인에 가입된 tooa 불가능 하지만 원하는 경우 tooremotely toohello SQL Server 기능을 VM에 연결:
  
  * Hello 방화벽 hello VM에서 hello 포트를 엽니다.
  * Hello에 대 한 가상 컴퓨터 끝점을 만들 포트 (*)를 설명 합니다.
* Hello 가상 컴퓨터가 Azure 가상 네트워킹과 같은 VPN 터널을 사용 하 여 조인된 tooa 도메인 경우 hello 끝점이 필요 하지 않습니다. 그러나 hello 방화벽 hello VM에서 hello 포트를 엽니다.
  
  | 포트 | 형식 | 설명 |
  | --- | --- | --- |
  | **80** |TCP |보고서 서버 원격 액세스(*) |
  | **1433** |TCP |SQL Server Management Studio(*) |
  | **1434** |UDP |SQL Server Browser입니다. 이 경우 조인 된 tooa 도메인에 VM을 hello 필요 합니다. |
  | **2382** |TCP |SQL Server Browser입니다. |
  | **2383** |TCP |SQL Server Analysis Services 기본 인스턴스 및 클러스터된 명명된 인스턴스입니다. |
  | **사용자 정의** |TCP |명명 된 인스턴스 포트를 선택 하면 포트 번호에 대 한 정적 Analysis Services를 만들고 hello 방화벽에서 포트 번호 hello의 차단을 해제 합니다. |

끝점을 만드는 방법에 대 한 자세한 내용은 hello 다음을 참조 하십시오.

* 끝점 만들기:[어떻게 tooSet 끝점 tooa 가상 컴퓨터](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
* SQL Server:의 hello "전체 구성 단계 tooconnect toohello 가상 컴퓨터를 사용 하 여 SQL Server Management Studio" 섹션을 참조 하 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](../sql/virtual-machines-windows-portal-sql-server-provision.md)합니다.

hello 다음 다이어그램에서는 VM 방화벽 tooallow 원격 액세스 toofeatures hello에 포트 tooopen hello 및 hello VM에 구성 요소

![Azure Vm에서 bi 응용 프로그램에 대 한 포트 tooopen](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>리소스
* Hello Azure 가상 컴퓨터 환경에서 사용 되는 Microsoft 서버 소프트웨어에 대 한 hello 지원 정책을 검토 합니다. 항목 hello BitLocker, 장애 조치 클러스터링 및 네트워크 부하 분산 등의 기능에 대 한 지원이 요약 되어 있습니다. [Azure 가상 컴퓨터에 대한 Microsoft 서버 소프트웨어 지원](http://support.microsoft.com/kb/2721672).
* [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Azure에서 SQL Server 가상 컴퓨터 프로비전](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [어떻게 tooAttach 데이터 디스크 tooa 가상 컴퓨터](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [데이터베이스 tooSQL Azure VM에서 서버 마이그레이션](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Hello Analysis Services 인스턴스의 서버 모드 확인](https://msdn.microsoft.com/library/gg471594.aspx)
* [다차원 모델링(Adventure Works 자습서)](https://technet.microsoft.com/library/ms170208.aspx)
* [Azure 설명서 센터](https://azure.microsoft.com/documentation/)
* [하이브리드 환경에서 Power BI 사용](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Microsoft SQL Server Connect를 통해 피드백 및 연락처 정보 제출](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>커뮤니티 콘텐츠
* [PowerShell을 사용한 Azure SQL 데이터베이스 관리](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

