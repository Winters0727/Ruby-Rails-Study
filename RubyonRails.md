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

![MVC](./Rails Picture/MVC.jpeg)

레일즈의 MVC 패턴을 그림으로 나타낸 것이다. 위 그림은 다음과 같은 프로세스를 가진다.

1. 사용자 브라우저로부터 "/users" URL에 대한 요청이 들어온다.
2. 레일즈에서 "/users#index" 라우트에 대한 동작은 User 컨트롤러에 있다.
3. "/users#index" 라우트에 대한 동작은 User 모델의 모든 유저들의 정보를 반환하는 것이다.(User.all) 
4. User 모델은 데이터베이스로부터 모든 유저들의 정보를 가져와 컨트롤러에 넘겨준다.
5. 컨트롤러는 넘겨받은 모든 유저들의 정보를 @users 라는 인스턴스 변수에 저장하여 "/users#index" URL에 해당하는 뷰에 넘겨준다.
6. 뷰는 eRuby(embedded Ruby) 언어를 통해 "/users" URL에 해당하는 템플릿(html) 페이지를 렌더링하여 컨트롤러에 넘겨준다.
7. 컨트롤러는 뷰에서 전달받은 HTML파일을 사용자 브라우저로 보낸다.

![ruby MVC example (1)](./Rails Picture/ruby-MVC-example-(1).png)

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

#### 기본 라우트 설정

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



#### 컨트롤러 생성

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



#### 동작(Action) 설정

컨트롤러를 정의했으니 다시 `articles/new` 라우트로 이동해보자. 이번에는 Unknown action 에러가 발생한다.

이는 컨트롤러를 정의했으나, 해당 라우트에 대한 동작을 정의하지 않았기 때문이다. 컨트롤러 파일 내부에 new 라우트에 대한 동작 new를 정의해주어야 한다.

```ruby
class ArticleController < ApplicationController
  def new
  end
end
```

여기서 new 메서드는 new 라우트에 대한 동작을 정의한다. 이제 다시 `articles/new` 라우트로 돌아가보자.



#### 템플릿 파일 생성

이번에는 No template 에러가 발생한다. 라우트에 대한 컨트롤러와 동작을 정의했으나, 뷰를 정의하지 않아 컨트롤러로부터 받은 정보를 보여줄 템플릿 파일이 존재하지 않기 때문이다.

에러메세지를 자세히 보면 다음과 같다.

```
ArticlesController#new은 요청 포맷(text/html)에 대한 템플릿이 존재하지 않습니다.

주의! 레일즈는 컨트롤러 이름으로 생성된 폴더에 라우트와 같은 이름의 템플릿이 있을거라고 예상합니다. 만약에 컨트롤러가 템플릿을 필요로 하지 않는 API로 204(No Content) 에러를 발생시킨다면 브라우저에 의한 에러(HTML 파일 요청)이니 무시하고 진행하면 됩니다. 
```

이 메세지는 레일즈가 먼저 어떤 템플릿을 찾는지를 보여준다. 이 경우, 라우트에 해당하는 `articles/new`에 해당하는 템플릿을 먼저 찾는다. 만약, `articles/new`에 해당하는 템플릿을 찾지 못했다면 레일즈는 `application/new`에 해당하는 템플릿을 찾는다. 이는 모든 컨트롤러는 ApplicationController를 상속받기 때문이다. (즉, 상속받은 상위 컨트롤러 클래스의 템플릿을 참조한다는 것이다.)

그 다음으로 요청 템플릿의 포맷에 대한 응답이 메세지의 `request.formats`에 정의되어 있다. 브라우저에서 `text/html` 포맷을 요구했으므로 레일즈에서는 HTML 템플릿을 찾는다.

이 에러를 가장 쉽게 해결하는 방법은 해당 라우트에 대한 뷰 폴더 안에 라우트와 같은 이름의 템플릿 파일을 생성해주면 된다. (`app/view/articles/new.html.erb`)

