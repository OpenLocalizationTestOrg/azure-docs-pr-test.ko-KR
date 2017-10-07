---
title: "Azure 관리 API 인증서 aaaUpload | Microsoft Docs"
description: "관리 API tooupload 사용자별 hello Azure 클래식 포털에 대 한 인증서는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="b25e3-103">Azure 관리 API Management 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="b25e3-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="b25e3-104">관리 인증서를 사용 하면 tooauthenticate hello 클래식 배포 모델에는 Azure에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="b25e3-105">많은 프로그램 및 도구 (예: Visual Studio 또는 Azure SDK hello) 이러한 인증서 tooautomate 구성 및 다양 한 Azure 서비스의 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="b25e3-106">주의가 필요합니다!</span><span class="sxs-lookup"><span data-stu-id="b25e3-106">Be careful!</span></span> <span data-ttu-id="b25e3-107">모든 사용자가 사용 하 여 인증을 허용 하는 이러한 종류의 인증서는 연결 된 toomanage hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="b25e3-108">Azure 인증서(자체 서명 인증서 포함)에 대한 자세한 내용은 [Azure Cloud Services에 대한 인증서 개요](cloud-services/cloud-services-certs-create.md#what-are-management-certificates)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b25e3-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="b25e3-109">사용할 수도 있습니다 [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) 자동화 목적을 위해 tooauthenticate 클라이언트 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="b25e3-110">관리 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="b25e3-110">Upload a management certificate</span></span>
<span data-ttu-id="b25e3-111">만든 관리 인증서, (hello 공개 키만.cer 파일)를 수행한 hello 포털에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="b25e3-112">Hello 인증서 hello 포털에 표시 되 면 일치 하는 인증서 (개인 키 포함)를 가진 사람이 면 누구나 hello 연결 된 구독에 대 한 hello 관리 API 및 액세스 hello 리소스를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="b25e3-113">Toohello 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="b25e3-114">클릭 **더 많은 서비스** hello 아래 Azure 서비스 목록에서 선택 **구독** hello에 _일반_ 서비스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![구독 메뉴](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="b25e3-116">Tooselect hello tooassociate hello 인증서로 지정 하는 올바른 구독이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="b25e3-117">Hello 올바른 구독을 선택한 후 키를 눌러 **관리 인증서** hello에 _설정을_ 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![설정](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="b25e3-119">키를 눌러 hello **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-119">Press hello **Upload** button.</span></span>

    ![인증서 페이지에 업로드](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="b25e3-121">Hello 대화 정보 및 키를 눌러 입력 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![설정](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="b25e3-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b25e3-123">Next steps</span></span>
<span data-ttu-id="b25e3-124">구독에 연결 된 관리 인증서를가지고 연결할 수 있습니다 (설치한 경우 로컬로 인증서와 일치 하는 hello) 프로그래밍 방식으로 toohello [클래식 배포 모델 REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) 및 자동화 안녕 다양 한 Azure 리소스도 해당 구독과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25e3-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
