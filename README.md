# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 
  To analyze audio signal by removing unwanted frequency. 
# APPARATUS REQUIRED: 
   PC installed with SCILAB/Python. 
# PROGRAM: 
```analyze audio signal
from google.colab import files
uploaded = files.upload()   
!pip install scipy matplotlib numpy
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from scipy.fft import fft, fftfreq, ifft

# Step 1: Load the audio
fs, data = wavfile.read("cat-meow-401729.wav")  
if data.ndim > 1:   # if stereo, take one channel
    data = data[:,0]

# Step 2: Plot original waveform
plt.figure(figsize=(10,4))
plt.plot(data)
plt.title("Original Audio Signal")
plt.xlabel("Samples")
plt.ylabel("Amplitude")
plt.show()

# Step 3: Do FFT (DFT)
N = len(data)
yf = fft(data)
xf = fftfreq(N, 1/fs)

plt.figure(figsize=(10,4))
plt.plot(xf[:N//2], np.abs(yf[:N//2]))
plt.title("Frequency Spectrum")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.show()

# Step 4: Remove unwanted frequency (example: remove around 1000 Hz)
filtered = yf.copy()
low, high = 995, 1005   # frequency range to remove
filtered[(xf>low) & (xf<high)] = 0
filtered[(xf<-low) & (xf>-high)] = 0

# Step 5: Inverse FFT to reconstruct signal
cleaned = np.real(ifft(filtered))

# Step 6: Plot cleaned waveform
plt.figure(figsize=(10,4))
plt.plot(cleaned)
plt.title("Filtered Audio Signal")
plt.xlabel("Samples")
plt.ylabel("Amplitude")
plt.show()

# Step 7: Save filtered audio
wavfile.write("cleaned_audio.wav", fs, cleaned.astype(np.int16))
print("Filtered audio saved as cleaned_audio.wav")
```


# OUTPUT: 
<img width="1097" height="488" alt="image" src="https://github.com/user-attachments/assets/d0b37ec0-3d0f-44ef-b879-f0407098df26" />
<img width="1064" height="507" alt="image" src="https://github.com/user-attachments/assets/c6bb4f95-f54b-4da4-b6e4-c896b6b8224a" />
<img width="1109" height="491" alt="image" src="https://github.com/user-attachments/assets/e6630501-292a-44ba-af16-731b635b2e8e" />


# RESULT


   The audio signal was successfully analyzed using DFT, and unwanted frequency components were removed, resulting in a clearer reconstructed signal.



