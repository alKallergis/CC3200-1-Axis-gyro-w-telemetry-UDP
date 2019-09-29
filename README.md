# CC3200-1-Axis-gyro-w-telemetry-UDP
This program receives 2 input servo channels(coming from a RC receiver) and outputs a servo channel controlled by a PD loop.
The timers are 24-bit PWM. TimerA2A is the input signal from the receiver. The timerA2B input determines the gains Kp & Kd of the control system.
When this channel's pulse is bigger than ~1.06ms,the gains are proportional to the pulse width. When it is smaller,the receiver signal(A2A) is
passed straight to the output.
An ITG-3205 gyroscope sensor is interfaced via i2c and set to work @ 1KHZ with a 42HZ LPF.
When the control works,the output channel is the output of a closed loop system where the error is the TimerA2A input signal
converted to degrees/second,minus the gyroscope z axis detected rate which is also in degrees/sec.
With a considered pulse width of 1-2ms and a period 20ms,the conversion is arbitrarily set to -500deg/s for 1ms and 500 deg/s for 2ms.
Note that any inputs and outputs outside the 1-2ms bounds are brought back to bounds.

An ADC is also used with interrupts to calculate an onboard voltage.
This cc3200 also has an AP open where one can connect and receive the UDP packets with the telemetry.The packets
are sent every transmissionPeriodPrescale times a positive edge is detected from the input channel.
