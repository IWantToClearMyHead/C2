### Hardware

The first computer is ENIAC, which was invented by J. Presper Eckert and John Mauchly at the University of Pennsylvania :tent: in 1943. 

- Case
- Motherboard
- CPU (Processor)
- GPU (Graphics Card)
- RAM (Memory]
- Storage Device (SSD, NVME SSD, HDD)
- Cooling (FAN, Chassis)
- PSU (Power Supply Unit)
- Display (Monitor, Screen)
- NIC
- Input Devices (Mouse, Keyboard, Camera, Speaker, Fingerprint)
- Bluetooth

### Software

There are many types according to the operation level.

- BIOS
- BL
- OS

### Interaction

We can try some command to see how computer work.

windows should change the language in English first. 
```
chcp 437
```

### CPU type

```
wmic cpu get /format:hform > cpu.html
```

### Memory type

```
wmic memorychip
```


### HDD

```
wmic diskdrive list full /format:hform > dd.html

diskpart

```
