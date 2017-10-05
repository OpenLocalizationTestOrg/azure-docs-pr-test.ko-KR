---
title: "Azure AD 페더레이션 메타데이터 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory가 Azure Active Directory 토큰을 수락하는 서비스에 대해 게시하는 페더레이션 메타데이터 문서를 설명합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="50f53-103">페더레이션 메타데이터</span><span class="sxs-lookup"><span data-stu-id="50f53-103">Federation metadata</span></span>
<span data-ttu-id="50f53-104">Azure Active Directory(Azure AD)는 Azure AD가 발급하는 보안 토큰을 수락하도록 구성된 서비스에 대한 페더레이션 메타데이터 문서를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="50f53-105">페더레이션 메타데이터 문서 형식은 [Web Services Federation Language(WS-Federation) 버전 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)에서 설명하며, [OASIS SAML(Security Assertion Markup Language) v2.0의 메타데이터](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf)를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="50f53-106">테넌트별 및 테넌트에 독립적인 메타데이터 끝점</span><span class="sxs-lookup"><span data-stu-id="50f53-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="50f53-107">Azure AD 테넌트별 및 테넌트 독립적 끝점을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="50f53-108">테넌트별 끝점은 특정 테넌트에 대해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="50f53-109">테넌트별 페더레이션 메타데이터에는 테넌트별 발급자 및 끝점 정보를 포함하는 테넌트에 관한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="50f53-110">테넌트별 끝점을 사용하는 단일 테넌트에 대한 액세스를 제한하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="50f53-111">테넌트 독립적 끝점은 모든 Azure AD 테넌트에 공통된 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="50f53-112">이 정보는 *login.microsoftonline.com* 에서 호스트되는 테넌트에 적용되며 테넌트 간에 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="50f53-113">테넌트 독립적 끝점은 특정 테넌트와 연결되어있지 않으므로 다중 테넌트 응용 프로그램에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="50f53-114">페더레이션 메타데이터 끝점</span><span class="sxs-lookup"><span data-stu-id="50f53-114">Federation metadata endpoints</span></span>
<span data-ttu-id="50f53-115">Azure AD는 페더레이션 메타데이터를 `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="50f53-116">**테넌트별 끝점**의 경우, `TenantDomainName`은(는) 다음 유형 중 하나가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="50f53-117">Azure AD 테넌트의 등록된 도메인 이름, 예: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="50f53-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="50f53-118">도메인의 변경할 수 없는 ID, 예: `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="50f53-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="50f53-119">**테넌트에 독립적인 끝점**의 경우 `TenantDomainName`은(는) `common`입니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="50f53-120">이 문서는 login.microsoftonline.com에서 호스트되는 모든 Azure AD 테넌트에 공통된 페더레이션 메타데이터 요소만을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="50f53-121">예를 들어, 테넌트별 끝점은 `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="50f53-122">테넌트 독립적 끝점은 [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml)입니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="50f53-123">브라우저에서 이 URL을 입력하여 페더레이션 메타데이터 문서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="50f53-124">페더레이션 메타데이터의 내용</span><span class="sxs-lookup"><span data-stu-id="50f53-124">Contents of federation Metadata</span></span>
<span data-ttu-id="50f53-125">다음 섹션에는 Azure AD에서 발급한 토큰을 사용하는 서비스에 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="50f53-126">엔터티 ID</span><span class="sxs-lookup"><span data-stu-id="50f53-126">Entity ID</span></span>
<span data-ttu-id="50f53-127">`EntityDescriptor` 요소는 `EntityID` 특성을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="50f53-128">`EntityID` 특성의 값은 발급자, 즉, 토큰을 발행한 보안 토큰 서비스(STS)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="50f53-129">토큰을 받을 때 발급자 유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="50f53-130">다음 메타데이터는 `EntityID` 요소가 있는 샘플 테넌트별 `EntityDescriptor` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="50f53-131">테넌트 독립적 끝점의 테넌트 ID를 사용자의 테넌트 ID로 바꾸어 테넌트별 `EntityID` 값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="50f53-132">결과 값은 토큰 발급자와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="50f53-133">이 전략을 통해 다중 테넌트 응용 프로그램이 지정된 테넌트에 대한 발급자의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="50f53-134">다음 메타데이터는 샘플 테넌트 독립적 `EntityID` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="50f53-135">`{tenant}` 는 자리 표시자가 아니라 문자 그대로의 의미를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="50f53-136">토큰 서명 인증서</span><span class="sxs-lookup"><span data-stu-id="50f53-136">Token signing certificates</span></span>
<span data-ttu-id="50f53-137">서비스는 Azure AD 테넌트에서 발급한 토큰을 받으면, 페더레이션 메타데이터 문서에 게시된 서명 키로 토큰의 서명  유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="50f53-138">페더레이션 메타데이터는 테넌트를 토큰 서명에 사용하는 인증서의 공개 부분을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="50f53-139">인증서 원시 바이트는 `KeyDescriptor` 요소에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="50f53-140">토큰 서명 인증서는 `use` 특성의 값이 `signing`인 경우의 서명에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="50f53-141">Azure AD를 통해 게시된 페더레이션 메타데이터 문서에는 Azure AD가 서명 인증서 업데이트를 준비하는 경우와 같은 여러 서명 키가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="50f53-142">페더레이션 메타데이터 문서가 둘 이상의 인증서를 포함하는 경우, 토큰의 유효성을 검사하는 서비스는 문서에서 모든 인증서를 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="50f53-143">다음 메타데이터는 서명 키가 있는 샘플 `KeyDescriptor` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

