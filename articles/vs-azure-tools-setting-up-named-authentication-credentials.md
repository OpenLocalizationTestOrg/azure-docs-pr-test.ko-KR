---
title: "명명된 인증 자격 증명 설정 | Microsoft Docs"
description: "Visual Studio가 사용할 수 있는 자격 증명을 제공하여 Azure에 대한 요청을 인증하고 응용 프로그램을 Visual Studio에서 Azure로 게시하거나 기존 클라우드 서비스를 모니터링하는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="3fb8c-103">명명된 인증 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="3fb8c-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="3fb8c-104">Visual Studio에서 Azure에 응용 프로그램을 게시하거나 기존 클라우드 서비스를 모니터링하려면 Visual Studio에서 Azure에 대한 요청을 인증하는 데 사용할 수 있는 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="3fb8c-105">이러한 자격 증명을 제공하기 위해 로그인 할 수 있는 Visual Studio의 여러 위치 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="3fb8c-106">예를 들어 서버 탐색기에서 **Azure** 노드에 대한 바로 가기 메뉴를 열고 **Microsoft Azure 구독에 연결...**을 선택할 수 있습니다. 로그인할 때 Azure 계정에 연결된 구독 정보를 Visual Studio에서 사용할 수 있으며 아무 작업도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="3fb8c-107">또한 Azure 도구는 구독 파일(.publishsettings 파일)을 사용하여 자격 증명을 제공하는 이전 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="3fb8c-108">이 항목에서는 Azure SDK 2.2에서 여전히 지원되는 이 메서드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="3fb8c-109">Azure에서 인증을 받으려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="3fb8c-110">구독 ID</span><span class="sxs-lookup"><span data-stu-id="3fb8c-110">Your subscription ID</span></span>
* <span data-ttu-id="3fb8c-111">유효한 X.509 v3 인증서</span><span class="sxs-lookup"><span data-stu-id="3fb8c-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="3fb8c-112">X.509 v3 인증서 키의 길이는 2048비트 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="3fb8c-113">Azure는 이 요구 사항을 충족하지 않거나 올바르지 않은 모든 인증서를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="3fb8c-114">Visual Studio는 자격 증명으로 인증서 데이터와 함께 구독 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="3fb8c-115">적절한 자격 증명은 인증서에 대한 공용 키가 포함된 구독 파일(.publishsettings 파일)에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="3fb8c-116">구독 파일에는 둘 이상의 구독에 대한 자격 증명이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="3fb8c-117">이 항목의 뒷부분에 설명된 대로 **구독 새로 만들기/편집** 대화 상자에서 구독 정보를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="3fb8c-118">인증서를 만들려는 경우 [Azure용 관리 인증서 만들기 및 업로드](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx)에서 지침을 참조한 다음 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에 수동으로 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="3fb8c-119">Visual Studio에서 클라우드 서비스를 관리해야 하는 이러한 자격 증명은 Azure 저장소 서비스에 대한 요청을 인증하는데 필요한 자격 증명과 동일하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="3fb8c-120">Visual Studio에서 인증 자격 증명 가져오기, 설정 또는 편집</span><span class="sxs-lookup"><span data-stu-id="3fb8c-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="3fb8c-121">다음 작업을 수행하는 경우 나타나는 **새 구독** 대화 상자에서 인증 자격 증명을 가져오거나 설정하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="3fb8c-122">**서버 탐색기**에서 **Azure** 노드에 대한 바로 가기 메뉴를 열어 **구독 관리 및 필터링...**를 선택하고, **인증서** 탭을 선택한 후 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="3fb8c-123">**가져오기**를 선택하여 현재 로드된 구독에 대한 구독 파일을 다운로드할 수 있는 Microsoft Azure 구독 가져오기 대화 상자를 열고 다운로드 위치로 이동한 후 인증에 사용할 수 있게 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="3fb8c-124">**새로 만들기**를 선택하여 인증에서 사용하기 위해 새 구독을 설정할 수 있는 새 구독 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="3fb8c-125">활성 구독을 선택한 후 **편집**을 선택하여 인증에서 사용하기 위해 기존 구독을 편집할 수 있는 구독 편집 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="3fb8c-126">다음 절차는 **새 구독** 대화 상자가 열려 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="3fb8c-127">Visual Studio에서 인증 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="3fb8c-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="3fb8c-128">인증 목록에 대한 **기존 인증서 선택** 에서 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="3fb8c-129">**전체 경로 복사** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="3fb8c-130">인증서(.cer 파일)에 대한 경로가 클립보드에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3fb8c-131">Visual Studio에서 Azure 응용 프로그램을 게시하려면 [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 이 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="3fb8c-132">Azure Portal에 인증서를 업로드하려면:</span><span class="sxs-lookup"><span data-stu-id="3fb8c-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="3fb8c-133">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="3fb8c-134">메시지가 표시되면 포털에 로그인한 다음 **설정**, **관리 인증서**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="3fb8c-135">관리 인증서 창에서 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="3fb8c-136">Azure 구독을 선택하고 방금 만든 .cer 파일의 전체 경로를 붙여 넣은 후 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb8c-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
