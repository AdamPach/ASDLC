# Record

Apply the case that matches the active work item's new state, then update Unrecorded Decisions and Open Threads.

- Implemented and tested → Implemented. Update Tested.
- Accepted (only after the developer confirms) → Done. Clear Tested. Set the next active work item; none left → Active work item: None.
- Developer asks for the next work item while the active work item is not Done → ask whether to accept it; yes → apply Accepted; no → stop.
