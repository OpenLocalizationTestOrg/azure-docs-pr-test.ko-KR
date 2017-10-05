---
title: "인증서를 사용하여 Windows에서 Azure Service Fabric 클러스터 보안 유지 | Microsoft Docs"
description: "이 문서에서는 클라이언트와 클러스터 사이 뿐만 아니라 독립 실행형 클러스터 또는 개인 클러스터 내에서 통신을 보호하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="341a8-103">X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="341a8-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="341a8-104">이 문서에서는 독립 실행형 Windows 클러스터의 다양한 노드 간에 통신을 보호하는 방법 뿐만 아니라 X.509 인증서를 사용하여 이 클러스터에 연결된 클라이언트를 인증하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="341a8-105">이렇게 하면 권한이 있는 사용자만 클러스터 및 배포된 응용 프로그램에 액세스할 수 있으며 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="341a8-106">인증서 보안은 클러스터가 만들어지기 전에 클러스터에서 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="341a8-107">노드 간 보안, 클라이언트-노드 보안 및 역할 기반 액세스 제어와 같은 클러스터 보안에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="341a8-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="341a8-108">어떤 인증서가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="341a8-108">Which certificates will you need?</span></span>
<span data-ttu-id="341a8-109">처음에 클러스터의 노드 중 하나에 [독립 실행형 클러스터 패키지를 다운로드](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="341a8-110">다운로드한 패키지에서 **ClusterConfig.X509.MultiMachine.json** 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="341a8-111">파일을 열고 **속성** 섹션의 **보안**을 위한 섹션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="341a8-112">이 섹션에서는 독립 실행형 Windows 클러스터를 보호하기 위한 인증서를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="341a8-113">클러스터 인증서를 지정하는 경우 **ClusterCredentialType** 값을  _**X509**_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="341a8-114">외부 연결에 대한 서버 인증서를 지정하려면 **ServerCredentialType**을 _**X509**_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="341a8-115">필수는 아니지만 적절히 보안된 클러스터에 대해 이 두 인증서를 모두 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="341a8-116">이러한 값을 *X509*로 설정하면 해당 인증서를 지정해야 합니다. 그러지 않으면 Service Fabric이 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="341a8-117">일부 시나리오에서는 _ClientCertificateThumbprints_ 또는 _ReverseProxyCertificate_만 지정하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="341a8-118">이러한 시나리오에서는 _ClusterCredentialType_ 또는 _ServerCredentialType_을 _X509_로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="341a8-119">[지문](https://en.wikipedia.org/wiki/Public_key_fingerprint) 은 인증서의 기본 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="341a8-120">[인증서의 지문을 검색하는 방법](https://msdn.microsoft.com/library/ms734695.aspx) 을 참고하여 만든 인증서의 지문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="341a8-121">다음 테이블에서는 클러스터 설치에 필요한 인증서를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="341a8-122">**CertificateInformation 설정**</span><span class="sxs-lookup"><span data-stu-id="341a8-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="341a8-123">**설명**</span><span class="sxs-lookup"><span data-stu-id="341a8-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="341a8-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="341a8-124">ClusterCertificate</span></span> |<span data-ttu-id="341a8-125">테스트 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-125">Recommended for test environment.</span></span> <span data-ttu-id="341a8-126">이 인증서는 클러스터에서 노드 간의 통신을 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="341a8-127">업그레이드에 두 개의 다른 인증서, 기본 및 보조 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="341a8-128">**지문** 섹션에서 기본 인증서의 지문 및 **ThumbprintSecondary** 변수에서 보조 인증서의 지문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="341a8-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="341a8-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="341a8-130">프로덕션 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-130">Recommended for production environment.</span></span> <span data-ttu-id="341a8-131">이 인증서는 클러스터에서 노드 간의 통신을 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="341a8-132">하나 또는 두 개의 클러스터 인증서 일반 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="341a8-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="341a8-133">ServerCertificate</span></span> |<span data-ttu-id="341a8-134">테스트 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-134">Recommended for test environment.</span></span> <span data-ttu-id="341a8-135">이 인증서가 클러스터에 연결하려고 시도할 때 클라이언트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="341a8-136">편의상 *ClusterCertificate* 및 *ServerCertificate*에 동일한 인증서를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="341a8-137">업그레이드에 두 개의 다른 서버 인증서, 기본 및 보조 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="341a8-138">**지문** 섹션에서 기본 인증서의 지문 및 **ThumbprintSecondary** 변수에서 보조 인증서의 지문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="341a8-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="341a8-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="341a8-140">프로덕션 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-140">Recommended for production environment.</span></span> <span data-ttu-id="341a8-141">이 인증서가 클러스터에 연결하려고 시도할 때 클라이언트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="341a8-142">편의상 *ClusterCertificateCommonNames* 및 *ServerCertificateCommonNames*에 동일한 인증서를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="341a8-143">하나 또는 두 개의 서버 인증서 일반 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="341a8-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="341a8-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="341a8-145">인증된 클라이언트에 설치하려는 인증서의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="341a8-146">클러스터에 대한 액세스를 허용하려는 컴퓨터에 다양한 클라이언트 인증서가 설치되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="341a8-147">**CertificateThumbprint** 변수에서 각 인증서의 지문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="341a8-148">**IsAdmin** 을 *true*로 설정한 경우 이 인증서가 설치된 클라이언트는 클러스터에서 관리자 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="341a8-149">**IsAdmin** 이 *false*로 설정된 경우 이 인증서가 있는 클라이언트는 사용자 액세스 권한(일반적으로 읽기 전용)에 대해 허용되는 작업을 수행할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="341a8-150">역할에 대한 자세한 내용은 [RBAC(역할 기반 액세스 제어)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="341a8-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="341a8-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="341a8-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="341a8-152">**CertificateCommonName**에 대한 첫 번째 클라이언트 인증서의 일반 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="341a8-153">**CertificateIssuerThumbprint** 는 이 인증서의 발급자 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="341a8-154">[인증서 사용](https://msdn.microsoft.com/library/ms731899.aspx) 을 참고하여 일반 이름 및 발급자에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="341a8-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="341a8-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="341a8-156">테스트 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-156">Recommended for test environment.</span></span> <span data-ttu-id="341a8-157">이는 [역방향 프록시](service-fabric-reverseproxy.md)를 보호하려는 경우 지정될 수 있는 선택적인 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="341a8-158">이 인증서를 사용하는 경우 reverseProxyEndpointPort가 nodeTypes로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="341a8-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="341a8-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="341a8-160">프로덕션 환경에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-160">Recommended for production environment.</span></span> <span data-ttu-id="341a8-161">이는 [역방향 프록시](service-fabric-reverseproxy.md)를 보호하려는 경우 지정될 수 있는 선택적인 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="341a8-162">이 인증서를 사용하는 경우 reverseProxyEndpointPort가 nodeTypes로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="341a8-163">다음은 클러스터, 서버 및 클라이언트 인증서가 제공된 예제 클러스터 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="341a8-164">cluster/server/reverseProxy 인증서의 경우 동일한 인증서 형식에 지문 및 일반 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="341a8-165">인증서 롤오버</span><span class="sxs-lookup"><span data-stu-id="341a8-165">Certificate roll over</span></span>
<span data-ttu-id="341a8-166">지문 대신 인증서 일반 이름을 사용하는 경우 인증서 롤오버를 위해 클러스터 구성을 업그레이드하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="341a8-167">인증서 롤오버가 발급자 롤오버를 포함하는 경우 새 발급자 인증서를 설치한 후에 2시간 이상 인증서 저장소에 이전의 발급자 인증서를 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="341a8-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="341a8-168">X.509 인증서를 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="341a8-169">클러스터 내에서 통신을 보호하려면 클러스터 노드에 대한 X.509 인증서를 먼저 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="341a8-170">또한 권한이 있는 컴퓨터/사용자에게 이 클러스터에 연결을 제한하려면 클라이언트 컴퓨터에 인증서를 가져와서 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="341a8-171">프로덕션 워크로드를 실행하는 클러스터의 경우 클러스터 보호를 위해 [CA(인증 기관)](https://en.wikipedia.org/wiki/Certificate_authority) 로 서명된 X.509 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="341a8-172">이러한 인증서를 얻는 방법에 대한 자세한 내용은 [방법: 인증서 가져오기](http://msdn.microsoft.com/library/aa702761.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="341a8-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="341a8-173">테스트 목적으로 사용하는 클러스터의 경우 자체 서명된 인증서를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="341a8-174">선택 사항: 자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="341a8-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="341a8-175">제대로 보호할 수 있는 자체 서명된 인증서를 만드는 한 가지 방법은 *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure* 디렉터리의 Service Fabric SDK 폴더에 있는 *CertSetup.ps1* 스크립트를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="341a8-176">이 파일을 편집하여 인증서의 기본 이름을 변경합니다(값 *CN = ServiceFabricDevClusterCert* 검색).</span><span class="sxs-lookup"><span data-stu-id="341a8-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="341a8-177">이 스크립트를 `.\CertSetup.ps1 -Install`로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="341a8-178">이제 암호로 보호된 PFX 파일에 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="341a8-179">먼저 인증서의 지문을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="341a8-180">*시작* 메뉴에서 *컴퓨터 인증서 관리*를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="341a8-181">**로컬 컴퓨터/개인** 폴더로 이동하고 방금 만든 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="341a8-182">인증서를 두 번 클릭하여 열고 *세부 정보* 탭을 선택하고 *지문* 필드로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="341a8-183">공백을 제거한 후 아래 PowerShell 명령에 지문 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="341a8-184">`String` 값을 적절한 보안 암호로 변경하여 보호하고 PowerShell에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="341a8-185">컴퓨터에 설치된 인증서의 세부 정보를 보기 위해 다음 PowerShell 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="341a8-186">또는 Azure 구독을 보유한 경우 [Key Vault에 인증서 추가](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault) 섹션을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="341a8-187">인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-187">Install the certificates</span></span>
<span data-ttu-id="341a8-188">인증서를 만든 후에 클러스터 노드에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="341a8-189">노드에 최신 Windows PowerShell 3.x가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="341a8-190">클러스터와 서버 인증서 및 모든 보조 인증서의 경우 각 노드에서 이러한 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="341a8-191">.pfx 파일을 노드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="341a8-192">관리자 권한으로 PowerShell 창을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="341a8-193">*$pswd* 를 이 인증서를 만드는 데 사용한 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="341a8-194">*$PfxFilePath* 를 이 노드에 복사된 .pfx의 전체 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="341a8-195">이제 네트워크 서비스 계정에서 실행되는 Service Fabric 프로세스가 다음 스크립트를 실행하여 사용할 수 있도록 이 인증서에 액세스 제어를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="341a8-196">서비스 계정에 대해 인증서의 지문 및 "NETWORK SERVICE"를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="341a8-197">*시작* > *컴퓨터 인증서 관리*에서 인증서를 열고 *모든 작업* > *개인 키 관리*를 보고 인증서의 ACL이 올바른지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="341a8-198">각 서버 인증서에 대해 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="341a8-199">또한 이러한 단계를 사용하여 클러스터에 대한 액세스를 허용하려는 컴퓨터에 클라이언트 인증서를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="341a8-200">보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="341a8-200">Create the secure cluster</span></span>
<span data-ttu-id="341a8-201">**ClusterConfig.X509.MultiMachine.json** 파일의 **보안** 섹션을 구성한 후에 [클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md#createcluster) 섹션을 진행하여 노드를 구성하고 독립 실행형 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="341a8-202">클러스터를 만드는 동안 **ClusterConfig.X509.MultiMachine.json** 파일을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="341a8-203">예를 들어, 명령은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="341a8-204">보안 독립 실행형 Windows 클러스터를 성공적으로 실행하고 여기에 연결할 인증된 클라이언트를 설정했다면 [PowerShell을 사용하여 보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) 섹션을 따라 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="341a8-205">예:</span><span class="sxs-lookup"><span data-stu-id="341a8-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="341a8-206">그런 다음 다른 PowerShell 명령을 실행하면 이 클러스터에 대해 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="341a8-207">예를 들어 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps)는 이 보안 클러스터의 노드 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="341a8-208">클러스터를 제거하려면 Service Fabric 패키지를 다운로드한 클러스터의 노드에 연결하고 명령줄을 열고 패키지 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="341a8-209">이제 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="341a8-210">인증서 구성이 잘못되면 배포 도중 클러스터가 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341a8-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="341a8-211">보안 문제를 자체 진단하려면 이벤트 뷰어 그룹 *응용 프로그램 및 서비스 로그* > *Microsoft-Service Fabric*에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="341a8-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

