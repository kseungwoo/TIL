> Udemy  [iOS & Swift - The Complete iOS App Development Bootcamp](https://www.udemy.com/course/ios-13-app-development-bootcamp/) 강의를 듣고 정리하였습니다. 
>



# 클론 코딩 해보자

어떤 개발이든 처음에 입문하기 가장 효과적인 방법은 역시 클론 코딩이죠. 

I am rich라는 이름의 앱을 클론 코딩해봅시다. 이 앱은 정말 간단하고 가벼워요. $1000이라는 거금을 지불해야 설치할 수 있는 유료 앱이지만 실상 앱을 깔고 실행해보면 아래 화면이 전부인 앱이죠. 결국 이 앱은 애플에 의해 앱스토어에서 삭제되었답니다.

<img src="https://user-images.githubusercontent.com/71204049/145682715-2ea8b071-9749-4a0a-82e2-d890b4847746.png" width="200">

(출처: [LA Times](https://latimesblogs.latimes.com/technology/2008/08/iphone-i-am-ric.html))



그럼 시작해보시죠!



# 프로젝트 생성

<img src="https://user-images.githubusercontent.com/71204049/145682857-893028ff-2812-45b1-9e3c-cdc3afaa0a26.png" width="300">

Xcode를 실행하고

<img src="https://user-images.githubusercontent.com/71204049/145682891-188055a8-e6fa-458b-98c0-2453a54add9b.png" width="300">

새 프로젝트를 생성합니다.

<img src="https://user-images.githubusercontent.com/71204049/145682954-7762044b-7f00-4a82-9b64-6a8a63d87876.png" width="500">

iOS 플랫폼에서 App 템플릿을 선택합니다. 부가적인 기능이 포함되지 않은 가장 기본적인 템플릿이에요.

<img src="https://user-images.githubusercontent.com/71204049/145683346-9d833802-f651-47f5-af01-0eefceaeb660.png" width="500">

새로운 프로젝트의 옵션을 입력할 차례에요. 여기서 몇 가지 짚고 넘어가 봅시다.

- Product Name: 만들 앱의 이름이에요.
- Bundle Identifier: 앱스토어에 표시될 앱의 주소에요. 유일성이 보장돼요. 도메인 주소와는 반대로 적어요.
- Interface: SwiftUI와 Storyboard 두 가지 선택지가 있어요. Storyboard를 사용합니다.



마지막으로, 프로젝트가 저장될 디렉토리를 지정하고 나면

<img src="https://user-images.githubusercontent.com/71204049/145683410-a822e08c-e721-47b0-a37d-a627a79c3462.png" width="800"	>

프로젝트 생성이 완료되었습니다. 간단하죠?

아, 그리고 Xcode는 프로젝트의 모든 변동사항을 자동으로 저장합니다.

<img src="https://user-images.githubusercontent.com/71204049/145683536-6a78b0e2-418d-4c4d-96d3-66df3d87d3c6.png" width="400">

만약 Xcode를 종료한 후 프로젝트를 다시 열고 싶다면, 프로젝트를 저장한 디렉토리에서 .xcodeproj 확장자를 가진 파일을 열면 됩니다.





# Xcode 가이드 투어

프로젝트도 생성했으니, 이제 Xcode와 가까워지는 시간을 갖도록 합시다.

<img src="https://user-images.githubusercontent.com/71204049/145683728-324f0e46-6d16-4c5f-9354-4be2fae76928.png" width="500">



프로젝트를 실행하면 중앙에 가장 먼저 보이는 탭입니다. 

- identify: 프로젝트를 생성할 때 설정했던 앱 이름과 Bundle Identifier, 버전 등을 관리할 수 있어요.
- deployment info: 만들 앱이 어떻게 배포될지 관리해요. 언제 어디서 실행될 것인지, minimum iOS 버전 타겟(최소 타겟 iOS 버전 이상부터 이용 가능)을 설정합니다.
- Device Orientation: 앱의 화면 회전 가능 여부를 설정할 수 있어요. Portrait(정방향), Upside Down(위아래 역전), Landscape Left/Right(왼쪽, 오른쪽 90도 회전) 옵션이 있네요. 만약 앱이 회전되지 않길 바란다면 Portrait만 체크하시면 돼요.
- Status Bar Style: 상태 바 표시 관련 설정을 할 수 있네요.



개발 도중에 이 화면으로 돌아오고 싶다면 언제든지

<img src="https://user-images.githubusercontent.com/71204049/145683784-026ff29a-2a63-41da-a016-953328cd9010.png" width="300">

파란색으로 선택된 프로젝트의 가장 상위 파일을 클릭하시면 돌아올 수 있어요. 그 아래 하위 파일로 .swift 코드 파일 (AppDelegate, SceneDelegate,ViewController)과 .storyboard 디자인 파일(Main)이 있네요.



<img src="https://user-images.githubusercontent.com/71204049/145685848-429bfa34-33af-4c70-b8fc-c008baeefae2.png" width="800">

상단에는 상태바가 있습니다. 이곳에서는 앱을 실행할 디바이스를 선택하고, 플레이 버튼을 클릭하면 실행할 수 있어요.

<img src="https://user-images.githubusercontent.com/71204049/145685928-505e75b6-867e-452a-904f-6bbf4bd80480.png" width="300">

왼쪽에는 아까도 보았던 네비게이션 바가 있네요. 이 곳에서는 원하는 분류별로 프로젝트의 파일들을 탐색할 수 있어요.



<img src="https://user-images.githubusercontent.com/71204049/145686572-9ed7863c-cb4d-47b9-a762-a7a868c98a45.png" width="700">

이번엔 main.storyboard 파일을 열어보았습니다. 

중앙의 오른쪽 위에 보이는 +버튼을 이용하면 다양한 컴포넌트를 스크린에 추가할 수 있습니다. 전 Label 컴포넌트를 추가해보았는데요. 

오른쪽 탭은 인스펙터(inspector)라고 불리며, 현재 선택한 파일에 대해 세부적으로 설정할 수 있어요. 위에선 스토리보드 파일을 선택했으니 컴포넌트의 세부 디자인, 사이즈, 앱에서의 컴포넌트 위치 등을 설정할 수 있죠. 이건 앞으로 개발을 하면서 차차 알아갈거에요.

왼쪽 탭은 Document Outline인데, 여기선 디자인 파일의 모든 컴포넌트들을 보여줍니다.



<img src="https://user-images.githubusercontent.com/71204049/145686648-d559f910-c1d6-452a-8dc3-55500af6102c.png" width="400">

Debug Area에서는 앱에서 발생하는 충돌이나 앱이 어떻게 실행되고 있는지 파악할 수 있어요.



<img src="https://user-images.githubusercontent.com/71204049/145686957-2c47b360-6ded-4a11-8b08-051a06974e60.png" width="800">

(출처: [Udemy IOS 부트캠프](https://www.udemy.com/course/ios-13-app-development-bootcamp/))



종합해보면 Xcode Map은 이렇게 생겼어요. 



# 컴포넌트 수정

<img src="https://user-images.githubusercontent.com/71204049/145700668-c16ff1f2-ccdc-41e8-8b6a-78f7b0b6ea04.png" width="600">

간단하게 Label의 텍스트, 글자 크기, 글씨체, 글씨 색상을 변경하고, View의 색상도 변경해보고 imageView 컴포넌트도 추가해보았습니다.

컴포넌트를 수정할 때는 오른쪽의 Inspector Pane을 이용하면 됩니다.

<img src="https://user-images.githubusercontent.com/71204049/145700758-71bbcd18-ef36-4b38-9a8d-37c4a2543cde.png" width="300">

이렇게 원하는 색상을 Hex Color Code로 지정할 수도 있어요.

아래 사이트는 다양한 조합의 색상들을 Hex Code로 안내합니다.

https://colorhunt.co/



<img src="https://user-images.githubusercontent.com/71204049/145700793-b4173139-f1f0-4f4b-81fe-4c5f2cef413b.png" width="400">

크기(Width, Height)와 위치(X,Y)도 조절할 수 있답니다.

<img src="https://user-images.githubusercontent.com/71204049/145700856-8b942ec9-35a8-4377-a6e5-4d3cee698817.png" width="400">

위치를 나타낼 때는 왼쪽 상단 가장자리를 (0,0)으로 기준하고, 오른쪽으로 X축, 아래쪽으로 Y축입니다.



아이폰 기종별 크기는 아래 사이트에서 자세히 확인하실 수 있어요.

https://www.paintcodeapp.com/news/ultimate-guide-to-iphone-resolutions



Xcode에서 크기 및 위치를 지정하는 단위는 픽셀(Pixel)이 아닌 포인트(Point)에요.

- 픽셀: 디지털 화면을 구성하는 최소 단위입니다. 해상도를 나타낼 때 주로 쓰이고 상대적인 값이에요.
- 포인트: 1포인트는 1/72인치 (약 0.352mm) 입니다. 절대적인 값이에요.

기술이 발전할수록 동일한 크기의 화면에 더 많은 픽셀을 담게 되는데, 이러한 픽셀 수를 기준한다면 해상도가 높은 기기에선 같은 디스플레이 면적의 픽셀 수가 더 늘어나기 때문에 의도한 것 보다 작게 보일 수 있어요.

따라서 우리는 절대적인 값인 포인트를 사용한답니다.



# 이미지 삽입

이제 imageView에 이미지를 삽입해보겠습니다. 먼저 삽입할 이미지를 Assets에 추가해야해요.

<img src="https://user-images.githubusercontent.com/71204049/145701653-f3abf765-d2a7-42c4-b373-e861b9a1b715.png" width="800">

이렇게 말이죠. 여기서 1x 2x 3x 동일한 세개의 이미지가 보이시나요?

<img src="https://user-images.githubusercontent.com/71204049/145701712-11792792-dbd1-4519-9ee6-78696986f5ac.png" width="800">

(출처: [blog.fluidui](https://blog.fluidui.com/designing-for-mobile-101-pixels-points-and-resolutions/))

- 1x: 1포인트당 1개의 픽셀
- 2x: 1포인트당 4개의 픽셀
- 3x: 1포인트당 9개의 픽셀

이전에도 말씀드렸지만, 디스플레이 해상도가 날이 갈수록 발전하면서 하나의 포인트에 더 많은 픽셀을 담을 수 있게 되었어요. 이에 따라 우리는 다양한 기기를 사용하는 사용자들에게 매끄러운 이미지를 제공하기 위해서 동일한 이미지를 1x, 2x, 3x로 나누어서 모두 제공해야 해요.

https://appicon.co/#image-sets

위 사이트를 이용하면 쉽고 간단하게 1x, 2x, 3x 이미지를 생성할 수 있어요!

<img src="https://user-images.githubusercontent.com/71204049/145701803-bef350c3-4cfe-40a3-900c-b3a64f96dac0.png" width="300">

이렇게 이미지를 imageView 컴포넌트에 넣어주었습니다.



# AppIcon 등록

마지막으로 AppIcon을 등록할게요.

<img src="https://user-images.githubusercontent.com/71204049/145701882-70d219de-788b-4bd0-af83-0fab45d6977a.png" widt="500">

와우.. 보이시나요? 하나의 앱 아이콘을 이렇게 다양한 픽셀과 포인트당 픽셀로 제공해야하네요. 이렇게 여러 차원에서 제공하는 이미지들은 앱스토어, 앱 알림, 스포트라이트, 세팅 등 다양한 상황에서 앱을 상징해주는 이미지로 쓰일거에요. 

여기서 한 가지 의문이 들 수 있어요. "하나의 높은 해상도 이미지만 제공해주면 iOS가 찰떡같이 상황에 맞게 이미지를 조정해서 사용자에게 보여주면 안될까? 너무 번거로워!"

맞아요. 개발자 입장에서 번거로운 일이고 높은 해상도의 이미지 하나를 제공해주면 iOS가 필요에 따라 이미지를 Scale down해서 보여주면 간단하겠네요. 그러나 매번 상황에 따라 이미지를 Scale down하는 작업은 앱의 성능을 저하시키고 속도를 느리게 할 거에요. 앱 입장에서는 매번 이미지를 변환하는 것보단 변환되어있는 이미지를 바로 쓰는게 편하겠죠. 유저의 사용성을 고려할 때 앱의 성능과 속도는 중요합니다.

https://www.canva.com/ 에서 이렇게

<img src="https://user-images.githubusercontent.com/71204049/145702280-43ea738e-e29e-432c-b77a-bf609767b563.png" width="700">

나만의 앱 아이콘을 만들고



https://appicon.co/#app-icon

위 사이트에서 1024x1024 앱 아이콘 이미지를 입력하면 모든 플랫폼을 위해 필요한 이미지들을 추출할 수 있어요. 

<img src="https://user-images.githubusercontent.com/71204049/145702377-015916ed-f155-4e8d-b03c-4b9c35e2d014.png" width="400">

다운받은 압축 파일을 풀면 이런 모습입니다. 디렉토리 명까지 프로젝트와 동일하네요! 그대로 프로젝트의 Assets.xcassets에 복붙해주면 됩니다.

<img src="https://user-images.githubusercontent.com/71204049/145702441-40c890af-d91f-48a7-a798-2b4647899c99.png" width="400">

세상 편하네요!!



# 앱 실행하기

<img src="https://user-images.githubusercontent.com/71204049/145702632-c2795d56-4ff1-407c-8e80-e95cffe64849.png" width="300">

iOS 시뮬레이터로 실행한 모습이에요! 다른 기종으로 실행하였을 때는 레이아웃이 잘리거나 맞지 않을 수 있는데 이는 스크린 크기에 관계없이 일관되게 디자인을 보여줄 수 있는 방법(Auto Layout과 Setting constraints)에 대해 배우면서 개선해나갈거에요.

