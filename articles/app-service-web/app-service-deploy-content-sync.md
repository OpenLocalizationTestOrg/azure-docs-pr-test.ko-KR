---
title: "클라우드 폴더 tooAzure 앱 서비스에서에서 aaaSync 콘텐츠"
description: "어떻게 toodeploy 콘텐츠를 통해 사용자 앱 tooAzure 앱 서비스는 클라우드 폴더에서을 동기화에 대해 알아봅니다."
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
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="ba95d-103">클라우드 폴더 tooAzure 앱 서비스의에서 콘텐츠를 동기화</span><span class="sxs-lookup"><span data-stu-id="ba95d-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="ba95d-104">이 자습서에서는 어떻게 toodeploy 너무[Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 하 여 Dropbox 및 OneDrive와 같은 인기 있는 클라우드 저장소 서비스에서 콘텐츠를 동기화 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="ba95d-105"><a name="overview"></a>콘텐츠 동기화 배포 개요</span><span class="sxs-lookup"><span data-stu-id="ba95d-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="ba95d-106">hello로 작동 하는 hello 주문형 콘텐츠 동기화 배포 [Kudu 배포 엔진](https://github.com/projectkudu/kudu/wiki) 앱 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="ba95d-107">Hello에 [Azure 포털](https://portal.azure.com), 클라우드 저장소에 지정 된 폴더, 응용 프로그램 코드 및이 폴더의 내용을 작업할 수 있습니다 및 hello로 동기화 tooApp 서비스의 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="ba95d-108">콘텐츠 동기화에서 빌드 및 배포에 대 한 hello Kudu 프로세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="ba95d-109"><a name="contentsync"></a>Tooenable 콘텐츠 배포를 동기화 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ba95d-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="ba95d-110">hello에서 tooenable 콘텐츠 동기화 [Azure 포털](https://portal.azure.com), 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="ba95d-111">Hello Azure 포털에서에서 앱의 블레이드에서 클릭 **설정** > **배포 원본을**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="ba95d-112">클릭 **소스 선택**을 선택한 후 **OneDrive** 또는 **Dropbox** 배포에 대 한 hello 소스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![콘텐츠 동기화](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="ba95d-114">Hello, Api의에서 기본적인 차이 때문에 **비즈니스용 OneDrive** 이 이번에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="ba95d-115">전체 hello 권한 부여 워크플로 tooenable 앱 서비스 tooaccess 특정 미리 지정 된 경로 대해 정의 된 OneDrive 또는 Dropbox 응용 프로그램 서비스 콘텐츠를 저장할 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="ba95d-116">권한 부여 hello 앱 s 서비스 플랫폼 제공 됩니다 후 hello 옵션 toocreate hello에 콘텐츠 폴더를 콘텐츠 경로 또는 toochoose이 지정 된 콘텐츠 경로 아래의 기존 콘텐츠 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="ba95d-117">앱 서비스 동기화에 사용 되는 클라우드 저장소 계정에서 콘텐츠 경로 지정 하는 hello hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="ba95d-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="ba95d-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="ba95d-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="ba95d-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="ba95d-120">Hello 후 hello Azure 포털에서에서 주문형 콘텐츠는 초기 동기화 hello 콘텐츠는 동기화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="ba95d-121">배포 기록을 hello로 사용할 수는 **배포** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![배포 기록](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="ba95d-123">Dropbox 배포에 대한 자세한 내용은 [Dropbox에서 배포](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba95d-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

