---
title: "Xamarin에서 Blob 저장소를 사용하는 방법 | Microsoft Docs"
description: "Xamarin용 Azure Storage 클라이언트 라이브러리를 사용하면 개발자들이 기본 사용자 인터페이스를 가진 iOS, Android 및 Windows Store 앱을 만들 수 있습니다. 이 자습서에서는 Xamarin을 사용하여 Azure Blob 저장소를 사용하는 응용 프로그램을 만드는 방법을 설명합니다."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 5ff4d86082c03dcd7098743a984a97aa70232d1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="1da9b-104">Xamarin에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1da9b-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="1da9b-105">개요</span><span class="sxs-lookup"><span data-stu-id="1da9b-105">Overview</span></span>
<span data-ttu-id="1da9b-106">Xamarin을 사용하면 개발자들이 공유된 C# 코드베이스를 사용하여 기본 사용자 인터페이스를 가진 iOS, Android 및 Windows Store 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="1da9b-107">이 자습서는 Xamarin 응용 프로그램과 함께 Azure Blob 저장소를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="1da9b-108">Azure Storage에 대한 자세한 내용을 보려면 코드를 살펴보기 전에 [Microsoft Azure Storage 소개](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1da9b-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="1da9b-109">새 Xamarin 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1da9b-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="1da9b-110">이 자습서에서는 Android, iOS 및 Windows를 대상으로 하는 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="1da9b-111">이 앱은 단순히 컨테이너를 만들고 이 컨테이너에 blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="1da9b-112">Windows에서 Visual Studio를 사용하게 되지만 macOS에서 Xamarin Studio를 사용하여 앱을 만들 때도 동일한 방식을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="1da9b-113">다음 단계에 따라 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="1da9b-114">아직 하지 않은 경우 [Visual Studio용 Xamarin](https://www.xamarin.com/download)을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="1da9b-115">Visual Studio를 열고 [비어 있는 앱(네이티브 이식 가능)]을 만듭니다(**파일 > 새로 만들기 > 프로젝트 > 플랫폼 간 > 비어 있는 앱(네이티브 공유)**).</span><span class="sxs-lookup"><span data-stu-id="1da9b-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="1da9b-116">솔루션 탐색기 창에서 해당 솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션에 대한 NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="1da9b-117">**WindowsAzure.Storage** 를 검색하고 솔루션의 모든 프로젝트에 안정적인 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="1da9b-118">프로젝트를 빌드한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-118">Build and run your project.</span></span>

<span data-ttu-id="1da9b-119">이제 단추를 클릭하고 카운터를 증가시켜주는 응용 프로그램이 완료되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="1da9b-120">컨테이너 만들기 및 blob 업로드</span><span class="sxs-lookup"><span data-stu-id="1da9b-120">Create container and upload blob</span></span>
<span data-ttu-id="1da9b-121">다음으로 `(Portable)` 프로젝트에서 `MyClass.cs`에 일부 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="1da9b-122">이 코드는 컨테이너를 만들고 이 컨테이너에 Blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="1da9b-123">`MyClass.cs` 는 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-123">`MyClass.cs` should look like the following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="1da9b-124">"your_account_name_here" 및 "your_account_key_here"를 실제 계정 이름과 계정 키로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="1da9b-125">iOS, Android 및 Windows Phone 프로젝트에는 모두 이식 가능한 프로젝트에 대한 참조가 있으므로 모든 공유 코드를 한 곳에서 작성하고 이 코드를 모든 프로젝트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="1da9b-126">이제 각 프로젝트에 `MyClass.performBlobOperation()` 코드 줄을 추가하여 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="1da9b-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="1da9b-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="1da9b-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="1da9b-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading the view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="1da9b-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="1da9b-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-the-application"></a><span data-ttu-id="1da9b-130">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="1da9b-130">Run the application</span></span>
<span data-ttu-id="1da9b-131">이제 Android 또는 Windows Phone 에뮬레이터에서 이 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="1da9b-132">iOS 에뮬레이터에서 이 응용 프로그램을 실행할 수도 있지만 Mac이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="1da9b-133">이 작업을 수행하는 방법에 대한 특정 지침은 [Visual Studio를 Mac에 연결](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="1da9b-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="1da9b-134">앱을 일단 실행하면 저장소 계정에 컨테이너 `mycontainer` 가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="1da9b-135">여기에는 `Hello, world!` 텍스트를 포함하는 Blob `myblob`가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="1da9b-136">[Microsoft Azure Storage Explorer](http://storageexplorer.com/)를 사용하여 이 사실을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1da9b-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1da9b-137">Next steps</span></span>
<span data-ttu-id="1da9b-138">이 자습서에서는 특히 Blob Storage에서 한 시나리오에 초점을 맞춰서 Xamarin에서 Azure Storage를 사용하는 플랫폼 간 응용 프로그램을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="1da9b-139">그러나 Blob Storage 뿐만 아니라 Table, File 및 Queue Storage로도 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da9b-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="1da9b-140">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1da9b-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="1da9b-141">.NET을 사용하여 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="1da9b-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="1da9b-142">.NET을 사용하여 Azure 테이블 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="1da9b-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="1da9b-143">.NET을 사용하여 Azure 큐 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="1da9b-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="1da9b-144">Windows에서 Azure 파일 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="1da9b-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

