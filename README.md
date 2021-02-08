# MYO toolbox for Ecole Centrale de Nantes
 
## Requirements 
Missing requirements will be installed as you follow the instructions given below. 
- _Python 3_
- _myo-python_
- _numpy_
- _scikit-learn_
- _scipy_
- _matplotlib_
- _keyboard_
- _pyserial_

## Description

This project contains Python scripts and classes that help to establish connection with Thalmic MYO armband, collect and plot EMG data, and implement a gesture recognition procedure. 

The developers of __Thalmic MYO__ have issued a C++ API that enables the users to create their own applications for the armband. After that, Niklas Rosenstein have developed __myo-python__, a Python interface for this API, using CFFI module and CPython. His implementation can be found here: https://github.com/NiklasRosenstein/myo-python. 

In this project, we build an infrastructure around __myo-python__ library that will help you develop EMG processing and EMG-based gesture recognition.
 
## Installation

### 0. Install Anaconda
If you are not familiar with Python and virtual environments, I suggest using Anaconda. Download a Python 3.7 Anaconda from [the official site](https://www.anaconda.com/products/individual) and install it. Use default installation options.

If you are familiar with virtual environments, create a new one and proceed to step __3__. 

### 1. Install MyoConnect

Download MyoConnect from Thalmic's [official web-site](https://support.getmyo.com/hc/en-us/articles/360018409792). Available for Windows and MacOS, a simple installation.

To set up MyoConnect for work, run it, then right-click on its icon in task bar, select __Preferences__, and uncheck all options in all tabs. Then, right-click on icon again, select __Application Manager__ and uncheck all options here too. 

### 2. Create a new __python 3.8__ virtual environment (explained for Anaconda):

On Windows, open __anaconda prompt__. On MacOS, run __Terminal__. Run the following commands and accept the changes:
```
conda create --name myo python=3.8 pip
```
Now activate the environment that we have just created (its name is __'myo'__):
```
conda activate myo
```
__Note:__ please remember that any time you want to run this project from a new command/terminal window, you need to activate this environment again.

### 3. Install _myo-python_ package

Install it from from our fork on Github. To do so, in command line, with 'myo' environment activated, run:
```
pip install https://github.com/smetanadvorak/myo-python/tarball/master
```
### 4. Setup the _myo-ecn_ package
[Download](https://github.com/smetanadvorak/myo_ecn/tarball/master) this project and put it in an appropriate directory on your disk. 
In command window, navigate to this project's folder and run:
```
pip install -e .
```

## How to run the code
### 1. Set up MyoConnect
This should be done only once at the beginning of your working session:

- Insert MYO's Bluetooth dongle in your USB port.
- Run MyoConnect, right-click on its icon in task bar, select __Armband Manager ...__.
- Approach the dongle with your armband. It should automatically get paired with MyoConnect.
- In MyoConnect, press 'Ping' to make sure that it is not connected to some other armband nearby. Your armband should vibrate in response to the ping.

<p align="center">
  <img width="500" src="docs/ping.png">
</p>

### 2. Setup the environment and run the code
- Open Anaconda Prompt (Windows) or Terminal (MacOS) and activate the 'myo' environment:
```
conda activate myo
```
	
- Navigate to the folder with this package, then to __./examples/streaming__ and run a test script:
```
python streaming.py
```
If everything is installed correctly, a matplotlib figure should appear with the EMG signals being traced in real time. 
This and other examples can be stopped by either pressing __ctrl-c__ (MacOS) or __shift-c__(Windows).

## Working with the examples

### 1. EMG streaming

Script [emg\_streaming.py](/examples/streaming/streaming.py) demonstrates a method to collect and plot EMG data from the armband in a real-time manner. Class [MultichannelPlot](/examples/streaming/MultichannelPlot.py) provides a solution for fast plotting of multichannel signals.

<p align="center">
  <img width="500" src="docs/streaming.png">
</p>

### 2. Acquisition to a file
Script [emg\_streaming.py](/examples/acquisition/acquisition.py) demonstrates a method to collect a specified amount of EMG data from the armband and save it to a file. 
It uses Class [Collector](/myo_ecn/listeners.py). The following command will acquire the signal for 10 seconds and save it to file __filename.csv__:
```python
python acquistion.py 10 filename
```

