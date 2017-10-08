---
title: "Azure 서비스 패브릭의 컬렉션 개체 serialization aaaReliable | Microsoft Docs"
description: "Azure Service Fabric 신뢰할 수 있는 컬렉션 개체 serialization"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="d4443-103">Azure Service Fabric의 신뢰할 수 있는 컬렉션 개체 serialization</span><span class="sxs-lookup"><span data-stu-id="d4443-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="d4443-104">복제 하 고 해당 항목 toomake이 내구성이 있는 컴퓨터 오류, 정전 있는지를 유지 하는 신뢰할 수 있는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="d4443-105">Tooreplicate와 toopersist 항목, 신뢰할 수 있는 컬렉션 필요 tooserialize 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="d4443-106">신뢰할 수 있는 컬렉션의 신뢰할 수 있는 상태 관리자에서 지정된 된 형식에 대 한 hello 적절 한 serializer를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="d4443-107">안정성 상태 관리자는 기본 제공 serializer가 포함 하 고 지정된 된 형식에 대해 등록 된 사용자 지정 serializer toobe 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="d4443-108">기본 제공 직렬 변환기</span><span class="sxs-lookup"><span data-stu-id="d4443-108">Built-in Serializers</span></span>

<span data-ttu-id="d4443-109">Reliable State Manager에는 일부 공용 형식에 대한 기본 제공 직렬 변환기가 포함되어 있으므로 기본적으로 해당 형식을 효율적으로 직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="d4443-110">다른 형식에 대 한 신뢰할 수 있는 상태 관리자가 대체 toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="d4443-111">기본 제공 serializer가 해당 유형을 변경할 수 없습니다 및 해당 형식 이름이 같은 hello 유형에 대 한 tooinclude 정보 필요 하지 않은 것을 알 수 있으므로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="d4443-112">Reliable State Manager에는 다음 형식에 대한 기본 제공 직렬 변환기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="d4443-113">Guid</span><span class="sxs-lookup"><span data-stu-id="d4443-113">Guid</span></span>
- <span data-ttu-id="d4443-114">bool</span><span class="sxs-lookup"><span data-stu-id="d4443-114">bool</span></span>
- <span data-ttu-id="d4443-115">byte</span><span class="sxs-lookup"><span data-stu-id="d4443-115">byte</span></span>
- <span data-ttu-id="d4443-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="d4443-116">sbyte</span></span>
- <span data-ttu-id="d4443-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="d4443-117">byte[]</span></span>
- <span data-ttu-id="d4443-118">char</span><span class="sxs-lookup"><span data-stu-id="d4443-118">char</span></span>
- <span data-ttu-id="d4443-119">string</span><span class="sxs-lookup"><span data-stu-id="d4443-119">string</span></span>
- <span data-ttu-id="d4443-120">decimal</span><span class="sxs-lookup"><span data-stu-id="d4443-120">decimal</span></span>
- <span data-ttu-id="d4443-121">double</span><span class="sxs-lookup"><span data-stu-id="d4443-121">double</span></span>
- <span data-ttu-id="d4443-122">float</span><span class="sxs-lookup"><span data-stu-id="d4443-122">float</span></span>
- <span data-ttu-id="d4443-123">int</span><span class="sxs-lookup"><span data-stu-id="d4443-123">int</span></span>
- <span data-ttu-id="d4443-124">uint</span><span class="sxs-lookup"><span data-stu-id="d4443-124">uint</span></span>
- <span data-ttu-id="d4443-125">long</span><span class="sxs-lookup"><span data-stu-id="d4443-125">long</span></span>
- <span data-ttu-id="d4443-126">ulong</span><span class="sxs-lookup"><span data-stu-id="d4443-126">ulong</span></span>
- <span data-ttu-id="d4443-127">short</span><span class="sxs-lookup"><span data-stu-id="d4443-127">short</span></span>
- <span data-ttu-id="d4443-128">ushort</span><span class="sxs-lookup"><span data-stu-id="d4443-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="d4443-129">사용자 지정 serialization</span><span class="sxs-lookup"><span data-stu-id="d4443-129">Custom Serialization</span></span>

