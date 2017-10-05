---
title: "Azure 모바일 계약 내에서 이모지 이모티콘 사용"
description: "푸시 알림 내에서 이모지 이모티콘을 사용하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="219ab-103">푸시 알림 내에서 이모지 이모티콘 사용</span><span class="sxs-lookup"><span data-stu-id="219ab-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="219ab-104">다음과 같은 쉬운 몇 가지 단계를 통해 푸시 알림에 이모지 이모티콘을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="219ab-105">먼저 메시지에서 보낼 이모지를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="219ab-106">장치 제조업체에서 새로 승인한 이모지를 장치 플랫폼에 추가하려면 다소 시간이 걸리므로 선택하는 이모지를 대상 장치에서 지원할지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="219ab-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="219ab-107">**Windows** 에서 이 [링크](http://apps.timwhitlock.info/emoji/tables/unicode) 를 탐색하고 ‘네이티브' 아이콘을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="219ab-108">**Mac**에서 편집 -> 이모지 및 기호 아래의 사전 응용 프로그램에서 이모지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="219ab-109">이제 Azure Mobile Engagement 포털에서 **Reach** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="219ab-110">푸시 알림 유형(공지, 설문 조사 등)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="219ab-111">이 예제에서는 공지 푸시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="219ab-112">알림 텍스트에 도달할 때까지 여러 알림 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="219ab-113">이 위치에서 이모지 이모티콘을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="219ab-114">제목, 메시지 또는 두 항목 모두에 이모티콘을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="219ab-115">위의 위치에서 찾은 이모지를 끌어서 놓거나 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="219ab-116">알림에 대한 다른 필드를 완료하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="219ab-117">테스트를 실행하거나 공지를 활성화할 때 지정된 대로 이모티콘이 있는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="219ab-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="219ab-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="219ab-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

