# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 
      !pip install scipy matplotlib numpy
      import numpy as np
      import matplotlib.pyplot as plt
      from scipy.io import wavfile
      from scipy.fft import fft, fftfreq, ifft
      
      # Step 1: Load the audio
      fs, data = wavfile.read("dog bark sound.wav")  
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

# OUTPUT: 
<img width="817" height="353" alt="image" src="https://github.com/user-attachments/assets/aa175c0b-7559-4877-b239-e8947934800e" />
<img width="783" height="373" alt="image" src="https://github.com/user-attachments/assets/65f659c7-2505-444a-97e2-9cfd6126afbc" />
<img width="817" height="382" alt="image" src="https://github.com/user-attachments/assets/5db6e291-878c-4566-aa98-a38b0ade4fe0" />


# RESULTS:
Thus the audio signal is analysed using dft.
