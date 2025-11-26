# SIMULATION-OF-FREQUENCY-DIVISION-MULTIPLEXING-FDM-AND-DEMULTIPLEXING-USING-SCILAB


### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.  

### EQUIPMENTS Needed

Computer with Scilab installed  

### ALGORITHM

1.Define six different frequencies to generate six sine wave signals.  
2.Generate the time vector to represent time samples.  
3.Compute six sine signals for each frequency over the time vector.  
4.Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.  
5.Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.  
6.Plot original signals, multiplexed signal, and demultiplexed signals for verification.  

### PROCEDURE
  Refer Algorithms and write code for the experiment.  
  • Open SCILAB in System  
  • Type your code in New Editor  
  • Save the file  
  • Execute the code  
  • If any Error, correct it in code and execute again  
  • Verify the generated waveform using Tabulation and Model Waveform  
  
### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

```
### TABULATION:
<img width="1920" height="1200" alt="Screenshot (77)" src="https://github.com/user-attachments/assets/f65dcc14-dc5e-4238-a380-9af7812c4b63" />
<img width="1920" height="1200" alt="Screenshot (78)" src="https://github.com/user-attachments/assets/c3c61e25-fa4d-4d40-9cfe-9a331f3982a6" />
<img width="1920" height="1200" alt="Screenshot (79)" src="https://github.com/user-attachments/assets/1d439047-9bc1-45d9-8301-b5588265a631" />


### GRAPH:
![WhatsApp Image 2025-11-19 at 15 54 51_ae673cf8](https://github.com/user-attachments/assets/790cf4a9-7608-4f11-abe1-ce8f84619605)





### RESULT:
The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