<span data-ttu-id="d4443-130">사용자 지정 serializer는 hello 유선으로 및 디스크에서 자주 사용 되는 tooincrease 성능 또는 tooencrypt hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="d4443-131">Hello 유형에 대 한 정보 tooserialize 않아도 이후 다른 이유로 사용자 지정 serializer는 일반적으로 제네릭 serializer 보다 더 효율적 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="d4443-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) tooregister 사용 되는 지정 된 유형의 화 hello에 대 한 사용자 지정 serializer는 이 등록 동작 hello StatefulServiceBase tooensure의 hello 건설에서 복구가 시작 되기 전에 모든 신뢰할 수 있는 컬렉션 한지 toohello 관련 serializer tooread 지속형된 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="d4443-133">사용자 지정 직렬 변환기가 기본 제공 직렬 변환기보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="d4443-134">예를 들어 int에 대 한 사용자 지정 serializer는 등록 된 경우에 int hello 기본 제공 serializer가 대신 사용 되는 tooserialize 정수</span><span class="sxs-lookup"><span data-stu-id="d4443-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="d4443-135">어떻게 tooimplement 사용자 지정 serializer</span><span class="sxs-lookup"><span data-stu-id="d4443-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="d4443-136">사용자 지정 serializer 필요한 tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="d4443-137">IStateSerializer<T>에는 기준 값이라는 추가 T를 사용하는 쓰기 및 읽기 오버로드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="d4443-138">이 API는 차등 serialization에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-138">This API is for differential serialization.</span></span> <span data-ttu-id="d4443-139">현재 차등 serialization 기능은 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="d4443-140">따라서 이러한 두 오버로드는 차등 serialization이 노출되고 사용될 때까지 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="d4443-141">다음은 4가지 속성을 포함하는 OrderKey라는 사용자 지정 형식 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="d4443-142">다음은 IStateSerializer<OrderKey>의 구현 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="d4443-143">baseValue를 사용하는 읽기 및 쓰기 오버로드는 이후 버전과의 호환성을 위해 해당 오버로드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="d4443-144">업그레이드 가능성</span><span class="sxs-lookup"><span data-stu-id="d4443-144">Upgradability</span></span>
<span data-ttu-id="d4443-145">에 [롤링 응용 프로그램 업그레이드](service-fabric-application-upgrade.md), hello 업그레이드가 적용된 tooa 노드의 하위 집합을 한 번에 하나의 업그레이드 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="d4443-146">이 과정에서 몇 가지 업그레이드 도메인을 hello 최신 버전의 응용 프로그램에 되며 hello 이전 버전의 응용 프로그램에 몇 가지 업그레이드 도메인이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="d4443-147">Hello 롤아웃 중 hello 새 버전의 응용 프로그램, 데이터의 수 tooread hello 이전 버전 이어야 합니다. 및 hello 이전 버전의 응용 프로그램 수 tooread hello 새 버전의 데이터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="d4443-148">Hello 데이터 형식이 앞 이나 뒤로 hello 업그레이드가 호환 되지 않는 경우 수 실패, 또는 데이터 있습니다 수 손실 또는 손상 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="d4443-149">기본 제공 serializer를 사용 하는 경우에 tooworry 호환성에 대 한를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="d4443-150">그러나 사용자 지정 직렬 변환기 또는 DataContractSerializer hello를 사용 하는 경우 hello 데이터 toobe 뒤로 무한히 있고 호환 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="d4443-151">즉, serializer의 각 버전 toobe 수 tooserialize 하며 모든 버전의 hello 형식 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="d4443-152">데이터 계약 사용자 추가, 제거 및 필드를 변경에 대 한 hello 잘 정의 된 버전 관리 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="d4443-153">또한 데이터 계약에는 알 수 없는 필드를 다루는 hello serialization 및 deserialization 프로세스에 연결 하 고 클래스 상속을 다루는 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="d4443-154">자세한 내용은 [데이터 계약 사용](https://msdn.microsoft.com/library/ms733127.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4443-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="d4443-155">사용자가 사용자 지정 serializer는 이전 버전과 호환이 있고 있는지 toomake를 사용 하는 hello serializer의 toohello 지침을 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="d4443-156">모든 버전을 지 원하는 일반적인 방법은 hello 처음과 선택적으로 속성을 추가 크기 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="d4443-157">이러한 방식으로 각 버전 hello 스트림의 hello 남은 부분으로 이동 하 고 수 만큼 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4443-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4443-158">Next steps</span></span>
  * [<span data-ttu-id="d4443-159">serialization 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="d4443-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="d4443-160">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="d4443-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="d4443-161">[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="d4443-162">[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="d4443-163">[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="d4443-164">Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="d4443-165">toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4443-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
