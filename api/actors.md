# Actors
The Actor library provides support for seamlessly running code within other global states.
`⚠️ WARNING: NOT ALL GAMES CONTAIN ACTORS`
---

# getactorsDDDDD NGIGER
```lua
function getactors(): table<number, Actor>
```
Returns a list of actors that you are able to execute code inside of.

### Example

Iterate through the list of actors and output them to the console.

```lua
for index, actor in getactors() do 
    print(index, actor)
end
```

# run_on_actor
```lua
function run_on_actor(actor: Actor?, script: string, (opt) channel_id: string): ()
```
Runs the code specified inside of that actor's global state.

### Example
Execute a simple Hello World! print script inside of the first actor present. (not all games contain Actors)

```lua
run_on_actor(getactors()[1], 'print("Hello World!")')
```

### Example 2
Transfer a message between the actor global state and your state

```lua
local comm_id, event = create_comm_channel()
event.Event:Connect(function(data)
    print(data) -- -> Hello World!
end)
run_on_actor(getactors()[1], [=[
    local channel = get_comm_channel(...)
    channel:Fire('print("Hello World!"')
]=], comm_id)
```

# create_comm_channel
```
function create_comm_channel(): (string, BindableEvent)
```
Returns a communication id, and a bindable event that can be used for transferring data between the actor global state and your state

### Example

```lua
local comm_id, event = create_comm_channel()
warn(comm_id, event) -- <RandomString>, BindableEvent
```

