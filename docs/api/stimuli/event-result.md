# Event Result

Represents whether this event will change in response to the event listener.  
Has three values:

### ALLOW

Indicates the event should cancel further processing and allow the behavior to occur

### PASS

Nothing is changed, the event should continue processing the next listener

### DENY

Indicates the event should cancel further processing and deny the behavior to occur

---

Returning any of these when listening to an event is what determines the control flow of the event.
