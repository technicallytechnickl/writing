---
title: Elixir In Action Summary
layout: post
---


## Module Formatting

defmodule *Application_Name.Module_Name* do

@moduledoc """

	This is the description of the module.
	
	Keep the first paragraph of the documentation concise and simple, typically one-line. Tools like ExDoc use the first line to generate a summary.
	
	Reference modules by their full name.
	
	Markdown uses backticks (`) to quote code. Elixir builds on top of that to automatically generate links when module or function names are referenced. For this reason, always use full module names. If you have a module called MyApp.Hello, always reference it as `MyApp.Hello` and never as `Hello`.
	
	Reference functions by name and arity if they are local, as in `world/1`, or by module, name and arity if pointing to an external module: `MyApp.Hello.world/1`.
	
	Reference a @callback by prepending c:, as in `c:world/1`.
	
	Reference a @type by prepending t:, as in `t:values/0`.
	
	Start new sections with second level Markdown headers ##. First level headers are reserved for module and function names.
	
	Place documentation before the first clause of multi-clause functions. Documentation is always per function and arity and not per clause.
	
	Use the :since key in the documentation metadata to annotate whenever new functions or modules are added to your API.

"""

@doc """
	This can be used per function and can include examples.

	## Examples
		iex> MyApp.Hello.world(:john)
		:ok
"""

@doc """ def(call, expr \\ nil) defines public functions. `\\` defines default value.
def *function_name* do

end

There are also:
- defguard
- defexception
- defdelegate
- defmacro
- defmodule
- defp - adding a `p` makes the definition private


Multi-clause functions can be used with matching:

		`defmodule Geometry do
			def area({:rectangle, a, b}) do
				a * b
			end	
			def area({:square, a}) do
				a * a
			end
			def area({:circle, r}) do
				r * r * 3.14
			end
		end`


## Operators
https://hexdocs.pm/elixir/1.13/operators.html

### Capture Operator
Allows a function (public or private within current module), to be renamed as an anonymous function.

`add = &(&1 + &2)`
`iex> add.(1, 2)`
`3`


## iex

Mix.install [:modbux]

## GenServer

Cheat sheet: https://elixir-lang.org/downloads/cheatsheets/gen-server.pdf 

## Observer

	`Mix.ensure_application!(:wx)
	Mix.ensure_application!(:runtime_tools)
	Mix.ensure_application!(:observer)
	:observer.start()`


