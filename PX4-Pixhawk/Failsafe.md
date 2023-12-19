### Magnetometer

The system automatically chooses the best available compass based on their *priority* (external magnetometers have a higher priority than internal magnetometers). If the primary compass fails in-flight, it will failover to the next one. If it fails before flight, arming will be denied.