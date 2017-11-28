---
title: Analysis Services aaaConnect tooAzure | Microsoft Docs
description: "Tooconnect tooand Azure에서 Analysis Services 서버에서 데이터를 가져오기 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="5522d-103">Tooan Azure Analysis Services 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="5522d-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="5522d-104">이 문서에서는 데이터 모델링 및 SQL Server Management Studio (SSMS) 또는 SQL Server Data Tools (SSDT)와 같은 관리 응용 프로그램을 사용 하 여 tooa 서버 연결을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="5522d-105">또는 Microsoft Excel, Power BI Desktop 또는 사용자 지정 응용 프로그램과 같은 클라이언트 보고 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="5522d-106">HTTPS를 사용 하는 연결 tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5522d-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="5522d-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="5522d-107">Client libraries</span></span>
[<span data-ttu-id="5522d-108">Hello 최신 클라이언트 라이브러리를 얻을</span><span class="sxs-lookup"><span data-stu-id="5522d-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="5522d-109">형식에 관계 없이 모든 연결 tooa 서버에 업데이트 된 AMO, ADOMD.NET 및 OLEDB 클라이언트 라이브러리 tooconnect tooand 인터페이스는 Analysis Services 서버와 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="5522d-110">SSMS, SSDT, Excel 2016 및 Power BI에 대 한 hello 최신 클라이언트 라이브러리 설치 되거나 월별 릴리스에로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="5522d-111">그러나 일부 경우에는 응용 프로그램 hello 최신 버전으로 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="5522d-112">예를 들어 정책 지연 시간을 업데이트 한 경우, 또는 Office 365 업데이트 hello 지연 된 채널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="5522d-113">서버 이름</span><span class="sxs-lookup"><span data-stu-id="5522d-113">Server name</span></span>

<span data-ttu-id="5522d-114">Azure에서 Analysis Services 서버를 만들면 여기서 hello 서버는 만든 toobe 고유 이름과 hello 지역을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="5522d-115">Hello 서버 이름에 대 한 연결을 지정할 때 hello 서버 이름 지정 체계를:</span><span class="sxs-lookup"><span data-stu-id="5522d-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="5522d-116">프로토콜은 문자열 **asazure**, 영역은 hello hello 서버 생성 된 위치 Uri입니다 (예를 들어 westus.asazure.windows.net) servername hello 지역 내에서 고유 서버 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="5522d-117">Hello 서버 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="5522d-117">Get hello server name</span></span>
<span data-ttu-id="5522d-118">**Azure 포털** > 서버 > **개요** > **서버 이름**, hello 전체 서버 이름 복사.</span><span class="sxs-lookup"><span data-stu-id="5522d-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="5522d-119">조직의 다른 사용자가 연결 하는 경우 toothis 서버 너무,이 서버 이름은 사람과 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="5522d-120">서버 이름을 지정할 때 hello 전체 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-120">When specifying a server name, hello entire path must be used.</span></span>

![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="5522d-122">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="5522d-122">Connection string</span></span>

<span data-ttu-id="5522d-123">TooAzure 연결할 때 사용 하 여 Analysis Services 테이블 형식 개체 모델에서 다음 연결 문자열 형식을 사용 하 여 hello hello:</span><span class="sxs-lookup"><span data-stu-id="5522d-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="5522d-124">통합 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="5522d-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="5522d-125">통합된 인증에 사용할 수 있는 경우 Azure Active Directory 자격 증명 캐시 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="5522d-126">파일이 없으면 hello Azure 로그인 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="5522d-127">사용자 이름 및 암호를 포함한 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="5522d-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="5522d-128">Windows 인증(통합 보안)</span><span class="sxs-lookup"><span data-stu-id="5522d-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="5522d-129">Hello 현재 프로세스를 실행 하는 hello Windows 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="5522d-130">.odc 파일을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="5522d-130">Connect using an .odc file</span></span>
<span data-ttu-id="5522d-131">이전 버전의 Excel 사용자는 Office 데이터 연결 (.odc) 파일을 사용 하 여 tooan Azure Analysis Services 서버를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="5522d-132">toolearn 더 참조 [Office 데이터 연결 (.odc) 파일을 만들](analysis-services-odc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5522d-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5522d-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5522d-133">Next steps</span></span>
<span data-ttu-id="5522d-134">[Excel로 연결](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="5522d-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="5522d-135">[Power BI로 연결](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="5522d-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="5522d-136">서버 관리</span><span class="sxs-lookup"><span data-stu-id="5522d-136">Manage your server</span></span>](analysis-services-manage.md)   

