# Ruby 정리

## 자료형

- 루비의 모든 자료형은 기본적으로 객체(Object)다.
- 루비에서 사용되는 기본 자료형들은 다음과 같다.
  - string
  - int, float
  - true, false
  - array
  - hash
- 클래스 생성자는 클래스.new다.

- objects.class를 사용하여 객체의 클래스를 알 수 있다.



### String

- 작은 따옴표('')와 큰 따옴표("")로 표현
- String 메서드
  - string.to_i : 숫자를 int로 변형
  - string.to_f : 숫자를 float로 변형
  - string.upcase : 대문자로 변형
  - string.downcase : 소문자로 변형
  - string.capitalize : 매 단어들의 첫 문자를 대문자로 변형
  - string.strip() : 공백 제거
  - string.split() : 공백 또는 값 기준으로 자르기
  - string.include? value : value 값을 포함하는가? (true / false)
  - string[start_index, end_index] : slicing 기능, end_index은 포함 X
  - Interpolation : "#{Value}"



### Number

- int, float
- Number 메서드
  - number.to_s : 숫자를 문자로 변환
  - 사칙연산 중
    - 7 / 3 : int / int 이므로 나머지를 제외한 몫인 2값 리턴
    - 7 / 3.0 : int / float 이므로 전체 값인 2.33333... 값 리턴
  - number.abs() : 절대값 반환
  - number.round() : 숫자를 반올림
  - number.ceil() : 숫자를 올림
  - number.floor : 숫자를 내림
  - Math.sqrt() : 루트 값
  - Math.log() : 로그 값



### Array

- Mutable 객체
- 다른 클래스의 객체가 섞여서 들어갈 수 있음
- Array 메서드
  - array.length() : 배열 길이 반환
  - array.include? value : value 값을 포함하는가? (true / false)
  - array.reverse() : 배열 순서를 역순으로 변환
  - array.sort() : 배열을 오름차순으로 정렬(단, 내부 객체들의 클래스가 같아야함)



### Hash

- Key-Value Pair(Python의 Dictionary와 유사)

  ```ruby
  hash = {
      "key" => "value",
      }
  ```



### Methods

- 메서드 형태

  ```ruby
  def method_name
    # tasks...
  end
  
  method_name
  
  def method_name(variable = default_value)
      # tasks with variable or default_value...
  end
  
  method_name(variable)
  ```

- 기본적으로 마지막 값을 반환

- 특정 지점에서 값을 반환하려면 앞에 return 키워드를 사용



## 기본 메서드

### 출력

- print : 줄 바꿈 X
- puts : 줄 바꿈 O



### 입력

- gets : 줄 바꿈 O
- gets.chomp() : 줄 바꿈 X



## 조건문

### IF

```ruby
if condition
    # tasks...
end

if condition_one and (&&) not (!) condition_two
    # tasks...
end

if condition_one or (||) not (!) condition_two
    # tasks...
end

if condition
    # task...
elsif another condition
    # task...
else
    # task...
end
```



### CASE

```ruby
val = gets.chomp()

case val
when val == value_a
    # task...
when val == value_b
    # task...
else
    # last task...
end
```



## 반복문

### while

```ruby
while condition #condition is true...
    # task...
end
```



### for

```ruby
for element in iterator
    # task...
end
```

```ruby
iterator.each do |element|
  # task...
end
```

```ruby
for i in 0..10 # 1~10
  puts i
end

11.each do |i| # 1~10
  puts i
end

for i in 0...10 # 1~9
  puts i
end
```



## 주석

### Comment

```ruby
# one line

=begin

multiple line

=end
```



## 파일

### Read files

```ruby
File.open("textfile.txt", "r") do |file|
 puts file.read()
 puts file.read().include? "text"
 puts file.readline()
end

File.open("textfile.txt", "r") do |file|
 for line in file.readlines()
   puts line
end
    
file = File.open("textfile.txt", "r")
  puts file.read()
file.close()
```



### Write files

```ruby
File.open("textfile.txt", "a") do |file| # w : overwritten
 file.write("\n Hi, my name is Mr.Park")
end
    
file = File.open("textfile.txt", "w")
  file.write("Something")
file.close()
```



## 에러처리

```ruby
begin # try task...
    
rescue # when error is occured...
    
end
```



## 클래스

```ruby
class Person
  attr_accessor :name, :sex, :age
end

winters = Person.new()
winters.name = "winters"
winters.sex = "male"
winters.age = 28

puts winters.name
```

```ruby
class Person
  attr_accessor :name, :sex, :age
  def initialize(name, sex, age)
    @name = name
    @sex = sex
    @age = age
  end
    
  def show_your_name
    puts @name
  end
end

winters = Person.new("winters", "male", 28)
winters.show_your_name
```



## 상속

```ruby
class Person
    attr_accessor :name, :sex, :age
    def initialize(name, sex, age)
      @name = name
      @sex = sex
      @age = age
    end
      
    def show_your_name
      puts @name
    end
  end
  
  class Student < Person # Student 클래스는 Person 클래스를 상속
    def show_your_name # Method Override
      puts "My name is #{@name} and my age is #{@age}"
    end
  end
  
  winters = Student.new("winters", "male", 28)
  winters.show_your_name
```



## 모듈

```ruby
module Tools
  def sayhi(name)
    puts "Hello, #{name}"
  end
  def saybye(name)
    puts "Good bye, #{name}"
  end
end

include Tools

Tools.saybye("winters")
```

```ruby
# require "파일명"
require_relative "test_module.rb" # require_relative : 상대경로
include Tools

Tools.sayhi("winters")
```

