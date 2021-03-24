# My preferred Haxe coding style


## Principles

### Simplicity in the code
### Simplicity in the rules


## Specifics

### Vertical whitespace and placement of brackets

```haxe
/**
	Helpers for Baz
**/
class Baz {
	/**
		Do some foo
	**/
	public function foo(a:Int) {
		...
	}

	function bar(b:Float) {
		...
	}
}
```

Both explicit (with curly braces) or implicit (without) blocks can be used with if-else, for and while statements.

```haxe
if (a > 0) {
	...
	return -1;
}
if (b > 0)
	return -1;
```

But don't mix explicit and implicit blocks within the same if-else statement.

```haxe
if (a > 0) {
	...
	return -1;
} else if (b > 0) {
	return 0;
}
```


### Indentation

Indentation is primarily done with tabs; indentation with spaces are only allowed in comments; tabs are 8 spaces wide.

**Switch case** are only indented one level from surrounding code.  In practice, there is no additional indentation between the switch statement and each case expression.

```haxe
switch foo {
case Bar:
	...
case Baz:
	...
}
```

Rationale: semantics.
haxe-formatter: `"indentCaseLabels": false`.

**Compiler conditionals** can be used in many different places.  For simplicity, always keep then aligned with the surrounding code.

```haxe
#if neko
import sys.thread.Lock;
#end

class Compute {

	#if neko
	var lock:Lock;
	function lock() {
		lock.acquire();
	}
	#else
	function lock() {
		// noop
	}
	#end

	function someInlineCode() {
		...
		#if neko
		lock = new Lock();
		#end
		// note: obviously try to avoid this
		...
		if (haxe.macro.Compiler.getDefine("travis") != null) {
			verbose = true;
		}
		// better, when possible (inspired by the Linux kernel coding style);
		// the compiler will optimize this away when appropriate
		...
		if (getCompilerFlag("travis") != null) {
			verbose = true;
		}
		// even better (import haxe.macro.Compiler.getDefine in getCompilerFlag;)
		...
	}

	macro function someMacro(expr:haxe.macro.Expr) {
		switch expr.def {
		#if (haxe >= version("4.0.0"))
		case EBinop(OpIn, _):
		#else
		case EIn(_):
		#end
			return ...
		...
		}
	}
```

Rationale: simplicity.
haxe-formatter: `"conditionalPolicy": "alignedNestedIncrease"` (default).


### Other horizontal whitespace

**Binary operators** should always be surrounded by one space.

```haxe
var d = a * b + c;
```

Rationale: Linux, haxe/std and simplicity.

**The `:` token** follows a special rule.

```haxe
// case a: using : for typing
typedef Baz = {
	a:Float,
	b:Float
}
function foo(a, b:Int, c:Int = 0, d = 0) {
	...
}
var foo:Int = 0;
var bar = (foo:Float);

// case b: using : in struc values
var baz:Baz = {a: 1, b: 2};
```

Rationale: (a) prevent bloat on function declaration and type checks; (b) don't mix with a binary assignment operator.

### Line width and line breaks

### Access modifiers

Should follow the order:

```
[public|private] [static] [override] [dynamic] [inline] [macro] [final] [extern]
```

```haxe
public static inline function foo(a, b:Int, c:Int = 0, d = 0) { ...
static inline function foo(a, b:Int, c:Int = 0, d = 0) { ...
public override function foo(a, b:Int, c:Int = 0, d = 0) { ...
static macro function foo(a, b:Int, c:Int = 0, d = 0) { ...
```

Rationale: there's merit to many orders and this one is reasonable and matches [`haxe.macro.Expr.Access`](https://github.com/HaxeFoundation/haxe/blob/456434674efae188514903163f703d1de33145c2/std/haxe/macro/Expr.hx#L813-L867).

### Comments

Single line comments:

```haxe
// start in lowercase
var foo = 1; // only skip one space
```

Multi-line or documentation comments:

```haxe
/**
	Compute the current value of foo

	Always use Haxe's doc style.
	Indent contents one level to the right.
	Start in upper case.
	Don't end the title with a period.
**/
public function foo() { ...
```

### Imports and static extensions

Separate imports of types from imports of functions and static extensions.  Sort each of those alphabetically.

```haxe
import haxe.macro.Context;
import haxe.macro.Expr;

import haxe.FPHelper.doubleToI64;
using haxe.macro.ExprTools;
```

Use your best judgement when dealing with conditional imports.


## Scratchpad


```haxe
final var foo = "bar";
```

