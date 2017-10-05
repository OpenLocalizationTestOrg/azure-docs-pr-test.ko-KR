---
title: "Azure(큰 인스턴스)에서 SAP HANA 설치 | Microsoft Docs"
description: "Azure(큰 인스턴스)에서 SAP HANA를 설치하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 280001f9057825b9dcd98c5180340a54e2e239cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-install-and-configure-sap-hana-large-instances-on-azure"></a><span data-ttu-id="4dfee-103">Azure(큰 인스턴스)에서 SAP HANA를 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4dfee-103">How to install and configure SAP HANA (large instances) on Azure</span></span>

<span data-ttu-id="4dfee-104">다음은 이 지침을 읽기 전에 알아야 할 중요한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-104">Following are some important definitions to know before you read this guide.</span></span> <span data-ttu-id="4dfee-105">[Azure(큰 인스턴스)에서 SAP HANA 개요 및 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)에서 HANA 큰 인스턴스 단위의 두 가지 다른 클래스를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-105">In [SAP HANA (large instances) overview and architecture on Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) we introduced two different classes of HANA Large Instance units with:</span></span>

- <span data-ttu-id="4dfee-106">SKU의 'Type I 클래스'인 S72, S72m, S144, S144m, S192 및 S192m.</span><span class="sxs-lookup"><span data-stu-id="4dfee-106">S72, S72m, S144, S144m, S192, and S192m, which we refer to as the 'Type I class' of SKUs.</span></span>
- <span data-ttu-id="4dfee-107">SKU의 'Type II 클래스'인 S384, S384m, S384xm, S576, S768, 및 S960.</span><span class="sxs-lookup"><span data-stu-id="4dfee-107">S384, S384m, S384xm, S576, S768, and S960, which we refer to as the 'Type II class' of SKUs.</span></span>

<span data-ttu-id="4dfee-108">클래스 지정자는 HANA 큰 인스턴스 설명서 전반에서 HANA 큰 인스턴스 SKU를 기반으로 하는 다양한 기능과 요구 사항을 언급하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-108">The class specifier is going to be used throughout the HANA Large Instance documentation to eventually refer to different capabilities and requirements based on HANA Large Instance SKUs.</span></span>

<span data-ttu-id="4dfee-109">자주 사용하는 다른 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-109">Other definitions we use frequently are:</span></span>
- <span data-ttu-id="4dfee-110">**큰 인스턴스 스탬프:** SAP HANA TDI 인증을 받았고 Azure 내에서 SAP HANA 인스턴스를 전용으로 실행하는 하드웨어 인프라 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-110">**Large Instance stamp:** A hardware infrastructure stack that is SAP HANA TDI certified and dedicated to run SAP HANA instances within Azure.</span></span>
- <span data-ttu-id="4dfee-111">**Azure(큰 인스턴스)에서 SAP HANA:** 다양한 Azure 지역에서 큰 인스턴스 스탬프로 배포된 SAP HANA TDI 인증 하드웨어에서 HANA 인스턴스를 실행하는 Azure 제품에 대한 공식적인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-111">**SAP HANA on Azure (Large Instances):** Official name for the offer in Azure to run HANA instances in on SAP HANA TDI certified hardware that is deployed in Large Instance stamps in different Azure regions.</span></span> <span data-ttu-id="4dfee-112">관련 용어인 **HANA 큰 인스턴스**는 Azure(큰 인스턴스)에서 SAP HANA의 줄임말이며 기술 배포 가이드에 널리 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-112">The related term **HANA Large Instance** is short for SAP HANA on Azure (Large Instances) and is widely used this technical deployment guide.</span></span>


<span data-ttu-id="4dfee-113">SAP HANA 설치는 사용자가 진행하며 Azure(큰 인스턴스) 서버에 새 SAP HANA가 전달된 후에 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-113">The installation of SAP HANA is your responsibility and you can start the activity after handoff of a new SAP HANA on Azure (Large Instances) server.</span></span> <span data-ttu-id="4dfee-114">그리고 Azure VNet과 HANA 큰 인스턴스 유닛 사이의 연결이 설정된 후에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-114">And after the connectivity between your Azure VNet(s) and the HANA Large Instance unit(s) got established.</span></span> 

> [!Note]
> <span data-ttu-id="4dfee-115">SAP 정책에 따라 SAP HANA 설치는 SAP HANA 설치를 수행하도록 인증된 사람이 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-115">Per SAP policy, the installation of SAP HANA must be performed by a person certified to perform SAP HANA installations.</span></span> <span data-ttu-id="4dfee-116">Certified SAP Technology Associate 시험, SAP HANA 설치 인증 시험에 합격한 사람 또는 SAP 인증 SI(시스템 통합자).</span><span class="sxs-lookup"><span data-stu-id="4dfee-116">A person, who has passed the Certified SAP Technology Associate exam, SAP HANA Installation certification exam, or by an SAP-certified system integrator (SI).</span></span>

