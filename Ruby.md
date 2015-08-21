# Ruby (todo)

### Links
- Style Guide https://github.com/styleguide/ruby
- Were to find tools/library: https://www.ruby-toolbox.com/

### Debug
- pry + http://cirw.in/blog/pry-to-the-rescue (debug your ruby code live)
- letters: http://lettersrb.com/api

irb: `_` is the last result.

## Variable
global variable
```
$count = 1
```

instance variable, using "@", accessing it by using "self." You don't need to declare it somewhere, just use it.

```
@count
```
Be careful, as you cannot simply declare and use it. It becomes not nil **only** after it's be assigned. (http://stackoverflow.com/questions/826734)

if using "attr_accessor", the variable becomes a C# property. Then we can use it by using "@"
```ruby
attr_accessor :count # note this statement uses symbol ':count', you can also use a string to define an attribute: 
attr_accessor 'count'
# is the same as 
def count; @count; end
def count=(var); @count = var; end
# to use it, @count = something.
```

class(static) variable: @@ (attribute all)
```
@@count
```
    
class(static) method
```ruby
def self.this_is_a_static_method=(value)
#or
def ClassName.this_is_a_static_method
# The above two are the same because in class definition call, self is set to class.
```

# class
By default, variable inside class are **protected**

:count is a symbol.
A Ruby symbol is a thing that has both a number (integer) representation and a string representation.

ruby constructor:
> 
    def initialize(a, b)
        self.a = a
    end

how to new: 
> 
    person = Person.new("a","b")

C# params:
> 
    public string Concat(params String[] items)
->
    def concat(*items)
        result = ""
        items.each do |item|
            result += item
        end
        result
    end

Method can be called without writing parentheses:
> 
    results = method_name parameter1, parameter2           # calling method, not using parentheses

Another technique that Ruby allows is to give a Hash when invoking a function, and that gives you best of all worlds: named parameters, and variable argument length.
> 
    def accepts_hash( var )
        print "got: ", var.inspect # will print out what it received
    end
    accepts_hash :arg1 => 'giving arg1', :argN => 'giving argN'
    # => got: {:argN=>"giving argN", :arg1=>"giving arg1"}
>

You see, the arguments for accepts_hash got rolled up into one hash variable. This technique is heavily used in the Ruby On Rails API.
Use Hash to remove arguments order dependency.
The above lines are equivalent to the more verbose ones:
> 
    accepts_hash( :arg1 => 'giving arg1', :argN => 'giving argN' )  # argument list enclosed in parens
    accepts_hash( { :arg1 => 'giving arg1', :argN => 'giving argN' } ) # hash is explicitly created

how to write **block**?
> 
    items.each { |item| result += item }
    items.each do |item|
        # ...
    end
    C#: public void Each<T>(this IEnumerable<T> list, Action<T> func); item.Each( (s)=> {result+=s;});

block: the `yield` statement actually calls the block
> 
    def do_twice
        yield
        yield
    end
    do_twice {puts 'hola'} # the block will be called twice because of two yields.

