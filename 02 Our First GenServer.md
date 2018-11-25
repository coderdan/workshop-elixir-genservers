# Our first Genserver

```elixir
mix new scores —sup
```

`start_link`

Start our `GenServer`:

```elixir
{:ok, pid} = GenServer.start_link(Scores, [])
GenServer.call(pid, :hi)
```

Error:

```
** (EXIT from #PID<0.148.0>) shell process exited with reason: an exception was raised:
    ** (RuntimeError) attempted to call GenServer #PID<0.151.0> but no handle_call/3 clause was provided
        (scores) lib/gen_server.ex:605: Scores.handle_call/3
        (stdlib) gen_server.erl:636: :gen_server.try_handle_call/4
        (stdlib) gen_server.erl:665: :gen_server.handle_msg/6
        (stdlib) proc_lib.erl:247: :proc_lib.init_p_do_apply/3
```

`handle_call/3`

```elixir
def handle_call(:hi, _from, state) do
  {:reply, :yo, state}
end
```

`GenServer.call/3`

`GenServer.call(pid, :hi)`

Let’s do something more interesting: A scores app.

```elixir
defmodule Scores do
  def set_score(server, name, score)
  def get_score(server, name)
  def increment_score(server, name)
  def clear_scores(server)
end
```

Make a function to wrap the call to `GenServer`

```elixir
  def set_score(server, name, score) do
    GenServer.call(server, {:set_score, name, score})
  end
```

implement `handle_call/3`

```elixir
  def handle_call({:set_score, name, score}, _from, state) do
    {:reply, :ok, Map.put(state, name, score)}
  end
```

Now you can do:

```elixir
{:ok, pid} = GenServer.start_link(Scores, [])
Scores.set_score(pid, :dan, 100)
```

### Your turn:

Implement the `get_score/2` function:

### Solution:

```elixir
def get_score(server, name) do
  GenServer.call(server, {:get_score, name})
end

def handle_call({:get_score, name}, _from, state) do
  {:reply, Map.get(state, name), state}
end
```