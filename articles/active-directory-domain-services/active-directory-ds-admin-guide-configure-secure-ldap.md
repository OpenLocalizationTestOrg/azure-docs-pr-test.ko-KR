---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2dcce-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="2dcce-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="2dcce-104">이 문서에서는 Azure AD 도메인 서비스 관리되는 도메인에 대해 LDAPS(Secure Lightweight Directory Access Protocol)를 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="2dcce-105">보안 LDAP는 'SSL(Secure Sockets Layer)/TLS(Transport Layer Security)를 통한 LDAP(Lightweight Directory Access Protocol)'라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2dcce-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2dcce-106">Before you begin</span></span>
<span data-ttu-id="2dcce-107">이 문서에 나열 된 tooperform hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="2dcce-108">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2dcce-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="2dcce-109">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="2dcce-110">**Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="2dcce-111">그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="2dcce-112">A **인증서 사용 toobe tooenable 보안 LDAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="2dcce-113">**권장** - 신뢰할 수 있는 공용 인증 기관에서 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="2dcce-114">이 구성 옵션은 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="2dcce-115">또는 선택할 수도 있습니다 너무[자체 서명 된 인증서를 만들](#task-1---obtain-a-certificate-for-secure-ldap) 이 문서의 뒷부분에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="2dcce-116">보안 LDAP 인증서 hello에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2dcce-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="2dcce-117">보안 LDAP를 사용 하기 전에 지침을 준수 하는 hello 당 유효한 인증서를 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="2dcce-118">Tooenable 시도 하면 오류가 발생 잘못/잘못 된 인증서로 관리 되는 도메인에 대 한 보안 LDAP 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="2dcce-119">**신뢰할 수 있는 발급자** -hello 인증서 보안 LDAP를 사용 하 여 toohello 관리 되는 도메인을 연결 하는 컴퓨터에서 신뢰할 수 없는 기관에서 발급 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="2dcce-120">이 기관은 이러한 컴퓨터에서 신뢰할 수 있는 공용 인증 기관일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="2dcce-121">**수명** -hello 인증서에 대해 유효 해야 합니다. 적어도 다음 3-6 개월 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="2dcce-122">관리 되는 도메인 보안 LDAP 액세스 tooyour hello 인증서 만료 되 면 중단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="2dcce-123">**주체 이름** -hello hello 인증서 주체 이름이 와일드 카드는 관리 되는 도메인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="2dcce-124">예를 들어 도메인 이름이 'contoso100.com' 이면 hello 인증서의 주체 이름 이어야 합니다 ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="2dcce-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="2dcce-125">Hello DNS 이름 (주체 대체 이름) toothis 와일드 카드 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="2dcce-126">**키 사용** -hello 인증서를 구성 해야 다음 hello를 사용 하는-디지털 서명 및 키 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="2dcce-127">**인증서 용도** -hello 인증서를 SSL 서버 인증에 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="2dcce-128">**엔터프라이즈 인증 기관:** Azure AD Domain Services는 조직의 엔터프라이즈 인증 기관에서 발급한 보안 LDAP 인증서를 사용하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="2dcce-129">이 제한은 hello 서비스 엔터프라이즈 루트 인증 기관으로 CA를 신뢰 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="2dcce-130">작업 1 - 보안 LDAP를 위한 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="2dcce-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="2dcce-131">첫 번째 작업 hello 보안 LDAP 액세스 toohello 관리 되는 도메인에 사용 되는 인증서를 받을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="2dcce-132">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-132">You have two options:</span></span>

* <span data-ttu-id="2dcce-133">인증 기관에서 인증서를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="2dcce-134">hello 기관 공용 인증 기관 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="2dcce-135">자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="2dcce-136">옵션 A(권장) - 인증 기관에서 보안 LDAP 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="2dcce-137">조직이 공용 인증 기관에서 인증서를 입수 하는 경우 해당 공용 인증 기관에서 tooobtain hello 보안 LDAP 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="2dcce-138">설명한 모든 hello 요구 사항을 충족 하는지 확인 인증서를 요청할 때 [hello 보안 LDAP 인증서에 대 한 요구 사항을](#requirements-for-the-secure-ldap-certificate)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="2dcce-139">보안 LDAP를 사용 하 여 tooconnect toohello 관리 되는 도메인을 필요로 하는 클라이언트 컴퓨터는 hello hello 보안 LDAP 인증서 발급자를 신뢰 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="2dcce-140">옵션 B - 보안 LDAP에 대한 자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="2dcce-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="2dcce-141">공용 인증 기관에서 인증서를 toouse 않으려는 경우 선택할 수 있습니다 toocreate 자체 서명 된 인증서 보안 LDAP에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="2dcce-142">**PowerShell을 사용하여 자체 서명된 인증서 만들기**</span><span class="sxs-lookup"><span data-stu-id="2dcce-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="2dcce-143">Windows 컴퓨터에서으로 새 PowerShell 창을 열고 **관리자** 형식 hello toocreate 새 자체 서명 된 인증서를 명령에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="2dcce-144">앞 예제는 hello, 바꿉니다 '*. contoso100.com' 관리 되는 도메인의 hello DNS 도메인 이름으로 합니다. 'Contoso100.onmicrosoft.com' 이라는 관리 되는 도메인을 만든 경우 대체 하는 예를 들어 '*. contoso100.com' 스크립트를 위에 hello에 ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="2dcce-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Azure AD 디렉터리 선택](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="2dcce-146">hello 새로 만든 자체 서명 된 인증서는 hello 로컬 컴퓨터 인증서 저장소에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dcce-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="2dcce-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2dcce-147">Next step</span></span>
[<span data-ttu-id="2dcce-148">작업 2-hello 보안 LDAP 인증서 tooa 내보냅니다. PFX 파일</span><span class="sxs-lookup"><span data-stu-id="2dcce-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
