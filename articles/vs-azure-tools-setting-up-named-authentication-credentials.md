---
title: "명명 된 인증 자격 증명 aaaSetting | Microsoft Docs"
description: "어떻게 tootooprovide 자격 증명을 Visual Studio에서 Visual Studio 또는 기존 toomonitor는 응용 프로그램 tooAzure tooauthenticate 요청 tooAzure toopublish를 사용할 수 있는 클라우드 서비스에 알아봅니다. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="b273a-103">명명된 인증 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="b273a-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="b273a-104">Visual Studio 또는 toomonitor 기존 클라우드 서비스는 응용 프로그램 tooAzure toopublish 자격 증명을 제공 해야 tooAzure 요청 Visual Studio가 tooauthenticate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="b273a-105">몇 가지 방법으로 로그인 할 수 있는 tooprovide에 이러한 자격 증명으로 Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="b273a-106">예를 들어 hello 서버 탐색기에서에서 열면 hello에 대 한 바로 가기 메뉴를 hello **Azure** 노드 선택 **tooMicrosoft Azure 구독 연결 중...** . 에 로그인 할 때 hello 구독 정보를 Azure 계정과 연결 된 Visual Studio에서 사용할 수 있으며 toodo 있는 더 많은 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="b273a-107">또한 azure Tools hello 구독 파일 (.publishsettings 파일)를 사용 하 여 자격 증명을 제공 하는 이전 방법인을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="b273a-108">이 항목에서는 Azure SDK 2.2에서 여전히 지원되는 이 메서드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="b273a-109">다음 항목 hello는 인증 tooAzure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="b273a-110">구독 ID</span><span class="sxs-lookup"><span data-stu-id="b273a-110">Your subscription ID</span></span>
* <span data-ttu-id="b273a-111">유효한 X.509 v3 인증서</span><span class="sxs-lookup"><span data-stu-id="b273a-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="b273a-112">hello hello X.509 v3 인증서 키 길이가 2048 비트 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="b273a-113">Azure는 이 요구 사항을 충족하지 않거나 올바르지 않은 모든 인증서를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="b273a-114">Visual Studio에서는 자격 증명으로 hello 인증서 데이터와 함께 구독 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="b273a-115">hello 적절 한 자격 증명 hello 인증서에 대 한 공개 키를 포함 하는 hello 구독 파일 (.publishsettings 파일)에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="b273a-116">hello 구독 파일에는 하나 이상의 구독에 대 한 자격 증명 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="b273a-117">Hello에서 hello 구독 정보를 편집할 수 **새로 만들기/편집 구독** 대화 상자에서이 항목의 뒷부분에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="b273a-118">원할 경우 toocreate 인증서를 직접의 toohello 지침을 참조할 수 있습니다 [Azure 용 관리 인증서 만들기 및 업로드](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) hello 인증서 toohello를 수동으로 업로드 하 고 [Azure 클래식 포털 ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="b273a-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="b273a-119">Visual Studio 클라우드 서비스가 아닌 toomanage 필요한 이러한 자격 증명 필요 tooauthenticate 사용 되는 동일한 자격 증명 hello Azure 저장소 서비스에 대 한 요청을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="b273a-120">Visual Studio에서 인증 자격 증명 가져오기, 설정 또는 편집</span><span class="sxs-lookup"><span data-stu-id="b273a-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="b273a-121">가져오기, 설정 하거나 hello에서 인증 자격 증명을 수정할 수 있습니다 **새 구독** hello 다음 작업을 수행 하는 경우 표시 되는 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="b273a-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="b273a-122">**서버 탐색기**개방형 hello에 대 한 바로 가기 메뉴를 hello **Azure** 노드를 선택 **구독 관리 및 필터링...** , hello 선택 **인증서** 탭을 hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="b273a-123">선택 **가져올** tooopen hello Microsoft Azure 구독 가져오기 대화 상자를 현재 hello에 대 한 hello 구독 파일을 다운로드할 수 있는 구독을 로드, 찾아보기 tooits 위치를 다운로드 한 다음에서 사용 하기 위해 가져옵니다 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="b273a-124">선택 **새로** tooopen hello 새 등록 대화 상자를 인증에 사용 하기 위해 새 구독을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="b273a-125">선택 **편집** (활성 구독을 선택) 이후 tooopen hello 등록 편집 대화 상자를 인증에 사용 하기 위해 기존 구독을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="b273a-126">hello 다음 절차에서는 가정 해당 hello **새 구독** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="b273a-127">Visual Studio에서 인증 자격 증명을 tooset</span><span class="sxs-lookup"><span data-stu-id="b273a-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="b273a-128">Hello에 **기존 인증서 선택** 인증 목록에 대 한 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="b273a-129">Hello 선택 **hello 전체 경로 복사** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="b273a-130">hello hello 인증서 (.cer 파일)에 대 한 경로가 클립보드 toohello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b273a-131">toopublish Azure 응용 프로그램 Visual Studio에서이 인증서 toohello 업로드 해야 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="b273a-132">tooupload hello 인증서 toohello Azure 포털:</span><span class="sxs-lookup"><span data-stu-id="b273a-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="b273a-133">열기 hello [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="b273a-134">메시지가 표시 되 면 toohello 포털에 로그인 한 다음 너무를 탐색**설정**, **관리 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="b273a-135">Hello 관리 인증서 창에서 선택 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="b273a-136">Azure 구독을 만든 hello 방금 hello.cer 파일의 전체 경로 붙여 넣고 선택 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b273a-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
