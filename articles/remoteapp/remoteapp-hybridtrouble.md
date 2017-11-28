---
title: "RemoteApp 하이브리드 컬렉션 만들기 aaaTroubleshoot | Microsoft Docs"
description: "자세한 내용은 방법 tootroubleshoot RemoteApp 하이브리드 컬렉션 만들기 실패"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="9ccf0-103">Azure RemoteApp 하이브리드 컬렉션 만들기 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9ccf0-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ccf0-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9ccf0-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9ccf0-106">하이브리드 컬렉션에서 호스트 되 고 hello Azure 클라우드 있지만 데이터에 액세스 하면 사용자와 로컬 네트워크에 저장 된 리소스에 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="9ccf0-107">사용자는 Azure Active Directory와 동기화 또는 페더레이션된 회사 자격 증명으로 로그인하여 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="9ccf0-108">기존 Azure 가상 네트워크를 사용하는 하이브리드 컬렉션을 배포하거나 새 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="9ccf0-109">Azure RemoteApp이 향후 증가할 것을 예상하여 CIDR 범위가 충분히 큰 가상 네트워크 서브넷을 만들거나 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="9ccf0-110">컬렉션을 아직 만들지 않았나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-110">Haven't created your collection yet?</span></span> <span data-ttu-id="9ccf0-111">참조 [하이브리드 컬렉션 만들기](remoteapp-create-hybrid-deployment.md) hello 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="9ccf0-112">Hello 방식으로 생각 해야 hello 컬렉션 작동 하지 않는 경우 또는 컬렉션을 만드는 데 문제가 있는 hello 다음 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="9ccf0-113">이미지가 올바르지 않음</span><span class="sxs-lookup"><span data-stu-id="9ccf0-113">Your image is invalid</span></span>
<span data-ttu-id="9ccf0-114">컬렉션에 대 한 Azure tooprovision 대기 중인 때 "GoldImageInvalid" 같은 메시지가 나타나면 템플릿 이미지 hello를 충족 하지 않는 것 [이미지 요구 사항 정의](remoteapp-imagereqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="9ccf0-115">따라서 읽을 것을 이동 [요구 사항](remoteapp-imagereqs.md), 이미지를 수정 및 toocreate 컬렉션을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="9ccf0-116">VNET에 네트워크 보안 그룹이 정의되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="9ccf0-117">네트워크 보안 그룹 컬렉션을 위해 사용 하는 hello 서브넷에 정의 되어 있는 경우 확인이 [Url 및 포트](remoteapp-ports.md) 서브넷 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="9ccf0-118">추가 네트워크 보안 그룹 toohello Vm을 배포할 사용자가 세부적으로 제어에 대 한 hello 서브넷에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="9ccf0-119">자체 DNS 서버를 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="9ccf0-120">VNET 서브넷에서 이러한 DNS 서버에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="9ccf0-121">VNET에 DNS 서버는 항상를 toomake 있는지 hello 및 hello VNET에서에서 호스팅되는 항상 수 tooresolve hello 가상 컴퓨터 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="9ccf0-122">이 작업에 Google DNS를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="9ccf0-123">하이브리드 컬렉션의 경우 자체 DNS 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="9ccf0-124">사용자 지정 네트워크 구성 스키마 또는 hello 관리 포털을 통해 가상 네트워크를 만들 때 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="9ccf0-125">DNS 서버는 장애 조치 방법 (것과 반대로 tooround 로빈)으로 지정 된 hello 순서에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="9ccf0-126">너무를 참조 하십시오[Vm 및 역할 인스턴스에 대 한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake DNS 서버가 구성 된 correcly 하는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="9ccf0-127">컬렉션에 대 한 hello DNS 서버는 액세스 가능 하 고이 컬렉션에 대해 지정한 hello VNET 서브넷에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="9ccf0-128">예:</span><span class="sxs-lookup"><span data-stu-id="9ccf0-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![DNS 정의](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="9ccf0-130">컬렉션에서 Active Directory 도메인 컨트롤러를 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="9ccf0-131">현재는 하나의 Active Directory 도메인만 Azure RemoteApp과 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="9ccf0-132">hello 하이브리드 컬렉션은 Azure Active Directory 계정을는 Windows Server Active Directory 배포에서 디렉터리 동기화 도구를 사용 하 여 동기화 된만 지원 합니다. 특히, 하거나 hello 암호 동기화 옵션으로 동기화 구성 된 Active Directory Federation Services (AD FS) 페더레이션과 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="9ccf0-133">디렉터리 통합 설정 및 toocreate 온-프레미스 도메인에 대 한 hello UPN 도메인 접미사와 일치 하는 사용자 지정 도메인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="9ccf0-134">자세한 내용은 [Azure RemoteApp에 대해 Active Directory 구성](remoteapp-ad.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="9ccf0-135">제공 된 hello 도메인 세부 정보가 유효 하 고 hello 도메인 컨트롤러는 Azure Remoteapp에 사용 되는 hello 서브넷에 VM 생성 hello에서 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="9ccf0-136">또한 hello 서비스 계정에 제공 된 자격 증명 권한이 tooadd 컴퓨터 toohello 도메인과 하는 제공 된 AD 이름을 hello 제공 hello hello VNET에에서 제공 된 DNS에서에서 확인할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="9ccf0-137">컬렉션을 만들 때 어떤 도메인 이름을 지정했나요?</span><span class="sxs-lookup"><span data-stu-id="9ccf0-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="9ccf0-138">hello 도메인 만들거나 추가한 내부 도메인 이름 (Azure AD 도메인 이름이 아닌) 이어야 합니다 이름과 확인 가능한 DNS 형식 (contoso.local)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="9ccf0-139">예를 들어 Active Directory 내부 이름이 (contoso.local) 있으며 Active Directory UPN (contoso.com)-toouse hello 내부 이름이 있는 사용자 컬렉션을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="9ccf0-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

