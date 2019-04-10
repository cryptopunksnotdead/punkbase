
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

To be done




## Frequently Asked Questions (F.A.Q.s) and Answers

**Q: Are Pragmas a new idea?**

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
| `encoding: <encoding_name>` | (or the `coding` shorhand) defaults to `utf-8` but you can use any supported encoding. See (or run) `Encoding.name_list` for all (built-in) encodings. |
| `frozen_string_literal: true\|false` | defaults to `false`. When enabled, Ruby throws errors when (frozen) strings (literals) are changed "in-place". |
| `warn_indent: true\|false` | defaults to `false`. When enabled, and running Ruby with the `-w` option, throws warnings for code that isn't indented by two spaces. |




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
