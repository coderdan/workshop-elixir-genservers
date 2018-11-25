## Summary

- Use `handle_call/3` and `GenServer.call/3` to make synchronous calls to a server (have a reply)
- Use `handle_cast/2` and `GenServer.cast/2` to make async calls (no reply)
- Use `init/1` to set any initial state
- Use `start_link/3` with a name to run automatically as part of your application

::TODO: Testing::

::TODO: where do GenServers fit into the Expert360 stack::

## Exercise

Implement a Robot Toy using a `GenServer` that behaves in the following way:

## Later

- Terminate and Stop
- Different replies
- When to use a GenServer and when not to
- Running periodic tasks with GenServer