위의 뷰 경로를 보면 파일 이름이 동작의 이름과 템플릿 파일의 포맷 형태, 그리고 템플릿 파일 빌더로 정해진다는 사실을 알 수 있다. `app/view/articles/new.html.erb` 파일의 경우, articles 컨트롤러의 new라는 동작에대해 HTML 포맷의 ERB 빌더 언어로 작성된 템플릿 파일임을 알 수 있다. 레일즈는 HTML 파일 외에도 많은 포맷을 지원하지만, 기본 설정은 HTML 포맷의 ERB 빌더다.

생성된 파일이 보이도록 다음과 같이 작성해보자.

```erb
<h1>New Articles</h1>
```

이제 `articles/new` 경로로 들어가면 에러 없이 정상적으로 New Articles라는 글이 보일 것이다.



#### 폼 설정

이번에는 폼 빌더를 활용하여 템플릿에 폼을 생성해보자. 레일즈는 기본적으로 제공하는 폼 빌더 헬퍼 메서드로 `form_with`를 제공한다. 이 메서드를 활용하여 위에서 생성한 템플릿 파일에 폼을 생성해보자.

```erb
<h1>New Articles</h1>
<%= form_with scope: :article, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

여기서 ERB의 블록에 대해서 정리해볼 필요가 있다.

- `<% %>` : 블록 내의 루비 코드를 실행하지만 값을 반환하지 않는다.
- `<%= %>` : 블록 내의 루비 코드를 실행하고 특정 값을 반환한다.
- `<%== %>` : `<%= raw %>`
- `<%# %>` : 블록 내에 작성된 내용을 주석처리한다.
- `%` : 한줄짜리 루비코드로 `<% %>`와 같은 역할을 한다.
- `%%` : 첫번째 %는 그대로 사용하고, 두번째 %는 이후의 루비 코드를 실행한다.
- `<%%` or `%%>` : 각각을 `<%`, `%>`로 대체한다.

먼저 `form_with`를 호출하면 폼을 위한 스코프를 정의해주어야한다. 이 경우에는 심볼 클래스의 `:article`로 정의했다. 이는 `form_with` 헬퍼에게 이 폼이 어떤 것을 위한 폼인지 정의해주는 역할을 한다. 블록 스코프 내의 `form`으로 정의된 `FormBuilder` 객체로 레이블과 텍스트 필드를 정의한다. 마지막으로 `form` 객체의 `submit` 메서드를 불러 제출 버튼을 생성해준다.

여기서 문제가 하나 발생하는데, 현재 폼의 동작 속성이 동일한 URL인 `articles/new`이기 때문이다. 문제가 되는 이유는 폼을 제출하여 동일한 라우트로 다시 이동할 때 새로 생성된 article을 보여주어야하기 때문이다.

따라서 폼을 제출할 때 다른 URL로 보낼 필요가 있다. 이는 `form_with`의 옵션인 `:url`을 사용하여 구현할 수 있다. 일반적으로 레일즈에서는 새로운 폼의 제출을 위한 동작을 "create"로 정의한다.

```erb
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
```

`url` 옵션의 값을 `articles_path`로 설정했다. 이는 앞에서 `config/route.rb`에 article에 대한 자원을 정의했었는데, 이 과정에서 articles에 대한 CRUD 라우트가 생성되었기 때문이다. 이는 앞에서 `rails routes` 라는 명령어로 확인했었다.

`articles_path` 헬퍼는 `articles` 접두사가 붙은 URI 패턴 중에 적절한 폼을 레일즈에게 알려준다. 그리고 폼은 자동으로 해당 라우트로 `POST` 요청을 보내게 된다. 이는 현 컨트롤러인 `ArticlesController`의 `create` 동작과 관련이 있다.

폼과 관련된 라우트가 정의되었으니 폼을 작성하여 제출함으로써 새로운 article를 생성할 수 있게 되었다. 하지만, 폼을 제출하면 Unknow action 에러가 발생하게 된다.

이는 `ArticlesController`에 `create` 동작이 정의되어 있지 않기 때문이다. 앞에서 했던 것처럼 컨트롤러에 동작을 정의해주자.

```ruby
class ArticlesController < ApplicationController
  def new
  end
  
  def create
  end
end
```

이 상태에서 다시 제출 버튼을 누르면 아무런 변화가 없고, `204 No Content` 에러가 발생한다. 이는 `create` 동작에 대한 리턴 값이 없기 때문이다. `create` 동작에 대한 리턴 값을 추가하여 데이터베이스에 저장시키면 에러가 해결된다.

