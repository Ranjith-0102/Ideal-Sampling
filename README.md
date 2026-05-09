# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Python

Libraries: GOOGLE COLAB,NumPy, Matplotlib, SciPy,
# Algorithm

# Ideal Sampling (Impulse Sampling)

1.Start

2.Define the time range t

3.Generate the original signal x(t) (e.g., sine wave)

4.Choose a sampling frequency fs

5.Calculate sampling interval Ts=1/fs

6.Select discrete sampling points at intervals of Ts

7.Extract signal values at those points

8.Represent samples as impulses (using stem plot)

9.Display the waveform

10.Stop

# Natural Sampling

1.Start

2.Define the time range t

3.Generate the original signal x(t)

4.Choose sampling frequency fs

5.Generate a periodic pulse train

6.Multiply the signal with the pulse train

7.Obtain the naturally sampled signal

8.Plot the waveform

9.Display the result

10.Stop

# Flat-top Sampling (Sample and Hold)

1.Start

2.Define the time range t

3.Generate the original signal x(t)

4.Choose sampling frequency fs

5.Calculate step size based on sampling interval

6.Sample the signal at regular intervals

7.Hold each sampled value constant until the next sample

8.Generate staircase (flat-top) waveform

9.Plot and display the signal

10.Stop

# Program
# Ideal
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Parameters
fs = 100        # Sampling frequency
f = 5           # Signal frequency

# Time vector
t = np.arange(0, 1, 1/fs)

# Continuous signal
x = np.sin(2 * np.pi * f * t)

# Impulse sampling
xs = x

# Reconstruction
xr = resample(xs, len(t))

# Plotting
plt.figure(figsize=(10, 8))

plt.suptitle(
    "NAME : RANJITH KUMAR A\nREG NO : 212224060210",
    fontsize=12,
    fontweight='bold'
)

# Continuous Signal
plt.subplot(3, 1, 1)
plt.plot(t, x)
plt.title("Continuous Signal (fs = 100 Hz)")
plt.grid(True)

# Sampled Signal
plt.subplot(3, 1, 2)
plt.stem(t, xs, basefmt=" ")
plt.title("Sampled Signal (Impulse Sampling)")
plt.grid(True)

# Reconstructed Signal
plt.subplot(3, 1, 3)
plt.plot(t, xr, 'r--')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```
# Natural
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs = 1000       # Sampling frequency
T = 1           # Time duration
fm = 5          # Message signal frequency
fp = 50         # Pulse frequency

# Time vector
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Pulse train
pw = fs // (2 * fp)      # Pulse width
p = np.zeros_like(t)

# Generate impulses
p[::fs // fp] = 1

# Create pulse train
p = np.convolve(p, np.ones(pw), mode='same')

# Natural sampling
nat = m * p

# Reconstruction using Low Pass Filter (LPF)
b, a = butter(4, 10 / (0.5 * fs), 'low')
rec = lfilter(b, a, nat)

# Plotting
plt.figure(figsize=(10, 9))

plt.suptitle(
    "NAME : RANJITH KUMAR A\nREG NO : 212224060210",
    fontsize=12,
    fontweight='bold'
)

# Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.grid(True)

# Pulse Train
plt.subplot(4, 1, 2)
plt.plot(t, p)
plt.title("Pulse Train")
plt.grid(True)

# Natural Sampling
plt.subplot(4, 1, 3)
plt.plot(t, nat)
plt.title("Natural Sampling")
plt.grid(True)

# Reconstructed Signal
plt.subplot(4, 1, 4)
plt.plot(t, rec, color='g')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()

```
# Flat-top
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs = 1000       # Sampling frequency
T = 1           # Time duration
fm = 5          # Message frequency
fp = 50         # Sampling frequency

# Time vector
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Sampling
bd = fs // fp                   # Sampling interval
idx = np.arange(0, len(t), bd)

# Flat-top sampled signal
flat = np.zeros_like(t)

for i in idx:
    flat[i:i + bd // 2] = m[i]

# Low-pass filter for reconstruction
b, a = butter(4, (2 * fm) / (0.5 * fs), 'low')
recon = lfilter(b, a, flat)

# Plotting
plt.figure(figsize=(10, 9))

plt.suptitle(
    "NAME : RANJITH KUMAR A\nREG NO : 212224060210",
    fontsize=12,
    fontweight='bold'
)

# Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.grid(True)

# Sampling Instants
plt.subplot(4, 1, 2)
plt.stem(t[idx], np.ones_like(idx), basefmt="")
plt.title("Sampling Instants")
plt.grid(True)

# Flat-Top Sampled Signal
plt.subplot(4, 1, 3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled Signal")
plt.grid(True)

# Reconstructed Signal
plt.subplot(4, 1, 4)
plt.plot(t, recon, color='g')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```
# Output Waveform

## Ideal Sampling

<img width="989" height="789" alt="DC EP 11" src="https://github.com/user-attachments/assets/93dc84a3-2db5-414a-9a83-c4c75fd7a2fd" />


## Natural Sampling

<img width="981" height="887" alt="DC EP 12" src="https://github.com/user-attachments/assets/a578aaa8-7021-4f43-8656-f9f139fb40bc" />



## Flat-top Sampling

<img width="981" height="887" alt="DC EP 14" src="https://github.com/user-attachments/assets/c33abe88-8c19-4eed-8a7f-97d977bf7de2" />





# Results
The experiment was successfully carried out using Python to generate and analyze ideal, natural, and flat-top sampling techniques.
