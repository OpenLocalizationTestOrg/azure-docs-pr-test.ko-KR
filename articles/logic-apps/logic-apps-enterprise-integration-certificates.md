---
title: "엔터프라이즈 통합 팩을 사용 하 여 aaaUsing 인증서 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello로 toouse 인증서 하는 방법에 대해 알아봅니다 | Azure 논리 앱"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="b5be3-103">인증서 및 엔터프라이즈 통합 팩에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="b5be3-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="b5be3-104">개요</span><span class="sxs-lookup"><span data-stu-id="b5be3-104">Overview</span></span>
<span data-ttu-id="b5be3-105">엔터프라이즈 통합 인증서 toosecure B2B 통신을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="b5be3-106">엔터프라이즈 통합 앱에서 두 가지 종류의 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="b5be3-107">공용 인증서는 CA(인증 기관)에서 구입해야 합니다</span><span class="sxs-lookup"><span data-stu-id="b5be3-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="b5be3-108">개인 인증서는 직접 발행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="b5be3-109">이 인증서는 참조 된 tooas 자체 서명 된 인증서 때로는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="b5be3-110">인증서란?</span><span class="sxs-lookup"><span data-stu-id="b5be3-110">What are certificates?</span></span>
<span data-ttu-id="b5be3-111">인증서는 전자 통신 hello 참가자의 hello id를 확인 하 고 전자 통신을 보안 하는 디지털 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="b5be3-112">인증서를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="b5be3-112">Why use certificates?</span></span>
<span data-ttu-id="b5be3-113">경우에 따라 B2B 통신을 기밀로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="b5be3-114">엔터프라이즈 통합 두 가지 방법으로 인증서 toosecure 이러한 통신을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="b5be3-115">메시지의 내용을 hello를 암호화 하 여</span><span class="sxs-lookup"><span data-stu-id="b5be3-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="b5be3-116">메시지에 디지털로 서명하여</span><span class="sxs-lookup"><span data-stu-id="b5be3-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="b5be3-117">공용 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="b5be3-117">Upload a public certificate</span></span>

<span data-ttu-id="b5be3-118">toouse는 *공용 인증서* B2B 기능을 사용 하 여 논리 앱을 먼저 통합 계정에 tooupload hello 인증서를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="b5be3-119">사용할 수 있는 toohelp hello에서 해당 속성을 정의 하면 B2B 메시지를 보안 인증서를 업로드 한 후에 [계약](logic-apps-enterprise-integration-agreements.md) 를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="b5be3-120">Toohello Azure 포털에에서 로그인 한 후 통합 계정에 공용 인증서를 업로드 하는 자세한 단계 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="b5be3-121">선택 **더 많은 서비스** 입력 **통합** hello 필터 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="b5be3-122">선택 **통합 계정** hello 결과 목록에서</span><span class="sxs-lookup"><span data-stu-id="b5be3-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="b5be3-123">![찾아보기 선택](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="b5be3-124">Hello 통합 계정 toowhich tooadd hello 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Hello 통합 계정 toowhich tooadd hello 인증서를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="b5be3-126">선택 hello **인증서** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="b5be3-127">![선택 hello 인증서 타일](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="b5be3-128">Hello에 **인증서** 선택 hello 열리면 블레이드 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="b5be3-129">![Hello 추가 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="b5be3-130">입력 한 **이름** 인증서 및으로 선택한 후 hello 인증서 종류에 대 한 **공용** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="b5be3-131">Hello의 hello 오른쪽에서 폴더 아이콘 선택 hello **인증서** 입력란.</span><span class="sxs-lookup"><span data-stu-id="b5be3-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="b5be3-132">Hello 파일 선택기를 열 때 찾아 tooupload tooyour 통합 계정을 지정 하는 hello 인증서 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="b5be3-133">Hello 인증서를 선택한 다음 선택 **확인** hello 파일 선택에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="b5be3-134">유효성을 검사 하 고 hello 인증서 tooyour 통합 계정에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="b5be3-135">Hello에 마지막으로 백업 **인증서 추가** 블레이드, 선택 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="b5be3-136">![Hello 확인 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="b5be3-137">선택 hello **인증서** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="b5be3-138">Hello 인증서를 새로 추가 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="b5be3-139">![Hello 새 인증서를 참조 하십시오.](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="b5be3-140">개인 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="b5be3-140">Upload a private certificate</span></span>

<span data-ttu-id="b5be3-141">toouse는 *개인 인증서* B2B 기능을 사용 하 여 논리 앱을의 개인 인증서 tooyour 통합 계정을 라인 hello 단계를 수행 하 여 업로드할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5be3-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="b5be3-142">[개인 키 tooKey 자격 증명 모음 업로드](../key-vault/key-vault-get-started.md "주요 자격 증명 모음에 알아보기") 설명과 **키 이름**</span><span class="sxs-lookup"><span data-stu-id="b5be3-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="b5be3-143">주요 자격 증명 모음에서 논리 앱 tooperform 작업에 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="b5be3-144">다음 PowerShell 명령을 hello를 사용 하 여 액세스 toohello 논리 앱 서비스 보안 주체에 부여할 수 있습니다.`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="b5be3-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="b5be3-145">Hello 이전 단계를 만든 후에 개인 인증서 toointegration 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="b5be3-146">다음은 Azure 포털 toohello에 로그인 한 후 통합 계정에 개인 인증서를 업로드 하는 자세한 단계를 hello:</span><span class="sxs-lookup"><span data-stu-id="b5be3-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="b5be3-147">Hello 통합 계정 toowhich hello 선택한 tooadd hello 인증서 선택 **인증서** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="b5be3-148">![선택 hello 인증서 타일](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="b5be3-149">Hello에 **인증서** 선택 hello 열리면 블레이드 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="b5be3-150">![Hello 추가 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="b5be3-151">입력 한 **이름** 인증서 및로 선택 hello 인증서 종류에 대 한 **개인** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="b5be3-152">hello hello 오른쪽에 hello 폴더 아이콘을 선택 **인증서** 입력란.</span><span class="sxs-lookup"><span data-stu-id="b5be3-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="b5be3-153">Hello 파일 선택기를 열 때 원하는 tooupload tooyour 통합 계정을 hello 해당 공용 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="b5be3-154">개인 인증서를 추가 하는 동안 반드시 tooadd 해당 공용 인증서의 tooshow [AS2 규약](logic-apps-enterprise-integration-as2.md) 수신 및 송신 설정 hello 메시지 서명 및 암호화에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="b5be3-155">선택 hello **리소스 그룹**, **주요 자격 증명 모음**, **키 이름** 및 선택 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="b5be3-156">![인증서 추가](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="b5be3-157">선택 hello **인증서** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="b5be3-158">Hello 인증서를 새로 추가 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b5be3-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="b5be3-159">![Hello 새 인증서를 참조 하십시오.](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5be3-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="b5be3-160">B2B 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="b5be3-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="b5be3-161">Key Vault에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b5be3-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "주요 자격 증명 모음에 대해 알아보기")  

