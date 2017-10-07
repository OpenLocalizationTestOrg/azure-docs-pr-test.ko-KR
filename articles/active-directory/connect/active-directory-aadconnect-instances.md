---
title: "Azure AD Connect: 서비스 인스턴스 동기화 | Microsoft Docs"
description: "이 페이지에서는 Azure AD 인스턴스에 대한 특별한 고려 사항을 문서화합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="10893-103">Azure AD Connect: 인스턴스에 대한 특별한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="10893-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="10893-104">Azure AD의 전세계 인스턴스 hello와 azure AD Connect은 가장 많이 사용 및 Office 365 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="10893-105">그러나 다른 인스턴스도 있고 URL 및 기타 특별한 고려 사항에 대한 다른 요구 사항을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="10893-106">Microsoft 클라우드 독일</span><span class="sxs-lookup"><span data-stu-id="10893-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="10893-107">hello [Microsoft 클라우드 독일](http://www.microsoft.de/cloud-deutschland) 독일어 데이터 트러스티 운영 되는 전체 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="10893-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="10893-108">프록시 서버에서 Url tooopen</span><span class="sxs-lookup"><span data-stu-id="10893-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="10893-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="10893-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="10893-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="10893-110">\*.windows.net</span></span> |
| <span data-ttu-id="10893-111">+인증서 해지 목록</span><span class="sxs-lookup"><span data-stu-id="10893-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="10893-112">Tooyour Azure AD 테 넌 트에 로그인 할 때 hello onmicrosoft.de 도메인의 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="10893-113">Hello Microsoft 클라우드 독일에 현재 존재 하는 기능은:</span><span class="sxs-lookup"><span data-stu-id="10893-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="10893-114">**Azure AD Connect Health**를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="10893-115">**자동 업데이트**를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="10893-116">**비밀번호 쓰기 저장**은 Azure AD Connect 버전 1.1.570.0 이상에서 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="10893-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="10893-117">다른 Azure AD Premium 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="10893-118">Microsoft Azure Government 클라우드</span><span class="sxs-lookup"><span data-stu-id="10893-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="10893-119">hello [Microsoft Azure Government 클라우드](https://azure.microsoft.com/features/gov/) 미국 정부에 대 한 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="10893-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="10893-120">이 클라우드는 DirSync의 이전 버전에서 지원되어 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="10893-121">Azure AD Connect의 1.1.180 빌드에서 hello 차세대 hello 클라우드 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="10893-122">이 세대 미국 전용 기반된 끝점을 사용 하는 있고 프록시 서버에서 다른 Url tooopen 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="10893-123">프록시 서버에서 Url tooopen</span><span class="sxs-lookup"><span data-stu-id="10893-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="10893-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="10893-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="10893-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="10893-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="10893-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="10893-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="10893-127">+인증서 해지 목록</span><span class="sxs-lookup"><span data-stu-id="10893-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="10893-128">Azure AD Connect 수 없으면 tooautomatically 검색 된 Azure AD 테 넌 트 hello 정부 클라우드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="10893-129">대신 tootake hello Azure AD Connect를 설치할 때 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="10893-130">Hello Azure AD Connect 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="10893-131">Hello 첫 번째 페이지 tooaccept hello EULA는 것을 표시 하는 경우 계속 하지 마십시오 두려면 hello 설치 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="10893-132">Regedit를 시작 하 고 hello 레지스트리 키 변경 `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello 값 `2`합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="10893-133">로 돌아가려면 toohello Azure AD Connect 설치 마법사, hello EULA에 동의 및 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="10893-134">설치 하는 동안 확인 되었는지 toouse hello **사용자 지정 구성** 설치 경로 (및 Express 설치가 아닌).</span><span class="sxs-lookup"><span data-stu-id="10893-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="10893-135">그 hello 설치를 정상적으로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="10893-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="10893-136">현재에 없는 hello Microsoft Azure Government 클라우드 기능:</span><span class="sxs-lookup"><span data-stu-id="10893-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="10893-137">**Azure AD Connect Health**를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="10893-138">**자동 업데이트**를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="10893-139">**비밀번호 쓰기 저장**은 Azure AD Connect 버전 1.1.570.0 이상에서 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="10893-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="10893-140">다른 Azure AD Premium 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10893-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10893-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10893-141">Next steps</span></span>
<span data-ttu-id="10893-142">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="10893-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
