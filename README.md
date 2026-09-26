# Digital Communication System Simulation

This repository contains a Python-based simulation of a complete, end-to-end digital communication system. The project models the transmission of an image through a simulated Additive White Gaussian Noise (AWGN) channel, implementing core digital signal processing techniques from data compression to equalization.

## System Architecture

The simulation pipeline is broken down into the following functional blocks:

*   **Image Pre-processing & Source Coding:** Reads an input grayscale image, divides it into 8x8 blocks, and applies a Discrete Cosine Transform (DCT) to each block. The DCT coefficients are scaled, quantized into 256 levels (8-bit representation), and flattened into a binary bitstream.
*   **Modulation & Pulse Shaping:** The bitstream is mapped using a polar line coding scheme. The system models two different pulse shaping filters: a Half-wave Sine pulse and a Square Root Raised Cosine (SRRC) pulse to control bandwidth and manage Inter-Symbol Interference (ISI).
*   **Channel Modeling:** Simulates an AWGN channel with a specific multi-path impulse response, incorporating zero-padding to match the system's sampling frequency (32 samples/bit). 
*   **Receiver & Matched Filter:** Implements a matched filter at the receiver end to maximize the Signal-to-Noise Ratio (SNR) before symbol detection.
*   **Equalization:** Applies both Zero-Forcing (ZF) and Minimum Mean Square Error (MMSE) equalizers to reverse channel distortion and mitigate ISI.
*   **Reconstruction:** Samples the post-equalization signal at peak eye-diagram openings, applies a 0V decision boundary to detect symbols, and reconstructs the DCT blocks to output the final image.

## Key Findings

*   **Pulse Shaping Trade-offs:** Frequency response and Power Spectral Density (PSD) analysis demonstrated that while Half-Sine pulses offer wide eye-diagram openings with no ISI, they consume significantly more bandwidth than SRRC pulses. 
*   **Equalizer Performance:** Eye diagram visualizations confirm that the ZF filter successfully inverted the channel frequency response to remove ISI, though it is susceptible to noise amplification at frequencies where the channel experiences deep fading.
*   **System Reliability:** The implemented reconstruction algorithm successfully recovered the transmitted image data. Under simulated conditions, the Half-Sine pulse yielded a Bit Error Rate (BER) of 0.619, while the SRRC pulse yielded a BER of 0.503.

## Repository Structure

*   `Digital_Comm_Simulation.ipynb`: The main Jupyter Notebook containing the Python implementation for all communication blocks.
*   `input_transmission_image.jpg`: The original input image used to generate the transmitted bitstream.
*   `Digital_Communication_System_Report.pdf`: Comprehensive academic report detailing the mathematical formulations, impulse/frequency response plots, PSD comparisons, and eye diagrams generated during the simulation.

## Dependencies

The simulation requires a standard scientific Python environment. Key libraries include:
*   `numpy`
*   `scipy.fftpack`
*   `opencv-python` (`cv2`)
*   `scikit-image` (`skimage`)
*   `matplotlib`