```ruby
def create
  render plain: params[:article].inspect
end
```

`render` 메서드는 간단한 hash로 `:plain`이라는 키와 `params[:article].inspect`라는 값을 갖는다. `params` 메서드는 폼으로부터 전달된 정보를 파라미터를 보여주는 객체다. `params`는 `ActionController::Parameter` 객체를 반환하는데, 해당 객체에 접근하기 위해서는 String이나 Symbol을 키로 넣어줘야한다.

다시 제출을 한다면 다음과 같은 메세지를 볼 수 있다.

```html
<ActionController::Parameters {"title"=>"First Article!", "text"=>"This is my first article."} permitted: false>
```

이제 동작은 폼으로부터 들어온 정보로부터 파라미터를 보여준다.



#### 모델 생성하기

레일즈에서 모델의 이름은 단수형이고, 그에 상응하는 데이터베이스 테이블들의 이름은 복수형이다. 레일즈는 모델을 생성하는 생성기를 제공하기 때문에 다음과 같이 명령어를 입력하여 모델을 생성할 수 있다.

```bash
$ rails g model Article title:string text:text
```

위 명령어는 레일즈에게 `Article`이라는 모델을 생성하는데 해당 모델은 String 값인 `title`과 text 값인 `text`를 인자로 받는다고 알려준다. 이 인자들은 `articles` 데이터베이스의 테이블에 자동으로 추가되고 `Article` 모델과 연동된다.

여기서 우리가 주목해야할 파일은 `app/modes/article.rb`와 `db/migrate/20201121073315_create_articles.rb`다.



#### 마이그레이션

방금 확인했듯이 `rails generate model` 명령어는 `db/migrate` 폴더에 `database migration` 파일을 작성한다. 마이그레이션은 데이터베이스의 테이블을 생성하거나 변경하도록 디자인된 루비 클래스들을 가리킨다. 레일즈는 rake 명령어를 통해 마이그레이션을 시키거나 마이그레이션된 데이터베이스를 롤백시킬 수도 있다. 마이그레이션 파일명은 타임스탬프를 가지므로 마이그레이션 파일들의 생성 순서를 알 수 있다.

`db/migrate/YYYYMMDDHHMMSS_create_articles.rb` 파일을 확인해보자.

```ruby
class CreateArticles < ActiveRecord::Migration[6.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text

      t.timestamps
    end
  end
end
```

먼저 마이그레이션은 `change`라는 메서드를 가지는데, 이 메서드는 마이그레이션 작업 과정에서 호출된다. 이 메서드는 레일즈가 롤백 시에도 어떻게 롤백을 해야할지 알려주는 역할을 한다. 마이그레이션 커맨드를 실행시키면 데이터베이스에 `articles`라는 테이블이 생기고, 여기에는 String 컬럼 1개와 Text 컬럼 1개가 생성된다.

```bash
$ rails db:migrate
```

다음과 같이 마이그레이트 명령이 실행되면 데이터베이스에 모델이 반영된 것이다.

```bash
== 20201121073315 CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0049s
== 20201121073315 CreateArticles: migrated (0.0050s) ==========================
```

단, 현재는 개발환경에서 작성한 것이므로 이 명령어는 `config/database.yml`의 `development` 섹션에 정의된 데이터베이스에 적용된다. 배포용으로 마이그레이션을 할 때는 다음과 같이 입력해야한다.

```bash
$ rails db:migrate RAILS_ENV=production
```



#### 컨트롤러를 통한 데이터 저장

다시 `ArticlesController`로 돌아가서 `create` 동작에 새로운 `Article` 모델 객체를 만들어 데이터베이스에 저장해보자.

```ruby
def create
  @article = Article.new(params[:article])
    
  @article.save
  redirect_to @article
end
```

`@article = Article.new(params[:article])`은 Article 모델 객체를 새로 생성하여 저장하는 것이고, `@article.save`는 생성된 객체를 데이터베이스에 저장한다. 마지막으로 `redirect_to @article`은 생성된 객체를 보여주는 부분으로 아직 `show`를 정의하지 않아 작동하지 않는다.

