# 면접을 위한 Ruby & Ruby on Rails 공부 기록

- 11월 20일 : Ruby, Ruby on Rails 기본 마크다운 생성, Ruby 공부
- 11월 21일 : Ruby on Rails를 이용한 CRU 기능 공부
- 11월 22일 : 
- 11월 23일 :
- 11월 24일 : 
- 11월 25일 : 
- 11월 26일 :  



## 루비

### 마크다운

- [Ruby from FreeCodeCamp](Ruby.md) / 출처 : https://www.youtube.com/watch?v=t_ispmWmdjY
- [Ruby-style-guide](https://github.com/dalzony/ruby-style-guide/blob/master/README-koKR.md)



## 루비 온 레일즈

### 레일즈란?

레일즈는 MVC(Model-View-Controller) 패턴을 따르는 루비로 작성된 웹 애플리케이션 프레임워크다. MVC 패턴은 레일즈를 이해하는 핵심으로, 모델층, 컨트롤러층, 뷰층은 각각의 업무를 담당한다.



### 모델층(Model Layer)

모델층은 도메인 모델로부터 정보를 제공하거나 애플리케이션의 특정 비즈니스 로직을 캡슐화하는 역할을 담당한다. 레일즈에서 데이터베이스에 저장되는 모델 클래스들은 `ActiveRecord::Base`를 상속받는다. Active Record는 데이터베이스로부터 가져온 데이터를 객체로 제공하거나 비즈니스 로직에 의해 적절히 가공된 데이터 객체를 제공한다. 레일즈의 모델들은 데이터베이스에 의해 정의되지만,  기본 루비 클래스로 모델을 정의하거나 Active Record 모듈에서 제공하는 인터페이스들을 적용한 루비 클래스가 될 수도 있다.



### 컨트롤러층(Controller Layer)

컨트롤러층은 들어온 HTTP 요청에 대해 적절한 반응을 제공하는 역할을 한다. 일반적으로 HTML 파일을 반환하지만, 레일즈 컨트롤러는 경우에 따라 XML, JSON, PDF 등의 파일도 제공한다. 컨트롤러는 모델에 적절한 요청을 보내어 데이터베이스로부터 정보를 받고, 이를 뷰를 통해 렌더링하여 적절한 형태의 HTTP 반응을 생성한다. 레일즈에서는 HTTP 요청은 경로에 따라 Action Dispatch에 의해 적절한 컨트롤러에 배치된다. 이 때 컨트롤러 클래스는 `ActionController::Base`를 상속받는다. Action Dispatch와 Action Controller는 Action Pack으로 번들링되어 있다.



### 뷰층(View Layer)

뷰층은 애플리케이션 자원을 적절한 형태로 제공해주는 "템플릿"으로 구성되어 있다. 템플릿 파일은 다양한 포맷을 지원하는데, 대부분의 템플릿은 ERB(Embedded Ruby) 엔진으로 작성된 HTML 포맷의 템플릿 파일로 작성된다. 뷰의 생성에는 Action View가 관여한다.



출처 : https://github.com/rails/rails/tree/v6.0.3.4

### 마크다운

- [Ruby on Rails Tutorial](Ruby on Rails.md) / 출처 : https://guides.rubyonrails.org/getting_started.html#creating-a-new-rails-project
- [Ruby on Rails - API](Ruby on Rails - API.md) / 출처 : https://guides.rubyonrails.org/api_app.html
- [Ruby on Rails - Route](Ruby on Rails - Route.md) / 출처 : https://guides.rubyonrails.org/routing.html
- [Ruby on Rails from FreeCodeCamp](Ruby on Rails - full course.md) / 출처 : https://www.youtube.com/watch?v=fmyvWz5TUWg
- [Ruby on Rails-style-guide](https://github.com/pureugong/rails-style-guide/blob/master/README-koKR.md#activerecord)

