# Ex: 07 - Simulation of Spread Spectrum Modulation
## AIM:
To simulate the process of Direct Sequence Spread Spectrum (DSSS) modulation using Binary Phase Shift Keying (BPSK).

## SOFTWARE REQUIRED:
Python IDE with numPy and Matplotlib.

## ALGORITHM:
Generate random binary data. Create a PN sequence of length 8. Perform BPSK modulation on the data (0 → -1, 1 → +1).
Spread the BPSK modulated signal using the PN sequence. Modulate the spread signal using a BPSK carrier. Plot the DSSS
spread signal and the BPSK modulated carrier waveform.

## PROGRAM:
```
import numpy as np
import matplotlib.pyplot as plt

#  System Parameters
data_length = 4
chips_per_bit = 8
bit_rate = 1000
carrier_freq = 20000
sample_rate = 160000

chip_rate = bit_rate * chips_per_bit
samples_per_chip = int(sample_rate / chip_rate)

#  Generate Random Data
data = np.random.randint(0,2,data_length)

# Generate PN Sequence
pn_seq = np.random.choice([-1,1], chips_per_bit)

print("Original Data Bits :", data)
print("PN Sequence :", pn_seq)

#  BPSK Mapping
def bpsk_map(bit):
    return 2*bit - 1

#  DSSS Spreading
spread_signal = []

for bit in data:
    bpsk_bit = bpsk_map(bit)
    spread_signal.extend(bpsk_bit * pn_seq)

spread_signal = np.array(spread_signal)

# Carrier Modulation
chip_samples = np.repeat(spread_signal, samples_per_chip)

t = np.arange(len(chip_samples)) / sample_rate

carrier = np.cos(2*np.pi*carrier_freq*t)

bpsk_waveform = chip_samples * carrier

#  PLOTS

plt.figure(figsize=(10,8))


# Spread signal
plt.subplot(2,1,1)
plt.step(range(len(spread_signal)), spread_signal, where='mid')
plt.title("DSSS Spread Signal (Baseband)")
plt.xlabel("Chip Index")
plt.ylabel("Amplitude")
plt.grid()

#BPSK Modulated waveform
plt.subplot(2,1,2)
plt.plot(t,bpsk_waveform)
plt.title("BPSK MODULATED WAVEFORM(carrier)")
plt.xlabel("Time(s)")
plt.ylabel("Amplitude")
plt.grid()
```

## OUTPUT:
<img width="866" height="701" alt="UD1" src="https://github.com/user-attachments/assets/d4f21f90-dbc3-43c7-8866-282178db93a3" />


## RESULT:
Thus, simulated the process of Direct Sequence Spread Spectrum (DSSS) modulation using Binary Phase Shift Keying (BPSK) successfully.
