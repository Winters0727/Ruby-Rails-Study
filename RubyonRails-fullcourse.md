# Ruby on Rails - full course

### 시작 전 환경체크

```bash
ruby -v

gem install rails

rails new new_path

rails s(erver)
```

- 레일즈의 기본 포트는 3000이다.



### MVC Pattern

- Model - View - Controller
- Model : Database, 데이터베이스
- View : Web Page, 사용자가 보는 화면
- Controller : Model과 View사이에서 연산작업 담당



### Generator

- 기본 명령 : rails generate
  - rails generate controller 컨트롤러\_이름 뷰\_이름
  - rails generate scaffold 스키마\_이름 컬럼\_이름:자료형...
  - rails generate migration 스키마_이름

```bash
rails g(enerate) controller home index

rails g(enerate) scaffold friends first_name:string last_name:string email:string twitter:string

rails g(enerate) migration friends
```



### Migration

- rails db:migrate



### Routes

- rails routes