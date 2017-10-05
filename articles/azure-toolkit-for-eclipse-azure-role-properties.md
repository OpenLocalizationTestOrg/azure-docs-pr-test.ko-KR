---
title: "Azure 역할 속성"
description: "Eclipse용 Azure 도구 키트를 사용하여 Azure 역할 설정을 구성하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a><span data-ttu-id="7e8a8-103">Azure 역할 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-103">Azure Role Properties</span></span>
<span data-ttu-id="7e8a8-104">Azure 역할에 대한 다양한 구성 설정은 Eclipse용 Azure 도구 키트 내에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-104">Various configuration settings for your Azure role can be set within the Azure Toolkit for Eclipse.</span></span>

## <a name="configuring-azure-role-properties"></a><span data-ttu-id="7e8a8-105">Azure 역할 속성 구성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-105">Configuring Azure Role Properties</span></span>
<span data-ttu-id="7e8a8-106">Azure 역할 속성을 구성하려면 작업자 역할에 대한 속성 대화 상자를 통해 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-106">Configuring your Azure Role Properties is accomplished through the property dialogs for your worker role.</span></span> <span data-ttu-id="7e8a8-107">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure** 하위 메뉴를 선택합니다</span><span class="sxs-lookup"><span data-stu-id="7e8a8-107">Open the context menu for the role in Eclipse's Project Explorer pane and select the **Azure** sub-menu.</span></span> <span data-ttu-id="7e8a8-108">(Eclipse 프로젝트 탐색기에서 역할이 보이지 않으면 프로젝트 탐색기에서 Azure 프로젝트를 확장합니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-108">(If you don't see the role in the Eclipse Project Explorer, expand your Azure project in Project Explorer.)</span></span>

![][ic789599]

<span data-ttu-id="7e8a8-109">**속성** 대화 상자에서 설정할 수 있는 다양한 속성은 이 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-109">The various properties that can be set from the **Properties** dialogs are described in this topic.</span></span> <span data-ttu-id="7e8a8-110">새 Azure 배포 프로젝트를 만들 때 많은 속성이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-110">Note that many properties are filled in automatically when you create a new Azure deployment project.</span></span>

<span data-ttu-id="7e8a8-111">다음 속성 페이지는 Azure 역할에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-111">The following property pages are available for Azure roles.</span></span>

* [<span data-ttu-id="7e8a8-112">가상 컴퓨터 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-112">Virtual machine properties</span></span>](#virtual_machine_properties)
* [<span data-ttu-id="7e8a8-113">캐싱 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-113">Caching properties</span></span>](#caching_properties)
* [<span data-ttu-id="7e8a8-114">인증서 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-114">Certificates properties</span></span>](#certificates_properties)
* [<span data-ttu-id="7e8a8-115">구성 요소 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-115">Components properties</span></span>](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [<span data-ttu-id="7e8a8-116">끝점 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-116">Endpoints properties</span></span>](#endpoints_properties)
* [<span data-ttu-id="7e8a8-117">환경 변수 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-117">Environment variables properties</span></span>](#environment_variables_properties)
* [<span data-ttu-id="7e8a8-118">부하 분산/세션 선호도(또는 "고정 세션") 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-118">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>](#session_affinity_properties)
* [<span data-ttu-id="7e8a8-119">로컬 저장소 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-119">Local storage properties</span></span>](#local_storage_properties)
* [<span data-ttu-id="7e8a8-120">서버 구성 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-120">Server configuration properties</span></span>](#server_configuration_properties)
* [<span data-ttu-id="7e8a8-121">SSL 오프로딩 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-121">SSL offloading properties</span></span>](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a><span data-ttu-id="7e8a8-122">가상 컴퓨터 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-122">Virtual machine properties</span></span>
<span data-ttu-id="7e8a8-123">Eclipse의 프로젝트 탐색기 창에서 역할에 대해 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **속성**을 클릭합니다. 다음 그림에 나와 있는 것처럼 가상 컴퓨터 크기를 변경하고 인스턴스 개수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-123">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Properties**, and you will have the ability to change the virtual machine size, and also change the number of instances, as shown in the following image.</span></span>

![][ic719499]

> [!NOTE]
> <span data-ttu-id="7e8a8-124">Windows에만 해당: 인스턴스 수를 1보다 큰 값으로 설정하고 또한 응용 프로그램 서버를 구성하는 경우 도구 키트는 설정에 관계 없이 1개의 역할 인스턴스만을 허용하여 에뮬레이터에서 실행합니다. </span><span class="sxs-lookup"><span data-stu-id="7e8a8-124">Windows only: when you set the number of instances to a value greater than 1 and you also configure an application server, the toolkit will allow only 1 role instance to run in the emulator, regardless of this setting.</span></span> <span data-ttu-id="7e8a8-125">이 동일한 컴퓨터에서 실행될 때 다른 서버 인스턴스 간의 포트 바인딩 충돌을 방지하려는 것입니다.(예를 들어 모두 포트 8080에 바인딩을 시도)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-125">This is to avoid port binding conflicts between the different server instances (for example, all trying to bind to port 8080) when they run on the same computer.</span></span> <span data-ttu-id="7e8a8-126">원하는 인스턴스 개수 설정은 유지되지만 클라우드로 배포하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-126">Your desired instance count setting is preserved, but it goes into effect only when you deploy to the cloud.</span></span>
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a><span data-ttu-id="7e8a8-127">캐싱 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-127">Caching properties</span></span>
<span data-ttu-id="7e8a8-128">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **캐싱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-128">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Caching**.</span></span> <span data-ttu-id="7e8a8-129">이 대화 상자에서 명명된 memcache와 호환 가능한 캐시를 사용할 수 있으며 이는 웹 응용 프로그램 속도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-129">Within this dialog, you can enable named co-located memcache-compatible caches, allowing you to help speed up your web applications.</span></span>

![][ic719483]

<span data-ttu-id="7e8a8-130">**캐싱** 속성 페이지 내에서 다음에 대한 전역 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-130">Within the **Caching** property page, you can specify global settings for the following:</span></span>

* <span data-ttu-id="7e8a8-131">배치된 캐싱의 사용 여부.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-131">whether co-located caching is enabled.</span></span>
* <span data-ttu-id="7e8a8-132">메모리의 백분율로 나타낸 캐시 크기.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-132">the cache size as a percent of memory.</span></span>
* <span data-ttu-id="7e8a8-133">응용 프로그램이 클라우드 서비스로 실행될 때 캐시 상태를 저장하기 위한 저장소 계정 이름 또는 캐시 상태를 저장하지 않으려면 해당 없음.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-133">the storage account name for saving the cache state when your application runs as a cloud service, or none if you do not want to save the cache state.</span></span> <span data-ttu-id="7e8a8-134">(계산 에뮬레이터에서 응용 프로그램을 실행하는 경우 저장소 계정 이름은 사용되지 않습니다.) 저장소 계정 이름을 **(자동)**(기본값)으로 설정하는 경우 캐싱 구성은 **Azure에 게시** 대화 상자에서 선택한 것과 동일한 저장소 계정을 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-134">(The storage account name is not used when you run your application in the compute emulator.) If you set the storage account name to **(auto)** (which is the default), your caching configuration will automatically use the same storage account as the one you select in the **Publish to Azure** dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="7e8a8-135">**(자동)** 설정은 Eclipse 도구 키트의 게시 마법사를 사용하여 배포를 게시하는 경우에만 원하는 효과를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-135">The **(auto)** setting will have the desired effect only if you publish your deployment using the Eclipse toolkit's publish wizard.</span></span> <span data-ttu-id="7e8a8-136">대신 수동으로 [Azure Management Portal][Azure Management Portal]과 같은 외부 메커니즘을 사용하는 .cspkg 파일을 게시하는 경우 배포가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-136">If instead you publish the .cspkg file manually using an external mechanism, such as the [Azure Management Portal][Azure Management Portal], the deployment will not function properly.</span></span>
> 
> 

<span data-ttu-id="7e8a8-137">다음 대화 상자는 캐시에 대한 속성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-137">The following dialog shows the properties for a cache.</span></span>

![][ic719501]

* <span data-ttu-id="7e8a8-138">**이름:** 배치된 캐시의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-138">**Name:** The name of the co-located cache.</span></span>
* <span data-ttu-id="7e8a8-139">**포트 번호:** 캐시에 사용할 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-139">**Port number:** The port number to use for the cache.</span></span>
* <span data-ttu-id="7e8a8-140">**만료 정책:** 캐시의 키가 만료되는 시기를 지정하는 다음 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-140">**Expiration policy:** One of the following values that specifies when a key in the cache expires.</span></span>
  * <span data-ttu-id="7e8a8-141">**절대:** **Minutes to live**에서 지정된 시간에 도달하면 키가 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-141">**Absolute:** The key expires when the time specified by **Minutes to live** is reached.</span></span>
  * <span data-ttu-id="7e8a8-142">**NeverExpires:** 키에 만료 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-142">**NeverExpires:** The key does not have an expiration time.</span></span>
  * <span data-ttu-id="7e8a8-143">**SlidingWindow:** **Minutes to live**에서 지정한 시간 동안 액세스 하지 않은 경우 키가 만료됩니다. 액세스할 때 마다 만료 시계가 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-143">**SlidingWindow:** The key expires if it has not been accessed for the amount of time specified by **Minutes to live**; each time it is accessed, the expiration clock is reset.</span></span>
* <span data-ttu-id="7e8a8-144">**Minutes to live:** memcached 키가 유효한 최대 시간(분)은 만료 정책에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-144">**Minutes to live:** Maximum number of minutes for a memcached key to live, subject to the expiration policy.</span></span>
* <span data-ttu-id="7e8a8-145">**다른 역할 인스턴스에서 복제된 백업을 통한 고가용성:** 사용하도록 설정하면 다른 역할 인스턴스에서 복제된 백업을 사용하여 고가용성 제공하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-145">**High availability with replicated backups on different role instances:** If enabled, helps provide high availability utilizing replicated backups on different role instances.</span></span> <span data-ttu-id="7e8a8-146">이 기능이 작동하기 위해 두 개 이상의 역할 인스턴스가 배포에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-146">Note that at least two role instances must be in effect for your deployment for this feature to work.</span></span>

<span data-ttu-id="7e8a8-147">새 캐시를 추가하려면 **캐싱** 속성 페이지에서 **추가** 단추를 클릭하고 **명명된 캐시 구성** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-147">To add a new cache, click the **Add** button in the **Caching** property page, and a **Configure Named Cache** dialog will be opened.</span></span> <span data-ttu-id="7e8a8-148">위에서 설명하는 속성에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-148">Provide values for the properties which are described above.</span></span>

<span data-ttu-id="7e8a8-149">명명된 캐시를 수정하려면 캐시를 선택하고 **캐싱** 속성 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-149">To modify a named cache, select the cache and click the **Edit** button in the **Caching** property page.</span></span> <span data-ttu-id="7e8a8-150">캐시 속성을 수정할 수 있게 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-150">A dialog will be opened allowing you to modify the cache properties.</span></span> <span data-ttu-id="7e8a8-151">**확인** 을 눌러서 캐시 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-151">Press **OK** to save the cache values.</span></span>

<span data-ttu-id="7e8a8-152">캐시를 삭제하려면 캐시를 선택하고 **캐싱** 속성 페이지에서 **제거** 단추를 클릭한 다음 **예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-152">To delete a cache, select the cache and click the **Remove** button in the **Caching** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="7e8a8-153">캐싱을 사용하는 방법에 대한 자세한 내용은 [공동 배치된 캐싱을 사용하는 방법][How to Use Co-located Caching]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-153">For more information on how to use caching, see [How to Use Co-located Caching][How to Use Co-located Caching].</span></span>

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a><span data-ttu-id="7e8a8-154">인증서 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-154">Certificates properties</span></span>
<span data-ttu-id="7e8a8-155">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-155">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Certificates**.</span></span>

![][ic710964]

<span data-ttu-id="7e8a8-156">이 대화 상자에서는 Eclipse 프로젝트에서 참조하는 인증서를 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-156">Within this dialog, you can add or remove certificates referenced by your Eclipse project.</span></span> <span data-ttu-id="7e8a8-157">여기에 나열된 인증서는 Java keystore 안에 자동으로 저장되지 않으며 따라서 Java 응용 프로그램 내에서 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-157">Note that the certificates listed here are not automatically stored inside any Java keystore, and therefore are not automatically available for any use from within a Java application.</span></span> <span data-ttu-id="7e8a8-158">Azure로 등록되므로 배포를 실행하고 이어서 다른 Windows 소프트웨어에 의해 사용되는 가상 컴퓨터에서 Windows 인증서 저장소에 미리 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-158">They are only registered with Azure so that they can be preloaded into the Windows certificate store on the virtual machines running your deployment and subsequently used by other Windows software.</span></span> <span data-ttu-id="7e8a8-159">현재 **인증서** 대화 상자에서 이런 방식으로 참조되는 인증서를 사용하는 도구 키트의 유일한 기능은 [SSL 오프 로딩][SSL Offloading]입니다. 이는 인터넷 정보 서비스(IIS) 및 응용 프로그램 요청 라우팅(ARR)에 의존하기 때문에 이 방식으로 사용할 수 있도록 적절한 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-159">Currently, the only feature of the toolkit that uses the certificates referenced this way in the **Certificates** dialog is [SSL Offloading][SSL Offloading], due to its reliance on Internet Information Services (IIS) and Application Request Routing (ARR), which require the proper certificate to be made available in this manner.</span></span>

<span data-ttu-id="7e8a8-160">게시 마법사를 사용하여 Azure에 프로젝트를 배포할 때 이전에 업로드 되지 않은 경우 Azure 서비스에 자동으로 업로드하기 위해 암호와 함께 이러한 인증서에 해당하는 개인 정보 교환(PFX) 파일을 가리키도록 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-160">When you deploy your project to Azure using the Publish wizard, you will be prompted to point at the Personal Information Exchange (PFX) files corresponding to these certificates, along with their passwords, in order to automatically upload them to the Azure service, but only if they have not been uploaded there previously.</span></span>

<a name="components_properties"></a> 

### <a name="components-properties"></a><span data-ttu-id="7e8a8-161">구성 요소 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-161">Components properties</span></span>
<span data-ttu-id="7e8a8-162">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **구성 요소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-162">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Components**.</span></span> <span data-ttu-id="7e8a8-163">이 대화 상자에서 역할의 구성 요소를 추가, 수정 또는 제거할 뿐만 아니라 처리되는 순서를 변경하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-163">Within this dialog, you have the ability to add, modify, or remove the components of your role, as well as change the order in which they are processed.</span></span>

![][ic719502]

<span data-ttu-id="7e8a8-164">구성 요소 기능을 사용하면 Java 응용 프로그램 프로젝트, 특수한 파일 및 배포에 필요한 실행 가능한 명령줄 문 등 Azure 배포 프로젝트에 종속성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-164">The components feature enables you to add dependencies to your Azure deployment project, such as Java application projects, special files, and executable command line statements that are needed by your deployment.</span></span>

<span data-ttu-id="7e8a8-165">각 구성 요소에 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-165">For each component, you can specify:</span></span>

* <span data-ttu-id="7e8a8-166">작성 시 Azure 배포 프로젝트에 구성 요소를 가져오려면 수행해야 하는 단계.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-166">The step to be taken when importing the component into your Azure deployment project when it is built.</span></span>
* <span data-ttu-id="7e8a8-167">Azure 클라우드에서 구성 요소를 배포할 때 수행해야 하는 단계.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-167">The step to be taken when deploying that component in the Azure cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="7e8a8-168">구성 요소 파일 또는 명령줄을 지정할 때 배포가 Windows 가상 컴퓨터에 게시되므로 사용자 지정 단계는 Windows 기반 운영 체제에 적합해야 한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-168">When specifying component files or command lines, keep in mind that your deployment will be published to a Windows virtual machine, so your custom steps must be valid for a Windows-based operating system.</span></span> 
> 
> 

<span data-ttu-id="7e8a8-169">구성 요소에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-169">Components have the following properties:</span></span>

* <span data-ttu-id="7e8a8-170">**가져오기:** 프로젝트를 빌드할 때 구성 요소를 프로젝트로 가져오는 방법을 나타내는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-170">**Import:** Method that indicates how the component will be imported into the project when the project is built.</span></span> <span data-ttu-id="7e8a8-171">다음 값 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-171">This can be one of the following values:</span></span>
  * <span data-ttu-id="7e8a8-172">**copy:** 구성 요소는 **From** 속성으로 지정된 로컬 경로에서 역할의 **approot** 디렉터리에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-172">**copy:** The component is copied from the local path specified by the **From** property into the role's **approot** directory.</span></span>
  * <span data-ttu-id="7e8a8-173">**EAR:** 구성 요소는 **From** 속성이 지정한 로컬 경로에 엔터프라이즈 응용 프로그램 프로젝트에서 가져오는 Java 엔터프라이즈 아카이브(EAR)입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-173">**EAR:** The component is a Java enterprise archive (EAR) imported from an Enterprise Application Project at the local path specified by the **From** property.</span></span> <span data-ttu-id="7e8a8-174">(도구 키트에서 해당 위치에 있는 프로젝트의 특성을 기준으로 자동으로 검색합니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-174">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="7e8a8-175">**JAR:** 구성 요소는 Java 웹 아카이브(JAR)이고 Java 프로젝트에 **From** 속성이 지정한 로컬 경로에 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-175">**JAR:** The component is a Java archive (JAR) and is imported from a Java project at the local path specified by the **From** property.</span></span> <span data-ttu-id="7e8a8-176">(도구 키트에서 해당 위치에 있는 프로젝트의 특성을 기준으로 자동으로 검색합니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-176">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="7e8a8-177">**없음:** 구성 요소를 가져오기 위해 어떤 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-177">**none:** No action is taken to import the component.</span></span> <span data-ttu-id="7e8a8-178">구성 요소가 역할의 **approot** 디렉터리에 이미 있다고 가정할 때 또는 **Deploy** 메서드가 **exec**일 경우 구성 요소가 단순히 **As** 속성에서 지정된 대로 실행 가능한 명령줄 문일 때 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-178">This is applicable when the component is assumed to already be present in the role's **approot** directory, or when the component is merely an executable command line statement, as specified in the **As** property when the **Deploy** method is **exec**.</span></span>
  * <span data-ttu-id="7e8a8-179">**WAR:** 구성 요소는 Java 웹 응용 프로그램 보관 파일(WAR)이고 **From** 속성이 지정한 로컬 경로에 동적 웹 프로젝트에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-179">**WAR:** The component is a Java web application archive (WAR) and is imported from a Dynamic Web Project at the local path specified by the **From** property.</span></span> <span data-ttu-id="7e8a8-180">(도구 키트에서 해당 위치에 있는 프로젝트의 특성을 기준으로 자동으로 검색합니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-180">(This is detected automatically by the toolkit based on the nature of the project at that location).</span></span>
  * <span data-ttu-id="7e8a8-181">**zip:** 구성 요소는 zip 파일이고 **From** 속성에 지정된 디렉터리 또는 파일을 압축하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-181">**zip:** The component is a zip file and is imported by zipping the directory or file specified by the **From** property.</span></span>
* <span data-ttu-id="7e8a8-182">**From:** 배포에 가져올 항목을 나타내는 폴더 또는 파일에 대한 로컬 컴퓨터의 원본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-182">**From:** Source path on your local machine to the folder or file that represents the item(s) to import to your deployment.</span></span> <span data-ttu-id="7e8a8-183">이 속성에 Windows 환경 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-183">Windows environment variables can be used in this property.</span></span> <span data-ttu-id="7e8a8-184">가져올 수 있는 모든 구성 요소는 프로젝트를 빌드할 때 역할의 **approot** 디렉터리로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-184">All importable components will be imported into the role's **approot** directory when the project is built.</span></span>
  
    <span data-ttu-id="7e8a8-185">(계산 에뮬레이터가 아닌) 클라우드로 배포할 때 다운로드에서 구성 요소를 배포하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-185">Note that you have the ability to deploy a component from a download when deploying to the cloud (not the compute emulator).</span></span> <span data-ttu-id="7e8a8-186">구성 요소를 추가에 대해 아래의 관련된 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-186">See related information below about adding a component.</span></span>    
* <span data-ttu-id="7e8a8-187">**As:** 역할의 **approot** 디렉터리로 가져오고 궁극적으로 Azure 클라우드에서 배포할 구성 요소의 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-187">**As:** File name under which the component will be imported into the role's **approot** directory and ultimately deployed in the Azure cloud.</span></span> <span data-ttu-id="7e8a8-188">로컬 컴퓨터에서와 동일한 이름을 유지하려면 이 속성을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-188">Leave this property blank to keep the name the same as it is on the local machine.</span></span> <span data-ttu-id="7e8a8-189">(즉, **Deploy** 메서드가 **exec**로 설정된 실행 가능한 구성 요소의 경우 임의의 Windows 명령줄 문일 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-189">(For executable components, that is, those whose **Deploy** method is set to **exec**, this can be an arbitrary Windows command line statement.)</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="7e8a8-190">이 값에 공백 문자를 사용하는 경우 배포 방법에 따라 다르게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-190">If you use space characters for this value, they will be handled differently depending on the deploy method.</span></span> <span data-ttu-id="7e8a8-191">배포 방법이 **exec**인 경우 공백은 파일 이름의 일부가 아니라 명령줄 인수 구분 기호로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-191">If the deploy method is **exec**, spaces will be interpreted as command line argument separators and not as part of the file name.</span></span> <span data-ttu-id="7e8a8-192">다른 모든 배포 방법의 경우 공백은 파일 이름의 일부로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-192">For all other deploy methods, spaces will be interpreted as part of the file name.</span></span>
  > 
  > 
* <span data-ttu-id="7e8a8-193">**배포:** 배포가 시작될 때 구성 요소에 적용되는 동작을 나타내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-193">**Deploy:** Method that indicates the action applied to the component when the deployment is started.</span></span> <span data-ttu-id="7e8a8-194">다음 값 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-194">This can be one of the following values:</span></span>
  
  * <span data-ttu-id="7e8a8-195">**copy:** 구성 요소가 **To** 속성으로 지정된 대상 경로에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-195">**copy:** The component is copied to the destination path specified by the **To** property.</span></span>
  * <span data-ttu-id="7e8a8-196">**exec:** 구성 요소가 배포가 시작 될 때 **To** 속성에서 지정한 경로의 컨텍스트에서 실행된 실행 가능한 Windows 명령줄 문입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-196">**exec:** The component is an executable Windows command line statement executed in the context of the path specified by the **To** property, at the time the deployment starts.</span></span>
  * <span data-ttu-id="7e8a8-197">**없음:** 배포가 시작될 때 어떤 작업도 구성 요소에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-197">**none:** No action is applied to the component when the deployment starts.</span></span>
  * <span data-ttu-id="7e8a8-198">**zip:** 구성 요소가 **To** 속성으로 지정된 대상 경로에 압축이 풀립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-198">**zip:** The component is unzipped to the destination path specified by the **To** property.</span></span> <span data-ttu-id="7e8a8-199">이 메서드는 **Import** 속성이 **zip**인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-199">This method is available only when the **Import** property is **zip**.</span></span>
* <span data-ttu-id="7e8a8-200">**To:** 구성 요소를 배포할 가상 컴퓨터에서 대상 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-200">**To:** Destination path on the virtual machine where the component will be deployed.</span></span> <span data-ttu-id="7e8a8-201">Windows 환경 변수는 이 속성에 사용할 수 있고 파일 경로는 **approot**에 상대적입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-201">Windows environment variables can be used in this property, and file paths are relative to **approot**.</span></span>

<span data-ttu-id="7e8a8-202">새 구성 요소를 추가하려면 **구성 요소** 속성 페이지에서 **추가** 단추를 클릭하고 **Azure 역할 구성 요소** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-202">To add a new component, click the **Add** button in the **Components** property page, and an **Azure Role Component** dialog will be opened.</span></span> <span data-ttu-id="7e8a8-203">위에서 설명하는 속성에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-203">Provide values for the properties which are described above.</span></span> 

<span data-ttu-id="7e8a8-204">다음 새로운 WAR 구성 요소를 추가하는 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-204">The following shows an example for adding a new WAR component.</span></span>

![][ic719503]

<span data-ttu-id="7e8a8-205">(계산 에뮬레이터가 아닌) 클라우드로 배포할 때 다운로드에서 구성 요소를 배포하려는 경우 **패키지에 포함하는 대신 클라우드에 위치할 때 다음에서 배포** 를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-205">When deploying to the cloud (not the compute emulator), if you want to deploy the component from a download, ensure that **When in cloud, instead of including in the package, deploy from** is checked.</span></span> <span data-ttu-id="7e8a8-206">Azure Storage 계정에서 다운로드하려는 경우 **저장소 계정** 드롭다운 목록에서 저장소 계정을 선택(**계정** 링크를 클릭하여 목록의 내용을 수정할 수 있습니다.)하며 이는 부분적으로 **URL** 필드를 입력하고 URL의 나머지 부분을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-206">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL.</span></span> <span data-ttu-id="7e8a8-207">Azure Storage를 사용하려면 **저장소 계정** 드롭다운 목록에서 **(없음)**을 선택하고 **URL** 필드에서 구성 요소에 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-207">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your component in the **URL** field.</span></span> <span data-ttu-id="7e8a8-208">다음 방법 중 하나를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-208">Specify one of the following methods:</span></span>

* <span data-ttu-id="7e8a8-209">**copy:** 다운로드 구성 요소가 **To Directory** 경로로 지정된 대상 경로에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-209">**copy:** The download component is copied to the destination path specified by the **To Directory** path.</span></span>
* <span data-ttu-id="7e8a8-210">**same:** 동일한 방법이 **다운로드 패키지에서 배포**처럼 **다운로드에서 배포**에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-210">**same:** The same method used for **Deploy from download** as for **Deploy from package**.</span></span>
* <span data-ttu-id="7e8a8-211">**zip:** 다운로드 구성 요소가 **To Directory** 경로로 지정된 대상 경로에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-211">**zip:** The download component is unzipped to the destination path specified by the **To Directory** path.</span></span>

<span data-ttu-id="7e8a8-212">구성 요소를 수정하려면 구성 요소를 선택하고 **구성 요소** 속성 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-212">To modify a component, select the component and click the **Edit** button in the **Components** property page.</span></span> <span data-ttu-id="7e8a8-213">구성 요소 속성을 수정할 수 있게 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-213">A dialog will be opened allowing you to modify the component properties.</span></span> <span data-ttu-id="7e8a8-214">**확인** 을 눌러서 구성 요소 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-214">Press **OK** to save the component values.</span></span>

<span data-ttu-id="7e8a8-215">구성 요소를 삭제하려면 구성 요소를 선택하고 **구성 요소** 속성 페이지에서 **제거** 단추를 클릭한 다음 **예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-215">To delete a component, select the component and click the **Remove** button in the **Components** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="7e8a8-216">구성 요소는 나열된 순서에 따라 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-216">Components are processed in the order listed.</span></span> <span data-ttu-id="7e8a8-217">**위로 이동** 및 **아래로 이동** 단추를 사용하여 순서를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-217">Use the **Move Up** and **Move Down** buttons to arrange the order.</span></span>

> [!NOTE]
> <span data-ttu-id="7e8a8-218">또한 서버 구성 기능은 구성 요소에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-218">The server configuration feature relies on components as well.</span></span> <span data-ttu-id="7e8a8-219">이러한 구성 요소는 해당하는 서버 구성을 제거하지 않고 제거되거나 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-219">Those components cannot be removed or edited without removing the corresponding server configuration.</span></span> <span data-ttu-id="7e8a8-220">이러한 구성 요소를 변경하려고 할 때 해당 사항에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-220">You will be prompted about that when attempting to make changes to such components.</span></span>
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a><span data-ttu-id="7e8a8-221">끝점 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-221">Endpoints properties</span></span>
<span data-ttu-id="7e8a8-222">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-222">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Endpoints**.</span></span> <span data-ttu-id="7e8a8-223">이 대화 상자 내에서 다음 그림에서 보이는 대로 끝점을 만들 뿐만 아니라 끝점을 편집하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-223">Within this dialog, you have the ability to create an endpoint, as well as edit or remove an endpoint, as shown in the following image.</span></span>

![][ic719505]

<span data-ttu-id="7e8a8-224">끝점을 추가하려면 **끝점** 속성 페이지에서 **추가** 단추를 클릭하고 **끝점 추가** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-224">To add an endpoint, click the **Add** button in the **Endpoints** property page, and an **Add Endpoint** dialog will be opened.</span></span>

![][ic710897]

<span data-ttu-id="7e8a8-225">끝점의 이름을 입력하고 형식(**Input**, **Internal** 또는 **InstanceInput** 중 하나)을 선택하며 공용 및 개인 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-225">Enter a name for the endpoint, select the type (either **Input**, **Internal**, or **InstanceInput**), and specify the public and private port.</span></span> <span data-ttu-id="7e8a8-226">**확인** 을 눌러 새 끝점 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-226">Press **OK** to save the new endpoint values.</span></span>

<span data-ttu-id="7e8a8-227">끝점의 형식에 따라 다음과 같이 포트 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-227">Depending on the type of endpoint, you may use port ranges as follows:</span></span>

* <span data-ttu-id="7e8a8-228">입력 인스턴스 끝점의 경우 공용 포트는 포트의 범위일 수 있고(예를 들어 **2000-2010**) 개인 포트는 고정된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-228">For an input instance endpoint, the public port can be a range of ports (for example **2000-2010**) and the private port is a fixed value.</span></span>
* <span data-ttu-id="7e8a8-229">내부 끝점의 경우 공용 포트를 사용하지 않고 개인 포트는 범위이거나 비어 있거나 별표로 설정되어 Azure에서 자동으로 설정된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-229">For an internal endpoint, the public port is not used, and the private port can be a range, or left blank or set to an asterisk to indicate it is automatically set by Azure.</span></span>
* <span data-ttu-id="7e8a8-230">입력 끝점의 경우 공용 포트는 고정된 값일 수 있고 개인 포트는 고정된 값일 수 있고 비어 있거나 별표로 설정되어 Azure에서 자동으로 설정된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-230">For input endpoints, the public port can only be a fixed value, and the private port can be a fixed value, or left blank or set to an asterisk to indicate it is automatically set by Azure.</span></span>

<span data-ttu-id="7e8a8-231">범위 대신 단일 포트 번호를 사용하려는 경우 범위 빈 값의 끝에 텍스트 상자를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-231">If you want to use a single port number instead of a range, leave the text box for the end of the range blank.</span></span>

<span data-ttu-id="7e8a8-232">자동으로 설정된 포트의 경우 런타임 중에 실제로 사용되는 포트를 결정해야 하면 응용 프로그램이 Azure 서비스 런타임 API를 사용할 수 있으며 이는 [com.microsoft.windowsazure.serviceruntime 패키지 요약][com.microsoft.windowsazure.serviceruntime package summary]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-232">For ports that are set to automatic, if you need to determine which port is actually used during runtime, your application can use the Azure Service Runtime API, which is documented in the [com.microsoft.windowsazure.serviceruntime package summary][com.microsoft.windowsazure.serviceruntime package summary].</span></span>

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

<span data-ttu-id="7e8a8-233">끝점을 수정하려면 끝점을 선택하고 **끝점** 속성 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-233">To modify an endpoint, select the endpoint and click the **Edit** button in the **Endpoints** property page.</span></span> <span data-ttu-id="7e8a8-234">끝점 이름, 형식 및 공용과 개인 포트를 수정할 수 있는 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-234">A dialog will be opened allowing you to modify the endpoint name, type, and public and private ports.</span></span> <span data-ttu-id="7e8a8-235">**확인** 을 눌러 수정된 끝점 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-235">Press **OK** to save the modified endpoint values.</span></span>

<span data-ttu-id="7e8a8-236">끝점을 삭제하려면 끝점을 선택하고 **끝점** 속성 페이지에서 **제거** 단추를 클릭한 다음 **예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-236">To delete an endpoint, select the endpoint and click the **Remove** button in the **Endpoints** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="7e8a8-237">역할에서 사용자가 활성화한 일부 기능(예: 캐싱, 세션 선호도 또는 SSL 오프로딩)을 제대로 구성하기 위해 도구 키트는 사용자 정의 끝점과 함께 나열될 특수한 끝점을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-237">In order to properly configure some of the features (such as Caching, Session Affinity, or SSL offloading) enabled by the user on a role, the toolkit may automatically configure special endpoints that will be listed along with user-defined endpoints.</span></span> <span data-ttu-id="7e8a8-238">도구 키트는 관련된 기능이 사용되는 한 사용자가 이렇게 자동으로 생성된 끝점을 편집하거나 삭제하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-238">The toolkit prevents the user from editing or deleting such automatically generated endpoints as long as the associated feature is enabled.</span></span>

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a><span data-ttu-id="7e8a8-239">환경 변수 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-239">Environment variables properties</span></span>
<span data-ttu-id="7e8a8-240">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **환경 변수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-240">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Environment Variables**.</span></span> <span data-ttu-id="7e8a8-241">이 대화 상자 내에서 다음 그림에서 보이는 대로 환경 변수를 만들 뿐만 아니라 환경 변수를 수정하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-241">Within this dialog, you have the ability to create an environment variable, as well as modify or remove an environment variable, as shown in the following image.</span></span>

![][ic719506]

<span data-ttu-id="7e8a8-242">환경 변수는 역할이 시작할 때 시작 스크립트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-242">Environment variables are available to your startup script when the role starts.</span></span>

> [!NOTE]
> <span data-ttu-id="7e8a8-243">환경 변수를 지정할 때 배포가 Windows 가상 컴퓨터에 게시되므로 환경 변수는 Windows 기반 운영 체제에 적합해야 한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-243">When specifying environment variables, keep in mind that your deployment will be published to a Windows virtual machine, so your environment variables must be valid for a Windows-based operating system.</span></span>
> 
> 

<span data-ttu-id="7e8a8-244">역할 시작 시 사용 가능한 환경 변수의 예로 **추가** 단추를 클릭하여 새 환경 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-244">As an example of an environment variable being available when the role starts, create a new environment variable by clicking the **Add** button.</span></span> <span data-ttu-id="7e8a8-245">다음은 **1.0** 값을 만들고 할당하는 **MyRoleVersion**이라는 환경 변수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-245">The following shows an environment variable named **MyRoleVersion** being created and assigned the value **1.0**.</span></span>

![][ic659268]

<span data-ttu-id="7e8a8-246">jsp 코드 내에서 `System.getenv` 메서드를 사용하여 값을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-246">Within your jsp code, you could display the value using the `System.getenv` method:</span></span>

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

<span data-ttu-id="7e8a8-247">응용 프로그램을 실행할 때 이 출력의 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-247">Resulting in this output when your application runs:</span></span>

![][ic552233]

<span data-ttu-id="7e8a8-248">환경 변수를 수정하려면 환경 변수를 선택하고 **환경 변수** 속성 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-248">To modify an environment variable, select the environment variable and click the **Edit** button in the **Environment Variables** property page.</span></span> <span data-ttu-id="7e8a8-249">환경 변수 속성을 수정할 수 있게 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-249">A dialog will be opened allowing you to modify the environment variable properties.</span></span> <span data-ttu-id="7e8a8-250">**확인** 을 눌러 환경 변수 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-250">Press **OK** to save the environment variable values.</span></span>

<span data-ttu-id="7e8a8-251">환경 변수를 삭제하려면 환경 변수를 선택하고 **환경 변수** 속성 페이지에서 **제거** 단추를 클릭한 다음 **예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-251">To delete an environment variable, select the environment variable and click the **Remove** button in the **Environment Variables** property page, and then click **Yes** to confirm the deletion.</span></span>

<span data-ttu-id="7e8a8-252">역할에서 사용자가 활성화한 일부 기능(예: 서버 구성, 원격 디버깅 또는 로컬 저장소)을 제대로 구성하기 위해 도구 키트는 사용자 정의 환경 변수와 함께 나열될 특수 환경 변수를 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-252">In order to properly configure some of the features (such as Server Configuration, Remote Debugging or Local Storage) enabled by the user on a role, the toolkit may automatically configure special environment variables that will be listed along with user-defined environment variables.</span></span> <span data-ttu-id="7e8a8-253">도구 키트는 관련된 기능이 사용되는 한 사용자가 이렇게 자동으로 생성된 환경 변수를 편집하거나 삭제하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-253">The toolkit prevents the user from editing or deleting such automatically generated environment variables as long as the associated feature is enabled.</span></span>

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a><span data-ttu-id="7e8a8-254">부하 분산/세션 선호도(또는 "고정 세션") 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-254">Load balancing / session affinity (a.k.a "sticky sessions") properties</span></span>
<span data-ttu-id="7e8a8-255">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **부하 분산**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-255">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Load Balancing**.</span></span> <span data-ttu-id="7e8a8-256">이 대화 상자에서 다음 그림에서 보여주듯 세션 선호도를 사용하거나 사용하지 않는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-256">Within this dialog, you have the ability to enable or disable session affinity, as shown in the following image.</span></span>

![][ic719492]

<span data-ttu-id="7e8a8-257">관련된 내용은 [세션 선호도][Session Affinity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-257">For related information, see [Session Affinity][Session Affinity].</span></span> <span data-ttu-id="7e8a8-258">또한 [SSL 오프로딩][SSL Offloading]에서 설명한 대로 SSL 오프로딩의 컨텍스트에서이 기능의 동작에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-258">Also, note this feature's behavior in the context of SSL offloading, as described at [SSL Offloading][SSL Offloading].</span></span>

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a><span data-ttu-id="7e8a8-259">로컬 저장소 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-259">Local storage properties</span></span>
<span data-ttu-id="7e8a8-260">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **로컬 저장소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-260">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="7e8a8-261">이 대화 상자 내에서 응용 프로그램을 실행하는 가상 컴퓨터에 대한 임시 로컬 저장소를 만들기, 수정 또는 제거하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-261">Within this dialog, you have the ability to create, modify or remove temporary local storage for the virtual machine that is running your application.</span></span> <span data-ttu-id="7e8a8-262">특정 값은 로컬 저장소의 크기를 설정할 수 있을 뿐만 아니라 다음 그림에서 보이는 것처럼 역할이 재활용될 때 내용이 보존되는지 여부를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-262">Specific values can be set for the size of the local storage, as well as whether the contents are preserved when the role is recycled, as shown in the following image.</span></span>

![][ic719508]

<span data-ttu-id="7e8a8-263">또한 필요에 따라 로컬 저장소에 해당하는 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-263">You can also optionally specify an environment variable that corresponds to the local storage.</span></span>

<span data-ttu-id="7e8a8-264">기본적으로 Azure에 배포하는 모든 항목은 역할 인스턴스의 **approot** 폴더에 배치(및 압축을 풀게)됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-264">By default, everything that you deploy into Azure is placed (and unzipped) in the **approot** folder of the role instance.</span></span> <span data-ttu-id="7e8a8-265">압축을 푼 후에도 대부분 간단한 배포의 크기가 맞는 반면 **approot** 디렉터리에 할당된 공간은 제한되고 잘 정의되지 않습니다. 1GB 보다 작은 점은 합리적인 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-265">While most simple deployments will fit there even after unzipping, the space allocated for the **approot** directory is limited and not well-defined (less than 1 GB is a reasonable rule of thumb).</span></span> <span data-ttu-id="7e8a8-266">따라서 Azure에서 **approot** 폴더에 맞지 않는 대형 배포에 충분한 디스크 공간을 할당하려면 **로컬 저장소** 대화 상자를 사용하여 로컬 저장소 리소스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-266">Therefore, to ensure Azure allocates sufficient disk space for larger deployments that might not fit in the **approot** folder, you should set up a local storage resource using the **Local Storage** dialog.</span></span> <span data-ttu-id="7e8a8-267">이 작업을 수행하는 간단한 방법은 [대규모 배포 배포][Deploying Large Deployments]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-267">For an easy way to do this, see [Deploying Large Deployments][Deploying Large Deployments].</span></span>

<span data-ttu-id="7e8a8-268">**로컬 저장소** 대화 상자에 표시된 대로 리소스를 통해 Eclipse 도구 키트에서 자동으로 연결된 환경 변수를 사용하여 시작 스크립트에서 저장소 리소스를 쉽게 참조할 수 있습니다.(예: **startup.cmd**)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-268">You can easily reference the storage resource from startup scripts (for example, your **startup.cmd**) using the environment variable automatically associated by the Eclipse toolkit with the resource, as shown in the **Local Storage** dialog.</span></span> <span data-ttu-id="7e8a8-269">이 환경 변수는 시작 스크립트를 실행할 때 구성한 로컬 리소스의 전체 경로를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-269">That environment variable will contain the full path of the local resource you've configured at the time your startup script is executed.</span></span> 

<span data-ttu-id="7e8a8-270">로컬 저장소 리소스를 수정하려면 로컬 저장소 리소스를 선택하고 **로컬 저장소** 속성 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-270">To modify a local storage resource, select the local storage resource and click the **Edit** button in the **Local Storage** property page.</span></span> <span data-ttu-id="7e8a8-271">로컬 저장소 리소스 속성을 수정할 수 있게 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-271">A dialog will be opened allowing you to modify the local storage resource properties.</span></span> <span data-ttu-id="7e8a8-272">**확인** 을 눌러 로컬 저장소 리소스 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-272">Press **OK** to save the local storage resource values.</span></span>

<span data-ttu-id="7e8a8-273">로컬 저장소 리소스를 삭제하려면 로컬 저장소 리소스를 선택하고 **로컬 저장소** 속성 페이지에서 **제거** 단추를 클릭한 다음 **예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-273">To delete a local storage resource, select the local storage resource and click the **Remove** button in the **Local Storage** property page, and then click **Yes** to confirm the deletion.</span></span>

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a><span data-ttu-id="7e8a8-274">서버 구성 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-274">Server configuration properties</span></span>
<span data-ttu-id="7e8a8-275">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **서버 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-275">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Server Configuration**.</span></span> <span data-ttu-id="7e8a8-276">이 대화 상자에서 배포에 사용되는 JDK 및 Java 응용 프로그램 서버를 추가, 제거 및 수정하는 기능 뿐만 아니라 배포에서 사용하는 응용 프로그램(예: WAR, JAR 또는 EAR 파일)을 추가 또는 제거하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-276">Within this dialog, you have the ability to add, remove, and modify the JDK and Java application server used by your deployment, as well as add or remove the applications (such as WAR, JAR or EAR files) used by your deployment.</span></span>

### <a name="jdk-configuration"></a><span data-ttu-id="7e8a8-277">JDK 구성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-277">JDK configuration</span></span>
<span data-ttu-id="7e8a8-278">이 대화 상자를 사용하면 배포에 사용할 JDK 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-278">This dialog allows you to specify the JDK package to use for your deployment.</span></span> <span data-ttu-id="7e8a8-279">Windows에서 Eclipse를 사용하는 경우 Azure 에뮬레이터에서 실행할 때 로컬로 사용할 JDK 패키지를 지정할 수 있고 로컬 설치 프로그램을 Azure에 배포하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-279">If you are using Eclipse on Windows, you can specify the JDK package to use locally when running in the Azure emulator and you have the option to deploy that local installation to Azure.</span></span> <span data-ttu-id="7e8a8-280">비 Windows 운영 체제에서 에뮬레이터 JDK 설정이 적용되지 않고 Windows와 호환되지 않으므로 로컬에 설치된 JDK를 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-280">On non-Windows operating systems, the emulator JDK setting is not applicable and you cannot deploy the locally installed JDK since it is not compatible with Windows.</span></span> <span data-ttu-id="7e8a8-281">그러나 사용 중인 운영 체제에 관계 없이 항상 Azure에 배포할 타사 JDK 패키지를 선택하거나 대체 다운로드 위치에서 사용자 고유의 Windows 호환 가능 JDK 패키지를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-281">However, regardless of the operating system that you are using, you can always choose among the 3rd party JDK packages to deploy to Azure, or point at your own Windows-compatible JDK package from an alternate download location.</span></span>

<span data-ttu-id="7e8a8-282">다음은 Windows에서 JDK를 지정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-282">The following is an example of how you can specify a JDK on Windows:</span></span>

![][ic780647]

<span data-ttu-id="7e8a8-283">Windows에서 Eclipse를 사용하는 경우 계산 에뮬레이터와 함께 사용할 JDK를 지정할 수 있습니다. 이렇게 하려면 **에뮬레이터 배포** 섹션에서 **로컬로 테스트하기 위해 이 파일 경로에서 JDK 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-283">If you are using Eclipse on Windows, you can specify a JDK to use with the compute emulator; to do so, ensure **Use the JDK from this file path for testing locally** is checked in the **Emulator deployment** section.</span></span> <span data-ttu-id="7e8a8-284">그런 다음 JDK의 로컬 경로를 지정합니다. 사용하려는 JDK가 자동으로 선택되지 않은 경우 다른 JDK를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-284">Then, specify the local path to your JDK; you can browse to different JDK if the one you want to use is not selected automatically.</span></span> <span data-ttu-id="7e8a8-285">또한 Azure 클라우드 서비스에 JDK를 배포 하는 옵션도 있습니다. 이렇게 하려면 **클라우드 배포** 섹션에서 **내 로컬 JDK 배포(클라우드 저장소에 자동 업로드)** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-285">You also have the option to deploy your JDK to your Azure cloud service; to do so, select the **Deploy my local JDK (auto-upload to cloud storage)** option in the **Cloud deployment** section.</span></span>

<span data-ttu-id="7e8a8-286">참고: 비 Windows 운영 체제에서 **에뮬레이터 배포** 설정 및 **내 로컬 JDK 배포** 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-286">Note: On non-Windows operating systems, the **Emulator deployment** settings and the **Deploy my local JDK** option are not available.</span></span> <span data-ttu-id="7e8a8-287">다음 예제에서는 Mac 또는 다른 지원되는 비 Windows 운영 체제에서 JDK를 지정하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-287">The following example illustrates specifying a JDK on a Mac or other supported non-Windows operating system:</span></span>

![][ic789643]

<span data-ttu-id="7e8a8-288">사용하는 운영 체제에 관계 없이 JDK 패키지의 원본 및 형식에 다음과 같은 두 가지 **클라우드 배포** 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-288">Regardless of the operating system you are on, you have the following two **Cloud deployment** options for the source and type of your JDK package:</span></span>

* <span data-ttu-id="7e8a8-289">**Azure에서 사용할 수 있는 타사 JDK 패키지 배포**</span><span class="sxs-lookup"><span data-stu-id="7e8a8-289">**Deploy a 3rd party JDK package available on Azure**</span></span> 
* <span data-ttu-id="7e8a8-290">**사용자 지정 다운로드에서 배포**</span><span class="sxs-lookup"><span data-stu-id="7e8a8-290">**Deploy from a custom download**</span></span> 

<span data-ttu-id="7e8a8-291">**Azure에서 사용할 수 있는 타사 JDK 패키지 배포** 옵션을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7e8a8-291">If you are using the **Deploy a 3rd party JDK package available from Azure** option:</span></span>

1. <span data-ttu-id="7e8a8-292">**Azure에서 사용할 수 있는 타사 JDK 패키지 배포**라는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-292">Check the checkbox named **Deploy a 3rd party JDK package available from Azure**.</span></span>
2. <span data-ttu-id="7e8a8-293">드롭다운 목록에서 Azure에서 사용할 수 있는 타사 JDK 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-293">From the drop-down list, select the 3rd party JDK package that is available on Azure.</span></span>
3. <span data-ttu-id="7e8a8-294">프로그램 **JDK** 탭은 Windows에서 다음과 유사: ![][ic780648] 및 Mac OS에서 다음과 유사 합니다 또는 지원 되는 다른 Windows 이외의 운영 체제:![][ic789643]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-294">Your **JDK** tab will look similar to the following on Windows:  ![][ic780648] And it will look similar to the following on Mac OS or other supported non-Windows operating systems:  ![][ic789643]</span></span>
4. <span data-ttu-id="7e8a8-295">**확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-295">Click **OK** to save your changes.</span></span>
5. <span data-ttu-id="7e8a8-296">타사 JDK 패키지 공급자에서 라이선스 규약에 동의하는지 묻는 메시지가 나타나면 라이선스 약관을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-296">When prompted to accept the license agreement from the 3rd party JDK package provider, review the license terms.</span></span> <span data-ttu-id="7e8a8-297">약관에 동의한 것으로 가정하면 **예**를 클릭하여 **라이선스 규약에 동의** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-297">Assuming you accept the terms, click **Yes** to close the **Accept license agreement** dialog.</span></span>
    <span data-ttu-id="7e8a8-298">항목이 **Azure에서 사용할 수 있는 타사 JDK 패키지 배포** 옵션에 대한 드롭다운 목록에 표시되는 기본적인 논리는 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-298">Note that the underlying logic for which items appear in the drop-down list for the **Deploy a 3rd party JDK package available from Azure** option can be customized.</span></span> <span data-ttu-id="7e8a8-299">항목을 사용자 지정하려면 **JDK** 대화 상자에서 **사용자 지정** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-299">To customize the items, in the **JDK** dialog, click the **Customize** link.</span></span> <span data-ttu-id="7e8a8-300">**JDK** 속성 페이지를 닫고 Eclipse에서 **componentsets.xml** 파일을 열어 필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-300">This will close the **JDK** property page and open the **componentsets.xml** file in Eclipse, which you can then modify as needed.</span></span> <span data-ttu-id="7e8a8-301">**componentsets.xml**에 대한 설명서는 **componentsets.xml** 파일 자체에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-301">Documentation for **componentsets.xml** is included in the **componentsets.xml** file itself.</span></span>

<span data-ttu-id="7e8a8-302">**사용자 지정 다운로드에서 JDK 배포** 옵션을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7e8a8-302">If you are using the **Deploy a JDK from a custom download** option:</span></span>

1. <span data-ttu-id="7e8a8-303">JDK 설치 디렉터리의 ZIP을 만들어서 디렉터리 노드 자체가 콘텐츠가 아닌 ZIP 구조의 하위가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-303">Create a ZIP of your JDK installation directory, ensuring that the directory node itself is the child of the ZIP structure, and not its contents.</span></span> <span data-ttu-id="7e8a8-304">나중에 필요하기 때문에 디렉터리의 이름을 기록하고 이 JDK 설치가 Windows 가상 컴퓨터에 배포된다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-304">Take note of the name of the directory, as you will need it later, and keep in mind this JDK installation will be deployed to a Windows virtual machine.</span></span>
2. <span data-ttu-id="7e8a8-305">ZIP을 Azure 저장소 계정에 Blob로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-305">Upload the ZIP into your Azure storage account as a blob.</span></span> <span data-ttu-id="7e8a8-306">Azure 저장소에 Blob를 업로드하는 경우 외부에서 사용 가능한 도구를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-306">You can do this using an externally available tool for uploading blobs to Azure storage.</span></span> <span data-ttu-id="7e8a8-307">개인 Blob을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-307">It is recommended to use a private blob.</span></span> <span data-ttu-id="7e8a8-308">ZIP 내용의 Blob URL을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-308">Take note of the blob URL of the ZIP contents.</span></span>
3. <span data-ttu-id="7e8a8-309">**사용자 지정 다운로드에서 JDK 배포**라는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-309">Check the checkbox named **Deploy a JDK from a custom download**.</span></span>
    <span data-ttu-id="7e8a8-310">Azure Storage 계정에서 다운로드하려는 경우 **저장소 계정** 드롭다운 목록에서 저장소 계정을 선택(**계정** 링크를 클릭하여 목록의 내용을 수정할 수 있습니다.)하며 이는 부분적으로 **URL** 필드를 입력하고 URL의 나머지 부분을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-310">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL.</span></span> <span data-ttu-id="7e8a8-311">Azure Storage를 사용하려면 **저장소 계정** 드롭 다운 목록에서 **(없음)**을 선택하고 **URL** 필드에서 JDK 다운로드에 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-311">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your JDK download in the **URL** field.</span></span> <span data-ttu-id="7e8a8-312">Azure 저장소를 사용하는 경우 URL의 Blob 이름은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-312">If using Azure storage, blob names in the URL must be lowercase.</span></span>
4. <span data-ttu-id="7e8a8-313">**JAVA_HOME** 텍스트 상자가 올바른 디렉터리 이름을 참조하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-313">Ensure that the **JAVA_HOME** textbox refers to the correct directory name.</span></span> <span data-ttu-id="7e8a8-314">기본적으로 동일한 JDK 디렉터리 이름을 로컬 사용을 위해 선택한 값으로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-314">By default, it will reference the same JDK directory name as the value you chose for your local use.</span></span> <span data-ttu-id="7e8a8-315">그러나 ZIP에 포함된 디렉터리에 다른 이름이 있는 경우(예를 들어 다른 버전 사용으로 인해) 이 설정이 (계산 에뮬레이터가 아닌) 클라우드에서 사용되기 때문에 그에 따라 **JAVA_HOME** 텍스트 상자의 디렉터리 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-315">But if the directory contained in the ZIP has a different name (for example, due to using a different version), update the directory name in the **JAVA_HOME** textbox accordingly, since this setting will be used in the cloud (not in the compute emulator).</span></span>
5. <span data-ttu-id="7e8a8-316">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-316">Click **OK** to save your changes.</span></span>

<span data-ttu-id="7e8a8-317">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-317">That's it.</span></span> <span data-ttu-id="7e8a8-318">이제 클라우드를 작성하면 패키지 크기가 훨씬 더 작지만 빌드 프로세스는 일반적으로 시간이 적게 걸려야 하고 클라우드에 게시할 때 배포 자체도 시간이 적게 소요되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-318">Now, when you build for the cloud, you will notice the package size will be much smaller, the build process should typically take less time, and the deployment itself when you publish to the cloud should also take less time.</span></span> <span data-ttu-id="7e8a8-319">**내 로컬 JDK 배포(클라우드 저장소에 자동 업로드)** 또는 **사용자 지정 다운로드에서 JDK 배포** 옵션은 응용 프로그램을 클라우드에 배포하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-319">Note that the **Deploy my local JDK (auto-upload to cloud storage)** or **Deploy a JDK from a custom download** options are in effect only when your application is deployed in the cloud.</span></span> <span data-ttu-id="7e8a8-320">계산 에뮬레이터 환경에 영향을 주지 않습니다. 계산 에뮬레이터에 배포하는 경우 여전히 로컬 버전의 구성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-320">They have no effect on your compute emulator experience; the local version of the components will still be used when you deploy to the compute emulator.</span></span> 

### <a name="server-configuration"></a><span data-ttu-id="7e8a8-321">서버 구성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-321">Server configuration</span></span>
<span data-ttu-id="7e8a8-322">다음은 응용 프로그램 서버를 지정할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-322">The following is an example of how you can specify an application server.</span></span>

![][ic796926]

<span data-ttu-id="7e8a8-323">**이 형식의 서버 배포** 확인란을 선택한 다음 사용하려는 응용 프로그램 서버의 형식을 선택하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-323">Verify that the **Deploy a server of this type** checkbox is selected, and then choose the type of application server you want to use.</span></span>

<span data-ttu-id="7e8a8-324">클라우드 배포에 사용할 서버를 지정하는 경우 다음과 같은 옵션의 장점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-324">For specifying a server to use for cloud deployment, you can take advantage of the following options:</span></span>

1. <span data-ttu-id="7e8a8-325">**Azure에서 사용할 수 있는 타사 서버 배포** - 배포 효율성 및 단순성이 중요하고 서버가 사용자 지정 구성을 요구하지 않는 개발/테스트 시나리오에서 특히 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-325">**Deploy a 3rd party server available on Azure** - this is especially applicable in dev/test scenarios where deployment efficiency and simplicity is a priority and the server does not require a custom configuration.</span></span> <span data-ttu-id="7e8a8-326">또는 시작 지점으로 이러한 서버 중 하나를 사용할 때 배포의 시작 논리에 적절한 서버 사용자 지정 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-326">Or when you want to use one of those servers as the starting point but you include appropriate server customization steps in your deployment's startup logic.</span></span>
2. <span data-ttu-id="7e8a8-327">**사용자 지정 다운로드에서 배포** - 클라우드에서 사용하려는 특별히 준비되고 구성된 서버가 있는 경우 프로덕션 시나리오에서 특히 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-327">**Deploy from a custom download** - this is especially applicable in production scenarios when you have a specially prepared and configured server that you want to use in the cloud.</span></span>
3. <span data-ttu-id="7e8a8-328">**내 로컬 서버 설치 배포** - 이 로컬 서버 설치가 이미 사용할 사용자 지정으로 구성된 경우 특히 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-328">**Deploy my local server installation** - this is especially applicable in if your local server installation is already custom-configured for your use.</span></span> <span data-ttu-id="7e8a8-329">또한 이 옵션을 선택하는 경우 아래에서 **로컬 서버 경로** 텍스트 상자에 로컬 서버 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-329">If you choose this option, you must also specify your local server's path in the **Local server path** text box below.</span></span>

<span data-ttu-id="7e8a8-330">**Azure에서 사용할 수 있는 타사 서버 배포** 옵션을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7e8a8-330">If you are using the **Deploy a 3rd party server available on Azure** option:</span></span>

1. <span data-ttu-id="7e8a8-331">**Azure에서 사용할 수 있는 타사 서버 배포**라는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-331">Check the checkbox named **Deploy a 3rd party server available on Azure**.</span></span>
2. <span data-ttu-id="7e8a8-332">드롭다운 메뉴에서 클라우드의 배포를 통해 사용하려는 서버 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-332">From the dropdown menu, select the desired server software to use with your deployment in the cloud.</span></span> <span data-ttu-id="7e8a8-333">이전에 사용한 서버 형식을 지정하는 경우 해당 서버 형식과 같은 제품군에 있는 클라우드 서버만 선택할 수 있도록 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-333">Note, if you already specified a type of server to use earlier, you will be limited to choosing only a cloud server that is in the same family as that server type.</span></span> <span data-ttu-id="7e8a8-334">하지만 서버 형식을 선택하지 않은 경우 Azure에서 현재 사용할 수 있는 서버 중에서 선택할 수 있고 서버 형식을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-334">But if you did not choose a server type, you can choose from any of the servers that are currently available on Azure and the server type will be automatically selected for you.</span></span>
3. <span data-ttu-id="7e8a8-335">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-335">Click **OK** to save your changes.</span></span>

<span data-ttu-id="7e8a8-336">**사용자 지정 다운로드에서 배포** 옵션을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7e8a8-336">If using the **Deploy from a custom download** option:</span></span>

1. <span data-ttu-id="7e8a8-337">앞의 단계에 따라 서버 형식을 이미 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-337">Make sure that you have already selected a server type according to the preceding steps.</span></span> <span data-ttu-id="7e8a8-338">선택한 서버 형식과 같은 제품군에서처럼 플러그인에 사용자 지정 다운로드에서 서버를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-338">This tells the plugin how to deploy the server from your custom download, as it must be from the same family as your selected server type.</span></span>
2. <span data-ttu-id="7e8a8-339">**사용자 지정 다운로드에서 배포**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-339">Check the checkbox named **Deploy from a custom download**.</span></span>
    <span data-ttu-id="7e8a8-340">Azure Storage 계정에서 다운로드하려는 경우 **저장소 계정** 드롭다운 목록에서 저장소 계정을 선택(**계정** 링크를 클릭하여 목록의 내용을 수정할 수 있습니다.)하며 이는 부분적으로 **URL** 필드를 입력하고 URL의 나머지 부분을 서버 다운로드 ZIP에 입력합니다.(Azure Storage를 사용할 때 URL의 Blob 이름은 소문자여야 함)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-340">If you want to download from your Azure storage account, select the storage account from the **Storage account** drop-down list (you can click the **Accounts** link to modify what is in the list), which will partially fill in the **URL** field, and then fill in the remaining portion of the URL to your server download ZIP (when using Azure storage, blob names in the URL must be lowercase).</span></span> <span data-ttu-id="7e8a8-341">Azure Storage를 사용하려면 **저장소 계정** 드롭다운 목록에서 **(없음)**을 선택하고 **URL** 필드에서 서버 다운로드 ZIP에 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-341">If you do not want to use Azure storage, select **(none)** from the **Storage account** drop-down list, and enter the URL to your server download ZIP in the **URL** field.</span></span> <span data-ttu-id="7e8a8-342">ZIP은 응용 프로그램 서버 설치 디렉터리를 나타내는 하위 폴더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-342">The ZIP would contain a child folder representing your application server installation directory.</span></span> <span data-ttu-id="7e8a8-343">예를 들어 Apache Tomcat 7.0.35에 zip를 사용하는 경우 zip 내에서 하위 폴더는 **apache-tomcat-7.0.35**와 같은 설치 디렉터리를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-343">For example, if you are using a zip for Apache Tomcat 7.0.35, within the zip would be the child folder representing the installation directory, such as **apache-tomcat-7.0.35**.</span></span> 
3. <span data-ttu-id="7e8a8-344">홈 디렉터리 환경 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-344">Specify the value for the home directory environment variable.</span></span> <span data-ttu-id="7e8a8-345">값이 있는 경우 기본적으로 로컬 응용 프로그램 서버에 사용되는 값이지만 클라우드 응용 프로그램 서버가 로컬 응용 프로그램 서버와 다른 경우 다른 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-345">It will default to the value used for your local application server, if any, but you can specify a different value if your cloud application server is different from your local application server.</span></span> <span data-ttu-id="7e8a8-346">하지만 클라우드 응용 프로그램 서버가 이전에 선택한 형식의 서버와 동일한 제품군인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-346">However, you need to make sure that your cloud application server is of the same family as the server type selected earlier.</span></span>
    <span data-ttu-id="7e8a8-347">나중에 클라우드 응용 프로그램 서버 zip 파일을 업데이트하는 경우 홈 디렉터리 설정을 수동으로 변경하거나 로컬 설정과 다시 일치시킬 수 있습니다.(로컬 응용 프로그램 서버도 변경한 경우)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-347">If you update your cloud application server zip in the future, you can manually change the home directory setting, or, to have it again match your local setting (if you changed your local application server too).</span></span>
4. <span data-ttu-id="7e8a8-348">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-348">Click **OK** to save your changes.</span></span>

<span data-ttu-id="7e8a8-349">항목이 **서버 구성** 속성 페이지의 **서버** 탭에 표시되는 기본 논리는 사용자 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-349">The underlying logic for which items appear in the **Server** tab of the **Server Configuration** property page can be customized.</span></span> <span data-ttu-id="7e8a8-350">이 기본값 이상으로 확장해야 하는 경우 또는 다른 서버를 추가하려는 경우 필요할 수 있는 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-350">This is an advanced feature that you might need if your needs extend beyond the default values or if you want to add other servers.</span></span> <span data-ttu-id="7e8a8-351">논리를 사용자 지정하려면 **서버** 대화 상자에서 **사용자 지정** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-351">To customize the logic, in the **Server** dialog, click the **Customize** link.</span></span> <span data-ttu-id="7e8a8-352">**서버 구성** 속성 페이지를 닫고 Eclipse에서 **componentsets.xml** 파일을 엽니다. 이렇게 하면 서버 구성 템플릿을 확장할 필요에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-352">This will close the **Server Configuration** property page and open the **componentsets.xml** file in Eclipse, which you can then modify as needed to extend the server configuration template.</span></span> <span data-ttu-id="7e8a8-353">**componentsets.xml**에 대한 설명서는 **componentsets.xml** 파일 자체에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-353">Documentation for **componentsets.xml** is included in the **componentsets.xml** file itself.</span></span>

<span data-ttu-id="7e8a8-354">**내 로컬 서버 배포(클라우드 저장소에 자동 업로드)** 옵션을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7e8a8-354">If you are using the **Deploy my local server (auto-upload to cloud storage)** option:</span></span>

1. <span data-ttu-id="7e8a8-355">**내 로컬 서버 배포(클라우드 저장소에 자동 업로드)**라는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-355">Check the checkbox named **Deploy my local server (auto-upload to cloud storage)**.</span></span>
2. <span data-ttu-id="7e8a8-356">**저장소 계정** 드롭다운 목록을 사용하여 **(자동)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-356">Using the **Storage account** drop-down list, select **(auto)**.</span></span> <span data-ttu-id="7e8a8-357">여기에서 **(자동)**을 지정하는 경우 Eclipse 도구 키트는 **Azure에 게시** 대화 상자의 배포에 대해 선택한 것과 같은 동일한 저장소 계정을 서버에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-357">If you specify **(auto)** here, the Eclipse toolkit will use the same storage account for your server as the one you select for your deployment in the **Publish to Azure** dialog.</span></span>
3. <span data-ttu-id="7e8a8-358">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-358">Click **OK** to save your changes.</span></span>

<span data-ttu-id="7e8a8-359">다음 조건 중 하나가 충족되는 경우 **로컬 서버 경로** 텍스트 상자의 컴퓨터에서 서버 설치 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-359">Select a server installation path on your computer in the **Local server path** text box if any of the following conditions are true:</span></span>

* <span data-ttu-id="7e8a8-360">에뮬레이터에서 배포를 테스트하려고 합니다.(Windows에만 적용)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-360">You want to test your deployment in the emulator (applies to Windows only).</span></span>
* <span data-ttu-id="7e8a8-361">로컬에 설치된 서버를 클라우드에 배포하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-361">You want to deploy your locally installed server to the cloud.</span></span>
* <span data-ttu-id="7e8a8-362">또한 클라우드에서 고유한 사용자 지정 서버 다운로드를 사용하려는 경우 **내 로컬 서버 배포(클라우드 저장소에 자동 업로드)** 옵션을 위에서 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-362">You want to use a custom server download of your own in the cloud, in which case, also ensure the **Deploy my local server (auto-upload to cloud storage)** option is selected above.</span></span>

<span data-ttu-id="7e8a8-363">위의 옵션이 상황에 적용되지 않는 경우 로컬 서버 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-363">If none of the preceding options apply to your situation, the local server setting is optional.</span></span>

### <a name="applications-configuration"></a><span data-ttu-id="7e8a8-364">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-364">Applications configuration</span></span>
<span data-ttu-id="7e8a8-365">다음은 응용 프로그램을 지정할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-365">The following is an example of how you can specify an application.</span></span>

![][ic719512]

<span data-ttu-id="7e8a8-366">**추가**를 클릭하여 다른 응용 프로그램을 추가하거나 **제거**를 클릭하여 응용 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-366">Click **Add** to add another application, or **Remove** to remove an application.</span></span> <span data-ttu-id="7e8a8-367">효율성을 위해 클라우드로 배포할 때 응용 프로그램의 원본에 다운로드를 사용하려는 경우 [구성 요소 속성](#components_properties) 을 사용하여 URL, 저장소 계정 등을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-367">For efficiency purposes, if you want to use a download for the source of an application when deploying to the cloud, use the [components properties](#components_properties) to specify a URL, storage account, etc.</span></span> 

<span data-ttu-id="7e8a8-368">2014년 4월 릴리스부터, 응용 프로그램은 자동으로 배포에 대해 선택한 것과 동일한 저장소 계정에 업로드됩니다.(**eclipsedeploy** 컨테이너에서)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-368">Beginning with the April 2014 release, your applications are automatically uploaded into the same storage account (under the **eclipsedeploy** container) as the one selected for your deployment.</span></span> <span data-ttu-id="7e8a8-369">배포의 시작 논리는 먼저 해당 저장소 계정에서 해당 응용 프로그램을 다운로드하는 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-369">The startup logic of your deployment contains a step that first downloads those applications from that storage account.</span></span> <span data-ttu-id="7e8a8-370">즉, 전체 패키지를 다시 빌드하고 배포하지 않고도 해당 저장소 계정에 직접 응용 프로그램의 최신 버전을 수동으로 업로드하거나(예: Azure 포털 사용) 도구 키트에서 원래 업로드된 WAR 파일을 대체하여 배포에서 응용 프로그램을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-370">This means that you may upgrade your applications in your deployment without needing to rebuild and redeploy the entire package, by manually uploading newer versions of the application directly into that storage account (using the Azure portal for example), replacing the WAR files originally uploaded there by the toolkit.</span></span> <span data-ttu-id="7e8a8-371">그런 다음 Azure 관리 포털을 사용하거나 명령줄 유틸리티를 통해 이러한 모든 역할 인스턴스를 재활용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-371">Then, just initiate the recycling of all those role instances using Azure's management portal again, or via command line utilities.</span></span> <span data-ttu-id="7e8a8-372">(Eclipse 도구 키트 내에서 직접 재활용하는 역할 트리거 기능은 현재 지원되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="7e8a8-372">(Triggering role recycling directly from within the Eclipse toolkit is not currently supported.)</span></span>

### <a name="notes-about-server-configuration"></a><span data-ttu-id="7e8a8-373">서버 구성에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="7e8a8-373">Notes about server configuration</span></span>
<span data-ttu-id="7e8a8-374">**서버 구성** 속성 페이지를 통해 만든 변경 사항은 package.xml 파일의 `<component>` 요소를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-374">Changes made through the **Server configuration** property page are reflected in the `<component>` elements of the package.xml file.</span></span>

<span data-ttu-id="7e8a8-375">JDK 또는 응용 프로그램 서버에 대해 **자동으로 업로드...** 또는 **다운로드에서 배포...** 옵션을 사용하거나 (계산 에뮬레이터가 아닌) 클라우드에 빌드 또는 네트워크에 연결하는 경우 Ant 빌더에서 다운로드의 가용성을 확인하는 대로 빌드 콘솔 출력에 다음과 같은 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-375">When you use the **Automatically upload...** or **Deploy from download...** options for either the JDK or application server, and you are building for the cloud (not the compute emulator), and you are connected to the network, you may notice build messages such as the following in the Console output, as the Ant builder verifies the download's availability:</span></span>

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

<span data-ttu-id="7e8a8-376">**다운로드에서 배포 …** 옵션을 선택한 경우 다음과 같은 경고가 표시될 수 있지만 빌드는 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-376">If you selected the **Deploy from download...** option, the following warning may be shown, but the build will continue:</span></span>

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

<span data-ttu-id="7e8a8-377">이 경고는 다운로드의 가용성이 확인되지 않았다는 점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-377">This warning is the only indication that the download's availability hasn't been verified.</span></span> <span data-ttu-id="7e8a8-378">따라서 배포가 어떤 이유로 클라우드에서 실패하는 경우 이 경고를 수신하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-378">So if a deployment fails in the cloud for some reason, check to see if you received this warning.</span></span>

<span data-ttu-id="7e8a8-379">다운로드 확인을 사용하지 않도록 설정하려는 경우(예: 빌드를 불필요하게 느리게 만든다고 생각하는 경우) package.xml의 `<windowsazurepackage>` 요소에서 `verifydownloads` 특성을 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-379">If you want to disable the download verification (for example, if you feel it unnecessarily slows down the build), set the `verifydownloads` attribute to `false` in the `<windowsazurepackage>` element of package.xml:</span></span> 

`<windowsazurepackage verifydownloads="false" ...>` 

<span data-ttu-id="7e8a8-380">**자동으로 업로드 …** 옵션을 선택한 경우 콘솔 창에서 업로드가 필요하면 5초 마다 업로드의 진행률을 보고하는 빌드 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-380">If you selected the **Automatically upload...** option, then in the console window you will see build messages reporting the progress of the upload every 5 seconds, whenever an upload is necessary.</span></span>

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a><span data-ttu-id="7e8a8-381">SSL 오프로딩 속성</span><span class="sxs-lookup"><span data-stu-id="7e8a8-381">SSL offloading properties</span></span>
<span data-ttu-id="7e8a8-382">Eclipse의 프로젝트 탐색기에서 역할에 대한 상황에 맞는 메뉴를 열고 **Azure**를 클릭한 다음 **SSL 오프로딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-382">Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **SSL Offloading**.</span></span> 

![][ic719481]

<span data-ttu-id="7e8a8-383">이 대화 상자 내에서 SSL 오프로딩을 사용할 수 있으며 이를 통해 Java 응용 프로그램 서버에서 SSL을 구성하지 않고 Azure의 Java 배포에서 HTTPS(Hypertext Transfer Protocol Secure) 지원을 손쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-383">Within this dialog, you can enable SSL offloading, allowing you to easily enable Hypertext Transfer Protocol Secure (HTTPS) support in your Java deployment on Azure, without requiring you to configure SSL in your Java application server.</span></span> <span data-ttu-id="7e8a8-384">자세한 내용은 [SSL 오프로딩][SSL Offloading] 및 [SSL 오프로딩을 사용하는 방법][How to Use SSL Offloading]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-384">For more information, see [SSL Offloading][SSL Offloading] and [How to Use SSL Offloading][How to Use SSL Offloading].</span></span>

## <a name="see-also"></a><span data-ttu-id="7e8a8-385">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7e8a8-385">See Also</span></span>
<span data-ttu-id="7e8a8-386">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-386">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="7e8a8-387">[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-387">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="7e8a8-388">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-388">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="7e8a8-389">[Azure 프로젝트 속성][Azure Project Properties]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-389">[Azure Project Properties][Azure Project Properties]</span></span>

<span data-ttu-id="7e8a8-390">[Azure Storage 계정 목록][Azure Storage Account List]</span><span class="sxs-lookup"><span data-stu-id="7e8a8-390">[Azure Storage Account List][Azure Storage Account List]</span></span>

<span data-ttu-id="7e8a8-391">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e8a8-391">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
