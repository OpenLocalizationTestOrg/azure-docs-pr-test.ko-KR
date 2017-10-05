---
title: "응용 프로그램 프록시 응용 프로그램을 구성하는 방법 | Microsoft 문서"
description: "몇 가지 간단한 단계로 응용 프로그램 프록시 응용 프로그램을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="16e86-103">응용 프로그램 프록시 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="16e86-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="16e86-104">이 문서에서는 온-프레미스 응용 프로그램을 클라우드에 노출하도록 Azure AD 내의 응용 프로그램 프록시 응용 프로그램을 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="16e86-105">권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="16e86-105">Recommended documents</span></span> 

<span data-ttu-id="16e86-106">관리 포털을 통한 응용 프로그램 프록시 응용 프로그램의 초기 구성 및 생성에 대해 배우려면 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="16e86-107">커넥터를 구성하는 방법에 대한 자세한 내용은 [Azure Portal에서 응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="16e86-108">인증서 업로드 및 사용자 지정 도메인 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="16e86-109">응용 프로그램 만들기/URL 설정</span><span class="sxs-lookup"><span data-stu-id="16e86-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="16e86-110">[Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) 문서의 단계에 따라 응용 프로그램을 만드는 중 오류가 발생한 경우 오류 세부 정보에서 응용 프로그램 문제 해결 방법에 대한 정보 및 제안 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="16e86-111">대부분의 오류 메시지에는 제안 수정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="16e86-112">일반적인 오류를 방지하려면 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="16e86-113">응용 프로그램 프록시 응용 프로그램을 만들 수 있는 권한을 가진 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="16e86-114">내부 URL이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-114">The internal URL is unique</span></span>

-   <span data-ttu-id="16e86-115">외부 URL이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-115">The external URL is unique</span></span>

-   <span data-ttu-id="16e86-116">URL이 http 또는 https로 시작하고 "/"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="16e86-117">URL은 IP 주소가 아닌 도메인 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="16e86-118">응용 프로그램을 만들 때 오류 메시지가 오른쪽 상단 모서리에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="16e86-119">알림 아이콘을 선택하여 오류 메시지를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-119">You can also select the notification icon to see the error messages.</span></span>

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="16e86-121">커넥터/커넥터 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="16e86-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="16e86-122">커넥터 및 커넥터 그룹에 대한 경고로 인해 응용 프로그램을 구성하는 데 어려움이 있는 경우 응용 프로그램 프록시 사용에 대한 지침에서 커넥터 다운로드 방법에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="16e86-123">커넥터에 대한 자세한 내용은 [커넥터 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="16e86-124">커넥터가 비활성 상태이면 서비스에 연결할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="16e86-125">필요한 모든 포트가 열려 있지 않은 경우 이러한 오류가 종종 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="16e86-126">필요한 포트 목록을 보려면 응용 프로그램 프록시 사용 설명서의 필수 조건 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="16e86-127">사용자 지정 도메인에 대한 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="16e86-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="16e86-128">사용자 지정 도메인을 사용하면 외부 URL의 도메인을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="16e86-129">사용자 지정 도메인을 사용하려면 해당 도메인의 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="16e86-130">사용자 지정 도메인 및 인증서 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="16e86-131">인증서를 업로드하는 데 문제가 발생하는 경우 포털의 오류 메시지에서 인증서 문제에 대한 추가 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16e86-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="16e86-132">인증서의 일반적인 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="16e86-133">만료된 인증서</span><span class="sxs-lookup"><span data-stu-id="16e86-133">Expired certificate</span></span>

-   <span data-ttu-id="16e86-134">자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="16e86-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="16e86-135">개인 키가 없는 인증서</span><span class="sxs-lookup"><span data-stu-id="16e86-135">Certificate is missing the private key</span></span>

<span data-ttu-id="16e86-136">인증서를 업로드하려고 할 때 오류 메시지가 오른쪽 상단 모서리에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="16e86-137">알림 아이콘을 선택하여 오류 메시지를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16e86-137">You can also select the notification icon to see the error messages.</span></span>

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="16e86-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16e86-139">Next steps</span></span>
[<span data-ttu-id="16e86-140">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="16e86-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
