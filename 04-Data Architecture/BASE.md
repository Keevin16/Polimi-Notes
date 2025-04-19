## Basically Available, Soft state, Eventually consistent

Focuses on **availability** and eventual **consistency**, allowing for **more flexibility** in distributed systems.

Meaning:
- **Basically Available**  
    The system guarantees **availability** even in the presence of partial failures. It may not return the most recent data, but it always gives a response.

- **Soft State**  
    The system state can **change over time** even without input (due to eventual consistency, timeouts, etc.).

- **Eventual Consistency**  
    The system will become **consistent over time**, given that no new updates are made. There’s no guarantee of **immediate** consistency.

#DataArchitecture