이제 Article 객체를 생성해보자. 제출 버튼을 누르면 ActiveModel::ForbiddenAttributesError가 발생한다.

레일즈는 애플리케이션을 안전하게 사용하기 위한 다양한 보안을 지원한다. 그리고 지금 만난 것이 그 중 하나인 `strong parameters`로, 컨트롤러의 동작에 사용되는 파라미터들은 정확히 정의해줘야한다는 것이다.

만약, 모든 컨트롤러에서 해당 파라미터로 하나의 모델에 접근할 수 있다면 꽤나 편리할 것이다. 하지만, 이러한 편리함 때문에 기능을 오용할 수도 있기 때문에 위험하다.

이런 일을 방지하기 위해서 레일즈에서는 `strong parameters`가 정의되어 있는데, 이 경우에는 `title`과 `text` 파라미터를 `create`에 확실하게 정의해줘야한다. 이를 위해서 다음과 같이 `require`와 `permit`을 사용해보자.

```ruby
@article = Article.new(params.require(:article).permit(:title, :text))
```

이 때, 파라미터들은 `create` 뿐만 아니라 `update`에서도 사용할 수 있으므로 다음과 같이 객체로서 저장해둔다면 다른 동작들에 대해서도 동일하게 사용할 수 있을 것이다. 단, 이 경우에는 `private`를 선언하여 외부에서 안의 값들을 불러올 수 없게 만들어야한다.

```ruby
private
  def article_params
    params.require(:article).permit(:title, :text)
  end

def create
  @article = Article.new(article_params)
  
  @article.save
  redirect_to @article
end
```



#### Article 보여주기

이제 제출 버튼을 눌러보면 레일즈는 `show`가 정의되지 않았다고 불평할 것이다. `rails routes`를 보면 `show`는 다음과 같이 정의되어 있다.

```
article GET /articles/:id(.:format) article#show
```

다시 컨트롤러 파일로 돌아가서 `show` 동작을 정의해보자.

```
컨트롤러에서 자주 사용되는 CRUD 동작 명령어는 다음과 같이 정의합니다.
index, show, new, edit, create, update, destory (public methods)
자신만의 동작 명령어를 사용해도 좋지만, 그 경우에는 컨트롤러 내에서 private로 선언해야합니다.
```

```ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
  end
  
  def new
  end
```

`Article.find`는 입력된 파라미터 값으로 데이터를 찾으며, 이 떄 데이터를 인스턴스 변수(`@article`)에 저장했다. 여기서 정의한 인스턴스 변수는 뷰에 전달되므로 뷰 파일(`app/views/articles/show.html.erb`)을 다음과 같이 작성한다.

```erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
 
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```



#### 리스트

`rails routes`에서 `index`는 다음과 같이 정의되어 있다.

```
articles GET /articles(.:format) articles#index
```

`ArticlesController`에 `index` 동작을 정의하자.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
```

마지막으로 `index`의 뷰에 Article 리스트를 작성한다.

```erb
<h1>Listing Articles</h1>
 
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
  </tr>
 
  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```



#### 링크 걸기

이제 `create`와 `show`에 익숙해졌으니 링크를 걸어보자. `app/views/welcome/index.html.erb`를 다음과 같이 변경해보자.

```erb
<h1>Hello, Rails!</h1>
<%= link_to 'My Blog', controller: 'articles' %>
<%= link_to 'New Article', new_article_path %>
```

`link_to`는 레일즈의 내장 뷰 헬퍼 메서드로 하이퍼링크를 걸어준다.

```erb
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
  ...
<% end %>
 
<%= link_to 'Back', articles_path %>
```

```erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
 
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
 
<%= link_to 'Back', articles_path %>
```

```
만약 같은 컨트롤러 내에서 이동한다면 :controller 설정을 추가할 필요가 없다. 레일즈는 현재 사용중인 컨트롤러를 기본값으로 사용하기 때문이다.
```



#### 제약 추가

Article 모델 파일을 살펴보자.

```ruby
class Article < ApplicationRecord
end
```

이 파일에 작성된 것은 없지만, Article 모델이 ApplicationRecord를 상속받는다는 사실을 잊지말자. 또한, ApplicationRecord는 CRUD를 포함한 다양한 기능을 제공하는 `ActiveRecord::Base`를 상속받는다.

레일즈는 데이터를 제약하여 모델로 보내주는 메서드를 제공한다. `app/models/article.rb` 파일을 작성해보자.

```ruby
class Article < ApplicationRecord
  validates :title, presence: true
                    length: { minimum: 5}
