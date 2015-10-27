# [Coffee](http://coffeescript.org/)

more coffeescript tricks: https://gist.github.com/dfurber/993584

#### iterate
- loop array: `for .. in`
- loop object: `for prop, value of obj`

#### fat arrow in coffeescript 
- read [this](http://webapplog.com/understanding-fat-arrows-in-coffeescript/)
- use => when we need @ to be the object in which method is written; use-> when we need @ to be the object in which method is executed.

#### String with format
```coffee
print = """
  1st line
  2nd line
  #{supports interpolation}
  last line
  """
```

#### Instance method, variables
```coffee
class Songs
  _titles: 0    # instance var, Although it's directly accessible, the leading _ defines it by convention as private property.
  get_count: ->
    @_titles # access instance var
  call_another_method: ->
    return @get_count() # call another instance method
```

#### How to write function as a part of parameter
```coffee
Router.go 'home', -> 
  this.render 'home'
, 
  name: 'h'
  old: 'b'
```

### reverse for loop
coffeescript reverse for loop: `for i in [arr.length-1..0] by -1`
[iterations in coffeescript](http://discontinuously.com/2012/05/iteration-in-coffeescript/)
