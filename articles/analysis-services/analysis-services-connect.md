---
title: "Azure Analysis Services에 연결 | Microsoft Docs"
description: "Azure의 Analysis Services 서버에서 데이터에 연결하고 가져오는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="d492c-103">Azure Analysis Services 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="d492c-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="d492c-104">이 문서에서는 SSMS(SQL Server Management Studio) 또는 SSDT(SQL Server 데이터 도구)와 같은 데이터 모델링 및 관리 응용 프로그램을 사용하여 서버에 연결하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="d492c-105">또는 Microsoft Excel, Power BI Desktop 또는 사용자 지정 응용 프로그램과 같은 클라이언트 보고 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="d492c-106">Azure Analysis Services에 연결에서 HTTPS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="d492c-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d492c-107">Client libraries</span></span>
[<span data-ttu-id="d492c-108">최신 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="d492c-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="d492c-109">종류에 관계없이 모든 서버 연결에서 Analysis Services 서버에 연결하고 인터페이스하려면 업데이트된 AMO, ADOMD.NET 및 OLEDB 클라이언트 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="d492c-110">SSMS, SSDT, Excel 2016 및 Power BI의 경우 최신 클라이언트 라이브러리가 설치되어 있거나 월별 릴리스로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="d492c-111">그러나 경우에 따라 응용 프로그램에 최신 버전이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="d492c-112">예를 들어 정책 지연 업데이트 또는 Office 365 업데이트가 지연된 채널에 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="d492c-113">서버 이름</span><span class="sxs-lookup"><span data-stu-id="d492c-113">Server name</span></span>

<span data-ttu-id="d492c-114">Azure에서 Analysis Services 서버를 만들 경우 고유한 이름 및 만들 서버 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="d492c-115">연결에서 서버 이름을 지정할 경우 서버 명명 구성표는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="d492c-116">프로토콜이 문자열 **asazure**인 경우 지역은 서버를 만든 지역의 URI(예: westus.asazure.windows.net)이고 서버 이름은 지역 내 고유 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="d492c-117">서버 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="d492c-117">Get the server name</span></span>
<span data-ttu-id="d492c-118">**Azure Portal** > 서버 > **개요** > **서버 이름**에서 전체 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="d492c-119">조직의 다른 사용자가 이 서버에 연결하는 경우 그들과 이 서버 이름을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="d492c-120">서버 이름을 지정할 경우 전체 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-120">When specifying a server name, the entire path must be used.</span></span>

![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="d492c-122">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="d492c-122">Connection string</span></span>

<span data-ttu-id="d492c-123">테이블 형식 개체 모델을 사용하여 Azure Analysis Services에 연결할 경우 다음 연결 문자열 서식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="d492c-124">통합 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="d492c-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="d492c-125">사용할 수 있는 경우 통합 인증에서 Azure Active Directory 자격 증명 캐시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="d492c-126">그렇지 않은 경우 Azure 로그인 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="d492c-127">사용자 이름 및 암호를 포함한 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="d492c-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="d492c-128">Windows 인증(통합 보안)</span><span class="sxs-lookup"><span data-stu-id="d492c-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="d492c-129">현재 프로세스를 실행 중인 Windows 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="d492c-130">.odc 파일을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="d492c-130">Connect using an .odc file</span></span>
<span data-ttu-id="d492c-131">이전 버전의 Excel 사용자는 Office 데이터 연결(.odc) 파일을 사용하여 Azure Analysis Services 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d492c-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="d492c-132">자세한 내용은 [Office 데이터 연결(.odc) 파일 만들기](analysis-services-odc.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d492c-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d492c-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d492c-133">Next steps</span></span>
<span data-ttu-id="d492c-134">[Excel로 연결](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="d492c-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="d492c-135">[Power BI로 연결](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="d492c-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="d492c-136">서버 관리</span><span class="sxs-lookup"><span data-stu-id="d492c-136">Manage your server</span></span>](analysis-services-manage.md)   

