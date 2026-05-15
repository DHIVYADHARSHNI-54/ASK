# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
# Program
```
import numpy as np
import matplotlib.pyplot as plt
fs = 1000         
bit_duration = 1   
fc = 5             
data = [1,0,1,1,0,1]   
 
t = np.arange(0, bit_duration, 1/fs)
message = []
 
for bit in data:
   message.extend([bit]*len(t))
 
message = np.array(message)
time = np.arange(0, len(message))/fs
carrier = np.sin(2*np.pi*fc*time)
ask_signal = message * carrier
demodulated = np.abs(ask_signal)
threshold = 0.5
reconstructed = (demodulated > threshold).astype(int)
plt.figure(figsize=(12,8))
 
# Message signal
plt.subplot(4,1,1)
plt.plot(time, message)
plt.title("Message Signal")
plt.ylim(-0.5,1.5)
plt.grid()
 
# Carrier signal
plt.subplot(4,1,2)
plt.plot(time, carrier)
plt.title("Carrier Signal")
plt.grid()
 
# ASK Modulated signal
plt.subplot(4,1,3)
plt.plot(time, ask_signal)
plt.title("ASK Modulated Signal")
plt.grid()
 
# Demodulated signal
plt.subplot(4,1,4)
plt.plot(time, reconstructed)
plt.title("Demodulated (Reconstructed) Signal")
plt.ylim(-0.5,1.5)
plt.grid()
 
plt.tight_layout()
plt.show()
```
# Output Waveform

<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/60e83bec-c94f-4f41-96a1-a34066b719d2" />

# Program:
```

import numpy as np
import matplotlib.pyplot as plt
fs = 1000         
bit_duration = 1
f1 = 8             
f0 = 2             
 
data = [1,0,1,1,0,1]
 
t = np.arange(0, bit_duration, 1/fs)
message = []
 
for bit in data:
   message.extend([bit]*len(t))
 
message = np.array(message)
time = np.arange(0, len(message))/fs
carrier1 = np.sin(2*np.pi*f1*time)   
carrier0 = np.sin(2*np.pi*f0*time)  
fsk_signal = []
 
for bit in data:
   if bit == 1:
       signal = np.sin(2*np.pi*f1*t)
   else:
       signal = np.sin(2*np.pi*f0*t)
   fsk_signal.extend(signal)
 
fsk_signal = np.array(fsk_signal)
demodulated = []
 
samples_per_bit = len(t)
 
for i in range(0, len(fsk_signal), samples_per_bit):
   segment = fsk_signal[i:i+samples_per_bit]
   ref1 = np.sin(2*np.pi*f1*t)
   ref0 = np.sin(2*np.pi*f0*t)
 
   energy1 = np.sum(segment * ref1)
   energy0 = np.sum(segment * ref0)
 
   if energy1 > energy0:
       demodulated.extend([1]*samples_per_bit)
   else:
       demodulated.extend([0]*samples_per_bit)
 
reconstructed = np.array(demodulated)
plt.figure(figsize=(12,8))
 
# Message signal
plt.subplot(4,1,1)
plt.plot(time, message)
plt.title("Message Signal")
plt.ylim(-0.5,1.5)
plt.grid()
 
# Carrier signal
plt.subplot(4,1,2)
plt.plot(time, carrier1)
plt.title("Carrier Signal (Example Frequency)")
plt.grid()
 
# FSK Modulated
plt.subplot(4,1,3)
plt.plot(time, fsk_signal)
plt.title("FSK Modulated Signal")
plt.grid()
 
# Demodulated
plt.subplot(4,1,4)
plt.plot(time, reconstructed)
plt.title("Demodulated (Reconstructed) Signal")
plt.ylim(-0.5,1.5)
plt.grid()
 
plt.tight_layout()
plt.show()
```
# Output waveform:

<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/e0a3a6cb-3e23-4d14-a7e9-fc559beaa5b9" />

# Results

Thus the Ask and Fsk are verified using the colab software successfully.


