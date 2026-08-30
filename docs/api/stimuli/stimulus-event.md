# Stimulus Event

A Stimulus Event is the base class for any event types in Stimuli. It stores the required listener type and an invoker for all listeners of this event type.

### create(Class&lt;T&gt;, EventInvokerFactory&lt;T&gt;)

---

Creates a new event based on the given class type. An example implementation looks something like:

```java linenums="1"
public interface CustomerSitEvent {
    StimulusEvent<CustomerSitEvent> EVENT = StimulusEvent.create(CustomerSitEvent.class, ctx -> (Customer customer) -> {
        try {
            for (var listener : ctx.getListeners()) {
                listener.onCustomerSit(customer);
            }
        } catch (Throwable t) {
            ctx.handleException(t);
        }
    });
    void onCustomerSit(Customer customer);
}
```

Listeners would then use EVENT to listen to this event.

TODO: document the invoker creation process and its uses