end
```

위 코드에서 제약 대상은 `title`이며, 길이를 최소 5개 이상 입력할 것을 조건으로 걸었다. 레일즈는 모델에 대해 다양한 제약사항을 걸 수 있는데 관련 내용은 `Active Record Validation` 문서를 참고하자.

제약사항을 걸었으므로 `@article.save`가 실행될 때 제약조건을 만족하지 못하는 인스턴스에 대해서는 `false`를 반환한다. 제약사항이 정확히 동작하는지 확인하기 위해 `create` 동작 코드를 다음과 같이 변경해보자.

```ruby
def create
  @article = Article.new(article_params)
 
  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end
 
private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

`@article.save`가 제약사항에 따라 진리값(true/false)을 반환하므로 조건문에 사용이 가능하다. 이제 제약조건을 만족하면 해당 Article로 이동하게되고, 만족하지 못했을 경우 `articles/new`의 뷰에 해당하는 `app/views/new.html.erb` 템플릿 파일이 렌더링된다.

```erb
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
 
  <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
          <li><%= msg %></li>
        <% end %>
      </ul>
    </div>
  <% end %>
 
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
 
<% end %>
 
<%= link_to 'Back', articles_path %>
```

`@articles.errors.any?` 메서드는 에러가 발생했는지 체크한다. 그리고 에러가 발생했을 경우에는 `@article.errors.full_message`로 에러 메세지 리스트를 출력한다.

`pluralize`는 레일즈의 헬퍼로 인자의 개수가 1개 이상이라면 이를 복수화해준다.

```ruby
def new
  @article = Article.new
end
```

이제 `new` 동작에 `@article = Article.new`를 추가해준다. 이를 정의해주지 않으면 `@article`은 `nil`을 가지게 되며, 이는 `@article.errors.any?`를 통해 에러를 반환한다.



#### 업데이트

CRUD 중에서 CR 기능을 구현하였으니 나머지 UD 기능을 구현해보자.

먼저 U에 해당하는 Update 기능이다. Update 기능을 구현하기에 앞서 Controller의 `edit` 동작을 작성하자.

```ruby
def edit
  @article = Article.find(params[:id])
end
```

```erb
<h1>Edit Article</h1>
 
<%= form_with(model: @article, local: true) do |form| %>
 
  <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
          <li><%= msg %></li>
        <% end %>
      </ul>
    </div>
  <% end %>
 
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
 
<% end %>
 
<%= link_to 'Back', articles_path %>
```

이제 `edit` 페이지가 완성됐으니 `update` 동작을 정의해주자. `form_with` 메서드에 Article 객체를 보내면 레일즈는 자동으로 변경된 Article을 보내기위한 URL을 설정해준다. 이 옵션은 레일즈에게 HTTP 메서드 중 `PATCH`로 자원의 업데이트를 위한 REST protocol에 해당한다.

또한, `form_with` 메서드에 모델 객체를 `model: @article`로 전달해주었는데, 전달된 모델의 인스턴스 내에 있는 데이터들을 상응하는 객체에 전달하도록 폼 헬퍼를 도와주는 역할을 한다.

이는 앞에서 `create`에서 사용한 `scope: :article`에서 Article 모델에 해당하는 빈 폼 객체를 생성해주는 역할과는 다르다.

이제 `update` 동작을 `ArticlesController`에 추가해보자.

```ruby
def update
  @article = Article.find(params[:id])
 
  if @article.update(article_params)
    redirect_to @article
  else
    render 'edit'
  end
end
```

`update` 메서드는 이미 존재하는 인스턴스 객체의 값을 업데이트해줄 떄 사용한다. 파라미터로는 `create`에서 사용한 article_params를 사용한다. 만약 파라미터의 값을 직접 지정해주었다면(`@article.update(title: 'A new title')`) 지정해 준 파라미터의 값만 변경되고 나머지 값은 그대로 유지된다.