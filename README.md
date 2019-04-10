
# Language Syntax Pragmas - Let's Evolve Ruby by Experiment in a Pragma(tic) Way

pragmas gem / library  - language syntax pragmas - turn on the future today or add your own ideas for easy (re)use for everyone - let's evolve the ruby language together by experimenting in the wild in a pragma(tic) way


* home  :: [github.com/s6ruby/pragmas](https://github.com/s6ruby/pragmas)
* bugs  :: [github.com/s6ruby/pragmas/issues](https://github.com/s6ruby/pragmas/issues)
* gem   :: [rubygems.org/gems/pragmas](https://rubygems.org/gems/pragmas)
* rdoc  :: [rubydoc.info/gems/pragmas](http://rubydoc.info/gems/pragmas)


## What's a Pragma?

Is this a new idea?  No. (Almost) every programming language
has pragma(tic) language flags / directives. See
[Directive (programming)](https://en.wikipedia.org/wiki/Directive_(programming))
@ Wikipedia for more.

What about Ruby today?

Yes, Ruby has (a few built-in) pragmas too in the form of "magic" comment pragmas / directives. With Ruby 2.3 and higher, the following are available:

- `# encoding:` Defaults to `utf-8` but you can use any supported encoding. See (or run) `Encoding.name_list` for all (built-in) encodings.
- `# coding:` A shorthand alias for `# encoding:`.
- `# frozen_string_literal:` Defaults to `false` but you can use `true` or `false`.
  When enabled, Ruby throw errors when (frozen) strings (literals) are changed "in-place".
- `# warn_indent:` Defaults to `false` but you can use `true` or `false`. When
  enabled, and running Ruby with the `-w` option, throws warnings for code that isn't indented by two spaces.

Example:

``` ruby
# encoding:              utf-8
# frozen_string_literal: true
# warn_indent:           true
```

The idea with pragmas is to let everyone (yes, you can) add ideas for easy (re)use for everyone -  
let's evolve the ruby language syntax together
by experimenting in the wild in a pragma(tic).  
Turn on the future today with pragmas.


## Usage

### By Example

To be done




## References

What's a (Language Syntax Preprocessor) Pragma / Directive?  See [Directive (programming)](https://en.wikipedia.org/wiki/Directive_(programming)) @ Wikipedia
on Pragmas in other languages (including C/C++, Ada, Common Lisp, Turbo Pascal,
Perl, Haskell, Python, JavaScript, and more).


## License

![](https://publicdomainworks.github.io/buttons/zero88x31.png)

The `pragmas` scripts are dedicated to the public domain.
Use it as you please with no restrictions whatsoever.


## Questions? Comments?

Send your questions and comments to the ruby-talk mailing list.
Thanks!
