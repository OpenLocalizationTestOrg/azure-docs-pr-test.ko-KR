---
title: "클라우드 서비스를 구성하는 방법(클래식 포털) | Microsoft Docs"
description: "Azure에서 클라우드 서비스를 구성하는 방법에 대해 알아봅니다. 또한 클라우드 서비스 구성을 업데이트하고 역할 인스턴스에 대한 원격 액세스를 구성하는 방법도 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 39bb294c96ce0c12d91cf8b3488ac3e1a7b2f7b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="87f35-104">클라우드 서비스를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="87f35-104">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87f35-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="87f35-105">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="87f35-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="87f35-106">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
> 
> 

<span data-ttu-id="87f35-107">Azure 클래식 포털에서 클라우드 서비스에 가장 일반적으로 사용되는 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-107">You can configure the most commonly used settings for a cloud service in the Azure classic portal.</span></span> <span data-ttu-id="87f35-108">또는 구성 파일을 직접 업데이트하려는 경우 업데이트할 서비스 구성 파일을 다운로드한 후 업데이트된 파일을 업로드하고 구성 변경 내용으로 클라우드 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-108">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="87f35-109">어느 방법이든 모든 역할 인스턴스에 구성 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-109">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="87f35-110">Azure 클래식 포털을 통해 [Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결을 사용](cloud-services-role-enable-remote-desktop.md)</span><span class="sxs-lookup"><span data-stu-id="87f35-110">The Azure classic portal also allows you to [enable Remote Desktop Connection for a Role in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)</span></span>

