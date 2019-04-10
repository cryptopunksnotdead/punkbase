
# Language Syntax Pragmas - Let's Evolve Ruby by Experimenting in a Pragma(tic) Way

pragmas gem / library  - language syntax pragmas - turn on the future today or add your own ideas for easy (re)use for everyone - let's evolve the ruby language together by experimenting in the wild in a pragma(tic) way


* home  :: [github.com/s6ruby/pragmas](https://github.com/s6ruby/pragmas)
* bugs  :: [github.com/s6ruby/pragmas/issues](https://github.com/s6ruby/pragmas/issues)
* gem   :: [rubygems.org/gems/pragmas](https://rubygems.org/gems/pragmas)
* rdoc  :: [rubydoc.info/gems/pragmas](http://rubydoc.info/gems/pragmas)



## Usage

The idea with pragmas is to let everyone (yes, you can) add ideas for easy (re)use for everyone -  
let's evolve the ruby language syntax together by experimenting in the wild in a pragma(tic) way.  
Turn on the future today with pragmas.


### By Example

#### Pattern Matcher

Will replace (transform) lines starting with

``` ruby
| None    =>
| Some(x) =>
```

to

``` ruby
None: ->()  
Some: ->(x)
```

Example in the wild:

``` ruby
match Map.find( Current.sender, account_from.allowances ), {
      | None          => { failwith( "Not allowed to spend from", from ) },
      | Some(allowed) => {
        match is_nat(allowed - tokens), {
          | None          => { failwith( "Not enough allowance for transfer", allowed ) },
          | Some(allowed) => {
            if allowed == 0.p
              Map.remove( Current.sender, account_from.allowances )
            else
              Map.add( Current.sender, allowed, account_from.allowances )
            end
          }
        }
      }
    }
```

turns into:

``` ruby
match Map.find( Current.sender, account_from.allowances ), {
      None: ->()        { failwith( "Not allowed to spend from", from ) },
      Some: ->(allowed) {
        match is_nat(allowed - tokens), {
          None: ->() { failwith( "Not enough allowance for transfer", allowed ) },
          Some: ->(allowed) {
            if allowed == 0.p
              Map.remove( Current.sender, account_from.allowances )
            else
              Map.add( Current.sender, allowed, account_from.allowances )
            end
          }
        }
      }
    }
```


#### Enum Type

Will replace (transform) lines starting with enum

``` ruby
enum Color = Red | Green | Blue
enum State = Fundraising | ExpiredRefund | Successful   #or
enum State = Fundraising
           | ExpiredRefund
           | Successful
```

to

``` ruby
enum :Color, :red, :green, :blue
enum :State, :fundraising, :expired_refund, :successful
enum :TravelClass, :first, :business, :economy
```

Note: For type-safe enums in ruby see [`s6ruby/enums` »](<https://github.com/s6ruby/enums>).


#### (Algebraic) Union Data Types (with Variants)

Will replace (transform) lines starting with data

``` ruby
data TravelClass = First | Business | Economy
```

to

``` ruby
data :TravelClass, :First, :Business, :Economy
```

Example in the wild:

``` ruby
ticket = First
cost = TravelClass.match ticket, {
         | First    => { 800 },
         | Business => { 500 },
         | Economy  => { 200 }
       }
}
```

Note: For (algebraic) union data types with (enumerated) variants in ruby see [`s6ruby/safedata` »](<https://github.com/s6ruby/safedata>).



#### Type Type

Will replace (transform) lines starting with type

``` ruby
type Storage =
type Account =
```

to

``` ruby
type :Storage,
type :Account,
```

Example in the wild:

``` ruby
type Account = {
  balance:      Nat,
  allowances:   Map‹Address→Nat› }

type Storage = {
  accounts:     BigMap‹Address→Account›,
  version:      Nat,
  total_supply: Nat,
  decimals:     Nat,
  name:         String,
  symbol:       String,
  owner:        Address }
```

turns into:

``` ruby
type :Account, {
  balance:      Nat,
  allowances:   Map‹Address→Nat› }

type :Storage, {
  accounts:     BigMap‹Address→Account›,
  version:      Nat,
  total_supply: Nat,
  decimals:     Nat,
  name:         String,
  symbol:       String,
  owner:        Address }
```


#### Struct Type

Will replace (transform) lines starting with struct

``` ruby
struct Voter    = 
struct Proposal =
```

to

``` ruby
struct :Voter, 
struct :Proposal,
```

Example in the wild:

``` ruby
struct Voter    = { weight:   0,
                    voted:    false,
                    vote:     0,
                    delegate: Address(0) }

struct Proposal = { vote_count: 0 }
```

turns into:

``` ruby
struct :Voter,    { weight:   0,
                    voted:    false,
                    vote:     0,
                    delegate: Address(0) }

struct :Proposal, { vote_count: 0 }
```


#### Storage / State

Will replace (transform) `@<id>` to `storage[:id]`

``` ruby
@owner
@greeting
```

to

``` ruby
storage[:owner]
storage[:greeting]
```


#### Auto Numbered Arguments / Parameters

Will replace `&<num>` to the upcoming `@<num>`

``` ruby
(1..9).each_slice(3).map { &1 + &2 + &3 }
[{name: 'foo'}, {name: 'bar'}].map { &1[:name] }
```

to

``` ruby
(1..9).each_slice(3).map { @1 + @2 + @3 }
[{name: 'foo'}, {name: 'bar'}].map { @1[:name] }
```


#### Do End-of-Line Block

Will replace `do:` until the end of the line with a `{}` code block

``` ruby
(1..9).each_slice(3).map do: &1 + &2 + &3
[{name: 'foo'}, {name: 'bar'}].map do: &1[:name]
```

to

``` ruby
(1..9).each_slice(3).map { &1 + &2 + &3 }
[{name: 'foo'}, {name: 'bar'}].map { &1[:name] }
```


#### Typed Data Structures

Will replace `<type>‹<value_type>›` with `<type>.define( <value_type> )` or
`<type>‹<key_type>→<value_type>›`  with `<type>.define( <key_type>, <value_type> )`

``` ruby
Array‹Operation›
Hash‹Address→Integer›
```

to

``` ruby
Array.define( Operation )
Hash.define( Address, Integer )
```

Note: For type-safe arrays, hash tables and more in ruby see [`s6ruby/safestruct` »](<https://github.com/s6ruby/safestruct>).



And so on and so forth. What's your idea / pragma?




## Frequently Asked Questions (F.A.Q.s) and Answers

**Q: Are pragmas a new idea?**

A: No. (Almost) every programming language
has pragma(tic) language flags / directives. See
[Directive (programming) @ Wikipedia](https://en.wikipedia.org/wiki/Directive_(programming))
for more.

**Q: What about classic "standard" Ruby today?**

A: Yes, Ruby has (a few built-in) pragmas too in the form of "magic" comment pragmas / directives. Example:

``` ruby
# encoding:              utf-8
# frozen_string_literal: true
# warn_indent:           true
```

With Ruby 2.3 and higher, the following are available:

| Pragma |   Comments   |
|--------|--------------|
| `encoding: <encoding_name>` (defaults to `utf-8`) or use the `coding:` shorhand | Use any supported encoding, see [`Encoding.name_list`](https://ruby-doc.org/core-2.6/Encoding.html#method-c-name_list) for all (built-in) encoding names. |
| `frozen_string_literal: true\|false` (defaults to`false`) | When enabled, Ruby throws errors when (frozen) strings (literals) are changed "in-place". |
| `warn_indent: true\|false` (defaults to `false`) | When enabled, and running Ruby with the `-w` option, throws warnings for code that isn't indented by two spaces. |




## References

What's a (Language Syntax Preprocessor) Pragma / Directive?  See [Directive (programming) @ Wikipedia](https://en.wikipedia.org/wiki/Directive_(programming))
on Pragmas in other languages (including C/C++, Ada, Common Lisp, Turbo Pascal,
Perl, Haskell, Python, JavaScript, and more).


## License

![](https://publicdomainworks.github.io/buttons/zero88x31.png)

The `pragmas` scripts are dedicated to the public domain.
Use it as you please with no restrictions whatsoever.


## Questions? Comments?

Send your questions and comments to the ruby-talk mailing list.
Thanks!
