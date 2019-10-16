<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="80093-101">Este tutorial le enseña a crear una aplicación nativa reAct que use la API de Microsoft Graph para recuperar la información de calendario de un usuario.</span><span class="sxs-lookup"><span data-stu-id="80093-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="80093-102">Si prefiere descargar solo el tutorial completo, puede descargar o clonar el repositorio de [GitHub](https://github.com/microsoftgraph/msgraph-training-react-native).</span><span class="sxs-lookup"><span data-stu-id="80093-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80093-103">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80093-103">Prerequisites</span></span>

<span data-ttu-id="80093-104">Antes de iniciar este tutorial, debe tener instalado lo siguiente en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="80093-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="80093-105">Al menos uno de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="80093-105">At least one of the following:</span></span>
  - <span data-ttu-id="80093-106">Kit de desarrollo de [Android Studio](https://developer.android.com/studio/) **y** [Java](https://jdk.java.net) (necesario para ejecutar el ejemplo en Android)</span><span class="sxs-lookup"><span data-stu-id="80093-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="80093-107">[Xcode](https://developer.apple.com/xcode/) (necesario para ejecutar el ejemplo en iOS)</span><span class="sxs-lookup"><span data-stu-id="80093-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="80093-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="80093-108">Node.js</span></span>](https://nodejs.org)

> [!NOTE]
> <span data-ttu-id="80093-109">Este tutorial se ha escrito con reaccionar la CLI nativa, que tiene requisitos previos específicos según el sistema operativo y las plataformas de destino.</span><span class="sxs-lookup"><span data-stu-id="80093-109">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="80093-110">Consulte [reaccionar nativo de introducción](https://facebook.github.io/react-native/docs/getting-started) para obtener instrucciones sobre cómo configurar el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="80093-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="80093-111">A continuación se enumeran las versiones usadas para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="80093-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="80093-112">Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.</span><span class="sxs-lookup"><span data-stu-id="80093-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="80093-113">Android Studio versión 3.4.2 con 1.8.0 JRE y el SDK de Android 9,0</span><span class="sxs-lookup"><span data-stu-id="80093-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="80093-114">Kit de desarrollo de Java versión 12.0.2</span><span class="sxs-lookup"><span data-stu-id="80093-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="80093-115">Versión 10,3 de Xcode</span><span class="sxs-lookup"><span data-stu-id="80093-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="80093-116">Node. js versión 10.16.0</span><span class="sxs-lookup"><span data-stu-id="80093-116">Node.js version 10.16.0</span></span>

## <a name="feedback"></a><span data-ttu-id="80093-117">Comentarios</span><span class="sxs-lookup"><span data-stu-id="80093-117">Feedback</span></span>

<span data-ttu-id="80093-118">Envíe sus comentarios sobre este tutorial en el [repositorio de github](https://github.com/microsoftgraph/msgraph-training-react-native).</span><span class="sxs-lookup"><span data-stu-id="80093-118">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