<span data-ttu-id="50f53-144">`KeyDescriptor` 요소는 페더레이션 메타데이터 문서에서 WS-Federation 관련 섹션 및 SAML 관련 섹션의 두 곳에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="50f53-145">두 섹션 모두에서 게시된 인증서는 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="50f53-146">WS-Federation 관련 섹션에서 WS-Federation 메타데이터 판독기는 `SecurityTokenServiceType` 형식을 가진 `RoleDescriptor` 요소에서 인증서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="50f53-147">다음 메타데이터는 샘플 `RoleDescriptor` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="50f53-148">SAML 관련 섹션에서 WS-Federation 메타데이터 판독기는 `IDPSSODescriptor` 요소에서 인증서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="50f53-149">다음 메타데이터는 샘플 `IDPSSODescriptor` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="50f53-150">테넌트 관련 및 테넌트 독립적 인증서의 형식에는 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="50f53-151">WS-Federation 끝점 URL</span><span class="sxs-lookup"><span data-stu-id="50f53-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="50f53-152">페더레이션 메타데이터는 WS-Federation 프로토콜에서 단일 로그인 및 단일 로그 아웃에 Azure AD가 사용하는 URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="50f53-153">이 끝점이 `PassiveRequestorEndpoint` 요소에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="50f53-154">다음 메타데이터는 테넌트별 끝점에 대한 샘플 `PassiveRequestorEndpoint` 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="50f53-155">테넌트 독립적 끝점의 경우, 다음 예제와 같이 WS-Federation URL은 WS-Federation 끝점에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="50f53-156">SAML 프로토콜 끝점 URL</span><span class="sxs-lookup"><span data-stu-id="50f53-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="50f53-157">페더레이션 메타데이터는 SAML 2.0 프로토콜에서 단일 로그인 및 단일 로그아웃에 Azure AD가 사용하는 URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="50f53-158">이 끝점은 `IDPSSODescriptor` 요소에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="50f53-159">로그인 및 로그아웃 URL은 `SingleSignOnService` 및 `SingleLogoutService` 요소에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="50f53-160">다음 메타데이터는 테넌트별 끝점에 대한 샘플 `PassiveResistorEndpoint` 를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="50f53-161">마찬가지로 다음 샘플과 같이 일반 SAML 2.0 프로토콜 끝점에 대한 끝점은 테넌트 독립적 페더레이션 메타데이터에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f53-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
