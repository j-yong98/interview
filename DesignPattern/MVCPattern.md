MVC 패턴
=
MVC 패턴이란?
-
- MVC 패턴은 모델(Model), 뷰(View), 컨트롤러(Controller)로 이루어진 디자인 패턴입니다.
- 애플리케이션의 역할을 세 가지로 구분하여 개발 프로세스에서 각각의 구성 요소에만 집중해서 개발을 할 수 있습니다.
- 재사용성과 확장성이 용이하다는 장점이 있다.
- 애플리케이션이 복잡해질수록 모델과 뷰의 관계가 복잡해지는 단점이 있다.

모델
-
- 모델은 애플리케이션의 데이터인 데이터베이스, 상수, 변수 등을 뜻합니다.
- 뷰에서 데이터를 생성하거나 수정하면 컨트롤러를 통해 모델을 생성하거나 갱신합니다.

뷰
-
- inputbox, checkbox, testarea 등 사용자 인터페이스 요소를 나타냅니다.
- 모델을 기반으로 사용자가 볼 수 있는 화면을 뜻합니다.
- 모델이 가지고 있는 정보를 따로 저장하지 않아야 하며 단순히 사각형 모양 등 화면에 표시하는 정보만 가지고 있어야 합니다.
- 변경이 일어나면 컨트롤러에 이를 전달해야 합니다.

컨트롤러
-
- 컨트롤러는 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 합니다.
- 이벤트 등 메인 로직을 담당합니다.
- 모델과 뷰의 생명주기를 관리하며, 모델이나 뷰의 변경 통지를 받으면 이를 해석하여 각각의 구성 요소에 해당 내용을 알려줍니다.