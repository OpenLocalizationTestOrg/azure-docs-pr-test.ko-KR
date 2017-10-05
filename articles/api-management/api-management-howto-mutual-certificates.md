---
title: "클라이언트 인증서 인증을 사용하여 백 엔드 서비스 보호 - Azure API Management | Microsoft Docs"
description: "Azure API 관리에서 클라이언트 인증서 인증을 사용하여 백 엔드 서비스를 보호하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="fc386-103">Azure API 관리에서 클라이언트 인증서 인증을 사용하여 백 엔드 서비스를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="fc386-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="fc386-104">API 관리에서는 클라이언트 인증서를 사용하여 API의 백 엔드 서비스에 대한 액세스를 보호하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="fc386-105">이 가이드에서는 API 게시자 포털에서 인증서를 관리하는 방법과 인증서를 사용하여 백 엔드 서비스에 액세스하도록 API를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="fc386-106">API Management REST API를 사용하여 인증서를 관리하는 방법에 대한 자세한 내용은 [Azure API Management REST API 인증서 엔터티][Azure API Management REST API Certificate entity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc386-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="fc386-107"><a name="prerequisites"> </a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc386-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="fc386-108">이 가이드에서는 클라이언트 인증서 인증을 사용하여 API의 백 엔드 서비스에 액세스하도록 API 관리 서비스 인스턴스를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="fc386-109">이 항목의 단계를 수행하기 전에 클라이언트 인증서 인증을 사용하도록 백 엔드 서비스를 구성해야 하며([Azure Websites에서 인증서 인증을 구성하려면 이 문서 참조][to configure certificate authentication in Azure WebSites refer to this article]) API Management 게시자 포털에서 업로드할 인증서 및 해당 인증서의 암호에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="fc386-110"><a name="step1"> </a>클라이언트 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="fc386-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="fc386-111">시작하려면 Azure Portal에서 API Management 서비스에 대한 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="fc386-112">API 관리 게시자 포털로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-112">This takes you to the API Management publisher portal.</span></span>

![API 게시자 포털][api-management-management-console]

> <span data-ttu-id="fc386-114">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc386-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="fc386-115">왼쪽의 **API Management** 메뉴에서 **보안**을 클릭하고 **클라이언트 인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![클라이언트 인증서][api-management-security-client-certificates]

<span data-ttu-id="fc386-117">새 인증서를 업로드하려면 **인증서 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-117">To upload a new certificate, click **Upload certificate**.</span></span>

![인증서 업로드][api-management-upload-certificate]

<span data-ttu-id="fc386-119">인증서를 찾은 다음 인증서의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="fc386-120">인증서는 **.pfx** 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="fc386-121">자체 서명된 인증서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-121">Self-signed certificates are allowed.</span></span>
> 
> 

![인증서 업로드][api-management-upload-certificate-form]

<span data-ttu-id="fc386-123">**업로드** 를 클릭하여 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="fc386-124">이때 인증서 암호의 유효성을 검사하여</span><span class="sxs-lookup"><span data-stu-id="fc386-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="fc386-125">암호가 잘못된 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![업로드된 인증서][api-management-certificate-uploaded]

<span data-ttu-id="fc386-127">업로드된 인증서는 **클라이언트 인증서** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="fc386-128">인증서가 여러 개인 경우 제목이나 지문의 마지막 4자를 적어 둡니다. 이러한 항목은 인증서를 사용하도록 API를 구성할 때 인증서를 선택하는 데 사용됩니다. 여기에 대해서는 다음 섹션인 [게이트웨이 인증에 클라이언트 인증서를 사용하도록 API 구성][Configure an API to use a client certificate for gateway authentication]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="fc386-129">사용하는 경우 인증서 체인 유효성 검사를 해제하려면(예: 자체 서명된 인증서) 이 FAQ [항목](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="fc386-130"><a name="step1a"> </a>클라이언트 인증서 삭제</span><span class="sxs-lookup"><span data-stu-id="fc386-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="fc386-131">인증서를 삭제하려면 원하는 인증서 옆에 있는 **삭제** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![인증서 삭제][api-management-certificate-delete]

<span data-ttu-id="fc386-133">**예, 삭제합니다.** 를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-133">Click **Yes, delete it** to confirm.</span></span>

![삭제 확인][api-management-confirm-delete]

<span data-ttu-id="fc386-135">인증서를 API에서 사용하고 있는 경우 경고 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="fc386-136">이러한 인증서를 삭제하려면 먼저 해당 인증서를 사용하도록 구성된 API에서 인증서를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![삭제 확인][api-management-confirm-delete-policy]

## <span data-ttu-id="fc386-138"><a name="step2"> </a>게이트웨이 인증에 클라이언트 인증서를 사용하도록 API 구성</span><span class="sxs-lookup"><span data-stu-id="fc386-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="fc386-139">왼쪽의 **API Management** 메뉴에서 **API**를 클릭하고 원하는 API의 이름을 클릭한 후에 **보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![API 보안][api-management-api-security]

<span data-ttu-id="fc386-141">**자격 증명 사용** 드롭다운 목록에서 **클라이언트 인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![클라이언트 인증서][api-management-mutual-certificates]

<span data-ttu-id="fc386-143">**클라이언트 인증서** 드롭다운 목록에서 원하는 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="fc386-144">인증서가 여러 개이면 이전 섹션에서 적어 둔 제목이나 지문의 마지막 4자를 통해 올바른 인증서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![인증서 선택][api-management-select-certificate]

<span data-ttu-id="fc386-146">**저장** 을 클릭하여 API에 대한 구성 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="fc386-147">이 변경 내용은 즉시 적용되며 해당 API의 작업 호출은 인증서를 사용하여 백 엔드 서버에서 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![API 변경 내용 저장][api-management-save-api]

> <span data-ttu-id="fc386-149">API의 백 엔드 서비스에 대해 게이트웨이 인증을 위해 지정된 인증서는 해당 API의 정책에 포함되며 정책 편집기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc386-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![인증서 정책][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="fc386-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc386-151">Next steps</span></span>
<span data-ttu-id="fc386-152">HTTP 기본 또는 공유 암호 인증과 같은 백 엔드 서비스를 보호하는 다른 방법에 대한 자세한 내용은 다음 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc386-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



