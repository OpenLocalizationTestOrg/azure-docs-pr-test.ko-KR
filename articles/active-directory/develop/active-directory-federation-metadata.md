---
title: "AD aaaAzure 페더레이션 메타 데이터 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory 토큰을 수락 하는 서비스에 대 한 Azure Active Directory에서 게시 하는 hello 페더레이션 메타 데이터 문서를 설명 합니다."
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
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="e7fda-103">페더레이션 메타데이터</span><span class="sxs-lookup"><span data-stu-id="e7fda-103">Federation metadata</span></span>
<span data-ttu-id="e7fda-104">Azure Active Directory (Azure AD) 서비스를 구성할 Azure AD에서 발행 하는 tooaccept hello 보안 토큰에 대 한 페더레이션 메타 데이터 문서를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="e7fda-105">hello 페더레이션 메타 데이터 문서 형식에 명시 된 hello [웹 서비스 페더레이션 언어 (Ws-federation) 버전 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)를 확장 하는 [hello OASIS SAML Security Assertion Markup Language ()에 대 한 메타 데이터 v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="e7fda-106">테넌트별 및 테넌트에 독립적인 메타데이터 끝점</span><span class="sxs-lookup"><span data-stu-id="e7fda-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="e7fda-107">Azure AD 테넌트별 및 테넌트 독립적 끝점을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="e7fda-108">테넌트별 끝점은 특정 테넌트에 대해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="e7fda-109">hello 테 넌 트 별 페더레이션 메타 데이터에는 hello 테 넌 트, 테 넌 트 별 발급자 및 끝점 정보를 포함 하는 방법에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="e7fda-110">응용 프로그램 액세스 tooa 단일 테 넌 트를 제한 하는 테 넌 트 별 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="e7fda-111">테 넌 트 독립적 끝점은 일반적인 tooall Azure AD 테 넌 트 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="e7fda-112">이 정보에는에서 호스팅되는 tootenants 적용 됩니다. *login.microsoftonline.com* 되며 테 넌 트 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="e7fda-113">테넌트 독립적 끝점은 특정 테넌트와 연결되어있지 않으므로 다중 테넌트 응용 프로그램에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="e7fda-114">페더레이션 메타데이터 끝점</span><span class="sxs-lookup"><span data-stu-id="e7fda-114">Federation metadata endpoints</span></span>
<span data-ttu-id="e7fda-115">Azure AD는 페더레이션 메타데이터를 `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="e7fda-116">에 대 한 **테 넌 트 별 끝점**, hello `TenantDomainName` 유형만 hello 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="e7fda-117">Azure AD 테넌트의 등록된 도메인 이름, 예: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="e7fda-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="e7fda-118">변경할 수 없는 hello hello 도메인의 ID 같은 테 넌 `72f988bf-86f1-41af-91ab-2d7cd011db45`합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="e7fda-119">에 대 한 **테 넌 트 독립적 끝점**, hello `TenantDomainName` 은 `common`합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="e7fda-120">이 문서는 있는 일반적인 tooall Azure AD 테 넌 트 login.microsoftonline.com에서 호스트 되는 페더레이션 메타 데이터 요소만 hello를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="e7fda-121">예를 들어, 테넌트별 끝점은 `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="e7fda-122">hello 테 넌 트 독립적 끝점은 [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="e7fda-123">브라우저에서이 URL을 입력 하 여 hello 페더레이션 메타 데이터 문서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="e7fda-124">페더레이션 메타데이터의 내용</span><span class="sxs-lookup"><span data-stu-id="e7fda-124">Contents of federation Metadata</span></span>
<span data-ttu-id="e7fda-125">hello 다음 섹션에서는 Azure AD에서 발급 한 hello 토큰을 사용 하는 서비스에 필요한 정보.</span><span class="sxs-lookup"><span data-stu-id="e7fda-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="e7fda-126">엔터티 ID</span><span class="sxs-lookup"><span data-stu-id="e7fda-126">Entity ID</span></span>
<span data-ttu-id="e7fda-127">hello `EntityDescriptor` 요소를 포함 한 `EntityID` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="e7fda-128">값의 hello hello `EntityID` hello 발급자를 나타내는 특성, 즉, hello 보안 토큰 서비스 (STS) hello 발급 된 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="e7fda-129">토큰을 받을 때의 중요 한 toovalidate hello 발급자입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="e7fda-130">hello 다음과 같은 메타 데이터를 보여줍니다. 테 넌 트 별 `EntityDescriptor` 인 요소는 `EntityID` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="e7fda-131">테 넌 트 특정 테 넌 트 ID toocreate로 hello 테 넌 트 독립적 끝점의 hello 테 넌 트 ID를 바꿀 수 있습니다 `EntityID` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="e7fda-132">hello 결과 값 토큰 발급자 hello와 동일를 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="e7fda-133">hello 전략 지정된 테 넌 트에 대 한 다중 테 넌 트 응용 프로그램 toovalidate hello 발급자를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="e7fda-134">hello 다음과 같은 메타 데이터를 보여줍니다. 테 넌 트 독립적 `EntityID` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="e7fda-135">유의 하십시오 해당 hello `{tenant}` 는 리터럴, 자리 표시자에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="e7fda-136">토큰 서명 인증서</span><span class="sxs-lookup"><span data-stu-id="e7fda-136">Token signing certificates</span></span>
<span data-ttu-id="e7fda-137">서비스가 Azure AD 테 넌 트에서 발급 된 토큰을 받으면 hello hello 토큰의 서명은 유효성을 검사 해야 hello 페더레이션 메타 데이터 문서에 게시 된 서명 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="e7fda-138">hello 페더레이션 메타 데이터는 hello hello 테 넌 트가 토큰 서명에 사용 하는 hello 인증서의 공개 부분을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="e7fda-139">hello에 hello 인증서 원시 바이트 표시 `KeyDescriptor` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="e7fda-140">hello 값 때 hello만 서명에 대 한 hello 토큰 서명 인증서가 유효한 `use` 특성은 `signing`합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="e7fda-141">Azure AD에서 게시 한 페더레이션 메타 데이터 문서는 Azure AD는 tooupdate hello 서명 인증서를 준비 하는 경우 등의 여러 서명 키를 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="e7fda-142">페더레이션 메타 데이터 문서에서 둘 이상의 인증서를 포함 하는 경우 hello 토큰의 유효성 검사 하는 서비스는 hello 문서에서 모든 인증서를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="e7fda-143">hello 다음과 같은 메타 데이터를 보여줍니다. `KeyDescriptor` 서명 키가 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="e7fda-144">hello `KeyDescriptor` 요소 hello 페더레이션 메타 데이터 문서; hello WS-페더레이션 관련 섹션과 SAML 관련 hello 섹션에 있는 두 위치에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="e7fda-145">두 섹션 모두에서 게시 된 hello 인증서는 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="e7fda-146">Hello WS-페더레이션 관련 섹션에서 Ws-federation 메타 데이터 판독기 hello 인증서를 읽을 것을 `RoleDescriptor` hello로 요소 `SecurityTokenServiceType` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="e7fda-147">hello 다음과 같은 메타 데이터를 보여줍니다. `RoleDescriptor` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="e7fda-148">Hello SAML 관련 섹션에서 Ws-federation 메타 데이터 판독기 hello 인증서를 읽을 것을 `IDPSSODescriptor` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="e7fda-149">hello 다음과 같은 메타 데이터를 보여줍니다. `IDPSSODescriptor` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="e7fda-150">테 넌 트 별 끝점과 테 넌 트 독립적 인증서의 hello 형식에는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="e7fda-151">WS-Federation 끝점 URL</span><span class="sxs-lookup"><span data-stu-id="e7fda-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="e7fda-152">hello 페더레이션 메타 데이터 URL을 Azure AD single sign-in 및 single sign-out에 Ws-federation 프로토콜에 대 한 사용 하 여 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="e7fda-153">이 끝점에서 hello 표시 `PassiveRequestorEndpoint` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="e7fda-154">hello 다음과 같은 메타 데이터를 보여줍니다. `PassiveRequestorEndpoint` 테 넌 트 별 끝점에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="e7fda-155">Hello 테 넌 트 독립적 끝점에 대 한 hello Ws-federation URL hello 다음 예제와 같이 hello Ws-federation 끝점에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="e7fda-156">SAML 프로토콜 끝점 URL</span><span class="sxs-lookup"><span data-stu-id="e7fda-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="e7fda-157">페더레이션 메타 데이터 hello single sign-in 및 single sign-out SAML 2.0 프로토콜에 대 한 Azure AD를 사용 하는 hello URL을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="e7fda-158">Hello에 이러한 끝점 표시 `IDPSSODescriptor` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="e7fda-159">hello에 나타나는 hello 로그인 및 로그 아웃 `SingleSignOnService` 및 `SingleLogoutService` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="e7fda-160">hello 다음과 같은 메타 데이터를 보여줍니다. `PassiveResistorEndpoint` 테 넌 트 별 끝점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="e7fda-161">마찬가지로 공통 SAML 2.0 프로토콜 끝점 hello에 대 한 hello 끝점 hello 다음 예제와 같이 hello 테 넌 트 독립적 페더레이션 메타 데이터에 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7fda-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
