---
title: "Azure 마이크로 서비스에서 FabricTransport 설정 변경 | Microsoft Docs"
description: "Azure Service Fabric 행위자 통신 설정에 대해 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="00370-103">Reliable Actors에 대한 FabricTransport 설정 구성</span><span class="sxs-lookup"><span data-stu-id="00370-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="00370-104">구성할 수 있는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="00370-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="00370-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="00370-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="00370-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="00370-107">다음과 같은 방식으로 기본 FabricTransport 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="00370-108">어셈블리 특성</span><span class="sxs-lookup"><span data-stu-id="00370-108">Assembly attribute</span></span>

<span data-ttu-id="00370-109">[FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) 특성은 행위자 클라이언트 및 행위자 서비스 어셈블리에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="00370-110">다음 예제에서는 FabricTransport OperationTimeout 설정의 기본값을 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00370-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="00370-111">두 번째 예에서는 FabricTransport MaxMessageSize 및 OperationTimeoutInSeconds의 기본 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="00370-112">구성 패키지</span><span class="sxs-lookup"><span data-stu-id="00370-112">Config package</span></span>

<span data-ttu-id="00370-113">[구성 패키지](service-fabric-application-model.md)를 사용하여 기본 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="00370-114">행위자 서비스에 대한 FabricTransport 설정 구성</span><span class="sxs-lookup"><span data-stu-id="00370-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="00370-115">settings.xml 파일에 TransportSettings 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="00370-116">기본적으로 행위자 코드는 "&lt;ActorName&gt;TransportSettings"로 SectionName을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="00370-117">찾을 수 없는 경우 "TransportSettings"로 sectionName을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="00370-118">행위자 클라이언트 어셈블리에 대한 FabricTransport 설정 구성</span><span class="sxs-lookup"><span data-stu-id="00370-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="00370-119">클라이언트를 서비스의 일부로 실행하지 않는 경우에는 client exe 파일과 같은 위치에 "&lt;Client Exe Name&gt;.settings.xml" 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="00370-120">그런 다음 해당 파일에서 TransportSettings 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="00370-121">SectionName은 "TransportSettings"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="00370-122">보조 인증서로 보안 행위자 서비스/클라이언트에 대한 FabricTransport 설정 구성.</span><span class="sxs-lookup"><span data-stu-id="00370-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="00370-123">CertificateFindValuebySecondary 매개 변수를 추가하여 보조 인증서 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00370-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="00370-124">다음은 수신기 TransportSettings에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="00370-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="00370-125">다음은 클라이언트 TransportSettings에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="00370-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="00370-126">주체 이름을 사용한 행위자 서비스/클라이언트 보안을 위한 FabricTransport 설정 구성.</span><span class="sxs-lookup"><span data-stu-id="00370-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="00370-127">사용자는 FindBySubjectName,add CertificateIssuerThumbprints 및 CertificateRemoteCommonNames 값으로 findType을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00370-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="00370-128">다음은 수신기 TransportSettings에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="00370-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="00370-129">다음은 클라이언트 TransportSettings에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="00370-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
