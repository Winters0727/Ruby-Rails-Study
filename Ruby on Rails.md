# Ruby on Rails

### Install rails

```bash
$ gem install rails
$ rails --version
$ rails new blog
$ cd blog
```

레일즈 프로젝트를 설치하면 다음과 같은 파일 및 폴더들이 생성된다.

|      **파일/폴더**      |                           **목적**                           |
| :---------------------: | :----------------------------------------------------------: |
|          app/           | 애플리케이션을 위한 models, views, controllers, helpers, mailers, channels, jobs, assests를 포함하는 폴더. 대부분의 작업이 이 폴더에서 이루어진다. |
|          bin/           |  애플리케이션 작동을 위한 스크립트 파일들을 포함하는 폴더.   |
|         config/         |         라우트, 데이터베이스 등의 설정등이 담긴 폴더         |
|        config.ru        |     Rack기반의 서버를 시작하기위한 Rack 설정이 담긴 파일     |
|           db/           | 현재 데이터베이스의 스키마와 데이터베이스 마이그레이션에 대한 파일들을 포함하는 폴더. |
| Gemfile<br>Gemfile.lock | 레일즈 애플리케이션이 어떤 Gem 의존성을 갖는지 기록하는 파일들. 이 파일들은 나중에 Bundler gem에 의해 사용된다. |
|          lib/           |       애플리케이션을 확장하는 모듈들을 포함하는 폴더.        |
|          log/           |              애플리케이션 로그를 저장하는 폴더.              |
|      package.json       | npm(노드 패키지 매니저)의 의존성을 저장하는 파일. 이 파일은 Yarn에 의해 사용된다. |
|         public/         |        정적 파일들과 compiled assets를 포함하는 폴더.        |
|        Rakefile         | This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing `Rakefile`, you should add your own tasks by adding files to the `lib/tasks` directory of your application. |
|        README.md        | 레일즈 애플리케이션에 대한 정보를 간략하게 적는 매뉴얼 마크다운 파일. 이 매뉴얼 파일에는 프로젝트 설치 과정과 애플리케이션의 역할에 대한 설명이 적혀있어야 한다. |
|        storage/         | 디스크 서비스를 위한 Active Storage 파일들을 저장하는 폴더. Active Storage Overview를 참고하자. |
|          test/          | Unit tests, fixtures, and other test apparatus. These are covered in [Testing Rails Applications](https://guides.rubyonrails.org/testing.html). |
|          tmp/           |         캐시, pid 등의 임시 파일들을 저장하는 폴더.          |
|         vendor/         | 서드파티코드들을 저장하는 폴더. 일반적인 레일즈 프로젝트에서는 vendored gems를 포함한다. |
|       .gitignore        | github에 파일을 commit & push할 때 무시할 폴더 및 파일들을 저장하는 파일. |
|      .ruby-version      |              루비 버전에 대한 정보를 담는 파일.              |



### 웹 서버 가동

```bash
$ rails server

# 윈도우를 사용중이라면 스크립트 파일을 bin 폴더에 있는 루비 인터프리터에 직접적으로 보내야 한다.

$ ruby bin/rails server
```



### 레일즈 동작 원리

레일즈로 어떤 동작을 실행시키기 위해서는 최소한의 **controller**와 **view**가 필요하다.

**컨트롤러**의 목적은 애플리케이션을 위해 특정 요청을 받는 것이다. **라우팅**은 어떤 컨트롤러가 어떤 요청을 받는지 정의한다. 보통 각각의 컨트롤러는 하나 이상의 라우트를 가지며, 서로 다른 루트는 서로 다른 동작을 가진다. 각각의 동작이 갖는 목적은 정보를 취합하여 뷰에 전달하기 위한 것이다.

**뷰**의 목적은 동작으로 취합된 정보를 사용자가 읽을 수 있는 정보로 보여주는 것이다. 여기서 주의할 점은 정보를 취합하는 역할은 **컨트롤러**지 뷰가 아니다. 뷰는 단지 전달된 정보를 보여주는 역할만을 담당한다. 기본적으로 뷰 템플릿들은 eRuby(Embedded Ruby)라는 언어로 작성되는데, eRuby는 응답이 사용자에게 보내지기 전에 레일즈 내의 요청-응답 사이클을 진행시키는 템플릿 엔진이다.

![MVC](MVC.jpeg)

레일즈의 MVC 패턴을 그림으로 나타낸 것이다. 위 그림은 다음과 같은 프로세스를 가진다.

1. 사용자 브라우저로부터 "/users" URL에 대한 요청이 들어온다.
2. 레일즈에서 "/users#index" 라우트에 대한 동작은 User 컨트롤러에 있다.
3. "/users#index" 라우트에 대한 동작은 User 모델의 모든 유저들의 정보를 반환하는 것이다.(User.all) 
4. User 모델은 데이터베이스로부터 모든 유저들의 정보를 가져와 컨트롤러에 넘겨준다.
5. 컨트롤러는 넘겨받은 모든 유저들의 정보를 @users 라는 인스턴스 변수에 저장하여 "/users#index" URL에 해당하는 뷰에 넘겨준다.
6. 뷰는 eRuby(embedded Ruby) 언어를 통해 "/users" URL에 해당하는 템플릿(html) 페이지를 렌더링하여 컨트롤러에 넘겨준다.
7. 컨트롤러는 뷰에서 전달받은 HTML파일을 사용자 브라우저로 보낸다.

![ruby MVC example (1)](ruby MVC example (1).png)

출처 : https://medium.com/@matthewmain/rails-request-response-cycle-819e9cd8fa4e



### 컨트롤러 생성

새 컨트롤러를 생성하기 위해서 컨트롤러 생성기(Controller Generator)를 통해 컨트롤러와 동작을 정의하면 된다.

```bash
$ rails generate controller controller_name action_name
```

Welcome이라는 컨트롤러에 index라는 동작을 정의해보자.

```bash
$ rails generate controller Welcome index
```

그러면 레일즈가 다음과 같이 파일들을 생성한다.

```bash
create  app/controllers/welcome_controller.rb # 컨트롤러 생성
 route  get 'welcome/index' # 라우트 생성
invoke  erb # Embedded Ruby 실행
create    app/views/welcome # Controller의 View 폴더 생성
create    app/views/welcome/index.html.erb # Controller의 Action에 대한 View 템플릿 파일 생성
invoke  test_unit
create    test/controllers/welcome_controller_test.rb # Controller 테스트 파일 생성
invoke  helper
create    app/helpers/welcome_helper.rb # Controller 헬퍼 파일 생성
invoke    test_unit
invoke  assets
invoke    scss
create      app/assets/stylesheets/welcome.scss # 스타일을 위한 SCSS 파일 생성
```

생성된 파일 중 우리가 주목해야할 파일은 컨트롤러와 뷰에 해당하는 파일이다.

```bash
app/controllers/welcome_controller.rb # Controller
app/views/welcome/index.html.erb # View
```

생성된 뷰 파일에 다음과 같이 레일즈를 작성해본다.

```erb
<h1>Hello, Rails!</h1>
```



### 애플리케이션 홈페이지 설정

레일즈의 기본 루트 URL은 3000번 포트를 사용한다. (http://localhost:3000)

이제 실제 레일즈에 index 페이지의 위치를 알려줘야한다.

`config/routes.rb `파일을 참조하자.

```ruby
Rails.application.routes.draw do
  get 'welcome/index'
 
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

애플리케이션의 라우팅 파일은 특별한 도메인 특화 언어(Domain-Specific Language, DSL)을 포함하여 레일즈에게 들어온 요청에 대한 컨트롤러와 동작을 연결해준다.이 곳에 `root 'welcome#index'`를 추가해보자.

`root 'welcome#index'`는 레일즈에게 애플리케이션의 루트에 대한 요청을 Welcome 컨트롤러의 index 동작에 연결해주고, `get 'welcome/index'`는 레일즈에게 기본 루트 URL + /welcome/index 에 대한 요청을 Welcome 컨트롤러의 index 동작에 연결해준다.

라우팅에 관한 정보는 *https://guides.rubyonrails.org/routing.html* 을 참고하자.



### 애플리케이션 만들기

블로그 애플리케이션을 위해 자원을 만들 차례다. 여기서 자원이란 작은 객체들의 모음(Collection)을 의미한다. 자원을 통해 Create, Read, Update, Delete와 같은 CRUD 기능을 구현할 수 있다.

레일즈는 `resources` 메서드를 이용하여 기본적인 REST 자원을 선언할 수 있다. 다음과 같이 `config/routes.rb`에 article 자원을 추가해보자.

```ruby
Rails.application.routes.draw do
  get 'welcome/index'
  
  resources :articles
    
  root 'welcome#index'
end
```

CLI에 `rails routes`를 입력하면 기본적은 RESTful 동작에 대한 라우트가 정의되어있는 것을 볼 수 있다.

```bash
Prefix Verb   URI Pattern                                                                              Controller#Action
welcome_index GET    /welcome/index(.:format)                                                                 welcome#index
articles GET    /articles(.:format)                                                                      articles#index
POST   /articles(.:format)                                                                      articles#create
new_article GET    /articles/new(.:format)                                                                  articles#new
edit_article GET    /articles/:id/edit(.:format)                                                             articles#edit
article GET    /articles/:id(.:format)                                                                  articles#show
PATCH  /articles/:id(.:format)                                                                  articles#update
PUT    /articles/:id(.:format)                                                                  articles#update
DELETE /articles/:id(.:format)                                                                  articles#destroy
root GET    /                       
```

Article을 생성하기 위해 `articles/new` 라우트로 이동해보자. 해당 라우트로 이동하면 Routing Error가 발생한다.

이 에러는 요청에 따른 라우트에 대한 컨트롤러가 아직 정립되지 않았기 때문이다. (즉, Articles에 대한 라우트를 라우터에 등록했지만 해당 라우터를 처리할 컨트롤러가 존재하지 않는다.)

앞에서 배운 명령어를 이용하여 Articles 컨트롤러를 생성해주자.

```bash
$ rails g controller Articles
```

Articles 컨트롤러를 생성하면 `app/controllers/articles_controller.rb` 파일이 다음과 같이 생성된다.

```ruby
class ArticleController < ApplicationController
end
```

생성되는 컨트롤러는 모두 ApplicationController 클래스를 상속받는다. ApplicationController은 후에 컨트롤러를 위한 동작들을 정의할 메서드들을 포함한다. 여기서 메서드들은 추후에 구현할 CRUD에 관련된 동작들을 위한 메서드들을 의미한다.

컨트롤러를 정의했으니 다시 `articles/new` 라우트로 이동해보자. 이번에는 Unknown action 에러가 발생한다.

이는 컨트롤러를 정의했으나, 해당 라우트에 대한 동작을 정의하지 않았기 때문이다. 컨트롤러 파일 내부에 new 라우트에 대한 동작 new를 정의해주어야 한다.

```ruby
class ArticleController < ApplicationController
  def new
  end
end
```

여기서 new 메서드는 new 라우트에 대한 동작을 정의한다. 이제 다시 `articles/new` 라우트로 돌아가보자.

이번에는 No template 에러가 발생한다. 라우트에 대한 컨트롤러와 동작을 정의했으나, 뷰를 정의하지 않아 컨트롤러로부터 받은 정보를 보여줄 템플릿 파일이 존재하지 않기 때문이다.

에러메세지를 자세히 보면 다음과 같다.

```
ArticlesController#new은 요청 포맷(text/html)에 대한 템플릿이 존재하지 않습니다.

주의! 레일즈는 컨트롤러 이름으로 생성된 폴더에 라우트와 같은 이름의 템플릿이 있을거라고 예상합니다. 만약에 컨트롤러가 템플릿을 필요로 하지 않는 API로 204(No Content) 에러를 발생시킨다면 브라우저에 의한 에러(HTML 파일 요청)이니 무시하고 진행하면 됩니다. 
```

이 메세지는 레일즈가 먼저 어떤 템플릿을 찾는지를 보여준다. 이 경우, 라우트에 해당하는 `articles/new`에 해당하는 템플릿을 먼저 찾는다. 만약, `articles/new`에 해당하는 템플릿을 찾지 못했다면 레일즈는 `application/new`에 해당하는 템플릿을 찾는다. 이는 모든 컨트롤러는 ApplicationController를 상속받기 때문이다. (즉, 상속받은 상위 컨트롤러 클래스의 템플릿을 참조한다는 것이다.)