<span data-ttu-id="4dfee-117">특히 HANA 2.0을 설치할 때 설치하기로 결정한 SAP HANA 릴리스에서 지원되는 OS를 확인하려면 [SAP Support Note # 2235581 - SAP HANA: 지원되는 운영 체제](https://launchpad.support.sap.com/#/notes/2235581/E)를 다시 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-117">Check again, especially when planning to install HANA 2.0, [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E) in order to make sure that the OS is supported with the SAP HANA release you decided to install.</span></span> <span data-ttu-id="4dfee-118">HANA 2.0에서 지원되는 OS는 HANA 1.0에서 지원되는 OS보다 더 제한적이라는 것을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-118">You realize that the supported OS for HANA 2.0 is more restricted than the OS supported for HANA 1.0.</span></span> 

## <a name="first-steps-after-receiving-the-hana-large-instance-units"></a><span data-ttu-id="4dfee-119">HANA 큰 인스턴스 단위를 받은 후 첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="4dfee-119">First steps after receiving the HANA Large Instance Unit(s)</span></span>

<span data-ttu-id="4dfee-120">HANA 큰 인스턴스를 받고 인스턴스에 대한 액세스 및 연결을 설정한 후 **첫 번째 단계**는 OS 공급자에게 인스턴스의 OS를 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-120">**First Step** after receiving the HANA Large Instance and having established access and connectivity to the instances, is to register the OS of the instance with your OS provider.</span></span> <span data-ttu-id="4dfee-121">이 단계에는 Azure에서 VM에 배포해야 하는 SUSE SMT 인스턴스에 SUSE Linux OS를 등록하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-121">This step would include registering your SUSE Linux OS in an instance of SUSE SMT that you need to have deployed in a VM in Azure.</span></span> <span data-ttu-id="4dfee-122">HANA 큰 인스턴스 유닛은 SMT 인스턴스(이 설명서의 뒷부분 참조)에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-122">The HANA Large Instance unit can connect to this SMT instance (see later in this documentation).</span></span> <span data-ttu-id="4dfee-123">또는 연결해야 하는 Red Hat Subscription Manager에 RedHat OS를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-123">Or your RedHat OS needs to be registered with the Red Hat Subscription Manager you need to connect to.</span></span> <span data-ttu-id="4dfee-124">이 [문서](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 설명도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-124">See also remarks in this [document](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4dfee-125">이 단계는 OS를 패치할 수도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-125">This step also is necessary to be able to patch the OS.</span></span> <span data-ttu-id="4dfee-126">고객에게 책임이 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-126">A task that is in the responsibility of the customer.</span></span> <span data-ttu-id="4dfee-127">SUSE의 경우 [여기](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html)서 SMT 설치 및 구성을 위한 설명서를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-127">For SUSE, find documentation to install and configure SMT [here](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).</span></span>

<span data-ttu-id="4dfee-128">**두 번째 단계**는 특정 OS 릴리스/버전의 새 패치 및 수정을 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-128">**Second Step** is to check for new patches and fixes of the specific OS release/version.</span></span> <span data-ttu-id="4dfee-129">HANA 큰 인스턴스의 패치 수준이 최신 상태인지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-129">Check whether the patch level of the HANA Large Instance is on the latest state.</span></span> <span data-ttu-id="4dfee-130">OS 패치/릴리스의 타이밍과 Microsoft가 배포할 수 있는 이미지의 변경 사항에 따라 최신 패치가 포함되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-130">Based on timing on OS patch/releases and changes to the image Microsoft can deploy, there might be cases where the latest patches may not be included.</span></span> <span data-ttu-id="4dfee-131">따라서 HANA 큰 인스턴스 유닛을 인수한 후 보안, 기능, 가용성 및 성능이 적절한 패치가 특정 Linux 공급 업체에 의해 릴리스되었는지 여부를 확인하고 적용해야 하는 필수 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-131">Hence it is a mandatory step after taking over a HANA Large Instance unit, to check whether patches relevant for security, functionality, availability, and performance were released meanwhile by the particular Linux vendor and need to be applied.</span></span>

<span data-ttu-id="4dfee-132">**세 번째 단계**는 특정 OS 릴리스/버전에 SAP HANA를 설치 및 구성하기 위해 관련 SAP Note를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-132">**Third Step** is to check out the relevant SAP Notes for installing and configuring SAP HANA on the specific OS release/version.</span></span> <span data-ttu-id="4dfee-133">개별 설치 시나리오에 따라 SAP Note 또는 구성에 대한 권장 사항이나 변경 사항이 달라지므로 Microsoft에서 항상 HANA 큰 인스턴스 단위를 완벽하게 구성할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-133">Due to changing recommendations or changes to SAP Notes or configurations that are dependent on individual installation scenarios, Microsoft will not always be able to have a HANA Large Instance unit configured perfectly.</span></span> <span data-ttu-id="4dfee-134">따라서 정확한 Linux 릴리스에서 SAP HANA와 관련된 SAP Notes를 반드시 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-134">Hence it is mandatory for you as a customer, to read the SAP Notes related to SAP HANA on your exact Linux release.</span></span> <span data-ttu-id="4dfee-135">또한 필요한 OS 릴리스/버전의 구성을 확인하고 이미 설정되지 않은 경우 구성 설정을 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-135">Also check the configurations of the OS release/version necessary and apply the configuration settings where not done already.</span></span>

<span data-ttu-id="4dfee-136">구체적으로 다음 매개 변수를 확인하고 다음과 같이 조정하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-136">In specific, check the following parameters and eventually adjusted to:</span></span>

- <span data-ttu-id="4dfee-137">net.core.rmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-137">net.core.rmem_max = 16777216</span></span>
- <span data-ttu-id="4dfee-138">net.core.wmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-138">net.core.wmem_max = 16777216</span></span>
- <span data-ttu-id="4dfee-139">net.core.rmem_default = 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-139">net.core.rmem_default = 16777216</span></span>
- <span data-ttu-id="4dfee-140">net.core.wmem_default = 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-140">net.core.wmem_default = 16777216</span></span>
- <span data-ttu-id="4dfee-141">net.core.optmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-141">net.core.optmem_max = 16777216</span></span>
- <span data-ttu-id="4dfee-142">net.ipv4.tcp_rmem = 65536 16777216 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-142">net.ipv4.tcp_rmem = 65536 16777216 16777216</span></span>
- <span data-ttu-id="4dfee-143">net.ipv4.tcp_wmem = 65536 16777216 16777216</span><span class="sxs-lookup"><span data-stu-id="4dfee-143">net.ipv4.tcp_wmem = 65536 16777216 16777216</span></span>

<span data-ttu-id="4dfee-144">SLES12 SP1 및 RHEL 7.2부터 이러한 매개 변수를 /etc/sysctl.d 디렉터리의 구성 파일에 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-144">Starting with SLES12 SP1 and RHEL 7.2, these parameters must be set in a configuration file in the /etc/sysctl.d directory.</span></span> <span data-ttu-id="4dfee-145">예를 들어 이름이 91-NetApp-HANA.conf인 구성 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-145">For example, a configuration file with the name 91-NetApp-HANA.conf must be created.</span></span> <span data-ttu-id="4dfee-146">이전 SLES 및 RHEL 릴리스의 경우 /etc/sysctl.conf에서 이러한 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-146">For older SLES and RHEL releases, these parameters must be set in/etc/sysctl.conf.</span></span>

<span data-ttu-id="4dfee-147">모든 RHEL 릴리스와 SLES12부터는</span><span class="sxs-lookup"><span data-stu-id="4dfee-147">For all RHEL releases and starting with SLES12, the</span></span> 
- <span data-ttu-id="4dfee-148">sunrpc.tcp_slot_table_entries = 128</span><span class="sxs-lookup"><span data-stu-id="4dfee-148">sunrpc.tcp_slot_table_entries = 128</span></span>

<span data-ttu-id="4dfee-149">매개 변수를 /etc/modprobe.d/sunrpc-local.conf에서 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-149">parameter must be set in/etc/modprobe.d/sunrpc-local.conf.</span></span> <span data-ttu-id="4dfee-150">파일이 없으면 다음 항목을 추가하여 먼저 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-150">If the file does not exist, it must first be created by adding the following entry:</span></span> 
- <span data-ttu-id="4dfee-151">options sunrpc tcp_max_slot_table_entries=128</span><span class="sxs-lookup"><span data-stu-id="4dfee-151">options sunrpc tcp_max_slot_table_entries=128</span></span>

<span data-ttu-id="4dfee-152">**네 번째 단계**는 HANA 큰 인스턴스 단위의 시스템 시간을 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-152">**Fourth Step** is to check the system time of your HANA Large Instance Unit.</span></span> <span data-ttu-id="4dfee-153">인스턴스는 HANA 큰 인스턴스 스탬프가 있는 Azure 지역의 위치를 나타내는 시스템 표준 시간대로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-153">The instances are deployed with a system time zone that represent the location of the Azure region the HANA Large Instance Stamp is located in.</span></span> <span data-ttu-id="4dfee-154">소유한 인스턴스의 시스템 시간이나 표준 시간대를 자유롭게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-154">You are free to change the system time or time zone of the instances you own.</span></span> <span data-ttu-id="4dfee-155">이렇게 하고 더 많은 인스턴스를 테넌트에 주문하면 새로 전달된 인스턴스의 표준 시간대를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-155">Doing so and ordering more instances into your tenant, be prepared that you need to adapt the time zone of the newly delivered instances.</span></span> <span data-ttu-id="4dfee-156">Microsoft 작업에서는 인계 후 인스턴스에서 사용자가 설정한 시스템 표준 시간대에 대해 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-156">Microsoft operations have no insights into the system time zone you set up with the instances after the handover.</span></span> <span data-ttu-id="4dfee-157">따라서 새로 배포된 인스턴스는 변경한 동일한 표준 시간대로 설정되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-157">Hence newly deployed instances might not be set in the same time zone as the one you changed to.</span></span> <span data-ttu-id="4dfee-158">따라서 인계된 인스턴스의 표준 시간대를 확인하고 필요할 경우 적용하는 것은 고객의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-158">As a result, it is your responsibility as customer to check and if necessary adapt the time zone of the instance(s) handed over.</span></span> 

<span data-ttu-id="4dfee-159">**다섯 번째 단계**는 etc/hosts를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-159">**Fifth Step** is to check etc/hosts.</span></span> <span data-ttu-id="4dfee-160">블레이드를 인계하면 다양한 용도로 서로 다른 IP 주소가 할당됩니다(다음 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-160">As the blades get handed over, they have different IP addresses assigned for different purposes (see next section).</span></span> <span data-ttu-id="4dfee-161">etc/hosts 파일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-161">Check the etc/hosts file.</span></span> <span data-ttu-id="4dfee-162">기존 테넌트에 단위가 추가된 경우 새로 배포된 시스템의 etc/hosts가 이전에 제공된 시스템의 IP 주소로 올바르게 유지되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-162">In cases where units are added into an existing tenant, don't expect to have etc/hosts of the newly deployed systems maintained correctly with the IP addresses of earlier delivered systems.</span></span> <span data-ttu-id="4dfee-163">따라서 새로 배포된 인스턴스에서 상호 작용하고 테넌트에 이전에 배포된 단위의 이름을 확인할 수 있도록 올바른 설정을 확인하는 것은 고객의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-163">Hence it is on you as customer to check the correct settings so, that a newly deployed instance can interact and resolve the names of earlier deployed units in your tenant.</span></span> 

## <a name="networking"></a><span data-ttu-id="4dfee-164">네트워킹</span><span class="sxs-lookup"><span data-stu-id="4dfee-164">Networking</span></span>
<span data-ttu-id="4dfee-165">Azure VNet을 디자인할 때 권장 사항을 따르고 다음 문서에 설명된 대로 해당 VNet을 HANA 큰 인스턴스에 연결한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-165">We assume that you followed the recommendations in designing your Azure VNets and connecting those VNets to the HANA Large Instances as described in these documents:</span></span>

- [<span data-ttu-id="4dfee-166">Azure에서 SAP HANA(큰 인스턴스) 개요 및 아키텍처</span><span class="sxs-lookup"><span data-stu-id="4dfee-166">SAP HANA (large Instance) Overview and Architecture on Azure</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [<span data-ttu-id="4dfee-167">Azure의 SAP HANA(큰 인스턴스) 인프라 및 연결</span><span class="sxs-lookup"><span data-stu-id="4dfee-167">SAP HANA (large instances) Infrastructure and connectivity on Azure</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="4dfee-168">단일 단위의 네트워킹에 대해 알아야 할 몇 가지 세부 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-168">There are some details worth to mention about the networking of the single units.</span></span> <span data-ttu-id="4dfee-169">모든 HANA 큰 인스턴스 단위에는 2개 또는 3개의 단위 NIC 포트에 할당된 2개 또는 3개의 IP 주소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-169">Every HANA Large Instance unit comes with two or three IP addresses that are assigned to two or three NIC ports of the unit.</span></span> <span data-ttu-id="4dfee-170">HANA 확장 구성 및 HANA 시스템 복제 시나리오에는 3개의 IP 주소가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-170">Three IP addresses are used in HANA scale-out configurations and the HANA System Replication scenario.</span></span> <span data-ttu-id="4dfee-171">단위의 NIC에 할당된 IP 주소 중 하나가 [Azure에서 SAP HANA(큰 인스턴스) 개요 및 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)에 설명된 서버 IP 풀을 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-171">One of the IP addresses assigned to the NIC of the unit is out of the Server IP pool that was described in the [SAP HANA (large Instance) Overview and Architecture on Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).</span></span>

<span data-ttu-id="4dfee-172">할당된 두 IP 주소가 있는 단위에 대한 배포는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-172">The distribution for units with two IP addresses assigned should look like:</span></span>

- <span data-ttu-id="4dfee-173">eth0.xx에는 Microsoft에 제출한 서버 IP 풀 주소 범위를 벗어나는 IP 주소가 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-173">eth0.xx should have an IP address assigned that is out of the Server IP Pool address range that you submitted to Microsoft.</span></span> <span data-ttu-id="4dfee-174">이 IP 주소는 OS의 /etc/hosts에서 유지 관리에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-174">This IP address shall be used for maintaining in /etc/hosts of the OS.</span></span>
- <span data-ttu-id="4dfee-175">eth1.xx에는 NFS와의 통신에 사용되는 IP 주소가 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-175">eth1.xx should have an IP address assigned that is used for communication to NFS.</span></span> <span data-ttu-id="4dfee-176">따라서 이러한 주소는 테넌트 내에서 인스턴스 트래픽에 대한 인스턴스를 허용하기 위해 etc/hosts에서 유지 관리할 필요가 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="4dfee-176">Therefore, these addresses do **NOT** need to be maintained in etc/hosts in order to allow instance to instance traffic within the tenant.</span></span>

<span data-ttu-id="4dfee-177">HANA 시스템 복제 또는 HANA 확장 배포의 경우 두 개의 IP 주소가 할당된 블레이드 구성은 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-177">For deployment cases of HANA System Replication or HANA scale-out, a blade configuration with two IP addresses assigned is not suitable.</span></span> <span data-ttu-id="4dfee-178">IP 주소가 두 개만 할당되어 있는 경우 이러한 구성을 배포하려면 할당된 세 번째 VLAN의 세 번째 IP 주소를 Azure의 SAP HANA Service Management에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-178">If having two IP addresses assigned only and wanting to deploy such a configuration, contact SAP HANA on Azure Service Management to get a third IP address in a third VLAN assigned.</span></span> <span data-ttu-id="4dfee-179">세 개의 NIC 포트에 새 개의 IP 주소가 할당되어 있는 HANA 큰 인스턴스 유닛에는 다음 사용 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-179">For HANA Large Instance units having three IP addresses assigned on three NIC ports, the following usage rules apply:</span></span>

- <span data-ttu-id="4dfee-180">eth0.xx에는 Microsoft에 제출한 서버 IP 풀 주소 범위를 벗어나는 IP 주소가 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-180">eth0.xx should have an IP address assigned that is out of the Server IP Pool address range that you submitted to Microsoft.</span></span> <span data-ttu-id="4dfee-181">따라서 이 IP 주소는 OS의 /etc/hosts에서 유지 관리에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-181">Hence this IP address shall not be used for maintaining in /etc/hosts of the OS.</span></span>
- <span data-ttu-id="4dfee-182">eth1.xx에는 NFS 저장소와의 통신에 사용되는 IP 주소가 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-182">eth1.xx should have an IP address assigned that is used for communication to NFS storage.</span></span> <span data-ttu-id="4dfee-183">따라서 이 주소 유형은 etc/hosts에서 유지 관리되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-183">Hence this type of addresses should not be maintained in etc/hosts.</span></span>
- <span data-ttu-id="4dfee-184">eth2.xx는 다른 인스턴스 간의 통신을 위해 etc/hosts에서 유지 관리되도록 독점적으로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-184">eth2.xx should be exclusively used to be maintained in etc/hosts for communication between the different instances.</span></span> <span data-ttu-id="4dfee-185">이 주소는 HANA가 노드 간 구성에 사용하는 IP 주소로 규모 확장 HANA 구성에서 유지해야 하는 IP 주소이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-185">These addresses would also be the IP addresses that need to be maintained in scale-out HANA configurations as IP addresses HANA uses for the inter-node configuration.</span></span>



## <a name="storage"></a><span data-ttu-id="4dfee-186">저장소</span><span class="sxs-lookup"><span data-stu-id="4dfee-186">Storage</span></span>

<span data-ttu-id="4dfee-187">Azure(큰 인스턴스)에서 SAP HANA에 대한 저장소 레이아웃은 [SAP HANA 저장소 요구 사항](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) 백서에 문서화된 SAP 권장 지침을 통해 Azure Service Management의 SAP HANA에 의해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-187">The storage layout for SAP HANA on Azure (Large Instances) is configured by SAP HANA on Azure Service Management through SAP recommended guide lines as documented in [SAP HANA Storage Requirements](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper.</span></span> <span data-ttu-id="4dfee-188">다른 HANA 큰 인스턴스 SKU가 있는 서로 다른 볼륨의 대략적인 크기는 [Azure에서 SAP HANA(큰 인스턴스) 개요 및 아키텍처](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-188">The rough sizes of the different volumes with the different HANA Large Instances SKUs got documented in [SAP HANA (large Instance) Overview and Architecture on Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4dfee-189">저장소 볼륨에 대한 명명 규칙은 아래 테이블에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-189">The naming conventions of the storage volumes are listed in the following table:</span></span>

| <span data-ttu-id="4dfee-190">저장소 사용</span><span class="sxs-lookup"><span data-stu-id="4dfee-190">Storage usage</span></span> | <span data-ttu-id="4dfee-191">탑재 이름</span><span class="sxs-lookup"><span data-stu-id="4dfee-191">Mount Name</span></span> | <span data-ttu-id="4dfee-192">볼륨 이름</span><span class="sxs-lookup"><span data-stu-id="4dfee-192">Volume Name</span></span> | 
| --- | --- | ---|
| <span data-ttu-id="4dfee-193">HANA data</span><span class="sxs-lookup"><span data-stu-id="4dfee-193">HANA data</span></span> | <span data-ttu-id="4dfee-194">/hana/data/SID/mnt0000<m></span><span class="sxs-lookup"><span data-stu-id="4dfee-194">/hana/data/SID/mnt0000<m></span></span> | <span data-ttu-id="4dfee-195">저장소 IP:/hana_data_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="4dfee-195">Storage IP:/hana_data_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="4dfee-196">HANA log</span><span class="sxs-lookup"><span data-stu-id="4dfee-196">HANA log</span></span> | <span data-ttu-id="4dfee-197">/hana/log/SID/mnt0000<m></span><span class="sxs-lookup"><span data-stu-id="4dfee-197">/hana/log/SID/mnt0000<m></span></span> | <span data-ttu-id="4dfee-198">저장소 IP:/hana_log_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="4dfee-198">Storage IP:/hana_log_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="4dfee-199">HANA log backup</span><span class="sxs-lookup"><span data-stu-id="4dfee-199">HANA log backup</span></span> | <span data-ttu-id="4dfee-200">/hana/log/backups</span><span class="sxs-lookup"><span data-stu-id="4dfee-200">/hana/log/backups</span></span> | <span data-ttu-id="4dfee-201">저장소 IP:/hana_log_backups_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="4dfee-201">Storage IP:/hana_log_backups_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="4dfee-202">HANA shared</span><span class="sxs-lookup"><span data-stu-id="4dfee-202">HANA shared</span></span> | <span data-ttu-id="4dfee-203">/hana/shared/SID</span><span class="sxs-lookup"><span data-stu-id="4dfee-203">/hana/shared/SID</span></span> | <span data-ttu-id="4dfee-204">저장소 IP:/hana_shared_SID_mnt00001_tenant_vol/shared</span><span class="sxs-lookup"><span data-stu-id="4dfee-204">Storage IP:/hana_shared_SID_mnt00001_tenant_vol/shared</span></span> |
| <span data-ttu-id="4dfee-205">usr/sap</span><span class="sxs-lookup"><span data-stu-id="4dfee-205">usr/sap</span></span> | <span data-ttu-id="4dfee-206">/usr/sap/SID</span><span class="sxs-lookup"><span data-stu-id="4dfee-206">/usr/sap/SID</span></span> | <span data-ttu-id="4dfee-207">저장소 IP:/hana_shared_SID_mnt00001_tenant_vol/usr_sap</span><span class="sxs-lookup"><span data-stu-id="4dfee-207">Storage IP:/hana_shared_SID_mnt00001_tenant_vol/usr_sap</span></span> |

<span data-ttu-id="4dfee-208">SID = HANA 인스턴스 시스템 ID</span><span class="sxs-lookup"><span data-stu-id="4dfee-208">Where SID = the HANA instance System ID</span></span> 

<span data-ttu-id="4dfee-209">tenant = 테넌트 배치 시 연산에 대한 내부 열거</span><span class="sxs-lookup"><span data-stu-id="4dfee-209">And tenant = an internal enumeration of operations when deploying a tenant.</span></span>

<span data-ttu-id="4dfee-210">위에서 볼 수 있듯이 HANA shared와 usr/sap는 같은 볼륨을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-210">As you can see, HANA shared and usr/sap are sharing the same volume.</span></span> <span data-ttu-id="4dfee-211">탑재 지점의 명명법에는 HANA 인스턴스의 시스템 ID는 물론 탑재 번호가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-211">The nomenclature of the mountpoints does include the System ID of the HANA instances as well as the mount number.</span></span> <span data-ttu-id="4dfee-212">강화(scale-up) 배포의 경우 탑재가 하나(예: mnt00001)만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-212">In scale-up deployments there only is one mount, like mnt00001.</span></span> <span data-ttu-id="4dfee-213">반면에 확장(scale-out) 배포의 경우 worker 및 master 노드를 포함하여 많은 탑재를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-213">Whereas in scale-out deployment you would see as many mounts, as, you have worker and master nodes.</span></span> <span data-ttu-id="4dfee-214">확장 환경의 경우, 데이터, 로그, 로그 백업 볼륨이 공유되고 확장 구성의 각 노드에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-214">For the scale-out environment, data, log, log backup volumes are shared and attached to each node in the scale-out configuration.</span></span> <span data-ttu-id="4dfee-215">여러 SAP 인스턴스를 실행하는 구성의 경우 다른 볼륨 세트가 만들어져 HAN 큰 인스턴스 유닛에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-215">For configurations running multiple SAP instances, a different set of volumes is created and attached to the HAN Large Instance unit.</span></span>

<span data-ttu-id="4dfee-216">이 문서를 읽고 HANA 큰 인스턴스 유닛을 살펴보면 유닛의 HANA/data에 상당히 많은 디스크 볼륨이 있고 HANA/log/backup 볼륨이 있다는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-216">As you read the paper and look a HANA Large Instance unit, you realize that the units come with rather generous disk volume for HANA/data and that we have a volume HANA/log/backup.</span></span> <span data-ttu-id="4dfee-217">HANA/data 크기가 너무 큰 이유는 고객에게 제공되는 저장소 스냅숏이 동일한 디스크 볼륨을 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-217">The reason why we sized the HANA/data so large is that the storage snapshots we offer for you as a customer are using the same disk volume.</span></span> <span data-ttu-id="4dfee-218">저장소 스냅숏을 더 많이 수행할수록 할당된 저장소 볼륨에서 더 많은 공간이 스냅숏에 소비된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-218">It means the more storage snapshots you perform, the more space is consumed by snapshots in your assigned storage volumes.</span></span> <span data-ttu-id="4dfee-219">HANA/log/backup 볼륨은 데이터베이스 백업을 넣는 볼륨으로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-219">The HANA/log/backup volume is not thought to be the volume to put database backups in.</span></span> <span data-ttu-id="4dfee-220">HANA 트랜잭션 로그 백업을 위한 백업 볼륨에 사용되도록 크기가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-220">It is sized to be used as backup volume for the HANA transaction log backups.</span></span> <span data-ttu-id="4dfee-221">향후 버전의 저장소 스냅숏 셀프 서비스는 이 특정 볼륨에 보다 빈번하게 스냅숏을 저장하도록 만드는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-221">In future versions of the storage snapshot self service, we will target this specific volume to have more frequent snapshots.</span></span> <span data-ttu-id="4dfee-222">HANA Large Instance 인프라에서 제공하는 재해 복구 기능에 옵트인하려는 경우 재해 복구 사이트를 보다 빈번하게 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-222">And with that more frequent replications to the disaster recovery site if you desire to option-in for the disaster recovery functionality provided by the HANA Large Instance infrastructure.</span></span> <span data-ttu-id="4dfee-223">자세한 내용은 [Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-223">See details in [SAP HANA (large instances) High Availability and Disaster Recovery on Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> 

<span data-ttu-id="4dfee-224">제공된 저장소 외에도 1TB 단위로 추가 저장소 용량을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-224">In addition to the storage provided, you can purchase additional storage capacity in 1 TB increments.</span></span> <span data-ttu-id="4dfee-225">이 추가 저장소는 HANA 큰 인스턴스에 새 볼륨으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-225">This additional storage can be added as new volumes to a HANA Large Instances.</span></span>

<span data-ttu-id="4dfee-226">Azure의 SAP HANA Service Management로 온보딩하는 동안 고객은 sidadm 사용자 및 sapsys 그룹(예: 1000,500)에 대한 사용자 ID(UID) 및 그룹 ID(GID)를 지정합니다. SAP HANA 시스템을 설치하는 동안 동일한 값이 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-226">During onboarding with SAP HANA on Azure Service Management, the customer specifies a User ID (UID) and Group ID (GID) for the sidadm user and sapsys group (ex: 1000,500) It is necessary that during installation of the SAP HANA system, these same values are used.</span></span> <span data-ttu-id="4dfee-227">유닛에 다수의 HANA 인스턴스를 배포하려는 경우 다수의 볼륨 세트(각 인스턴스당 하나씩)를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-227">As you want to deploy multiple HANA instances on a unit, you get multiple sets of volumes (one set for each instance).</span></span> <span data-ttu-id="4dfee-228">결과적으로 배포 시 다음을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-228">As a result, at deployment time you need to define:</span></span>

- <span data-ttu-id="4dfee-229">다수의 HANA 인스턴스에 대한 SID(sidadm은 여기서 파생되었음).</span><span class="sxs-lookup"><span data-stu-id="4dfee-229">The SID of the different HANA instances (sidadm is derived out of it).</span></span>
- <span data-ttu-id="4dfee-230">다수의 HANA 인스턴스에 대한 메모리 크기.</span><span class="sxs-lookup"><span data-stu-id="4dfee-230">Memory sizes of the different HANA instances.</span></span> <span data-ttu-id="4dfee-231">인스턴스당 메모리 크기는 각각의 개별적인 볼륨 세트에서 볼륨의 크기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-231">Since the memory size per instances defines the size of the volumes in each individual volume set.</span></span>

<span data-ttu-id="4dfee-232">저장소 공급자 권장 사항에 따라 탑재된 모든 볼륨(부팅 LUN 제외)에 대해 다음 탑재 옵션이 구성됩니다 .</span><span class="sxs-lookup"><span data-stu-id="4dfee-232">Based on storage provider recommendations the following mount options are configured for all mounted volumes (excludes boot LUN):</span></span>

- <span data-ttu-id="4dfee-233">nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0</span><span class="sxs-lookup"><span data-stu-id="4dfee-233">nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0</span></span>

<span data-ttu-id="4dfee-234">탑재 지점은 다음 그래픽과 같이 /etc/fstab에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-234">These mount points are configured in /etc/fstab like shown in the following graphics:</span></span>

![HANA 큰 인스턴스 유닛의 탑재된 볼륨의 fstab](./media/hana-installation/image1_fstab.PNG)

<span data-ttu-id="4dfee-236">S72m HANA 큰 인스턴스 유닛에 대한 df -h 명령의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-236">The output of the command df -h on a S72m HANA Large Instance unit would look like:</span></span>

![HANA 큰 인스턴스 유닛의 탑재된 볼륨의 fstab](./media/hana-installation/image2_df_output.PNG)


<span data-ttu-id="4dfee-238">큰 인스턴스 스탬프의 저장소 컨트롤러와 노드는 NTP 서버와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-238">The storage controller and nodes in the Large Instance stamps are synchronized to NTP servers.</span></span> <span data-ttu-id="4dfee-239">Azure(큰 인스턴스) 장치의 SAP HANA와 Azure VM을 NTP 서버에 대해 동기화할 경우 Azure 또는 큰 인스턴스 스탬프에서 인프라 및 계산 장치 간에 중대한 시간 변동이 발생하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-239">With you synchronizing the SAP HANA on Azure (Large Instances) units and Azure VMs against an NTP server, there should be no significant time drift happening between the infrastructure and the compute units in Azure or Large Instance stamps.</span></span>

<span data-ttu-id="4dfee-240">아래 사용된 저장소에 대해 SAP HANA를 최적화하려면 다음 SAP HANA 구성 매개 변수도 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-240">In order to optimize SAP HANA to the storage used underneath, you should also set the following SAP HANA configuration parameters:</span></span>

- <span data-ttu-id="4dfee-241">max_parallel_io_requests 128</span><span class="sxs-lookup"><span data-stu-id="4dfee-241">max_parallel_io_requests 128</span></span>
- <span data-ttu-id="4dfee-242">async_read_submit on</span><span class="sxs-lookup"><span data-stu-id="4dfee-242">async_read_submit on</span></span>
- <span data-ttu-id="4dfee-243">async_write_submit_active on</span><span class="sxs-lookup"><span data-stu-id="4dfee-243">async_write_submit_active on</span></span>
- <span data-ttu-id="4dfee-244">async_write_submit_blocks all</span><span class="sxs-lookup"><span data-stu-id="4dfee-244">async_write_submit_blocks all</span></span>
 
<span data-ttu-id="4dfee-245">SAP HANA 1.0 버전 SPS12까지는 [SAP Note #2267798 - SAP HANA 데이터베이스의 구성](https://launchpad.support.sap.com/#/notes/2267798)에 설명된 대로 SAP HANA 데이터베이스 설치 중에 이러한 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-245">For SAP HANA 1.0 versions up to SPS12, these parameters can be set during the installation of the SAP HANA database, as described in [SAP Note #2267798 - Configuration of the SAP HANA Database](https://launchpad.support.sap.com/#/notes/2267798)</span></span>

<span data-ttu-id="4dfee-246">hdbparam 프레임워크를 사용하여 SAP HANA 데이터베이스 설치 후 매개 변수를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-246">You also can configure the parameters after the SAP HANA database installation by using the hdbparam framework.</span></span> 

<span data-ttu-id="4dfee-247">SAP HANA 2.0에서는 hdbparam 프레임워크가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-247">With SAP HANA 2.0, the hdbparam framework has been deprecated.</span></span> <span data-ttu-id="4dfee-248">따라서 SQL 명령을 사용하여 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-248">As a result the parameters must be set using SQL commands.</span></span> <span data-ttu-id="4dfee-249">자세한 내용은 [SAP Note #2399079: HANA 2에서 hdbparam 제거](https://launchpad.support.sap.com/#/notes/2399079)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-249">For details, see [SAP Note #2399079: Elimination of hdbparam in HANA 2](https://launchpad.support.sap.com/#/notes/2399079).</span></span>


## <a name="operating-system"></a><span data-ttu-id="4dfee-250">운영 체제</span><span class="sxs-lookup"><span data-stu-id="4dfee-250">Operating system</span></span>

<span data-ttu-id="4dfee-251">제공되는 OS 이미지의 스왑 공간은 [SAP Support Note #1999997 - FAQ: SAP HANA 메모리](https://launchpad.support.sap.com/#/notes/1999997/E)(영문)에 따라 2GB로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-251">Swap space of the delivered OS image is set to 2 GB according to the [SAP Support Note #1999997 - FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/1999997/E).</span></span> <span data-ttu-id="4dfee-252">원하는 다른 모든 설정은 고객이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-252">Any different setting desired needs to be set by you as a customer.</span></span>

<span data-ttu-id="4dfee-253">[SUSE Linux Enterprise Server 12 SP1 for SAP Applications](https://www.suse.com/products/sles-for-sap/hana)는 Azure(큰 인스턴스)에서 SAP HANA에 대해 설치되는 Linux 배포판입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-253">[SUSE Linux Enterprise Server 12 SP1 for SAP Applications](https://www.suse.com/products/sles-for-sap/hana) is the distribution of Linux installed for SAP HANA on Azure (Large Instances).</span></span> <span data-ttu-id="4dfee-254">이 특정 배포판은 SAP 관련 기능을 &quot;바로 사용할 수 있게&quot; 제공합니다(SLES에서 SAP을 효과적으로 실행하기 위해 미리 설정된 매개 변수 포함).</span><span class="sxs-lookup"><span data-stu-id="4dfee-254">This particular distribution provides SAP-specific capabilities &quot;out of the box&quot; (including pre-set parameters for running SAP on SLES effectively).</span></span>

<span data-ttu-id="4dfee-255">SLES의 SAP HANA 배포와 관련된 몇 가지 유용한 리소스(고가용성 설정, SAP 작업과 관련된 보안 강화 등)에 대해서는 SUSE 웹 사이트의 [리소스 라이브러리/백서](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) 및 SCN(SAP Community Network)의 [SUSE의 SAP](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-255">See [Resource Library/White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) on the SUSE website and [SAP on SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) on the SAP Community Network (SCN) for several useful resources related to deploying SAP HANA on SLES (including the set-up of High Availability, security hardening specific to SAP operations, and more).</span></span>

<span data-ttu-id="4dfee-256">SUSE 관련 링크에 있는 유용한 추가 SAP 정보:</span><span class="sxs-lookup"><span data-stu-id="4dfee-256">Additional and useful SAP on SUSE-related links:</span></span>

- [<span data-ttu-id="4dfee-257">SUSE Linux의 SAP HANA 사이트</span><span class="sxs-lookup"><span data-stu-id="4dfee-257">SAP HANA on SUSE Linux Site</span></span>](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- <span data-ttu-id="4dfee-258">[SAP 모범 사례: 복제 큐에 넣기 – SUSE Linux Enterprise 12의 SAP NetWeaver](https://www.suse.com/docrepcontent/container.jsp?containerId=9113)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-258">[Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).</span></span>
- <span data-ttu-id="4dfee-259">[ClamSAP - SAP용 SLES 바이러스 방지](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap)(SLES 12 for SAP Applications 포함)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-259">[ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (including SLES 12 for SAP Applications).</span></span>

<span data-ttu-id="4dfee-260">SLES 12에서 SAP HANA 구현에 적용할 수 있는 SAP Support Note:</span><span class="sxs-lookup"><span data-stu-id="4dfee-260">SAP Support Notes applicable to implementing SAP HANA on SLES 12:</span></span>

- <span data-ttu-id="4dfee-261">[SAP Support Note #1944799 – SLES 운영 체제 설치를 위한 SAP HANA 지침](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-261">[SAP Support Note #1944799 – SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).</span></span>
- <span data-ttu-id="4dfee-262">[SAP Support Note #2205917 – SAP HANA DB: SLES 12 for SAP Applications를 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2205917/E)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-262">[SAP Support Note #2205917 – SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E).</span></span>
- <span data-ttu-id="4dfee-263">[SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: 설치 참고](https://launchpad.support.sap.com/#/notes/1984787)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-263">[SAP Support Note #1984787 – SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787).</span></span>
- <span data-ttu-id="4dfee-264">[SAP Support Note #171356 – SAP Software on Linux: 일반 정보](https://launchpad.support.sap.com/#/notes/1984787)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-264">[SAP Support Note #171356 – SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787).</span></span>
- <span data-ttu-id="4dfee-265">[SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-265">[SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070).</span></span>

<span data-ttu-id="4dfee-266">[SAP HANA용 Red Hat Enterprise Linux](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana)(영문)는 HANA 큰 인스턴스에서 SAP HANA를 실행하기 위한 또 다른 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-266">[Red Hat Enterprise Linux for SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) is another offer for running SAP HANA on HANA Large Instances.</span></span> <span data-ttu-id="4dfee-267">RHEL 6.7 및 7.2 릴리스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-267">Releases of RHEL 6.7 and 7.2 are available.</span></span> 

<span data-ttu-id="4dfee-268">Red Hat 관련 링크에 있는 유용한 추가 SAP 정보:</span><span class="sxs-lookup"><span data-stu-id="4dfee-268">Additional and useful SAP on Red Hat related links:</span></span>
- <span data-ttu-id="4dfee-269">[Red Hat Linux 사이트의 SAP HANA](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat)</span><span class="sxs-lookup"><span data-stu-id="4dfee-269">[SAP HANA on Red Hat Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).</span></span>

<span data-ttu-id="4dfee-270">Red Hat에서 SAP HANA 구현에 적용할 수 있는 SAP Support Note:</span><span class="sxs-lookup"><span data-stu-id="4dfee-270">SAP Support Notes applicable to implementing SAP HANA on Red Hat:</span></span>

- <span data-ttu-id="4dfee-271">[SAP Support Note #2009879 – RHEL(Red Hat Enterprise Linux) 운영 체제를 위한 SAP HANA 지침](https://launchpad.support.sap.com/#/notes/2009879/E)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-271">[SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879/E).</span></span>
- <span data-ttu-id="4dfee-272">[SAP Support Note #2292690 - SAP HANA DB: RHEL 7을 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2292690)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-272">[SAP Support Note #2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).</span></span>
- <span data-ttu-id="4dfee-273">[SAP Support Note #2247020 - SAP HANA DB: RHEL 6.7을 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2247020)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-273">[SAP Support Note #2247020 - SAP HANA DB: Recommended OS settings for RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).</span></span>
- <span data-ttu-id="4dfee-274">[SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-274">[SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070).</span></span>
- <span data-ttu-id="4dfee-275">[SAP Support Note #2228351 - Linux: RHEL 6 또는 SLES 11의 SAP HANA Database SPS 11 수정 번호 110 이상](https://launchpad.support.sap.com/#/notes/2228351)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-275">[SAP Support Note #2228351 - Linux: SAP HANA Database SPS 11 revision 110 (or higher) on RHEL 6 or SLES 11](https://launchpad.support.sap.com/#/notes/2228351).</span></span>
- <span data-ttu-id="4dfee-276">[SAP Support Note #2397039 - FAQ: RHEL의 SAP](https://launchpad.support.sap.com/#/notes/2397039)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-276">[SAP Support Note #2397039 - FAQ: SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039).</span></span>
- <span data-ttu-id="4dfee-277">[SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/1496410)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-277">[SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410).</span></span>
- <span data-ttu-id="4dfee-278">[SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/2002167)(영문)</span><span class="sxs-lookup"><span data-stu-id="4dfee-278">[SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167).</span></span>

## <a name="time-synchronization"></a><span data-ttu-id="4dfee-279">시간 동기화</span><span class="sxs-lookup"><span data-stu-id="4dfee-279">Time synchronization</span></span>

<span data-ttu-id="4dfee-280">SAP NetWeaver 아키텍처를 기반으로 구축된 SAP 응용 프로그램은 SAP 시스템을 구성하는 다양한 구성 요소의 시간 차이에 민감합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-280">SAP applications built on the SAP NetWeaver architecture are sensitive on time differences for the various components that comprise the SAP system.</span></span> <span data-ttu-id="4dfee-281">오류 제목이 ZDATE\_LARGE\_TIME\_DIFF인 SAP ABAP 짧은 덤프에 익숙할 수 있습니다. 서로 다른 서버 또는 VM의 시스템 시간이 너무 멀리 떨어지면 이러한 짧은 덤프가 표시되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-281">SAP ABAP short dumps with the error title of ZDATE\_LARGE\_TIME\_DIFF are likely familiar, as these short dumps appear when the system time of different servers or VMs is drifting too far apart.</span></span>

<span data-ttu-id="4dfee-282">Azure(큰 인스턴스)에 있는 SAP HANA의 경우 Azure에서 수행되는 시간 동기화가 큰 인스턴스 스탬프의 계산 장치에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-282">For SAP HANA on Azure (Large Instances), time synchronization done in Azure doesn&#39;t apply to the compute units in the Large Instance stamps.</span></span> <span data-ttu-id="4dfee-283">이 동기화는 원시 Azure VM에서 SAP 응용 프로그램을 실행하는 데는 적용할 수 없습니다. Azure가 시스템 시간이 적절하게 동기화되도록 보장하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-283">This synchronization is not applicable for running SAP applications in native Azure VMs, as Azure ensures a system&#39;s time is properly synchronized.</span></span> <span data-ttu-id="4dfee-284">결과적으로 Azure VM에서 실행되는 SAP 응용 프로그램 서버와 HANA 큰 인스턴스에서 실행되는 SAP HANA 데이터베이스 인스턴스에서 사용할 수 있는 별도의 시간 서버를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-284">As a result, a separate time server must be set up that can be used by SAP application servers running on Azure VMs and the SAP HANA database instances running on HANA Large Instances.</span></span> <span data-ttu-id="4dfee-285">큰 인스턴스 스탬프의 저장소 인프라는 NTP 서버와 시간 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-285">The storage infrastructure in Large Instance stamps is time synchronized with NTP servers.</span></span>

## <a name="setting-up-smt-server-for-suse-linux"></a><span data-ttu-id="4dfee-286">SUSE Linux용 SMT 서버 설정</span><span class="sxs-lookup"><span data-stu-id="4dfee-286">Setting up SMT server for SUSE Linux</span></span>
<span data-ttu-id="4dfee-287">SAP HANA 큰 인스턴스는 인터넷에 직접 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-287">SAP HANA Large Instances don't have direct connectivity to the Internet.</span></span> <span data-ttu-id="4dfee-288">따라서 이러한 유닛을 OS 제공자에 등록하고 패치를 다운로드하여 적용하는 것은 간단한 프로세스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-288">Hence it is not a straightforward process to register such a unit with the OS provider and to download and apply patches.</span></span> <span data-ttu-id="4dfee-289">SUSE Linux의 경우 Azure VM에 SMT 서버를 설정하는 것이 하나의 솔루션이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-289">In the case of SUSE Linux, one solution could be to set up an SMT server in an Azure VM.</span></span> <span data-ttu-id="4dfee-290">반면에 Azure VM은 HANA 큰 인스턴스에 연결된 Azure VNet에서 호스트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-290">Whereas the Azure VM needs to be hosted in an Azure VNet, which is connected to the HANA Large Instance.</span></span> <span data-ttu-id="4dfee-291">이러한 SMT 서버를 사용하면 HANA Large Instance 유닛이 패치를 등록하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-291">With such an SMT server, the HANA Large Instance unit could register and download patches.</span></span> 

<span data-ttu-id="4dfee-292">SUSE의 [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf)(SLES 12 SP2용 구독 관리 도구) 사이트에 자세한 지침이 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-292">SUSE provides a larger guide on their [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf).</span></span> 

<span data-ttu-id="4dfee-293">HANA Large Instance에 대한 작업을 수행하는 SMT 서버를 설치하기 위한 전제 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-293">As precondition for the installation of an SMT server that fulfills the task for HANA Large Instance, you would need:</span></span>

- <span data-ttu-id="4dfee-294">HANA Large Instance ER 회로에 연결된 Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="4dfee-294">An Azure VNet that is connected to the HANA Large Instance ER circuit.</span></span>
- <span data-ttu-id="4dfee-295">조직과 연결된 SUSE 계정.</span><span class="sxs-lookup"><span data-stu-id="4dfee-295">A SUSE account that is associated with an organization.</span></span> <span data-ttu-id="4dfee-296">조직에는 유효한 SUSE 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-296">Whereas the organization would need to have some valid SUSE subscription.</span></span>

### <a name="installation-of-smt-server-on-azure-vm"></a><span data-ttu-id="4dfee-297">Azure VM에 SMT 서버 설치</span><span class="sxs-lookup"><span data-stu-id="4dfee-297">Installation of SMT server on Azure VM</span></span>

<span data-ttu-id="4dfee-298">이 단계에서는 Azure VM에 SMT 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-298">In this step, you install the SMT server in an Azure VM.</span></span> <span data-ttu-id="4dfee-299">첫 번째 조치는 [SUSE Customer Center](https://scc.suse.com/)(SUSE 고객 센터)에 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-299">The first measure is to log in to the [SUSE Customer Center](https://scc.suse.com/)</span></span>

<span data-ttu-id="4dfee-300">로그인한 상태에서 Organization(조직)--> Organization Credentials(조직 자격 증명)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-300">As you are logged in, go to Organization--> Organization Credentials.</span></span> <span data-ttu-id="4dfee-301">이 섹션에서 SMT 서버를 설정하는 데 필요한 자격 증명을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-301">In that section you should find the credentials that are necessary to set up the SMT server.</span></span>

<span data-ttu-id="4dfee-302">세 번째 단계는 Azure VNet에 SUSE Linux VM을 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-302">The third step is to install a SUSE Linux VM in the Azure VNet.</span></span> <span data-ttu-id="4dfee-303">VM을 배포하려면 Azure의 SLES 12 SP2 갤러리 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-303">To deploy the VM, take a SLES 12 SP2 gallery image of Azure.</span></span> <span data-ttu-id="4dfee-304">배포 과정에서 DNS 이름을 정의하지 않고 고정 IP 주소를 사용하지 마십시오(아래 스크린샷 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-304">In the deployment process, don't define a DNS name and do not use static IP addresses as seen in this screen shot</span></span>

![SMT 서버용 VM 배포](./media/hana-installation/image3_vm_deployment.png)

<span data-ttu-id="4dfee-306">배포된 VM은 더 작은 VM이고 Azure VNet에서 내부 IP 주소인 10.34.1.4를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-306">The deployed VM was a smaller VM and got the internal IP address in the Azure VNet of 10.34.1.4.</span></span> <span data-ttu-id="4dfee-307">VM의 이름은 smtserver였습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-307">Name of the VM was smtserver.</span></span> <span data-ttu-id="4dfee-308">설치 후 HANA 큰 인스턴스 유닛에 대한 연결이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-308">After the installation, the connectivity to the HANA Large instance unit(s) was checked.</span></span> <span data-ttu-id="4dfee-309">이름 확인을 구성하는 방식에 따라 Azure VM의 etc/hosts에 HANA 큰 인스턴스 유닛의 확인을 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-309">Dependent on how you organized name resolution you might need to configure resolution of the HANA Large Instance units in etc/hosts of the Azure VM.</span></span> <span data-ttu-id="4dfee-310">패치를 보관하는 데 사용할 VM에 디스크를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-310">Add an additional disk to the VM that is going to be used to hold the patches.</span></span> <span data-ttu-id="4dfee-311">부팅 디스크 자체가 너무 작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-311">The boot disk itself could be too small.</span></span> <span data-ttu-id="4dfee-312">데모의 경우 다음 스크린샷처럼 디스크가 /srv/www/htdocs에 탑재되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-312">In the case demonstrated, the disk got mounted to /srv/www/htdocs as shown in the following screenshot.</span></span> <span data-ttu-id="4dfee-313">100GB 디스크로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-313">A 100 GB disk should suffice.</span></span>

![SMT 서버용 VM 배포](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

<span data-ttu-id="4dfee-315">HANA 큰 인스턴스 유닛에 로그인하고 /etc/hosts를 유지 관리하고 네트워크를 통해 SMT 서버를 실행해야 하는 Azure VM에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-315">Log in to the HANA Large Instance unit(s), maintain /etc/hosts and check whether you can reach the Azure VM that is supposed to run the SMT server over the network.</span></span>

<span data-ttu-id="4dfee-316">이 확인이 성공적으로 완료되면 SMT 서버를 실행할 Azure VM에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-316">After this check is done successfully, you need to log in to the Azure VM that should run the SMT server.</span></span> <span data-ttu-id="4dfee-317">putty를 사용하여 VM에 로그인하는 경우 bash 창에서 다음 명령을 순서대로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-317">If you are using putty to log in to the VM, you need to execute this sequence of commands in your bash window:</span></span>

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

<span data-ttu-id="4dfee-318">이 명령을 실행한 후 bash를 다시 시작하여 설정을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-318">After executing these commands, restart your bash to activate the settings.</span></span> <span data-ttu-id="4dfee-319">그런 다음 YAST를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-319">Then start YAST.</span></span>

<span data-ttu-id="4dfee-320">YAST에서 Software Maintenance(소프트웨어 유지 관리)로 이동하여 smt를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-320">In YAST, go to Software Maintenance and search for smt.</span></span> <span data-ttu-id="4dfee-321">smt를 선택하면 yast2-smt로 자동으로 전환됩니다(아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-321">Select smt, which switches automatically to yast2-smt as shown below</span></span>

![yast의 SMT](./media/hana-installation/image5_smt_in_yast.PNG)


<span data-ttu-id="4dfee-323">smtserver에 설치를 위한 선택 사항을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-323">Accept the selection for installation on the smtserver.</span></span> <span data-ttu-id="4dfee-324">설치가 완료되면 SMT 서버 구성으로 이동하여 앞에서 검색한 SUSE Customer Center(SUSE 고객 센터)의 조직 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-324">Once installed, go to the SMT server configuration and enter the organizational credentials from the SUSE Customer Center you retrieved earlier.</span></span> <span data-ttu-id="4dfee-325">Azure VM 호스트 이름을 SMT 서버 URL로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-325">Also enter your Azure VM hostname as the SMT Server URL.</span></span> <span data-ttu-id="4dfee-326">이 데모에서는 https://smtserver 입니다(다음 그래픽 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-326">In this demonstration, it was https://smtserver as displayed in the next graphics.</span></span>

![SMT 서버 구성](./media/hana-installation/image6_configuration_of_smtserver1.png)

<span data-ttu-id="4dfee-328">다음 단계로, SUSE Customer Center(SUSE 고객 센터)에 대한 연결이 작동하는지 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-328">As next step, you need to test whether the connection to the SUSE Customer Center works.</span></span> <span data-ttu-id="4dfee-329">다음 그래픽에서 볼 수 있듯이 데모에서는 작동이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-329">As you see in the following graphics, in the demonstration case, it did work.</span></span>

![SUSE Customer Center(SUSE 고객 센터)에 대한 연결 테스트](./media/hana-installation/image7_test_connect.png)

<span data-ttu-id="4dfee-331">SMT 설정이 시작되면 데이터베이스 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-331">Once the SMT setup starts, you need to provide a database password.</span></span> <span data-ttu-id="4dfee-332">새로운 설치이므로 다음 그래픽과 같이 암호를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-332">Since it is a new installation, you need to define that password as shown in the next graphics.</span></span>

![데이터베이스에 대한 암호 정의](./media/hana-installation/image8_define_db_passwd.PNG)

<span data-ttu-id="4dfee-334">다음 인터랙션은 인증서가 만들어 질 때 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-334">The next interaction you have is when a certificate gets created.</span></span> <span data-ttu-id="4dfee-335">다음과 같이 대화 상자를 통해 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-335">Go through the dialog as shown next and the step should proceed.</span></span>

![SMT 서버의 인증서 만들기](./media/hana-installation/image9_certificate_creation.PNG)

<span data-ttu-id="4dfee-337">구성 끝 부분의 'Run synchronization check'(동기화 확인 실행) 단계에서 몇 분 정도가 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-337">There might be some minutes spent in the step of 'Run synchronization check' at the end of the configuration.</span></span> <span data-ttu-id="4dfee-338">SMT 서버를 설치하고 구성한 후에는 탑재 지점인 /srv/www/htdocs/ 아래에서 repo 디렉터리와 repo의 하위 디렉터리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-338">After the installation and configuration of the SMT server, you should find the directory repo under the mount point /srv/www/htdocs/ plus some sub-directories under repo.</span></span> 

<span data-ttu-id="4dfee-339">다음 명령으로 SMT 서버 및 관련 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-339">Restart the SMT server and its related services with these commands.</span></span>

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a><span data-ttu-id="4dfee-340">SMT 서버에 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="4dfee-340">Download of packages onto SMT server</span></span>

<span data-ttu-id="4dfee-341">모든 서비스가 다시 시작된 후 Yast를 사용하여 SMT Management에서 적절한 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-341">After all the services are restarted, select the appropriate packages in SMT Management using Yast.</span></span> <span data-ttu-id="4dfee-342">패키지 선택은 SMT 서버를 실행하는 SLES 릴리스 또는 VM 버전이 아니라 HANA 큰 인스턴스 서버의 OS 이미지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-342">The package selection depends on the OS image of the HANA Large Instance  server and not on the SLES release or version of the VM running the SMT server.</span></span> <span data-ttu-id="4dfee-343">선택 화면의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-343">An example of the selection screen is shown below.</span></span>

![패키지 선택](./media/hana-installation/image10_select_packages.PNG)

<span data-ttu-id="4dfee-345">패키지 선택이 끝나면 설정한 SMT 서버에 선택한 패키지의 초기 복사를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-345">Once you are finished with the package selection, you need to start the initial copy of the select packages to the SMT server you set up.</span></span> <span data-ttu-id="4dfee-346">이 복사는 smt-mirror 명령을 사용하여 셸에서 트리거됩니다(아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-346">This copy is triggered in the shell using the command smt-mirror as shown below</span></span>


![SMT 서버에 패키지 다운로드](./media/hana-installation/image11_download_packages.PNG)

<span data-ttu-id="4dfee-348">위에서 볼 수 있듯이 패키지는 탑재 지점 /srv/www/htdocs 아래 생성된 디렉터리에 복사되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-348">As you see above, the packages should get copied into the directories created under the mount point /srv/www/htdocs.</span></span> <span data-ttu-id="4dfee-349">이 프로세스는 시간이 어느 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-349">This process can take a while.</span></span> <span data-ttu-id="4dfee-350">선택한 패키지 수에 따라 최대 1시간 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-350">Dependent on how many packages you select, it could take up to one hour or more.</span></span>
<span data-ttu-id="4dfee-351">이 프로세스를 마치면 SMT 클라이언트 설정으로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-351">As this process finishes, you need to move to the SMT client setup.</span></span> 

### <a name="set-up-the-smt-client-on-hana-large-instance-units"></a><span data-ttu-id="4dfee-352">HANA 큰 인스턴스 유닛에 SMT 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="4dfee-352">Set up the SMT client on HANA Large Instance units</span></span>

<span data-ttu-id="4dfee-353">이 경우 클라이언트는 HANA 큰 인스턴스 유닛입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-353">The client(s) in this case are the HANA Large Instance units.</span></span> <span data-ttu-id="4dfee-354">SMT 서버 설정이 clientSetup4SMT.sh 스크립트를 Azure VM에 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-354">The SMT server setup copied the script clientSetup4SMT.sh into the Azure VM.</span></span> <span data-ttu-id="4dfee-355">이 스크립트를 SMT 서버에 연결할 HANA 큰 인스턴스 유닛으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-355">Copy that script over to the HANA Large Instance unit you want to connect to your SMT server.</span></span> <span data-ttu-id="4dfee-356">-h 옵션을 사용하여 스크립트를 시작하고 매개 변수로 SMT 서버의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-356">Start the script with the -h option and give it as parameter the name of your SMT server.</span></span> <span data-ttu-id="4dfee-357">이 예제에서는 smtserver입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-357">In this example smtserver.</span></span>

![SMT 클라이언트 구성](./media/hana-installation/image12_configure_client.PNG)

<span data-ttu-id="4dfee-359">클라이언트에 의해 서버에서 인증서 로드가 성공했지만 등록이 실패하는 시나리오가 있을 수 있습니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-359">There might be a scenario where the load of the certificate from the server by the client succeeded, but the registration failed as shown below.</span></span>

![클라이언트 등록 실패](./media/hana-installation/image13_registration_failed.PNG)

<span data-ttu-id="4dfee-361">등록이 실패하면 [ SUSE 지원 문서](https://www.suse.com/de-de/support/kb/doc/?id=7006024)를 읽고 문서에 설명된 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-361">If the registration failed, read this [SUSE support document](https://www.suse.com/de-de/support/kb/doc/?id=7006024) and execute the steps described there.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4dfee-362">서버 이름으로 VM 이름을 제공해야 합니다. 이 경우 smtserver이며 정규화된 도메인 이름은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-362">As server name you need to provide the name of the VM, in this case smtserver, without the fully qualified domain name.</span></span> <span data-ttu-id="4dfee-363">VM 이름만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-363">Just the VM name works.</span></span> 

<span data-ttu-id="4dfee-364">이 단계를 실행한 후에는 HANA 큰 인스턴스 유닛에서 다음 명령을 실행해야 합니다</span><span class="sxs-lookup"><span data-stu-id="4dfee-364">After these steps have been executed, you need to execute the following command on the HANA Large Instance unit</span></span>

```
SUSEConnect –cleanup
```

> [!Note] 
> <span data-ttu-id="4dfee-365">지난 테스트에서는 해당 단계 후 항상 몇 분을 기다려야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-365">In our tests we always had to wait a few minutes after that step.</span></span> <span data-ttu-id="4dfee-366">SUSE 문서에 설명된 시정 조치 후에 즉시 실행되는 clientSetup4SMT.sh는 인증서가 아직 유효하지 않다는 메시지로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-366">The immediate execution clientSetup4SMT.sh, after the corrective measures described in the SUSE article, ended with messages that the certificate would not be valid yet.</span></span> <span data-ttu-id="4dfee-367">대개 5~10분을 기다려서 clientSetup4SMT.sh를 실행하면 클라이언트 구성이 성공적으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-367">Waiting for 5-10 minutes usually and executing clientSetup4SMT.sh ended in a successful client configuration.</span></span>

<span data-ttu-id="4dfee-368">SUSE 문서의 단계를 기반으로 수정해야 하는 문제가 발생하면 HANA 큰 인스턴스 유닛에서 clientSetup4SMT.sh를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-368">If you ran into the issue that you needed to fix based on the steps of the SUSE article, you need to restart clientSetup4SMT.sh on the HANA Large Instance unit again.</span></span> <span data-ttu-id="4dfee-369">이제 아래와 같이 성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-369">Now it should finish successfully as shown below.</span></span>

![클라이언트 등록 성공](./media/hana-installation/image14_finish_client_config.PNG)

<span data-ttu-id="4dfee-371">이 단계에서 Azure VM에 설치된 SMT 서버에 연결하기 위해 HANA 큰 인스턴스 유닛의 SMT 클라이언트를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-371">With this step, you configured the SMT client of the HANA Large Instance unit to connect against the SMT server you installed in the Azure VM.</span></span> <span data-ttu-id="4dfee-372">이제 'zypper up' 또는 'zypper in'을 사용하여 HANA 큰 인스턴스에 OS 패치를 설치하거나 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-372">You now can take 'zypper up' or 'zypper in' to install OS patches to HANA Large Instances or install additional packages.</span></span> <span data-ttu-id="4dfee-373">이전에 다운로드한 패치만 SMT 서버에서 가져올 수 있는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-373">It is understood that you only can get patches that you downloaded before on the SMT server.</span></span>


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a><span data-ttu-id="4dfee-374">HANA 큰 인스턴스에 SAP HANA 설치의 예</span><span class="sxs-lookup"><span data-stu-id="4dfee-374">Example of an SAP HANA installation on HANA Large Instances</span></span>
<span data-ttu-id="4dfee-375">이 섹션에서는 HANA 큰 인스턴스 유닛에 SAP HANA를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-375">This section illustrates how to install SAP HANA on a HANA Large Instance unit.</span></span> <span data-ttu-id="4dfee-376">시작 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-376">The start state we have look  like:</span></span>

- <span data-ttu-id="4dfee-377">SAP HANA 큰 인스턴스에 배포하기 위해 Microsoft에 모든 데이터를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-377">You provided Microsoft all the data to deploy you an SAP HANA Large Instance.</span></span>
- <span data-ttu-id="4dfee-378">Microsoft로부터 SAP HANA 큰 인스턴스를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-378">You received the SAP HANA Large Instance from Microsoft.</span></span>
- <span data-ttu-id="4dfee-379">온-프레미스 네트워크에 연결된 Azure VNet을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-379">You created an Azure VNet that is connected to your on-premise network.</span></span>
- <span data-ttu-id="4dfee-380">HANA 큰 인스턴스용 ExpressRoute 회로를 동일한 Azure VNet에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-380">You connected the ExpressRotue circuit for HANA Large Instances to the same Azure VNet.</span></span>
- <span data-ttu-id="4dfee-381">HANA 큰 인스턴스의 점프 박스로 사용하는 Azure VM을 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-381">You installed an Azure VM you use as a jump box for HANA Large Instances.</span></span>
- <span data-ttu-id="4dfee-382">점프 박스에서 HANA 큰 인스턴스 유닛으로 연결할 수 있고 그 반대로도 연결할 수 있는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-382">You made sure that you can connect from the jump box to your HANA Large Instance unit and vice versa.</span></span>
- <span data-ttu-id="4dfee-383">필요한 패키지와 패치가 모두 설치되어 있는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-383">You checked whether all the necessary packages and patches are installed.</span></span>
- <span data-ttu-id="4dfee-384">사용 중인 OS에 HANA 설치에 관한 SAP 메모 및 문서를 읽었고 선택한 HANA 릴리스가 OS 릴리스에서 지원되는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-384">You read the SAP notes and documentations regarding HANA installation on the OS you are using and made sure that the HANA release of choice is supported on the OS release.</span></span>

<span data-ttu-id="4dfee-385">다음 순서로 표시되는 내용은 점프 박스 VM(이 경우 Windows OS에서 실행 중인)에 HANA 설치 패키지를 다운로드하고, HANA 큰 인스턴스 유닛에 패키지를 복사하고 설치하는 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-385">What is shown in the next sequences is the download of the HANA installation packages to the jump box VM, in this case running on a Windows OS, the copy of the packages to the HANA Large Instance unit and the sequence of the setup.</span></span>

### <a name="download-of-the-sap-hana-installation-bits"></a><span data-ttu-id="4dfee-386">SAP HANA 설치 비트 다운로드</span><span class="sxs-lookup"><span data-stu-id="4dfee-386">Download of the SAP HANA installation bits</span></span>
<span data-ttu-id="4dfee-387">HANA 큰 인스턴스 장치는 인터넷에 직접 연결되어 있지 않기 때문에 설치 패키지를 SAP에서 HANA 큰 인스턴스 VM으로 직접 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-387">Since the HANA Large Instance units don't have direct connectivity to the internet, you can't directly download the installation packages from SAP to the HANA Large Instance VM.</span></span> <span data-ttu-id="4dfee-388">인터넷에 직접 연결되지 않는 상황을 해결하려면 점프 박스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-388">To overcome the missing direct internet connectivity, you need the jump box.</span></span> <span data-ttu-id="4dfee-389">패키지를 점프 박스 VM에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-389">You download the packages to the jump box VM.</span></span>

<span data-ttu-id="4dfee-390">HANA 설치 패키지를 다운로드하려면 SAP Marketplace에 액세스할 수 있는 SAP S-user 또는 다른 사용자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-390">In order to download the HANA installation packages, you need an SAP S-user or other user, which allows you to access the SAP Marketplace.</span></span> <span data-ttu-id="4dfee-391">로그인한 후 화면의 순서에 따라 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-391">Go through this sequence of screens after logging in:</span></span>

<span data-ttu-id="4dfee-392">[SAP Service Marketplace](https://support.sap.com/en/index.html)로 이동하여 > Download Software(소프트웨어 다운로드) > Installations and Upgrade(설치 및 업그레이드) >By Alphabetical Index(알파벳 순서에 따라)를 클릭하고 H – SAP HANA Platform Edition > SAP HANA Platform Edition 2.0 > Installation(설치) 아래에서 다음 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-392">Go to [SAP Service Marketplace](https://support.sap.com/en/index.html) > Click Download Software > Installations and Upgrade >By Alphabetical Index >Under H – SAP HANA Platform Edition > SAP HANA Platform Edition 2.0 > Installation > Download the following files</span></span>

![HANA 설치 다운로드](./media/hana-installation/image16_download_hana.PNG)

<span data-ttu-id="4dfee-394">데모에서는 SAP HANA 2.0 설치 패키지를 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-394">In the demonstration case, we downloaded SAP HANA 2.0 installation packages.</span></span> <span data-ttu-id="4dfee-395">Azure 점프 박스 VM에서 자동 압축 해제 아카이브를 디렉터리에 추출합니다(아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="4dfee-395">On the Azure jump box VM, you expand the self-extracting archives into the directory as shown below.</span></span>

![HANA 설치 추출](./media/hana-installation/image17_extract_hana.PNG)

<span data-ttu-id="4dfee-397">아카이브가 추출되면 추출을 통해 생성된 디렉터리(위의 경우 51052030)를 HANA 큰 인스턴스 유닛에서 /hana/shared 볼륨으로 작성한 디렉터리로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-397">As the archives are extracted, copy the directory created by the extraction, in the case above 51052030, to the HANA Large instance unit into the /hana/shared volume into a directory you created.</span></span>

> [!Important]
> <span data-ttu-id="4dfee-398">공간에 제한되어 있고 다른 프로세스에서도 사용해야 하므로 설치 패키지를 루트 또는 부팅 LUN에 복사하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4dfee-398">Do Not copy the installation packages into the root or boot LUN since space is limited and needs to be used by other processes as well.</span></span>


### <a name="install-sap-hana-on-the-hana-large-instance-unit"></a><span data-ttu-id="4dfee-399">HANA 큰 인스턴스 유닛에 SAP HANA 설치</span><span class="sxs-lookup"><span data-stu-id="4dfee-399">Install SAP HANA on the HANA Large Instance unit</span></span>
<span data-ttu-id="4dfee-400">SAP HANA를 설치하려면 root 사용자로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-400">In order to install SAP HANA, you need to log in as user root.</span></span> <span data-ttu-id="4dfee-401">root만 SAP HANA를 설치할 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-401">Only root has enough permissions to install SAP HANA.</span></span>
<span data-ttu-id="4dfee-402">먼저 해야 할 일은 /hana/shared에 복사한 디렉터리에 대한 권한을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-402">The first thing you need to do is to set permissions on the directory you copied over into /hana/shared.</span></span> <span data-ttu-id="4dfee-403">권한은 다음과 같이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-403">The permissions need to set like</span></span>

```
chmod –R 744 <Installation bits folder>
```

<span data-ttu-id="4dfee-404">그래픽 설치를 사용하여 SAP HANA를 설치하려면 gtk2 패키지가 HANA 큰 인스턴스에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-404">If you want to install SAP HANA using the graphical setup, the gtk2 package needs to be installed on the HANA Large Instances.</span></span> <span data-ttu-id="4dfee-405">명령을 사용하여 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-405">Check whether it is installed with the command</span></span>

```
rpm –qa | grep gtk2
```

<span data-ttu-id="4dfee-406">이후 단계에서는 그래픽 사용자 인터페이스를 사용하여 SAP HANA 설치를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-406">In further steps, we are demonstrating the SAP HANA setup with the graphical user interface.</span></span> <span data-ttu-id="4dfee-407">다음 단계로 설치 디렉터리로 이동하여 하위 디렉터리인 HDB_LCM_LINUX_X86_64로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-407">As next step, go into the installation directory and navigate into the sub directory HDB_LCM_LINUX_X86_64.</span></span> <span data-ttu-id="4dfee-408">시작</span><span class="sxs-lookup"><span data-stu-id="4dfee-408">Start</span></span>

```
./hdblcmgui 
```
<span data-ttu-id="4dfee-409">해당 디렉터리에서.</span><span class="sxs-lookup"><span data-stu-id="4dfee-409">out of that directory.</span></span> <span data-ttu-id="4dfee-410">이제 설치를 위해 데이터를 제공해야 하는 일련의 화면이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-410">Now you are getting guided through a sequence of screens where you need to provide the data for the installation.</span></span> <span data-ttu-id="4dfee-411">데모에서는 SAP HANA 데이터베이스 서버 및 SAP HANA 클라이언트 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-411">In the case demonstrated, we are installing the SAP HANA database server and the SAP HANA client components.</span></span> <span data-ttu-id="4dfee-412">따라서 아래와 같이 'SAP HANA Database'(SAP HANA 데이터베이스)가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-412">Therefore our selection is 'SAP HANA Database' as shown below</span></span>

![설치 시 HANA 선택](./media/hana-installation/image18_hana_selection.PNG)

<span data-ttu-id="4dfee-414">다음 화면에서는 'Install New System'(새 시스템 설치) 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-414">In the next screen, you choose the option 'Install New System'</span></span>

![HANA 신규 설치 선택](./media/hana-installation/image19_select_new.PNG)

<span data-ttu-id="4dfee-416">이 단계 후에는 SAP HANA 데이터베이스 서버에 추가로 설치할 수 있는 몇 가지 추가 구성 중 하나를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-416">After this step, you need to select between several additional components that can be installed additionally to the SAP HANA database server.</span></span>

![추가 HANA 구성 요소 선택](./media/hana-installation/image20_select_components.PNG)

<span data-ttu-id="4dfee-418">이 문서에서는 SAP HANA Client와 SAP HANA Studio를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-418">For the purpose of this documentation, we chose the SAP HANA Client and the SAP HANA Studio.</span></span> <span data-ttu-id="4dfee-419">강화 인스턴스도 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-419">We also installed a scale-up instance.</span></span> <span data-ttu-id="4dfee-420">따라서 다음 화면에서 'Single-Host System'(단일 호스트 시스템)을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-420">hence in the next screen, you need to choose 'Single-Host System'</span></span> 

![강화 설치 선택](./media/hana-installation/image21_single_host.PNG)

<span data-ttu-id="4dfee-422">다음 화면에서 몇 가지 데이터를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-422">In the next screen, you need to provide some data</span></span>

![SAP HANA SID 제공](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> <span data-ttu-id="4dfee-424">HANA SID(System ID)로 HANA 큰 인스턴스 배포를 주문할 때 Microsoft에 제공한 것과 동일한 SID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-424">As HANA System ID (SID), you need to provide the same SID, as you provided Microsoft when you ordered the HANA Large Instance deployment.</span></span> <span data-ttu-id="4dfee-425">다른 SID를 선택하면 다른 볼륨의 액세스 권한 문제로 인해 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-425">Choosing a different SID makes the installation fail due to access permission problems on the different volumes</span></span>

<span data-ttu-id="4dfee-426">설치 디렉터리로 /hana/shared 디렉터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-426">As installation directory you use the /hana/shared directory.</span></span> <span data-ttu-id="4dfee-427">다음 단계에서는 HANA 데이터 파일과 HANA 로그 파일의 위치를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-427">In the next step, you need to provide the locations for the HANA data files and the HANA log files</span></span>


![HANA 로그 위치 제공](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> <span data-ttu-id="4dfee-429">데이터 및 로그 파일로 이 화면의 이전 화면에서 선택한 SID가 포함된 탑재 지점과 함께 제공된 볼륨을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-429">You should define as data and log files the volumes that came already with the mount points that contain the SID you chose in the screen selection before this screen.</span></span> <span data-ttu-id="4dfee-430">SID가 앞의 화면에서 입력한 내용과 일치하지 않으면 뒤로 돌아가서 탑재 지점에 있는 값으로 SID를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-430">If the SID does mismatch with the one you typed in, in the screen before, go back and adjust the SID to the value you have on the mount points.</span></span>

<span data-ttu-id="4dfee-431">다음 단계에서 호스트 이름을 검토하고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-431">In the next step, review the host name and eventually correct it.</span></span> 

![호스트 이름 검토](./media/hana-installation/image24_review_host_name.PNG)

<span data-ttu-id="4dfee-433">다음 단계에서는 HANA 큰 인스턴스 배포를 주문할 때 Microsoft에 제공한 데이터를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-433">In the next step, you also need to retrieve data you gave to Microsoft when you ordered the HANA Large Instance deployment.</span></span> 

![시스템 사용자 UID 및 GID 제공](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> <span data-ttu-id="4dfee-435">유닛 배포를 주문할 때 Microsoft에 제공한 것과 동일한 사용자 ID 및 사용자 그룹 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-435">You need to provide the same System User ID and ID of User Group as you provided Microsoft as you order the unit deployment.</span></span> <span data-ttu-id="4dfee-436">동일한 ID를 제공하지 못하면 HANA 큰 인스턴스 유닛에 SAP HANA를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-436">If you fail to give the very same IDs, the installation of SAP HANA on the HANA Large Instance unit fails.</span></span>

<span data-ttu-id="4dfee-437">다음 두 화면에서는 이 문서에는 없지만 SAP HANA 데이터베이스 인스턴스의 일부로 설치되는 SAP Host Agent에 사용되는 SAP HANA 데이터베이스의 SYSTEM 사용자에 대한 암호와 sapadm 사용자에 대한 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-437">In the next two screens, which we are not showing in this documentation, you need to provide the password for the SYSTEM user of the SAP HANA database and the password for the sapadm user, which is used for the SAP Host Agent that gets installed as part of the SAP HANA database instance.</span></span>

<span data-ttu-id="4dfee-438">암호를 정의한 후 확인 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-438">After defining the password, a confirmation screen is showing up.</span></span> <span data-ttu-id="4dfee-439">나열된 모든 데이터를 확인하고 설치를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-439">check all the data listed and continue with the installation.</span></span> <span data-ttu-id="4dfee-440">아래와 같이 설치 진행률을 보여주는 진행률 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-440">You reach a progress screen that documents the installation progress, like the one below</span></span>

![설치 진행률 확인](./media/hana-installation/image27_show_progress.PNG)

<span data-ttu-id="4dfee-442">설치를 마치면 다음과 같은 그림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-442">As the installation finishes, you should a picture like the following one</span></span>

![설치를 마쳤습니다.](./media/hana-installation/image28_install_finished.PNG)

<span data-ttu-id="4dfee-444">이 시점에서 SAP HANA 인스턴스가 실행되어 사용할 준비가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-444">At this point, the SAP HANA instance should be up and running and ready for usage.</span></span> <span data-ttu-id="4dfee-445">SAP HANA Studio에서 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-445">You should be able to connect to it from SAP HANA Studio.</span></span> <span data-ttu-id="4dfee-446">또한 SAP HANA의 최신 패치를 확인하고 해당 패치를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dfee-446">Also make sure that you check for the latest patches of SAP HANA and apply those patches.</span></span>
























































 







 




