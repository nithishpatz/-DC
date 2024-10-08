~~~
import numpy as np
import matplotlib.pyplot as plt
data = [1, 0, 1, 0, 1, 1, 0, 1] 
bit_duration = 1 
fc = 5 
amplitude = 5 
sampling_rate = 1000
t = np.arange(0, bit_duration * len(data), 1/sampling_rate)
message_signal = np.array([])
for bit in data:
    if bit == 1:
        message_signal = np.concatenate((message_signal, np.ones(sampling_rate)))
    else:
        message_signal = np.concatenate((message_signal, np.zeros(sampling_rate)))
carrier_signal = amplitude * np.sin(2 * np.pi * fc * t)
ask_signal = np.array([])
for bit in data:
    if bit == 1:
        ask_signal = np.concatenate((ask_signal, amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate))))
    else:
        ask_signal = np.concatenate((ask_signal, np.zeros(sampling_rate)))
plt.figure(figsize=(12.0, 8))
plt.subplot(5, 1, 1)
plt.plot(t, message_signal)
plt.title('Message Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.ylim([-0.2, 1.2])
plt.subplot(5, 1, 2)
plt.plot(t, carrier_signal)
plt.title('Carrier Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.subplot(5, 1, 3)
plt.plot(t, ask_signal)
plt.title('ASK Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
fc0=10
fsk_signal = np.array([])

for bit in data:
    if bit == 1:
        fsk_signal = np.concatenate((fsk_signal, amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate))))
    else:
        fsk_signal = np.concatenate((fsk_signal, amplitude * np.sin(2 * np.pi * fc0 * np.arange(0, bit_duration, 1/sampling_rate))))
plt.subplot(5, 1, 4)
plt.plot(t, fsk_signal)
plt.title('FSK Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
psk_signal = np.array([])

for bit in data:
    if bit == 1:
        psk_signal = np.concatenate((psk_signal, amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate))))
    else:
        psk_signal = np.concatenate((psk_signal, amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate) + np.pi)))
plt.subplot(5, 1, 5)
plt.plot(t, psk_signal)
plt.title('PSK Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.tight_layout()
plt.show()
~~~
*output*
![download](https://github.com/user-attachments/assets/e5f5c790-e594-44fc-8c3a-56c1c0d9a9ec)

