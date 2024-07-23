# Instances lifecycle

"Building an elastic application means that the resources it needs are added or removed dynamically."

The EC2 instance transitions through many states from the moment it is started to the moment it is terminated:
1. Launching: enters a pending state (basically a booting state);
2. Then, it proceeds to a running state. At this point the instance may be rebooted, stopped, stop-hibernating or termination;
3. If it is stopped it must be started again (if needed) which would bring it to a pending state.
4. Termination is another process, in this case the image is stopped and dropped. **If an instance is terminated all data stored in it is lost**.

There is a feature which keeps the image visible for a fixed time after its instance has been terminated.