<span data-ttu-id="87f35-111">Azure는 각 역할에 둘 이상의 역할 인스턴스가 있는 경우에만 구성 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-111">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="87f35-112">이에 따라, 가상 컴퓨터 하나는 클라이언트 요청을 처리하고 다른 하나는 업데이트를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-112">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="87f35-113">자세한 내용은 [Service Level Agreements(서비스 수준 약정)](https://azure.microsoft.com/support/legal/sla/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87f35-113">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="87f35-114">클라우드 서비스 변경하기</span><span class="sxs-lookup"><span data-stu-id="87f35-114">Change a cloud service</span></span>
1. <span data-ttu-id="87f35-115">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-115">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
   
    ![구성 페이지](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    <span data-ttu-id="87f35-117">**구성** 페이지에서 모니터링을 구성하고, 역할 설정을 업데이트하고, 게스트 운영 체제 및 역할 인스턴스 패밀리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-117">On the **Configure** page, you can configure monitoring, update role settings, and choose the guest operating system and family for role instances.</span></span> 
2. <span data-ttu-id="87f35-118">**모니터링**에서 모니터링 수준을 Verbose 또는 Minimal로 설정하고 자세한 모니터링에 필요한 진단 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-118">In **monitoring**, set the monitoring level to Verbose or Minimal, and configure the diagnostics connection strings that are required for verbose monitoring.</span></span>
3. <span data-ttu-id="87f35-119">역할을 기준으로 그룹화된 서비스 역할의 경우 다음 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-119">For service roles (grouped by role), you can update the following settings:</span></span>
   
    * <span data-ttu-id="87f35-120">**설정** 서비스 구성 파일(.cscfg)의 *ConfigurationSettings* 요소에 지정된 기타 구성 설정의 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-120">**Settings** Modify the values of miscellaneous configuration settings that are specified in the *ConfigurationSettings* elements of the service configuration (.cscfg) file.</span></span>

    * <span data-ttu-id="87f35-121">**인증서**</span><span class="sxs-lookup"><span data-stu-id="87f35-121">**Certificates**</span></span>  
        <span data-ttu-id="87f35-122">역할의 SSL 암호화에 사용 중인 인증서 지문을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-122">Change the certificate thumbprint that's being used in SSL encryption for a role.</span></span> <span data-ttu-id="87f35-123">인증서를 변경하려면 먼저 새 인증서를 업로드해야 합니다( **인증서** 페이지).</span><span class="sxs-lookup"><span data-stu-id="87f35-123">To change a certificate, you must first upload the new certificate (on the **Certificates** page).</span></span> <span data-ttu-id="87f35-124">그런 다음, 역할 설정에 표시되는 인증서 문자열에서 인증서 지문을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-124">Then update the thumbprint in the certificate string displayed in the role settings.</span></span>
4. <span data-ttu-id="87f35-125">**운영 체제**에서 역할 인스턴스의 버전이나 운영 체제 제품군을 변경하거나 **자동**을 선택하여 현재 운영 체제 버전의 자동 업데이트를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-125">In **operating system**, you can change the operating system family or version for role instances, or choose **Automatic** to enable automatic updates of the current operating system version.</span></span> <span data-ttu-id="87f35-126">운영 체제 설정은 웹 역할 및 작업자 역할에는 적용되지만 가상 컴퓨터에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-126">The operating system settings apply to web roles and worker roles, but do not affect Virtual Machines.</span></span>
   
    <span data-ttu-id="87f35-127">배포하는 동안 모든 역할 인스턴스에 최신 운영 체제 버전이 설치되며 운영 체제는 기본적으로 자동 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-127">During deployment, the most recent operating system version is installed on all role instances, and the operating systems are updated automatically by default.</span></span> 
   
    <span data-ttu-id="87f35-128">코드의 호환성 요구 사항으로 인해 다른 운영 체제 버전에서 클라우드 서비스를 실행하기 위해 필요한 경우 운영 체제 제품군 및 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-128">If you need for your cloud service to run on a different operating system version because of compatibility requirements in your code, you can choose an operating system family and version.</span></span> <span data-ttu-id="87f35-129">특정 운영 체제 버전을 선택하면 클라우드 서비스를 위한 자동 운영 체제 업데이트가 일시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-129">When you choose a specific operating system version, automatic operating system updates for the cloud service are suspended.</span></span> <span data-ttu-id="87f35-130">운영 체제가 업데이트를 받도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-130">You will need to ensure the operating systems receive updates.</span></span>
   
    <span data-ttu-id="87f35-131">앱과 최신 운영 체제 버전 사이의 호환성 문제를 모두 해결하면 해당 운영 체제 버전을 **자동**으로 설정하여 자동 운영 체제 업데이트를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-131">If you resolve all compatibility issues that your apps have with the most recent operating system version, you can enable automatic operating system updates by setting the operating system version to **Automatic**.</span></span> 
   
    ![OS 설정](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. <span data-ttu-id="87f35-133">구성 설정을 저장하려면 역할 인스턴스에 적용하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-133">To save your configuration settings, and push them to the role instances, click **Save**.</span></span> <span data-ttu-id="87f35-134">변경 내용을 취소하려면 **최소**를 클릭합니다. **저장** 및 **취소**는 설정 변경 후 명령 모음에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-134">(Click **Discard** to cancel the changes.) **Save** and **Discard** are added to the command bar after you change a setting.</span></span>

## <a name="update-a-cloud-service-configuration-file"></a><span data-ttu-id="87f35-135">클라우드 서비스 구성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="87f35-135">Update a cloud service configuration file</span></span>
1. <span data-ttu-id="87f35-136">현재 구성과 함께 클라우드 서비스 구성 파일(.cscfg)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-136">Download a cloud service configuration file (.cscfg) with the current configuration.</span></span> <span data-ttu-id="87f35-137">클라우드 서비스의 **구성** 페이지에서 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-137">On the **Configure** page for the cloud service, click **Download**.</span></span> <span data-ttu-id="87f35-138">**저장** 또는 **다른 이름으로 저장**을 클릭하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-138">Then click **Save**, or click **Save As** to save the file.</span></span>
2. <span data-ttu-id="87f35-139">서비스 구성 파일을 업데이트한 후 구성 업데이트를 업로드하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-139">After you update the service configuration file, upload and apply the configuration updates:</span></span>
   
   1. <span data-ttu-id="87f35-140">**구성** 페이지에서 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-140">On the **Configure** page, click **Upload**.</span></span>
      
       ![구성 업로드](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. <span data-ttu-id="87f35-142">**구성 파일**에서 **찾아보기**를 사용하여 업데이트된 .cscfg 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-142">In **Configuration file**, use **Browse** to select the updated .cscfg file.</span></span>
   3. <span data-ttu-id="87f35-143">클라우드 서비스에 인스턴스가 하나뿐인 역할이 포함된 경우 **Apply configuration even if one or more roles contain a single instance** 확인란을 선택하여 역할의 구성 업데이트를 진행하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-143">If your cloud service contains any roles that have only one instance, select the **Apply configuration even if one or more roles contain a single instance** check box to enable the configuration updates for the roles to proceed.</span></span>
      
       <span data-ttu-id="87f35-144">모든 역할에 대해 두 개 이상의 인스턴스를 정의하지 않는 경우 Azure는 서비스 구성 업데이트 과정에서 최소 99.95%의 클라우드 서비스 가용성을 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-144">Unless you define at least two instances of every role, Azure cannot guarantee at least 99.95 percent availability of your cloud service during service configuration updates.</span></span> <span data-ttu-id="87f35-145">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87f35-145">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
   4. <span data-ttu-id="87f35-146">**확인** (확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-146">Click **OK** (checkmark).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87f35-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87f35-147">Next steps</span></span>
* <span data-ttu-id="87f35-148">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-148">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="87f35-149">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87f35-149">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="87f35-150">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="87f35-150">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* [<span data-ttu-id="87f35-151">Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="87f35-151">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>](cloud-services-role-enable-remote-desktop.md)
* <span data-ttu-id="87f35-152">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="87f35-152">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