convert a block to a Proc: using lambda
block is like a unborn Proc. [source](http://en.wikibooks.org/wiki/Ruby_Programming/Syntax/Method_Calls)
> 
    say = lambda { |something| puts something }

how to patch class?
> 
    class << ThisIsAClassBeingPatched
        def new_method
            puts 'new method'
        end
    end

# scope
!! NOT TURE a block can overrite the variable
> 
    f = 'a'
    ['a', 'b', 'c'].each do |f|
        puts f
    end
    puts f # f is now 'c'

`if` doesn't introduce new scope!
> 
    if k.start_with? "0x"
        value = k.to_i(16)
      else
        value = k.to_i(2
    end
    puts value


# statement

"unless" is a negation of "if"

you can/should put "unless" and "if" at the end of the statement, like English:
- puts "it's valid" if is_valid
- puts "it's not valid" unless is_valid
you can put them together:
- puts "do this if a is true and b is not true" if a unless b

ruby range: 
```ruby
(1..10).each {|num| puts num}
(1..10) does from 1 to 10 (including ends)
(1...10) does from 1 to 9
(1..10).step(2) steps 2 so it is 1, 3, ...
("aaa".."bbb") gets every permutation: "aaa", "aab"...
("aaa".."bbb").to_a.length
```

<< is a concat method, it works with string too:
    a = “b"
    a << "c"

how to do swtich/case?
it is called case..when in Ruby:
```ruby
  case year
    when 1983
        puts "1983"
    when 1982
        puts "1982"
    else
        puts 'anything'
    end
```

===, triple equal, longer rope but sags in the middel, which means it is more flexible than equal. It means included.
>    assert( (1900..1930) === 1918, true)

exception handling:
```ruby
    def pick
        raise ArgumentError, 'this is error'
        rescue ArgumentError
            redo
        end
    end
```

throw exception:
> fail 'message'

yield is used to invoke block
```ruby
    def a_method
        puts 'a'
        yield '1st', '2nd'
        puts 'b'
    end
    a_method { |a, b| puts 'in block, #{a}, #{b}'}
    # outputs: 'a', 'in block 1st 2nd', 'b'
```

Ultimately blocks are really just an implementation of the strategy pattern.


使用最新的lambda字面量语法。
> 
lambda = ->(a, b) { a + b }
lambda.(1, 2)

使用_来表示无用的代码块参数。
> 
result = hash.map { |_, v| v + 1 }

string difference between single quote and double quote:
- single quote: no interpolation: '#{my_name}' => #{my_name}
- single quote: no interpolation so no escaping. '\n' => \n
- "".empty? is true; ni.to_s.empty? is true

nil
- nil.empty? throws exception. You'll have to use nil.nil?
- **only nil and false evaluates false in if statement; everything other object (including 0) evaluates therubygame.

shortcut `p :name` is the same as `puts :name.inspect`

parentheses in Ruby are optional:
> stylesheet_link_tag("application", :media => "all")
is the same as
stylesheet_link_tag "application", :media => "all"

when hash are the last argument, the curly brases are optional
> stylesheet_link_tag "application", { :media => "all" }
is the same as
stylesheet_link_tag "application", :media => "all"

# collection

Array (like C# List)
```ruby
    define: a = [1,2]
    use `%w[]` to make a string array
        `a = %w[foo bar baz quux] => ["foo", "bar", "baz", "quux"] `
    insert: a << 3 (insert method) object a.push(3)
    insert: a.push(3,4,5)
    fetch: last item: a[-1]
    fetch methods: first, last, second
    methods: shuffle, sort, reverse, or use 'bang' method to change itself
    map or collect is like C# Select
    select or find, or reject is like C# Where
    transform array to string:
        colors = ["blue", "red"]
        puts colors.join(',')
```

Enumerable
- condition
    find(return the first), select/find_all(return all)
- transform
    map: `[1, 2, 3, 4].map { |i| i.to_s }` or `[1, 2, 3, 4].map(&:to_s)`

What is Enumerable.inject or reduce?? There is alow a each_with_object method:
- use a memo to combine all elements.
- if using block, pass 'memo' and 'object'
    array.inject({}).{|memo, object| do_something_to_h_using_a; h}
    array.each_with_object({}) {|a, h| do_something_to_h_using_a} # <= h not here

Hash (key value pair)
```ruby
    define: jobs = {}
    `h = Hash.new(0)` the constructor defines a **default** value for all nonexistent key
    jobs["random key"] is nil if no default value is defined, see above line
    jobs["developer"] = "Andrew"
    jobs = { "developer" => "Andrew" } # the keys are strings, the '=>' is called **hashrocket**
    jobs = { :developer => "Andrew", :developer2 => "AZ" } # the keys are symbols
    jobs = { developer: "Andrew", developer2: "AZ" } # the keys become symbol! This is the v1.9 feature, see here: http://logicalfriday.com/2011/06/20/i-dont-like-the-ruby-1-9-hash-syntax/
    The v1.9 feature makes ruby looks more like other language such as JavaScript.
    using symbol: jobs = {} jobs[:Developer] = "Andrew"
    the convension is to put extra space at the two end of a hash
    jobs.each { |key, value| puts "x"}
    fetch method: jobs.fetch(:Developer, "default value")

    used in parameter: the parameter accepts a hash, if nothing is passed, it uses the default value {}
        def print_name(params = {})
```

Set (unordered value with no duplicates, like HashSet in C#)


# ?? Class inheritance
example:
```ruby
    class Employee
        attr_accessor :first_name
        attr_accessor :second_name
    end

    class Manager < Employee
        def vacation_days
            25
        end
    end

    # NOTE this shows duck typing: this class is not even an employee but can be passed to print_days
    class Dancer
        def vacation_days
            40
        end
    end

    def print_days(employee)
        puts "#{employee.vacation_days}"
    end
```

how does Ruby know employee has a vacation_days method? duck typing.

# Metaprogramming
TODO
- read http://stackoverflow.com/questions/10692961/inheriting-class-methods-from-mixins
- http://www.devalot.com/articles/2008/09/ruby-singleton

Ruby class:
- String < Object < BasicObject
- use `superclass` to get its super class

singleton methods: methods defined to a particular object.
>   animal = 'cat'
    def animal.speak
        puts 'miaow'
    end
    animal.speak

`class << foo` opens foo's singleton class (eigenclass).
class << self opens up self's singleton class, so that methods can be redefined for the current self object (which inside a class or module body is the class or module itself). Usually, this is used to define class/module ("static") methods:
> 
class String
  class << self
    def value_of obj
      obj.to_s
    end
  end
end
String.value_of 42   # => "42"

module:
    module Mod
        def meth
            'lala'
        end
    end
    usage:
    Mod.meth
include a module makes module a super class of the target class:
    class Object < BaseClass
    after include module:
    class Object < Module < BaseClass

mixins: include the module then module methods become instance methods.
    class Song
        include Mod
    end
    s = Song.new
    s.meth

How to test a single method from a module?
> 
Module Foo
    def get_file; end
    def self.get_file_can_call_directly; end
end
Class.new.extend(Foo).get_file
Foo.get_file_can_call_directly

How to create a method that creates methods?
The following creates instance methods
> 
def define_methods_for_enviroment(names)
    names.each do |name|
        class_eval <<-EOS
            def #{name}
                data[env]['#{name}']
            end
        EOS
    end
end

`extend` vs `include`
- `extend` will make the methods available to class level: add as class methods
NOTE `a.extend model_b` is different, it'll add instance methods to the object a.
- `inlucde` will add as instance methods


# string

String#split: if passing a empty delimiter, string is splitted as characters if no spaces
> 
'abc'.split => ['a', 'b', 'c']
'ab c'.split => ['ab', 'c']

---

# path
Use `require_relative` to load file
>   require_relative '../lib/cmd'

# regex
Use `match` or `=~` (equals-tilde operator) to match regex;
- `match` returns MatchObject or nil, it returns the 1st match
- `=~` returns matched position number in int or nil
`match` returns MatchData, where the 1st is the entire match string and others are matches.
> 'B0'.match /([A-Z])([0-9])/
=> #<MatchData "B0" 1:"B" 2:"0">

Use `scan` to return all match results.
> str.match[2] reads much nicer than str.scan[0][1].
ruby-1.9.2-p290 :002 > 'a 1-night stay, a 2-night stay'.scan(/(a )?(\d*)[- ]night/i).to_a
 => [["a ", "1"], ["a ", "2"]] 
ruby-1.9.2-p290 :004 > 'a 1-night stay, a 2-night stay'.match(/(a )?(\d*)[- ]night/i).to_a
 => ["a 1-night", "a ", "1"]

---

# How
check null and if not null check other property:
> if user && user.authenticate(params[:session][:password])

assign to a value if it's nil but otherwise leave it alone.
> a = @current_user ||= find_by_id(1)

different return value
> first, *rest = ex.split(/, /)

array slice
> users[2..40]

Use hash and lambda for rules: how rubygem "> 1.3" works (from rubygems::requirement.rb)
> 
    OPS = { #:nodoc:
    "="  =>  lambda { |v, r| v == r },
    "!=" =>  lambda { |v, r| v != r },
    ">"  =>  lambda { |v, r| v > r  },
    "<"  =>  lambda { |v, r| v < r  },
    ">=" =>  lambda { |v, r| v >= r },
    "<=" =>  lambda { |v, r| v <= r },
    "~>" =>  lambda { |v, r| v >= r && v.release < r.bump }
  }
> 
 def satisfied_by? version
    # #28965: syck has a bug with unquoted '=' YAML.loading as YAML::DefaultKey
    requirements.all? { |op, rv| (OPS[op] || OPS["="]).call version, rv }
  end

Use hash to represent rules: how do you implement the rock/scissors/paper rules?
> 
    # this two line provide both rule and the list of possible throws
    @defeat = {rock: :scissors, scissors: :paper, paper: :rock}
    @throws = @defeat.keys
    # rule checking
    user_throw = get_user_throw().to_sym
    computer_throw = @throws.sample
    if computer_throw == @defeat[user_throw]
        puts 'computer win'
    end


#### How to colorize text
'colorize' gem
NOTE on windows you need to manually require 'win32console' when using it, as 'colorize' only checks if RUBY_PLATFORM =~ /win32/ and in some cases RUBY_PLATFORM returns i386-mingw32.
