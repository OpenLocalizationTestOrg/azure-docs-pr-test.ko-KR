---
title: "Azure 데이터 카탈로그 릴리스 정보 | Microsoft Docs"
description: "Azure Data Catalog에 대한 릴리스 정보입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="f66e6-103">Azure 데이터 카탈로그 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f66e6-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="f66e6-104">Azure 데이터 카탈로그의 2015년 11월 20일 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f66e6-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="f66e6-105">Power BI Desktop에서 데이터 원본 열기</span><span class="sxs-lookup"><span data-stu-id="f66e6-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="f66e6-106">**Azure 데이터 카탈로그** 포털에서 "Power BI Desktop에서 열기" 옵션을 사용할 때 Power BI Desktop 응용 프로그램에서 다음 두 가지 문제 중 하나가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="f66e6-107">"문서를 열 수 없습니다."라는 제목의 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="f66e6-108">Power BI Desktop 응용 프로그램이 열리지만 파일이 비어 있는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="f66e6-109">각 경우에 대해 [PowerBI.com](https://powerbi.com)에서 최신 버전의 Power BI Desktop을 다운로드 및 설치하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="f66e6-110">Azure 데이터 카탈로그의 2015년 11월 13일 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f66e6-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="f66e6-111">Teradata에 등록 및 연결</span><span class="sxs-lookup"><span data-stu-id="f66e6-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="f66e6-112">Teradata 데이터 원본에 연결 시 사용자는 사용할 소프트웨어의 비트 수(32비트 또는 64비트)와 일치하는 올바른 Teradata ODBC 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="f66e6-113">이 ADC 릴리스 날짜 현재, 최신 [windows용 Teradata ODBC 드라이버(버전 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) 는 Office 2013과 호환되지만 Office 2016과는 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="f66e6-114">Azure 데이터 카탈로그의 2015년 7월 13일 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f66e6-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="f66e6-115">Oracle 데이터베이스에 등록 및 연결</span><span class="sxs-lookup"><span data-stu-id="f66e6-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="f66e6-116">Oracle 데이터베이스 데이터 원본에 연결 시 사용자는 사용할 소프트웨어의 비트 수(32비트 또는 64비트)와 일치하는 올바른 Oracle 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="f66e6-117">32비트 Windows를 실행하는 컴퓨터에서 Oracle 데이터 원본 등록 시 32비트 Oracle 드라이버가 사용됨</span><span class="sxs-lookup"><span data-stu-id="f66e6-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="f66e6-118">64비트 Windows를 실행하는 컴퓨터에서 Oracle 데이터 원본 등록 시 64비트 Oracle 드라이버가 사용됨</span><span class="sxs-lookup"><span data-stu-id="f66e6-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="f66e6-119">64비트 Windows를 비롯하여 Microsoft Office 32비트 버전을 실행하는 컴퓨터에서 Excel을 사용하여 Oracle 데이터 원본에 연결 시 32비트 Oracle 드라이버가 사용됨</span><span class="sxs-lookup"><span data-stu-id="f66e6-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="f66e6-120">Microsoft Office 64비트 버전을 실행하는 컴퓨터에서 Excel을 사용하여 Oracle 데이터 원본에 연결 시 64비트 Oracle 드라이버가 사용됨</span><span class="sxs-lookup"><span data-stu-id="f66e6-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="f66e6-121">SQL Server Reporting Services에 등록 및 연결</span><span class="sxs-lookup"><span data-stu-id="f66e6-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="f66e6-122">SSRS(SQL Server Reporting Services) 데이터 원본은 현재 기본 모드 서버로만 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="f66e6-123">SharePoint 모드에서 SSRS 지원은 이후 릴리스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="f66e6-124">Excel에서 데이터 자산 열기</span><span class="sxs-lookup"><span data-stu-id="f66e6-124">Opening data assets in Excel</span></span>
<span data-ttu-id="f66e6-125">**Azure Data Catalog** 포털에서 Microsoft Excel의 데이터 자산을 열 때 **Microsoft Excel 보안 공지** 대화 상자가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="f66e6-126">이는 예상된 표준 동작입니다. 사용자는 **사용**을 선택하여 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="f66e6-127">자세한 내용은 [의심스러운 웹 사이트의 링크 및 파일에 대한 보안 경고 사용 또는 사용 안 함](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66e6-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="f66e6-128">프록시 및 정책 구성과 데이터 원본 등록</span><span class="sxs-lookup"><span data-stu-id="f66e6-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="f66e6-129">Azure 데이터 카탈로그 포털에 로그온할 수 있는 상황이 발생할 수 있지만, 데이터 원본 등록 도구에 로그온을 시도할 때 로그온하지 않도록 하는 오류 메시지가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="f66e6-130">이 문제 동작에는 다음과 같은 잠재적인 두 가지 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="f66e6-131">**원인 1: Active Directory Federation Services 구성** 데이터 원본 등록 도구가 폼 인증을 사용하여 Active Directory에 대한 사용자 로그온의 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="f66e6-132">로그온이 성공하려면 Active Directory 관리자가 전역 인증 정책에서 폼 인증을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="f66e6-133">일부 상황에서 이 오류 동작은 사용자가 회사 네트워크에 있을 때만 또는 회사 네트워크 외부에서 연결할 때만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="f66e6-134">전역 인증 정책을 사용하면 인트라넷 및 엑스트라넷 연결을 위해 인증 방법을 개별적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="f66e6-135">폼 인증이 사용자가 연결되는 네트워크에 사용하도록 설정되지 않은 경우 로그온 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="f66e6-136">자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66e6-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="f66e6-137">**원인 2: 네트워크 프록시 구성** 회사 네트워크가 프록시 서버를 사용하는 경우 등록 도구가 프록시를 통해 Azure Active Directory에 연결하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="f66e6-138">도구의 구성 파일을 편집하고 이 섹션을 파일에 추가하여 사용자가 등록 도구를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="f66e6-139">RegistrationTool.exe.config 파일을 찾으려면 등록 도구를 시작하여 Windows 작업 관리자 유틸리티를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="f66e6-140">작업 관리자의 세부 정보 탭에서 RegistrationTool.exe를 마우스 오른쪽 단추로 클릭하고 팝업 메뉴에서 파일 위치 열기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f66e6-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
