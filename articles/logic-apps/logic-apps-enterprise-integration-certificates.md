---
title: "<span data-ttu-id=\"c75c5-101\">엔터프라이즈 통합 팩에서 인증서 사용 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"c75c5-101\">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"c75c5-102\">엔터프라이즈 통합 팩에서 인증서를 사용하는 방법 알아보기 | Azure Logic Apps</span><span class=\"sxs-lookup\"><span data-stu-id=\"c75c5-102\">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>"
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
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="c75c5-103">인증서 및 엔터프라이즈 통합 팩에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="c75c5-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="c75c5-104">개요</span><span class="sxs-lookup"><span data-stu-id="c75c5-104">Overview</span></span>
<span data-ttu-id="c75c5-105">엔터프라이즈 통합에서는 인증서를 사용하여 B2B 통신을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="c75c5-106">엔터프라이즈 통합 앱에서 두 가지 종류의 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="c75c5-107">공용 인증서는 CA(인증 기관)에서 구입해야 합니다</span><span class="sxs-lookup"><span data-stu-id="c75c5-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="c75c5-108">개인 인증서는 직접 발행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="c75c5-109">이러한 인증서를 자체 서명된 인증서라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="c75c5-110">인증서란?</span><span class="sxs-lookup"><span data-stu-id="c75c5-110">What are certificates?</span></span>
<span data-ttu-id="c75c5-111">인증서는 전자 통신에서 참가자의 ID를 확인하고 전자 통신을 보호하는 디지털 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="c75c5-112">인증서를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="c75c5-112">Why use certificates?</span></span>
<span data-ttu-id="c75c5-113">경우에 따라 B2B 통신을 기밀로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="c75c5-114">엔터프라이즈 통합에서는 인증서를 사용하여 다음 두 가지 방법으로 이러한 통신을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="c75c5-115">메시지의 콘텐츠를 암호화하여</span><span class="sxs-lookup"><span data-stu-id="c75c5-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="c75c5-116">메시지에 디지털로 서명하여</span><span class="sxs-lookup"><span data-stu-id="c75c5-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="c75c5-117">공용 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="c75c5-117">Upload a public certificate</span></span>

<span data-ttu-id="c75c5-118">B2B 기능이 포함된 논리 앱에서 *공용 인증서* 를 사용하려면 먼저 통합 계정에 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="c75c5-119">인증서를 업로드한 후에는 사용자가 만드는 [규약](logic-apps-enterprise-integration-agreements.md) 에서 해당 속성을 정의할 때 인증서를 사용하여 B2B 메시지를 안전하게 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="c75c5-120">Azure Portal에 로그인한 후 통합 계정에 공용 인증서를 업로드하는 자세한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="c75c5-121">**추가 서비스**를 선택하고 필터 검색 상자에 **통합**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="c75c5-122">결과 목록에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="c75c5-123">![찾아보기 선택](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="c75c5-124">인증서를 추가할 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-124">Select the integration account to which you want to add the certificate.</span></span>  
![인증서를 추가할 통합 계정 선택](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="c75c5-126">**인증서** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="c75c5-127">![인증서 타일 선택](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="c75c5-128">열린 **인증서** 블레이드에서 **추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="c75c5-129">![추가 단추 선택](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="c75c5-130">인증서 **이름**을 입력한 다음 드롭다운에서 인증서 유형을 **공용**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="c75c5-131">**인증서** 텍스트 상자의 오른쪽에서 폴더 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="c75c5-132">파일 선택기가 열리면 통합 계정에 업로드하려는 인증서 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="c75c5-133">인증서를 선택한 다음 파일 선택기에서 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="c75c5-134">그러면 인증서의 유효성을 검사하고 통합 계정에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="c75c5-135">마지막으로, 다시 **인증서 추가** 블레이드로 돌아와서 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="c75c5-136">![확인 단추 선택](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="c75c5-137">**인증서** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="c75c5-138">새로 추가된 인증서가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="c75c5-139">![새 인증서가 보임](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="c75c5-140">개인 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="c75c5-140">Upload a private certificate</span></span>

<span data-ttu-id="c75c5-141">B2B 기능과 함께 Logic Apps에서 *개인 인증서*를 사용하려면 다음 단계를 수행하여 통합 계정으로 개인 인증ㅇ서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="c75c5-142">[개인 키를 Key Vault에 업로드](../key-vault/key-vault-get-started.md "Key Vault에 대해 알아보기") 및 **키 이름** 입력</span><span class="sxs-lookup"><span data-stu-id="c75c5-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="c75c5-143">Logic Apps에 Key Vault에서 작업을 수행할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="c75c5-144">다음 PowerShell 명령을 사용하여 Logic Apps 서비스 주체에 대한 액세스 권한을 부여할 수 있습니다. `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="c75c5-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="c75c5-145">이전 단계를 수행한 후 통합 계정에 개인 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="c75c5-146">Azure Portal에 로그인한 후 통합 계정에 개인 인증서를 업로드하는 자세한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="c75c5-147">인증서를 추가할 통합 계정을 선택하고 **인증서** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="c75c5-148">![인증서 타일 선택](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="c75c5-149">열린 **인증서** 블레이드에서 **추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="c75c5-150">![추가 단추 선택](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="c75c5-151">인증서 **이름**을 입력하고, 드롭다운에서 인증서 유형을 **개인**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="c75c5-152">**인증서** 텍스트 상자의 오른쪽에서 폴더 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="c75c5-153">파일 선택기가 열리면 통합 계정에 업로드하려는 해당 공용 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="c75c5-154">개인 인증서를 추가할 때 메시지를 서명하고 암호화하는 [AS2 규약](logic-apps-enterprise-integration-as2.md) 수신 및 송신 설정에 나타나도록 해당 공용 인증서를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="c75c5-155">**리소스 그룹**, **Key Vault**, **키 이름**을 차례로 선택하고 **확인** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="c75c5-156">![인증서 추가](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="c75c5-157">**인증서** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="c75c5-158">새로 추가된 인증서가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c75c5-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="c75c5-159">![새 인증서가 보임](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c75c5-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="c75c5-160">B2B 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="c75c5-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="c75c5-161">Key Vault에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="c75c5-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "주요 자격 증명 모음에 대해 알아보기")  

