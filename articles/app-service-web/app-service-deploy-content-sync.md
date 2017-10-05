---
title: "클라우드 폴더에서 Azure 앱 서비스로 콘텐츠 동기화"
description: "클라우드 폴더에서 콘텐츠 동기화를 통해 Azure 앱 서비스에 앱을 배포하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="7cc64-103">클라우드 폴더에서 Azure 앱 서비스로 콘텐츠 동기화</span><span class="sxs-lookup"><span data-stu-id="7cc64-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="7cc64-104">이 자습서는 Dropbox 및 OneDrive와 같은 인기 있는 클라우드 저장소 서비스에서 콘텐츠를 동기화하여 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 를 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="7cc64-105"><a name="overview"></a>콘텐츠 동기화 배포 개요</span><span class="sxs-lookup"><span data-stu-id="7cc64-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="7cc64-106">주문형 콘텐츠 동기화 배포는 앱 서비스와 통합된 [Kudu 배포 엔진](https://github.com/projectkudu/kudu/wiki) 에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="7cc64-107">[Azure 포털](https://portal.azure.com)에서 클라우드 저장소의 폴더를 지정하고 해당 폴더에서 앱 코드 및 콘텐츠 작업을 수행한 다음 단추를 클릭하여 앱 서비스를 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="7cc64-108">콘텐츠 동기화는 빌드 및 배포에 Kudu 프로세스를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="7cc64-109"><a name="contentsync"></a>콘텐츠 동기화 배포를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="7cc64-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="7cc64-110">[Azure 포털](https://portal.azure.com)에서 콘텐츠 동기화를 사용하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="7cc64-111">Azure Portal의 앱 블레이드에서 **설정** > **배포 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="7cc64-112">**원본 선택**을 클릭한 다음 배포 원본으로 **OneDrive** 또는 **Dropbox**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![콘텐츠 동기화](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="7cc64-114">API의 기본적인 차이 때문에 **비즈니스용 OneDrive**는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="7cc64-115">모든 앱 서비스 콘텐츠가 저장될 OneDrive 또는 Dropbox에 대해 미리 정의된 특정 지정 경로에 액세스하도록 앱 서비스를 설정하여 권한 부여 워크플로를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="7cc64-116">권한 부여 후에 앱 서비스 플랫폼은 지정된 콘텐츠 경로에 콘텐츠 폴더를 만드는 옵션 또는 이 지정된 콘텐츠 경로에서 기존 콘텐츠 폴더를 선택하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="7cc64-117">앱 서비스 동기화에 사용된 클라우드 저장소 계정에 지정된 콘텐츠 경로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="7cc64-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="7cc64-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="7cc64-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="7cc64-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="7cc64-120">초기 콘텐츠 동기화 후 Azure 포털에서 필요에 따라 콘텐츠 동기화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="7cc64-121">배포 기록은 **배포** 블레이드에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![배포 기록](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="7cc64-123">Dropbox 배포에 대한 자세한 내용은 [Dropbox에서 배포](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc64-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

