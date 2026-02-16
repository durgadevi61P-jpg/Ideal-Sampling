# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
1.Personal Computer

2.Google Colab
# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs=500
t=np.arange(0,1,1/fs)
m=np.sin(2*np.pi*5*t)

step=int(fs/50)
idx=np.arange(0,len(t),step)
w=int(fs/(2*50))

pulse=np.zeros(len(t)); pulse[idx]=1
ideal=np.zeros(len(t)); ideal[idx]=m[idx]
natural=np.zeros(len(t))
flat=np.zeros(len(t))

for i in idx:
    natural[i:i+w]=m[i:i+w]
    flat[i:i+w]=m[i]

b,a=butter(5,7/(0.5*fs),'low')
rec=filtfilt(b,a,flat)

plt.figure(figsize=(14,14))

plt.subplot(611); plt.plot(t,m); plt.title("Message"); plt.grid(True)
plt.subplot(612); plt.stem(t[idx],np.ones(len(idx)),basefmt=" "); plt.title("Sampling"); plt.grid(True)
plt.subplot(613); plt.stem(t[idx],ideal[idx],basefmt=" "); plt.title("Ideal"); plt.grid(True)
plt.subplot(614); plt.plot(t,natural); plt.title("Natural"); plt.grid(True)
plt.subplot(615); plt.plot(t,flat); plt.title("Flat Top"); plt.grid(True)
plt.subplot(616); plt.plot(t,rec); plt.title("Reconstructed"); plt.grid(True)

plt.tight_layout(); plt.show()
```
# Output Waveform
![WhatsApp Image 2026-02-16 at 3 33 12 PM](https://github.com/user-attachments/assets/caf398a4-651b-4dc8-ad5c-e9d6a8f1f579)



```
# Results
Natural sampling of the given continuous-time signal was successfully performed. The original signal was approximately reconstructed from the natural sampled signal.

