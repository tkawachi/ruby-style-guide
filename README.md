# まえがき
# Prelude

> 良いものと素晴らしいものを分けるものがスタイルである。<br/>
> -- Bozhidar Batsov

> Style is what separates the good from the great. <br/>
> -- Bozhidar Batsov

Ruby 開発者として私が常に頭を悩ませるのは、Python 開発者には素晴らしい
プログラミングスタイルリファレンス
([PEP-8](http://www.python.org/dev/peps/pep-0008/))
があるのに、Ruby にはコーディングスタイルとベストプラクティスの公式なガイドが
無いことだ。私はスタイルが意味をもつと信じている。
また、我々、良い Ruby 開発者は、待ち望まれていたこの文章を作りだすことができるとも信じている。

One thing has always bothered me as Ruby developer - Python developers
have a great programming style reference
([PEP-8](http://www.python.org/dev/peps/pep-0008/)) and we never got
an official guide, documenting Ruby coding style and best
practices. And I do believe that style matters. I also believe that
such fine fellows, like us Ruby developers, should be quite capable to
produce this coveted document.

このガイドは会社の内部的な Ruby コーディングガイドラインとして始まった。
ある時点で、私がやっている仕事は一般的な Ruby コミュニティのメンバにとって
興味深いかもしれないし、世間的には別の会社内部ガイドラインは必要ないかもしれない
と思った。しかし、コミュニティドリブンでコミュニティに支持されている
プラクティスの集合、イディオム、スタイルルールによって世間が恩恵をうけることも確かだ。

This guide started its life as our internal company Ruby coding guidelines
(written by yours truly). At some point I decided that the work I was
doing might be interesting to members of the Ruby community in general
and that the world had little need for another internal company
guideline. But the world could certainly benefit from a
community-driven and community-sanctioned set of practices, idioms and
style prescriptions for Ruby programming.

このガイドは、初めから
世界中の優秀な Ruby コミュニティのメンバから多くのフィードバックを受けることが
できた。
全ての提案とサポートに感謝します。
資料を互いに、また全ての Ruby 開発者にも有益にしていきましょう。

Since the inception of the guide I've received a lot of feedback from
members of the exceptional Ruby community around the world. Thanks for
all the suggestions and the support! Together we can make a resource
beneficial to each and every Ruby developer out there.

あなたが Rails に取り組んでいるなら、このガイドの補足である
[Ruby on Rails 3 Style Guide](https://github.com/bbatsov/rails-style-guide)
もチェックするといいかもしれない。

By the way, if you're into Rails you might want to check out the
complementary
[Ruby on Rails 3 Style Guide](https://github.com/bbatsov/rails-style-guide).

## 目次
## Table of Contents

* [Ruby スタイルガイド](#guide)
    * [ソースコードレイアウト](#layout)
    * [文法](#syntax)
    * [名前付け](#naming)
    * [コメント](#comments)
    * [注釈](#annotations)
    * [クラス](#classes)
    * [例外](#exceptions)
    * [コレクション](#collections)
    * [文字列](#strings)
    * [パーセントリテラル](#literals)
    * [その他](#misc)
    * [設計](#design)
* [貢献する](#contributing)
* [広める](#spreadtheword)

* [The Ruby Style Guide](#guide)
    * [Source Code Layout](#layout)
    * [Syntax](#syntax)
    * [Naming](#naming)
    * [Comments](#comments)
    * [Annotations](#annotations)
    * [Classes](#classes)
    * [Exceptions](#exceptions)
    * [Collections](#collections)
    * [Strings](#strings)
    * [Percent Literals](#literals)
    * [Miscellaneous](#misc)
    * [Design](#design)
* [Contributing](#contributing)
* [Spread the word](#spreadtheword)

# Ruby スタイルガイド
# The Ruby Style Guide

Ruby スタイルガイドは、現実世界で他の Ruby プログラマがメンテナンスできる
コードを書けるようにするベストプラクティスを推奨する。
A style guide that reflects real-world usage gets used, and a
style guide that holds to an ideal that has been rejected by the people it is
supposed to help risks not getting used at all &ndash; no matter how good it is.


This Ruby style guide recommends best practices so that real-world Ruby
programmers can write code that can be maintained by other real-world Ruby
programmers. A style guide that reflects real-world usage gets used, and a
style guide that holds to an ideal that has been rejected by the people it is
supposed to help risks not getting used at all &ndash; no matter how good it is.

ガイドは関連するルールによっていくつかのセクションに分かれている。
ルールには根拠を付与するようにトライした。
(省略されている場合は、十分明白だとみなした場合である。)

The guide is separated into several sections of related rules. I've
tried to add the rationale behind the rules (if it's omitted I've
assumed that is pretty obvious).

全てのルールはどこからともない思いつきではない。
プロフェッショナルソフトウェアエンジニアとして広範囲に渡る私のキャリア、
Ruby コミュニティのメンバーからのフィードバックや提案、
["Programming Ruby 1.9"](http://pragprog.com/book/ruby3/programming-ruby-1-9)
や ["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177)
といった重要視されている Ruby プログラミング資料が基礎になっている。

I didn't come up with all the rules out of nowhere - they are mostly
based on my extensive career as a professional software engineer,
feedback and suggestions from members of the Ruby community and
various highly regarded Ruby programming resources, such as
["Programming Ruby 1.9"](http://pragprog.com/book/ruby3/programming-ruby-1-9)
and ["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177).

このガイドはまだ作業中だ - いくつかのルールは例が不足しているし、
明瞭に説明する例を欠いているものもある。
期限内にこれらの問題は解決される予定だ - 今は心に留めておいてほしい。

The guide is still a work in progress - some rules are lacking
examples, some rules don't have examples that illustrate them clearly
enough. In due time these issues will be addressed - just keep them in
mind for now.

[Transmuter](https://github.com/TechnoGate/transmuter)
を使ってこのガイドの PDF や HTML 版を生成できる。

You can generate a PDF or an HTML copy of this guide using
[Transmuter](https://github.com/TechnoGate/transmuter).

<a name="layout">
## ソースコードレイアウト
## Source Code Layout

> 自分以外の全てのスタイルは醜く読めないものであることは、
> ほぼすべての人が知っている。
> 「自分以外の」を除いて、それはきっと正しい… <br/>
> -- Jerry Coffin (on indentation)

> Nearly everybody is convinced that every style but their own is
> ugly and unreadable. Leave out the "but their own" and they're
> probably right... <br/>
> -- Jerry Coffin (on indentation)

* ソースファイルエンコーディングとして `UTF-8` を使うこと
* Use `UTF-8` as the source file encoding.
* インデントには 2 スペースを使うこと
* Use two **spaces** per indentation level.

    ```Ruby
    # good
    def some_method
      do_something
    end

    # bad - four spaces
    def some_method
        do_something
    end
    ```

* Unixスタイルの改行を使うこと (*BSD/Solaris/Linux/OSX ユーザはデフォルトで良い。
  Windows ユーザは注意して。)
    * Git を使っている場合は、Windows の改行が交じってしまうのを避けるために
      以下の設定をしたくなるかもしれない。
* Use Unix-style line endings. (*BSD/Solaris/Linux/OSX users are covered by default,
  Windows users have to be extra careful.)
    * If you're using Git you might want to add the following
    configuration setting to protect your project from Windows line
    endings creeping in:

        ```$ git config --global core.autocrlf true```

* 演算子の両側、コンマ・コロン・セミコロンの後ろ、`{` の両側、`}`の前には
  スペースを置くこと。空白は Ruby インタプリタには(ほぼ)関係ないが、
  適切に使うことが簡単に読めるコードの鍵である。
* Use spaces around operators, after commas, colons and semicolons, around `{`
  and before `}`. Whitespace might be (mostly) irrelevant to the Ruby
  interpreter, but its proper use is the key to writing easily
  readable code.

    ```Ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    [1, 2, 3].each { |e| puts e }
    ```

    唯一の例外は指数演算子を使うときだ。

    The only exception is when using the exponent operator:

    ```Ruby
    # bad
    e = M * c ** 2

    # good
    e = M * c**2
    ```

* `(`, `[` の後、 `]`, `)` の前にはスペースを置かないこと
* No spaces after `(`, `[` or before `]`, `)`.

    ```Ruby
    some(arg).other
    [1, 2, 3].length
    ```

* `when` を `case` と同じ深さにインデントすること。多くの人が賛同しないのは
  知っているが、"The Ruby Programming Language" と "Programming Ruby" の
  両方で確立されたスタイルだ。
* Indent `when` as deep as `case`. I know that many would disagree
  with this one, but it's the style established in both the "The Ruby
  Programming Language" and "Programming Ruby".

    ```Ruby
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end

    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end
    ```

* `def` の間に空行を入れること。またメソッドを論理的段落に分割するために空行を入れること。
* Use empty lines between `def`s and to break up a method into logical
  paragraphs.

    ```Ruby
    def some_method
      data = initialize(options)

      data.manipulate!

      data.result
    end

    def some_method
      result
    end
    ```

* API ドキュメント用に RDoc とその慣習を用いること。
  コメント行と `def` の間に空行を入れないこと。
* Use RDoc and its conventions for API documentation.  Don't put an
  empty line between the comment block and the `def`.
* 1行80文字以内に保つこと。
* Keep lines fewer than 80 characters.
* 行末の空白を避けること。
* Avoid trailing whitespace.

<a name="syntax"/>
## 文法
## Syntax

* 引数があるときは括弧付きの `def` を使うこと。
  メソッドが引数を取らないときは括弧を省略すること。
* Use `def` with parentheses when there are arguments. Omit the
  parentheses when the method doesn't accept any arguments.

     ```Ruby
     def some_method
       # body omitted
     end

     def some_method_with_arguments(arg1, arg2)
       # body omitted
     end
     ```

* 自分が何をしているか正確に分かっていない限り `for` は使わないこと。
  殆どの場合イテレータが代わりに使われるべきだ。
  `for` は `each` にねじりを加えて実装されている -
  `for` は `each` と異なりスコープを導入しないため、ブロック内で定義された
  変数は外から見える。
* Never use `for`, unless you know exactly why. Most of the time iterators
  should be used instead. `for` is implemented in terms of `each` (so
  you're adding a level of indirection), but with a twist - `for`
  doesn't introduce a new scope (unlike `each`) and variables defined
  in its block will be visible outside it.

    ```Ruby
    arr = [1, 2, 3]

    # bad
    for elem in arr do
      puts elem
    end

    # good
    arr.each { |elem| puts elem }
    ```

* 複数行 `if/unless` で `then` を使わないこと
* Never use `then` for multi-line `if/unless`.

    ```Ruby
    # bad
    if some_condition then
      # body omitted
    end

    # good
    if some_condition
      # body omitted
    end
    ```

* `if/then/else/end` より三項演算子(`?:`)の使用が好ましい。
  より一般的に使われており、簡潔である。
* Favor the ternary operator(`?:`) over `if/then/else/end` constructs.
  It's more common and obviously more concise.

    ```Ruby
    # bad
    result = if some_condition then something else something_else end

    # good
    result = some_condition ? something : something_else
    ```

* 三項演算子の分岐先には1つの式しか置かないこと。
  これは三項演算子がネストしてはならないことを意味する。
  そのような場合には `if/else` の使用が好ましい。
* Use one expression per branch in a ternary operator. This
  also means that ternary operators must not be nested. Prefer
  `if/else` constructs in these cases.

    ```Ruby
    # bad
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # good
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* `if x: ...` は使わないこと - Ruby 1.9 で削除される。
  代わりに三項演算子を使うこと。
* Never use `if x: ...` - it is removed in Ruby 1.9. Use
  the ternary operator instead.

    ```Ruby
    # bad
    result = if some_condition: something else something_else end

    # good
    result = some_condition ? something : something_else
    ```

* `if x; ...` は使わないこと。代わりに三項演算子を使うこと。
* Never use `if x; ...`. Use the ternary operator instead.

* 1行 case には `when x then ...` を使うこと。
  `when x: ...` は Ruby 1.9 で削除される。
* Use `when x then ...` for one-line cases. The alternative syntax
  `when x: ...` is removed in Ruby 1.9.

* `when x; ...` は使わないこと。前のルールを参照。
* Never use `when x; ...`. See the previous rule.

* `&&/||` を boolean 式に使い、`and/or` を制御フローに使うこと。
  (親指のルール: 外側の括弧を使わなければならないとしたら、間違った演算子を使っている)
* Use `&&/||` for boolean expressions, `and/or` for control flow.  (Rule
  of thumb: If you have to use outer parentheses, you are using the
  wrong operators.)

    ```Ruby
    # boolean expression
    if some_condition && some_other_condition
      do_something
    end

    # control flow
    document.saved? or document.save!
    ```

* 複数行にわたる `?:` (三項演算子) は避けること。
  代わりに `if/unless` を使う。
* Avoid multi-line `?:` (the ternary operator), use `if/unless` instead.

* Body が 1行の時は `if/unless` 修飾子の使用が好ましい。
  または `and/or` の制御フローでも良い。
* Favor modifier `if/unless` usage when you have a single-line
  body. Another good alternative is the usage of control flow `and/or`.

    ```Ruby
    # bad
    if some_condition
      do_something
    end

    # good
    do_something if some_condition

    # another good option
    some_condition and do_something
    ```

* 否定条件には `if` より `unless` (または `or` 制御フロー)の使用が好ましい
* Favor `unless` over `if` for negative conditions (or control
  flow `or`).

    ```Ruby
    # bad
    do_something if !some_condition

    # good
    do_something unless some_condition

    # another good option
    some_condition or do_something
    ```

* `else` 付き `unless` は使わないこと。肯定ケースを先に書きなおすこと。
* Never use `unless` with `else`. Rewrite these with the positive case first.

    ```Ruby
    # bad
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # good
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* 条件が代入を含まない限り、`if/unless/while` 条件の周りに括弧をつけないこと。
  (`=`のリターン値を使用 を参照)

* Don't use parentheses around the condition of an `if/unless/while`,
  unless the condition contains an assignment (see "Using the return
  value of `=`" below).

    ```Ruby
    # bad
    if (x > 10)
      # body omitted
    end

    # good
    if x > 10
      # body omitted
    end

    # ok
    if (x = self.next_value)
      # body omitted
    end
    ```
* 内部DSL (e.g. Rake, Rails, RSpec) の一部として提供されるメソッドや、
  Ruby で "keyword" 状態のメソッド (e.g. `attr_reader`, `puts`)、
  また属性アクセスメソッドでは括弧を省略すること。
  それ以外の全てのメソッド呼び出しでは括弧を付けること。
* Omit parentheses around parameters for methods that are part of an
  internal DSL (e.g. Rake, Rails, RSpec), methods that are with
  "keyword" status in Ruby (e.g. `attr_reader`, `puts`) and attribute
  access methods. Use parentheses around the arguments of all other
  method invocations.

    ```Ruby
    class Person
      attr_reader :name, :age

      # omitted
    end

    temperance = Person.new('Temperance', 30)
    temperance.name

    puts temperance.age

    x = Math.sin(y)
    array.delete(e)
    ```
* 1行ブロックでは `do...end` より `{...}` が好ましい。
  複数行ブロックに `{...}` を使うのは避けること
  (複数行ブロックからなるのメソッドチェインは間違いなく醜い)。
  "制御フロー" と "メソッド定義" (e.g. Rakefile 内や他の DSL) では常に
  `do...end` を使うこと。
  メソッドチェインには `do...end` を使わないこと。
* Prefer `{...}` over `do...end` for single-line blocks.  Avoid using
  `{...}` for multi-line blocks (multiline chaining is always
  ugly). Always use `do...end` for "control flow" and "method
  definitions" (e.g. in Rakefiles and certain DSLs).  Avoid `do...end`
  when chaining.

    ```Ruby
    names = ["Bozhidar", "Steve", "Sarah"]

    # good
    names.each { |name| puts name }

    # bad
    names.each do |name|
      puts name
    end

    # good
    names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

    # bad
    names.select do |name|
      name.start_with?("S")
    end.map { |name| name.upcase }
    ```

    {...} を使った複数行ブロックからなるメソッドチェインは問題ないという人もいるだろうが、
    自分自身に問いかけて欲しい - 本当にそのコードは読みやすいか、ブロックの内容を
    気の利いたメソッドとして抽出できないだろうか、と。

    Some will argue that multiline chaining would look OK with the use of {...}, but they should
    ask themselves - it this code really readable and can't the blocks contents be extracted into
    nifty methods.

* 不要な箇所での `return` は避けること。
* Avoid `return` where not required.

    ```Ruby
    # bad
    def some_method(some_arr)
      return some_arr.size
    end

    # good
    def some_method(some_arr)
      some_arr.size
    end
    ```
* メソッド引数にデフォルト値を代入するとき、`=` 演算子の周りにスペースを入れること。
* Use spaces around the `=` operator when assigning default values to method parameters:

    ```Ruby
    # bad
    def some_method(arg1=:default, arg2=nil, arg3=[])
      # do something...
    end

    # good
    def some_method(arg1 = :default, arg2 = nil, arg3 = [])
      # do something...
    end
    ```

    前者のスタイルを提案している Ruby 本もあるが、後者のほうが実際にははるかに
    人目を引く。(そして、議論を呼ぶだろうが、少し読みやすい)

    While several Ruby books suggest the first style, the second is much more prominent
    in practice (and arguably a bit more readable).

* 不要な継続行 (\\) は避けること。
  実際には継続行を全く使わないこと。
* Avoid line continuation (\\) where not required. In practice, avoid using
  line continuations at all.

    ```Ruby
    # bad
    result = 1 - \
             2

    # good (but still ugly as hell)
    result = 1 \
             - 2
    ```

* `=` (代入)のリターン値を使用するのは問題ないが、その場合は代入を括弧で囲むこと。
* Using the return value of `=` (an assignment) is ok, but surround the
  assignment with parenthesis.

    ```Ruby
    # good - shows intented use of assignment
    if (v = array.grep(/foo/)) ...

    # bad
    if v = array.grep(/foo/) ...
    
    # also good - shows intended use of assignment and has correct precedence.
    if (v = self.next_value) == "hello" ...
    ```

* 変数の初期化に `||=` は自由に使って良い。
* Use `||=` freely to initialize variables.

    ```Ruby
    # set name to Bozhidar, only if it's nil or false
    name ||= 'Bozhidar'
    ```

* Boolean 変数の初期化に `||=` を使わないこと。
  (現在の値が `false` の時に何が起きるか考えてみて)
* Don't use `||=` to initialize boolean variables. (Consider what
would happen if the current value happened to be `false`.)

    ```Ruby
    # bad - would set enabled to true even if it was false
    enabled ||= true

    # good
    enabled = true if enabled.nil?
    ```

* Perl スタイルの特殊変数 (`$0-9`, `$`` など) を使わないこと。
  大変不可解であり、1行スクリプト以外では非推奨である。
* Avoid using Perl-style special variables (like `$0-9`, `$``,
  etc. ). They are quite cryptic and their use in anything but
  one-liner scripts is discouraged.

* メソッド名と開き括弧の間にはスペースを入れないこと。
* Never put a space between a method name and the opening parenthesis.

    ```Ruby
    # bad
    f (3 + 2) + 1

    # good
    f(3 + 2) + 1
    ```

* メソッドへの最初の引数が開き括弧で始まる場合は、メソッド呼び出しの括弧を必ず付けること。
  例えば `f((3 + 2) + 1)` のように書く。
* If the first argument to a method begins with an open parenthesis,
  always use parentheses in the method invocation. For example, write
`f((3 + 2) + 1)`.

* Ruby インタプリタを常に `-w` オプション付きで実行すること。
  上記ルールのどれかを忘れたら警告してくれるよ!
* Always run the Ruby interpreter with the `-w` option so it will warn
  you if you forget either of the rules above!

<a name="naming"/>
## Naming

> The only real difficulties in programming are cache invalidation and
> naming things. <br/>
> -- Phil Karlton

* Use `snake_case` for methods and variables.
* Use `CamelCase` for classes and modules.  (Keep acronyms like HTTP,
  RFC, XML uppercase.)
* Use `SCREAMING_SNAKE_CASE` for other constants.
* The names of predicate methods (methods that return a boolean value)
  should end in a question mark.
  (i.e. `Array#empty?`).
* The names of potentially "dangerous" methods (i.e. methods that modify `self` or the
  arguments, `exit!`, etc.) should end with an exclamation mark.
* When using `inject` with short blocks, name the arguments `|a, e|`
  (accumulator, element).
* When defining binary operators, name the argument `other`.

    ```Ruby
    def +(other)
      # body omitted
    end
    ```

* Prefer `map` over *collect*, `find` over *detect*, `select` over
  *find_all*, `size` over *length*. This is not a hard requirement; if the
  use of the alias enhances readability, it's ok to use it.

<a name="comments"/>
## Comments

> Good code is its own best documentation. As you're about to add a
> comment, ask yourself, "How can I improve the code so that this
> comment isn't needed?" Improve the code and then document it to make
> it even clearer. <br/>
> -- Steve McConnell

* Write self-documenting code and ignore the rest of this section. Seriously!
* Comments longer than a word are capitalized and use punctuation. Use [one
  space](http://en.wikipedia.org/wiki/Sentence_spacing) after periods.
* Avoid superfluous comments.

    ```Ruby
    # bad
    counter += 1 # increments counter by one
    ```

* Keep existing comments up-to-date. No comment is better than an outdated
  comment.
* Avoid writing comments to explain bad code. Refactor the code to
  make it self-explanatory. (Do or do not - there is no try.)

<a name="annotations"/>
## Annotations

* Annotations should usually be written on the line immediately above
  the relevant code.
* The annotation keyword is followed by a colon and a space, then a note
  describing the problem.
* If multiple lines are required to describe the problem, subsequent
  lines should be indented two spaces after the `#`.

    ```Ruby
    def bar
      # FIXME: This has crashed occasionally since v3.2.1. It may
      #   be related to the BarBazUtil upgrade.
      baz(:quux)
    end
    ```

* In cases where the problem is so obvious that any documentation would
  be redundant, annotations may be left at the end of the offending line
  with no note. This usage should be the exception and not the rule.

    ```Ruby
    def bar
      sleep 100 # OPTIMIZE
    end
    ```

* Use `TODO` to note missing features or functionality that should be
  added at a later date.
* Use `FIXME` to note broken code that needs to be fixed.
* Use `OPTIMIZE` to note slow or inefficient code that may cause
  performance problems.
* Use `HACK` to note code smells where questionable coding practices
  were used and should be refactored away.
* Use `REVIEW` to note anything that should be looked at to confirm it
  is working as intended. For example: `REVIEW: Are we sure this is how the
  client does X currently?`
* Use other custom annotation keywords if it feels appropriate, but be
  sure to document them in your project's `README` or similar.

<a name="classes"/>
## Classes

* Always supply a proper `to_s` method.

    ```Ruby
    class Person
      attr_reader :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end

      def to_s
        "#@first_name #@last_name"
      end
    end
    ```

* Use the `attr` family of functions to define trivial accessors or
  mutators.
* Consider adding factory methods to provide additional sensible ways
  to create instances of a particular class.
* Prefer duck-typing over inheritance.
* Avoid the usage of class (`@@`) variables due to their "nasty" behavior
  in inheritance.
* Assign proper visibility levels to methods (`private`, `protected`)
in accordance with their intended usage. Don't go off leaving
everything `public` (which is the default). After all we're coding
in *Ruby* now, not in *Python*.
* Indent the `public`, `protected`, and `private` methods as much the
  method definitions they apply to. Leave one blank line above them.

    ```Ruby
    class SomeClass
      def public_method
        # ...
      end

      private
      def private_method
        # ...
      end
    end

* Use `def self.method` to define singleton methods. This makes the methods
  more resistant to refactoring changes.

    ```Ruby
    class TestClass
      # bad
      def TestClass.some_method
        # body omitted
      end

      # good
      def self.some_other_method
        # body omitted
      end

      # Also possible and convenient when you
      # have to define many singleton methods.
      class << self
        def first_method
          # body omitted
        end

        def second_method_etc
          # body omitted
        end
      end
    end
    ```

<a name="exceptions"/>
## Exceptions

* Don't suppress exceptions.
* Don't use exceptions for flow of control.
* Avoid rescuing the `Exception` class.

<a name="collections"/>
## Collections

* It's ok to use arrays as sets for a small number of elements.
* Prefer `%w` to the literal array syntax when you need an array of
strings.
* Avoid the creation of huge gaps in arrays.
* Use `Set` instead of `Array` when dealing with lots of elements.
* Use symbols instead of strings as hash keys.
* Avoid the use of mutable object as hash keys.
* Use the new 1.9 literal hash syntax in preference to the hashrocket syntax.
* Rely on the fact that hashes in 1.9 are ordered.
* Never modify a collection while traversing it.

<a name="strings"/>
## Strings

* Prefer string interpolation instead of string concatenation:

    ```Ruby
    # bad
    email_with_name = user.name + ' <' + user.email + '>'

    # good
    email_with_name = "#{user.name} <#{user.email}>"
    ```

* Prefer single-quoted strings when you don't need string interpolation or
  special symbols such as `\t`, `\n`, `'`, etc.

    ```Ruby
    # bad
    name = "Bozhidar"

    # good
    name = 'Bozhidar'
    ```

* Don't use `{}` around instance variables being interpolated into a
  string.

    ```Ruby
    class Person
      attr_reader :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end

      # bad
      def to_s
        "#{@first_name} #{@last_name}"
      end

      # good
      def to_s
        "#@first_name #@last_name"
      end
    end
    ```

* Avoid using `String#+` when you need to construct large data chunks.
  Instead, use `String#<<`. Concatenation mutates the string instance in-place
  and is always faster than `String#+`, which creates a bunch of new string objects.

    ```Ruby
    # good and also fast
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

<a name="literals"/>
## Percent Literals

* Use `%w` freely.

    ```Ruby
    STATES = %w(draft open closed)
    ```

* Use `%()` for single-line strings which require both interpolation
  and embedded double-quotes. For multi-line strings, prefer heredocs.

    ```Ruby
    # bad (no interpolation needed)
    %(<div class="text">Some text</div>)
    # should be '<div class="text">Some text</div>'

    # bad (no double-quotes)
    %(This is #{quality} style)
    # should be "This is #{quality} style"

    # bad (multiple lines)
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # should be a heredoc.

    # good (requires interpolation, has quotes, single line)
    %(<tr><td class="name">#{name}</td>)
    ```

* Use `%r` only for regular expressions matching *more than* one '/' character.

    ```Ruby
    # bad
    %r(\s+)

    # still bad
    %r(^/(.*)$)
    # should be /^\/(.*)$/

    # good
    %r(^/blog/2011/(.*)$)
    ```

* Avoid `%q`, `%Q`, `%x`, `%s`, and `%W`.

* Prefer `()` as delimiters for all `%` literals.

<a name="misc"/>
## Misc

* Write `ruby -w` safe code.
* Avoid hashes as optional parameters. Does the method do too much?
* Avoid methods longer than 10 LOC (lines of code). Ideally, most methods will be shorter than
  5 LOC. Empty lines do not contribute to the relevant LOC.
* Avoid parameter lists longer than three or four parameters.
* If you really have to, add "global" methods to Kernel and make them private.
* Use class instance variables instead of global variables.

    ```Ruby
    #bad
    $foo_bar = 1

    #good
    class Foo
      class << self
        attr_accessor :bar
      end
    end

    Foo.bar = 1
    ```

* Avoid `alias` when `alias_method` will do.
* Use `OptionParser` for parsing complex command line options and
  `ruby -s` for trivial command line options.
* Write for Ruby 1.9. Don't use legacy Ruby 1.8 constructs.
    * Use the new JavaScript literal hash syntax.
    * Use the new lambda syntax.
    * Methods like `inject` now accept method names as arguments.

      ```Ruby
      [1, 2, 3].inject(:+)
      ```

* Avoid needless metaprogramming.

<a name="design"/>
## Design

* Code in a functional way, avoiding mutation when that makes sense.
* Do not mutate arguments unless that is the purpose of the method.
* Do not mess around in core classes when writing libraries. (Do not monkey
  patch them.)
* [Do not program
  defensively.](http://www.erlang.se/doc/programming_rules.shtml#HDR11)
* Keep the code simple and subjective. Each method should have a single,
  well-defined responsibility.
* Avoid more than three levels of block nesting.
* Don't overdesign. Overly complex solutions tend to be brittle and hard to
  maintain.
* Don't underdesign. A solution to a problem should be as simple as
  possible, but no simpler than that. Poor initial design can lead to a lot
  of problems in the future.
* Be consistent. In an ideal world, be consistent with these guidelines.
* Use common sense.

<a name="contributing"/>
# Contributing

Nothing written in this guide is set in stone. It's my desire to work
together with everyone interested in Ruby coding style, so that we could
ultimately create a resource that will be beneficial to the entire Ruby
community.

Feel free to open tickets or send pull requests with improvements. Thanks in
advance for your help!

<a name="spreadtheword"/>
# Spread the Word

A community-driven style guide is of little use to a community that
doesn't know about its existence. Tweet about the guide, share it with
your friends and colleagues. Every comment, suggestion or opinion we
get makes the guide just a little bit better. And we want to have the
best possible guide, don't we?
