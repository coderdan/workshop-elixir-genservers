# Asynchronous Messages

To send asynchronously we use `handle_cast/2`.

`b GenServer.handle_cast`

We’ll implement `increment_score/2` with `handle_cast/2`

```elixir
  def increment_score(server, name) do
    GenServer.cast(server, {:increment_score, name})
  end

  def handle_cast({:increment_score, name}, state) do
    {:noreply, Map.update(state, name, 1, fn v -> v + 1 end)}
  end
```

```elixir
  def handle_cast({:increment_score, name}, state) do
    {:noreply, Map.update(state, name, 1, &(&1 + 1))}
  end
```

## Your turn:

Implement the `clear_scores/1` function.

### Solution

```elixir
  def clear_scores(server) do
    GenServer.cast(server, :clear_scores)
  end

  def handle_cast(:clear_scores, _state) do
    {:noreply, %{}}
  end
```
