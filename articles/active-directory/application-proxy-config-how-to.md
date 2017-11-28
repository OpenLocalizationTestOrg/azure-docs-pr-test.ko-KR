---
title: "응용 프로그램 프록시 응용 프로그램 aaaHow tooconfigure | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 몇 가지 간단한 단계에서는 응용 프로그램 프록시 응용 프로그램 구성"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="dce76-103">어떻게 tooconfigure 응용 프로그램 프록시 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dce76-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="dce76-104">이 문서가 도움이 toounderstand 방법을 Azure AD tooexpose 내에서 응용 프로그램 프록시 응용 프로그램 tooconfigure 온-프레미스 응용 프로그램 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="dce76-105">권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="dce76-105">Recommended documents</span></span> 

<span data-ttu-id="dce76-106">hello 초기 구성과 hello 관리자 포털을 통해 응용 프로그램 프록시 응용 프로그램 만들기에 대 한 toolearn hello에 따라 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="dce76-107">커넥터를 구성 하는 방법에 대 한 세부 정보를 참조 하십시오. [hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="dce76-108">인증서 업로드 및 사용자 지정 도메인 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dce76-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="dce76-109">응용 프로그램/설정 hello Url hello를 만들려면</span><span class="sxs-lookup"><span data-stu-id="dce76-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="dce76-110">Hello hello의 단계를 따르는 경우 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) 설명서 및가 정보에 대 한 hello 오류 세부 정보 및 방법에 대 한 제안 사항 참조 hello 응용 프로그램을 만드는 동안 오류가 발생 하기 toofix hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="dce76-111">대부분의 오류 메시지에는 제안 수정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="dce76-112">tooavoid 일반적인 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="dce76-113">관리자 권한 toocreate 응용 프로그램 프록시 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="dce76-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="dce76-114">hello 내부 URL은 고유</span><span class="sxs-lookup"><span data-stu-id="dce76-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="dce76-115">hello 외부 URL이 고유</span><span class="sxs-lookup"><span data-stu-id="dce76-115">hello external URL is unique</span></span>

-   <span data-ttu-id="dce76-116">hello http 또는 https를 사용한 Url 시작 하 고 끝나야는 "/"</span><span class="sxs-lookup"><span data-stu-id="dce76-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="dce76-117">hello URL에 IP 주소가 아닌 도메인 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="dce76-118">hello 응용 프로그램을 만들 때 hello 오른쪽 위 모서리에 hello 오류 메시지가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="dce76-119">Hello 알림 아이콘 toosee hello 오류 메시지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="dce76-121">커넥터/커넥터 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="dce76-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="dce76-122">Hello 커넥터 및 커넥터 그룹에 대 한 경고로 인해 응용 프로그램을 구성 하는 데 문제가 있는 경우 응용 프로그램 프록시를 사용 하도록 설정 방법에 대 한 세부 정보에 대 한 지침을 참조 toodownload 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="dce76-123">커넥터에 대 한 자세한 toolearn hello를 참조 하십시오 [커넥터 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="dce76-124">커넥터를 활성 없는 경우이 없습니다 tooreach hello 서비스 되는지 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="dce76-125">종종 모든 hello 필요한 포트가 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="dce76-126">필요한 포트 목록이 toosee 응용 프로그램 프록시 설명서를 활성화 하는 hello의 hello 필수 구성 요소 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="dce76-127">사용자 지정 도메인에 대한 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="dce76-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="dce76-128">사용자 지정 도메인을 사용 하면 외부 Url의 toospecify hello 도메인 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="dce76-129">toouse 사용자 지정 도메인을 해당 도메인에 대 한 tooupload hello 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="dce76-130">사용자 지정 도메인 및 인증서 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dce76-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="dce76-131">인증서를 업로드 하는 문제를 발생 하는 경우 hello 인증서 문제가 hello에 대 한 자세한 내용은 hello 포털에서 hello 오류 메시지를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="dce76-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="dce76-132">인증서의 일반적인 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="dce76-133">만료된 인증서</span><span class="sxs-lookup"><span data-stu-id="dce76-133">Expired certificate</span></span>

-   <span data-ttu-id="dce76-134">자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="dce76-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="dce76-135">Hello 개인 키를 인증서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="dce76-136">hello 오류 메시지에 hello 오른쪽 위 모서리 tooupload hello 인증서를 사용 하는 대로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="dce76-137">Hello 알림 아이콘 toosee hello 오류 메시지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dce76-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="dce76-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dce76-139">Next steps</span></span>
[<span data-ttu-id="dce76-140">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="dce76-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
