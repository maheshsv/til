# Basic Actor in Elixir

> Excerpted from "Seven Concurrency models in Seven Weeks: Actors".

```elixir
defmodule Talker do
  def loop do
    receive do
      {:greet, name} -> IO.puts("Hello #{name}")
      {:praise, name} -> IO.puts("#{name}, you're amazing.")
      {:celebrate, name, age} -> IO.puts("Here's to another #{age} years, #{name}")
      {:shutdown} -> exit(:normal)
    end
    loop
  end
end

Process.flag(:trap_exit, true)
pid = spawn_link(&Talker.loop/0)

send(pid, {:greet, "Harry"})
send(pid, {:praise, "Darwin"})
send(pid, {:celebrate, "Actor", 18})
send(pid, {:shutdown})

receive do
  {:EXIT, ^pid, reason} -> IO.puts("Talker has exited (#{reason})")
end
```
